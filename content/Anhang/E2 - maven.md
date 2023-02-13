---
title: E2 - Maven (Übersicht)
---

Bei Maven handelt es sich um ein Build Tool, welches vor allem für Java Projekte eingesetzt wird (aber nicht auf Java beschränkt ist).

# Lifecycle

Maven ist Lifecycle basiert. Es gibt drei Lifecycle mit mehreren Schritten. Bei einem Maven Aufruf wird ein (oder mehrere) Ziel(e) angegeben. Maven arbeitet dann den entsprechenden Lifecycle ab bis einschließlich dem angegebenen Ziel.

## clean Lifecycle

Der clean Lifecycle dient der Bereinigung des Projektes und besteht aus den Zielen / Schritten:

| Ziel | Beschreibung |
| - | - |
| pre-clean | Führt Dinge aus, die vor der eigentlichen Bereinigung benötigt werden. |
| clean | Löscht alle Dateien, die durch vorherige Builds erzeugt wurden. |
| post-clean | Führt Dinge aus, um die Bereinigung abzuschließen. |

## site Lifecycle

Der site Lifecycle ist speziell für die Erstelluing von Webseiten erstellt worden. Der Lifecycle besteht aus den Zielen / Schritten


| Ziel | Beschreibung |
| - | - |
| pre-site | Führt Dinge aus, die vor der eigentlichen Site Generierung benötigt werden. |
| site | Erzeugt die Site. |
| post-site | Führt Schritte aus, die die Sit Generierung finalisieren. |
| site-deploy | Kopiert die Site zu dem angegebenen Webserver. |

## build (default) Lifecycle

Der Maven Build Lifecycle besteht aus mehreren Phasen, die in einer bestimmten Reihenfolge durchgeführt werden. Hier ist eine Übersicht über die wichtigsten Phasen:

validate: Überprüfung, ob das Projekt korrekt definiert ist und alle erforderlichen Informationen vorliegen.
compile: Kompilierung des Quellcodes.
test: Ausführung von Unit-Tests.
package: Erstellung eines ausführbaren Pakets (z. B. JAR oder WAR).
integration-test: Ausführung von Integrations-Tests.
verify: Überprüfung der Integrität des Pakets.
install: Installation des Pakets in den lokalen Maven-Repository.
deploy: Bereitstellung des Pakets in ein Remote-Repository, damit es von anderen Projekten verwendet werden kann.
Jede Phase kann spezifische Plugins aktivieren, die bestimmte Aktionen ausführen, um den Build-Prozess zu unterstützen. Jede Phase muss erfolgreich abgeschlossen werden, bevor die nächste Phase ausgeführt wird. Außerdem kann jede Phase übersprungen werden, indem man ein spezielles Ziel direkt aufruft, z. B. mvn install, um die Phasen validate bis install auszuführen.


