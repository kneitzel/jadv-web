---
title: "1.4. Implementation"
---
{{< toc >}}
# Projekt

Wir erstellen in IntelliJ ein neues Maven Projekt. Dazu reicht es es aus, einfach unter New Project folgende Auswahl zu treffen:

<img src="./1.4-new-project.png" width="25%"></img>

- Name: jadventure
- Location: Ein Ort, an dem ein neues Verzeichnis jadventure angelegt werden soll für das Projekt.
- Create Git repository: Ja
- Language: Java
- Build System: Maven
- JDK: 17
- Add sample code: Ja
- Advanced Settings:
	- GroupId: org.jadv
	- ArtefactId: jadventure

Im Anschluss am Besten noch über das Maven Toolfenster den Maven Wrapper hinzufügen durch einen ```mvn wrapper:wrapper``` Aufruf.

Alternativ kannst Du das Projekt von 
<a href="https://github.com/kneitzel/JAdventure" target="_blank"> GitHub JAdventure Projekt unter https://github.com/kneitzel/JAdventure (extern) </a> {{< de >}} {{< en >}} laden.

# Entities
Die ganzen Entity Klassen legen wir in den Namespace org.jadv.model. Um den Code klein zu halten, nutzen wir <a href="https://projectlombok.org/" target="_blank"> Lombok (extern)</a> {{< en >}}.

Im Folgenden gibt es nur eine kurze Zusammenfassung - auf der jeweiligen Unterseite finden sich mehr Details.

## Level
Die Klasse Level enthält die folgenden Felder:
- String name
- int width
- int height
- List&lt;GameObject&gt; childs

## GameObject

Die Klasse GameObject bekommt
- String name
- Size size
- Position position

## Size

Die Klasse Size ist eine abstrakte Klasse mit den zwei abgeleiteten Klassen RectangleSize (mit width / height) und CircleSize (mit radius)

## Position
Die Klasse Position bekommt
- int x
- int y
für die Koordinate sowie einen Link auf den parent:
- Object parent

# Serialisierung mit Gson

## Problem 1: Serialisierung Abgeleiteter Klassen

Wir müssen bei der Serialisierung und Deserialisierung immer genau wissen, was für eine Klasse wir gerade serialisieren bzw. deserialisieren.

Damit wir bei der Deserialisierung wissen, was für eine Klasse da heraus kommen soll, schreiben wir den Klassennamen mit in das Objekt.

Dazu führen wir eine Klasse SavedObject ein, die ein Feld type hat, das auf den Namen der Klasse gesetzt ist.

Die Serialisierung und Deserialisierung läuft dann über einen Adapter, der sicher stellt, dass ein Objekt korrekt verarbeitet wird.

## Problem 2: Zirkuläre Referenzen
Die Level verweisen auf die Objekte im Level. Die Objekte im Level verweisen über die Position auf das Level.
Eine solche zirkuläre Abhängigkeit kann so nicht gespeichert werden. Wir haben hier den einfachen Weg gewählt, dass die Position die Parent Referenz als transient markiert, das heisst, dass dieses Feld weder mit geschrieben noch mit gelesen wird.

Damit wir ein Level richtig laden können, müssen wir nach dem Laden durch alle Child Elemente gehen und in diesen den Parent richtig setzen.

