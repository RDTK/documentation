.. _command-install-jenkins:

=================
 Install-Jenkins
=================

.. program:: install-jenkins

Synopsis
========

:samp:`build-generator {[GLOBAL-OPTIONS]} install-jenkins [COMMAND-OPTIONS] DIRECTORY`

Description
===========

Install and configure a Jenkins CI server.

* Download Jenkins itself.

* Download and install Jenkins plugins needed by the build generator.

* Install Jenkins configuration files that make the instance work well with the
  build-generator.

* Optionally, if username, email and password are supplied, set up a user
  account.



.. option:: --password=PASSWORD

   Type: ``(OR NULL STRING)`` Default: ``false``

   Password for the initial user account.

.. option:: --email=EMAIL-ADDRESS

   Type: ``(OR NULL STRING)`` Default: ``false``

   Email-address for the initial user account.

.. option:: --username=USENAME

   Type: ``(OR NULL STRING)`` Default: ``false``

   Username for the initial user account.

.. option:: --plugin=PLUGIN

   Type: ``(LIST STRING)`` Default: ``(extra-columns)``

   List of plugins to install in addition to the required ones.

   The following plugins are required and will be installed in any case:

   * ansicolor

   * build-timeout

   * checkstyle

   * copyartifact

   * git

   * github

   * groovy

   * htmlpublisher

   * junit

   * mailer

   * mercurial

   * pmd

   * publish-over-ssh

   * redmine

   * sloccount

   * sonar

   * subversion

   * tasks

   * timestamper

   * warnings

   * warnings-ng

   * xunit



   This option can be supplied multiple times.

.. option:: --jenkins-download-url=URL

   Type: ``URI`` Default: ``http://mirrors.jenkins-ci.org/war-stable/latest/jenkins.war``

   URL from which the Jenkins archive should be downloaded.

.. option:: --profile=PROFILE

   Type: ``(MEMBER SINGLE-USER LOCAL-DOCKER)`` Default: ``SINGLE-USER``

   A Jenkins usage profile to which the installation should be tailored.

.. option:: DIRECTORY

   Type: ``DIRECTORY-PATHNAME`` Default: ``false``

   Destination directory for the Jenkins installation.
