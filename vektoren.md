[gimmick: math]()
Vektoren
========

Von hier nach da, relativ
-------------------------

Ein Vektor beschreibt eine Verschiebung im Raum. Vektoren haben eine Richtung und eine Länge, auch Magnitude genannt.
Am einfachsten kann man sich Vektoren als Pfeile vorstellen, die in eine bestimmte Richtung zeigen, und so werden sie auch meist grafisch dargestellt.

<img src="https://cdn.rawgit.com/jiDOK/FQ1Wiki/master/VectorsSVG/Vektoren01.svg">

Wir benutzen Vektoren in unseren zwei und dreidimensionalen Koordinatensystemen, um beispielsweise Richtungen, Geschwindigkeiten, oder Positionen anzugeben.

Übrigens hat ein Vektor selbst eigentlich keine Position, er ist eine rein relative Größe. Man legt daher einen Nullpunkt (Origin) fest, auf den sich dann ein Ortsvektor (Position Vector) beziehen kann. Der Ortsvektor zeigt vom Nullpunkt aus auf die entsprechende Position.

In Unity und C# notieren wir die Vektoren in Koordinatenschreibweise. Das heißt wir geben als Komponenten die Werte an, die er auf der entsprechenden Achse annimmt. Z.B. `new Vector3(2f, 4f, 0f)`. Der Vektor \\( \vec  v = (2, 4, 0) \\) beschreibt einen Punkt, der um 2 Einheiten auf der X-Achse, 4 Einheiten auf der Y-Achse und 0 Einheiten auf der Z-Achse verschoben ist. Verschoben - aber von wo aus? Das ist flexibel, es kann die Verschiebung vom Nullpunkt oder von einem beliebiegen anderen Punkt gemeint sein.

Im diesem Sinne kann man einen Vektor auch einfach als ein mathematisches Objekt sehen, das eine Ansammlung von Zahlen, nämlich seine Komponenten, beherbergt. Die Bedeutung bleibt dabei offen. So läßt sich ein dreidimensionaler Vektor auch benutzen um beispielsweise Farben (RGB) oder Rotationen auszudrücken. Bei räumlichen Vektoren werden die Komponenten meist x und y (2D) oder x, y und z (3D) genannt.

Addition
--------

### Vektor plus Vektor gleich Vektor

Bei der Addition von Vektoren kommt auch wieder ein Vektor heraus. Die Addition von Vektoren ist rechnerisch sehr simpel, es werden einfach jeweils die gleichnamigen Komponenten addiert:
$$ (a_x, a_y) + (b_x, b_y) = (a_x + b_x, a_y + b_y) \$$
Also zum Beispiel:

\\( (5, 1) + (3, 9) = (8, 10) \\)

Diese Addition von zwei Vektoren entspricht der Hintereinanderausführung der zugehörigen Verschiebungen

<img src="https://cdn.rawgit.com/jiDOK/FQ1Wiki/master/VectorsSVG/Vektoren02.svg">

Dieses Prinzip des Hintereinander gilt auch für die Aufteilung auf die jeweiligen Komponenten. Es ist möglich zunächst nur auf der X-Achse, dann nur auf der Y-Achse zu verschieben:

<img src="https://cdn.rawgit.com/jiDOK/FQ1Wiki/master/VectorsSVG/Vektoren04.svg">

\\( (0, 0) + (5, 0) + (3, 0) + (0, 1) + (0, 9) = (8, 10) \\)

Subtraktion
-----------

Die Subtraktion läuft nach dem gleichen Schema ab.

\\( (5, 1) - (3, 9) = (2, -8) \\)

In der grafischen Darstellung muß der abgezogene Vektor natürlich in die Gegenrichtung weisen -  ein negativer Vektor zeigt immer in die exakt entgegengesetzte Richtung seiner positiven Version.

<img src="https://cdn.rawgit.com/jiDOK/FQ1Wiki/master/VectorsSVG/Vektoren03.svg">

Wenn man einen Vektor mit negativen Komponenten addiert, passiert das gleiche wie sonst beim Rechnen mit negativen Zahlen auch:

\\( (-3, 8, 2) + (-2, -8, 1) = (-5, 0, 3) \\)

Multiplikation, Division
------------------------

### Vektor mal Zahl oder Vektor oder wie?

Bei der Multiplikation ergibt sich ein anderes Bild: Wenn man den Vektor mit einer Zahl, einem sogenannten Skalar multipliziert, kommt wieder ein Vektor heraus. Der hat die gleiche Richtung wie das Original, aber eine andere Länge. Auch bei der Multiplikation werden wieder die einzelnen Komponenten isoliert betrachtet.

\\( (1, 3) * 3 = (3, 9) \\)

Der Vektor ist nun dreimal so lang.
Rückwärts funktioniert es auch:

\\( (3, 9) / 3 = (1, 3) \\)

Auch die negativen Zahlen bieten keine Überraschungen:

\\( (-5, 4) * -2 = (10, -8) \\)

Der Vektor ist nun doppelt so lang allerdings in entgegengesetzter Richtung.

<img src="https://cdn.rawgit.com/jiDOK/FQ1Wiki/master/VectorsSVG/Vektoren05.svg">

Dieses Prinzip des Multiplizierens mit einem Skalar wird Skalierung (Englisch: Scaling) genannt.

Wenn man jedoch einen Vektor mit einem anderen Vektor multiplizieren will ergeben sich verschiedene Möglichkeiten.
Die Möglichkeit, die uns zunächst interessieren soll, ist das Dot Product, auf Deutsch etwas verwirrend Skalarprodukt genannt. 

Das Dot Product
---------------

Hier kommt als Ergebnis eine einfache Zahl - ein Skalar - heraus.

<a href="https://www.codecogs.com/eqnedit.php?latex=\large&space;a&space;\cdot&space;b&space;=&space;a_x&space;*&space;b_x&space;&plus;&space;a_y&space;*&space;b_y" target="_blank"><img src="https://latex.codecogs.com/svg.latex?\large&space;a&space;\cdot&space;b&space;=&space;a_x&space;*&space;b_x&space;&plus;&space;a_y&space;*&space;b_y" title="\large a \cdot b = a_x * b_x + a_y * b_y" /></a>

<a href="https://www.codecogs.com/eqnedit.php?latex=\large&space;c&space;\cdot&space;d&space;=&space;c_x*d_x&space;&plus;&space;c_y*d_y&space;&plus;&space;c_z*d_z" target="_blank"><img src="https://latex.codecogs.com/svg.latex?\large&space;c&space;\cdot&space;d&space;=&space;c_x*d_x&space;&plus;&space;c_y*d_y&space;&plus;&space;c_z*d_z" title="\large c \cdot d = c_x*d_x + c_y*d_y + c_z*d_z" /></a>

Wie man sieht ist diese Operation keine reine Multiplikation, sondern beinhaltet auch das Addieren der Zwischenergebnisse.
Obwohl diese Rechnung erst einmal ziemlich zufällig und rätselhaft wirkt ist sie eine der wichtigsten Aktionen, die wir mit Vektoren anstellen können.

Das Dot Product hat die magische Eigenschaft, uns mitzuteilen, "wie sehr" zwei Vektoren in die gleiche Richtung zeigen. Zeigen sie in die gleiche Richtung, ist das Dot Product positiv. Stehen sie senkrecht aufeinander, ist das Dot Product 0. Zeigen sie in entgegengesetzte Richtungen, ist das Dot Product negativ. Wenn man die Vektoren normalisiert, läßt sich sogar der exakte Winkel bestimmen!

