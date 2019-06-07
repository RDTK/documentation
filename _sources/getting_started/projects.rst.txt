Creating Projects
=================


Creating a Project
------------------

Create the :term:`project` :term:`recipe` in the :file:`citk/projects`
directory with the following content, replacing :samp:`{URL}` and
:samp:`{BUILDTYPE}` with appropriate values:

.. code-block:: YAML

    templates:
    - BUILDTYPE
    - base

    variables:
      repository: URL

    branches:
    - master

The :samp:`{BUILDTYPE}` :term:`template` depends on your project
:term:`nature`.

Templates
.........

.. container:: toggle

    .. container:: header

        **CMAKE**

    Use the ``cmake`` :term:`template`.


.. container:: toggle

    .. container:: header

        **JAVA**

    For Maven_ :term:`projects <project>` add the ``maven``
    :term:`template`.

    This will ``run mvn install deploy`` and
    ``dependency:copy-dependencies`` targets.

    Additional targets can be added with the ``maven.targets`` variable:

    .. code-block:: YAML

        variables:

          maven.targets:
          - foo
          - bar


.. container:: toggle

    .. container:: header

        **ROS**

    If your repository contains multiple packages your should use
    catkin tools to build them using the ``catkin`` :term:`template`.


.. container:: toggle

    .. container:: header

        **Python**

    If the project contains a :file:`setup.py` you need to use the
    ``setuptools`` :term:`template`.

More :term:`templates <template>` and their variables can be found
here_


Adding a Github Project
-----------------------

Create the :term:`project` :term:`recipe` in the :file:`citk/projects`
directory with the following content, replacing :samp:`{USER}` and
:samp:`{PROJECT}` with the organization and project name respectively:

.. code-block:: YAML

    templates:
    - BUILDTYPE
    - github
    - base

    variables:
      github.user: USER
      github.project: PROJECT

    branches:
    - master

.. _here: todo
