# Git Cheatsheet ############

#### Lokales Repository neu einrichten
    $ mkdir myproject
    $ cd myproject
    $ git init

#### Edit, Add, Commit
    $ # Dateien bearbeiten
    $ git add file1 file2 file3
    $ git commit

Commits haben als ID den SHA-1-Hash aus Inhalt, Commit-Message und Parent-Commit.
Diese ID ist also global eindeutig.

#### Lokale Branches

- Branches sind "nur" Pointer auf Commits.
- `master` ist der Default-Branch.
- `HEAD` ist ein Alias für den zuletzt ausgecheckten Commit.
- `<commit>^` ist der Parent von `<commit>`, `HEAD^` ist also der direkte
  Vorgänger von `HEAD`, `master^` der vorletzte Commit im Branch `master`.
- Weiter zurück geht es mit `~`:
    - `HEAD~1` ist das gleiche wie `HEAD^`
    - `HEAD~3` ist der Commit 3 Schritte vor `HEAD`.

##### Branch anlegen und dorthin wechseln
    $ git branch meinNeuerBranch
    $ git checkout meinNeuerBranch

oder:
  
    $ git checkout -b meinNeuerBranch
    
##### Branch wechseln
    $ git checkout <branchname>
    
##### Branches mergen
Den Inhalt von `myfeature` in `master` mergen:

    $ git checkout master
    $ git merge myfeature

Git erzeugt einen Merge-Commit, der zwei Parents hat: Den vorigen in diesem Branch, und den letzten im anderen Branch. Zugriff hat man mit einer erweiterten `^`-Syntax:

`HEAD^1`, der "First Parent", ist der Parent auf dem aktuellen Branch, hier also der vorige Commit in `master`. `HEAD^2` ist der Parent auf dem anderen Branch, hier der letzte Commit in `myfeature`.

##### Historie anzeigen
Alle Commits in diesem Branch und hineingemergete Commits:

    $ git log
    
Mit Branch-Grafik:

    $ git log --graph

Komprimiert:

    $ git log --pretty=oneline

Nur Commits und Merges in diesem Branch anzeigen, keine Commits aus gemergeten Branches (siehe auch oben "Branches mergen"):

    $ git log --first-parent

#### Zusammenarbeit
##### Entferntes Repository clonen
    $ git clone git@github.com:duesenklipper/wicket-safemodel.git
    $ cd wicket-safemodel
Git legt automatisch eine Remote `origin` an. Alle remote tracking Branches liegen unter `<remotename>/<branchname>`, z.b. `origin/master`.

##### Weitere remote repositories anbinden
    $ git remote add <remotename> <url>
    $ git fetch <remotename>
    
    

##### Updates von anderen holen
    $ git fetch origin
    $ git merge origin/master
Oder:

    $ git pull origin master
    
