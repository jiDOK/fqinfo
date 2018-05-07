## Loops

Ein Loop ist ein Teil eines Programmes, der sich eine Zeitlang in einer Schleife wiederholt.
Kann man sich so vorstellen, wie einen Musikloop oder eine Runde auf dem Karussell. 

Wenn man am Ende angekommen ist, fängt man vorne wieder an.

Allerdings versucht ein Loop, das so schnell wie möglich zu tun! Und zwar so lange bis eine bestimmte Bedingung erfüllt ist.
Das kann z.B. von eine Zähler-Variable abhängen, die mit jedem Durchlauf eins hochzählt. So tut es die klassische for-Schleife. 

```cs
for (int i = 0; i < 100; i++)
{
    // falls i < 100 ist, führe aus was hier steht, falls nicht, beende die Schleife
    Debug.Log("i hat den Wert " + i.ToString());
}

```

Ist die Bedingung erfüllt, dann endet die Schleife und es geht im Programm weiter.

Während ein Loop läuft kann nichts anderes passieren im Programm, weswegen sich hier eine große Gefahr von Crashes verbirgt.

## Loops und Arrays

Man kann mit einer for-Schleife sehr bequem durch ein Array durchsteppen. 

```cs
using UnityEngine;

public class Example : MonoBehaviour
{
    public GameObject[] gameObjects;// bitte im Editor füllen!

    void Start()
    {
        for (int i = 0; i < gameObjects.Length; i++)
        {
            gameObjects[i].transform.localScale = new Vector3(0.2f, 0.2f, 0.2f);
        }
    }
}

```

Die GameObjects sitzen einfach hintereinander in dem Array und haben einen bestimmten Index, beim Array immer von 0 aufsteigend:

```cs
GameObject[] gameObjects = new GameObject[8];
```

| Index | Name           |
| ----- | -------------- |
| 0     | gameObjects[0] |
| 1     | gameObjects[1] |
| 2     | gameObjects[2] |
| 3     | gameObjects[3] |
| 4     | gameObjects[4] |
| 5     | gameObjects[5] |
| 6     | gameObjects[6] |
| 7     | gameObjects[7] |

Wenn das i sich erhöht bekommen wir in unserer Schleife mit gameObjects[i] jeweils eine Referenz zum folgenden Objekt. Am Anfang, wenn i == 0 ist, bekommen wir gameObjects[0], beim nächsten Mal ist i == 1 und wir erhalten gameObjects[1] und so weiter. Wie man sieht, ist der letzte Index (7) genau eins kleiner als die Anzahl der vorhandenen Objekte. Deswegen steht in der Schleife oben i < gameObjects.Length als Bedingung, die 8 wäre schon zu hoch und wir wären out of range!

## Dimensionen

Das obige Array ist ein eindimensionales Array, es sitzen die Objekte in einer Reihe hintereinander. Manchmal kann es sinnvoll sein ein mehrdimensionales Array zu benutzen, zum Beispiel ein zweidimensionales Array, um ein Raster oder Grid zu erzeugen.

```cs
using UnityEngine;

public class Example : MonoBehaviour
{
    public int xLength = 4;
    public int yLength = 4;

    GameObject[,] gameObjectGrid;

    void Start()
    {
        gameObjectGrid = new GameObject[xLength, yLength];

        for (int x = 0; x < xLength; x++)
        {
            for (int y = 0; y < yLength; y++)
            {
                gameObjectGrid[x, y] = GameObject.CreatePrimitive(PrimitiveType.Cube);
            }
        }
    }
}

```


Ein Komma in den eckigen Klammern [,] bedeutet ein zweidimensionales Array, zwei Kommas  [,,] ein dreidimensionales Array usw.  
Die Struktur für zwei Dimensionen sieht so aus:

```cs
GameObject[,] gameObjectGrid = new GameObject[3,4];
```

|       | 0                   | 1                   | 2                   | 3                   |
| ----- | ------------------- | ------------------- | ------------------- | ------------------- |
| **0** | gameObjectGrid[0,0] | gameObjectGrid[1,0] | gameObjectGrid[2,0] | gameObjectGrid[3,0] |
| **1** | gameObjectGrid[0,1] | gameObjectGrid[1,1] | gameObjectGrid[2,1] | gameObjectGrid[3,1] |
| **2** | gameObjectGrid[0,2] | gameObjectGrid[1,2] | gameObjectGrid[2,2] | gameObjectGrid[3,2] |
| **3** | gameObjectGrid[0,3] | gameObjectGrid[1,3] | gameObjectGrid[2,3] | gameObjectGrid[3,3] |
| **4** | gameObjectGrid[0,4] | gameObjectGrid[1,4] | gameObjectGrid[2,4] | gameObjectGrid[3,4] |



 <br>



## Aufgabe

#### Helligkeit als Position

* Importiere ein Bild, z.B. aus dem Internet, als Textur in Unity. Optional das Seitenverhältnis noch anpassen (1:1)
* Schreibe ein Script, dieses soll:
  * ein Grid von Cubes instanziieren, als Primitives oder als Prefabs. Benutze dafür eine doppelte for-Schleife mit x und y
  * Die Textur an den x- und y-Punkten sampeln (Google: "unity sample texture pixel at point")
  *  und die Position des aktuellen Cubes[x,y] durch die Helligkeit der Textur setzen lassen.

Was könnte man noch tun mit dieser Technik? Können wir mit den Materialfarben der Cubes noch etwas anstellen? Kann man die Höhe auch invertieren?

<br>

<br>