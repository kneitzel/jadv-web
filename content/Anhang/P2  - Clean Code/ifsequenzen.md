---
title: if Sequenzen vermeiden
---

In der Welt der Softwareentwicklung begegnen wir häufig Situationen, in denen die Ausführung von Code von den Werten bestimmter Variablen abhängt. Diese Abhängigkeit führt oft zu einer Kette von if-Anweisungen, die jeweils unterschiedliche Aktionen basierend auf dem Wert der Variablen auslösen. Solche if-Sequenzen sind zwar grundlegend für die bedingte Logik in der Programmierung, können jedoch schnell zu komplexen und schwer wartbaren Code-Strukturen führen.

Ein typisches Beispiel für eine solche Situation ist im Folgenden dargestellt. Hier sehen wir, wie leicht sich ein scheinbar einfaches if-Elseif-Konstrukt in einen unübersichtlichen und fehleranfälligen Code verwandeln kann. Diese Art von Code ist nicht nur schwer zu lesen, sondern birgt auch das Risiko von Fehlern bei zukünftigen Änderungen und Erweiterungen.

In diesem Dokument werden wir verschiedene Methoden und Techniken untersuchen, um solche if-Sequenzen effizienter zu gestalten. Unser Ziel ist es, die Lesbarkeit, Wartbarkeit und Skalierbarkeit des Codes durch den Einsatz von Best Practices und fortgeschrittenen Programmierkonzepten zu verbessern.

Beispiel:
```java
if (someVar == SOME_VALUE) {
  // ....
} else if (someVar == SOME_OTHER_VALUE) {
  // ....
} else if (someVar == ANOTHER_VALUE) {
  // ....
} ....

```

**Prüfung der Notwendigkeit: Vermeidung von Verteiler Methoden**

Ein wesentlicher erster Schritt in der effizienten Gestaltung von Code ist es, die Notwendigkeit von sogenannten "Verteiler Methoden" kritisch zu hinterfragen. Oftmals können diese Methoden, die lediglich dazu dienen, Aktionen auf Basis bestimmter Bedingungen zu verteilen, komplett vermieden werden, was zu einer klareren und wartbareren Code-Struktur führt.

Ein klassisches Beispiel hierfür sind die in der Vergangenheit häufig eingesetzten ActionListener-Implementierungen in Benutzeroberflächen. In einem solchen Szenario implementiert eine Klasse das ActionListener-Interface und in der actionPerformed-Methode wird dann überprüft, welches UI-Element (z.B. ein Button) das Event ausgelöst hat. Anschließend werden entsprechende Aktionen ausgeführt, abhängig von der Quelle des Events.

Ein modernerer und effizienterer Ansatz ist es, jedem UI-Control direkt eine spezifische Methode zuzuweisen. Dies kann über eine Methodenreferenz oder eine Lambda-Expression erfolgen. So wird für jedes UI-Element eine individuelle Reaktionslogik definiert, die direkt und deklarativ mit dem Element verbunden ist.

```java
// Beispiel mit Methodenreferenz
meinButton.addActionListener(this::handleButtonAction);

// Beispiel mit Lambda-Expression
meinButton.addActionListener(e -> {
    // Aktion für den Button
});
```

Das Prinzip, Verteiler Methoden durch spezifischere und direkt zugeordnete Funktionen zu ersetzen, ist nicht nur auf UI-Events beschränkt, sondern lässt sich auf eine Vielzahl von Szenarien in der Softwareentwicklung anwenden. Im Kern jeder Verteiler Methode steht die Entscheidungslogik, die auf Basis von Parametern unterschiedliche Aktionen auslöst. Diese Struktur findet sich in vielen Bereichen der Programmierung wieder, sei es bei der Verarbeitung von API-Anfragen, der Steuerung von Workflow-Abläufen oder anderen situationsspezifischen Entscheidungspunkten.

Anstatt einen einzigen Methodenaufruf zu verwenden, der intern eine Vielzahl von Bedingungen und Verzweigungen abarbeitet, können wir das Konzept der direkten Zuweisung spezifischer Funktionen nutzen. Durch die direkte Zuweisung einer konkreten Funktion oder Aktion, die auf den spezifischen Kontext und die jeweiligen Parameter abgestimmt ist, kann die Notwendigkeit einer zentralen Verteilungsfunktion häufig umgangen werden.

**Vom Problem zur ersten Lösung: Die Switch-Anweisung**

Nachdem wir nun die typischen Schwierigkeiten verstanden haben, die durch umfangreiche if-Sequenzen entstehen, wenden wir uns der ersten potenziellen Lösung zu: der Switch-Anweisung. Diese stellt in vielen Fällen eine direktere und übersichtlichere Alternative zu verschachtelten if-Elseif-Strukturen dar.

