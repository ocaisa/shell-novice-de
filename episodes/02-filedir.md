---
title: Dateien und Verzeichnisse durchsuchen
teaching: 30
exercises: 10
---


::::::::::::::::::::::::::::::::::::::: objectives

- Erläutern Sie die Gemeinsamkeiten und Unterschiede zwischen einer Datei und einem
  Verzeichnis.
- Übersetzt einen absoluten Pfad in einen relativen Pfad und umgekehrt.
- Konstruieren Sie absolute und relative Pfade, die bestimmte Dateien und Verzeichnisse
  identifizieren.
- Verwenden Sie Optionen und Argumente, um das Verhalten eines Shell-Befehls zu ändern.
- Demonstrieren Sie die Verwendung der Tabulatorvervollständigung und erklären Sie ihre
  Vorteile.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- Wie kann ich mich auf meinem Computer bewegen?
- Wie kann ich sehen, welche Dateien und Verzeichnisse ich habe?
- Wie kann ich den Speicherort einer Datei oder eines Verzeichnisses auf meinem Computer
  angeben?

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: instructor

Die Einführung und Navigation im Dateisystem in der Shell (behandelt im Abschnitt
[Navigieren in Dateien und Verzeichnissen](02-filedir.md)) kann verwirrend sein. Sie
können sowohl das Terminal als auch den GUI-Dateiexplorer nebeneinander geöffnet haben,
damit die Lernenden den Inhalt und die Dateistruktur sehen können, während sie das
Terminal zum Navigieren im System verwenden.

::::::::::::::::::::::::::::::::::::::::::::::::::

Der Teil des Betriebssystems, der für die Verwaltung von Dateien und Verzeichnissen
zuständig ist, wird **Dateisystem** genannt. Es organisiert unsere Daten in Dateien, die
Informationen enthalten, und Verzeichnissen (auch "Ordner" genannt), die Dateien oder
andere Verzeichnisse enthalten.

Mehrere Befehle werden häufig verwendet, um Dateien und Verzeichnisse zu erstellen, zu
überprüfen, umzubenennen und zu löschen. Um sie zu erforschen, gehen wir zu unserem
offenen Shell-Fenster.

Lassen Sie uns zuerst herausfinden, wo wir uns befinden, indem wir einen Befehl namens
`pwd` ausführen (was für 'print working directory' steht). Verzeichnisse sind wie *Orte*
- zu jeder Zeit, während wir die Shell benutzen, sind wir an genau einem Ort, der unser
**aktuelles Arbeitsverzeichnis** genannt wird. Befehle lesen und schreiben meist Dateien
im aktuellen Arbeitsverzeichnis, d.h. 'hier', daher ist es wichtig zu wissen, wo man
sich befindet, bevor man einen Befehl ausführt.`pwd` zeigt Ihnen, wo Sie sich befinden:

```bash
$ pwd
```

```output
/Users/nelle
```

Hier ist die Antwort des Computers `/Users/nelle`, was Nelles **Home-Verzeichnis** ist:

::::::::::::::::::::::::::::::::::::::::: callout

## Home-Verzeichnis Variation

Der Pfad zum Heimatverzeichnis sieht auf verschiedenen Betriebssystemen unterschiedlich
aus. Unter Linux kann er wie `/home/nelle` aussehen, und unter Windows wird er ähnlich
wie `C:\Documents and Settings\nelle` oder `C:\Users\nelle` sein. (Beachten Sie, dass es
bei verschiedenen Windows-Versionen etwas anders aussehen kann.) In den zukünftigen
Beispielen haben wir die Mac-Ausgabe als Standard verwendet - die Linux- und
Windows-Ausgabe kann leicht abweichen, sollte aber im Allgemeinen ähnlich sein.

