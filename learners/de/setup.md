---
title: Einrichtung
---


## Dateien herunterladen

Sie müssen einige Dateien herunterladen, um dieser Lektion folgen zu können.

1. Laden Sie [shell-lesson-data.zip][zip-file] herunter und verschieben Sie die Datei
   auf Ihren Desktop.
2. Entpacken/Extrahieren Sie die Datei. **Sagen Sie Ihrem Lehrer Bescheid, wenn Sie bei
   diesem Schritt Hilfe benötigen**. Sie sollten nun einen neuen Ordner mit dem Namen
   `shell-lesson-data` auf Ihrem Desktop haben.

## Software installieren

Wenn Sie die Shell-Software noch nicht installiert haben, müssen Sie sie [herunterladen
und installieren][install_shell].

## Öffnen Sie eine neue Shell

Nach der Installation der Software

3. Öffnen Sie ein Terminal. Wenn Sie nicht sicher sind, wie Sie ein Terminal auf Ihrem
   Betriebssystem öffnen können, lesen Sie die folgenden Anweisungen.
4. Geben Sie im Terminal `cd` ein und drücken Sie die <kbd>Return</kbd>-Taste. Dieser
   Schritt stellt sicher, dass Sie mit Ihrem Heimatordner als Arbeitsverzeichnis
   beginnen.

In dieser Lektion werden Sie erfahren, wie Sie auf die Datendateien in diesem Ordner
zugreifen können.

::::::::::::::::::::::::::::::::::::::::: callout

## Wo man Befehle eingibt: Wie man eine neue Shell öffnet

Die Shell ist ein Programm, das es uns ermöglicht, Befehle an den Computer zu senden und
Ausgaben zu erhalten. Sie wird auch als Terminal oder Kommandozeile bezeichnet.

Einige Computer enthalten ein Standard-Unix-Shell-Programm. Die folgenden Schritte
beschreiben einige Methoden zur Identifizierung und zum Öffnen eines
Unix-Shell-Programms, wenn Sie bereits eines installiert haben. Es gibt auch
Möglichkeiten, ein Unix-Shell-Programm, einen Linux/UNIX-Emulator oder ein Programm für
den Zugriff auf eine Unix-Shell auf einem Server zu identifizieren und herunterzuladen.

Wenn keine der unten genannten Optionen auf Ihre Situation zutrifft, versuchen Sie es
mit einer Online-Suche nach: Unix-Shell [Ihr Computermodell] [Ihr Betriebssystem].


::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::: solution

### Windows {#windows}

Auf Computern mit Windows-Betriebssystemen ist nicht automatisch ein Unix-Shell-Programm
installiert. In dieser Lektion empfehlen wir Ihnen die Verwendung eines Emulators, der
in [Git für Windows][install_shell] enthalten ist und Ihnen Zugang sowohl zu
Bash-Shell-Befehlen als auch zu Git bietet.

Nach der Installation können Sie ein Terminal öffnen, indem Sie das Programm Git Bash
aus dem Windows-Startmenü starten.

**Für fortgeschrittene Benutzer:**

Als Alternative zu Git für Windows können Sie das [Windows Subsystem für Linux
installieren][wsl], das unter Windows 10 und höher Zugriff auf ein
Bash-Shell-Befehlszeilenwerkzeug bietet.

Bitte beachten Sie, dass die Befehle im Windows Subsystem für Linux (WSL) leicht von
denen abweichen können, die in der Lektion gezeigt oder im Workshop vorgestellt werden.

::::::::::::

:::::::::::: solution

### MacOS {#macos}

Für einen Mac-Computer, auf dem macOS Mojave oder frühere Versionen laufen, ist die
Standard-Unix-Shell Bash. Für einen Mac-Computer, auf dem macOS Catalina oder spätere
Versionen laufen, ist die Standard-Unix-Shell Zsh. Ihre Standard-Shell ist über das
Terminal-Programm in Ihrem Dienstprogramme-Ordner verfügbar.

Um Terminal zu öffnen, versuchen Sie eine oder beide der folgenden Möglichkeiten:

- Wählen Sie im Finder das Menü "Go" und dann "Utilities". Suchen Sie Terminal im Ordner
  "Utilities" und öffnen Sie es.
- Verwenden Sie die Mac 'Spotlight' Computer-Suchfunktion. Suchen Sie nach: `Terminal`
  und drücken Sie <kbd>Return</kbd>.

Um zu ueberpruefen, ob Ihr Rechner fuer die Verwendung einer anderen Sprache als Bash
eingerichtet ist, geben Sie `echo $SHELL` in Ihr Terminalfenster ein.

Wenn Ihr Rechner so eingerichtet ist, dass er etwas anderes als Bash verwendet, können
Sie ihn starten, indem Sie ein Terminal öffnen und `bash` eingeben.

[How to Use Terminal on a Mac][mac-terminal]

::::::::::::

:::::::::::: solution

### Linux {#linux}

Die Standard-Unix-Shell für Linux-Betriebssysteme ist normalerweise Bash. Bei den
meisten Linux-Versionen ist sie über das [Gnome-Terminal][gnome-terminal] oder die
[KDE-Konsole][kde-konsole] oder [xterm] erreichbar, die Sie über das Anwendungsmenü oder
die Suchleiste finden können. Wenn Ihr Rechner so eingerichtet ist, dass er etwas
anderes als Bash verwendet, können Sie ihn starten, indem Sie ein Terminal öffnen und
`bash` eingeben.

::::::::::::

[zip-file]: data/shell-lesson-data.zip
[install_shell]:
https://carpentries.github.io/workshop-template/install_instructions/#shell
[wsl]: https://learn.microsoft.com/en-us/windows/wsl/install
[mac-terminal]:
https://www.macworld.co.uk/feature/mac-software/how-use-terminal-on-mac-3608274/
[gnome-terminal]: https://help.gnome.org/users/gnome-terminal/stable/
[kde-konsole]: https://konsole.kde.org/
[xterm]: https://en.wikipedia.org/wiki/Xterm




