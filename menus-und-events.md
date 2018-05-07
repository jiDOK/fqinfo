# Menus und Events #

## Message Hub gegen Spaghetti ##

Unity's UI-System bietet die Möglichkeit, auf jedem GameObject sehr einfach Methoden aufzurufen und sogar Variablen zu übergeben.

![](https://answers.unity.com/storage/temp/60681-rmouse-ui-77.png)

 Leider führt diese Einfachheit sehr schnell zu Spaghetti-Code - schlimmer als das: Spaghetti-Verknüpfungen im Editor. Für kleine und kleinste Projekte spielt dies keine Rolle, aber es ist gut, einen Ausweg aus der Situation zu kennen, falls es nötig wird.

Die sauberste mir bekannte Strategie ist es ein MessageHub-Script für alle UI-Events oder Gruppen von UI-Events zu erstellen.

Jedes Aktive UI-Element (Slider, Buttons, Checkboxes etc.) gibt seine Events an das MessageHub-Script weiter, das wiederum einzelne oder zusammengefaßte UnityEvents triggert. UnityEvents werden hinter den Kulissen auch von den UI-Elementen verwendet. Wir können diese jedoch auch selbst erstellen und auslösen ("invoken").

```cs
using UnityEngine;
using UnityEngine.Events;

public class MessageHub : MonoBehaviour
{
    public UnityEvent GoToPlayMode = new UnityEvent();
    
    void PlayButton()
    {
    	GoToPlayMode.Invoke();
    }
}
```

Sobald wir eine Referenz zu dem invokenden Script haben, können wir mit AddListener() das Event abonnieren. Wir übergeben eine Methode, die im Fall des Events ausgeführt werden soll.

```cs
using UnityEngine;

public class Listener : MonoBehaviour
{
    public MessageHub hub;

    void OnEnable()
    {
    	hub.GoToPlayMode.AddListener(OnPlayMode);
    } 
	
    public void OnPlayMode()
    {
        // Do Playmode-Stuff
    }
}
```

Wenn wir Daten übergeben wollen müssen wir etwas nervigen Boilerplate-Code schreiben. Dafür können wir dann das neue Event wieder und wieder verwenden.

```cs
using UnityEngine;
using UnityEngine.Events;

public class PointManager
{
	public MyIntEvent PointsChanged = new UnityEvent<int>();
	
    int points = 100;
	public int Points
    {
        get{ return points; }
        set
        {
            points = value;
            PointsChanged.Invoke(points);
        }
    }

[System.Serializable]
public class MyIntEvent : UnityEvent<int>
{
}

```

Dadurch, daß interessierte Objekte alle dem MessageHub zuhören statt vielen verteilten UI-Elementen, die nur im Editor sichtbar sind und sich selbst zum Abo an- und abmelden (subscriben), wird alles wesentlich übersichtlicher und die Koppelungen, obwohl lose, in Visual Studio sind mit einer Suche leicht zu finden. Loose Coupling ist eine für UI-Events allgemein empfohlene Strategie, so daß wir hier das beste beider Welten vereinen.
