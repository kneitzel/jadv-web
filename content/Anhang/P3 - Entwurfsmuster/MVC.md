---
title: Model-View-Controller (MVC)
---

{{< toc >}}


## Model
Das Model enthält in erster Linie die Daten, die angezeigt werden bzw. die eingegeben werden. Die hier verwendeten Klassen können auch Business-Logik und andere Funktionalitätem beinhalten, aber diese spielen bei der Nutzung im MVC Pattern keien Rolle.

## View
Die View ist zuständig für das Anzeigen der Daten und die Entgegennahme von Anwender Aktionen. Um die Daten anzeigen zu können, kennt die View das Model. Auf die Aktionen des Anwenders reagiert die View selbst nicht. Statt dessen stellt die View diese Aktionen über das Observer-Pattern zur Verfügung. Weiterhin registriert sich die View als Observer bei dem Model um bei Veränderungen des Models die Anzeige anpassen zu können.

## Controller
Der Controller kennt das Model und die View. So stellt er alle benötigten Daten im Model zur Verfügung und stellt diese der View zur Verfügung. Um Aktionen des Anwenders verarbeiten zu können, registriert sich der Controller bei der View um die Events zu bearbeiten.