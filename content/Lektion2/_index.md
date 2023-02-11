---
title: "2. Iteration"
---

{{< toc >}}

# Übersicht

Die Schritte eines agilen Vorgehens haben wir in Lektion 1 im Detail beleuchtet. In diesem Kapitel werden wir darauf verzichten und uns mehr auf die Umsetzung konzentrieren.


Für diese Lektion stehen die folgenden Punkte an:
- Technische Schulden: In der Lektion 1 habe ich Übungen genannt, die durchgeführt werden konnten. Wie die Ergebnisse aussehen können, wird kurz erläutert.
- Erweiterung von Level und GameObject um eine grafische Komponente (2.2.)
- Laden / Speichern von Grafiken und Leveln aus den Ressourcen des Programmes.
- Erstellung eines Clients mit Swing zur Anzeige eines Levels mit Gegenständen (2.3)

Der Schwerpunkt liegt auf dem Client und der Erläuterung des MVC (Model-View-Controller) Patterns. Weiterhin werden wir uns in dieser Lektion um ein paar erste Clean-Code-Aspekte kümmern.

## Erweiterung des Modells

Level und GameObject müssen dargestellt werden können. Dazu müssen wir beiden Klassen ein neues Feld geben: graphicResource.

graphicResource ist ein String, das den Namen einer Ressource enthält.

## Laden der Ressourcen

Wenn wir die Namen von Ressourcen angeben, dann müssen wir eine Möglichkeit einbauen, diese Ressourcen auch zu laden.

Dazu benötigen wir die folgenden Schritte:
- Bereitstellung erster Ressourcen
- Laden der bereitgestellten Bilder
- Laden eins bereitgestellten Levels

## Clean Code: Kein doppelter Code!

Wenn wir uns die Service etwas ansehen, dann machen diese fast das Gleiche! Die einzigen Unterschiede sind:
- Die Methodennamen weichen voneinander ab.
- Der Rückgabetyp ist unterschiedlich
- Die Auswertung des Dateiinhalts ist unterschiedlich.
- Der RESOURCE_PATH und RESOURCE_TYPE weichen voneinander ab.

Hier kann man aber direkt ein Refactoring machen, in dem wir die gemeinsame Funktionalität in eine gemeinsame Oberklasse verschieben.

## Clean Code: API mit JavaDoc kommentieren

Es ist wichtig, dass die API gut dokumentiert wird. Daher sollte man sich angewöhnen, immer JavaDoc Kommentare zu schreiben.

