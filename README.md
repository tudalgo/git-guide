# FOP Git Quick Guide (unverbindlich)

In diesem guide werden CLI (command-line-interface) befehle so ausgedruckt:

```shell
$ befehl
```

Das `$` ist nur ein Indikator, dass es sich um ein Befehl handelt, und soll nicht geschrieben werden. Der wirkliche Befehl wäre in
diesem Fall nur das Wort "befehl" (ohne Anführungszeichen). Um einen Befehl auszuführen, drücken Sie die Enter-Taste.

## Voraussetzung: Git installieren

Schauen sie erst, ob Sie schon git installiert haben, indem Sie in einem Terminal den folgenden befehl ausführen:

```shell
$ git --version
```

Falls sie schon git installiert haben, kommt ungefähr so eine Nachricht:

*Die letzte Version ist 2.35.0. Es kann aber sein, dass Sie eine ältere Version haben*

```shell
git version 2.35.0
```

Wenn stadtessen eine Fehlernachricht kommen, sollten sie git installieren. Die Download-Seite finden
sie [hier](https://git-scm.com/download).

## Git repository clonen

Um eine git repository runterzuladen, muss man sie "clonen". Es gibt zwei Möglichkeiten, das zu machen.

### Clone per SSH (empfohlen)

#### 1. SSH-Key Erstellen

Falls Sie keine SSH-key haben, können Sie so eine erstellen:

```shell
$ ssh-keygen -t rsa -b 4096
```

Erklärung vom Befehl:

- `-t rsa` = mit type rsa
- `-b 4096` = mit 4096 bits

Im ordner `~/.ssh/` sollten es jetzt zwei dateien geben:

*`~` bedeutet Home-Verzeichnis*

1. `id_rsa` - private-key (nicht teilen!!)
2. `id_rsa.pub` - public-key (kann man teilen)

#### 2. Public-key auf GitHub hochladen

Es ist [hier](https://github.com/settings/keys) möglich, Ihre SSH-key hochzuladen. Klicken Sie erst auf "New SSH key", und
kopieren sie den inhalt der Datei `~/.ssh/id_rsa.pub` (wichtig, die mit .pub) auf der Seite.

#### 3. Clone

Nun können Sie die Vorlage clonen. Für das Projekt sieht es zum Beispiel so aus:

```shell
$ git clone git@github.com:FOP-2022/FOP-2022-Projekt-Student.git
```

Bei der Ausführung wird ein Ordner namens `FOP-2022-Projekt-Student` erstellt.

### Clone per HTTPS

Es ist auch möglich die Vorlage per HTTPS zu clonen.

```shell
$ git clone https://github.com/FOP-2022/FOP-2022-Projekt-Student.git
```

## Upstream remote einstellen

Ein "Remote" ist der online-server wo die Daten einer Repository gespeichert werden. Wenn die Vorlage gecloned wird, erstellt git
automatisch den Remote namens `origin` der zur Vorlage verlinkt.

Dieser Remote sollte erst auf `upstream` umbenannt werden, damit Sie später den namen `origin` für ihren eigenen Remote benutzen
können. Das können Sie so machen:

```shell
$ git remote rename origin upstream
```

## Private Repository erstellen

Der nächste Schritt ist eine Private Repository zu erstellen, wo Ihre Gruppen-Daten sicher online gespeichert werden.

Als erstes erstellt ein Gruppenmitglied eine leere Private Repository auf GitHub. Das
geht [hier](https://github.com/alexstaeding?tab=repositories).

```
1. Name: FOP-2022-Projekt-Student
2. Private
3. Create repository
```

*Wichtig: Die check-boxen unter "Initialize this repository with:" nicht anklicken!*

## Private Repository lokal als Remote definieren

Als Nächstes wird die neu-erstellte Repository als Remote namens `origin` definiert. Ersetzten sie `<GitHub username>` durch ihrem
GitHub Benutzername.

SSH:

```shell
$ git remote add origin git@github.com:<GitHub username>/FOP-2022-Projekt-Root.git
```

HTTPS:

```shell
$ git remote add origin https://github.com/<GitHub username>/FOP-2022-Projekt-Root.git
```

## Push!

Nun können Sie die Private Repository initialisieren. Das machen Sie so:

```shell
$ git push -u origin master
```

*Falls Sie per HTTPS cloned haben und bis jetzt noch keine Login-Credentials angegeben haben, werden sie jetzt gefragt.*

Der setup ist jetzt fertig.

## Empfohlene git config

Um unbeabsichtigte merge commits zu vermeiden, können Sie git so einstellen, dass die bei `git pull` nicht automatisch gemacht
werden. Falls durch einen `git pull` ein "fast-forward" nicht möglich ist, wird stattdessen einen Fehler geworfen. Um die remote
changes trotzdem lokal einzubinden, ist es mit dem Befehl `git pull --rebase` möglich. Eine gute erklärung zu dem Befehl finden
Sie [hier](https://www.atlassian.com/git/tutorials/syncing/git-pull).

```shell
$ git config --global pull.ff only
```

Stellt sicher, dass neue Dateien auf dem Remote immer nur LF line-endings nutzen (und nicht CRLF).

```shell
$ git config --global core.autocrlf input
```

## Branch erstellen

Es wird wahrscheinlich sinnvoll sein, parallel zu arbeiten. Das geht mit branches:

- `git checkout -b <name>`

## Committen

Um die zwischenarbeit zu speichern, können Sie im privaten repo commits pushen. Das geht so:

- `git add -A` // um alles zu stagen, see https://git-scm.com/docs/git-add
- `git commit -m "Message here"`
- `git push`

## Update von upstream

Falls sich die Vorlage aktualisiert, können Sie so die changes mergen:

- `git fetch upstream` // fetch (but do not apply) changes from remote "upstream"
- `git merge upstream/master` // merge latest changes from vorlage

# Das wars

Falls Sie noch Fragen haben, können Sie im Forum oder im #git-help Kanal auf dem discord server diese stellen.

Useful links:
- [Git Cheat Sheet](https://education.github.com/git-cheat-sheet-education.pdf)
- [Atlassian Git Guide](https://www.atlassian.com/git/tutorials)
- [Git Scm Docs](https://git-scm.com/docs)
