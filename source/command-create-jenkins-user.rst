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

   * type:``(OR NULL STRING)``

   * default:``false``

   Password for the new user account.



.. option:: --email=EMAIL-ADDRESS

   * type:``(OR NULL STRING)``

   * default:``false``

   Email-address for the new user account.



.. option:: --username=USENAME

   * type:``(OR NULL STRING)``

   * default:``false``

   Username for the new user account.



.. option:: DIRECTORY

   * type:``DIRECTORY-PATHNAME``

   * default:``false``

   Home directory of the Jenkins instance in which the user should be created.



