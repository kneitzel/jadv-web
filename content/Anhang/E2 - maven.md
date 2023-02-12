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

Im build oder default Lifecycle wird das ganze Projekt gebaut. Die Ziele / Schritte des build Lifecycle sind:

| Ziel | Beschreibung |
| - | - |
| validate | Validiert, dass das Projekt korrekt ist und alle notwendigen Informationen angegeben wurden. |
| initialize | Initialisiert den Build (Setzt die Properties und erzeugt Verzeichnisse |
| generate-sources | Generiert Sourcen die bei der Übersetzung mit eingebunden werden |
| process-sources | Verarbeitet die Sourcen um z.B. Werte zu filtern. |
| generate-resources | Generiert Ressourcen die dann mit in das Paket eingebunden werden. |
| process-resources | Kopiert (und verarbeitet) die Ressourcen in das Zielverzeichnis |
| compile | Übersetzt die Sourcen des Projektes |
| process-classes | Verarbeitet die fertig übersetzten Klassen z.B. für Bytecode Manipulationen. |
| generate-test-sources | Generiert Test Sourcen, die dann mit übersetzt werden. |
| process-test-sources | Verarbeitet die Test Sourcen um z.B. Werte zu filtern. |
| generate-test-resources | Erzeugt Ressourcen für die Tests. |
| process-test-resources | Kopiert (und verarbeitet) die Ressourcen in das Zielverzeichnis. |
| test-compile | Übersetzt die Test-Sourcen des Projektes |
| process-test-classes | Verarbeitet die fertig übersetzten Test-Klassen z.B. für Bytecode Manipulationen. |
| test | Führt die Tests aus. Diese Tests sollten nicht benötigt werden um das Paket zu bauen oder zu deployen (Test kann übersprungen werdn!) |
| prepare-package | Fügt notwendige Schritte aus um die Paketierung vorzubereiten. |
| package | Baut das Paket in dem vorgegebenen Format z.B. als JAR File.|
| pre-integration-test | Führt Schritte aus, die notwendig sind um die Integrationstest durchzuführen. |
| integration-test | Führt die Integrationstest aus, d.h. kopiert und installiert das Paket in die Umgebung, in der die Integrationstest laufen sollen. |
| post-integration-test | Führt Schritte aus, die nach den Integrationstest laufen sollen z.B. der Bereinigung der Integrations-Umgebung. |
| verify | Schritte um sicher zu stellen, dass das gebaute Paket gültig ist und den Qualitätsansprüchen genügt. |
| install | Installiert das Paket im lokalen Repository. Damit steht es anderen Paketen als Abhängigkeit zur Verfügung. |
| deploy | Sollte in einem Integrations- und Produktionsumfeld ausgeführt werden. Kopiert das finale Paket in ein entferntes Repository um es anderen Entwicklern zugängig zu machen. |

# Maven Wrapper

