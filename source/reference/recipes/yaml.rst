.. _recipes-yaml:

===================
 YAML Based Syntax
===================

On the syntactic level, all recipes are currently based on
YAML_. Since YAML is a superset of JSON_, descriptions can also be
written using JSON syntax.

Useful features and caveats of the YAML syntax:

* For shell scripts and fragments of shell code, literal style scalar
  nodes can be useful:

  .. code-block:: yaml

     command: |
       if [ -r "\${file}" ] ; then
         frob "\${file}" 'foo bar' \
         && fez
       fi

  Note how double quotes (``"``), single quotes (``'``) and
  backslashes (``\``) can be used freely without escaping while
  ``\${…}`` is needed to prevent the :program:`build-generator` from
  applying its variable substitution. The ``|`` on the previous line
  indicates that the value should be taken literally which means
  whitespace and newlines are kept without modification. Any common
  whitespace (that is preceding all lines of the value) is
  stripped. Thus, the above example would be processed as a string
  consisting of the following four lines::

    if [ -r "\${file}" ] ; then
      frob "\${file}" 'foo bar' \
      && fez
    fi

* Due to the fact that YAML does not generally require delimiters
  around strings, a little bit of care has to be taken when specifying
  versions. The potential problem is that something like ``master`` is
  parsed as a string while something like ``1.0`` is parsed as a
  floating point number by default. For this reason, certain version
  numbers have to be specified as ``"``- or ``'``-delimited strings:

  .. code-block:: yaml

     no-problem:       master
     still-no-problem: 1.0.0
     bad:              1.0
     good:             '1.0'

* As an extension to core YAML syntax, recipes can include other YAML
  documents as well as text files:

  * A tagged scalar node of the form :samp:`!b!include {FILENAME}`
    causes :samp:`{FILENAME}` to be loaded as a YAML file and spliced
    into the current recipe, replacing the tagged scalar
    node. Example:

    .. code-block:: yaml

       packages:
         !b!include package-list.yaml

  * A tagged scalar node of the form :samp:`!b!literal-include {FILENAME}`
    causes :samp:`{FILENAME}` to be read as a string and spliced into
    the current recipe, replacing the tagged scalar node. Example:

    .. code-block:: yaml

       patch: !b!literal-include patches/foo.diff

       command: |

         cat <<'EOF' | patch -l p1

         ${patch}

         EOF