Die Switch-Anweisung in Java ermöglicht es uns, eine Variable gegen eine Reihe von Werten zu prüfen und entsprechend unterschiedliche Aktionen durchzuführen. Anstatt mehrere if-Anweisungen zu verwenden, können wir mit einem einzigen Switch-Block verschiedene Fälle effizient abhandeln. Diese Struktur trägt dazu bei, den Code zu vereinfachen und verbessert seine Lesbarkeit, indem sie eine klare Trennung der verschiedenen Handlungsstränge bietet.

```java
switch (someVar) {
    case SOME_VALUE:
        // ....
        break;

    case SOME_OTHER_VALUE:
        // ....
        break;

    ....
}
```

Obwohl die Switch-Anweisung eine erhebliche Verbesserung gegenüber verschachtelten if-Elseif-Strukturen darstellen kann, gibt es bestimmte Situationen, in denen sie an ihre Grenzen stößt. Diese Einschränkungen zu verstehen, ist entscheidend, um zu erkennen, wann alternative Ansätze erforderlich sind.

- *Komplexe Bedingungen*: Switch-Anweisungen sind ideal für den Vergleich eines einzelnen Variablenwerts mit festen Konstanten. Wenn jedoch komplexere Bedingungen erforderlich sind, wie mehrere Variablen oder Bereiche von Werten, dann sind Switch-Anweisungen nicht geeignet. In solchen Fällen erfordert die Logik eine Reihe von if-Elseif-Anweisungen oder eine andere fortgeschrittene Methode.

- *Dynamische Fallauswahl*: Die Fälle in einer Switch-Anweisung müssen bei der Kompilierung bekannt und konstant sein. Dynamische oder zur Laufzeit bestimmte Fälle können nicht direkt in eine Switch-Anweisung integriert werden.

- *Begrenzung auf vergleichbare Datentypen*: Switch-Anweisungen in Java sind auf bestimmte Datentypen beschränkt, wie int, char, String und Enums. Wenn Sie mit anderen Datentypen oder komplexen Objekten arbeiten, müssen Sie auf andere Strukturen zurückgreifen.

**Innovativer Ansatz: Einsatz von Maps und funktionalen Interfaces**

Nachdem wir die Einschränkungen der Switch-Anweisung betrachtet haben, richten wir unseren Blick auf einen fortschrittlicheren und flexibleren Ansatz zur Handhabung von bedingten Aktionen: die Kombination einer Map mit funktionalen Interfaces. Dieser Ansatz nutzt die Map-Struktur, um Schlüssel-Wert-Paare zu definieren, wobei der Schlüssel (Key) der zu prüfende Wert und der Wert (Value) ein funktionales Interface ist, das die gewünschte Aktion kapselt.

Die Wahl des funktionalen Interfaces richtet sich nach den spezifischen Anforderungen Ihres Anwendungsfalls. Java bietet eine Vielzahl von funktionalen Interfaces im Paket java.util.function, die für die meisten Anforderungen passend sind. Alternativ können Sie auch ein benutzerdefiniertes funktionales Interface erstellen, um spezifische Anforderungen zu erfüllen.

Der Einsatz einer Map in Verbindung mit funktionalen Interfaces ermöglicht eine klare Trennung zwischen der Entscheidungslogik und den auszuführenden Aktionen. Dies verbessert nicht nur die Lesbarkeit des Codes, sondern erhöht auch die Wartbarkeit und Erweiterbarkeit, da neue Fälle einfach durch Hinzufügen neuer Schlüssel-Wert-Paare zur Map berücksichtigt werden können.

Ein konkretes Beispiel für diese Methode könnte wie folgt aussehen:
```java
// Das funktionale Interface. Wir geben im Beispiel nichts zurück und nutzen keine Parameter ...
Interface MyFunctionalInterface {
  void doSomething();
}

// Aufbau der Map. Hier einfach mit Lambda Expressions, aber ich empfehle Methoden-Referenzen für eine gute Lesbarkeit!
Map<Integer, MyFunctionalInterface> myActions = new HashMap<>();
map.put(0, () -> System.out.println("0") );
map.put(1, () -> System.out.println("1") );
map.put(2, () -> System.out.println("2") );

// Der Ersatz für die switch Anweisung oder die ifs
MyFunctionalInterface action = myActions.get(someVar);
if (action != null) {
    action.doSomething();
} else {
    // throw Exception or handle the unknown value somehow.
}
```

Während der Einsatz von Maps in Verbindung mit funktionalen Interfaces eine flexible und leistungsfähige Methode zur Handhabung bedingter Logik darstellt, gibt es einige wichtige Einschränkungen und Überlegungen, die berücksichtigt werden sollten:

- *Komplexität der Initialisierung*: Der Aufbau und die Initialisierung der Map können komplex werden, besonders wenn viele verschiedene Fälle und Aktionen beteiligt sind. Dies kann den Code an der Stelle, an der die Map konfiguriert wird, unübersichtlich machen.

