# Git & GitHub Workflow Anleitung

Dieses Dokument beschreibt die grundlegenden Schritte, um ein bestehendes Projekt auf GitHub zu veröffentlichen, es auf einen anderen Computer zu klonen und es zu aktualisieren.

## 1. Bestehendes Projekt zu GitHub hinzufügen

Um ein bereits existierendes Projekt (wie dieses) in ein neues GitHub-Repository hochzuladen, führe die folgenden Befehle im Hauptverzeichnis deines Projekts aus:

```bash
# Initialisiert ein neues, leeres Git-Repository im aktuellen Ordner
git init

# Fügt das entfernte GitHub-Repository als "origin" hinzu
# Ersetze die URL durch die deines Repositories
git remote add origin https://github.com/...

# Fügt alle aktuellen Dateien zum Staging-Bereich hinzu
git add .

# Erstellt einen neuen Commit mit den hinzugefügten Dateien
git commit -m "Initial commit"

# Lädt den "master"-Branch zum "origin"-Repository hoch
git push -u origin master
```

## 2. Repository auf einem anderen Computer auschecken

Um eine Kopie des Projekts von GitHub auf einen anderen Computer herunterzuladen, benutze den folgenden Befehl:

```bash
# Klont das Repository in einen neuen Ordner
# Ersetze die URL durch die deines Repositories
git clone https://github.com/...
```

## 3. Lokalen Entwicklungsstand aktualisieren

Wenn sich auf GitHub Änderungen befinden, die du lokal übernehmen möchtest (z.B. weil du auf einem anderen Computer gearbeitet hast), kannst du deinen lokalen Stand wie folgt aktualisieren:

```bash
# Lädt die neuesten Änderungen vom "origin"-Repository herunter
git pull origin master
```

## 4. Branch in main-Branch mergen

Wenn du in einem separaten Branch (z.B. "Branch1") entwickelt hast und diese Änderungen nun in den main-Branch integrieren möchtest, folge diesen Schritten:

```bash
# Wechselt zum main-Branch
git checkout main

# Holt die neuesten Änderungen vom Remote-Repository (empfohlen)
git pull origin main

# Merged den Feature-Branch in den aktuellen Branch (main)
git merge Branch1

# Falls es Merge-Konflikte gibt, müssen diese manuell gelöst werden
# Git zeigt dir die betroffenen Dateien an
# Nach dem Lösen der Konflikte:
git add .
git commit -m "Merge Branch1 into main"

# Lädt die gemergten Änderungen zum Remote-Repository hoch
git push origin main
```

**Optional:** Nach erfolgreichem Merge kannst du den Feature-Branch löschen, wenn er nicht mehr benötigt wird:

```bash
# Löscht den Branch lokal
git branch -d Branch1

# Löscht den Branch auf dem Remote-Repository.
git push origin --delete Branch1
```

## 5. Lokale Dateien auf GitHub-Stand zurücksetzen

Wenn du lokale Änderungen verwerfen und deinen lokalen Stand komplett mit dem aktuellen GitHub-Branch überschreiben möchtest, gibt es drei Optionen:

### Option 1: Hard Reset (Destruktiv)
**Achtung:** Alle lokalen, nicht committeten Änderungen gehen verloren!

```bash
# Lädt die neuesten Informationen vom Remote-Repository
git fetch origin

# Setzt den lokalen Stand hart auf den Remote-Branch zurück
# Ersetze <branch-name> mit dem gewünschten Branch (z.B. main oder ein Feature-Branch)
git reset --hard origin/<branch-name>
```

### Option 2: Stash dann Reset (Sicherer)
Diese Variante speichert deine lokalen Änderungen in einem Stash, bevor sie verworfen werden. Du kannst sie später wiederherstellen.

```bash
# Speichert lokale Änderungen im Stash mit einer Beschreibung
git stash push -m "Saving local changes before reset"

# Lädt die neuesten Informationen vom Remote-Repository
git fetch origin

# Setzt den lokalen Stand hart auf den Remote-Branch zurück
git reset --hard origin/<branch-name>

# Optional: Später die gestashten Änderungen wiederherstellen
# git stash pop
```

### Option 3: Hard Reset + Untracked Files löschen (Am destruktivsten)
**Achtung:** Diese Option löscht ALLE lokalen Änderungen UND alle nicht versionierten Dateien!

```bash
# Lädt die neuesten Informationen vom Remote-Repository
git fetch origin

# Setzt den lokalen Stand hart auf den Remote-Branch zurück
git reset --hard origin/<branch-name>

# Löscht alle untracked Dateien und Verzeichnisse
git clean -fd
```

**Tipp:** Mit `git status` kannst du vorher überprüfen, welche Änderungen betroffen wären.






## Um auf den Branch ClaudeCode_WEB-DEV zu wechseln und die Dateien zu laden, verwende diese Befehle in der Console:

# 1. Remote Branches aktualisieren
git fetch origin

# 2. Zu dem Branch wechseln
git checkout ClaudeCode_WEB-DEV

# Falls der Branch noch nicht lokal vorhanden ist, verwende stattdessen:
git checkout -b ClaudeCode_WEB-DEV origin/ClaudeCode_WEB-DEV

Mit git status kannst du danach überprüfen, auf welchem Branch du dich befindest.