Wir nehmen auch an, dass der Befehl `pwd` das Home-Verzeichnis des Benutzers zurückgibt.
Wenn `pwd` etwas anderes zurückgibt, müssen Sie möglicherweise mit `cd` dorthin
navigieren, oder einige Befehle in dieser Lektion werden nicht wie beschrieben
funktionieren. Siehe [Andere Verzeichnisse erforschen](#exploring-other-directories) für
weitere Details über den `cd` Befehl.


::::::::::::::::::::::::::::::::::::::::::::::::::

Um zu verstehen, was ein "Heimatverzeichnis" ist, schauen wir uns an, wie das
Dateisystem als Ganzes organisiert ist. Für dieses Beispiel werden wir das Dateisystem
auf dem Computer unserer Wissenschaftlerin Nelle darstellen. Nach dieser
Veranschaulichung werden Sie Befehle lernen, um Ihr eigenes Dateisystem zu erforschen,
das ähnlich aufgebaut sein wird, aber nicht exakt identisch ist.

Auf Nelle's Computer sieht das Dateisystem wie folgt aus:

![](fig/filesystem.svg){alt='Das Dateisystem besteht aus einem Stammverzeichnis, das
Unterverzeichnisse mit den Namen bin, data, users und tmp enthält'}

Das Dateisystem sieht aus wie ein auf dem Kopf stehender Baum. Das oberste Verzeichnis
ist das **Wurzelverzeichnis**, das alles andere enthält. Wir verweisen auf es mit einem
Schrägstrich, `/`, allein; dieses Zeichen ist der führende Schrägstrich in
`/Users/nelle`.

Innerhalb dieses Verzeichnisses gibt es mehrere andere Verzeichnisse: `bin` (wo einige
eingebaute Programme gespeichert werden), `data` (für verschiedene Datendateien),
`Users` (wo sich die persönlichen Verzeichnisse der Benutzer befinden), `tmp` (für
temporäre Dateien, die nicht langfristig gespeichert werden müssen), und so weiter.

Wir wissen, dass unser aktuelles Arbeitsverzeichnis `/Users/nelle` innerhalb von
`/Users` gespeichert ist, weil `/Users` der erste Teil seines Namens ist. Ebenso wissen
wir, dass `/Users` innerhalb des Stammverzeichnisses `/` gespeichert ist, weil sein Name
mit `/` beginnt.

::::::::::::::::::::::::::::::::::::::::: callout

## Schrägstriche

Beachten Sie, dass es zwei Bedeutungen für das Zeichen `/` gibt. Wenn es am Anfang eines
Datei- oder Verzeichnisnamens steht, bezieht es sich auf das Stammverzeichnis. Wenn es
*innerhalb* eines Pfades erscheint, ist es nur ein Trennzeichen.


::::::::::::::::::::::::::::::::::::::::::::::::::

Unter `/Users` finden wir ein Verzeichnis für jeden Benutzer mit einem Konto auf Nelles
Rechner, ihre Kollegen *imhotep* und *larry*.

![](fig/home-directories.svg){alt='Wie andere Verzeichnisse sind Home-Verzeichnisse
Unterverzeichnisse unterhalb von "/Users" wie "/Users/imhotep", "/Users/larry"
oder"/Users/nelle"'}

Die Dateien des Benutzers *imhotep* sind in `/Users/imhotep` gespeichert, die des
Benutzers *larry* in `/Users/larry` und die von Nelle in `/Users/nelle`. Nelle ist der
Benutzer in unseren Beispielen hier; daher bekommen wir `/Users/nelle` als unser
Heimatverzeichnis. Wenn Sie eine neue Eingabeaufforderung öffnen, befinden Sie sich
normalerweise zunächst in Ihrem Heimatverzeichnis.

Jetzt wollen wir den Befehl lernen, mit dem wir den Inhalt unseres eigenen Dateisystems
sehen können. Wir können sehen, was sich in unserem Heimatverzeichnis befindet, indem
wir `ls` ausführen:

```bash
$ ls
```

```output
Applications Documents    Library      Music        Public
Desktop      Downloads    Movies       Pictures
```

(Auch hier können die Ergebnisse je nach Betriebssystem und Anpassung des Dateisystems
leicht unterschiedlich ausfallen)

`ls` gibt die Namen der Dateien und Verzeichnisse im aktuellen Verzeichnis aus. Wir
können die Ausgabe verständlicher machen, indem wir die **Option** `-F` verwenden, die
`ls` anweist, die Ausgabe zu klassifizieren, indem es den Datei- und Verzeichnisnamen
eine Markierung hinzufügt, um anzuzeigen, was sie sind:

- ein nachgestelltes `/` zeigt an, dass dies ein Verzeichnis ist
- `@` zeigt einen Link an
- `*` zeigt eine ausführbare Datei an

Abhängig von den Standardeinstellungen Ihrer Shell kann die Shell auch Farben verwenden,
um anzuzeigen, ob ein Eintrag eine Datei oder ein Verzeichnis ist.

```bash
$ ls -F
```

```output
Applications/ Documents/    Library/      Music/        Public/
Desktop/      Downloads/    Movies/       Pictures/
```

Hier kann man sehen, dass das Home-Verzeichnis nur **Unterverzeichnisse** enthält. Alle
Namen in der Ausgabe, die kein Klassifizierungssymbol haben, sind **Dateien** im
aktuellen Arbeitsverzeichnis.

::::::::::::::::::::::::::::::::::::::::: callout

## Löschen des Terminals

Wenn Ihr Bildschirm zu unübersichtlich wird, können Sie Ihr Terminal mit dem Befehl
`clear` leeren. Sie können immer noch auf frühere Befehle zugreifen, indem Sie
<kbd>↑</kbd> und <kbd>↓</kbd> verwenden, um sich Zeile für Zeile zu bewegen, oder indem
Sie in Ihrem Terminal scrollen.


::::::::::::::::::::::::::::::::::::::::::::::::::

### Hilfe holen

`ls` hat eine Menge anderer **Optionen**. Es gibt zwei übliche Wege, um herauszufinden,
wie man einen Befehl benutzt und welche Optionen er akzeptiert --- **Abhängig von Ihrer
Umgebung könnte es sein, dass nur einer dieser Wege funktioniert:**

1. Wir können die Option `--help` an jeden Befehl übergeben (verfügbar unter Linux und
   Git Bash), zum Beispiel:

  ```bash
  $ ls --help
  ```

2. Wir können sein Handbuch mit `man` lesen (verfügbar auf Linux und macOS):

  ```bash
  $ man ls
  ```

Wir werden im Folgenden beide Möglichkeiten beschreiben.

::::::::::::::::::::::::::::::::::::::::: callout

## Hilfe für eingebaute Befehle

Einige Befehle sind in die Bash-Shell eingebaut, anstatt als separate Programme im
Dateisystem zu existieren. Ein Beispiel ist der Befehl `cd` (Verzeichnis wechseln). Wenn
Sie eine Meldung wie `No manual entry for cd` erhalten, versuchen Sie stattdessen `help
cd`. Mit dem Befehl `help` erhalten Sie Nutzungsinformationen für [Bash
built-ins](https://www.gnu.org/software/bash/manual/html_node/Bash-Builtins.html).


::::::::::::::::::::::::::::::::::::::::::::::::::

#### Die `--help` Option

Die meisten Bash-Befehle und -Programme, die für die Ausführung innerhalb der Bash
geschrieben wurden, unterstützen eine Option `--help`, die weitere Informationen zur
Verwendung des Befehls oder Programms anzeigt.

```bash
$ ls --help
```

```output
Usage: ls [OPTION]... [FILE]...
List information about the FILEs (the current directory by default).
Sort entries alphabetically if neither -cftuvSUX nor --sort is specified.

Mandatory arguments to long options are mandatory for short options, too.
  -a, --all                  do not ignore entries starting with .
  -A, --almost-all           do not list implied . and ..
      --author               with -l, print the author of each file
  -b, --escape               print C-style escapes for nongraphic characters
      --block-size=SIZE      scale sizes by SIZE before printing them; e.g.,
                               '--block-size=M' prints sizes in units of
                               1,048,576 bytes; see SIZE format below
  -B, --ignore-backups       do not list implied entries ending with ~
  -c                         with -lt: sort by, and show, ctime (time of last
                               modification of file status information);
                               with -l: show ctime and sort by name;
                               otherwise: sort by ctime, newest first
  -C                         list entries by columns
      --color[=WHEN]         colorize the output; WHEN can be 'always' (default
                               if omitted), 'auto', or 'never'; more info below
  -d, --directory            list directories themselves, not their contents
  -D, --dired                generate output designed for Emacs' dired mode
  -f                         do not sort, enable -aU, disable -ls --color
  -F, --classify             append indicator (one of */=>@|) to entries
...        ...        ...
```

::::::::::::::::::::::::::::::::::::::::: callout

### Wann sollte man kurze oder lange Optionen verwenden?
Wenn Optionen sowohl als kurze als auch als lange Optionen vorhanden sind:

- Verwenden Sie die Option short, wenn Sie Befehle direkt in die Shell eingeben, um die
  Anzahl der Tastenanschläge zu minimieren und Ihre Aufgabe schneller zu erledigen.
- Verwenden Sie die Option long in Skripten, um Klarheit zu schaffen. Sie wird viele
  Male gelesen und nur einmal eingegeben.

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::: callout

## Nicht unterstützte Kommandozeilenoptionen

Wenn Sie versuchen, eine Option zu verwenden, die nicht unterstützt wird, geben `ls` und
andere Befehle normalerweise eine Fehlermeldung ähnlich der folgenden aus:

```bash
$ ls -j
```

```error
ls: invalid option -- 'j'
Try 'ls --help' for more information.
```

::::::::::::::::::::::::::::::::::::::::::::::::::

#### Der `man` Befehl

Die andere Möglichkeit, etwas über `ls` zu erfahren, ist die Eingabe von

```bash
$ man ls
```

Dieser Befehl verwandelt Ihr Terminal in eine Seite mit einer Beschreibung des Befehls
`ls` und seiner Optionen.

Um durch die `man`-Seiten zu navigieren, können Sie <kbd>↑</kbd> und <kbd>↓</kbd>
benutzen, um sich zeilenweise zu bewegen, oder versuchen Sie <kbd>b</kbd> und
<kbd>Leertaste</kbd>, um eine ganze Seite nach oben oder unten zu springen. Um nach
einem Zeichen oder Wort in den `man`-Seiten zu suchen, verwenden Sie <kbd>/</kbd>,
gefolgt von dem Zeichen oder Wort, das Sie suchen. Manchmal führt eine Suche zu mehreren
Treffern. In diesem Fall können Sie zwischen den Treffern mit <kbd>N</kbd> (vorwärts)
und <kbd>Shift</kbd>\+<kbd>N</kbd> (rückwärts) wechseln.

Um die `man`-Seiten zu **beenden**, drücken Sie <kbd>q</kbd>.

::::::::::::::::::::::::::::::::::::::::: callout

## Manual pages on the web

Natürlich gibt es noch eine dritte Möglichkeit, auf die Hilfe für Befehle zuzugreifen:
die Suche im Internet über Ihren Webbrowser. Wenn Sie die Internetsuche verwenden, hilft
es, den Ausdruck `unix man page` in Ihre Suchanfrage aufzunehmen, um relevante
Ergebnisse zu finden.

GNU bietet Links zu seinen [Handbüchern](https://www.gnu.org/manual/manual.html)
einschließlich der [core GNU
utilities](https://www.gnu.org/software/coreutils/manual/coreutils.html), die viele in
dieser Lektion vorgestellte Befehle abdeckt.


::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Weitere `ls`-Optionen erforschen

Sie können auch zwei Optionen gleichzeitig verwenden. Was bewirkt der Befehl `ls`, wenn
er mit der Option `-l` verwendet wird? Was ist, wenn man sowohl die Option `-l` als auch
die Option `-h` verwendet?

Ein Teil der Ausgabe bezieht sich auf Eigenschaften, die wir in dieser Lektion nicht
behandeln (wie z.B. Dateiberechtigungen und Besitzverhältnisse), aber der Rest sollte
trotzdem nützlich sein.

::::::::::::::: solution

## Lösung

Die Option `-l` bewirkt, dass `ls` ein **l**langes Auflistungsformat verwendet, das
nicht nur die Datei-/Verzeichnisnamen, sondern auch zusätzliche Informationen wie die
Dateigröße und den Zeitpunkt der letzten Änderung anzeigt. Wenn Sie sowohl die Option
`-h` als auch die Option `-l` verwenden, macht dies die Dateigröße '**h**menschlich
lesbar', d.h. es wird etwas wie `5.3K` statt `5369` angezeigt.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Auflistung in umgekehrter chronologischer Reihenfolge

Standardmäßig listet `ls` den Inhalt eines Verzeichnisses in alphabetischer Reihenfolge
nach Namen auf. Der Befehl `ls -t` listet den Inhalt eines Verzeichnisses nicht
alphabetisch, sondern nach dem Zeitpunkt der letzten Änderung auf. Der Befehl `ls -r`
listet den Inhalt eines Verzeichnisses in umgekehrter Reihenfolge auf. Welche Datei wird
zuletzt angezeigt, wenn Sie die Optionen `-t` und `-r` kombinieren? Hinweis:
Möglicherweise müssen Sie die Option `-l` verwenden, um das Datum der letzten Änderung
zu sehen.

::::::::::::::: solution

## Lösung

Die zuletzt geänderte Datei wird zuletzt aufgelistet, wenn `-rt` verwendet wird. Dies
kann sehr nützlich sein, um die letzten Bearbeitungen zu finden oder zu prüfen, ob eine
neue Ausgabedatei geschrieben wurde.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

### Erforschung anderer Verzeichnisse

Wir können `ls` nicht nur für das aktuelle Arbeitsverzeichnis verwenden, sondern auch,
um den Inhalt eines anderen Verzeichnisses aufzulisten. Werfen wir einen Blick auf unser
Verzeichnis `Desktop`, indem wir `ls -F Desktop` ausführen, d.h. den Befehl `ls` mit der
**Option** `-F` und dem [**Argument**][Argumente] `Desktop`. Das Argument `Desktop` sagt
`ls`, dass wir eine Auflistung von etwas anderem als unserem aktuellen
Arbeitsverzeichnis wollen:

```bash
$ ls -F Desktop
```

```output
shell-lesson-data/
```

Beachten Sie, dass dieser Befehl einen Fehler zurückgibt, wenn ein Verzeichnis namens
`Desktop` in Ihrem aktuellen Arbeitsverzeichnis nicht existiert. Normalerweise existiert
ein `Desktop`-Verzeichnis in Ihrem Home-Verzeichnis, von dem wir annehmen, dass es das
aktuelle Arbeitsverzeichnis Ihrer Bash-Shell ist.

Ihre Ausgabe sollte eine Liste aller Dateien und Unterverzeichnisse in Ihrem
Desktop-Verzeichnis sein, einschließlich des `shell-lesson-data`-Verzeichnisses, das Sie
im [Setup für diese Lektion](../learners/setup.md) heruntergeladen haben. (Auf den
meisten Systemen wird der Inhalt des Verzeichnisses `Desktop` in der Shell als Symbole
in einer grafischen Benutzeroberfläche hinter allen offenen Fenstern angezeigt. Prüfen
Sie, ob dies bei Ihnen der Fall ist.)

Die hierarchische Organisation von Dingen hilft uns, den Überblick über unsere Arbeit zu
behalten. Es ist zwar möglich, Hunderte von Dateien in unserem Home-Verzeichnis
abzulegen, so wie es möglich ist, Hunderte von gedruckten Papieren auf unserem
Schreibtisch zu stapeln, aber es ist viel einfacher, Dinge zu finden, wenn sie in
sinnvoll benannten Unterverzeichnissen organisiert sind.

Jetzt, da wir wissen, dass sich das Verzeichnis `shell-lesson-data` in unserem
Desktop-Verzeichnis befindet, können wir zwei Dinge tun.

Zuerst können wir mit der gleichen Strategie wie zuvor den Inhalt der Datei betrachten,
indem wir einen Verzeichnisnamen an `ls` übergeben:

```bash
$ ls -F Desktop/shell-lesson-data
```

```output
exercise-data/  north-pacific-gyre/
```

Zweitens können wir unseren Standort in ein anderes Verzeichnis ändern, so dass wir uns
nicht mehr in unserem Heimatverzeichnis befinden.

Der Befehl zum Wechseln der Speicherorte ist `cd` gefolgt von einem Verzeichnisnamen, um
unser Arbeitsverzeichnis zu wechseln.`cd` steht für "Verzeichnis wechseln", was ein
wenig irreführend ist. Der Befehl wechselt nicht das Verzeichnis, sondern das aktuelle
Arbeitsverzeichnis der Shell. Mit anderen Worten, er ändert die Einstellungen der Shell,
in welchem Verzeichnis wir uns befinden. Der Befehl `cd` ist vergleichbar mit einem
Doppelklick auf einen Ordner in einer grafischen Oberfläche, um in diesen Ordner zu
gelangen.

Nehmen wir an, wir wollen in das Verzeichnis `exercise-data` wechseln, das wir oben
gesehen haben. Wir können die folgende Reihe von Befehlen verwenden, um dorthin zu
gelangen:

```bash
$ cd Desktop
$ cd shell-lesson-data
$ cd exercise-data
```

Diese Befehle verschieben uns von unserem Home-Verzeichnis in unser Desktop-Verzeichnis,
dann in das Verzeichnis `shell-lesson-data` und dann in das Verzeichnis `exercise-data`.
Sie werden feststellen, dass `cd` nichts ausgibt. Das ist normal. Viele Shell-Befehle
geben bei erfolgreicher Ausführung nichts auf dem Bildschirm aus. Wenn wir aber `pwd`
danach ausführen, können wir sehen, dass wir jetzt in
`/Users/nelle/Desktop/shell-lesson-data/exercise-data` sind.

Wenn wir `ls -F` jetzt ohne Argumente ausführen, listet es den Inhalt von
`/Users/nelle/Desktop/shell-lesson-data/exercise-data` auf, weil wir uns jetzt dort
befinden:

```bash
$ pwd
```

```output
/Users/nelle/Desktop/shell-lesson-data/exercise-data
```

```bash
$ ls -F
```

```output
alkanes/  animal-counts/  creatures/  numbers.txt  writing/
```

Wir wissen jetzt, wie wir im Verzeichnisbaum nach unten gehen (d.h. wie wir in ein
Unterverzeichnis gehen), aber wie gehen wir nach oben (d.h. wie verlassen wir ein
Verzeichnis und gehen in sein übergeordnetes Verzeichnis)? Wir könnten das Folgende
versuchen:

```bash
$ cd shell-lesson-data
```

```error
-bash: cd: shell-lesson-data: No such file or directory
```

Aber wir bekommen einen Fehler! Woran liegt das?

Mit unseren bisherigen Methoden kann `cd` nur Unterverzeichnisse innerhalb Ihres
aktuellen Verzeichnisses anzeigen. Es gibt verschiedene Möglichkeiten, Verzeichnisse
oberhalb des aktuellen Standorts zu sehen; wir beginnen mit der einfachsten.

Es gibt eine Abkürzung in der Shell, um eine Verzeichnisebene nach oben zu gehen. Sie
funktioniert wie folgt:

```bash
$ cd ..
```

`..` ist ein spezieller Verzeichnisname, der "das Verzeichnis, das dieses enthält"
bedeutet, oder einfacher ausgedrückt, das **Elternteil** des aktuellen Verzeichnisses.
Sicherlich, wenn wir `pwd` nach `cd ..` ausführen, sind wir wieder in
`/Users/nelle/Desktop/shell-lesson-data`:

```bash
$ pwd
```

```output
/Users/nelle/Desktop/shell-lesson-data
```

Das spezielle Verzeichnis `..` wird normalerweise nicht angezeigt, wenn wir `ls`
ausführen. Wenn wir es anzeigen wollen, können wir die Option `-a` zu `ls -F`
hinzufügen:

```bash
$ ls -F -a
```

```output
./  ../  exercise-data/  north-pacific-gyre/
```

`-a` steht für 'show all' (einschließlich versteckter Dateien); es zwingt `ls` dazu, uns
Datei- und Verzeichnisnamen zu zeigen, die mit `.` beginnen, wie z.B. `..` (was sich,
wenn wir in `/Users/nelle` sind, auf das Verzeichnis `/Users` bezieht). Wie Sie sehen
können, wird auch ein anderes spezielles Verzeichnis angezeigt, das einfach `.` heißt,
was "das aktuelle Arbeitsverzeichnis" bedeutet. Es mag überflüssig erscheinen, einen
Namen dafür zu haben, aber wir werden bald einige Anwendungen dafür sehen.

Beachten Sie, dass in den meisten Kommandozeilen-Tools mehrere Optionen mit einem
einzigen `-` und ohne Leerzeichen zwischen den Optionen kombiniert werden können; `ls -F
-a` ist äquivalent zu `ls -Fa`.

::::::::::::::::::::::::::::::::::::::::: callout

## Andere versteckte Dateien

Zusätzlich zu den versteckten Verzeichnissen `..` und `.` können Sie auch eine Datei
namens `.bash_profile` sehen. Diese Datei enthält normalerweise Einstellungen für die
Shell-Konfiguration. Sie können auch andere Dateien und Verzeichnisse sehen, die mit `.`
beginnen. Dies sind normalerweise Dateien und Verzeichnisse, die zur Konfiguration
verschiedener Programme auf Ihrem Computer verwendet werden. Das Präfix `.` wird
verwendet, um zu verhindern, dass diese Konfigurationsdateien das Terminal überladen,
wenn ein Standardbefehl `ls` verwendet wird.


::::::::::::::::::::::::::::::::::::::::::::::::::

Diese drei Befehle sind die grundlegenden Befehle zum Navigieren im Dateisystem Ihres
Computers: `pwd`, `ls` und `cd`. Lassen Sie uns einige Variationen dieser Befehle
untersuchen. Was passiert, wenn Sie `cd` allein eingeben, ohne ein Verzeichnis
anzugeben?

```bash
$ cd
```

Wie können Sie überprüfen, was passiert ist? `pwd` gibt uns die Antwort!

```bash
$ pwd
```

```output
/Users/nelle
```

Es hat sich herausgestellt, dass `cd` ohne ein Argument Sie zu Ihrem Heimatverzeichnis
zurückbringt, was großartig ist, wenn Sie sich in Ihrem eigenen Dateisystem verirrt
haben.

Versuchen wir, zum Verzeichnis `exercise-data` von vorhin zurückzukehren. Beim letzten
Mal haben wir drei Befehle verwendet, aber wir können die Liste der Verzeichnisse, die
wir nach `exercise-data` verschieben wollen, in einem Schritt zusammenstellen:

```bash
$ cd Desktop/shell-lesson-data/exercise-data
```

Überprüfen Sie, ob wir uns an die richtige Stelle bewegt haben, indem Sie `pwd` und `ls
-F` ausführen.

Wenn wir vom Datenverzeichnis eine Ebene nach oben gehen wollen, können wir `cd ..`
verwenden. Es gibt aber noch eine andere Möglichkeit, in ein beliebiges Verzeichnis zu
wechseln, unabhängig davon, wo man sich gerade befindet.

Bislang haben wir bei der Angabe von Verzeichnisnamen oder sogar eines Verzeichnispfades
(wie oben) **relative Pfade** verwendet. Wenn Sie einen relativen Pfad mit einem Befehl
wie `ls` oder `cd` verwenden, wird versucht, diesen Ort von der Stelle aus zu finden, an
der wir uns befinden, und nicht von der Wurzel des Dateisystems.

Es ist jedoch möglich, den **absoluten Pfad** zu einem Verzeichnis anzugeben, indem man
den gesamten Pfad vom Stammverzeichnis aus einschließt, was durch einen führenden
Schrägstrich angezeigt wird. Der führende Schrägstrich sagt dem Computer, dass er den
Pfad vom Stammverzeichnis des Dateisystems aus verfolgen soll, so dass er sich immer auf
genau ein Verzeichnis bezieht, egal wo wir uns befinden, wenn wir den Befehl ausführen.

Dies erlaubt es uns, unser `shell-lesson-data`-Verzeichnis von überall im Dateisystem zu
erreichen (auch innerhalb von `exercise-data`). Um den absoluten Pfad zu finden, den wir
suchen, können wir `pwd` verwenden und dann das Stück extrahieren, das wir nach
`shell-lesson-data` verschieben wollen.

```bash
$ pwd
```

```output
/Users/nelle/Desktop/shell-lesson-data/exercise-data
```

```bash
$ cd /Users/nelle/Desktop/shell-lesson-data
```

Führen Sie `pwd` und `ls -F` aus, um sicherzustellen, dass wir uns in dem Verzeichnis
befinden, das wir erwarten.

::::::::::::::::::::::::::::::::::::::::: callout

## Zwei weitere Abkürzungen

Die Shell interpretiert ein Tilde-Zeichen (`~`) am Anfang eines Pfades als "das
Heimatverzeichnis des aktuellen Benutzers". Wenn zum Beispiel Nelles Heimatverzeichnis
`/Users/nelle` ist, dann ist `~/data` äquivalent zu `/Users/nelle/data`. Das
funktioniert nur, wenn es das erste Zeichen im Pfad ist; `here/there/~/elsewhere` ist
*nicht* `here/there/Users/nelle/elsewhere`.

Eine weitere Abkürzung ist das Zeichen `-` (Bindestrich). mit `cd` wird `-` in *das
vorherige Verzeichnis, in dem ich mich befand*, übersetzt, was schneller ist, als sich
den vollständigen Pfad zu merken und dann einzugeben. Dies ist ein *sehr* effizienter
Weg, um *zwischen zwei Verzeichnissen hin und her zu wechseln* -- d.h. wenn Sie `cd -`
zweimal ausführen, landen Sie wieder im Ausgangsverzeichnis.

Der Unterschied zwischen `cd ..` und `cd -` ist, dass ersteres Sie *nach oben* bringt,
während letzteres Sie *zurück* bringt.

***

Versuchen Sie es! Navigieren Sie zunächst zu `~/Desktop/shell-lesson-data` (Sie sollten
bereits dort sein).

```bash
$ cd ~/Desktop/shell-lesson-data
```

Dann `cd` in das `exercise-data/creatures` Verzeichnis

```bash
$ cd exercise-data/creatures
```

Wenn Sie nun

```bash
$ cd -
```

Sie werden sehen, dass Sie wieder in `~/Desktop/shell-lesson-data` sind. Führen Sie `cd
-` erneut aus und Sie befinden sich wieder in
`~/Desktop/shell-lesson-data/exercise-data/creatures`


::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Absolute vs. Relative Pfade

Welchen der folgenden Befehle könnte Nelle ausgehend von `/Users/nelle/data` verwenden,
um zu ihrem Heimatverzeichnis zu navigieren, das `/Users/nelle` ist?

1. `cd .`
2. `cd /`
3. `cd /home/nelle`
4. `cd ../..`
5. `cd ~`
6. `cd home`
7. `cd ~/data/..`
8. `cd`
9. `cd ..`

::::::::::::::: solution

## Lösung

1. Nein: `.` steht für das aktuelle Verzeichnis.
2. Nein: `/` steht für das Stammverzeichnis.
3. Nein: Nelle's Heimatverzeichnis ist `/Users/nelle`.
4. Nein: Dieser Befehl geht zwei Ebenen nach oben, d.h. er endet mit `/Users`.
5. Ja: `~` steht für das Heimatverzeichnis des Benutzers, in diesem Fall `/Users/nelle`.
6. Nein: Dieser Befehl würde in ein Verzeichnis `home` im aktuellen Verzeichnis
   navigieren, wenn es existiert.
7. Ja: unnötig kompliziert, aber korrekt.
8. Ja: Abkürzung, um zum Heimatverzeichnis des Benutzers zurückzukehren.
9. Ja: geht eine Ebene höher.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Relative Pfadauflösung

Wenn `pwd` `/Users/thing` anzeigt, was zeigt dann `ls -F ../backup` im untenstehenden
Dateisystemdiagramm an?

1. `../backup: No such file or directory`
2. `2012-12-01 2013-01-08 2013-01-27`
3. `2012-12-01/ 2013-01-08/ 2013-01-27/`
4. `original/ pnas_final/ pnas_sub/`

![](fig/filesystem-challenge.svg){alt='Ein Verzeichnisbaum unterhalb des
Users-Verzeichnisses, in dem "/Users" die Verzeichnisse "backup" und "thing" enthält;
"/Users/backup" enthält "original", "pnas\_final" und "pnas\_sub"; "/Users/thing"
enthält "backup"; und "/Users/thing/backup" enthält "2012-12-01", "2013-01-08" und
"2013-01-27"'}

::::::::::::::: solution

## Lösung

1. Nein: Es *gibt* ein Verzeichnis `backup` in `/Users`.
2. Nein: dies ist der Inhalt von `Users/thing/backup`, aber mit `..` haben wir nach
   einer Ebene weiter oben gefragt.
3. Nein: siehe vorherige Erklärung.
4. Ja: `../backup/` verweist auf `/Users/backup/`.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## `ls` Reading Comprehension

Wenn `pwd` `/Users/backup` anzeigt und `-r` `ls` anweist, die Dinge in umgekehrter
Reihenfolge anzuzeigen, welche(s) Kommando(s) führt/führen zu folgender Ausgabe, wenn
man das untenstehende Dateisystemdiagramm verwendet

```output
pnas_sub/ pnas_final/ original/
```

![](fig/filesystem-challenge.svg){alt='Ein Verzeichnisbaum unterhalb des
Users-Verzeichnisses, in dem "/Users" die Verzeichnisse "backup" und "thing" enthält;
"/Users/backup" enthält "original", "pnas\_final" und "pnas\_sub"; "/Users/thing"
enthält "backup"; und "/Users/thing/backup" enthält "2012-12-01", "2013-01-08" und
"2013-01-27"'}

1. `ls pwd`
2. `ls -r -F`
3. `ls -r -F /Users/backup`

::::::::::::::: solution

## Lösung

1. Nein: `pwd` ist nicht der Name eines Verzeichnisses.
2. Ja: `ls` ohne Verzeichnisargument listet Dateien und Verzeichnisse im aktuellen
   Verzeichnis auf.
3. Ja: verwendet explizit den absoluten Pfad.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

## Allgemeine Syntax eines Shell-Befehls

Wir haben nun Befehle, Optionen und Argumente kennengelernt, aber es ist vielleicht
sinnvoll, einige Begriffe zu formalisieren.

Betrachten Sie den folgenden Befehl als ein allgemeines Beispiel für einen Befehl, den
wir in seine Bestandteile zerlegen werden:

```bash
$ ls -F /
```

![](fig/shell_command_syntax.svg){alt='Allgemeine Syntax eines Shell-Befehls'}

`ls` ist der **Befehl**, mit einer **Option** `-F` und einem **Argument** `/`. Wir haben
bereits Optionen kennengelernt, die entweder mit einem einzelnen Bindestrich beginnen
(`-`), bekannt als **kurze Optionen**, oder mit zwei Bindestrichen (`--`), bekannt als
**lange Optionen**. [Optionen] ändern das Verhalten eines Befehls und Argumente] sagen
dem Befehl, womit er arbeiten soll (z.B. Dateien und Verzeichnisse). Manchmal werden
Optionen und Argumente auch als **Parameter** bezeichnet. Ein Befehl kann mit mehr als
einer Option und mehr als einem Argument aufgerufen werden, aber ein Befehl benötigt
nicht immer ein Argument oder eine Option.

Manchmal sieht man, dass Optionen als **Schalter** oder **Flags** bezeichnet werden,
besonders bei Optionen, die kein Argument benötigen. In dieser Lektion werden wir bei
dem Begriff *Option* bleiben.

Jeder Teil ist durch Leerzeichen getrennt. Wenn Sie das Leerzeichen zwischen `ls` und
`-F` weglassen, sucht die Shell nach einem Befehl namens `ls-F`, den es nicht gibt. Auch
die Großschreibung kann wichtig sein. Zum Beispiel zeigt `ls -s` die Größe von Dateien
und Verzeichnissen neben den Namen an, während `ls -S` die Dateien und Verzeichnisse
nach Größe sortiert, wie unten gezeigt:

```bash
$ cd ~/Desktop/shell-lesson-data
$ ls -s exercise-data
```

```output
total 28
 4 animal-counts   4 creatures  12 numbers.txt   4 alkanes   4 writing
```

Beachten Sie, dass die von `ls -s` zurückgegebenen Größen in *Blöcken* angegeben sind.
Da diese für verschiedene Betriebssysteme unterschiedlich definiert sind, erhalten Sie
möglicherweise nicht die gleichen Zahlen wie im Beispiel.

```bash
$ ls -S exercise-data
```

```output
animal-counts  creatures  alkanes  writing  numbers.txt
```

Wenn man das alles zusammennimmt, erhält man mit dem obigen Befehl `ls -F /` eine Liste
der Dateien und Verzeichnisse im Stammverzeichnis `/`. Ein Beispiel für die Ausgabe, die
Sie mit dem obigen Befehl erhalten könnten, finden Sie unten:

```bash
$ ls -F /
```

```output
Applications/         System/
Library/              Users/
Network/              Volumes/
```

### Nelle's Pipeline: Organisieren von Dateien

Mit diesem Wissen über Dateien und Verzeichnisse ist Nelle bereit, die Dateien zu
organisieren, die die Protein-Assay-Maschine erstellen wird.

Sie legt ein Verzeichnis mit dem Namen `north-pacific-gyre` an (um sich daran zu
erinnern, woher die Daten stammen), das die Datendateien von der Testmaschine und ihre
Datenverarbeitungsskripte enthält.

Jede ihrer physischen Proben ist gemäß der Konvention ihres Labors mit einer eindeutigen
zehnstelligen ID gekennzeichnet, z. B. "NENE01729A". Diese ID hat sie in ihrem
Entnahmeprotokoll verwendet, um den Ort, die Zeit, die Tiefe und andere Merkmale der
Probe aufzuzeichnen, daher beschließt sie, sie im Dateinamen jeder Datendatei zu
verwenden. Da die Ausgabe des Prüfgeräts im Klartext erfolgt, nennt sie ihre Dateien
`NENE01729A.txt`, `NENE01812A.txt` usw. Alle 1520 Dateien werden im selben Verzeichnis
gespeichert.

Jetzt kann Nelle in ihrem aktuellen Verzeichnis `shell-lesson-data` sehen, welche
Dateien sie hat, indem sie den Befehl benutzt:

```bash
$ ls north-pacific-gyre/
```

Dieser Befehl ist eine Menge zu tippen, aber sie kann die Shell die meiste Arbeit durch
die so genannte **Tab-Vervollständigung** erledigen lassen. Wenn sie tippt:

```bash
$ ls nor
```

und drückt dann <kbd>Tab</kbd> (die Tabulator-Taste auf ihrer Tastatur), vervollständigt
die Shell automatisch den Verzeichnisnamen für sie:

```bash
$ ls north-pacific-gyre/
```

Erneutes Drücken von <kbd>Tab</kbd> bringt nichts, da es mehrere Möglichkeiten gibt;
zweimaliges Drücken von <kbd>Tab</kbd> bringt eine Liste aller Dateien.

Wenn Nelle dann <kbd>G</kbd> drückt und dann wieder <kbd>Tab</kbd> drückt, wird die
Shell 'goo' anhängen, da alle Dateien, die mit 'g' beginnen, die ersten drei Zeichen
'goo' gemeinsam haben.

```bash
$ ls north-pacific-gyre/goo
```

Um alle diese Dateien zu sehen, kann sie <kbd>Tab</kbd> noch zweimal drücken.

```bash
ls north-pacific-gyre/goo
goodiff.sh   goostats.sh
```

Dies wird **Tabulatorvervollständigung** genannt, und wir werden es in vielen anderen
Werkzeugen sehen, wenn wir fortfahren.



[Arguments]: https://swcarpentry.github.io/shell-novice/reference.html#argument


:::::::::::::::::::::::::::::::::::::::: keypoints

- Das Dateisystem ist für die Verwaltung von Informationen auf der Festplatte zuständig.
- Informationen werden in Dateien gespeichert, die wiederum in Verzeichnissen (Ordnern)
  abgelegt sind.
- Verzeichnisse können auch andere Verzeichnisse speichern, die dann einen
  Verzeichnisbaum bilden.
- `pwd` gibt das aktuelle Arbeitsverzeichnis des Benutzers aus.
- `ls [path]` gibt eine Auflistung einer bestimmten Datei oder eines bestimmten
  Verzeichnisses aus; `ls` allein listet das aktuelle Arbeitsverzeichnis auf.
- `cd [path]` ändert das aktuelle Arbeitsverzeichnis.
- Die meisten Befehle nehmen Optionen an, die mit einem einzelnen `-` beginnen.
- Verzeichnisnamen in einem Pfad werden unter Unix mit `/` getrennt, unter Windows
  jedoch mit `\`.
- `/` allein ist das Stammverzeichnis des gesamten Dateisystems.
- Ein absoluter Pfad gibt einen Ort an, der vom Stamm des Dateisystems ausgeht.
- Ein relativer Pfad gibt einen Ort an, der von der aktuellen Position ausgeht.
- `.` allein bedeutet 'das aktuelle Verzeichnis'; `..` bedeutet 'das Verzeichnis über
  dem aktuellen'.

::::::::::::::::::::::::::::::::::::::::::::::::::



