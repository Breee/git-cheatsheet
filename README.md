# Cheatsheet 1 - Einführung

| Befehl                                         | Aktion                                                                         |
|------------------------------------------------|--------------------------------------------------------------------------------|
| ```apt update && apt install git```            | Installiert git auf Linux (Debian-Derivaten)                                   |
| ```git clone <adresse>```                      | Repository an angegebener Adresse holen und in lokalen Ordner ablegen          |
| ```git status```                               | Anzeigen, welche Dateien modified/staged/untracked sind                        |
| ```git diff```                                 | Änderungen anzeigen                                                            |
| ```git diff <datei>```                         | Änderungen in \<datei\> anzeigen                                               |
| ```git diff --staged```                        | Änderungen im Stage-Bereich anzeigen                                           |
| ```git log```                                  | Historie anzeigen                                                              |
| ```git log --graph```                          | Historie als Graph anzeigen                                                    |
| ```git config <einstellung> <wert>```          | Setzt eine Einstellung für das aktuelle Repository                             |
| ```git config --global <einstellung> <wert>``` | Setzt eine Einstellung systemweit                                              |
| ```git config --list```                        | Alle aktuellen Einstellungen mit Wert anzeigen                                 |
| ```git add <pfad>```                           | Eine Datei als staged markieren                                                |
| ```git restore --staged <pfad>```              | Die Datei wieder unstaged markieren                                            |
| ```git restore <pfad>```                       | Eine Datei im modified state wieder auf den Originalinhalt zurücksetzen        |
| ```git commit```                               | Einen Commit mit allen Dateien in der Staging Area erstellen                   |
| ```git mv datei1 datei2```                     | Eine Dateiumbenennung stagen                                                   |
| ```git rm datei```                             | Eine Dateientfernung stagen                                                    |
| ```git push```                                 | Commits auf Server schieben                                                    |
| ```git pull```                                 | Commits vom Server holen                                                       |
| ```git help <befehl>```                        | Hilfe zum Git-Befehl anzeigen                                                  |


# Cheatsheet 2 - Änderungen Rückgängig Machen

## Allgemein

| Befehl                    | Aktion                                                          |
|---------------------------|-----------------------------------------------------------------|
| ```git blame <datei>```   | Autor zu jeder Zeile in `<datei>` anzeigen                      |
| ```git commit --amend```  | Commit oder Commit-Nachricht korrigieren                        |
| ```git revert <commit>``` | Fügt einen Commit mit den inversen Änderungen von `<commit>` an |
| ```git reset <commit>```  | Setzt den Stand des Repositories auf `<commit>` zurück          |

## Git reset

| Befehl                             | Verändert Head | Verändert Index | Verändert Working Directory |
|------------------------------------|----------------|-----------------|-----------------------------|
| ```git reset --soft <commit>```    | ja             | nein            | nein                        |
| ```git reset [--mixed] <commit>``` | ja             | ja              | nein                        |
| ```git reset --hard <commit>```    | ja             | ja              | ja                          |


# Cheatsheet 3 - Branches

## Teil 1

| Befehl                                          | Aktion                                                                                                  |
|-------------------------------------------------|---------------------------------------------------------------------------------------------------------|
| ```git checkout <branch>```                     | Auf lokal bestehenden Branch wechseln oder remote existierenden Branch lokal anlegen und drauf wechseln |
| ```git checkout -b <branch>```                  | Neuen Branch anlegen und drauf wechseln                                                                 |
| ```git branch```                                | Verfügbare Branches anzeigen                                                                            |
| ```git branch -a```                             | Alle Branches anzeigen (auch Remote)                                                                    |
| ```git branch <branch>```                       | Neuen Branch anlegen                                                                                    |
| ```git branch -d <branch>```                    | Branch löschen                                                                                          |
| ```git fetch [<remote>] [<branch>]```           | Änderungen vom Server holen                                                                             |
| ```git push [<remote>] [<branch>]```            | Änderungen auf den Server schieben                                                                      |
| ```git push --set-upstream <remote> <branch>``` | Lokalen Branch auf den Server schieben                                                                  |
| ```git merge <branch>```                        | `<branch>` in aktuellen Branch mergen                                                                   |
| ```git merge --no--ff <branch>```               | Merge der keinen fast-forward-merge macht                                                               |

## Teil 2

| Befehl                            | Aktion                                               |
|-----------------------------------|------------------------------------------------------|
| ```git rebase <branch>```         | Den aktuellen Branch an `<branch>` anhängen          |
| ```git pull --rebase <branch>```  | Änderungen vom Server holen und rebase ausführen     |
| ```git stash```                   | Nicht-committete Änderungen temporär "beiseitelegen" |
| ```git stash pop```               | Letzten Eintrag vom Stash holen und anwenden         |



