.. _command-analyze:

=========
 Analyze
=========

.. program:: analyze

Synopsis
========

:samp:`build-generator {[GLOBAL-OPTIONS]} analyze [COMMAND-OPTIONS] URI-OR-DIRECTORY*`

Description
===========

Analyze project repositories w.r.t. dependencies and meta-data.

Analysis results are printed to the standard output stream in JSON format.

.. option:: URI-OR-DIRECTORY*

   * type:``(LIST (OR PROPER-PURI PATHNAME))``

   * default:``false``

   Location(s) of the project repository(ies).

   For repository locations specified as URIs, the following syntax is used:

   .. code-block:: sh

      SCHEMA://HOST[:PORT][/PATH][#BRANCH][?scm=SCM&sub-directory=SUB-DIRECTORY]




   where SCM is "git", "subversion", "mercurial" or "archive", BRANCH is the
   branch and SUB-DIRECTORY is the sub-directory within the repository that
   that should be analyzed. All other components of the URI are passed to
   respective version control system.

   This option can be supplied multiple times.

.. option:: --nature=NATURE

   * type:``(LIST (MEMBER FREESTYLE MAVEN CMAKE ASDF ROS-PACKAGE ROS-PACKAGES))``

   * default:``false``

   Nature(s) according to which the project(s) should be analyzed.

   The project nature(s) is/are guessed if not specified.

   This option can be supplied multiple times.

