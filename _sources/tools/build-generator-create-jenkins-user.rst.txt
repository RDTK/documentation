.. _command-create-jenkins-user:

=====================
 Create-Jenkins-User
=====================

.. program:: create-jenkins-user

Synopsis
========

:samp:`build-generator {[GLOBAL-OPTIONS]} create-jenkins-user --email=EMAIL-ADDRESS --password=PASSWORD --username=USENAME DIRECTORY`

Description
===========

Create a user account in a Jenkins instance.

.. option:: --password=PASSWORD

   Type: ``(OR NULL STRING)`` Default: ``false``

   Password for the new user account.

.. option:: --email=EMAIL-ADDRESS

   Type: ``(OR NULL STRING)`` Default: ``false``

   Email-address for the new user account.

.. option:: --username=USENAME

   Type: ``(OR NULL STRING)`` Default: ``false``

   Username for the new user account.

.. option:: DIRECTORY

   Type: ``DIRECTORY-PATHNAME`` Default: ``false``

   Home directory of the Jenkins instance in which the user should be created.
