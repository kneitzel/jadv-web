---
title: DRY - Don't Repeat Yourself
---

{{< toc >}}

Eine Fehlerquelle kann doppelter Code sein. Wenn etwas mehrfach im Code umgesetzt wurde, dann besteht die Gefahr, dass bei der Notwendigkeit einer Änderung nicht alle Stellen geändert werden.

Desweiteren wird der Code dadurch unnötig aufgebläht und damit unübersichtlicher.

# Doppelten Code erkennen

Im einfachsten Fall weist einen die Entwicklungsumgebung auf doppelten Code hin. IntelliJ markiert dann den Anfang eines Blockes und zeigt die Warnung an, dass die nächsten x Zeilen an anderer Stelle noch einmal vorkommen.

Aber wenn man die Augen aufhält und aktiv nach doppeltem Code sucht, dann findet man auch immer mehr Stellen, bei denen eine Funktionalität doppelt ist.

# Doppelten Code eliminieren

Doppelten Code zu eliminieren ist in der Regel nicht besonders schwer. Oft reicht es schon aus, die betreffenden Zeilen in eine eigene Methode auszulagern und dann diese Methode aufzurufen.

Es kann aber auch durchaus einige Komplexität hinzu kommen, die dann weitergehende Schritte erfordert.

So kann es erforderlich sein:
- Komplexe Parameter zu nutzen (z.B. Functgion, BiFunction oder andere Interfaces)
- Über Vererbung eine Klassenhirarchie aufzubauen
- für unterschiedliche Typen Generics zu verwenden.

Ein Beispiel für so eine Lösung findet sich in Lektion 2 unter 2.4.

