.. _command-config:

========
 Config
========

.. program:: config

Synopsis
========

:samp:`build-generator {[GLOBAL-OPTIONS]} config ACTION [OPTION]`

Description
===========

Describe configuration sources and the current configuration.

Configuration information is merged from multiple sources (highest priority
first):

* Options specified on the commandline

* Environment variables named BUILD_GENERATOR_option_name

* Configuration files named build-generator.conf in the current directory,
  ~/.config/ and /etc/. This can be changed using the
  BUILD_GENERATOR_CONFIG_FILES environment variable.



Setting the BUILD_GENERATOR_CONFIG_DEBUG environment variable to an arbitrary
value causes debug information regarding configuration sources and the current
configuration to printed during startup.

.. option:: [OPTION]

   * type:``(OR NULL STRING)``

   * default:``false``

   Name(s) of option(s) to which the action should be applied.



.. option:: ACTION

   * type:``(MEMBER GET LIST TREE)``

   * default:``false``

   The configuration action to perform.



