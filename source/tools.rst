.. _commands:

==========
 Commands
==========

.. program:: build-generator

Synopsis
========

:samp:`build-generator {[GLOBAL-OPTIONS]} {COMMAND} {[COMMAND-OPTIONS]}`

Global Options
==============



.. option:: --trace-variable=VARIABLE-NAME

   * type:``(LIST STRING INHERIT? T)``

   * default:``false``

   Trace all accesses to the specified variable.

   This option can be supplied multiple times.

.. option:: --cache-age-limit=AGE-IN-SECONDS

   * type:``(OR NULL NON-NEGATIVE-INTEGER)``

   * default:``1800``

   Acceptable age of cached information in seconds.

   Older cached information will not be used and will be replaced by newly
   computed information.



.. option:: --cache-directory=DIRECTORY

   * type:``DIRECTORY-PATHNAME``

   * default:``false``

   Directory into which cached data like repository mirrors should be written.



.. option:: --temp-directory=DIRECTORY

   * type:``DIRECTORY-PATHNAME``

   * default:``/tmp/``

   Directory into which temporary files should be written.



.. option:: --progress-style=STYLE

   * type:``(MEMBER NONE CMAKE ONE-LINE)``

   * default:``CMAKE``

   Progress display style.



.. option:: -j=NUMBER-OF-PROCESSES

   * type:``POSITIVE-INTEGER``

   * default:``8``

   Number of threads (and processes) to execute in parallel.



.. option:: --non-interactive

   * type:``BOOLEAN``

   * default:``false``

   Avoid any user interaction.



.. option:: --on-error=POLICY

   * type:``ERROR-POLICY``

   * default:``((CAUSED-BY-UNFULFILLED-PROJECT-DEPENDENCY-ERROR . CONTINUE) (T . FAIL))``

   Continue when encountering errors?

   Can be simply

   .. code-block:: sh

      "abort" to abort immediately for any error
      "fail"
      to continue but indicate failure for all errors
      "continue"
      to continue without indicating failure for all errors
      "debug"
      to enter the debug for all errors




   To choose specific actions for particularerrors, rules can be written
   according to thefollowing grammar:

   .. code-block:: sh

      error-policy ::= rule* default
      rule
      ::= error "=>" action ":"
      error
      ::= "object-error" | "simple-object-error" | "syntax-error" |
      "repository-access-error" | "repository-analysis-error" |
      "project-analysis-error" | "analysis-error" | "dependency-error" |
      "instantiation-error" | "deployment-error" | "report-error"
      default
      ::= action
      action
      ::= "abort" | "fail" | "continue" | "debug"




   Example:

   .. code-block:: sh

      dependency-error=>continue:analysis-error=>fail:abort




   The above continues the run with exit code zero in case dependency-errors
   are encountered, continues and returns a non-zero exit code for
   analysis-errors and immediately aborts with non-zero exit code for all other
   errors.



.. option:: --debug

   * type:``BOOLEAN``

   * default:``false``

   Enable debug mode.



.. option:: -h

   * type:``BOOLEAN``

   * default:``false``

   Print this help and exit.



.. option:: --version

   * type:``BOOLEAN``

   * default:``false``

   Print version information and exit.





Supported Commands
==================

.. toctree:: :hidden:

   command-analyze

   command-config

   command-create-jenkins-user

   command-generate

   command-help

   command-info-aspects

   command-info-variables

   command-install-jenkins

   command-platform-requirements

   command-report

   command-validate

   command-version

*  :ref:`analyze <command-analyze>`

  Analyze project repositories w

*  :ref:`config <command-config>`

  Describe configuration sources and the current configuration

*  :ref:`create-jenkins-user <command-create-jenkins-user>`

  Create a user account in a Jenkins instance

*  :ref:`generate <command-generate>`

  Generate Jenkins jobs for a given distribution

*  :ref:`help <command-help>`

  Print help either for all commands or for a given command

*  :ref:`info-aspects <command-info-aspects>`

  Print information about available aspects

*  :ref:`info-variables <command-info-variables>`

  Print information about recognized variables

*  :ref:`install-jenkins <command-install-jenkins>`

  Install and configure a Jenkins CI server

*  :ref:`platform-requirements <command-platform-requirements>`

  Analyze system packages required on a given platform

*  :ref:`report <command-report>`

  Generate one or more reports for given distribution(s)

*  :ref:`validate <command-validate>`

  Perform basic sanity checks for a given recipe repository

*  :ref:`version <command-version>`

  Print the version of this program and some components

