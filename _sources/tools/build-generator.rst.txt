.. _build-generator:

=================
 build-generator
=================

.. program:: build-generator

Synopsis
========

:samp:`build-generator {[GLOBAL-OPTIONS]} {COMMAND} {[COMMAND-OPTIONS]}`

Supported Commands
==================

.. toctree:: :hidden:

   build-generator-analyze

   build-generator-config

   build-generator-create-jenkins-user

   build-generator-generate

   build-generator-help

   build-generator-info-aspects

   build-generator-info-variables

   build-generator-install-jenkins

   build-generator-platform-requirements

   build-generator-report

   build-generator-validate

   build-generator-version

*  :ref:`analyze <command-analyze>` -- Analyze project repositories w

*  :ref:`config <command-config>` -- Describe configuration sources and the current configuration

*  :ref:`create-jenkins-user <command-create-jenkins-user>` -- Create a user account in a Jenkins instance

*  :ref:`generate <command-generate>` -- Generate Jenkins jobs for a given distribution

*  :ref:`help <command-help>` -- Print help either for all commands or for a given command

*  :ref:`info-aspects <command-info-aspects>` -- Print information about available aspects

*  :ref:`info-variables <command-info-variables>` -- Print information about recognized variables

*  :ref:`install-jenkins <command-install-jenkins>` -- Install and configure a Jenkins CI server

*  :ref:`platform-requirements <command-platform-requirements>` -- Analyze system packages required on a given platform

*  :ref:`report <command-report>` -- Generate one or more reports for given distribution(s)

*  :ref:`validate <command-validate>` -- Perform basic sanity checks for a given recipe repository

*  :ref:`version <command-version>` -- Print the version of this program and some components



Global Options
==============

.. option:: --trace-variable=VARIABLE-NAME

   Type: ``(LIST STRING INHERIT? T)`` Default: ``false``

   Trace all accesses to the specified variable.

   This option can be supplied multiple times.

.. option:: --cache-age-limit=AGE-IN-SECONDS

   Type: ``(OR NULL NON-NEGATIVE-INTEGER)`` Default: ``1800``

   Acceptable age of cached information in seconds.

   Older cached information will not be used and will be replaced by newly
   computed information.

.. option:: --cache-directory=DIRECTORY

   Type: ``DIRECTORY-PATHNAME`` Default: ``false``

   Directory into which cached data like repository mirrors should be written.

.. option:: --temp-directory=DIRECTORY

   Type: ``DIRECTORY-PATHNAME`` Default: ``/tmp/``

   Directory into which temporary files should be written.

.. option:: --progress-style=STYLE

   Type: ``(MEMBER NONE CMAKE ONE-LINE)`` Default: ``CMAKE``

   Progress display style.

.. option:: -j=NUMBER-OF-PROCESSES

   Type: ``POSITIVE-INTEGER`` Default: ``8``

   Number of threads (and processes) to execute in parallel.

.. option:: --on-error=POLICY

   Type: ``ERROR-POLICY`` Default: ``((CAUSED-BY-UNFULFILLED-PROJECT-DEPENDENCY-ERROR . CONTINUE) (T . FAIL))``

   Continue when encountering errors?

   Can be simply

   ::

      "abort" to abort immediately for any error
      "fail" to continue but indicate failure for all errors
      "continue" to continue without indicating failure for all errors
      "debug" to enter the debug for all errors

   To choose specific actions for particular errors, rules can be written
   according to the following grammar:

   ::

      error-policy ::= rule* default
      rule ::= error "=>" action ":"
      error ::= "object-error" | "simple-object-error" | "syntax-error" |
                "repository-access-error" | "repository-analysis-error" |
                "project-analysis-error" | "analysis-error" | "dependency-error" |
                "instantiation-error" | "deployment-error" | "report-error"
      default ::= action
      action ::= "abort" | "fail" | "continue" | "debug"

   Example:

   ::

      dependency-error=>continue:analysis-error=>fail:abort

   The above continues the run with exit code zero in case dependency-errors
   are encountered, continues and returns a non-zero exit code for
   analysis-errors and immediately aborts with non-zero exit code for all other
   errors.

.. option:: --debug

   Type: ``BOOLEAN`` Default: ``false``

   Enable debug mode.

.. option:: -h

   Type: ``BOOLEAN`` Default: ``false``

   Print this help and exit.

.. option:: --version

   Type: ``BOOLEAN`` Default: ``false``

   Print version information and exit.
