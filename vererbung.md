# Vererbung in der objekt-orientierten Programmierung #
## Hintergründe ##

Ein Konzept, das uns immer wieder begegnet, wenn wir uns mit Programmierung und Unity beschäftigen, ist das Konzept der Vererbung. 

Wie der Name es vielleicht erahnen läßt, ist es zumindest teilweise aus der Biologie und der biologischen Klassifizierung inspiriert und soll und soll dazu dienen, Programme robust und flexibel zu machen.

Den ursprünglichen Erfindern von OOP, wie Kristen Nygaard und Ole-Johan Dahl, ging es vor allem um die Nachbildung realer Objekte. Außerdem sollten Programmzeilen gespart werden: Objekte lassen sich wiederverwenden und durch Vererbung außerdem leicht zu spezialisierteren Versionen weiterentwickeln. Die Sprache an der die beiden arbeiteten, SIMULA, war für Simulationen (z. B. von physikalischen Prozessen) gedacht. 

Später kamen wichtige Einflüsse von dem amerikanischen Informatiker Alan Kay hinzu. Er hatte die Vision, ein Computersystem wie einen biologischen Körper zu gestalten, Programme sollten sich wie Zellen verhalten, die zwar eigenständig, aber dennoch Teil eines großen Ganzen sind.

Solche Visionen traten später ein wenig zugunsten pragmatischer Ansätze und Kompromisse zurück, sie bleiben jedoch wichtiger Teil der objekt-orientierten Philosophie.

In der biologischen Vererbung sehen wir, daß Eigenschaften der Eltern von ihren Kindern übernommen werden. Genauso funktioniert es auch in der Programmierung. Konkret bedeutet dies, wenn eine Klasse von einer anderen Klasse erbt, dann stehen alle nicht privaten Member (z.B. Variablen und Methoden) auch der Kindklasse zur Verfügung.

Note: Die Vererbung (englisch _Inheritance_) gilt als eine der drei (manchmal vier) Säulen der OOP. Trotzdem wird sie in vielen Fällen heutzutage eher vermieden ("Composition over Inheritance")

## Das Grundkonzept ##

Wenn wir eine neue Klasse in C# schreiben, versuchen wir eine für unsere Zwecke sinnvolle Einheit zu erzeugen. Oft ist diese einem echten Objekt/Ding/Wesen nachgebildet, kann aber auch ein rein abstraktes Konstrukt sein. So hat ein Enemy oder ein CeilingLight Vorbilder in der realen Welt, wärend ein InputWrapper, CollisionManager oder PoemGenerator etwas eher abstraktes darstellen. 

Eine solche Einheit kann weiterhin entweder alle relevanten Eigenschaften und Funktionen vollständig in dem Code-Objekt vereinen, oder aber nur einen Teil davon repräsentieren. Letzteres wäre dann eine modularere Herangehensweise, normalerweise als Composition bezeichnet. Das eigentliche Objekt würde sich in diesem Fall aus mehreren Teilobjekten zusammensetzen. In Unity könnten wir ein langes Enemy-Script zum Beispiel in Movement-, Weapon-, Health-Scripts etc. unterteilen, die dann nebeneinander auf dem GameObject liegen. 

Dies ermöglicht es, die Teile neu zu kombinieren, um Variationen oder ganz neue Objekte zu erhalten. Das Health-Script könnte zum Beispiel auf dem Enemy, dem Player und vielleicht sogar auf einer zerstörbaren Wand liegen, wenn es abstrakt genug gestaltet ist. Das Health-Script würden sich dann alle drei Objekte teilen, während das Movement auf der Wand fehlen würde und der Player ein ganz eigenes PlayerMovement-Script besitzen könnte, das sich erheblich von EnemyMovement unterscheidet.

Für solche wiederverwendbaren Komponenten bietet sich eine gewisse Abstraktion an, damit ihr Konzept für möglichst viele Situationen paßt (BattleBehaviour auf EnemySoldier und BattleBehaviour auf SaberToothTiger) aber gleichzeitig müssen möglicherweise gewisse Details berücksichtigt werden: Im BattleBehaviour existiert beispielsweise eine Attack()-Methode, aber der EnemySoldier kann vielleicht schießen und boxen, während der Tiger brüllend und beißend nach vorne springt. 

