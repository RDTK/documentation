.. _concept-dependencies:

==========================
 Handling of Dependencies
==========================

Overview
========

|Project| needs to be aware of dependencies between :term:`projects
<project>` to be able to determine an order in which a given set of
:term:`projects <project>` can be built. To this end, dependency in
|Project|  manifests itself in form of the following facets:

#. Identification of isolated "requires" and "provides" properties of
   :term:`projects <project>`

#. Construction of a global dependency graph based on the above
   properties whose nodes are :term:`project` versions

#. Implementation of the ordering constraint implied by the above
   graph in form of serial or parallel build plan.

In more detail:

1. "requires" and "provides" properties of :term:`projects <project>`
   can be registered in two ways:

   * The "analysis" phase of the generator tries to identify the
     "provided" and "required" things for all :term:`project` versions
     referenced by the :term:`distribution`.

     This analysis works by looking at build-system-dependent
     dependency declarations in the :term:`project` repository
     (e.g. ``find_package`` in :file:`CMakeLists.txt` for `CMake`_
     :term:`nature`, ``<dependencies>`` in :file:`pom.xml` for
     `Maven`_ :term:`nature`, etc.).

     The results of this analysis form the "ordinary" "requires" and
     "provides" lists of a :term:`project` version. Entries are
     conceptually triples ``(NATURE NAME [VERSION])``. See
     :ref:`concept-dependencies-semantics` for details

   * ``extra-requires`` and ``extra-provides`` entries have to be
     added to :term:`recipes <recipe>` for things that the "analysis"
     phase of the generator cannot detect automatically (Therefore
     "extra").  For example, the generator cannot detect that an
     autotools :term:`project` installs a binary and that a second
     :term:`project` needs this binary installed during its build. In
     such a case, the providing and the requiring project version each
     contain an entry such as ``("program" "my-binary" "1.2.3")`` in
     their ``extra-provides`` and ``extra-requires`` list
     respectively. Such a matching pair allows the generator to detect
     the dependency between the :term:`project` versions.

2. schlägt sich im Wesentlichen im internen Datenmodell des
   build-generators nieder, lässt sich aber mit der --report-directory
   im JSON-Format exportieren.

3. kann sich darin äußern, dass die Beziehungen aus 2. in Form von Up-
   und Downstream-Abhängigkeit zwischen den generierten Jenkins-Jobs
   umgesetzt werden. Die zweite Möglichkeit ist die Erzeugung eines
   Buildflows, der unter Berücksichtigung dieser Beziehungen einen
   teilweise Parallelisierung erlaubt.

   The detected dependencies are used by the generator to determine a
   legal (partially parallelized) build order which is implemented as
   a configuration for the "build-flow" Jenkins plugin.

..
   Es gibt einige Distributionen, in denen Platformabhängigkeiten
   eingetragen sind, diese sind aber überwiegend falsch (die allermeistens
   Abhängigkeiten müssten stattdessen in Projektrezepten stehen). Das
   einzige mir bekannte Positivbeispiel ist
   monitoring-experiments-nightly.distribution.

   Im Allgemeinen sollten diese Abhängigkeiten fast immer in einzelnen
   Projektrezepten eingetragen werden. Ich konnte jetzt kein Beispiel
   finden, in dem unterschiedliche Abhängigkeiten für verschiedene
   Ubuntu-Versionen angegeben sind, aber als grundlegendes Beispiel eignet
   sich rsc.project.

..
   > Irgendwo muss ja stehen, dass rsc vor rsb-cpp gebaut wird... Ist das
   > alles in den templates vergraben?

   Nur ein kleiner Aspekt davon: Templates für Continuous Integration
   sorgen dafür, dass der build-generator generierte Jobs mit Up- und
   Downstream-Beziehungen ausstattet. Templates für den "Toolkit-Modus"
   verhindern das, dafür werden die Jobs in den Buildflow eingetragen.

Syntax of extra-requires and extra-provides Fields
==================================================

Array entries in both fields are of one of the following two forms:

.. parsed-literal::

   [ ":samp:`{NATURE}`", ":samp:`{NAME}`", ":samp:`{VERSION}`" ]
   [ ":samp:`{NATURE}`", ":samp:`{NAME}`" ]

The tree fields have the following semantics

``NATURE``

  In vielen Fällen schon, eigentlich aber eher "Kategorie". Es gibt
  z.B.  auch ``[ "c-header", "spread.h" ]`` oder ``[ "program",
  "sbin/spread" ]``.  Grund: rsb-{cpp,java,python,cl} sind z.B. alle
  Provider von "RSB" aber in verschiedenen Kategorien.

``NAME``

  Eher Name.

``VERSION``

  optionale Version?

.. _concept-dependencies-semantics:

Semantics
=========

Die Semantik ist insgesamt relativ wenig festgelegt. Die Regel ist
eigentlich nur:

Eine Abhängigkeit mit Projekt A als Upstream-Projekt und Projekt B als
Downstream-Projekt entsteht dann, wenn mindestens ein Paar von
extra-provides in Projekt A und extra-requires in Projekt B existiert,
in dem die Kategorie (Feld 1) und der Name (Feld 2) übereinstimmen und
die Versionsfelder, falls vorhanden, kompatibel sind, d.h. die
angebotene Version ist größer oder gleich. Nicht angegebenen Versionen
werden als kompatibel angenommen.

Der build-generator zeigt zwischendurch die benötigten aber nicht
angebotenen Dinge (egal ob via extra-requires oder als Ergebnis der
automatischen Analyse) an.

Der extra-{requires,provides} Mechanismus wird in vielen Fällen nicht
korrekt verwendet, so dass sich im Rezept-Repository viele falsche
Beispiele befinden.

> Und warum ist das "python-provide" ( ["setuptools", "rst",
> "${version-name}"] ) nur 'rst' anstatt 'rsb/rst'? Vielleicht ja auch nur
> Zufall...

Bei Kategorien, die zu automatisch analysierbaren Build-Systemen gehören
(z.B. Maven, ASDF, CMake teilweise, Setuptools teilweise, pkg-config
teilweise) sollten die in extra-{requires,provides} angegebenen Namen
den Namen innerhalb des jeweiligen Build-Systems entsprechen, damit die
zusätzlich angegebenen Abhängigkeitsinformationen mit den Ergebnissen
der automatischen Analyse kombinierbar sind.

"rsb/rst" ist ein Name aus der "maven" Kategorie. In dieser Kategorie
entsprechen die Namen den Werten der GroupId und ArtifactId Feldern.
"rst" ist ein Name innerhalb der "setuptools" Kategorie.

Triggering between Up- and Downstream
=====================================

Consider the following dependency structure::

  A<---B<---C
  ^         |
   `--------'

The following values are allowed:

  direct (the default)

    All jobs corresponding to direct dependencies trigger a given job.

    In the above example, A and B trigger C.

  minimal

    Jobs corresponding to direct dependencies which are not among the
    dependency closure of the direct dependencies trigger a given jobs.

    In the above example, only B triggers C since (A is in the
    dependency closure of the direct dependency B).

  none

    There is no triggering by upstream jobs.
