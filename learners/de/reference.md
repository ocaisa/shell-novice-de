---
title: Zusammenfassung der grundlegenden Befehle
---


## Zusammenfassung der grundlegenden Befehle

| Action       | Files | Folders      |
| ------------ | ----- | ------------ |
| Inspect      | ls    | ls           |
| View content | cat   | ls           |
| Navigate to  |       | cd           |
| Move         | mv    | mv           |
| Copy         | cp    | cp -r        |
| Create       | nano  | mkdir        |
| Delete       | rm    | rmdir, rm -r |

## Dateisystem-Hierarchie

Das Folgende ist ein Überblick über ein Standard-Unix-Dateisystem. Die genaue Hierarchie
hängt von der jeweiligen Plattform ab. Ihre Datei-/Verzeichnisstruktur kann leicht
abweichen:

![](fig/standard-filesystem-hierarchy.svg){alt='Linux-Dateisystem-Hierarchie'}

## Glossar

[absoluter Pfad]{#absolute-path} : Ein [Pfad](#path), der sich auf einen bestimmten Ort
in einem Dateisystem bezieht. Absolute Pfade werden normalerweise in Bezug auf das
[Wurzelverzeichnis](#root-directory) des Dateisystems geschrieben und beginnen entweder
mit "/" (unter Unix) oder "\\" (unter Microsoft Windows). Siehe auch: [relativer
Pfad](#relative-path).

[argument]{#argument} : Ein Wert, der einer Funktion oder einem Programm übergeben wird,
wenn es ausgeführt wird. Der Begriff wird oft austauschbar (und uneinheitlich) mit
[parameter](#parameter) verwendet.

[command-shell]{#command-shell} : Siehe [shell](#shell)

[command-line interface]{#command-line-interface} : Eine Benutzeroberfläche, die auf der
Eingabe von Befehlen basiert, normalerweise in einer [REPL](#read-evaluate-print-loop).
Siehe auch: [grafische Benutzeroberfläche](#graphical-user-interface).

[comment]{#comment} : Eine Bemerkung in einem Programm, die dem menschlichen Leser
helfen soll zu verstehen, was vor sich geht, aber vom Computer ignoriert wird.
Kommentare in Python, R und der Unix-Shell beginnen mit einem `#`-Zeichen und laufen bis
zum Ende der Zeile; Kommentare in SQL beginnen mit `--`, und andere Sprachen haben
andere Konventionen.

[current working directory]{#current-working-directory} : Das Verzeichnis, von dem aus
[relative Pfade](#relative-path) berechnet werden; gleichbedeutend mit dem Ort, an dem
Dateien, auf die nur durch den Namen verwiesen wird, gesucht werden. Jeder
[Prozess](#process) hat ein aktuelles Arbeitsverzeichnis. Das aktuelle
Arbeitsverzeichnis wird gewöhnlich mit der Kurzschreibweise `.` (ausgesprochen "Punkt")
bezeichnet.

[Dateisystem]{#Dateisystem} : Ein Satz von Dateien, Verzeichnissen und E/A-Geräten (wie
Tastaturen und Bildschirme). Ein Dateisystem kann über viele physische Geräte verteilt
sein, oder viele Dateisysteme können auf einem einzigen physischen Gerät gespeichert
sein; das [Betriebssystem](#operating-system) verwaltet den Zugriff.

[Dateinamenerweiterung]{#Dateinamenerweiterung} : Der Teil eines Dateinamens, der nach
dem letzten "."-Zeichen kommt. Nach Konvention identifiziert dies den Typ der Datei:
`.txt` bedeutet "Textdatei", `.png` bedeutet "Portable Network Graphics Datei", und so
weiter. Diese Konventionen werden von den meisten Betriebssystemen nicht eingehalten: Es
ist durchaus möglich (aber verwirrend!), eine MP3-Tondatei `homepage.html` zu nennen. Da
viele Anwendungen Dateinamenserweiterungen verwenden, um den [MIME-Typ](#mime-type) der
Datei zu identifizieren, kann eine falsche Benennung von Dateien zum Scheitern dieser
Anwendungen führen.

[filter]{#filter} : Ein Programm, das einen Datenstrom umwandelt. Viele
Unix-Befehlszeilen-Tools sind als Filter geschrieben: Sie lesen Daten von der
[Standardeingabe](#Standardeingabe), verarbeiten sie und schreiben das Ergebnis auf die
[Standardausgabe](#Standardausgabe).

[for-Schleife]{#for-loop} : Eine Schleife, die für jeden Wert in einer Menge, Liste oder
einem Bereich einmal ausgeführt wird. Siehe auch: [while-Schleife](#while-loop).

[grafische Benutzeroberfläche]{#graphical-user-interface} : Eine Benutzeroberfläche, die
auf der Auswahl von Elementen und Aktionen auf einer grafischen Anzeige basiert und
normalerweise mit der Maus gesteuert wird. Siehe auch:
[Befehlszeilenschnittstelle](#command-line-interface).

[home directory]{#home-directory} : Das Standardverzeichnis, das mit einem Konto auf
einem Computersystem verbunden ist. Konventionell werden alle Dateien eines Benutzers in
oder unter seinem Home-Verzeichnis gespeichert.

[loop]{#loop} : Ein Satz von Anweisungen, die mehrfach ausgeführt werden. Besteht aus
einem [Schleifenkörper](#loop-body) und (normalerweise) einer Bedingung zum Verlassen
der Schleife. Siehe auch [for loop](#for-loop) und [while loop](#while-loop).

[loop body]{#loop-body} : Die Menge der Anweisungen oder Befehle, die innerhalb einer
[for-Schleife](#for-loop) oder [while-Schleife](#while-loop) wiederholt werden.

[MIME-Typ]{#mime-type} : MIME-Typen (Multi-Purpose Internet Mail Extensions) beschreiben
verschiedene Dateitypen für den Austausch im Internet, z. B. Bilder, Audio und
Dokumente.

[Betriebssystem]{#Betriebssystem} : Software, die die Interaktionen zwischen Benutzern,
Hardware und Software verwaltet [Prozesse](#Prozess). Gängige Beispiele sind Linux,
macOS und Windows.

[option]{#option} : Eine Möglichkeit, ein Argument oder eine Einstellung für ein
Befehlszeilenprogramm anzugeben. Unix-Anwendungen verwenden üblicherweise einen
Bindestrich gefolgt von einem einzelnen Buchstaben, z.B. `-v`, oder zwei Bindestriche
gefolgt von einem Wort, z.B. `--verbose`, während DOS-Anwendungen einen Schrägstrich
verwenden, z.B. `/V`. Je nach Anwendung kann einer Option auch ein einzelnes Argument
folgen, wie in `-o /tmp/output.txt`.

[parameter]{#parameter} : Eine Variable, die in der Deklaration einer Funktion genannt
wird und die dazu dient, einen Wert zu halten, der an den Aufruf übergeben wird. Der
Begriff wird oft austauschbar (und inkonsistent) mit [argument](#argument) verwendet.

[übergeordnetes Verzeichnis]{#parent-directory} : Das Verzeichnis, das das betreffende
Verzeichnis "enthält". Jedes Verzeichnis in einem Dateisystem außer dem
[Wurzelverzeichnis](#root-directory) hat ein Elternverzeichnis. Auf das
Elternverzeichnis eines Verzeichnisses wird normalerweise mit der Kurzschreibweise `..`
(ausgesprochen "dot dot") verwiesen.

[path]{#path} : Eine Beschreibung, die den Ort einer Datei oder eines Verzeichnisses
innerhalb eines [Dateisystems](#file-system) angibt. Siehe auch: [absoluter
Pfad](#absolute-path), [relativer Pfad](#relative-path).

[pipe]{#pipe} : Eine Verbindung zwischen dem Ausgang eines Programms und dem Eingang
eines anderen. Wenn zwei oder mehr Programme auf diese Weise verbunden sind, nennt man
sie eine "Pipeline".

[process]{#process} : Eine laufende Instanz eines Programms, die Code, Variablenwerte,
offene Dateien und Netzwerkverbindungen usw. enthält. Prozesse sind die "Akteure", die
das [Betriebssystem](#Betriebssystem) verwaltet; es lässt jeden Prozess typischerweise
für ein paar Millisekunden am Stück laufen, um den Eindruck zu erwecken, dass sie
gleichzeitig ausgeführt werden.

[prompt]{#prompt} : Ein Zeichen oder mehrere Zeichen, die von einer
[REPL](#read-evaluate-print-loop) angezeigt werden, um anzuzeigen, dass sie auf ihren
nächsten Befehl wartet.

[quoting]{#quoting} : (in der Shell): Die Verwendung von Anführungszeichen verschiedener
Art, um die Shell daran zu hindern, Sonderzeichen zu interpretieren. Um zum Beispiel die
Zeichenkette `*.txt` an ein Programm zu übergeben, ist es normalerweise notwendig, sie
als `'*.txt'` (mit einfachen Anführungszeichen) zu schreiben, damit die Shell nicht
versucht, den Platzhalter `*` zu erweitern.

[read-evaluate-print loop]{#read-evaluate-print-loop} : (REPL): Eine
[Befehlszeilenschnittstelle](#command-line-interface), die einen Befehl vom Benutzer
liest, ihn ausführt, das Ergebnis ausgibt und auf einen weiteren Befehl wartet.

[redirect]{#redirect} : Die Ausgabe eines Befehls an eine Datei statt an den Bildschirm
oder einen anderen Befehl senden, oder äquivalent die Eingabe eines Befehls aus einer
Datei lesen.

[Regulärer Ausdruck]{#regulärer-Ausdruck} : Ein Muster, das eine Menge von Zeichenketten
angibt. Reguläre Ausdrücke werden am häufigsten verwendet, um Zeichenfolgen in
Zeichenketten zu finden.

[relativer Pfad]{#relative-path} : Ein [Pfad](#path), der den Ort einer Datei oder eines
Verzeichnisses in Bezug auf das [aktuelle
Arbeitsverzeichnis](#current-working-directory) angibt. Jeder Pfad, der nicht mit einem
Trennzeichen ("/" oder "\\") beginnt, ist ein relativer Pfad. Siehe auch: [absoluter
Pfad](#absolute-path).

[Root-Verzeichnis]{#root-directory} : Das oberste Verzeichnis in einem
[Dateisystem](#dateisystem). Sein Name ist "/" unter Unix (einschließlich Linux und
macOS) und "\\" unter Microsoft Windows.

[shell]{#shell} : Eine [Befehlszeilenschnittstelle](#command-line-interface) wie Bash
(die Bourne-Again-Shell) oder die Microsoft Windows DOS-Shell, die dem Benutzer die
Interaktion mit dem [Betriebssystem](#operating-system) ermöglicht.

[shell-script]{#shell-script} : Ein Satz von [shell](#shell) Befehlen, die in einer
Datei zur Wiederverwendung gespeichert sind. Ein Shell-Skript ist ein Programm, das von
der Shell ausgeführt wird; der Name "Skript" wird aus historischen Gründen verwendet.

[Standardeingabe]{#Standard-Eingabe} : Der Standard-Eingabestrom eines Prozesses. In
interaktiven Kommandozeilenanwendungen ist er typischerweise mit der Tastatur verbunden;
in einer [pipe](#pipe) empfängt er Daten von der [standard output](#standard-output) des
vorhergehenden Prozesses.

[Standardausgabe]{#standard-output} : Der Standard-Ausgabestrom eines Prozesses. In
interaktiven Kommandozeilenanwendungen werden die an die Standardausgabe gesendeten
Daten auf dem Bildschirm angezeigt; in einer [pipe](#pipe) werden sie an die
[Standardeingabe](#standard-input) des nächsten Prozesses weitergeleitet.

[sub-directory]{#sub-directory} : Ein Verzeichnis, das in einem anderen Verzeichnis
enthalten ist.

[tab-completion]{#tab-completion} : Eine Funktion vieler interaktiver Systeme, bei der
das Drücken der Tabulator-Taste die automatische Vervollständigung des aktuellen Wortes
oder Befehls auslöst.

[variable]{#variable} : Ein Name in einem Programm, der mit einem Wert oder einer
Sammlung von Werten verbunden ist.

[while-Schleife]{#while-loop} : Eine Schleife, die so lange ausgeführt wird, wie eine
Bedingung erfüllt ist. Siehe auch: [for-Schleife](#for-loop).

[wildcard]{#wildcard} : Ein Zeichen, das beim Mustervergleich verwendet wird. In der
Unix-Shell passt der Platzhalter `*` auf null oder mehr Zeichen, so dass `*.txt` auf
alle Dateien passt, deren Namen auf `.txt` enden.

## Externe Referenzen

### Öffnen eines Terminals

- [Wie man Terminal auf einem Mac
  benutzt](https://www.macworld.co.uk/feature/mac-software/how-use-terminal-on-mac-3608274/)
- [Git für Windows](https://git-for-windows.github.io/)
- [Wie man das Bash-Shell-Befehlszeilen-Tool unter Windows 10
  installiert](https://www.windowscentral.com/how-install-bash-shell-command-line-windows-10)
- [Installieren und Verwenden der Linux Bash Shell unter Windows
  10](https://www.howtogeek.com/249966/how-to-install-and-use-the-linux-bash-shell-on-windows-10/)
- [Verwenden der Windows 10 Bash
  Shell](https://www.howtogeek.com/265900/everything-you-can-do-with-windows-10s-new-bash-shell/)
- [Einen UNIX/Linux-Emulator (Cygwin) oder Secure Shell (SSH) Client (Putty)
  verwenden](https://faculty.smu.edu/reynolds/unixtut/windows.html)

### Handbücher

- [GNU Handbücher](https://www.gnu.org/manual/manual.html)
- [GNU
  Kerndienstprogramme](https://www.gnu.org/software/coreutils/manual/coreutils.html)

### Verschiedenes

- [Nordpazifischer Wirbelsturm](https://en.wikipedia.org/wiki/North_Pacific_Gyre)
- [Great Pacific Garbage
  Patch](https://en.wikipedia.org/wiki/Great_Pacific_Garbage_Patch)
- ['Die Langlebigkeit digitaler Informationen sicherstellen' von Jeff
  Rothenberg](https://www.clir.org/pubs/archives/ensuring.pdf)
- [Computerfehler-Haikus](https://wiki.c2.com/?ComputerErrorHaiku)
- [Wie man Dateien schön benennt, von Jenny
  Bryan](https://speakerdeck.com/jennybc/how-to-name-files)


