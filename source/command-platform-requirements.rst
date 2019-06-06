.. _command-platform-requirements:

=======================
 Platform-Requirements
=======================

.. program:: platform-requirements

Synopsis
========

:samp:`build-generator {[GLOBAL-OPTIONS]} platform-requirements [COMMAND-OPTIONS] --platform=PLATFORM-SPEC DISTRIBUTION-NAME*`

Description
===========

Analyze system packages required on a given platform.

.. option:: --platform=PLATFORM-SPEC

   * type:``STRING``

   * default:``false``

   The platform for which dependencies should be computed.

   The platform is specified as a space-separated sequence of increasingly
   specific component strings:

   .. code-block:: sh

      SYSTEM-NAME [SYSTEM-VERSION [ARCHITECTURE]]




   Examples:

   * "ubuntu"

   * "ubuntu bionic"

   * "ubuntu bionic x86_64"





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

