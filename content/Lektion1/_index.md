---
title: "1. Erste Planungen / Implementationen"
---

{{< toc >}}

# PeerTube & YouTube Video
{{< video 
	id="video1" width="800" height="460" 
	img="/files/video-images/1-übersicht.png"
	youtube=""
	peertube="https://cliptube.org/a/konradn"
	pp="/files/pp/JAdventure_1-Übersicht.pptx"
>}}

Wenn man etwas programmieren will, dann ist es immer notwendig, sich erst einmal darüber klar zu werden, was man bauen möchte.

Gerade am Anfang ist dies ein schwerer Schritt, denn man ist bei allen Übungen gewohnt, dass man sich darüber nicht den Kopf zerbrechen musste. Die Übung, die zu bearbeiten war, hat schon im Detail gesagt, was benötigt wurde.

In dieser ersten Lektion wird es nun weniger um Java sondern mehr um das Projekt gehen.

Dabei sind mehrere Schritte sinnvoll und bilden eine Art Grundgerüst für ein agiles Vorgehen (Die konkreten agilen Verfahren habenn dies detailierter spezifiziert, aber der grobe Rahmen ist immer gleich). Diese Schritte werden in Zyklen immer wieder von Anfang an durchlaufen.

# 1. Vision
Bei der Vision überlegen wir uns, was wir denn am Ende haben wollen. Wo wollen wir hin? Was sind unsere Träume? Hier ruhig alle Ideen aufsammeln. Ob, wie und in welchem Zeitrahmen diese umgesetzt werden können, ist dabei nebensächlich.

Verantwortlich ist hier oft eine spezielle Rolle, die oft als Productowner oder Productmanagement bezeichnet wird.

In einem beruflichen Umfeld würde man hier noch einiges vertiefen. So ist es üblich, den Markt zu analysieren: Gibt es sowas evtl. schon? Ist der Markt überhaupt da für so ein Produkt, wie wir es uns vorstellen? Was würden Kunden dafür denn vermutlich zahlen wollen?

All diese Fragen sind für uns aber erst einmal uninteressant. Unser Ziel ist es, eine Software zu entwickeln, um dabei eine mögliche Vorgehensweise zu lernen.

| Wichtig | Dieser Schritt kann in zukünftigen Iterationen auch entfallen oder stark verkürzt werden. |
|-|-|

# 2. Verwaltung der Features

Aus der Vision muss man konkrete Features ableiten. Diese Features kann man in verschiedenen Weisen dokumentieren. Eine übliche Form sind User Stories, die man schreiben kann. 

Eine mögliche Form einer User Story kann ein einfacher Satz sein:

Als &lt;Rolle&gt; möchte ich &lt;Beschreibung&gt; damit ich &lt;Beschreibung&gt;.

Optional kommen bereits Abnahmekriterien dazu. Was muss erfüllt sein, damit ich das als erfüllt ansehe? Dies muss noch nicht zwingend dokumentiert werden aber es sollte ein gutes Verständnis geben.

| | |
|-|-|
| Beispiel | Als **Spieler** möchte ich **mich auf der Karte bewegen können** damit ich **die Gegend erkunden kann**. |

Diese Liste an Anforderungen bilden eine Grundlage für die Entwicklung. Eine Bezeichnung, die man oft hört (und in SCRUM verwendet wird) ist Backlog.

Dieses Backlog bildet sozusagen unseren Arbeitsvorrat und enthält die Dinge, die wir entwicklen müssen.

Wichtig ist, dass wir hier noch nicht sofort für alle Elemente in irgendwelche Details gehen. Dies kommt erst, sobald eine Story in Frage kommt für eine Implementierung.

Sobald so ein Backlog Item in Frage kommt, muss überlegt werden, ob es bereits konkret genug formuliert wurde. Ist etwas zu allgemein oder zu umfangreich, dann muss dies in mehrere Features aufgeteilt werden. Ein Beispiel ist schnell konstuiert:

