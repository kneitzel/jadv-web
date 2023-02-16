---
title: P2 - Clean Code (Übersicht)
---

TODO: Noch nicht abgeschlossen

{{< toc >}}

# Was ist Clean Code

Als Umschreibung, was Clean Code ist, einfach zwei Zitate, die relativ gut umschreiben:

```
Any fool can write code that a computer can understand.
Good programmers write code that humans can understand.
```
Martin Fowler

```
Clean code is simple and direct. 
Clean code reads like well-written prose. 
Clean code never obscures the designer’s intent but rather is full of 
crisp abstractions and straightforward lines of control.
```
Grady Booch

# Warum Clean Code

Clean Code ist gut strukturiert, einfach zu verstehen und einfach zu pflegen. Hier sind einige der wichtigsten Gründe, warum man Clean Code schreiben sollte:

Lesbarkeit: Clean Code ist einfach zu lesen und verstehen, was es anderen Entwicklern erleichtert, den Code nachzuvollziehen und zu warten.

Wartbarkeit: Clean Code ist einfach zu pflegen und zu aktualisieren, was die Zeit und Kosten für die Wartung des Codes reduziert.

Fehlerbehebung: Clean Code macht es einfacher, Fehler zu identifizieren und zu beheben, da die Struktur und Logik des Codes klar sind.

Zusammenarbeit: Clean Code erleichtert die Zusammenarbeit zwischen Entwicklern, da es einfacher ist, den Code zu verstehen und zu erweitern.

Skalierbarkeit: Clean Code ist skalierbar und ermöglicht es, den Code einfach zu erweitern und an neue Anforderungen anzupassen.

Insgesamt ist Clean Code eine wichtige Praxis, die dazu beiträgt, dass Code effizienter, fehlerfreier und einfacher zu pflegen ist. Es ist wichtig, Zeit und Anstrengung in die Schreibweise von Clean Code zu investieren, um die Vorteile in der Zukunft zu nutzen.

# Code Smells

Code Smells sind Anzeichen für schlechten Code, die darauf hindeuten, dass eine Refaktorisierung erforderlich ist, um den Code lesbarer, wartbarer und skalierbarer zu machen. Hier sind einige der häufigsten Code Smells in Java-Programmen:

Duplizierter Code: Wenn der gleiche Code in mehreren Klassen oder Methoden vorliegt, ist dies ein Indiz dafür, dass der Code refaktorisiert werden sollte, um den Code lesbarer und wartbarer zu machen.

Überlange Methoden: Wenn eine Methode sehr lang ist, ist es schwierig, den Code zu verstehen und zu warten. Dies kann durch das Zerlegen der Methode in kleinere, einfacher zu verstehende Methoden gelöst werden.

Überlange Klassen: Wenn eine Klasse sehr viele Methoden und Felder enthält, kann dies ein Indiz dafür sein, dass die Klasse zu komplex ist und in kleinere Klassen aufgeteilt werden sollte.

Magischer Code: Wenn eine Klasse oder Methode schwer zu verstehen ist, weil sie magische Konstanten oder magische Zahlen enthält, kann dies ein Indiz dafür sein, dass der Code refaktorisiert werden sollte, um ihn lesbarer und wartbarer zu machen.

God Objects: Wenn eine Klasse sehr viele Verantwortungen hat und sehr komplex ist, kann dies ein Indiz dafür sein, dass die Klasse in kleinere Klassen aufgeteilt werden sollte, um den Code lesbarer und wartbarer zu machen.

Abhängigkeiten: Wenn eine Klasse oder Methode von vielen anderen Klassen oder Methoden abhängt, kann dies ein Indiz dafür sein, dass der Code refaktorisiert werden sollte, um die Abhängigkeiten zu minimieren und den Code wartbarer zu machen.

Es ist wichtig, regelmäßig auf Code Smells zu achten und den Code zu refaktorisieren, wenn dies erforderlich ist, um den Code lesbarer, wartbarer und skalierbarer zu machen.

# SOLID Principles

**SOLID** ist ein Akronym, das für fünf Prinzipien der objektorientierten Programmierung steht, die dazu beitragen, dass Code gut strukturiert, wartbar und einfach zu erweitern ist. Hier sind die fünf SOLID-Prinzipien:

**Single Responsibility Principle (SRP)**: Eine Klasse sollte nur eine Verantwortung haben, was bedeutet, dass sie nur für eine einzige Aufgabe zuständig sein sollte.

**Open/Closed Principle (OCP)**: Eine Klasse sollte offen für Erweiterungen sein, aber geschlossen für Änderungen. Das bedeutet, dass der Code erweitert werden kann, ohne den bestehenden Code zu ändern.

**Liskov Substitution Principle (LSP)**: Untertypen sollten in jeder Hinsicht mit ihren Basistypen kompatibel sein. Das bedeutet, dass ein Untertyp anstelle eines Basistyps verwendet werden kann, ohne dass dabei negative Auswirkungen auftreten.

**Interface Segregation Principle (ISP)**: Klassen sollten nur die Methoden implementieren müssen, die sie tatsächlich verwenden. Dies vermeidet, dass Klassen unnötigerweise mit Methoden belastet werden, die sie nicht verwenden.

**Dependency Inversion Principle (DIP)**: Abhängigkeiten sollten auf Abstraktionen statt auf konkreten Implementierungen ausgerichtet sein. Dies erleichtert die Wartung des Codes und ermöglicht es, Abhängigkeiten leicht zu ändern, wenn sich die Anforderungen ändern.

Diese fünf Prinzipien bilden die Grundlage für guten objektorientierten Code und helfen dabei, eine gut strukturierte, skalierbare und wartbare Anwendung zu erstellen. Es ist wichtig, sie bei der Entwicklung von Code im Hinterkopf zu behalten, um sicherzustellen, dass der Code gut strukturiert und einfach zu pflegen ist.

# Weiterführende Quellen

<a href="https://clean-code-developer.de" target="_blank"> Clean Code Developer (extern) </a> {{< de >}}
