# Github Rezept

## Einige Infos
### Was ist Git?
Das subversion tool. Das Programm. Die Technologie. Git ist nicht dasselbe wie Github.
### Was ist Github?
Der Host. Die Cloud. Alternativ gibt es auch Gitlab.
### Was ist ein Repository?
Ein Repository ist ein abgekapseltes Projekt - wie ein einzelner Server auf einem Github Account (wie zBs. opengisch, signedav oder qgis)
### Wofür ist Git und Github etc. im Gegensatz zu einer Cloud?
- Bei Github trackt man alle Änderungen (mit manueller Beschreibung).
- Bei Github pusht man aktiv (manuell) Änderungen.
- Github ermöglicht aktive (kontrolliert vom User) Konfliktlösung.
### Arbeite ich online?
Auch wenn es möglich ist über den Browser Dateien in Github zu ändern, zieht man sich üblicherweise das Repository lokal in einen Ordner. Arbeitet dort, speichert dort, commitet dort (trackt einzelne Änderungen) und pusht schliesslich wieder auf das Online Repository.
### Was ist ein Github Account 
- Ein Account pro User
- User können selbst Repositories führen oder man kann Organisationen gründen
- Organisationen (zBs. opengisch) kann auch Repositories führen
### Konsole 
Es ist am einfachsten, diese Github Kommandos lokal auf einem Terminal/Konsole auszuführen. Das ist eine textbasierte Steuerung des Betriebssystems. Hier einige Commandos:

```bash
# Auflisten des Inhalts in meinem Documents Verzeichnis mit: ls -l
dave@windows ~/Documents
$ ls -l
total 2
drwxrwxr-x  3 dave dave 4096 Jan 17 14:13 flyingtapir
drwxrwxr-x  4 dave dave 4096 Mär 22 11:47 arbeiten

# In ein Verzeichnis gehen mit: cd <verzeichnis>
dave@windows ~/Documents
$ cd arbeiten
dave@windows ~/Documents/arbeiten

# Zurück gehen mit: cd ..
dave@windows ~/Documents/arbeiten
$ cd ..
dave@windows ~/Documents

# Neues Verzeichnis erstellen mit: mkdir <verzeichnis>
dave@windows ~/Documents
$ mkdir github_repos
```

## 1. Repository "klonen": Wie ich das Repository auf meinen Computer bringe

Das Repository von Github musst du nun bei dir lokal haben. Dafür musst du es "klonen". Die zu "klonende" URL findest du auf Github:
![image](https://user-images.githubusercontent.com/28384354/226886694-632c1fb5-c307-4bd6-a2e0-c729f93cb413.png)


Und dann "klonst" du mit dem Git-Kommando `git clone` in deiner Konsole:

```bash
# Repository klonen
dave@windows ~/Documents/github_repos
$ git clone git@github.com:signedav/github-cookbook.git
```

Wenn es ein neues Repository war, dann kommt noch die Warnung, dass es ein leeres Repository ist - das ist okay.

Anschliessend hast du einen neuen Ordner erstellt mit dem Namen des Repositories:
```bash
dave@windows ~/Documents/github_repos
$ ls -l
total 8
drwxrwxr-x 2 dave dave 4096 Mär 22 11:47 erster_ordner
-rw-rw-r-- 1 dave dave 2737 Mär 22 12:10 README.md
```

Du hast dort auch einen unsichtbaren Ordner `.git` - der ist aber (noch) nicht relevant hier.

### Benutze SSH und nicht HTTPS wenn du lesen möchtest

> Für lesenden Zugriff reicht eine HTTPS-URL, jedoch wird ein SSH-Key zum Schreiben auf GitHub-Repositories benötigt. Denn die Authentifizierung von Nutzerinnen und Nutzern per Username/Password wird auf GitHub seit August 2021 nicht mehr unterstützt.

#### Einrichten deiner SSH Verbindung

## 2. Ändern eines Files

Die Files abändern, Ordner hinzufügen und löschen etc. kannst du alles über den Explorer und mit den Tools deiner Wahl machen. Da musst du dich nicht mehr mit der Konsole herumschlagen.

## 3. Änderungen "stagen" und "commiten"

### Status eines Files

Es gibt drei Status von Dateien:
1. Lokal gespeichert.
2. Staged. Quasi "bereit gelegt".
3. Commitet. Bestätigt und Kommentiert, was du geändert hast.
4. Auf den Server (Github) geladen (gepusht). Das sehen wir im nächsten Schritt.

Den Status siehst du mit dem Git-Kommando `git status`:
```bash
# Status des lokalen Repositories
dave@windows ~/Documents/github_repos
$ git status
On branch main
Your branch is up to date with 'origin/main'.

nothing to commit, working tree clean
```

#### Lokal gespeichert
Wenn du nun ein File (zBs. README.md) geändert und gespeichert hast, siest du es als lokal gespeichert und abgeändert.
```bash
# Status des lokalen Repositories
dave@windows ~/Documents/github_repos
$ git status
On branch main
Your branch is up to date with 'origin/main'.

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
	modified:   README.md

no changes added to commit (use "git add" and/or "git commit -a")
```
Dort siehst du `modified:   README.md`

#### Staged
Um es nun bereit zu legen, um die Änderung zu bestätigen musst du es "stagen". 

Doch vorher möchtest du vielleicht überprüfen, was sich überhaupt geändert hat. Dies machst du mit dem Git-Kommando `git diff`.
```bash
# Änderungen eines Files seit dem letzten "commit"
dave@windows ~/Documents/github_repos
$ git diff
diff --git a/README.md b/README.md
index 5e0fb03..a12f268 100644
--- a/README.md
+++ b/README.md
@@ -101,8 +101,7 @@ nothing to commit, working tree clean
 
-Wenn du nun ein File geändert und gespeichert hast, siest du es als lokal gespeichert und abgeändert.
-
+Wenn du jetzt ein File geändert und gespeichert hast und es ist so wie du es möchtest.
```

Wenn es gut ist, kannst du es nun "bereit legen" mit dem Git-Kommando `git add <dateiname>` oder um alle Files zu "stagen" `git add .`

```bash
# Stagen eines Files
dave@windows ~/Documents/github_repos
$ git add README.md
```

Der Status sieht jetzt so aus:

```bash
# Status des lokalen Repositories
dave@windows ~/Documents/github_repos
$ git status
On branch main
Your branch is ahead of 'origin/main' by 1 commit.
  (use "git push" to publish your local commits)

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	modified:   README.md
```

#### Committet

## 4. Änderungen auf das online Repository "pushen"