- *Leistungseinbußen bei großen Maps*: Bei einer großen Anzahl von Schlüsseln kann der Zugriff auf die Map weniger effizient sein als eine einfache if-Elseif-Struktur oder eine Switch-Anweisung. Dies gilt insbesondere, wenn der Schlüsselvergleich selbst aufwendig ist.

- *Verwaltung des Zustands*: Da funktionale Interfaces oft zustandslos sind, kann die Handhabung von Zuständen innerhalb der Aktionen schwierig sein. Dies kann zu Problemen führen, wenn die auszuführenden Aktionen auf den Zustand der Anwendung oder auf vorherige Aktionen angewiesen sind.

- *Behandlung fehlender Schlüssel*: Es muss eine Strategie für den Fall implementiert werden, dass kein passender Schlüssel in der Map gefunden wird. Dies erfordert oft zusätzlichen Code zur Fehlerbehandlung oder für Standardaktionen.

- *Lesbarkeit und Wartbarkeit*: Obwohl diese Methode die Hauptlogik vereinfacht, kann sie die Lesbarkeit beeinträchtigen, insbesondere für Entwickler, die nicht vertraut mit funktionalen Programmierkonzepten sind. Außerdem kann die Wartung dieser Struktur anspruchsvoller sein, besonders wenn Änderungen an den Aktionen oder Schlüsseln vorgenommen werden müssen.

Zusammenfassend bietet die Verwendung von Maps mit funktionalen Interfaces zwar eine leistungsstarke Lösung für bestimmte Szenarien, erfordert jedoch sorgfältige Planung und Überlegung bezüglich der Komplexität, Leistung, Zustandsverwaltung, Fehlerbehandlung und allgemeinen Wartbarkeit.

**Einsatz von Enumerations mit Funktionen für klare und erweiterbare Code-Strukturen**

In unserem vorherigen Beispiel haben wir die Nutzung von int-Werten zur Darstellung einer 
begrenzten Anzahl von Möglichkeiten erkundet. 
Eine solche Herangehensweise öffnet jedoch die Tür für unerwünschte oder illegale Werte. 
Eine elegante und robuste Lösung für dieses Problem ist der Einsatz von Enumerations (Enums), 
welche in Java nicht nur als einfache Wertelisten dienen, sondern auch komplexe Verhaltensweisen kapseln können.

Enums in Java sind weitaus mächtiger als ihre Pendants in vielen anderen Sprachen. 
Sie sind im Grunde genommen vollwertige Klassen, die neben den festgelegten Konstanten auch 
Instanzvariablen, Methoden und Konstruktoren enthalten können. Diese Eigenschaften ermöglichen 
es uns, Enums zu verwenden, um komplexe Entscheidungslogik auf eine saubere und wartbare Weise 
zu strukturieren. Anstatt sich auf externe if-Sequenzen oder Switch-Anweisungen zu verlassen, 
können wir das benötigte Verhalten direkt in den Enum-Mitgliedern einbetten. Dies führt nicht 
nur zu einem klareren und leichter zu wartenden Code, sondern erhöht auch die Sicherheit, da 
nur die vordefinierten Enum-Werte verwendet werden können.

Im folgenden Abschnitt illustrieren wir, wie Enums mit eingebetteten Funktionen eingesetzt 
werden können, um eine strukturierte und leicht erweiterbare Lösung für die Verarbeitung 
verschiedener Fälle zu bieten.

```java
// Das funktionale Interface, wir geben mal nichts zurück und nutzen keine Parameter ...
Interface MyFunctionalInterface {
  void doSomething();
}

// Die Enumeration
public enum MyValues {
  SOME_VALUE( () -> System.out.println("SOME_VALUE") ),
  SOME_OTHER_VALUE( () -> System.out.println("some other value") );

  final private MyFunctionalInterface action;

  MyValues(MyFunctionalInterface action) {
    this.action = action;
  }

  public void doAction() {
    action.doSomething();
  }
}

// Die Nutzung wird einfach, da myVal nun vom Typ der Enumeration ist:
myVal.doAction();
```

Die Implementierung von Enumerations mit eingebetteten Funktionen in Java ist eine fortschrittliche Technik, die für bestimmte Szenarien sehr nützlich sein kann. Jedoch bringt dieser Ansatz auch spezifische Einschränkungen und Herausforderungen mit sich, die es zu berücksichtigen gilt:

- *Begrenzte Flexibilität*: Enums in Java sind statisch, was bedeutet, dass die Anzahl und Art der Fälle (Enum-Konstanten) zur Kompilierzeit festgelegt werden müssen. Dies schränkt die Flexibilität ein, da dynamische oder zur Laufzeit generierte Fälle nicht ohne weiteres integriert werden können.

