---
title: Working With Files and Directories
teaching: 30
exercises: 20
---


::::::::::::::::::::::::::::::::::::::: objectives

- Erstellen Sie eine Verzeichnishierarchie, die einem vorgegebenen Diagramm entspricht.
- Erstellen Sie Dateien in dieser Hierarchie mit Hilfe eines Editors oder durch Kopieren
  und Umbenennen vorhandener Dateien.
- Löschen, Kopieren und Verschieben von angegebenen Dateien und/oder Verzeichnissen.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- Wie kann ich Dateien und Verzeichnisse erstellen, kopieren und löschen?
- Wie kann ich Dateien bearbeiten?

::::::::::::::::::::::::::::::::::::::::::::::::::


## Verzeichnisse erstellen

Wir wissen jetzt, wie wir Dateien und Verzeichnisse erkunden können, aber wie erstellen
wir sie überhaupt?

In dieser Folge lernen wir das Erstellen und Verschieben von Dateien und Verzeichnissen
am Beispiel des Verzeichnisses `exercise-data/writing`.

### Schritt eins: sehen, wo wir sind und was wir schon haben

Wir sollten uns immer noch im Verzeichnis `shell-lesson-data` auf dem Desktop befinden,
was wir mit überprüfen können:

```bash
$ pwd
```

```output
/Users/nelle/Desktop/shell-lesson-data
```

Als nächstes wechseln wir in das Verzeichnis `exercise-data/writing` und schauen, was es
enthält:

```bash
$ cd exercise-data/writing/
$ ls -F
```

```output
haiku.txt  LittleWomen.txt
```

### Erstellen Sie ein Verzeichnis

Erzeugen wir ein neues Verzeichnis mit dem Namen `thesis` mit dem Befehl `mkdir thesis`
(der keine Ausgabe hat):

```bash
$ mkdir thesis
```

Wie der Name schon vermuten lässt, bedeutet `mkdir` "Verzeichnis erstellen". Da `thesis`
ein relativer Pfad ist (d.h. keinen führenden Schrägstrich hat, wie
`/what/ever/thesis`), wird das neue Verzeichnis im aktuellen Arbeitsverzeichnis
erstellt:

```bash
$ ls -F
```

```output
haiku.txt  LittleWomen.txt  thesis/
```

Da wir das Verzeichnis `thesis` gerade erst erstellt haben, befindet sich darin noch
nichts:

```bash
$ ls -F thesis
```

Beachten Sie, dass `mkdir` nicht darauf beschränkt ist, einzelne Verzeichnisse auf
einmal zu erstellen. Die Option `-p` erlaubt es `mkdir`, ein Verzeichnis mit
verschachtelten Unterverzeichnissen in einem einzigen Vorgang zu erstellen:

```bash
$ mkdir -p ../project/data ../project/results
```

Die Option `-R` für den Befehl `ls` listet alle verschachtelten Unterverzeichnisse
innerhalb eines Verzeichnisses auf. Lassen Sie uns `ls -FR` verwenden, um die neue
Verzeichnishierarchie, die wir gerade im Verzeichnis `project` erstellt haben, rekursiv
aufzulisten:

```bash
$ ls -FR ../project
```

```output
../project/:
data/  results/

../project/data:

../project/results:
```

::::::::::::::::::::::::::::::::::::::::: callout

## Zwei Möglichkeiten, das Gleiche zu tun

Die Verwendung der Shell zur Erstellung eines Verzeichnisses unterscheidet sich nicht
von der Verwendung eines Datei-Explorers. Wenn Sie das aktuelle Verzeichnis mit dem
grafischen Dateiexplorer Ihres Betriebssystems öffnen, wird das Verzeichnis `thesis`
auch dort erscheinen. Während die Shell und der Dateiexplorer zwei verschiedene Wege
sind, mit den Dateien zu interagieren, sind die Dateien und Verzeichnisse selbst
dieselben.

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::: callout

## Gute Namen für Dateien und Verzeichnisse

Komplizierte Namen von Dateien und Verzeichnissen können Ihnen das Leben schwer machen,
wenn Sie mit der Kommandozeile arbeiten. Hier geben wir Ihnen ein paar nützliche Tipps
für die Namen Ihrer Dateien und Verzeichnisse.

1. Keine Leerzeichen verwenden.

Leerzeichen können einen Namen aussagekräftiger machen, aber da Leerzeichen zur Trennung
von Argumenten in der Befehlszeile verwendet werden, ist es besser, sie in Namen von
Dateien und Verzeichnissen zu vermeiden. Sie können stattdessen `-` oder `_` verwenden
(z.B. `north-pacific-gyre/` anstelle von `north pacific gyre/`). Um dies zu testen,
versuchen Sie `mkdir north pacific gyre` einzugeben und sehen Sie, welches Verzeichnis
(oder Verzeichnisse!) erstellt wird, wenn Sie mit `ls -F` prüfen.

2. Beginnen Sie den Namen nicht mit `-` (Bindestrich).

Die Befehle behandeln Namen, die mit `-` beginnen, als Optionen.

3. Bleiben Sie bei Buchstaben, Zahlen, `.` (Punkt), `-` (Bindestrich) und `_`
   (Unterstrich).

