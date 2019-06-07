.. _recipes-template:

===========
 Templates
===========

Templates describe generic properties for certain recurring aspects of
:term:`projects <project>`. These could be build system instructions
or common settings for redmine instances.

Templates are separated into distinct modes which describe completely
disparate usage purposes and therefore end up in differently
configured Jenkins build jobs. This separation is achieved through
distinct directory structures. The different directories are described
in the following:

:file:`_common`

  Contains templates that are shared by all distinct modes. This
  directory cannot be used as a generator mode. In case a specific
  mode uses a template from this directory, it is symlinked into that
  mode's directory.

:file:`toolkit`

  Describes a mode that can be used to generate build jobs which are
  able to bootstrap a complete software distribution from scratch by
  installing it to a shared filesystem prefix.  Therefore, the Jenkins
  jobs are orchestrated by a buildflow job which triggers the distinct
  jobs per software project in the appropriate order. No polling of
  SCM is performed in this mode and jobs have to be triggered manually
  via the Jenkins interface.

:file:`ci-deploy`

  This mode is used to continuously update a software distribution
  installed in a shared prefix whenever an SCM change to a software
  component appeared. This mode does not handle the bootstrapping
  phase correctly as it starts building software projects whenever a
  change is detected or an upstream project's build finished.

:file:`ci`

  Continuous integration mode for continuously building and testing
  software without installing it to a distinct filesystem prefix.
  Artifact copying is used between build job workspaces to handle
  dependency resolution.

Template Syntax
---------------

A typical template description looks as follows

.. code-block:: yaml

   inherit:
     - foo-template

   variables:
     natures:
       - cmake

   aspects:
     - name:   cmake-cpp.cmake/unix
       aspect: cmake/unix
       conditions:
         unix: .*
       variables:
         aspect.cmake.environment: ${cmake.environment|}
         aspect.cmake.options:     ${cmake.options}
         aspect.cmake.targets:     ${cmake.targets}

     jobs:
       - name: toolkit
         tags:
         - toolkit
         - architecture-dependent
         - gcc
         - unix
         - linux
         variables:
           build-job-name: ${project-name}-${version-name}-toolkit-${distribution-name}
           cmake.environment:
             - PKG_CONFIG_PATH="${toolkit.dir}/lib/pkgconfig:\${PKG_CONFIG_PATH}"
             - "@{next-value|[]}"
           cmake.options:
             - CMAKE_INSTALL_PREFIX="${toolkit.dir}"

             - CMAKE_BUILD_TYPE=RelWithDebInfo

             - CMAKE_SKIP_BUILD_RPATH=FALSE
             - CMAKE_BUILD_WITH_INSTALL_RPATH=FALSE
             - CMAKE_INSTALL_RPATH="${toolkit.dir}/lib"

             - "@{next-value|[]}"
           cmake.targets:
             - install

The following fields are most important:

:samp:`{FILENAME}`

  This is not an actual field but the name of the :term:`recipe file
  <recipe>` with its extension removed (e.g. ``cmake-cpp`` for a
  :term:`recipe file <recipe>` named :file:`cmake-cpp.template`).

  Name of the template describing its purpose.

``variables``

  Variables specific to this template.

``variables`` » ``kind``

  ``"project"``

    "normal" project job

  ``"matrix"``

    matrix job

  :samp:`[ "{ELEMENT-NAME}", "{PLUGIN-NAME@PLUGIN-VERSION}" ]`

    arbitrary kind

``aspects``

  :term:`Aspects <aspect>` are specific configuration fragments to
  include in the generated Jenkins jobs.

``jobs``

  The kind of Jenkins jobs to generate for projects that have this
  template assigned.
