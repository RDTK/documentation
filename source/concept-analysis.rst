.. _concept-analysis:

======================
 Analysis of Projects
======================

TODO introduction

CMake Projects
==============

Für ist die Prozedur kompliziert und heuristisch. Kurz gesagt wird das
Projektverzeichnis rekursiv nach Dateien mit Namen
:file:`CMakeLists.txt`, :file:`*[Cc]onfig.cmake[.in]` und
:file:`*.pc[.in]` durchsucht.

In den :file:`CMakeLists.txt`-Dateien werden heuristisch bestimmte
CMake-Befehle gesucht:

* ``set()``, ``option()``, um definierte Variablen zu finden
* ``find_package()``, ``pkg_check_module()``, …, um Abhängigkeiten zu finden

Diese CMake-Befehle werden teilweise interpretiert,
d.h. Variablenreferenzen werden so gut es geht aufgelöst. Für
auflösbare ``find_package()``, ``pkg_check_module()``, … Befehle werden
"require"-Einträge von der Art "cmake" bzw. "pkg-config" erstellt.

In gefundenen :file:`*[Cc]config.cmake[.in]`- und
:file:`*.pc.in``-Dateien werden ebenfalls so gut es geht
Variablenreferenzen aufgelöst und dann "provide" Einträge von der Art
"cmake" und "pkg-config" erstellt.

ROS Packages
============

Für ROS-Packages wird aus der :file:`package.xml` file ein
"provide"-Eintrag von der Art "ros-package" aus dem Paketnamen und der
-version, sowie "require"-Einträge von der gleichen Art für die
aufgelisteten Dependencies erstellt.
