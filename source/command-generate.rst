.. _command-generate:

==========
 Generate
==========

.. program:: generate

Synopsis
========

:samp:`build-generator {[GLOBAL-OPTIONS]} generate [COMMAND-OPTIONS] DISTRIBUTION-NAME*`

Description
===========

Generate Jenkins jobs for a given distribution.

.. option:: --api-token=API-TOKEN

   * type:``(OR NULL STRING)``

   * default:``false``

   API token for Jenkins authentication.



.. option:: --password=PASSWORD

   * type:``(OR NULL STRING)``

   * default:``false``

   Password for Jenkins authentication.



.. option:: --username=LOGIN

   * type:``(OR NULL STRING)``

   * default:``false``

   Username for Jenkins authentication.



.. option:: --base-uri=URI

   * type:``URI``

   * default:``https://localhost:8080/``

   Jenkins base URI.



.. option:: --delete-other-pattern=REGEX

   * type:``(OR NULL STRING)``

   * default:``false``

   When deleting previously automatically generated jobs, only consider jobs
   whose name matches the regular expression REGEX.

   The default value corresponds to the common case of deleting only jobs
   belonging to previous versions of the distribution(s) being generated, i.e.
   the regular expression (DISTRIBUTION-NAME₁|DISTRIBUTION-NAME₂|…)$.



.. option:: --delete-other

   * type:``BOOLEAN``

   * default:``false``

   Delete previously automatically generated jobs when they are not re-created
   in this generation run.



.. option:: --set=VARIABLE-NAME=VALUE

   * type:``(LIST VARIABLE-ASSIGNMENT)``

   * default:``false``

   Overwrite a variable after loading the distribution.

   Arguments to this option have to be of the form VARIABLE-NAME=VALUE.

   This option can be supplied multiple times.

.. option:: --mode=MODE

   * type:``STRING``

   * default:``toolkit``

   The mode according to which jobs should be generated.

   Selects the set of templates stored in the templates/MODE directory.



.. option:: DISTRIBUTION-NAME*

   * type:``(LIST STRING)``

   * default:``false``

   Distribution recipes(s) which should be processed.

   This option can be supplied multiple times.

