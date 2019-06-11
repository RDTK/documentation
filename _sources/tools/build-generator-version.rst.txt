.. _command-version:

=========
 Version
=========

.. program:: version

Synopsis
========

:samp:`build-generator {[GLOBAL-OPTIONS]} version [COMMAND-OPTIONS]`

Description
===========

Print the version of this program and some components.

Optionally, also print changelog entries for a range of releases.

.. option:: -c=COUNT

   Type: ``(OR BOOLEAN (INTEGER 1 *))`` Default: ``false``

   Number of releases for which a list of changes should be printed.

   True to print changes for all releases.

   False to not print any changes.
