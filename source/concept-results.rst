.. _concept-results:

===========================================
 Results of and Problems during Processing
===========================================

* Warnungen

  Kommen fast nicht vor, spielen im Grunde keine Rolle.

* Fehler

  Eigentlich alle Fehlermeldungen des Generators sind das Resultat von
  Fehlern. Das gilt auch für alle abhängigkeitsbezogenen Meldungen und
  die neuen Fehlermeldungen über nicht verarbeitbare CMake-
  Ausdrücke. Ohne --on-error continue brechen alle Fehler die
  Ausführung ab. Umgekehrt lässt sich mit --on-error continue
  angesichts fast aller Fehler die Ausführung fortsetzen. Die
  fortgesetzte Ausführung ist dabei so vollständig wie
  möglich. D.h. z.B., dass Jobs erzeugt werden, wenn es
  Abhängigkeitsprobleme oder gewisse Analyseprobleme gibt, aber nicht,
  wenn bereits mit der Rezept-Datei etwas nicht stimmt oder die
  referenzierte Version fehlt.

* Fataler Fehler

  Der einzige fatale Fehler (d.h. --on-error continue wirkt nicht und
  die Ausführung bricht ab), der mir z.Z. einfällt, ist eine falsche
  "access"-Deklaration.

UNIX Exit Code
==============

Es gibt noch eine kleine Nuance: Patrick hat sich mal gewünscht, dass
bei --on-error continue der UNIX-exit code des Prozesses anzeigen soll,
ob alle Fehler abhängigkeitsbezogen waren, oder ob es noch andere
Fehler gab.
