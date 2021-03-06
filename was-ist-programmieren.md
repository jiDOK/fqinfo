# Was ist Programmieren? #

[//]: # "TODO: Bilder"

Beispiele aus dem Alltag:
## Die Eisbestellung ##
"Bitte nehme diesen Brief für mich mit zur Post. Auf dem Rückweg bringe mir doch bitte ein Eis mit, und zwar hätte ich gerne 2 Kugeln Vanille und eine Kugel Melone. Falls es Melone nicht zur Auswahl gibt, nehme ich stattdessen Erdbeere."
Wenn du einem Freund oder Verwandten einen solchen Auftrag gibst, bedeutet das, daß er oder sie Anweisungen von dir erhält, die in einer bestimmten Reihenfolge ausgeführt werden sollen (und daß du davon ausgehst, daß er das auch tut.) Das ist im Grunde schon Programmierung!
## Computer sind doof ##
Da deine Bekannten und Freunde intelligente Wesen sind, kannst du dich dabei auf die nötigsten Informationen beschränken. Du kannst vielleicht sogar davon ausgehen, daß du das Eis im Becher bekommst, weil derjenige weiß, daß du keine Eiswaffeln magst.
Ein Computer ist leider nicht so schlau. Alles muß man ihm haarklein erklären und für jede Eventualität vorsorgen, auf die er beim Ausführen der Anweisungen stoßen könnte.

## Der Algorithmus ##
Die gleiche Bestellung für einen Computer würde vom Konzept her eher folgendermaßen aussehen:

* Nehme Brief
* Fahre zur Post
* Gehe zum Briefkasten
* Werfe Brief in Briefschlitz
* Fahre zur Eisdiele
* Gehe zur Theke
* Bestelle 3 Kugeln im Becher, davon 2 Vanille, 1 Melone
* Wenn Melone nicht vorrätig: Bestelle 1 Vanille, 2 Schokolade
* Bezahle
* Fahre nach Hause
* Gebe Eis

Einen solcher Block gesammelter Anweisungen, die Schritt für Schritt auszuführen sind nennt man auch Algorithmus.
Jeder einzelne der oben aufgeführten Schritte ließe sich wieder in kleinere Teile zerlegen (Öffne Autotür, steige ein, stecke Schlüssel ins Zündschloß etc.)

Weitere Beispiele aus dem Alltag: Kochrezepte, Aufbauanleitung vom schwedischen Möbelhaus, Wecker stellen.
Unter diesen Beispielen ist der Wecker etwas besonderes, weil hier nicht ein anderer Mensch "programmiert" wird, sondern ein technisches Gerät. Der Wecker hat ein spezielles Interface (Knöpfe oder Drehknöpfe), das man benutzen muß, um ihn zu stellen. Bei einem Computer, nenn man so etwas API - Application Programming Interface.

## Variablen und Verzweigungen ##
Im oben beschriebenen Beispiel tauchen bereits zwei der wichtigsten Grundkonzepte der Programmierung auf: zum einen Verzweigungen und Bedingungen (*Conditional Statements*), zum anderen Variablen.
"Wenn Melone nicht vorrätig" ist ein Conditional Statement und je nach Ergebnis verzweigt sich das Programm in zwei verschiedene Pfade. Beim Bezahlen finden diese beiden *Paths* dann gleich wieder zusammen.
Die Variablen reagieren auf die Bedingung und erhalten je nach Pfad andere Werte: entweder 2 Vanille oder 1 Vanille, entweder Melone oder Schokolade. In einem Programm könnten sie beispielsweise numberOfScoops und scoopFlavour heißen. Eine andere Möglichkeit wäre es, die beiden zusammenzufassen. 

```cs
int scoopsVanilla = 500;
int scoopsMelon = 320;
```
<br>
<br>