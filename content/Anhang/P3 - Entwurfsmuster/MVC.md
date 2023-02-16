---
title: Model-View-Controller (MVC)
---

{{< toc >}}

Das MVC-Entwurfsmuster (Model-View-Controller) ist ein bekanntes Softwareentwicklungsmuster, das verwendet wird, um die Trennung von Benutzeroberfläche, Geschäftslogik und Datenmodell zu erreichen. Es sorgt dafür, dass die Komponenten unabhängig voneinander entwickelt und gewartet werden können, was es einfacher macht, Änderungen an der Benutzeroberfläche oder an der Geschäftslogik durchzuführen, ohne dass dabei andere Teile des Systems beeinträchtigt werden. Außerdem kann das MVC-Entwurfsmuster verwendet werden, um die Skalierbarkeit und Wartbarkeit von Anwendungen zu verbessern.

Es besteht aus den folgenden drei Komponenten:

## Model
Das Modell repräsentiert das Datenmodell und beinhaltet die Geschäftslogik. Es enthält Informationen über den Zustand des Systems und bietet Methoden, um diese Daten zu manipulieren. Es ist von der Programmsteuerung und Präsentation unabhängig. Die Präsentation wird über das Beobachter-Entwurfsmuster (Observer-Pattern) über Änderungen informiert.

## View
Die Präsentation (View) ist zuständig für das Anzeigen der Daten aus dem Datenmodel und die Entgegennahme von Benutzer Interaktionen. Dazu kennt es das Datenmodell und wird über das Beobachter-Entwurfsmuster über Änderungen am Model informiert. Vom Benutzer veränderte Daten können zurück in das Datenmodell geschrieben werden. Frameworks für Oberflächen bieten dazu teilweise sogenanntes Binding bereit.
Über das Beobachter-Entwurfsmuster informiert die Präsentation die Programmsteuerung über vom Benutzer getriggerte Aktionen. Dies findet in der Regel über eine Abstraktion statt, d.h. die Programmsteuerung bekommt lediglich die Intention mitgeteilt aber nicht wie diese mitgeteilt wurde. Beispiel: Der Anwender drückt den "Beenden" Knopf. Daher wird die Programmsteuerung informiert, dass der Anwender die Anwendung beenden möchte. Das dies über den Beenden Knopf erfolgte und z.B. nicht über das Datei Menü ist dabei in der Regel uninteressant.


## Controller:
Der Controller  (Programmsteuerung) verwaltet die Interaktion zwischen View und Modell. Es reagiert auf Benutzereingaben, die es als Observer von der View bekommt und manipuliert das Modell entsprechend.


# Framework für MVC

Den Aufbau des MVC Entwurfsmuster verdeutlichen wir im Folgenden an einem kleinen Framework, welches Basisklassen für Model, View und Controller bereit stellt.

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
  