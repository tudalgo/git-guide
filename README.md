# FOP Git Quick Guide

In diesem Guide werden CLI (command-line-interface)-Befehle so ausgedrückt:

```shell
befehl
```

Um einen Befehl auszuführen, geben Sie diesen in Ihr Terminal ein und drücken Sie die Enter-Taste.

## Voraussetzung: Git installieren

Schauen Sie zunächst, ob Sie schon git installiert haben, indem Sie in einem Terminal den folgenden Befehl ausführen:

```shell
git --version
```

Falls Sie git bereits installiert haben, kommt ungefähr so eine Nachricht:

*Die letzte Version ist 2.35.0. Es kann aber sein, dass Sie eine ältere Version haben*

```shell
git version 2.35.0
```

Wenn Sie stattdessen eine Fehlernachricht bekommen, sollten Sie git installieren. Die Download-Seite finden
Sie [hier](https://git-scm.com/download).

## Git repository clonen

Um ein git-Repository herunterzuladen, muss man es "clonen". Es gibt zwei Möglichkeiten, das zu machen.

### Clone per SSH (empfohlen)

#### 1. SSH-Key Erstellen

Falls Sie keinen SSH-Key haben, können Sie folgendermaßen einen erstellen:

```shell
ssh-keygen -t rsa -b 4096
```

*Tipp: Falls sie auf Windows sind, und der Befehl nicht geht, können Sie OpenSSH
mit [diesem Guide](https://docs.microsoft.com/en-us/windows-server/administration/openssh/openssh_install_firstuse) installieren.*

Erklärung vom Befehl:

- `-t rsa` = mit type rsa
- `-b 4096` = mit 4096 bits

Im Ordner `~/.ssh/` sollten es jetzt zwei Dateien geben:

*`~` bedeutet Home-Verzeichnis*

1. `id_rsa` - private-key (nicht teilen!!)
2. `id_rsa.pub` - public-key (kann man teilen)

#### 2. Public-Key auf GitHub hochladen

Es ist [hier](https://github.com/settings/keys) möglich, Ihre SSH-Key hochzuladen. Klicken Sie erst auf "New SSH key", und
kopieren Sie den inhalt der Datei `~/.ssh/id_rsa.pub` (wichtig, die mit .pub) auf der Seite.

#### 3. Clone

Nun können Sie die Vorlage clonen. Für das Projekt sieht es zum Beispiel so aus:

```shell
git clone git@github.com:FOP-2022/FOP-2022-Projekt-Student.git
```

Bei der Ausführung wird ein Ordner namens `FOP-2022-Projekt-Student` erstellt.

### Clone per HTTPS

Es ist auch möglich die Vorlage per HTTPS zu clonen. Wir empfehlen Ihnen, statt HTTPS besser SSH, wie oben beschrieben, zu
verwenden. Dies erleichtert Ihnen die Authentifizierung bei der Verwendung Ihrer eigenen Repositories.

```shell
git clone https://github.com/FOP-2022/FOP-2022-Projekt-Student.git
```

## Upstream remote einstellen

Ein "Remote" ist der Online-Server wo die Daten einer Repository gespeichert werden. Wenn die Vorlage gecloned wird, erstellt git
automatisch den Remote namens `origin`, der die Vorlage verlinkt.

Dieser Remote sollte zuerst auf `upstream` umbenannt werden, damit Sie später den Namen `origin` für Ihren eigenen Remote benutzen
können. Das können Sie folgendermaßen machen:

```shell
git remote rename origin upstream
```

## Private Repository erstellen

*Wichtig: Keine fork von der Vorlage erstellen. Forks von Public Repositories können nicht Private gemacht werden.*

*Wichtig: Unter Verwendung der Vorlage, falls Sie den Befehl `git init` ausführen müssen, haben Sie was falsch gemacht.*

Der nächste Schritt ist eine Private Repository zu erstellen, wo Ihre Gruppen-Daten sicher online gespeichert werden.

Als erstes erstellt ein Gruppenmitglied eine leere Private Repository auf GitHub. Das
geht [hier](https://github.com/new).

```
1. Name: FOP-2022-Projekt-Student
2. Private
3. Create repository
```

*Wichtig: Die Checkboxen unter "Initialize this repository with:" nicht anklicken!*

## Private Repository lokal als Remote definieren

Als Nächstes wird die neu erstellte Repository als Remote namens `origin` definiert. Ersetzten Sie `<GitHub username>` durch Ihren
GitHub-Benutzernamen.

SSH:

```shell
git remote add origin git@github.com:<GitHub username>/FOP-2022-Projekt-Student.git
```

HTTPS:

```shell
git remote add origin https://github.com/<GitHub username>/FOP-2022-Projekt-Student.git
```

## Push!

Nun können Sie die Private Repository initialisieren. Das machen Sie so:

```shell
git push -u origin master
```

*Falls Sie per HTTPS cloned haben und bis jetzt noch keine Login-Credentials angegeben haben, werden sie jetzt gefragt.*

Der Projekt-Setup ist jetzt fertig.

## Empfohlene git config

Um unbeabsichtigte Merge-Commits zu vermeiden, können Sie git so einstellen, dass diese bei `git pull` nicht automatisch erzeugt
werden. Falls durch einen `git pull` ein "fast-forward" nicht möglich ist, wird stattdessen ein Fehler geworfen. Um die remote
changes trotzdem lokal einzubinden, können Sie den Befehl `git pull --rebase` ausführen. Eine gute Erklärung zu diesem Befehl
finden Sie [hier](https://www.atlassian.com/git/tutorials/syncing/git-pull).

```shell
git config --global pull.ff only
```

Stellt sicher, dass neue Dateien auf dem Remote immer nur LF line-endings nutzen (und nicht CRLF).

```shell
git config --global core.autocrlf input
```

## Branch erstellen

Es wird wahrscheinlich sinnvoll sein, parallel zu arbeiten. Das geht mit Branches:

- `git checkout -b <name>`

## Committen

Um die Zwischenarbeit zu speichern, können Sie im privaten Repo Commits pushen. Das geht so:

- `git add -A` // um alles zu stagen, siehe: https://git-scm.com/docs/git-add
- `git commit -m "Message here"`
- `git push`

## Update von upstream

Falls sich die Vorlage aktualisiert, können Sie so die Änderungen mergen:

- `git fetch upstream` // fetch (but do not apply) changes from remote "upstream"
- `git merge upstream/master` // neuste Änderungen der Vorlage einfügen

# Das war's

Dieser Guide soll Ihnen einen ersten Überblick geben, wie Sie das Projekt einrichten und erste Schritte mit Git machen können.
Allerdings kann er keine umfassende Einführung in die Arbeit und Funktionsweise von Git ersetzen. Hierfür verweisen wir Sie auf
die unten angegebenen Ressourcen.

Falls Sie noch Fragen haben, können Sie diese im Forum oder im #git-help Kanal auf dem Discord-Server stellen.

Useful links:

- [Git Cheat Sheet](https://education.github.com/git-cheat-sheet-education.pdf)
- [Atlassian Git Guide](https://www.atlassian.com/git/tutorials)
- [Git Scm Docs](https://git-scm.com/docs)
