---
title: Leonux-Programming-Language (Part 01 - Writing a VM in C)
published: true
---

Ich schreibe diesen Post, um den Entwicklungsprozess  meiner eigenen Programmiersprache LEONUX zu teilen.

Das soll zum einen dazu dienen, dass ich gezwungen bin, eine gewisse Struktur in meine Gedanken und den Prozess
an sich zu bringen, andererseits aber auch, dass andere von meinen Fehlern lernen können :) und auf mögliche Fragen,
hier vielleicht passende Antworten bekommen.

> Ich möchte noch festhalten, dass ich selber kein Experte auf dem Gebiet bin und es nur darum ging, mögliche Ideen zur Thematik
einfach mal umzusetzen, ohne in manchen Projektentscheidungen großartig auf Performance und mögliche, daraus resultierende 
Nachteile zu achten. Jedoch war es trotzdem das Ziel, eine relativ performante VM zu bauen, obwohl ein gewisser Performance 
Trade-off gemacht wurde, gerade bei der Implementierung des Stacks. Die benutzte Programmiersprache ist C, da man so eine gute
Kontrolle über den Speicher hat und natürlich primär wegen der höheren Ausführungsgeschwindigkeit, als es z.B. in Python oder Java
der Fall ist.

## Was ist eigentlich eine VM in diesem Kontext?

Bei Programmiersprachen gibt es zwei Arten, die man unterscheidet. (Im Folgenden generalisiere ich etwas...)

- Kompilierte Programmiersprachen

> Kompilierte Programmiersprachen werden durch einen sogenannten Compiler meist in Maschinencode übersetzt, welcher dann direkt
durch den Prozessor ausgeführt werden kann. Es hat jedoch den Nachteil, dass Maschinencode plattformabhängig ist und sich somit
unterscheiden kann. Deshalb muss er auch für jede Plattform passend kompiliert werden und ist nicht portabel.
Jedoch ist die Ausführungsgeschwindigkeit entsprechend schnell, weshalb sich der Aufwand eines Compilers durchaus lohnen kann.

- Interpretierte Programmiersprachen

> Interpretierte Programmiersprachen gehen das Problem anders an, indem der Code bei der Ausführung line-by-line interpretiert
und direkt ausgeführt wird (durch den Interpreter). Durch den Extra-Aufwand des Interpretierens und die fehlende Optimierung
(Der Compiler kann das Programm unter Umständen optimieren) ist die Ausführung natürlich deutlich langsamer. Dies kann jedoch
eine bessere Fehleranalyse ermöglichen.

Eine virtuelle Maschine ist in diesem Kontext meist eine Plattform, für welche das auszuführende Programm in eine Zwischensprache
kompiliert wird, welche dann durch die VM interpretiert und dann ausgeführt, bzw. unter Umständen durch JIT-Compiler in 
Maschinencode kompiliert und dann ausgeführt wird.
Man kann sich eine VM wie eine Art virtueller, unter Umständen mehr oder weniger abstrahierter Prozessor mit bestimmtem
Befehlssatz vorstellen.

Damit ist die Sprache recht kompatibel, da sie unabhängig von der eigentlichen Zielplattform ist, bzw. die VM eine einheitliche
Plattform darstellt. Daraus resultiert natürlich, dass der Code portabel ist für alle Zielplattformen, für die eine passende VM
existiert.

## Was werden wir konkret entwickeln?

Wir werden eine Sprache entwickeln, die durch einen Compiler in eine einfache Zwischensprache übersetzt wird, mit einem
überschaubaren Befehlssatz. Wir werden diesen vermutlich in Python entwickeln.
Im Anschluss wird diese dann durch eine passende VM ausgeführt. Diese werden wir in C entwickeln.

Dabei bauen wir die VM in recht abstrahierter Form. Wir nutzen als Speicher vorallem Stacks, statt Registern und 
eine built-in dynamische Speicherverwaltung. Auf GarbageCollection werden wir zunächst verzichten.
Für den Befehlssatz nehmen wir eine relativ High-Level-Repräsentation und keinen Bytecode.
(was eigentlich die üblichere Variante ist, jedoch weniger leicht zu implementieren ist)

