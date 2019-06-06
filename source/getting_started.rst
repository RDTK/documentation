Getting Started
===============

In general, the |project| is supported on `Ubuntu Linux (16.04/18.04) <https://www.ubuntu.com/download>`_.
However, running the |project| on other Linux flavors is also possible. To this end, please substitute the
corresponding distribution dependent commands, e.g., *apt-get install*


In order to get started, you will need to install the following dependencies in order to run |project| tools.
Open a terminal and run:

.. code-block:: bash

    sudo apt-get install openjdk-8-jdk curl python2.7 python2.7-dev \
    python-setuptools git subversion maven build-essential cmake

In general, you can install the RDTK in any location (prefix). However, in order
to establish a common ground for the tutorials we declare:

.. code-block:: bash

   export RDTK_ROOT=$HOME/RDTK

**Please note:** If you choose another prefix, remember to change it in the subsequent steps
of this tutorial.

Install Jenkins
---------------

.. code-block:: bash

   export RDTK_ROOT=$HOME/RDTK
   mkdir -p $RDTK_ROOT
   # Get generator binary from https://github.com/rdtk/generator/release
   # and copy the binary to $RDTK_ROOT
   cd $RDTK_ROOT
   # Replace USER_NAME_CHANGE_ME and PW_CHANGE_ME
   ./build-generator install-jenkins --profile local-docker \
   -u USER_NAME_CHANGE_ME -p PW_CHANGE_ME -e a@b.c install-test
   # This might take between 60 and 300 seconds
   cd install-test
   ./start_jenkins


Now open your browser and visit: https://localhost:8080 use *USER_NAME_CHANGE_ME* and password
*PW_CHANGE_ME* to login. You can find the login dialog in the top right corner.


Clone Recipes
-------------

In order to get the recipes and distributions included in the RDTK, please execute the following
code block.

.. code-block:: bash

   cd $RDTK_ROOT
   git clone https://opensource.cit-ec.de/git/citk


Generate Distribution Jobs
---------------------------

Next, to generate Build Jobs on your freshly installed Jenkins CI Server, you need to provide a
distribution file. You can 'find' distributions in:

.. code-block:: bash

   cd $RDTK_ROOT
   cd citk/distributions
   ls


Projects incorporated in a distribution can be found in:

.. code-block:: bash

   cd $RDTK_ROOT
   cd citk/projects
   ls

As an example we will generate all build jobs for the **build-generator-nightly.distribution**
`(source file) <https://opensource.cit-ec.de/projects/citk/repository/revisions/master/entry/distributions/build-generator-experiments.distribution>`_.

.. code-block:: bash

   cd $RDTK_ROOT
   ./build-generator generate -u USER_NAME -p TEST \
   -D 'view.create?=true' -D view.name='Bootstrapping Tutorial' \
   citk/distributions/build-generator-nightly.distribution


If you reload https://localhost:8080 you should see newly generated jobs.
In order to build and deploy your distribution find a job named **-orchestrate** and
trigger it using the stopwatch icon. **NOTE:*** distributions define an *install prefix*
as follows

.. code-block:: bash

  toolkit.volume: /tmp/
  toolkit.dir: ${toolkit.volume}/${distribution-name}

In the scope of this tutorial you can find the result of the build in
in **/tmp/build-generator-nightly**
