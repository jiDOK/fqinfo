Steering Behaviours
===

Was sind Steering Behaviours?
---
Steering bedeutet Steuern, Behaviour ist das Verhalten. "Steering Behaviours for Autonomous Agents" ist der Titel eines Papers von Craig W. Reynolds, das 1997 begonnen und 1999 auf der GDC präsentiert wurde.

Es geht darin um Lenk- oder Steuerungsverhalten von "autonomen Agents", also die Simulation von selbständig handelnden Akteuren. Reynolds ließ sich unter anderem von dem Wissenschaftler Valentino Braitenberg inspirieren, dessen Forschungen sich im Grenzgebiet zwischen Hirnforschung, Psychologie und Kybernetik bewegten. Dieser hatte ein bekanntes Buch geschrieben, "Vehikel". Es befaßt sich mit roboterhaften Akteuren, deren Verhalten sehr real und selbstmotiviert erscheint, obwohl es durch simpelste Vorgaben bestimmt wird.

Solche Forschungen in Künstlicher Intelligenz wecken natürlich sofort das Interesse der Game Designer und A.I. Programmer.

Reynolds befaßt sich mit einem speziellen Teilbereich der K.I.(Künstlichen Intelligenz): Es geht ihm weniger um übergeordnete oder strategische Verhaltensweisen der simulierten Wesen, sondern eher um instinktive Bewegungsmanöver aus dem Moment heraus. Beispiele: einem anderen Vehikel oder Hindernis ausweichen, sich in einen Schwarm einfügen, jemanden verfolgen, vor jemandem fliehen, Essen suchen und aufheben, von Wind- oder Wasserströmungen erfaßt werden und so weiter. 

Um dies zu erreichen berechnet man in jedem Augenblick aus einem "Snapshot" der momentanen Situation verschiedene Lenk- oder Steuerungskräfte (Steering Forces), die sich dann am Ende kombinieren lassen und an das Bewegungsmodul weitergegeben werden. 

Eine sehr einfache Möglichkeit dafür, dies im Code zu erreichen: die resultierende Gesamt-Steering-Force zu der momentanen Velocity hinzu addieren. Dies geht ohne Probleme, weil beide Werte als Vektoren (`Vector3`) gespeichert sind.
```cs
velocity += steeringForce;
```

Der resultierende neue Geschwindigkeitsvektor muß dann nur noch zur momentanen World Position addiert werden:
```cs
transform.position += velocity;
```

Eine andere Möglichkeit ist es, die errechnete Steering Force an Unity's Physik Engine weiterzugeben zum Beispiel per `Rigidbody.AddForce()`, diese Methode möchte ebenfalls einen Vektor (Vector3) übergeben bekommen.

Steering Forces lassen sich sowohl in 2D als auch in 3D berechnen, allerdings sind sie ursprünglich mehr für die 2D-Welt konzipiert. Wenn man sie in 3D benutzt, ohne spezielle Vorkehrungen zu treffen, kann es passieren, daß Akteure im Boden versinken oder abheben. Es ist allerdings ohne weiteres möglich die Kräfte in 2D zu berechnen und dann auf eine 3D-Welt zu projizieren.

Der Algorithmus, um die einzelnen Steering Forces zu berechnen besteht aus zwei Teilen: 
Zunächst wird eine Desired Velocity (erwünschte Geschwindigkeit) berechnet. Dies kann sehr einfach vor sich gehen, oder komplexere Berechnungen erfordern. 

Hint: Velocity ist Geschwindigkeit als Vektor, also eine Verschiebung in eine bestimmte Richtung mit einer bestimmten Stärke (Vector Length oder Magnitude).

Dann wird diese Desired Velocity nachbearbeitet, mit der aktuellen Velocity verrechnet, noch einmal in ihrer Magnitude begrenzt und schließlich kann die resultierende Steering Force weiterverwendet werden, um z.B. ein Movement-Script anzutreiben.

Beispiel: Seek
---

Ein einfaches Steering Behaviour ist das Seek Behaviour, es simuliert den Wunsch des Akteurs, sofort ein bestimmtes Target aufsuchen zu wollen. Also beispielsweise will ein Rowdy-NPC (_Akteur_ oder _Vehicle_) zum Player (_Target_) rennen, um ihn zusammenzuschlagen. 