**Als Geschäftsführer möchte ich ein MMORPG haben, damit ich es verkaufen und damit viel Geld verdienen kann.**

Hier ist sofort klar: Das ist nichts, das man behandeln kann.

Um hier eien Aussage zu treffen werden die Backlog Items gewichtet: Jeder Eintrag bekommt eine Wertung. Hier sollte ein erste Aufwandsabschätzung erfolgen und dazu können alle Entwickler abstimmen. Dabei kann z.B mit Werten 1, 2, 4, 8 und unendlich gearbeitet werden. Hier geht es nicht um konkrete Aufwände sondern eine grobe Abschätzung untereinander - Eine Wertung 4 sollte ca. so lange dauern wie zwei Wertung 2 Einträge. Unendlich besagt, dass es auf jeden Fall weiter unterteilt werden muss.

## Abhängigkeiten

Die einzelnen Backlog Items können Abhängigkeiten haben. So ist klar, dass ich ein Spielfeld erst anzeigen kann, wenn ich ein Spielfeld habe. Oder auf dem Spielfeld kann sich ein Spieler erst bewegen, wenn es das Spielfeld und den Spieler als Objekte gibt.

## Gewichtung

Der Produkt Verantwortliche bewertet die einzelnen Einträge. Was ist ihm am wichtigsten? Was ist am unwichtigsten? In diese Bewertung können auch Kriterien einfließen wie der Aufwand, denn zwei 1er Einträge können natürlich mehr Wert haben als ein 2er Eintrag.

Durch die Gewichtung und die Abhängigkeiten können die Backlog Items in eine klare Reihenfolge gebracht werden. Diese Reihenfolge dient der Priorisierung der Entwicklung.

# 3. Planung der nächsten Entwicklung

Mit der Priorisierung der Backlock Entries kann nun die konkrete Entwicklung geplant werden. Dazu wird geschaut, wie viel Kapazität in der nächsten Entwicklungsphasae zur Verfügung steht und abgeschätzt, wie viele Elemente der Liste abgearbeitet werden können.

Diese top Elemente werden dann für die weitere Planung genommen und betrachtet.

Für jeden Eintrag werden nun noch die Abnahmekriterien geprüft und vervollständigt. Es wird also klar gesagt, was erfüllt sein muss. Beim bewegen des Spielers über die Karte wäre das z.B., dass der Spieler keine Felder betreten kann, die blockiert sind.

Sobald dies mit dem Productowner erfolgt ist, können die Entwickler für sich jeden Eintrag in einzelne Tasks zerlegen: Was muss konkret getan werden, damit man diesen Backlog Entry erfüllt?

Jeder Task wird auch bezüglich des Zeitbedarfs bewertet. Ein Task sollte in der Regel in einem Tag oder weniger zu erfüllen sein. In Ausnahmefällen mag es auch etwas mehr sein, aber nie mehr wie zwei Tage!

Ergebnis dieser Phase ist dann eine Liste von Tasks, die abzuarbeiten sind. 

# 4. Implementation

Der nächste Schritt ist die Umsetzung der geplanten Tasks. Diese - und wenn möglich wirklich nur diese - werden umgesetzt.

Dabei ist eine Sache zu beachten:
Ein Task umfasst neben der Implementation selbst immer auch die Dokumentation und den Test eben dieser Tasks. Nur mit Test und Dokumentation kann ein Task als abgeschlossen angesehen werden.


# 5. Präsentation und Review

Ein ganz wichtiger Punkt ist immer die Presentation der Ergebnisse und ein Review des Prozesses.

Die fertig gestellten Tasks sollten, wenn möglich, ein (teilweise) einsetzbares Produkt ergeben. Dieses kann präsentiert und vorgeführt werden und wird dann im idealen Fall auch eingesetzt.

Es ist aber auch immer wichtig, sich zusammen zu setzen und zu überlegen: Was ist gut gelaufen? Was ist schlecht gelaufen? Kann (oder muss) der Prozess geändert werden? Stimmt soweit alles? Hier ist die klare Festlegung, wie weiter verfahren wird. 
