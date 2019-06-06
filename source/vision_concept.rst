Vision and Concept
==================


Software systems in a scientific context:

- Large: Often tens to hundreds of software components
- Heterogeneous: Hosting solutions, version control systems, programming languages, build systems, licenses, maintenance models, 3rd party/1st party, legacy components
- Complex: Dependency structure, versions, variability

Researchers develop software in many different ways:

- Everyone tries to use best suited technologies and process
- Different non-functional requirements (documentation, maintainability, maturity, level of professionalism in development process)
- Teams set up their own CI, sometimes repository hosting – centralized IT services focus on other aspects


Bringing together multiple usually disparate aspects:

- Organizational, social and historical aspects of projects
- Versioning (across version control systems and repository hosting solutions)
- Build system-level dependencies (across build systems and programming languages)

...to facilitate

- Construction and testing
- Deployment
- (Re-)use and reproducibility
- Documentation
- Dissemination

...of large, heterogeneous, complex research software system

TODO: add concept overview image here


Simplified Meta Model
---------------------

.. image:: https://github.com/RDTK/dissemination/raw/master/presentations/2019-generator-jenkins-install-docker-slaves/figures/meta-model.png
    :width: 800px
    :align: center
    :alt: alternate text


Build Generator Process
-----------------------

.. image:: https://github.com/RDTK/dissemination/raw/master/presentations/2019-generator-jenkins-install-docker-slaves/figures/build-generator-process.png
    :width: 800px
    :align: center
    :alt: alternate text


Bootstrapping Process
---------------------

.. image:: https://github.com/RDTK/dissemination/raw/master/presentations/2019-generator-jenkins-install-docker-slaves/figures/bootstrapping.png
    :width: 800px
    :align: center
    :alt: alternate text


Docker Builds
-------------

.. image:: https://github.com/RDTK/dissemination/raw/master/presentations/2019-generator-jenkins-install-docker-slaves/figures/docker-process-ci-initial-setup.png
    :width: 800px
    :align: center
    :alt: alternate text

.. image:: https://github.com/RDTK/dissemination/raw/master/presentations/2019-generator-jenkins-install-docker-slaves/figures/docker-process-ci-scm-trigger.png
    :width: 800px
    :align: center
    :alt: alternate text


