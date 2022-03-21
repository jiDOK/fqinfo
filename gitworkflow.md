Git Workflow
===

Zunächst müssen wir Git herunterladen von https://git-scm.com/

<img src="https://raw.githubusercontent.com/jiDOK/fqinfo/gh-pages/Images/GitWorkflow/Git01.png?sanitize=true">
<img src="https://raw.githubusercontent.com/jiDOK/fqinfo/gh-pages/Images/GitWorkflow/Git02.png?sanitize=true">

Dann installieren mit den folgenden Einstellungen:


<img src="https://raw.githubusercontent.com/jiDOK/fqinfo/gh-pages/Images/GitWorkflow/Git04.png?sanitize=true">
<img src="https://raw.githubusercontent.com/jiDOK/fqinfo/gh-pages/Images/GitWorkflow/Git05.png?sanitize=true">
<img src="https://raw.githubusercontent.com/jiDOK/fqinfo/gh-pages/Images/GitWorkflow/Git06.png?sanitize=true">
<img src="https://raw.githubusercontent.com/jiDOK/fqinfo/gh-pages/Images/GitWorkflow/Git07.png?sanitize=true">
<br>
Hier sind beide Versionen ok:
<br>
<img src="https://raw.githubusercontent.com/jiDOK/fqinfo/gh-pages/Images/GitWorkflow/Git08.png?sanitize=true">
<img src="https://raw.githubusercontent.com/jiDOK/fqinfo/gh-pages/Images/GitWorkflow/Git09.png?sanitize=true">
<img src="https://raw.githubusercontent.com/jiDOK/fqinfo/gh-pages/Images/GitWorkflow/Git10.png?sanitize=true">
<img src="https://raw.githubusercontent.com/jiDOK/fqinfo/gh-pages/Images/GitWorkflow/Git11.png?sanitize=true">
<img src="https://raw.githubusercontent.com/jiDOK/fqinfo/gh-pages/Images/GitWorkflow/Git12.png?sanitize=true">
<img src="https://raw.githubusercontent.com/jiDOK/fqinfo/gh-pages/Images/GitWorkflow/Git13.png?sanitize=true">
<img src="https://raw.githubusercontent.com/jiDOK/fqinfo/gh-pages/Images/GitWorkflow/Git14.png?sanitize=true">
<img src="https://raw.githubusercontent.com/jiDOK/fqinfo/gh-pages/Images/GitWorkflow/Git15.png?sanitize=true">
<img src="https://raw.githubusercontent.com/jiDOK/fqinfo/gh-pages/Images/GitWorkflow/Git16.png?sanitize=true">
<img src="https://raw.githubusercontent.com/jiDOK/fqinfo/gh-pages/Images/GitWorkflow/Git17.png?sanitize=true">
<img src="https://raw.githubusercontent.com/jiDOK/fqinfo/gh-pages/Images/GitWorkflow/Git18.png?sanitize=true">
<img src="https://raw.githubusercontent.com/jiDOK/fqinfo/gh-pages/Images/GitWorkflow/Git19.png?sanitize=true">
<br>
Nun dieses Zip-File herunterladen: 
<br>
https://gist.github.com/jiDOK/58b5b22ed9377fd02e76c876abb00846
<br>
Dann entzippen und die beiden Dateien in den Unity-Projektordner kopieren.

<img src="https://raw.githubusercontent.com/jiDOK/fqinfo/gh-pages/Images/GitWorkflow/Git20.png?sanitize=true">
Die .gitignore-Datei schließt gewisse Ordner und Dateitypen vom Tracking aus.<br>
Die .gitattributes-Datei bestimmt die Dateitypen für das LFS-System (welche Dateien als große Dateien behandelt werden.)
<br>
Jetzt einen Rechtsklick in den Projektordner und "Git Bash here" auswählen.
<img src="https://raw.githubusercontent.com/jiDOK/fqinfo/gh-pages/Images/GitWorkflow/Git21.png?sanitize=true">
<br>
Im Git-Bash-Fenster zunächst die Konfiguration für Username und User-E-Mail anlegen, hier ein Beispiel mit Phantasienamen:
```plaintext
git config --global user.name "SuperMonsterCoffee"
```

```plaintext
git config --global user.email "monsterhunter3d@beispiel.de"
```

Dann können wir die folgenden Befehle nacheinander ausführen lassen:
<br>
```plaintext
git init
```
```plaintext
git lfs install
```
```plaintext
git add -A
```
```plaintext
git commit -m "first commit"
```
Wenn wir dann ``git status`` eingeben, sollte alles OK sein ("``nothing to commit, working tree clean``")
<br>
Dann auf gitlab.com gehen und einloggen. 

Ein neues leeres Projekt anlegen, am Besten mit dem gleichen Namen wie das Unityprojekt.
<img src="https://raw.githubusercontent.com/jiDOK/fqinfo/gh-pages/Images/GitWorkflow/Git22.png?sanitize=true">
<img src="https://raw.githubusercontent.com/jiDOK/fqinfo/gh-pages/Images/GitWorkflow/Git23.png?sanitize=true">
<img src="https://raw.githubusercontent.com/jiDOK/fqinfo/gh-pages/Images/GitWorkflow/Git24.png?sanitize=true">
Warning: Kein Readme hinzufügen!

Dann die URL kopieren unter Clone With HTTPS
<img src="https://raw.githubusercontent.com/jiDOK/fqinfo/gh-pages/Images/GitWorkflow/Git25.png?sanitize=true">

Im Git Bash 
``plaintext
git remote set origin
``
schreiben und dann mit einem Middle Mouse Button Click die eben kopierte URL dahinter einfügen. In meinem Beispiel sähe das so aus:

```plaintext
git remote add origin https://gitlab.com/jiDOK1/gpcoding-22-03.git
```
Bei euch wäre die URL natürlich anders.

Nun folgt noch der Command um es in die Cloud hochzuladen und verknüpfen

```plaintext
git push -u origin master
```
Gegebenenfalls muß man Nutzername und Kennwort für Gitlab ausfüllen.
Wenn die Projektseite auf gitlab.com aktualisiert wird, sollte nun die Projektstruktur sichtbar sein (Assets-Ordner usw.)
<img src="https://raw.githubusercontent.com/jiDOK/fqinfo/gh-pages/Images/GitWorkflow/Git26.png?sanitize=true">