Dafür muß die Richtung vom NPC zum Player ausgerechnet werden:
```cs
Vector3 desired = player.transform.position - npc.transform.position;
```

<img src="https://cdn.rawgit.com/jiDOK/fqinfo/gh-pages/Images/SteeringBehaviours/SteeringBehaviours01.svg">

Note: Das Berechnen oder Auslesen einer solchen erwünschten Richtung kann von Steering Behaviour zu Steering Behaviour stark variieren. Das Flee Behaviour entspricht einem gespiegelten Seek Behaviour, andere Behaviours wie Wandering oder Path Following erfordern komplexere Algorithmen.

Statt die Richtung (`desired`, kurz für _Desired Direction_ oder _Desired Velocity_) nun ungefiltert als neue Velocity zu benutzen (was zur Folge hätte direkt ans Ziel zu teleportieren), wird sie in einen dreiteiligen Prozess eingespeist:

1 Sie wird normalisiert und auf eine bestimmte Länge gebracht. Diese Länge liegt als `float` vor und wird `maxSpeed` genannt. Sie soll hemmende Umwelteinflüsse wie z.B. Reibung auf einfache Weise repräsentieren. Schneller als mit dieser Magnitude kann der NPC / das Vehikel nicht reisen. Da wir annehmen, daß der Wunsch hinzurennen immer gleich groß ist, setzen wir den Vektor in jedem Fall auf `maxSpeed`. (Dies könnte man natürlich auch variieren und kleinere Werte zulassen.) 
```cs
float maxSpeed = 2f;
desired = desired.normalized * maxSpeed;
```

<img src="https://cdn.rawgit.com/jiDOK/fqinfo/gh-pages/Images/SteeringBehaviours/SteeringBehaviours02.svg">

2 Danach wird sie mit der aktuellen Velocity zusammengefaßt. Die derzeitige Geschwindigkeit darf also in die Berechnung der Steering Force (Lenkkraft) einfließen indem sie von unserer erwünschten Richtung abgezogen wird:
```cs
steeringForce = desired - velocity;
```

<img src="https://cdn.rawgit.com/jiDOK/fqinfo/gh-pages/Images/SteeringBehaviours/SteeringBehaviours03.svg">

Note: Diese Formel ist der Kern des Algorithmus für alle Steering Behaviours und ist für die weichen und natürlich wirkenden Bewegungskurven verantwortlich.

3 Zum Schluß wird die resultierende Kraft noch einmal beschränkt: Da weder Lebewesen noch Fahrzeuge unendliche Kraftreserven haben, darf das Resultat eine frei wählbare Obergrenze namens maxForce nicht überschreiten.
```cs
float maxForce = 0.5f;
steeringForce = Vector3.ClampMagnitude(steeringForce, maxForce);
```


<img src="https://cdn.rawgit.com/jiDOK/fqinfo/gh-pages/Images/SteeringBehaviours/SteeringBehaviours04.svg">


Dadurch wird auch die Trägheit oder Snappiness der Steuerung bestimmt.

Eine typische Art und Weise mit der Steering Force umzugehen, ist sie auf die aktuelle Velocity aufzurechnen.

```cs
velocity += steeringForce;
```

<img src="https://cdn.rawgit.com/jiDOK/fqinfo/gh-pages/Images/SteeringBehaviours/SteeringBehaviours05.svg">


Optional können mehrere Arten von Steering Behaviour zusammengerechnet werden. Um zu verhindern, daß sie sich gegenseitig neutralisieren, können sie zusätzlich gewichtet werden. 

Man kann sich sehr verschiedene Forces ausdenken. Von Wasser- und Windströmungen, über Obstacle Avoidance bis hin zu Flocking Behaviour oder Erdanziehungskräften können die unterschiedlichsten physikalischen und psychologischen Kräfte simuliert und kombiniert werden. Dies macht das System sehr flexibel und gut optimierbar für eine große Anzahl von Szenarios.

Links
---
Das Original-Paper von Craig W. Reynolds<br>
https://www.red3d.com/cwr/steer/gdc99/<br>
Gute Erklärung, ausführliche Übersicht und Implementation (Processing) von Dan Shiffman:<br>
http://natureofcode.com/book/chapter-6-autonomous-agents/<br>
