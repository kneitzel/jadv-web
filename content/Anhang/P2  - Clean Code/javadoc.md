---
title: JavaDoc
---

Es ist oft hilfreichm die API im Detail zu dokumentieren. Dies geschieht am einfachsten direkt im Source Code mit Hilfe von JavaDoc.

JavaDoc Kommentare können vor
- Klassen
- Feldern
- Konstruktoren und Methoden
gesetzt werden. JavaDoc Kommentare starten entweder jede Zeile mit ```///``` oder sie bilden einen Kommentarblock per ```/**``` und beenden diesen mit ```*/```.

Viele Entwicklungsumgebungen unterstützen den Entwickler indem sie bei Start einer JavaDoc Kommentares direkt einen Block mit den üblichen Angaben erzeugen.

# JavaDoc auf einer Klasse

Die wichtigsten Elemente, die in der JavaDoc-Dokumentation einer Klasse enthalten sein sollten, sind:

Überschrift: Eine Überschrift, die den Namen der Klasse enthält.

Beschreibung: Eine kurze Beschreibung, die das Ziel und den Zweck der Klasse beschreibt.

@author: Der Name des Autors der Klasse.

@version: Die Version der Klasse.

@see: Verweise auf ähnliche oder verwandte Klassen oder Methoden.

Beispiele: Beispiele, wie die Klasse verwendet wird, um ein besseres Verständnis zu ermöglichen.

Beispiel:
```java
/**
* Die Klasse Circle repräsentiert einen Kreis mit einem Radius.
*
* @author Jane Doe
* @version 1.0
* @see java.lang.Math#PI
*/
```

# JavaDoc auf einem Feld

Ein JavaDoc-Kommentar auf einem Feld sollte eine kurze Beschreibung des Zweckes des Feldes enthalten.

Beispiel:
```java
/**
* Der Radius des Kreises.
*/
private double radius;
```

# JavaDoc auf einer Methode

Ein JavaDoc-Kommentar auf einer Methode kann folgende Informationen enthalten:

Überschrift: Eine Überschrift, die den Namen der Methode enthält.

Beschreibung: Eine kurze Beschreibung des Zweckes und der Funktionalität der Methode.

@param: Eine Liste der Parameter, die die Methode erwartet, inklusive einer kurzen Beschreibung jedes Parameters.

@return: Eine Beschreibung der Rückgabewerte der Methode, falls vorhanden.

@throws: Eine Liste der Ausnahmen, die von der Methode ausgelöst werden können, inklusive einer kurzen Beschreibung jeder Ausnahme.

Beispiele: Beispiele, wie die Methode verwendet wird, um ein besseres Verständnis zu ermöglichen.

Beispiel:
```java
/**
* Berechnet den Umfang des Kreises.
*
* @return Der Umfang des Kreises.
* @see java.lang.Math#PI
*/
public double getCircumference() {
    return 2 * Math.PI * radius;
}
```
