Bootstrapping the |project|
===========================

In general you can install the RDTK in any location. However, in order
to establish a common ground for the tutorials we declare:

.. code-block:: bash

   export RDTK_ROOT=$HOME/RDTK

**Please note:** if you choose another folder, remember to change also it in the following steps.

Install Jenkins
----------------

.. code-block:: bash

   export RDTK_ROOT=$HOME/RDTK
   mkdir -p $RDTK_ROOT
   # Get generator binary from https://github.com/rdtk/generator/release
   # and copy the binary to $RDTK_ROOT
   cd $RDTK_ROOT
   ./build-generator install-jenkins --profile local-docker \
   -u USER_NAME -p TEST -e a@b.c install-test
   # This might take between 60 and 300 seconds
   cd install-test
   ./start_jenkins


Now open your browser and visit: https://localhost:8080 use USER_NAME and Password TEST to login


Clone Recipes
-------------

.. code-block:: bash

   cd $RDTK_ROOT
   git clone https://opensource.cit-ec.de/git/citk


Generate Distribution Jobs
---------------------------

In order to generate Build Jobs you need to provide a distribution file. You
can find distributions in:

.. code-block:: bash

   cd $RDTK_ROOT
   cd citk/distributions
   ls

As an example we will generate all build jobs for: **build-generator-nightly.distribution**

.. code-block:: bash

   cd $RDTK_ROOT
   ./build-generator generate -u USER_NAME -p TEST \
   -D 'view.create?=true' -D view.name='Bootstrapping Tutorial' \
   citk/distributions/build-generator-nightly.distribution


If you refresh https://localhost:8080 you should see newly generated jobs.
In order to build your distribution find a job named **orchestrate** and
activate it using the stopwatch icon.