# Cheatsheet 4 - History Rewriting

| Command                                                          | Action                                                  |
|------------------------------------------------------------------|---------------------------------------------------------|
| ```git rebase -i HEAD~4```                                       | Interaktiver Rebase der letzten 4 Commits               |
| ```git cherry-pick <commit-hash> [...more commit hashes...]```   | Einzelnen Commit auf HEAD anwenden                      |
|                                                                  |                                                         |
| ```git apply <patchfile>```                                      | Patch-Datei anwenden                                    |
| ```git format-patch <branch> -o <dir>```                         | Unterschiede des aktuellen Branch zu `<branch>` als Patch-Dateien in `<dir>` generieren |
| ```git format-patch <branch> -1 <commit_hash> -o <dir>```        | Generiert Patch-Datei für `<commit_hash>` in `<dir>`    |
| ```git am <patchfiles>```                                        | Wendet Patch-Dateien an und erstellt Commits daraus     |
|                                                                  |                                                         |
| ```git filter-branch --tree-filter <commmand> HEAD```            | Alle Parent-Commits auschecken und Command anwenden     |
| ```git filter-branch --all --tree-filter <command>```            | Alle Commits auschecken und Command anwenden            |
| ```git filter-branch --index-filter <command> HEAD```            | Command auf allen Parent-Commits im INDEX ausfügren     |
|                                                                  |                                                         |
| ```git push --force-with-lease```                                | Remote Versions DB mit lokaler überschreiben            |
|                                                                  |                                                         |
| ```git reflog```                                                 | Zeigt das Reflog für HEAD                               |
| ```git reflog show <branch_name>```                              | Zeigt das Reflog für `<branch_name>`                    |
| ```git reflog stash```                                           | Zeigt das Reflog für den Stash                          |


# Cheatsheet 5 - Fortgeschrittene Git Features

| Command                               | Action                                                                                 |
|---------------------------------------|----------------------------------------------------------------------------------------|
| ```git checkout HEAD~```              |                                                                                        |
| ```git checkout HEAD^```              | Wechselt zum Vorgänger von HEAD                                                        |
| ```git checkout master~2```           |                                                                                        |
| ```git checkout master^^```           | Wechselt zum Vor-Vorgänger von master                                                  |
|                                       |                                                                                        |
| ```git add -p```                      | Dateien interaktiv und nur teilweise stagen                                            |
|                                       |                                                                                        |
| ```git submodule add <url>```         | Submodul zu Repository hinzufügen                                                      |
| ```git submodule init```              | Submodule initialisieren (aktualisiert .gitmodules)                                    |
| ```git submodule update```            | Submodule aktualisieren, sodass sie auf dem erwarteten Stand des Parent-Projektes sind |
|                                       |                                                                                        |
| ```git bisect start```                | Bisect beginnen                                                                        |
| ```git bisect good <commit>```        | Markiert den initialen guten Commit                                                    |
| ```git bisect bad <commit>```         | Markiert den initialen schlechten Commit                                               |
| ```git bisect good```                 | Markiert den aktuellen Commit als gut                                                  |
| ```git bisect bad```                  | Markiert den aktuellen Commit als schlecht                                             |
| ```git bisect run <command>```        | Automatisierter lauf von bisect (Return code: good (== 0) or bad (!= 0)                |
|                                       |                                                                                        |
| ```git lfs install .```               | Installiert lfs für das aktuelle Repository                                            |
| ```git lfs track '*.png'```           | Trackt alle png-Dateien mit lfs                                                        |
|                                       |                                                                                        |
| ```git log -3```                      | Zeigt die letzten 3 Commits                                                            |
| ```git log --after="2019-7-1"```      | Zeigt die Commits nach "2019-7-1"                                                      |
| ```git log --author="Alice"```        | Zeigt Commits von der Autorin 'Alice' (Regex möglich)                                  |
| ```git log --grep="Closes #1337"```   | Zeigt Commits die die Commit-Nachricht "Closes #1337" enthalten                        |
| ```git log -- document.txt code.py``` | Zeigt Commits für die angegebene(n) Datei(en)                                          |
| ```git log master..feature```         | Zeigt den Unterschied zwischen Branch "master" und "feature" an                        |
| ```git log --no-merges```             | Zeigt Nicht-Merge Commits                                                              |
| ```git log --merges```                | Zeigt Merge Commits                                                                    |


