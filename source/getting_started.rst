Getting Started
===============

In general, the |project| is supported on `Ubuntu Linux (16.04/18.04) <https://www.ubuntu.com/download>`_.
However, running the |project| on other Linux flavors is also possible. To this end, please substitute the
corresponding distribution dependent commands, e.g., ``apt-get install``


In order to get started, you will need to install the following dependencies to run |project| tools.
Open a terminal and run:

.. code-block:: bash

    sudo apt-get install openjdk-8-jdk curl python2.7 python2.7-dev \
    python-setuptools git subversion maven build-essential cmake

In general, you can install the RDTK in any location (prefix). However, in order
to establish a common configuration for the tutorials we declare:

.. code-block:: bash

   export RDTK_ROOT=$HOME/RDTK
   mkdir -p $RDTK_ROOT && cd $RDTK_ROOT

Also, please note if you open new shells/terminals in this tutorial, remember to export
``export RDTK_ROOT=$HOME/RDTK`` in the new shell. Alternatively, add ``export RDTK_ROOT=$HOME/RDTK``
to your ``$HOME/.bashrc``.

Install Jenkins
---------------

First you need to download the build-generator from https://github.com/RDTK/generator/releases/latest or via console:

.. code-block:: bash

  # Replace with newest verion from https://github.com/RDTK/generator/releases/latest
  export latest=0.29
  wget https://github.com/RDTK/generator/releases/download/release-$latest/build-generator-$latest-x86_64-linux

.. code-block:: bash

  # Change dir to the download folder of the build-generator
  mv build-generator-$latest-x86_64-linux $RDTK_ROOT
  cd $RDTK_ROOT
  ln -s build-generator-$latest-x86_64-linux build-generator
  chmod u+x build-generator

Install and start Jenkins:

.. code-block:: bash

  # Set yout own USERNAME and PASSWORD and EMAIL
  export JENKINS_USER=USERNAME
  export JENKINS_MAIL=EMAIL@foo.com
  export JENKINS_PASS=PASSWORD
  ./build-generator install-jenkins -u $JENKINS_USER -p $JENKINS_PASS -e $JENKINS_MAIL jenkins
  # This might take between 60 and 300 seconds
  jenkins/start_jenkins

Now open your browser and visit: https://localhost:8080 use username and password to login. You can find the login dialog in the top right corner.


Clone Recipes
-------------

To get the recipes and distributions included in the |project|, please execute the following
code block.

.. code-block:: bash

   cd $RDTK_ROOT
   git clone https://opensource.cit-ec.de/git/citk


Generate Distribution Jobs
--------------------------

Next, to generate Build Jobs on your freshly installed Jenkins CI Server, you need to provide a
distribution file. You can 'find' distributions in:

.. code-block:: bash

   cd $RDTK_ROOT/citk/distributions
   ls


Projects incorporated in a distribution can be found in:

.. code-block:: bash

   cd $RDTK_ROOT/citk/projects
   ls

As an example we will generate all build jobs for the ``build-generator-nightly.distribution``
`(source) <https://opensource.cit-ec.de/projects/citk/repository/revisions/master/entry/distributions/build-generator-experiments.distribution>`_.

.. code-block:: bash

   cd $RDTK_ROOT
   ./build-generator generate -u $JENKINS_USER -p $JENKINS_PASS \
   -D 'view.create?=true' -D view.name='Bootstrapping Tutorial' \
   citk/distributions/build-generator-nightly.distribution

.. note::

  You can use an jenkins api token (-a YOUR_API_TOKEN) insteat of the password.
  YOUR_API_TOKEN can be found out using the Jenkins web interface.

If you reload https://localhost:8080 you should see newly generated jobs.
In order to build and deploy your distribution find a job named **-orchestrate** and
trigger it using the stopwatch icon. **NOTE:** distributions define an *install prefix*
as follows

.. code-block:: bash

  toolkit.volume: /tmp/
  toolkit.dir: ${toolkit.volume}/${distribution-name}

In the scope of this tutorial you can find the result of the build in
in ``/tmp/build-generator-nightly``
