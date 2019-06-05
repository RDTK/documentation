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
     …

   versions:
     - project₁@version₁
     - project₂@version₂
     …

The following fields are most important:

:samp:`{FILENAME}`

  This is not an actual field but the name of the :term:`recipe file
  <recipe>` with its extension removed (e.g. ``rsb`` for a
  :term:`recipe file <recipe>` named :file:`rsb.distribution`).

  TODO

``variables``

  TODO

``include``

  TODO

``versions``

  A list of :term:`project` names and versions with elements of the
  form

  .. parsed-literal::

     :samp:`{NAME}@{VERSION}`
     :samp:`name: "{NAME}" versions: - {VERSION₁} - {VERSION₂}`

  which should be part the :term:`distribution`. Note that multiple
  versions of a :term:`project` can be specified in one entry but
  multiple entry for the same :term:`project` are not allowed.

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
