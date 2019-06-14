.. _recipes-person:

================
 Person Recipes
================

This kind of recipe specifies information about a person involved in
:term:`projects <project>` or :term:`distributions <distribution>`
described in the recipe repository. Being involved may mean appearing
in the ``recipe.maintainer`` variable of a recipe, appearing in a
:term:`project's <project>` version control log or appearing in a
:term:`project's <project>` build system-level metadata. The
information specified in person recipes is mainly used for
documentation and reporting purposes such as generating the |project|
:ref:`web catalog <web-catalog>`.

Person Recipe Syntax
====================

.. code-block:: yaml

   name: Jane Doe

   aliases:
     - jdoe
     - ai_hacker_3117

   identities:
     - mailto:jdoe@employer.example
     - mailto:jane.doe@private-email-address.example

   variables:
     gdpr.opt-in?: true


Important Fields
================

:samp:`{FILENAME}`

  In contrast to other recipe kinds, the filename is not significant
  for person recipes.

``name``

  The "primary" name for the person. This should be the name the
  person wants to be addressed as.

``aliases``

  A list of additional names the person may be addressed as. This can
  be used to associate appearances to a person that have no apparent
  connection. For example, project metadata containing an entry like
  ``<author>ai_hacker_3117</author>`` could not automatically be
  associated with a person whose only name was ``name: Jane Doe``. But
  adding the name to the ``aliases`` section enables the association.

``identities``

  A list of email addresses belonging to a person. As with
  ``aliases``, multiple entries can be used to associate appearances
  with different email addresses with the person entity.

``variables`` » ``gdpr.opt-in?``

  A Boolean indicating whether the person agrees to having their
  information processed in the sense of the EU's `general data
  protection regulation`_.

  When the |project| :ref:`web catalog <web-catalog>` is being
  generated in GDPR-compliance mode, the specified value controls
  whether an entry is created for the person.
