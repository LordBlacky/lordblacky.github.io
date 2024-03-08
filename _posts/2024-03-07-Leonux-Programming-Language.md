---
title: Leonux-Programming-Language (Part 01 - Writing a VM in C)
published: true
---

Ich schreibe diesen Post, um den Entwicklungsprozess  meiner eigenen Programmiersprache LEONUX zu teilen.

Das soll zum einen dazu dienen, dass ich gezwungen bin, eine gewisse Struktur in meine Gedanken und den Prozess
an sich bekomme, andererseits aber auch, dass andere von meinen Fehlern lernen können :) und auf mögliche Fragen,
hier vielleicht passende Antworten bekommen.

> Ich möchte noch festhalten, dass ich selber kein Experte auf dem Gebiet bin und es nur darum ging, mögliche Ideen zur Thematik
einfach mal umzusetzen, ohne in manchen Projektentscheidungen großartig auf Performance und mögliche, daraus resultierende 
Nachteile zu achten. Jedoch war es trotzdem das Ziel, eine relativ performante VM zu bauen, obwohl ein gewisser Performance 
Trade-off gemacht wurde, gerade bei der Implementierung des Stacks. Die benutzte Programmiersprache ist C, da man so eine gute
Kontrolle über den Speicher hat und natürlich primär wegen der höheren Ausführungsgeschwindigkeit, als es z.B. in Python oder Java
der Fall ist.

## Was ist eigentlich eine VM ?
