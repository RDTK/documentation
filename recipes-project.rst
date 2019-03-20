.. _recipes-project:

=================
 Project Recipes
=================

Project :term:`recipes <recipe>` include some aspects of software
projects:

* Name of the :term:`project`

* :term:`Nature` of the :term:`project` (e.g. `CMake`_, Python
  setuptools, …)

* Repository URL

* Specific build instructions if different from default build
  instructions for the :term:`project's <project>`
  :term:`nature`. Moreover, customizations are possible.

A basic :term:`project` :term:`recipe`, which in this case would be
stored in a file named :file:`rsb-cpp.project`, looks like this:

.. code-block:: json

   {
     "templates": [ "code-cor-lab", "cmake-cpp", "base" ],

     "variables": {
       "description":     "C++ implementation of the robotics service bus (RSB)",
       "keywords":        [ "middleware", "integration", "robotics" ],

       "repository":      "https://code.cor-lab.org/git/rsb.git.cpp",

       "redmine-project": "rsb",

       "cmake.options":   [
         "BUILD_TESTS=OFF",
         "BUILD_EXAMPLES=OFF",
         "@{next-value|[]}"
       ]
     }
   }

The following fields are most important:

:samp:`{FILENAME}`

  This is not an actual field but the name of the :term:`recipe file
  <recipe>` with its extension removed (e.g. ``rsb-cpp`` for a
  :term:`recipe file <recipe>` named :file:`rsb-cpp.project`).

  Must be unique w.r.t. to all other :term:`projects <project>` in the
  repository. Should in general not contain any version information
  (unless particular versions of a project genuinely constitute their
  own :term:`projects <project>`).

``templates``

  TODO A list of :term:`template` names characterizing the technical
  and organizational nature of the project. For most basic purposes,
  it is sufficient to choose a suitable :term:`template` for the build
  system used by the project and the ``base`` :term:`template` to
  inherit specifications for the general nature of build jobs to
  create.

  TODO It is important to note that :term:`templates <template>` first
  mentioned have higher precedence for defining variables then
  :term:`templates <template>` further to the end of the
  list. Therefore, the ``base`` :term:`template` should always be
  listed last so that more specific :term:`templates <template>` can
  override variables defined in the base :term:`template`.

Repository Information
======================

``variables`` » ``scm``

  Kind of the repository from which a copy of the :term:`project` can
  be obtained.

  Only needed if the repository kind cannot be guessed from the value
  of the ``repository`` field.

  Currently supported values: ``git``, ``svn``, ``mercurial``,
  ``archive``.

``variables`` » ``repository``

  URL of the repository from which a copy of the :term:`project` can
  be obtained.

  When omitted, automatic analysis of the project will not be
  performed and the generated Jenkins job will not obtain a copy of
  the project as the first build step.

Project Description
===================

``variables`` » ``natures``

  A list of :term:`natures <nature>` of the :term:`project`, for
  example `CMake`_ project, `Maven`_ project, etc.

  The :term:`nature` of a :term:`project` can guide the analysis of
  the associated repository.

  This information is usually provided by :term:`templates <template>`
  specified in the ``template`` field, but can be overriden, for
  example in "freestyle" projects or other more complicated projects.

``variables`` » ``description``

  A description of the :term:`project` can be multiple lines or even
  paragraphs.

``variables`` » ``keywords``

  A list of keywords characterizing the :term:`project`.

Dependencies
============

.. seealso::

   :ref:`concept-dependencies`
     TODO

There are two ways determining :

Dependency information for a given project can be manually specified
in the fields

``variables`` » ``extra-requires``

  TODO

``variables`` » ``extra-provides``

  TODO
