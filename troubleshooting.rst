.. _troubleshooting:

===============
Troubleshooting
===============

.. seealso::

   :ref:`support`
     If this page doesn't help

.. _troubleshooting-reporting-bugs:

Reporting Bugs
==============

Problem

  I'm pretty sure I have found a bug in |project|. What can I do about
  it?

Solution

  First of all, it is entirely possible that you found a bug. We
  appreciate bug reports and encourage you to report all (suspected)
  bugs you see, even if you are not entirely certain. Bug reports
  about things that turn out to not actually be bugs are expected and
  not a problem. However, to save yourself and us time and effort, we
  ask you to keep the following things in mind when reporting bugs.

  Include the following information in your bug report:

    Platform

      Mainly operating system and processor architecture. For example,
      "Ubuntu Precise on x86_64" is a very helpful description.

    Programs and Programming Languages

      In which programming language did you write the failing program?
      If multiple programs are expected to communicate, briefly
      describe the whole setup.

    |project| Version

      Describe which |project| version you are using and how you
      obtained it (e.g. installed Debian packages, compiled from
      source, etc.).

    What did you do?

      Describe what your code does (and include the code, if possible)
      and/or which programs you started. If you use a |project|
      configuration file or environment variables, please describe
      those as well.

    What did you expect to happen?

      For example: "I expected a Jenkins job to be generated for the
      :term:`project` described in the :term:`recipe`
      ``my-project.project``".

    What happened instead?

      For example: "The Jenkins job has not been generated" or "The
      build-generated program crashed with the following backtrace"
      (include error messages and/or backtraces whenever possible).

  Creating the Report as a `new issue`_:

  * In the "Subject" field, try do give a brief description of the
    specific problem. That is, if you can, write "build-generator does
    generate job and displays an error message for CMake project in
    password-protected GIT repository" instead of "build-generator
    crashes".

  * Put the information mentioned above into the "Description" field
    and select the value of the "Category" field according to the
    program and/or programming language.

  * Please try to report bugs in the correct project. We understand
    that this may be hard to figure out and a bug report in the
    "wrong" project is definitely better than no bug report at all.

Missing Dependency
==================

Problem

  The ref:`build-generator <tool-build-generator>` reports something
  like::

    #<VERSION-SPEC flobi-minimal-0.1:flobi-sim:flobi-minimal-0.1 {10089D4903}> (1 missing dependency):
      No provider for (:CMAKE "flobi_description" (0 1 0)).

Solution

  Das heißt entweder, dass im flobi-sim-Rezept extra-requires::

    [ "cmake", flobi_description", "0.1.0" ]

  steht, oder das im assoziierten Projekt
  find_package(flobi_description 0.1.0) in einer CMakeLists.txt-Datei
  gefunden wurde.

  Wer dieses CMake-Paket anbieten müsste, und wie, weiß ich
  nicht. Normalerweise würde ich ein flobi_desciption-Rezept erwarten,
  dass ein passendes extra-provides enthält, oder eine
  flobi_description-config.cmake[.in] im assoziierten Projekt.

Checking out a specific Revision or Commit
==========================================

Problem

  Das ist echt frustrierend. *Welche Möglichkeit gibt es denn, eine
  spezielle svn revision auszuchecken???*

Solution

  .. code-block:: json

     { "versions": [
         {
             "name":   "test-branch-and-revision",
             "variables": {
                 "branch": "trunk",
                 "commit": "13047"
             }
         },
         {
             "name":   "test-directory-and-revision",
             "variables": {
                 "directory": "foo/bar",
                 "commit": "2342"
             }
         }
     ] }

Inspecting Analysis Results
===========================

Problem

  I'm not sure whether the generator's analysis produces correct
  results for my use-case. How can I check?

Solution

  Übrigens lassen sich die gefundenen Abhängigkeiten mit der
  :option:`--report-directory` Option des Generators
  veranschaulichen. Ich muss dort allerdings reverse dependencies und
  fehlende Abhängigkeiten erst noch einbauen. Ein Beispiel ist im
  Anhang.