- *Komplexität und Verständlichkeit*: Die Verwendung von Funktionen innerhalb von Enums kann den Code komplexer und schwerer verständlich machen, insbesondere für Entwickler, die nicht vertraut mit fortgeschrittenen Konzepten in Java sind. Dies kann die Wartbarkeit und Erweiterbarkeit des Codes beeinträchtigen.

- *Überladung der Enums*: Enums sind in erster Linie für die Darstellung einer festen Menge von Konstanten gedacht. Durch das Hinzufügen von Verhaltenslogik können Enums überladen wirken, was gegen das Prinzip der Trennung von Zuständigkeit (Separation of Concerns) verstößt.

- *Speicherbedarf*: Jede Enum-Instanz enthält Referenzen auf die zugehörigen funktionalen Interfaces. Bei einer großen Anzahl von Enums kann dies zu einem erhöhten Speicherbedarf führen, besonders wenn die eingebetteten Funktionen umfangreiche Ressourcen benötigen.

- *Einschränkungen bei der Wiederverwendbarkeit*: Da die Funktionen eng mit den spezifischen Enums verknüpft sind, ist ihre Wiederverwendbarkeit in anderen Kontexten oft begrenzt. Dies kann zu einer Duplizierung von Code führen, wenn ähnliche Funktionen in unterschiedlichen Teilen des Programms benötigt werden.

- *Testbarkeit*: Das Testen von Enums mit eingebetteten Funktionen kann komplizierter sein, da jede Funktion möglicherweise in einem eng gekoppelten Kontext mit der Enum-Definition steht. Dies kann die Erstellung isolierter und fokussierter Tests erschweren.

Insgesamt bietet die Verwendung von Enums mit eingebetteten Funktionen eine interessante Möglichkeit zur Strukturierung des Codes, jedoch sollten diese Einschränkungen und Herausforderungen sorgfältig abgewogen werden, um zu entscheiden, ob dieser Ansatz für ein gegebenes Problem angemessen ist.

**Vertiefung und Erweiterung des Themas: Weiterführende Entwurfsmuster und Konzepte**

Für Entwickler, die sich intensiver mit der Optimierung und Strukturierung von Code beschäftigen möchten, bieten folgende Entwurfsmuster und Konzepte interessante Ansätze, die über die grundlegenden Techniken hinausgehen:

- *Strategy Pattern (Strategiemuster)*: Dieses Muster ermöglicht es, eine Familie von Algorithmen zu definieren, sie in separate Klassen zu kapseln und sie austauschbar zu machen. Das Strategiemuster eignet sich besonders gut, um spezifische Verhaltensweisen oder Algorithmen dynamisch zur Laufzeit auszuwählen, was die Flexibilität und Erweiterbarkeit des Codes erhöht.

- *Command Pattern (Kommandomuster)*: Das Kommandomuster wandelt Anfragen oder einfache Operationen in Objekte um. Dies ermöglicht die Parametrisierung von Objekten mit Operationen, die Verzögerung oder das Zurückstellen der Ausführung von Operationen und die Speicherung von Operationen in einer Warteschlange. Es ist besonders nützlich, um Operationen zu entkoppeln, die ausführende von der auslösenden Klasse zu trennen und komplexe Kommandosequenzen zu implementieren.

- *Observer Pattern (Beobachtermuster)*: Das Observer Pattern ist nützlich in Szenarien, in denen sich der Zustand eines Objekts ändern kann und andere abhängige Objekte automatisch über diese Änderungen informiert werden müssen. Dieses Muster fördert eine lose Kopplung, da das Zielobjekt nicht direkt mit den beobachtenden Objekten interagieren muss.

- *Factory Method Pattern (Fabrikmethode)*: Dieses Muster bietet eine Schnittstelle zur Erstellung von Objekten, lässt aber die genaue Klasse der zu erstellenden Objekte offen und delegiert die Entscheidung an Unterklassen. Es ist besonders vorteilhaft, wenn ein System gegenüber zukünftigen Erweiterungen offen bleiben soll.

- *Decorator Pattern (Dekorierermuster)*: Das Dekorierermuster ermöglicht die dynamische Erweiterung der Funktionalität eines Objekts zur Laufzeit. Es bietet eine flexible Alternative zur Unterklassenbildung zur Erweiterung von Funktionalitäten.

Jedes dieser Muster bietet einzigartige Vorteile und Lösungsansätze für bestimmte Software-Design-Probleme. Die Wahl des richtigen Musters hängt von den spezifischen Anforderungen des Projekts und den zu lösenden Problemen ab. Die Beschäftigung mit diesen Mustern kann Entwicklern nicht nur helfen, bestehende Herausforderungen effektiver zu bewältigen, sondern auch ihr Verständnis für strukturierte und wartbare Software-Architektur vertiefen.


