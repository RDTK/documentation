.. _recipes:

=========
 Recipes
=========

..
   TODO turn this into an overview page with four children:
   recipes-basics, recipes-project recipes-distribution
   recipes-template

.. toctree::
   :hidden:

   recipes/project
   recipes/distribution
   recipes/template

Kinds of recipes:

:ref:`Project Recipes <recipes-project>`

  Descriptions of :term:`projects <project>`

:ref:`Distribution Recipes <recipes-distribution>`

  Descriptions of :term:`distributions <distribution>` which are
  groups of :term:`project` versions that can be built and used
  together.

:ref:`Template Recipes <recipes-template>`

  Descriptions of common :term:`project` kinds including how to build
  and install the respective kinds of :term:`projects <project>`
  depending on the overall development mode.

On the syntactic level, all descriptions are currently based on
`YAML`_.

Variables and the Substitution Sub-Language
===========================================

Objects such as :term:`projects <project>`, :term:`distributions
<distribution>` are basically named entities with a dictionary of
variable names and their values. In `JSON`_, this translates into

.. parsed-literal::

   …

   variables:
     :samp:`"{NAME₁}"`: :samp:`{VALUE₁}`
     :samp:`"{NAME₂}"`: :samp:`{VALUE₂}`
     …

The value part of a variable definition is either a string or a list
of values. A small substitution sub-language, syntactically similar to
"parameter expansion" in UNIX shells, can be used to refer to values
of other variables. To this end we distinguish ``${}`` and ``@{}``
substitution, which act differently on strings and lists.

Some examples of variable definitions

.. code-block:: yaml

   list.a:  [ "abc", "def" ]
   list.b:  [ "123", "456" ]
   list.c:  [ "@{list.a}", "@{list.b}", "uvw", "${text}" ]
   text:    "xyz"

   dashed:  "${list.c}-"
   product: "(${list.a} * ${list.b})"

The basic syntax is as follows:

* Scalar substitution

  :samp:`$\{{NAME}\}`

    Expands to the value of the variable named :samp:`{NAME}`.

    Lists stay lists. However, ultimately a list is flattened into a
    string by concatenating all quoted items with a space used as
    delimiter.

  :samp:`$\{{NAME}|\}` or :samp:`$\{{NAME}|{DEFAULT}\}`

    Expands to the value of the variable named :samp:`{NAME}` if there
    is one and :samp:`{DEFAULT}` otherwise.

  :samp:`$\{next-value|{DEFAULT}\}`

    Expands to the value of the variable being defined in the parent
    scope if there is such a value and :samp:`{DEFAULT}` otherwise. As
    before, :samp:`{DEFAULT}` can be empty or omitted entirely.

* List substitution

  Concatenates the elements of a list into a single string if there is
  surrounding text. Otherwise, i.e. if there is no surrounding text,
  it evaluates to the first element of the list. Obviously, this only
  applies to list variables.

  :samp:`@\{{NAME}\}`

    In string context, expands to the first item of list variable
    :samp:`{NAME}`.

    In list context, expands to the list of items of list variable
    :samp:`{NAME}`, which allows to extend lists this:

    .. code-block:: json

       [ "@{list.a}", "@{list.b|[]}", "new item" ]


  :samp:`{TEXT₁}@{{NAME}}{TEXT₂}`

    Expands to the string concatenated from :samp:`{TEXT₁}`, elements
    of list variable :samp:`{NAME}` and :samp:`{TEXT₂}`.

  :samp:`@\{{NAME}|[]\}`

    Expands to the value of the variable named :samp:`{NAME}` if there
    is one and the empty list of values (as indicated by ``[]``)
    otherwise.

  ``@{next-value|[]}``

    Expands to the value of the variable being defined in the parent
    scope if there is such a value and the empty list (``[]``)
    otherwise. As before, ``[]`` can be omitted.

* Products

  If the evaluation of a variable results in a list, this list is
  "multiplied" with the rest of the value string.

* Examples

  Assuming the following variables are defined (repeated from above):

  .. code-block:: yaml

     list.a:  [ "abc", "def" ]
     list.b:  [ "123", "456" ]
     list.c:  [ "@{list.a}", "@{list.b}", "uvw", "${text}" ]
     text:    "xyz"
     dashed:  "${list.c}-"
     product: "(${list.a} * ${list.b})"

  , the following results would be produced::

    "${list.a}"           => [ "abc", "def" ]
    "@{list.a}"           => "abc"
    "@{list.a} foo"       => "abcdef foo"

    "@{list.a} @{list.b}" => "abcdef 123456"
    "@{list.c|[]} "       => "abcdef123456uvwxyz"

    "${dashed}"           => [ "abc-", "def-", "123-", "456-", "uvw-", "xyz-" ]
    "@{dashed} "          => "abc-def-123-456-uvw-xyz-"

    "${product}"          => [ "(abc * 123)", "(abc * 456)", "(def * 123)", "(def * 456)" ]
    "@{product} "         => "(abc * 123)(abc * 456)(def * 123)(def * 456)"

Like in UNIX shells, substitutions are performed recursively, that is
:samp:`${{${NAME}}}` expands to the value of the variable named by the
value of the variable :samp:`{NAME}`. The same is true for
:samp:`{DEFAULT}`.

Variable Scopes
---------------

TODO Different objects in the description language like projects or
distributions have separate variable sections. However, all these
sections are effectively considered when generating a build job and
thereby resolving to the values of required variables. This resolution
process is determined by the parent-child relation of the different
objects. This relation is as follow (``->`` indicates that the left
side is a parent of the right side)::

  DISTRIBUTION -> PROJECT -> VERSION -> JOB[including template]

TODO When a variable needs to be resolved the resolution process iterates
from the most specific object (e.g. a ``JOB``) to the most general
object until the first definition is found. This definition sets the
variable value. In case this definition contains a ``next-value`` (see
above), the iteration continues on the next level to resolve the
``next-value`` part.

Access and Credentials
======================

:ref:`Project Descriptions <recipes-project>` and :ref:`Distribution
Descriptions <recipes-distribution>` can specify whether the described
:term:`project` or :term:`distribution` is publicly accessible. For a
publicly accessible :term:`project` or :term:`distribution`, the
entire associated source code can be obtained without any
authentication.

Conversely, if project source code has to be obtained from a
repository that requires authentication, the necessary authentication
can be configured.

For access and credentials specification, the following variables are
important:

``variables`` » ``access``

    Specifies access restrictions of the :term:`project` or
    :term:`distribution`. If present, has to have one of the values
    ``private`` and ``public``. Omitting the variable is equivalent to
    ``public``.

``variables`` » ``scm.credentials``

    The value of this variable names an entry in Jenkins' global
    credentials store that should be associated to the repository of
    this project in generated Jenkins jobs.

The following rules apply:

* :term:`Projects <project>` with ``scm.credentials`` entries must
  specify ``private`` ``access``.

* :term:`Distributions <distribution>` with one or more ``private``
  projects must specify ``private`` ``access``.
