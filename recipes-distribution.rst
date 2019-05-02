.. _recipes-distribution:

======================
 Distribution Recipes
======================

TODO introduction see project-recipe

A basic :term:`distribution` description, which in this case would be
stored in a file named :file:`toolkit.distribution`, looks like this:

.. code-block:: yaml

   variables:
     …

   include:
     "distributions": [
     ],
     "projects":      [
     ]

   versions:  [
       {
         "name": "nightly",
         "include": {
           "projects": [
             [ "spread",  "trunk"      ],
             [ "cbf",     "0.1", "0.2" ]
           ]
         }
       }
     ]
   }

The following fields are most important:

:samp:`{FILENAME}`

  This is not an actual field but the name of the :term:`recipe file
  <recipe>` with its extension removed (e.g. ``rsb`` for a
  :term:`recipe file <recipe>` named :file:`rsb.distribution`).

  TODO

``variables``

  TODO

``include`` » ``distributions``

  TODO

``include`` » ``projects``

  A list of :term:`project` names and versions with elements of the
  form

  .. parsed-literal::

     :samp:`[ "{NAME}", "{VERSION₁}", "{VERSION₂}", … ]`

  which should be part the :term:`distribution`. Note that multiple
  versions of a :term:`project` can be specified in one entry but
  multiple entry for the same :term:`project` are not allowed.

``versions``

  A list of version specification declaring existing versions of the
  :term:`distribution`. Like the toplevel dictionary, entries in this
  list can contain ``variables`` and ``include``.

``versions`` » ``name``

  TODO

``versions`` » ``match``

  TODO

  Example:

  .. code-block:: yaml

     versions:
     - pattern: "^(([^-]+)-stable)$"
       variables:
         name: "${match:1}"
         numeric: "${match:2}"

``versions`` » ``match`` » ``pattern``

  TODO

``versions`` » ``match`` » :samp:`{NAME}`

  An entry of the form :samp:`[ "{NAME}", "{VALUE}" ]` causes the
  variable :samp:`{NAME}` to be set to :samp:`{VALUE}`.
  :samp:`{VALUE}` can refer to capture groups created in the regular
  expression in ``versions`` » ``match`` » ``pattern`` via the usual
  :samp:`\\{GROUP-ID}` syntax.

``versions`` » ``variables``

  TODO

``versions`` » ``include`` » ``distributions``

  Like the global ``include`` » ``distributions`` field, but specific
  to a versions. The value can refer to the value of the global
  variable via ``${next-value}``.

  TODO overwriting entries?

``versions`` » ``include`` » ``projects``

  Like the global ``include`` » ``projects`` field, but specific to a
  versions. The value can refer to the value of the global variable
  via ``${next-value}``.

  TODO overwriting entries?