Viele andere Zeichen haben in der Befehlszeile eine besondere Bedeutung. In dieser
Lektion werden wir einige davon kennenlernen. Es gibt Sonderzeichen, die dazu führen
können, dass Ihr Befehl nicht wie erwartet funktioniert und sogar zu Datenverlust führen
kann.

Wenn Sie auf Namen von Dateien oder Verzeichnissen verweisen müssen, die Leerzeichen
oder andere Sonderzeichen enthalten, sollten Sie den Namen in einfache
[Anführungszeichen](https://www.gnu.org/software/bash/manual/html_node/Quoting.html)
setzen (`''`).

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::: instructor

Lernende können sich manchmal in Befehlszeilen-Texteditoren wie Vim, Emacs oder Nano
verfangen. Das Schließen des Terminalemulators und das Öffnen eines neuen kann
frustrierend sein, da die Lernenden erneut zum richtigen Ordner navigieren müssen.
Unsere Empfehlung, um dieses Problem zu entschärfen, ist, dass die Lehrkräfte während
der Workshops denselben Texteditor wie die Lernenden verwenden sollten (in den meisten
Fällen Nano).

::::::::::::::::::::::::::::::::::::::::::::::::::

### Erstellen einer Textdatei

Ändern wir unser Arbeitsverzeichnis in `thesis` mit `cd`, dann starten wir einen
Texteditor namens Nano, um eine Datei namens `draft.txt` zu erstellen:

```bash
$ cd thesis
$ nano draft.txt
```

::::::::::::::::::::::::::::::::::::::::: callout

## Welcher Editor?

Wenn wir sagen, `nano` ist ein Texteditor, dann meinen wir auch wirklich 'Text'. Er kann
nur mit einfachen Zeichendaten arbeiten, nicht mit Tabellen, Bildern oder anderen
menschenfreundlichen Medien. Wir verwenden ihn in den Beispielen, weil er einer der am
wenigsten komplexen Texteditoren ist. Aufgrund dieser Eigenschaft ist er jedoch
möglicherweise nicht leistungsfähig oder flexibel genug für die Arbeit, die Sie nach
diesem Workshop erledigen müssen. Auf Unix-Systemen (wie Linux und macOS) verwenden
viele Programmierer [Emacs](https://www.gnu.org/software/emacs/) oder
[Vim](https://www.vim.org/) (die beide mehr Zeit zum Erlernen benötigen) oder einen
grafischen Editor wie [Gedit](https://projects.gnome.org/gedit/) oder
[VScode](https://code.visualstudio.com/). Unter Windows können Sie auch
[Notepad++](https://notepad-plus-plus.org/) verwenden. Windows hat auch einen
eingebauten Editor namens `notepad`, der von der Kommandozeile aus auf die gleiche Weise
wie `nano` für die Zwecke dieser Lektion ausgeführt werden kann.

Unabhängig davon, welchen Editor Sie verwenden, müssen Sie wissen, wo er Dateien sucht
und speichert. Wenn Sie ihn von der Shell aus starten, wird er (wahrscheinlich) Ihr
aktuelles Arbeitsverzeichnis als Standardspeicherort verwenden. Wenn Sie das Startmenü
Ihres Computers verwenden, speichert er die Dateien möglicherweise stattdessen in Ihrem
Desktop- oder Dokumentenverzeichnis. Sie können dies ändern, indem Sie beim ersten Mal,
wenn Sie "Speichern unter..." wählen, in ein anderes Verzeichnis wechseln

::::::::::::::::::::::::::::::::::::::::::::::::::

Geben wir ein paar Zeilen Text ein.

![](fig/nano-screenshot.png){alt="Screenshot des Nano-Texteditors in Aktion mit dem Text
It's not publish or perish any more, it's share and thrive"}

Wenn wir mit unserem Text zufrieden sind, können wir die Taste
<kbd>Strg</kbd>+<kbd>O</kbd> drücken (drücken Sie die Taste <kbd>Strg</kbd> oder
<kbd>Steuerung</kbd> und halten Sie sie gedrückt, während Sie die Taste <kbd>O</kbd>
drücken), um unsere Daten auf die Festplatte zu schreiben. Wir werden aufgefordert,
einen Namen für die Datei anzugeben, die unseren Text enthalten soll. Drücken Sie
<kbd>Return</kbd>, um die vorgeschlagene Vorgabe `draft.txt` zu übernehmen.

Sobald unsere Datei gespeichert ist, können wir <kbd>Strg</kbd>\+<kbd>X</kbd> benutzen,
um den Editor zu verlassen und zur Shell zurückzukehren.

::::::::::::::::::::::::::::::::::::::::: callout

## Steuerung, Strg oder ^-Taste

Die Steuerungstaste wird auch als "Strg"-Taste bezeichnet. Es gibt verschiedene
Möglichkeiten, die Verwendung der Steuerungstaste zu beschreiben. Zum Beispiel können
Sie eine Anweisung sehen, die <kbd>Steuertaste</kbd> zu drücken und, während Sie sie
gedrückt halten, die <kbd>X</kbd>-Taste zu drücken, beschrieben als eine der folgenden:

- `Control-X`
- `Control+X`
- `Ctrl-X`
- `Ctrl+X`
- `^X`
- `C-x`

In nano sehen Sie am unteren Rand des Bildschirms `^G Get Help ^O WriteOut`. Das
bedeutet, dass Sie `Control-G` benutzen können, um Hilfe zu bekommen und `Control-O`, um
Ihre Datei zu speichern.

::::::::::::::::::::::::::::::::::::::::::::::::::

`nano` hinterlässt nach dem Beenden keine Ausgabe auf dem Bildschirm, aber `ls` zeigt
nun, dass wir eine Datei namens `draft.txt` erstellt haben:

```bash
$ ls
```

```output
draft.txt
```

::::::::::::::::::::::::::::::::::::::: challenge

## Dateien auf eine andere Art erstellen

Wir haben gesehen, wie man Textdateien mit dem Editor `nano` erstellt. Versuchen Sie nun
den folgenden Befehl:

```bash
$ touch my_file.txt
```

1. Was hat der Befehl `touch` bewirkt? Wenn Sie Ihr aktuelles Verzeichnis mit dem
   GUI-Dateiexplorer betrachten, wird die Datei angezeigt?

2. Benutze `ls -l`, um die Dateien zu untersuchen. Wie groß ist `my_file.txt`?

3. Wann sollten Sie eine Datei auf diese Weise erstellen?

::::::::::::::: solution

## Lösung

1. Der Befehl `touch` erzeugt eine neue Datei namens `my_file.txt` in Ihrem aktuellen
   Verzeichnis. Sie können diese neu erzeugte Datei beobachten, indem Sie `ls` an der
   Eingabeaufforderung eingeben. die Datei `my_file.txt` kann auch in Ihrem
   GUI-Dateiexplorer angezeigt werden.

2. Wenn Sie die Datei mit `ls -l` untersuchen, stellen Sie fest, dass die Größe von
   `my_file.txt` 0 Bytes beträgt. Mit anderen Worten, sie enthält keine Daten. Wenn Sie
   `my_file.txt` mit Ihrem Texteditor öffnen, ist sie leer.

3. Einige Programme erzeugen nicht selbst Ausgabedateien, sondern setzen voraus, dass
   bereits leere Dateien erzeugt worden sind. Wenn das Programm ausgeführt wird, sucht
   es nach einer vorhandenen Datei, die es mit seiner Ausgabe füllen kann. Mit dem
   Befehl touch können Sie auf effiziente Weise eine leere Textdatei erzeugen, die von
   solchen Programmen verwendet werden kann.

:::::::::::::::::::::::::

Um spätere Verwirrung zu vermeiden, empfehlen wir, die soeben erstellte Datei zu
löschen, bevor Sie mit dem Rest der Episode fortfahren, da sonst die zukünftigen
Ausgaben von den in der Lektion angegebenen abweichen können. Verwenden Sie dazu den
folgenden Befehl:

```bash
$ rm my_file.txt
```

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::: callout

## What's In A Name?

Sie haben vielleicht bemerkt, dass alle Dateien von Nelle mit "irgendetwas dot
irgendetwas" benannt sind, und in diesem Teil der Lektion haben wir immer die
Erweiterung `.txt` verwendet. Dies ist nur eine Konvention; wir können eine Datei
`mythesis` oder fast alles andere nennen, was wir wollen. Die meisten Leute verwenden
jedoch meist zweiteilige Namen, um ihnen (und ihren Programmen) zu helfen, verschiedene
Arten von Dateien zu unterscheiden. Der zweite Teil eines solchen Namens wird
**Dateinamenserweiterung** genannt und gibt an, welche Art von Daten die Datei enthält:
`.txt` steht für eine einfache Textdatei, `.pdf` für ein PDF-Dokument, `.cfg` ist eine
Konfigurationsdatei mit Parametern für ein Programm oder ein anderes, `.png` ist ein
PNG-Bild, und so weiter.

Dies ist nur eine Konvention, wenn auch eine wichtige. Dateien enthalten lediglich
Bytes; es liegt an uns und unseren Programmen, diese Bytes gemäß den Regeln für einfache
Textdateien, PDF-Dokumente, Konfigurationsdateien, Bilder usw. zu interpretieren.

Die Benennung eines PNG-Bildes eines Wals als `whale.mp3` verwandelt es nicht irgendwie
auf magische Weise in eine Aufnahme eines Walgesangs, obwohl es *möglicherweise* das
Betriebssystem veranlasst, die Datei mit einem Musikabspielprogramm zu verknüpfen. Wenn
in diesem Fall jemand in einem Datei-Explorer-Programm auf `whale.mp3` doppelklickt,
wird der Musik-Player automatisch (und fälschlicherweise) versuchen, die Datei
`whale.mp3` zu öffnen.

::::::::::::::::::::::::::::::::::::::::::::::::::

## Verschieben von Dateien und Verzeichnissen

Rückkehr in das Verzeichnis `shell-lesson-data/exercise-data/writing`,

```bash
$ cd ~/Desktop/shell-lesson-data/exercise-data/writing
```

In unserem Verzeichnis `thesis` haben wir eine Datei `draft.txt`, was kein besonders
informativer Name ist, also ändern wir den Namen der Datei mit `mv`, was die Abkürzung
für 'move' ist:

```bash
$ mv thesis/draft.txt thesis/quotes.txt
```

Das erste Argument sagt `mv`, was wir "verschieben", während das zweite angibt, wohin es
gehen soll. In diesem Fall verschieben wir `thesis/draft.txt` nach `thesis/quotes.txt`,
was den gleichen Effekt hat wie das Umbenennen der Datei. Sicherlich zeigt uns `ls`,
dass `thesis` nun eine Datei namens `quotes.txt` enthält:

```bash
$ ls thesis
```

```output
quotes.txt
```

Bei der Angabe des Zieldateinamens muss man vorsichtig sein, denn `mv` überschreibt
stillschweigend jede vorhandene Datei mit demselben Namen, was zu Datenverlust führen
kann. Standardmäßig wird `mv` vor dem Überschreiben von Dateien nicht nach einer
Bestätigung fragen. Eine zusätzliche Option, `mv -i` (oder `mv --interactive`),
veranlasst `mv` jedoch, eine solche Bestätigung zu verlangen.

Beachten Sie, dass `mv` auch bei Verzeichnissen funktioniert.

Lassen Sie uns `quotes.txt` in das aktuelle Arbeitsverzeichnis verschieben. Wir
verwenden wieder `mv`, aber dieses Mal benutzen wir nur den Namen eines Verzeichnisses
als zweites Argument, um `mv` mitzuteilen, dass wir den Dateinamen behalten, aber die
Datei an einen neuen Ort verschieben wollen. (Deshalb heißt der Befehl 'move'.) In
diesem Fall ist der Verzeichnisname, den wir verwenden, der spezielle Verzeichnisname
`.`, den wir bereits erwähnt haben.

```bash
$ mv thesis/quotes.txt .
```

Dies hat zur Folge, dass die Datei aus dem Verzeichnis, in dem sie sich befand, in das
aktuelle Arbeitsverzeichnis verschoben wird. `ls` zeigt uns nun, dass `thesis` leer ist:

```bash
$ ls thesis
```

```output
$
```

Alternativ können wir bestätigen, dass die Datei `quotes.txt` nicht mehr im Verzeichnis
`thesis` vorhanden ist, indem wir explizit versuchen, sie aufzulisten:

```bash
$ ls thesis/quotes.txt
```

```error
ls: cannot access 'thesis/quotes.txt': No such file or directory
```

`ls` mit einem Dateinamen oder Verzeichnis als Argument listet nur die angeforderte
Datei oder das Verzeichnis auf. Wenn die als Argument angegebene Datei nicht existiert,
gibt die Shell einen Fehler zurück, wie wir oben gesehen haben. Wir können dies
benutzen, um zu sehen, dass `quotes.txt` jetzt in unserem aktuellen Verzeichnis
vorhanden ist:

```bash
$ ls quotes.txt
```

```output
quotes.txt
```

::::::::::::::::::::::::::::::::::::::: challenge

## Verschieben von Dateien in einen neuen Ordner

Nachdem sie die folgenden Befehle ausgeführt hat, stellt Jamie fest, dass sie die
Dateien `sucrose.dat` und `maltose.dat` in den falschen Ordner gelegt hat. Die Dateien
hätten in den Ordner `raw` gelegt werden müssen.

```bash
$ ls -F
 analyzed/ raw/
$ ls -F analyzed
fructose.dat glucose.dat maltose.dat sucrose.dat
$ cd analyzed
```

Füllen Sie die Felder aus, um diese Dateien in den Ordner `raw/` zu verschieben (d. h.
in den Ordner, in dem sie sie vergessen hat)

```bash
$ mv sucrose.dat maltose.dat ____/____
```

::::::::::::::: solution

## Lösung

```bash
$ mv sucrose.dat maltose.dat ../raw
```

Erinnern Sie sich, dass `..` sich auf das übergeordnete Verzeichnis (d.h. eines über dem
aktuellen Verzeichnis) und `.` auf das aktuelle Verzeichnis bezieht.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

## Kopieren von Dateien und Verzeichnissen

Der Befehl `cp` funktioniert ähnlich wie `mv`, nur dass er eine Datei kopiert, anstatt
sie zu verschieben. Wir können überprüfen, ob er das Richtige getan hat, indem wir `ls`
mit zwei Pfaden als Argumente benutzen --- wie die meisten Unix-Befehle kann `ls`
mehrere Pfade auf einmal angegeben werden:

```bash
$ cp quotes.txt thesis/quotations.txt
$ ls quotes.txt thesis/quotations.txt
```

```output
quotes.txt   thesis/quotations.txt
```

Wir können auch ein Verzeichnis und seinen gesamten Inhalt kopieren, indem wir die
Option [rekursiv](https://en.wikipedia.org/wiki/Recursion) `-r` verwenden, z.B. um ein
Verzeichnis zu sichern:

```bash
$ cp -r thesis thesis_backup
```

Wir können das Ergebnis überprüfen, indem wir den Inhalt der beiden Verzeichnisse
`thesis` und `thesis_backup` auflisten:

```bash
$ ls thesis thesis_backup
```

```output
thesis:
quotations.txt

thesis_backup:
quotations.txt
```

Es ist wichtig, die Option `-r` anzugeben. Wenn Sie ein Verzeichnis kopieren wollen und
diese Option weglassen, werden Sie eine Meldung sehen, dass das Verzeichnis weggelassen
wurde, weil `-r not specified`.

``` bash
$ cp thesis thesis_backup
cp: -r not specified; omitting directory 'thesis'
```


::::::::::::::::::::::::::::::::::::::: challenge

## Umbenennung von Dateien

Angenommen, Sie haben in Ihrem aktuellen Verzeichnis eine Klartextdatei erstellt, die
eine Liste der statistischen Tests enthält, die Sie zur Analyse Ihrer Daten benötigen,
und diese Datei `statstics.txt` genannt

Nachdem Sie diese Datei erstellt und gespeichert haben, stellen Sie fest, dass Sie den
Dateinamen falsch geschrieben haben! Sie möchten den Fehler korrigieren. Welchen der
folgenden Befehle können Sie dazu verwenden?

1. `cp statstics.txt statistics.txt`
2. `mv statstics.txt statistics.txt`
3. `mv statstics.txt .`
4. `cp statstics.txt .`

::::::::::::::: solution

## Lösung

1. Nein. Dies würde zwar eine Datei mit dem richtigen Namen erstellen, aber die falsch
   benannte Datei ist noch im Verzeichnis vorhanden und müsste gelöscht werden.
2. Ja, das würde funktionieren, um die Datei umzubenennen.
3. Nein, der Punkt(.) gibt an, wohin die Datei verschoben werden soll, liefert aber
   keinen neuen Dateinamen; identische Dateinamen können nicht erstellt werden.
4. Nein, der Punkt(.) gibt an, wohin die Datei kopiert werden soll, liefert aber keinen
   neuen Dateinamen; identische Dateinamen können nicht erstellt werden.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Verschieben und Kopieren

Wie lautet die Ausgabe des abschließenden Befehls `ls` in der unten dargestellten
Reihenfolge?

```bash
$ pwd
```

```output
/Users/jamie/data
```

```bash
$ ls
```

```output
proteins.dat
```

```bash
$ mkdir recombined
$ mv proteins.dat recombined/
$ cp recombined/proteins.dat ../proteins-saved.dat
$ ls
```

1. `proteins-saved.dat recombined`
2. `recombined`
3. `proteins.dat recombined`
4. `proteins-saved.dat`

::::::::::::::: solution

## Lösung

Wir beginnen im Verzeichnis `/Users/jamie/data` und erstellen einen neuen Ordner namens
`recombined`. Die zweite Zeile verschiebt (`mv`) die Datei `proteins.dat` in den neuen
Ordner (`recombined`). Die dritte Zeile erstellt eine Kopie der Datei, die wir gerade
verschoben haben. Der knifflige Teil hier ist, wohin die Datei kopiert wurde. Erinnern
Sie sich, dass `..` "eine Ebene höher gehen" bedeutet, also ist die kopierte Datei jetzt
in `/Users/jamie`. Beachten Sie, dass `..` in Bezug auf das aktuelle Arbeitsverzeichnis
interpretiert wird, **nicht** in Bezug auf den Ort der kopierten Datei. Das Einzige, was
mit ls (in `/Users/jamie/data`) angezeigt wird, ist also der neu zusammengestellte
Ordner.

1. Nein, siehe Erklärung oben.`proteins-saved.dat` befindet sich auf`/Users/jamie`
2. Ja
3. Nein, siehe Erklärung oben.`proteins.dat` befindet sich
   auf`/Users/jamie/data/recombined`
4. Nein, siehe Erklärung oben.`proteins-saved.dat` befindet sich auf`/Users/jamie`

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

## Entfernen von Dateien und Verzeichnissen

Kehren wir zum Verzeichnis `shell-lesson-data/exercise-data/writing` zurück und räumen
wir dieses Verzeichnis auf, indem wir die von uns erstellte Datei `quotes.txt`
entfernen. Der Unix-Befehl, den wir dafür verwenden, ist `rm` (kurz für 'remove'):

```bash
$ rm quotes.txt
```

Wir können bestätigen, dass die Datei mit `ls` verschwunden ist:

```bash
$ ls quotes.txt
```

```error
ls: cannot access 'quotes.txt': No such file or directory
```

::::::::::::::::::::::::::::::::::::::::: callout

## Gelöscht wird für immer

Die Unix-Shell verfügt nicht über einen Papierkorb, aus dem gelöschte Dateien
wiederhergestellt werden können (obwohl die meisten grafischen Oberflächen von Unix dies
tun). Wenn wir Dateien löschen, werden sie stattdessen aus dem Dateisystem entfernt,
damit ihr Speicherplatz auf der Festplatte wiederverwendet werden kann. Es gibt zwar
Werkzeuge zum Auffinden und Wiederherstellen gelöschter Dateien, aber es gibt keine
Garantie, dass sie in jeder Situation funktionieren, da der Computer den Speicherplatz
der Datei möglicherweise sofort wiederverwendet.

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Sichere Verwendung von `rm`

Was passiert, wenn wir `rm -i thesis_backup/quotations.txt` ausführen? Warum sollten wir
diesen Schutz brauchen, wenn wir `rm` verwenden?

::::::::::::::: solution

## Lösung

```output
rm: remove regular file 'thesis_backup/quotations.txt'? y
```

Die Option `-i` wird vor (jedem) Löschen nachfragen (verwenden Sie <kbd>Y</kbd>, um das
Löschen zu bestätigen oder <kbd>N</kbd>, um die Datei zu behalten). Die Unix-Shell hat
keinen Mülleimer, so dass alle gelöschten Dateien für immer verschwinden werden. Mit der
Option `-i` können wir überprüfen, dass wir nur die Dateien löschen, die wir auch
wirklich löschen wollen.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

Wenn wir versuchen, das Verzeichnis `thesis` mit `rm thesis` zu entfernen, erhalten wir
eine Fehlermeldung:

```bash
$ rm thesis
```

```error
rm: cannot remove 'thesis': Is a directory
```

Das passiert, weil `rm` standardmäßig nur auf Dateien und nicht auf Verzeichnisse wirkt.

`rm` kann ein Verzeichnis *mitsamt seinem Inhalt* löschen, wenn wir die rekursive Option
`-r` verwenden, und zwar *ohne jegliche Bestätigungsaufforderung*:

```bash
$ rm -r thesis
```

Da es keine Möglichkeit gibt, mit der Shell gelöschte Dateien wiederherzustellen, sollte
`rm -r` *mit großer Vorsicht* verwendet werden (Sie könnten die interaktive Option `rm
-r -i` hinzufügen).

## Operationen mit mehreren Dateien und Verzeichnissen

Oft muss man mehrere Dateien auf einmal kopieren oder verschieben. Dies kann durch die
Angabe einer Liste von einzelnen Dateinamen oder durch die Angabe eines Namensmusters
unter Verwendung von Platzhaltern geschehen. Wildcards sind Sonderzeichen, die verwendet
werden können, um unbekannte Zeichen oder Zeichensätze bei der Navigation im
Unix-Dateisystem darzustellen.

::::::::::::::::::::::::::::::::::::::: challenge

## Kopieren mit mehreren Dateinamen

Für diese Übung können Sie die Befehle im Verzeichnis `shell-lesson-data/exercise-data`
testen.

Was macht `cp` im folgenden Beispiel, wenn man mehrere Dateinamen und einen
Verzeichnisnamen angibt?

```bash
$ mkdir backup
$ cp creatures/minotaur.dat creatures/unicorn.dat backup/
```

Was macht `cp` in dem folgenden Beispiel, wenn drei oder mehr Dateinamen angegeben
werden?

```bash
$ cd creatures
$ ls -F
```

```output
basilisk.dat  minotaur.dat  unicorn.dat
```

```bash
$ cp minotaur.dat unicorn.dat basilisk.dat
```

::::::::::::::: solution

## Lösung

Wenn mehr als ein Dateiname gefolgt von einem Verzeichnisnamen angegeben wird (d.h. das
Zielverzeichnis muss das letzte Argument sein), kopiert `cp` die Dateien in das genannte
Verzeichnis.

Wenn drei Dateinamen angegeben werden, gibt `cp` einen Fehler wie den folgenden aus,
weil es einen Verzeichnisnamen als letztes Argument erwartet.

```error
cp: target 'basilisk.dat' is not a directory
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

### Verwendung von Wildcards für den gleichzeitigen Zugriff auf mehrere Dateien

::::::::::::::::::::::::::::::::::::::::: callout

## Platzhalter

`*` ist eine **Wildcard**, die für null oder mehr andere Zeichen steht. Betrachten wir
das Verzeichnis `shell-lesson-data/exercise-data/alkanes`: `*.pdb` steht für
`ethane.pdb`, `propane.pdb` und jede Datei, die mit ".pdb" endet. Auf der anderen Seite
repräsentiert `p*.pdb` nur `pentane.pdb` und `propane.pdb`, weil das 'p' am Anfang nur
Dateinamen repräsentieren kann, die mit dem Buchstaben 'p' beginnen.

`?` ist auch ein Platzhalter, aber er steht für genau ein Zeichen. So könnte
`?ethane.pdb` für `methane.pdb` stehen, während `*ethane.pdb` sowohl für `ethane.pdb`
als auch für `methane.pdb` steht.

Wildcards können in Kombination miteinander verwendet werden. Zum Beispiel bedeutet
`???ane.pdb` drei Zeichen, gefolgt von `ane.pdb`, was `cubane.pdb ethane.pdb octane.pdb`
ergibt.

Wenn die Shell einen Platzhalter sieht, expandiert sie diesen, um eine Liste passender
Dateinamen zu erstellen, *bevor* sie den vorangehenden Befehl ausführt. Wenn ein
Platzhalterausdruck ausnahmsweise auf keine Datei passt, übergibt die Bash den Ausdruck
als Argument an den Befehl, wie er ist. Wenn Sie beispielsweise `ls *.pdf` in das
Verzeichnis `alkanes` eingeben (das nur Dateien enthält, deren Namen auf `.pdb` enden),
erhalten Sie die Fehlermeldung, dass es keine Datei namens `*.pdf` gibt. Im Allgemeinen
sehen Befehle wie `wc` und `ls` jedoch die Listen der Dateinamen, die diesen Ausdrücken
entsprechen, aber nicht die Platzhalter selbst. Es ist die Shell, nicht die anderen
Programme, die die Wildcards expandiert.

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Liste der Dateinamen, die einem Muster entsprechen

Welche(r) `ls`-Befehl(e) erzeugt/erzeugen diese Ausgabe, wenn er/sie im Verzeichnis
`alkanes` ausgeführt wird/werden?

`ethane.pdb methane.pdb`

1. `ls *t*ane.pdb`
2. `ls *t?ne.*`
3. `ls *t??ne.pdb`
4. `ls ethane.*`

::::::::::::::: solution

## Lösung

Die Lösung ist `3.`

`1.` zeigt alle Dateien, deren Namen null oder mehr Zeichen enthalten (`*`), gefolgt von
dem Buchstaben `t`, dann null oder mehr Zeichen (`*`), gefolgt von `ane.pdb`. Dies
ergibt `ethane.pdb methane.pdb octane.pdb pentane.pdb`.

`2.` zeigt alle Dateien, deren Namen mit null oder mehr Zeichen beginnen (`*`), gefolgt
von dem Buchstaben `t`, dann ein einzelnes Zeichen (`?`), dann `ne.` gefolgt von null
oder mehr Zeichen (`*`). Dies ergibt `octane.pdb` und `pentane.pdb`, aber keine
Übereinstimmung mit etwas, das auf `thane.pdb` endet.

`3.` behebt die Probleme von Option 2, indem zwei Zeichen (`??`) zwischen `t` und `ne`
übereinstimmen. Dies ist die Lösung.

`4.` zeigt nur Dateien, die mit `ethane.` beginnen.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Mehr zu Wildcards

Sam hat ein Verzeichnis mit Kalibrierungsdaten, Datensätzen und Beschreibungen der
Datensätze:

```bash
.
├── 2015-10-23-calibration.txt
├── 2015-10-23-dataset1.txt
├── 2015-10-23-dataset2.txt
├── 2015-10-23-dataset_overview.txt
├── 2015-10-26-calibration.txt
├── 2015-10-26-dataset1.txt
├── 2015-10-26-dataset2.txt
├── 2015-10-26-dataset_overview.txt
├── 2015-11-23-calibration.txt
├── 2015-11-23-dataset1.txt
├── 2015-11-23-dataset2.txt
├── 2015-11-23-dataset_overview.txt
├── backup
│   ├── calibration
│   └── datasets
└── send_to_bob
    ├── all_datasets_created_on_a_23rd
    └── all_november_files
```

Bevor sie zu einer weiteren Exkursion aufbricht, möchte sie ihre Daten sichern und
einige Datensätze an ihren Kollegen Bob senden. Sam verwendet die folgenden Befehle, um
diese Aufgabe zu erledigen:

```bash
$ cp *dataset* backup/datasets
$ cp ____calibration____ backup/calibration
$ cp 2015-____-____ send_to_bob/all_november_files/
$ cp ____ send_to_bob/all_datasets_created_on_a_23rd/
```

Hilf Sam, indem du die Lücken ausfüllst.

Die resultierende Verzeichnisstruktur sollte wie folgt aussehen

```bash
.
├── 2015-10-23-calibration.txt
├── 2015-10-23-dataset1.txt
├── 2015-10-23-dataset2.txt
├── 2015-10-23-dataset_overview.txt
├── 2015-10-26-calibration.txt
├── 2015-10-26-dataset1.txt
├── 2015-10-26-dataset2.txt
├── 2015-10-26-dataset_overview.txt
├── 2015-11-23-calibration.txt
├── 2015-11-23-dataset1.txt
├── 2015-11-23-dataset2.txt
├── 2015-11-23-dataset_overview.txt
├── backup
│   ├── calibration
│   │   ├── 2015-10-23-calibration.txt
│   │   ├── 2015-10-26-calibration.txt
│   │   └── 2015-11-23-calibration.txt
│   └── datasets
│       ├── 2015-10-23-dataset1.txt
│       ├── 2015-10-23-dataset2.txt
│       ├── 2015-10-23-dataset_overview.txt
│       ├── 2015-10-26-dataset1.txt
│       ├── 2015-10-26-dataset2.txt
│       ├── 2015-10-26-dataset_overview.txt
│       ├── 2015-11-23-dataset1.txt
│       ├── 2015-11-23-dataset2.txt
│       └── 2015-11-23-dataset_overview.txt
└── send_to_bob
    ├── all_datasets_created_on_a_23rd
    │   ├── 2015-10-23-dataset1.txt
    │   ├── 2015-10-23-dataset2.txt
    │   ├── 2015-10-23-dataset_overview.txt
    │   ├── 2015-11-23-dataset1.txt
    │   ├── 2015-11-23-dataset2.txt
    │   └── 2015-11-23-dataset_overview.txt
    └── all_november_files
        ├── 2015-11-23-calibration.txt
        ├── 2015-11-23-dataset1.txt
        ├── 2015-11-23-dataset2.txt
        └── 2015-11-23-dataset_overview.txt
```

::::::::::::::: solution

## Lösung

```bash
$ cp *calibration.txt backup/calibration
$ cp 2015-11-* send_to_bob/all_november_files/
$ cp *-23-dataset* send_to_bob/all_datasets_created_on_a_23rd/
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Organisieren von Verzeichnissen und Dateien

Jamie arbeitet an einem Projekt und stellt fest, dass ihre Dateien nicht sehr gut
organisiert sind:

```bash
$ ls -F
```

```output
analyzed/  fructose.dat    raw/   sucrose.dat
```

Die Dateien `fructose.dat` und `sucrose.dat` enthalten die Ausgabe ihrer Datenanalyse.
Welche(r) in dieser Lektion behandelte(n) Befehl(e) muss sie ausführen, damit die
folgenden Befehle die gezeigte Ausgabe erzeugen?

```bash
$ ls -F
```

```output
analyzed/   raw/
```

```bash
$ ls analyzed
```

```output
fructose.dat    sucrose.dat
```

::::::::::::::: solution

## Lösung

```bash
mv *.dat analyzed
```

Jamie muss ihre Dateien `fructose.dat` und `sucrose.dat` in das Verzeichnis `analyzed`
verschieben. Die Shell expandiert \*.dat, um alle .dat-Dateien im aktuellen Verzeichnis
zu finden. Der Befehl `mv` verschiebt dann die Liste der .dat-Dateien in das Verzeichnis
"analyzed".

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Reproduzieren Sie eine Ordnerstruktur

Sie beginnen ein neues Experiment und möchten die Verzeichnisstruktur Ihres vorherigen
Experiments duplizieren, damit Sie neue Daten hinzufügen können.

Angenommen, das vorherige Experiment befindet sich in einem Ordner namens `2016-05-18`,
der einen Ordner `data` enthält, der wiederum Ordner namens `raw` und `processed`
enthält, die Datendateien enthalten. Das Ziel ist es, die Ordnerstruktur des Ordners
`2016-05-18` in einen Ordner namens `2016-05-20` zu kopieren, so dass die endgültige
Verzeichnisstruktur wie folgt aussieht:

```output
2016-05-20/
└── data
   ├── processed
   └── raw
```

Welcher der folgenden Befehle würde dieses Ziel erreichen? Was würden die anderen
Befehle bewirken?

```bash
$ mkdir 2016-05-20
$ mkdir 2016-05-20/data
$ mkdir 2016-05-20/data/processed
$ mkdir 2016-05-20/data/raw
```

```bash
$ mkdir 2016-05-20
$ cd 2016-05-20
$ mkdir data
$ cd data
$ mkdir raw processed
```

```bash
$ mkdir 2016-05-20/data/raw
$ mkdir 2016-05-20/data/processed
```

```bash
$ mkdir -p 2016-05-20/data/raw
$ mkdir -p 2016-05-20/data/processed
```

```bash
$ mkdir 2016-05-20
$ cd 2016-05-20
$ mkdir data
$ mkdir raw processed
```

::::::::::::::: solution

## Lösung

Mit den ersten beiden Befehlssätzen wird dieses Ziel erreicht. Der erste Satz verwendet
relative Pfade, um das oberste Verzeichnis vor den Unterverzeichnissen zu erstellen.

Der dritte Satz von Befehlen führt zu einem Fehler, weil das Standardverhalten von
`mkdir` kein Unterverzeichnis eines nicht existierenden Verzeichnisses erstellt: die
Zwischenebenen-Ordner müssen zuerst erstellt werden.

Der vierte Satz von Befehlen erreicht dieses Ziel. Denken Sie daran, dass die Option
`-p`, gefolgt von einem Pfad zu einem oder mehreren Verzeichnissen, `mkdir` veranlasst,
alle dazwischen liegenden Unterverzeichnisse zu erstellen, falls erforderlich.

Der letzte Befehlssatz erzeugt die Verzeichnisse "raw" und "processed" auf der gleichen
Ebene wie das Verzeichnis "data".

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: keypoints

- `cp [old] [new]` kopiert eine Datei.
- `mkdir [path]` erstellt ein neues Verzeichnis.
- `mv [old] [new]` verschiebt (benennt) eine Datei oder ein Verzeichnis um.
- `rm [path]` entfernt (löscht) eine Datei.
- `*` passt auf null oder mehr Zeichen in einem Dateinamen, also passt `*.txt` auf alle
  Dateien, die auf `.txt` enden.
- `?` passt auf jedes einzelne Zeichen in einem Dateinamen, also passt `?.txt` auf
  `a.txt` aber nicht auf `any.txt`.
- Die Verwendung der Steuerungstaste kann auf viele Arten beschrieben werden,
  einschließlich `Ctrl-X`, `Control-X` und `^X`.
- Die Shell hat keinen Mülleimer: Wenn etwas gelöscht ist, ist es wirklich weg.
- Die meisten Dateinamen lauten `something.extension`. Die Erweiterung ist nicht
  erforderlich und garantiert nichts, wird aber normalerweise verwendet, um die Art der
  Daten in der Datei anzugeben.
- Abhängig von der Art Ihrer Arbeit benötigen Sie möglicherweise einen
  leistungsfähigeren Texteditor als Nano.

::::::::::::::::::::::::::::::::::::::::::::::::::

