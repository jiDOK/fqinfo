Zum Beginn eines neuen Projekts
===============================

Wenn wir ein neues Projekt starten, sollten wir verschiedene Einstellungen zur Konfiguration des Projektes vornehmen. 

* Vorüberlegung Rendering Path 
  * Vorüberlegung, welche Rendering Pipeline sich am besten eignet
  * wenn möglich bereits auswählen, kann aber auch noch nach der Prototyping-Phase geändert werden
* Global Illumination
  * In der Prototyping-Phase Realtime GI und Mixed GI komplett ausstellen
  * In jedem Fall Auto Generate Lighting ausstellen
* Skybox ggf. ausstellen / umstellen, Environment Lighting wählen (Skybox, Gradient, Color)
* Color Space auf Linear stellen ( _Edit > ProjectSettings > Player > Other >  Rendering > Color Space_ )
* Optional: Lighting Template erstellen
  * Eine Szene komplett ohne Lighting, Skybox usw. für Menus und Ähnliches
  * Eine Szene mit den Lighting-Einstellungen für eine normale Szene
  * Später kann die entsprechende Szene als Template geladen und unter neuem Namen gespeichert werden
* Unity auf C# 6 einstellen
  * .NET auf 4.6 stellen (_Edit > ProjectSettings > Player > Other Settings >  Configuration > Scripting Runtime Version_)
  * ggf. Developer Pack für 4.6 herunterladen (wird in Visual Studio automatisch vorgeschlagen)
* Ordner-Struktur erstellen (_Scenes, _Materials, _Scripts etc... )
* Bei allen wichtigeren oder größeren Projekten: Version Control starten 
  * Einstellungen für Version Control (Git) in _ProjectSettings > Editor_: 
    * Version Control Mode: Visible Meta Files 
    * Asset Serialization Mode: Force Text
  * ggf. Git LFS für größere Dateien wie Texturen, Videos etc. anschalten
  * Ersten Commit erstellen
* Assets und Helper importieren und falls möglich zur .gitignore hinzufügen um Platz in der Cloud zu sparen

Hint: Die meisten Licht- und GI-Einstellungen finden sich im Lighting Window ( _Window > Lighting > Settings_ )