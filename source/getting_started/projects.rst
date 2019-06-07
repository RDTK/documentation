Creating Projects
=================


Creating a Project
------------------

Create the project under citk/projects with the following content:

.. code-block:: YAML

    templates:
    - <BUILDTYPE>
    - base

    variables:
      repository: <URL>

    branches:
    - master

Replace URL and BUILDTYPE.

The <BUILDTYPE> template depends on your project style.


Templates
.........

.. container:: toggle

    .. container:: header

        **CMAKE**

    Use the ``cmake`` Template.


.. container:: toggle

    .. container:: header

        **JAVA**

    For Maven projects add the ``maven`` Template.
    
    This will run mvn install deploy and dependency:copy-dependencies targets.

    Additional targets can be added with the ``maven.targets`` variable:

    .. code-block:: YAML

        variables:

          maven.targets:
          - foo
          - bar
    

.. container:: toggle

    .. container:: header

        **ROS**

    If your repository contains multiple packages your should use catkin tools to build them using the ``catkin`` Template.


.. container:: toggle

    .. container:: header

        **Python**

    If the project contains a setup.py you need to use the ``setuptools`` Template.

More Templates and their variables can be found here_


Adding a Github Project
-----------------------

Create the project under citk/projects with the following content, replacing <user> and <project> with the organization and project names:

.. code-block:: YAML

    templates:
    - <BUILDTYPE>
    - github
    - base

    variables:
      github.user: <user>
      github.project: <project>

    branches:
    - master



.. _here: todo 