Advanced
=======================

Deployment Modes
-----------------------

Users can choose different deploy modes in ``RDTK``:

1. ``toolkit``
    Describes a mode that can be used to generate build jobs which are
    able to bootstrap a complete software distribution from scratch by
    installing it to a shared filesystem prefix. Therefore, the Jenkins
    jobs are orchestrated by a buildflow job which triggers the distinct
    jobs per software project in the appropriate order. No polling of SCM
    is performed in this mode and jobs have to be triggered manually via
    the Jenkins interface.

2. ``ci-deploy``
    This mode is used to continuously update a software distribution
    installed in a shared prefix whenever an SCM change to a software
    component appeared. This mode does not handle the bootstrapping phase
    correctly as it starts building software projects whenever a change is
    detected or an upstream project's build finished.

3. ``ci``
    Continuous integration mode for continuously building and testing
    software without installing it to a distinct filesystem prefix.
    Artifact copying is used between build job workspaces to handle
    dependency resolution.

4. ``Makefile``
    TODO

5. ``Docker``
    TODO

Private Repository
-----------------------

In cases where access to a repository is restricted, :program:`build-generator` needs to know some login credentials. 

If you are using GitHub for example, you can generate an `access token <https://github.com/settings/tokens>`_ with read-only access to your repository by ticking ``repo -> public_repo`` and then use this token as password along with your GitHub login name.

:program:`build-generator` requires you to store your credentials **unecrypted** in a file called ``~/.netrc``, using the following syntax for every remote machine your distribution is referencing:

.. code-block:: perl

    machine projects.cit-ec.uni-bielefeld.de
        login your_user_name
        password secret_api_token_OR_plain_password

TODO Subversion

TODO Jenkins credentials store

Speed up generator analyze (Caching)
------------------------------------

:program:`build-generator` is using ``git ls-remote`` a lot. When generating often, this process can take up much time. It is then recommended to enable caching, try :option:`cache-directory` and  :option:`cache-age-limit`.


Generate Catalog Representation
-------------------------------

``RDTK`` includes a human readable representation of data generated from recipes and source code. 
You can use :program:`build-generator` to emit these catalog-like pages:

.. code-block:: bash

    export OUTPUT_DIR="$HOME/catalog"
    export DISTRIBUTION="$RDTK_ROOT/citk/distribution/example-*.distribution"
    build-generator report -k catalog -o "$OUTPUT_DIR" "$DISTRIBUTION"

Then use your browser to open the ``.xml`` files

.. code-block:: bash

    xdg-open "$OUTPUT_DIR/distribution/*.xml"
