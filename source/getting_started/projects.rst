Creating Projects
=================

- Primer here (templates, recipes, distros), complete examples should be a link to recipe 'manual' in other repo

Lorem Ipsum is simply dummy text of the printing and typesetting industry.
Lorem Ipsum has been the industry's standard dummy text ever since the 1500s,
when an unknown printer took a galley of type and scrambled it to make a type specimen book.
It has survived not only five centuries, but also the leap into electronic typesetting, remaining
essentially unchanged. It was popularised in the 1960s with the release of Letraset sheets containing
Lorem Ipsum passages, and more recently with desktop publishing software like Aldus PageMaker including
versions of Lorem Ipsum.


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

Where <BUILDTYPE> depends on your project style:

.. container:: toggle

    .. container:: header

        **CMAKE**

    Use the::

        cmake

    Template.

.. container:: toggle

    .. container:: header

        **JAVA**

    For Maven projects add the::

        maven
    
    Template. This will run mvn xxx targets,

    howto add additional targets 

.. container:: toggle

    .. container:: header

        **ROS**

    If your repository contains multiple packages your should use catkin tools to build them using the::

        catkin

    Template.

.. container:: toggle

    .. container:: header

        **Python**

    If the project contains a setup.py you need to use the::

        setuptools

    Template.