| Ziel | Beschreibung |
| - | - |
| validate | Überprüfung, ob das Projekt korrekt definiert ist und alle erforderlichen Informationen vorliegen. |
| initialize | Initialisiert den Build (Setzt die Properties und erzeugt Verzeichnisse |
| generate-sources | Generiert Sourcen die bei der Übersetzung mit eingebunden werden |
| process-sources | Verarbeitet die Sourcen um z.B. Werte zu filtern. |
| generate-resources | Generiert Ressourcen die dann mit in das Paket eingebunden werden. |
| process-resources | Kopiert (und verarbeitet) die Ressourcen in das Zielverzeichnis |
| compile | Kompilierung des Quellcodes. |
| process-classes | Verarbeitet die fertig übersetzten Klassen z.B. für Bytecode Manipulationen. |
| generate-test-sources | Generiert Test Sourcen, die dann mit übersetzt werden. |
| process-test-sources | Verarbeitet die Test Sourcen um z.B. Werte zu filtern. |
| generate-test-resources | Erzeugt Ressourcen für die Tests. |
| process-test-resources | Kopiert (und verarbeitet) die Ressourcen in das Zielverzeichnis. |
| test-compile | Übersetzt die Test-Sourcen des Projektes |
| process-test-classes | Verarbeitet die fertig übersetzten Test-Klassen z.B. für Bytecode Manipulationen. |
| test | Ausführung von Unit-Tests. Diese Tests sollten nicht benötigt werden um das Paket zu bauen oder zu deployen (Test kann übersprungen werden!) |
| prepare-package | Fügt notwendige Schritte aus um die Paketierung vorzubereiten. |
| package | Baut das Paket in dem vorgegebenen Format z.B. als JAR File.|
| pre-integration-test | Führt Schritte aus, die notwendig sind um die Integrationstest durchzuführen. |
| integration-test | Führt die Integrationstest aus, d.h. kopiert und installiert das Paket in die Umgebung, in der die Integrationstest laufen sollen. |
| post-integration-test | Führt Schritte aus, die nach den Integrationstest laufen sollen z.B. der Bereinigung der Integrations-Umgebung. |
| verify | Überprüfung der Integrität des Pakets. |
| install | Installation des Pakets in den lokalen Maven-Repository. Damit steht es anderen Projekten des Entwicklers als Abhängigkeit zur Verfügung. |
| deploy | Bereitstellung des Pakets in ein Remote-Repository, damit es von anderen Projekten verwendet werden kann. Sollte in einem Integrations- und Produktionsumfeld ausgeführt werden. |

## Beispiele von Aufrufen

```mvn clean package```

Es werden die beiden Ziele clean und package angegeben. clean ist ein Ziel des clean Lifecycle und package vom build Lifecycle.
Daher durchläuft Maven hier erst den clean Lifecycle bis einschließlich clean: pre-clean, clean
Danacg wird der build lifecycle durchlaufen bis einschließlich package: validate, initialize, generate-sources, process-sources, generare-resources, process-resources, compile, process-classes, generate-test-sources, process-test-sources, generate-test-resources, process-test-resources, test-compile, process-test-classes, test, prepare-package, package

# Maven Wrapper

Der Maven Wrapper ist ein Mechanismus, der es ermöglicht, eine bestimmte Version von Maven in einem Projekt zu verwenden, unabhängig von den installierten Versionen auf einem System. Es besteht aus einer Reihe von Skripten und Konfigurationsdateien, die in einem Projekt bereitgestellt werden, um eine bestimmte Version von Maven zu verwenden, wenn das Projekt gebaut wird.

Der Maven Wrapper wird verwendet, um folgendes zu erreichen:

Reproduzierbarkeit: Indem eine bestimmte Version von Maven in einem Projekt verwendet wird, kann sichergestellt werden, dass dasselbe Ergebnis erzielt wird, unabhängig von den installierten Versionen auf einem System.

Konsistenz: Indem eine bestimmte Version von Maven in einem Projekt verwendet wird, kann sichergestellt werden, dass alle Entwickler dasselbe Verhalten und dieselben Ergebnisse erhalten.

Einfachheit: Durch die Verwendung des Maven Wrappers müssen Entwickler nicht selbst dafür sorgen, dass eine bestimmte Version von Maven installiert ist, was die Einrichtung des Projekts vereinfacht.

Insgesamt ermöglicht der Maven Wrapper eine bessere Kontrolle über die verwendete Version von Maven in einem Projekt und erleichtert die Reproduzierbarkeit, Konsistenz und Einrichtung des Projekts.


## Installation des Maven Wrapper

Den maven wrapper kann man über das Maven, welches eine Entwicklungsumgebung mit sich bringt, installieren über einen Aufruf
```mvn wrapper:wrapper```. In IntelliJ ist dies z.B. über das Maven Toolfenster möglich.

Sollte dies nicht direkt funktionieren, weil Maven das wrapper Plugin nicht kennt, so kann dieses in der POM eingefügt werden:
https://mvnrepository.com/artifact/org.apache.maven.plugins/maven-wrapper-plugin

Z.B. aktuell:
```xml
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-wrapper-plugin</artifactId>
    <version>3.1.1</version>
</plugin>
```

Nach der Installation des Maven Wrappers können wir im Projektverzeichnis die mvnw Scripte nutzen, um Maven zu starten. Beim Aufruf wird somit nur das mvn durch mvnw ersetzt (bzw. ./mvnw bei Unix und Mac Systemen).

Das heruntergleadene Maven findet sich dann im ~/.m2/wrapper Verzeichnis und wird auch von dort durch die Skripte gestartet.

# Maven Projekte

Jedes Maven Projekt sollte eindeutig identifizierbar sein. Identifiziert wird dabei ein Projekt über:

## groupId
Eine groupId identifiziert den Ersteller / Verantwortlichen für das Projekt. Dies kann eine Firma oder eien Gruppe sein. Wenn eine Gruppe / eine Person speziell ein Projekt bearbeitet, dann kann dies natürlich auch der Name des Projektes sein.

Da dies eindeutig sein sollte, ist es eine gute Idee, hier einen umgedrehten Domainnamen zu verwenden. So habe ich die Kontrolle über jadv.org, daher ist die groupId bei mir org.jadv.

Wenn man keine domain hat, über die man die Kontrolle hat, dann kann man prinzipiell
- direkt den Projektnamen verwenden (das könnte bei mir jadventure sein, prominente Beispiele sind z.B. JUnit, welche bei JUnit 4 noch junit als GroupId verwendet hat).
- es ist auch denkbar, eine bekannte Adresse zu nehmen, bei denen man einen Useraccount hat und da eben den Useraccount mit anzuhängen: com.github.kneitzel da ich bei github.com der user kneitzel bin.

**Dies ist aber natürlich nur wichtig, wenn ich mein Projekt auch veröffentlichen möchte. Da man dies aber nicht immer vorher weiss, macht es Sinn, hier von Anfang an einen gültigen Namen zu wählen.**

## artefactId

Die ArtefactId bezeichnet das Projekt und sollte innerhalb der groupId eindeutig sein. Der Projektname ist bei JAdventure, so dass ich den Namen in Kleinbuchstaben als artefactId gewählt habe.

## version
Jede Veröffentlichung sollte eine klare Version haben. Hier sind 2 - 4 Zahlen, getrennt durch Punkte, üblich.

An diese Version kann auch noch etwas angehängt werden. Dies findet man speziell für Alpha und Beta Versionen. Diese werden teilweise direkt als solche bezeichnet (-ALPHA, -BETA) oder es gibt Milestone Releases (-M1, -M2, ...). Hier gibt es aber keine festen Vorgaben.

Üblich ist aber ein -SNAPSHOT. Snapshot Versionen sind Versionen in der Entwicklung hin zu einer Version. 1.0.0-SNAPSHOT ist also eine Version die entwickelt wird und die später eine 1.0.0 werden soll.
Snaptshot Versionen dienen nur in der Entwicklung - wenn man mehrere voneinander abhängige Projekte entwickelt, dann bezieht man so eine Version mit ein, die in Entwicklung ist. **Diese Versionen sollten aber nie auf ein öffentliches Repository hochgeladen werden!**

## Project Object Model - POM

Ein Projekt wird in einer pom.xml beschrieben. Dabei handelt es sich um ein XML Dokument, dessen Struktur auch über eine Schema Definition beschrieben wurde.

### Minimales Projekt

Ein minimales Projekt beinhaltet lediglich die Modelversion und die Identifizierung des Projekts:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">

    <modelVersion>4.0.0</modelVersion>

    <groupId>org.jadv</groupId>
    <artifactId>jadventure</artifactId>
    <version>1.0-SNAPSHOT</version>
</project>
```

Damit es keine Probleme bezüglich der Kodierung der Dateien und der verwendeten Java Version gibt, sollten diese in den Properties immer klar angegeben werden: Dies geschieht in einem Properties-Block:

```xml
<properties>
    <maven.compiler.source>17</maven.compiler.source>
    <maven.compiler.target>17</maven.compiler.target>
    <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
</properties>
```

In diesen Beispiel Properties setzen wir die Java Version auf 17 und bestimmen, dass Code-Dateien in UTF-8 gespeichert wurden.

## Übergeordnetes Projekt

Jedes Projekt hat ein übergeordnetes Projekt - das sogenannte parent Projekt. Dies kann in der pom.xml angegeben werden:
```xml
<parent>
    <artifactId>artefact</artifactId>
    <groupId>group</groupId>
    <version>version</version>
</parent>
```

Das übergeordnete Projekt wird über artefactId, groupId und version eindeutig bestimmt. Die Details des Projekts werden dann aus dem Repository geladen und alle Einstellungen übernommen.

Sollte kein übergeordnetes Projekt angegeben werden, so wird die sogenannte Super POM als übergeordnetes Projekt genommen. Diese enthält eine erste Konfiguration z.B. die Festlegung, wo die Sourcen (src/main/java und src/test/java) und die Ressourcen (src/main/resourcen und src/test/resourcen) zu finden sind. Aber auch diverse Plugins werden eingebunden wie z.B. das Compiler Plugin.

## Module

Man kann untergeordnete Projekte haben. Dabei ist wichtig: Sobald ein Projekt untergeordnete Projekte, sogenannte Module, hat, kann das Projekt nichts anderes produzieren als eine eine pom mit Konfigurationen.
Zu den Modulen gehört also auch immer die Einstellung: ```<packaging>pom</packagiung>```

Bei der Angabe von Modulen muss es dann mit dem gleichen Namen ein Unterverzeichnis geben. Maven schaut dann in dem Unterverzeichnis nach einer pom.xml um diese ebenfalls zu bearbeiten. Üblich ist, dass diese Module dann das übergeordnete Projekt als Parent angeben. Dies ist aber nicht verpflichtend.

Die einzelnen Module sind in dem Element modules, so dass die Struktur so aussieht:
```xml
<packaging>pom</packagiung>
<modules>
    <module>someDir</module>
    <module>otherDir</module>
</modules>
```

Mit diesen Einträgen erwartet Maven die Unterverzeichnisse someDir und otherDir, die beide eine pom.xml enthalten müssen.

## Dependencies / DependencyManagement

Abhängigkeiten können verwaltet werden über ein Element dependencies. Jede Abhängigkeit wird mit groupId, archetypeId und Version definiert und Maven lädt die Abhängigkeit sowie alle davon abhängende Abhängigkeiten (transitive Abhängigkeiten).

Das Element dependencyManagement konfiguriert Abhängigkeiten ebenso wie das dependency Element mit der Ausnahme, dass die Abhängigkeit nur bekannt gemacht wird mit Version und ggf. einer Konfiguration (z.B. dem Verhindern, dass Abhängigkeiten mit geladen werden). Diese Abhängigkeit kann dann in folgenden Objekten verwendet werden, ohne Details anzugeben.

Wir können ein Beispiel konstruieren, dass in dem Paren Projekt eine Library festgelegt wird und dann das Unterprojekt nur noch die Abhängigkeit selbst angibt:

Im Parent Projekt findet sich:
```xml
<dependencyManagement>
    <dependencies>
        <dependency>
            <groupId>org.apache.logging.log4j</groupId>
            <artifactId>log4j-core</artifactId>
            <version>2.19.0</version>
        </dependency>
    </dependencies>
</dependencyManagement>
```

Im Modul wird dann die Abhängigkeit nur noch ohne Version angegeben:
```xml
<dependency>
    <groupId>org.apache.logging.log4j</groupId>
    <artifactId>log4j-core</artifactId>
</dependency>
```

Dieses Vorgehen findet sich in einigen Franeworks. Spring Boot erzeugt Projekte, die ein Spring-boot-starter Parent haben, das dann von sehr vielen Abhängigkeiten die Version definiert. Im eigenen Spring Boot Projekt wird dann beid en Abhängigkeiten keine Version mehr angegeben und so wird sicher gestellt, dass es durch unterschiedliche Versionen nicht zu Inkompatibilitäten und Problemen kommen kann.

## Plugins / Plugin DependencyManagement

In dem build Element wird der eigentliche Build konfiguriert. In Maven werden die eigentlichen Tätigkeiten immer durch Plugins durchgeführt. Das Super POM bindet bereits einige Plugins ein und weitere Plugins können dann auch noch eingebunden werden.

So wie bei dependencies ein dependencyManagement verfügbar ist, gibt es bei plugins auch ein pluginManagement. Hier kann bereits ein Plugin konfiguriert werden, ohne dass es direkt im Projekt verwendet wird. In untergeordneten Projekten kann das dann eingebunden werden, ohne die Version oder die Konfiguration noch einmal angeben zu müssen.