.. _glossary:

==========
 Glossary
==========

.. glossary::

   template

     Describes :term:`aspects <aspect>` and configuration defaults of
     a given :term:`project` :term:`nature`. For example, a template
     could describe how a `CMake`_-based C++ project can be built,
     tested and installed.

   distribution

     A collection of particular versions of :term:`projects <project>`
     that can be built, tested and installed together.

   project

     A software project that is processed by the |Project|
     system. Conceptually consists of a repository from which the
     source code of the project can be obtained, a :term:`nature` that
     indicates how the project can be processed and a set of
     versions.

     The above description is not completely accurate because versions
     can differ w.r.t. repository and :term:`nature`.

   recipe

     A text file describing a :term:`distribution`, :term:`project`,
     person, etc.

   nature

     The nature of a :term:`project` is determined by the build
     system, programming language, etc. Examples include
     `CMake`_-based project, `ROS`_ package or `ASDF`_ system. From
     the perspective of |Project|, the nature indicates how a
     :term:`project` has to be analyzed, built, tested and installed.

   aspect

     Are instantiated in :term:`templates <template>` and each
     describe one, well aspect, of how to build, test or install or
     otherwise work with projects of a given :term:`nature`. In
     particular, aspects often manage one piece of `Jenkins`_
     configuration that should be generated for a :term:`project` of a
     certain :term:`nature`.