Vererbung ist eine Möglichkeit, hier die notwendige Variation zu erzeugen, so daß ein anderes Script bei beiden einfach die von der Elternklasse garantierte Attack()-Methode aufrufen kann, ohne sich um die Details kümmern zu müssen. Dieses Konzept, daß die Eltern ein Verhalten garantieren, nennt sich Polymorphie ("Vielgestaltigkeit"). Die Kinder haben unterschiedliche, vielgestaltige Implementationen des entsprechenden Verhaltens.

## Die Implementierung ##

Angenommen wir haben die Klasse BattleBehaviour mit einer Attack()-Methode. Standardmäßig werden ein paar Energiepunkte abgezogen.
```cs
public class BattleBehaviour
{
	protected int stamina = 25;
    public virtual void Attack()
    {
        stamina--;
    }
}
```
Wenn jetzt ein Kind von dieser Klasse erbt, stehen die public und protected Variablen und Methoden zur Verwendung bereit. Außerdem kann das Kind eigenes Verhalten hinzufügen. Je nach Wunsch kann das Verhalten des Kindes das Elternverhalten ersetzen oder ergänzen.

```cs
public class TigerBattleBehaviour : BattleBehaviour
{
    public override void Attack()
    {
        base.Attack();// Ruft die Elternmethode auf
        Debug.Log("Jumping and Roaring!!");// Fügt eigenes Verhalten hinzu
    }
}

public class SuperSoldierBattleBehaviour : BattleBehaviour
{
    public override void Attack()
    {
        Debug.Log("Super Soldiers don't lose stamina!");
        Debug.Log("Bang! Pow!");
    }
}
```
Oft taucht auch die Situation auf, daß die Elternklasse zwar Gemeinsamkeiten der Kinder zusammenfassen, aber selbst nicht instanziiert werden soll. Zum Beispiel könnte es eine Überklasse ElectricalGadget geben, daß Methoden zum zerstören, reparieren, anschalten, eine Wattzahl, einen Preis und ähnliches bereit hält, deren Exemplare aber nur in konkreteren Formen wie Telefon, Mixer und Toaster vorkommen sollen. Da bietet sich dann eine abstrakte Klasse an. Hauptmerkmal einer abstrakten Klasse ist eben, daß sie selbst nicht instanziiert werden kann. Ihre public und protected Member (Variablen, Properties, Methoden...) stehen zur Verfügung, virtuelle Member können überschrieben,  abstrakte Member _müssen_ überschrieben/implementiert werden. 

Abstrakte Member können nur in einer abstrakten Klasse stehen und stellen so etwas wie einen Vertrag dar: Wer von solch einer Klasse erbt, muß die abstrakten Member implementieren, so ist garantiert, daß diese vorhanden und benutzbar sind (andernfalls gibt es einen Compiler-Error und das Programm wird nicht laufen).

```cs
public abstract class Enemy
{
    // Anders als Field-Variablen können Properties abstract sein
    // Stamina muß öffentlich les- und schreibbar implementiert werden
    public abstract int Stamina { get; set; }
    // BattleBehaviour muß öffentlich lesbar implementiert werden
    public abstract BattleBehaviour { get; }
}
```

Wenn eine Klasse ein Blueprint für ein konkretes Objekt ist (Man denke an den Bauplan eines Reihenhausarchitekten und die daraus entstehenden Häuser), dann ist die abstrakte Klasse vielleicht so etwas wie eine gesetzliche Regelung zur Erstellung von Blueprints. Jeder Bauplan vom Typ _VorstadthausNord_ muß eine Regenrinne und einen Deichbereich vorsehen. Jeder Burgplan ohne Verlies ist ungültig usw. Dies regelt die abstrakte Elternklasse.

Abstrakte Klassen lassen uns Polymorphie nutzen, aber es gibt noch einen weiteren Weg: Composition - umgesetzt mit Interfaces. Dazu jedoch später mehr.

## Links ##
Linnes biologische Klassifizierung:
https://de.wikipedia.org/wiki/Systema_Naturae
Vortrag von Alan Kay aus den 80ern, wo er über OOP, Zellen u. biologische Systeme spricht:
https://youtu.be/QjJaFG63Hlo?t=770
Um das Video stereo zu machen:
https://addons.mozilla.org/en-US/firefox/addon/soundfixer/
Vererbung, virtuelle und abstrakte Member, und Polymorphie:
https://stackoverflow.com/questions/17717570/why-does-calling-a-method-in-my-derived-class-call-the-base-class-method
Erweitertes Beispiel aus dem letzten Link im interaktiven Code Editor:
https://dotnetfiddle.net/7GLO6S
Soldier- und Tiger-Beispiel in der gleichen Sandbox:
https://dotnetfiddle.net/1SsNqX