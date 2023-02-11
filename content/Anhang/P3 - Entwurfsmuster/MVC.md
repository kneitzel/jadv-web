---
title: Model-View-Controller (MVC)
---

{{< toc >}}

Das MVC Entwurfsmuster unterteilt die eine Software in drei Komponenten. Zum einen das Datenmodell (Model), die Präsentation (View) und die Programmsteuerung (Controller). Ziel ist, ein möglichst flexiblen Aufbau zu bekommen, der Änderungen und Anpassungen in Zukunft erleichtern und wie Wiederverwendbarkeit erhöhen soll. So ist es denkbar, die Präsentationsebene anzupassen oder auszutauschen ohne irgend welche Anpassungen im Model oder Controller vorzunehmen.
Weiterhin ermöglicht diese Aufteilung eine einfache Arbeitsteilung zwischen Entwicklern, da unabhängig voneinander entwickelt werden kann.

In der praktischen Entwicklungsarbeit ist ein großer Vorteil der sauberen Trennung, dass die ganze Logik in Datenmodell und Programmsteuerung über Unit Tests getestet werden kann. Lediglich für die Präsentation sind spezielle, meist komplexere, Oberflächentests (UI Tests) zu erstellen.

## Model
Das Datenmodell enthält die Daten, die von der Präsentation bereit gestellt werden. Es ist von der Programmsteuerung und Präsentation unabhängig. Die Präsentation wird über das Beobachter-Entwurfsmuster (Observer-Pattern) über Änderungen informiert.

## View
Die Präsentation (View) ist zuständig für das Anzeigen der Daten aus dem Datenmodel und die Entgegennahme von Benutzer Interaktionen. Dazu kennt es das Datenmodell und wird über das Beobachter-Entwurfsmuster über Änderungen informiert. Vom Benutzer veränderte Daten können zurück in das Datenmodell geschrieben werden. Frameworks für Oberflächen bieten dazu teilweise sogenanntes Binding bereit.
Über das Beobachter-Entwurfsmuster informiert die Präsentation die Programmsteuerung über vom Benutzer getriggerte Aktionen. Dies findet in der Regel über eine Abstraktion statt, d.h. die Programmsteuerung bekommt lediglich die Intention mitgeteilt aber nicht wie diese mitgeteilt wurde. Beispiel: Der Anwender drückt den "Beenden" Knopf. Daher wird die Programmsteuerung informiert, dass der Anwender die Anwendung beenden möchte. Das dies über den Beenden Knopf erfolgte und z.B. nicht über das Datei Menü ist dabei in der Regel uninteressant.

## Controller
Die Programmsteuerung (Controller) ist verantwortlch für das Datenmodell und die Präsentation. So füllt es die notwendigen Daten in das Datenmodell und übergibt das Datenmodell an die Präsentation. Der Controller trägt sich als Beobachter bei der Präsentation ein, um Aktionen des Anwenders zu erfahren und um diese dann zu verarbeiten. Dabei können die Daten im Datenmodell angepasst werden. Bei Änderungen informiert das Datenmodell die Präsentation, so dass die Anzeige aktualisiert werden kann.

# Framework für MVC

Wie das MVC Pattern aufgebaut wird, kann man an dem Framework erkennen, das im Rahmen dieses Kurses entstanden ist.

## Model Class

Die Basisklasse für das Datenmodell ist Model und implementiert lediglich das Beobachter Entwurfsmuster. Zentraler Punkt des Entwurfsmusters ist die Verwaltung der Beobachter. Der Beobachter bekommt lediglich eine Information, dass sich das Datenmodell geändert hat incl. einer Referenz auf das Datenmodell. Dies ist ein sehr grober Aufbau - prinzipiell ist auch denkbar, dass man hier deutlich mehr Informationen übergibt. So wäre denkbar, sich an den [PropertyChangeListener](https://docs.oracle.com/en/java/javase/17/docs/api/java.desktop/java/beans/PropertyChangeListener.html) zu halten, aber uns soll bei der Implementation die generelle Information, dass ich das Model geändert hat, reichen. Daher nutzen wir ein [Consumer&lt;Model&gt;](https://docs.oracle.com/en/java/javase/17/docs/api/java.base/java/util/function/Consumer.html).

Damit sich beobachter ein- und austragen können, fügen wir die Methoden addChangeListener und removeChangeListener hinzu.

Für die Signalisierung einer Veränderung erstellen wir eine Methode hasChanged(). Diese geht die Liste der ChangeListener durch um diese über die Veränderung am Model zu informieren.

| Wichtig! | Die Implementierung ist in Bezug auf mehrere Threads nicht sicher! Beim Iterieren über die Liste darf diese nicht verändert werden. |

## View Class

Die Basisklasse für die Präsentation ist View und implementiert:
- Es beinhaltet ein Model. Dazu fordert es die Methode getModel. Das Überschreiben bietet den Vorteil, dass die Klasse dabei das konkrete Modell zurück geben kann. Damit hat man nur an einer konkreten Stelle die Notwendigkeit eines Cast. Der Setter für das Datenmodell fügt die View auch direkt als Beobachter bei dem Datenmodell ein.
- Es wird ein Observer für Controller implementiert. Dazu gehörn Methoden zum Hinzufügen und Löschen von Controllern.
- Die Methoden init und show dienen der Implementation In der Methode init() kann sich die Präsentation initialisieren. Dies kann dazu genutzt werden, die notwendigen Controls zu erzeugen. Die Methode show dient dann der Anzeige der Präsentation.
- updateView() dient der Aktualisierung der Anzeige. Die Präsentation ruft diese Methode automatisch auf, wenn das Model sich geändert hat, so dass die angezeigten Werte mit den neuen Werten ersetzt werden können.
- updateModel() dient der Aktualisierung des Models falls notwendig. Diese Methode kann genutzt werden, um Werte aus Controls in das Datenmodell zu übernehmen.
- sendAction dient der Übermittlung einer Aktion an die Programmsteuerung. Vorher wird updateModel aufgerufen, so dass das Datenmodell aktuelle Werte enthält.

## Controller Class

Die Basisklasse für die Programmsteuerung ist Controller.
- Der Konstruktor erwartet eine Referenz auf ein Datenmodell und auf die View. Die abgeleitete Klasse sollte diese erzeugen.
  - Diese Parameter werden in Instanzvariablen gesichert
  - Das Datenmodell wird der Präsentation bereit gestellt
  - Die Programmsteuerung trägt sich als Beobachter in der Präsentation ein
  - Zuletzt wird die Präsentation initialisiert.
  - getView / getModel sind abstrakte Methoden, die überschrieben werden sollen. Damit haben wir für Model und View im Controller nur einen Cast bei Zugriffen.
  - handleAction() ist die Methode, die bei Aktivitäten von der Präsentation aufgerufen wird.
  