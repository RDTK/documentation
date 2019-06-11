.. _command-report:

========
 Report
========

.. program:: report

Synopsis
========

:samp:`build-generator {[GLOBAL-OPTIONS]} report [COMMAND-OPTIONS] -k=KIND -o=DIRECTORY DISTRIBUTION-NAME*`

Description
===========

Generate one or more reports for given distribution(s).

More concretely, write information about distributions and projects into one or
more report files. The written information includes most of the content of the
respective underlying recipe but also expanded variable values, inferred
variable values and analysis results.

.. option:: -o=DIRECTORY

   Type: ``DIRECTORY-PATHNAME`` Default: ``false``

   Directory into which output should be written.

.. option:: -k=KIND

   Type: ``(LIST (MEMBER JSON GRAPH CATALOG))`` Default: ``false``

   The kind(s) of report(s) that should be generated.

   This option can be supplied multiple times.

.. option:: -D=VARIABLE-NAME=VALUE

   Type: ``(LIST VARIABLE-ASSIGNMENT)`` Default: ``false``

   Overwrite a variable after loading the distribution.

   Arguments to this option have to be of the form ``VARIABLE-NAME=VALUE`` .

   This option can be supplied multiple times.

.. option:: -m=MODE

   Type: ``STRING`` Default: ``toolkit``

   The mode according to which jobs should be generated.

   Selects the set of templates stored in the templates/MODE directory.

.. option:: DISTRIBUTION-NAME*

   Type: ``(LIST STRING)`` Default: ``false``

   Distribution recipes(s) which should be processed.

   This option can be supplied multiple times.
