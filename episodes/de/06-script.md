---
title: Shell-Skripte
teaching: 30
exercises: 15
---


::::::::::::::::::::::::::::::::::::::: objectives

- Schreiben Sie ein Shell-Skript, das einen Befehl oder eine Reihe von Befehlen für
  einen festen Satz von Dateien ausführt.
- Führen Sie ein Shell-Skript von der Kommandozeile aus.
- Schreiben Sie ein Shell-Skript, das mit einer Reihe von Dateien arbeitet, die der
  Benutzer auf der Kommandozeile definiert.
- Erstellen Sie Pipelines, die Shell-Skripte enthalten, die Sie und andere geschrieben
  haben.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- Wie kann ich Befehle speichern und wiederverwenden?

::::::::::::::::::::::::::::::::::::::::::::::::::

Endlich sind wir bereit zu sehen, was die Shell zu einer so mächtigen
Programmierumgebung macht. Wir werden die Befehle, die wir häufig wiederholen, in
Dateien speichern, so dass wir alle diese Operationen später mit einem einzigen Befehl
erneut ausführen können. Aus historischen Gründen wird ein Bündel von Befehlen, die in
einer Datei gespeichert sind, gewöhnlich als **Shell-Skript** bezeichnet, aber täuschen
Sie sich nicht --- es sind eigentlich kleine Programme.

Durch das Schreiben von Shell-Skripten wird Ihre Arbeit nicht nur schneller, sondern Sie
müssen auch nicht die gleichen Befehle immer wieder neu eingeben. Außerdem wird sie
dadurch genauer (weniger Tippfehler) und reproduzierbarer. Wenn Sie später auf Ihre
Arbeit zurückkommen (oder wenn jemand anderes Ihre Arbeit findet und darauf aufbauen
möchte), können Sie die gleichen Ergebnisse reproduzieren, indem Sie einfach Ihr Skript
ausführen, anstatt sich eine lange Liste von Befehlen zu merken oder neu einzugeben.

Beginnen wir damit, zu `alkanes/` zurückzugehen und eine neue Datei zu erstellen,
`middle.sh`, die unser Shell-Skript werden wird:

```bash
$ cd alkanes
$ nano middle.sh
```

Der Befehl `nano middle.sh` öffnet die Datei `middle.sh` mit dem Texteditor 'nano' (der
in der Shell läuft). Wenn die Datei nicht existiert, wird sie erstellt. Wir können den
Texteditor verwenden, um die Datei direkt zu bearbeiten, indem wir die folgende Zeile
einfügen:

```source
head -n 15 octane.pdb | tail -n 5
```

Dies ist eine Abwandlung der Pipe, die wir zuvor konstruiert haben und die die Zeilen
11-15 der Datei `octane.pdb` auswählt. Denken Sie daran, dass wir sie *noch* nicht als
Befehl ausführen; wir binden die Befehle nur in eine Datei ein.

Dann speichern wir die Datei (`Ctrl-O` in nano) und beenden den Texteditor (`Ctrl-X` in
nano). Überprüfen Sie, ob das Verzeichnis `alkanes` nun eine Datei namens `middle.sh`
enthält.

Sobald wir die Datei gespeichert haben, können wir die Shell bitten, die darin
enthaltenen Befehle auszuführen. Unsere Shell heißt `bash`, also führen wir den
folgenden Befehl aus:

```bash
$ bash middle.sh
```

```output
ATOM      9  H           1      -4.502   0.681   0.785  1.00  0.00
ATOM     10  H           1      -5.254  -0.243  -0.537  1.00  0.00
ATOM     11  H           1      -4.357   1.252  -0.895  1.00  0.00
ATOM     12  H           1      -3.009  -0.741  -1.467  1.00  0.00
ATOM     13  H           1      -3.172  -1.337   0.206  1.00  0.00
```

Die Ausgabe unseres Skripts entspricht genau dem, was wir erhalten würden, wenn wir die
Pipeline direkt ausführen würden.

::::::::::::::::::::::::::::::::::::::::: callout

## Text vs. Was auch immer

Normalerweise nennen wir Programme wie Microsoft Word oder LibreOffice Writer
"Texteditoren", aber wir müssen etwas vorsichtiger sein, wenn es um die Programmierung
geht. Microsoft Word verwendet standardmäßig `.docx`-Dateien, um nicht nur Text, sondern
auch Formatierungsinformationen über Schriftarten, Überschriften und so weiter zu
speichern. Diese zusätzlichen Informationen werden nicht als Zeichen gespeichert und
bedeuten nichts für Tools wie `head`, das erwartet, dass Eingabedateien nur die
Buchstaben, Ziffern und Satzzeichen einer normalen Computertastatur enthalten. Wenn Sie
Programme bearbeiten, müssen Sie daher entweder einen reinen Texteditor verwenden oder
darauf achten, dass Sie Dateien als reinen Text speichern.


::::::::::::::::::::::::::::::::::::::::::::::::::

Was, wenn wir Zeilen aus einer beliebigen Datei auswählen wollen? Wir könnten jedes Mal
`middle.sh` editieren, um den Dateinamen zu ändern, aber das würde wahrscheinlich länger
dauern, als den Befehl noch einmal in der Shell einzugeben und ihn mit einem neuen
Dateinamen auszuführen. Lassen Sie uns stattdessen `middle.sh` editieren und es
vielseitiger machen:

```bash
$ nano middle.sh
```

Ersetzen Sie nun in "nano" den Text `octane.pdb` durch die spezielle Variable namens
`$1`:

```source
head -n 15 "$1" | tail -n 5
```

Innerhalb eines Shell-Skripts bedeutet `$1` "der erste Dateiname (oder ein anderes
Argument) in der Befehlszeile". Wir können unser Skript nun wie folgt ausführen:

```bash
$ bash middle.sh octane.pdb
```

```output
ATOM      9  H           1      -4.502   0.681   0.785  1.00  0.00
ATOM     10  H           1      -5.254  -0.243  -0.537  1.00  0.00
ATOM     11  H           1      -4.357   1.252  -0.895  1.00  0.00
ATOM     12  H           1      -3.009  -0.741  -1.467  1.00  0.00
ATOM     13  H           1      -3.172  -1.337   0.206  1.00  0.00
```

oder auf eine andere Datei wie diese:

```bash
$ bash middle.sh pentane.pdb
```

```output
ATOM      9  H           1       1.324   0.350  -1.332  1.00  0.00
ATOM     10  H           1       1.271   1.378   0.122  1.00  0.00
ATOM     11  H           1      -0.074  -0.384   1.288  1.00  0.00
ATOM     12  H           1      -0.048  -1.362  -0.205  1.00  0.00
ATOM     13  H           1      -1.183   0.500  -1.412  1.00  0.00
```

::::::::::::::::::::::::::::::::::::::::: callout

## Doppelte Anführungszeichen um Argumente

Aus demselben Grund, aus dem wir die Schleifenvariable in doppelte Anführungszeichen
setzen, umgeben wir `$1` mit doppelten Anführungszeichen, falls der Dateiname zufällig
Leerzeichen enthält.


::::::::::::::::::::::::::::::::::::::::::::::::::

Zurzeit müssen wir jedes Mal `middle.sh` bearbeiten, wenn wir den Bereich der
zurückgegebenen Zeilen anpassen wollen. Wir können das ändern, indem wir unser Skript so
konfigurieren, dass es stattdessen drei Befehlszeilenargumente verwendet. Nach dem
ersten Kommandozeilenargument (`$1`) ist jedes weitere Argument, das wir angeben, über
die speziellen Variablen `$1`, `$2`, `$3` zugänglich, die sich jeweils auf das erste,
zweite und dritte Kommandozeilenargument beziehen.

Da wir dies wissen, können wir zusätzliche Argumente verwenden, um den Bereich der
Zeilen zu definieren, die an `head` bzw. `tail` übergeben werden sollen:

```bash
$ nano middle.sh
```

```source
head -n "$2" "$1" | tail -n "$3"
```

Wir können jetzt laufen:

```bash
$ bash middle.sh pentane.pdb 15 5
```

```output
ATOM      9  H           1       1.324   0.350  -1.332  1.00  0.00
ATOM     10  H           1       1.271   1.378   0.122  1.00  0.00
ATOM     11  H           1      -0.074  -0.384   1.288  1.00  0.00
ATOM     12  H           1      -0.048  -1.362  -0.205  1.00  0.00
ATOM     13  H           1      -1.183   0.500  -1.412  1.00  0.00
```

Indem wir die Argumente für unseren Befehl ändern, können wir das Verhalten unseres
Skripts ändern:

```bash
$ bash middle.sh pentane.pdb 20 5
```

```output
ATOM     14  H           1      -1.259   1.420   0.112  1.00  0.00
ATOM     15  H           1      -2.608  -0.407   1.130  1.00  0.00
ATOM     16  H           1      -2.540  -1.303  -0.404  1.00  0.00
ATOM     17  H           1      -3.393   0.254  -0.321  1.00  0.00
TER      18              1
```

Das funktioniert, aber es kann sein, dass die nächste Person, die `middle.sh` liest,
einen Moment braucht, um herauszufinden, was sie tut. Wir können unser Skript
verbessern, indem wir einige **Kommentare** am Anfang hinzufügen:

```bash
$ nano middle.sh
```

```source
# Select lines from the middle of a file.
# Usage: bash middle.sh filename end_line num_lines
head -n "$2" "$1" | tail -n "$3"
```

Ein Kommentar beginnt mit einem `#`-Zeichen und läuft bis zum Ende der Zeile. Der
Computer ignoriert Kommentare, aber sie sind von unschätzbarem Wert, wenn es darum geht,
anderen (auch Ihrem zukünftigen Ich) zu helfen, Skripte zu verstehen und zu benutzen.
Die einzige Einschränkung ist, dass Sie jedes Mal, wenn Sie das Skript ändern,
überprüfen sollten, ob der Kommentar noch korrekt ist. Eine Erklärung, die den Leser in
die falsche Richtung lenkt, ist schlimmer als gar keine.

Was ist, wenn wir viele Dateien in einer einzigen Pipeline verarbeiten wollen? Wenn wir
zum Beispiel unsere `.pdb` Dateien nach Länge sortieren wollen, würden wir eingeben:

```bash
$ wc -l *.pdb | sort -n
```

weil `wc -l` die Anzahl der Zeilen in den Dateien auflistet (erinnern Sie sich, dass
`wc` für 'word count' steht, das Hinzufügen der Option `-l` bedeutet stattdessen 'count
lines') und `sort -n` die Dinge numerisch sortiert. Wir könnten dies in eine Datei
schreiben, aber dann würde es immer nur eine Liste von `.pdb` Dateien im aktuellen
Verzeichnis sortieren. Wenn wir in der Lage sein wollen, eine sortierte Liste anderer
Arten von Dateien zu erhalten, brauchen wir einen Weg, um all diese Namen in das Skript
zu bekommen. Wir können nicht `$1`, `$2` und so weiter verwenden, weil wir nicht wissen,
wie viele Dateien es gibt. Stattdessen verwenden wir die spezielle Variable `$@`, was
soviel bedeutet wie 'Alle Befehlszeilenargumente für das Shell-Skript'. Wir sollten auch
`$@` in Anführungszeichen setzen, um den Fall von Argumenten mit Leerzeichen zu
behandeln (`"$@"` ist eine spezielle Syntax und entspricht `"$1"` `"$2"` ...).

Hier ist ein Beispiel:

```bash
$ nano sorted.sh
```

```source
# Sort files by their length.
# Usage: bash sorted.sh one_or_more_filenames
wc -l "$@" | sort -n
```

```bash
$ bash sorted.sh *.pdb ../creatures/*.dat
```

```output
9 methane.pdb
12 ethane.pdb
15 propane.pdb
20 cubane.pdb
21 pentane.pdb
30 octane.pdb
163 ../creatures/basilisk.dat
163 ../creatures/minotaur.dat
163 ../creatures/unicorn.dat
596 total
```

::::::::::::::::::::::::::::::::::::::: challenge

## Liste eindeutiger Arten

Leah hat mehrere hundert Datendateien, von denen jede wie folgt formatiert ist:

```source
2013-11-05,deer,5
2013-11-05,rabbit,22
2013-11-05,raccoon,7
2013-11-06,rabbit,19
2013-11-06,deer,2
2013-11-06,fox,1
2013-11-07,rabbit,18
2013-11-07,bear,1
```

Ein Beispiel für diesen Dateityp findet sich in
`shell-lesson-data/exercise-data/animal-counts/animals.csv`.

Wir können den Befehl `cut -d , -f 2 animals.csv | sort | uniq` verwenden, um die
einzelnen Arten in `animals.csv` zu erzeugen. Um diese Befehlsfolge nicht jedes Mal
abtippen zu müssen, kann ein Wissenschaftler stattdessen auch ein Shell-Skript
schreiben.

Schreiben Sie ein Shell-Skript mit dem Namen `species.sh`, das eine beliebige Anzahl von
Dateinamen als Befehlszeilenargumente annimmt und eine Variation des obigen Befehls
verwendet, um eine Liste der einzelnen Arten, die in jeder dieser Dateien vorkommen,
separat auszugeben.

::::::::::::::: solution

## Lösung

```bash
# Script to find unique species in csv files where species is the second data field
# This script accepts any number of file names as command line arguments

# Loop over all files
for file in $@
do
    echo "Unique species in $file:"
    # Extract species names
    cut -d , -f 2 $file | sort | uniq
done
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

Angenommen, wir haben gerade eine Reihe von Befehlen ausgeführt, die etwas Nützliches
bewirkt haben - zum Beispiel die Erstellung eines Diagramms, das wir in einer Arbeit
verwenden möchten. Wir möchten das Diagramm später bei Bedarf erneut erstellen können,
also wollen wir die Befehle in einer Datei speichern. Anstatt die Befehle erneut
einzugeben (und sie möglicherweise falsch zu machen), können wir so vorgehen:

```bash
$ history | tail -n 5 > redo-figure-3.sh
```

Die Datei `redo-figure-3.sh` enthält jetzt:

```source
297 bash goostats.sh NENE01729B.txt stats-NENE01729B.txt
298 bash goodiff.sh stats-NENE01729B.txt /data/validated/01729.txt > 01729-differences.txt
299 cut -d ',' -f 2-3 01729-differences.txt > 01729-time-series.txt
300 ygraph --format scatter --color bw --borders none 01729-time-series.txt figure-3.png
301 history | tail -n 5 > redo-figure-3.sh
```

Nach einer kurzen Bearbeitung in einem Editor, um die fortlaufenden Nummern der Befehle
zu entfernen und die letzte Zeile, in der wir den Befehl `history` aufgerufen haben,
haben wir eine absolut genaue Aufzeichnung darüber, wie wir diese Figur erstellt haben.

::::::::::::::::::::::::::::::::::::::: challenge

## Warum Befehle in der Historie aufzeichnen, bevor sie ausgeführt werden?

Wenn Sie den Befehl ausführen:

```bash
$ history | tail -n 5 > recent.sh
```

Der letzte Befehl in der Datei ist der Befehl `history` selbst, d.h. die Shell hat
`history` zum Befehlsprotokoll hinzugefügt, bevor sie ihn tatsächlich ausführt.
Tatsächlich fügt die Shell *immer* Befehle in das Protokoll ein, bevor sie ausgeführt
werden. Warum, glauben Sie, tut sie das?

::::::::::::::: solution

## Lösung

Wenn ein Befehl einen Absturz oder ein Hängen verursacht, könnte es nützlich sein, zu
wissen, was dieser Befehl war, um das Problem zu untersuchen. Würde der Befehl erst nach
seiner Ausführung aufgezeichnet werden, hätten wir im Falle eines Absturzes keine
Aufzeichnung des zuletzt ausgeführten Befehls.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

In der Praxis entwickeln die meisten Leute Shell-Skripte, indem sie Befehle an der
Shell-Eingabeaufforderung ein paar Mal ausführen, um sicherzustellen, dass sie das
Richtige tun, und sie dann zur Wiederverwendung in einer Datei speichern. Diese
Arbeitsweise ermöglicht es den Leuten, das, was sie über ihre Daten und ihren
Arbeitsablauf herausgefunden haben, mit einem Aufruf von `history` und ein wenig
Bearbeitung zu recyceln, um die Ausgabe zu bereinigen und als Shell-Skript zu speichern.

## Nelle's Pipeline: Erstellen eines Skripts

Nelles Vorgesetzter bestand darauf, dass alle ihre Analysen reproduzierbar sein müssen.
Der einfachste Weg, alle Schritte festzuhalten, ist ein Skript.

Zuerst kehren wir in das Projektverzeichnis von Nelle zurück:

```bash
$ cd ../../north-pacific-gyre/
```

Sie erstellt eine Datei mit `nano` ...

```bash
$ nano do-stats.sh
```

...die das Folgende enthält:

```bash
# Calculate stats for data files.
for datafile in "$@"
do
    echo $datafile
    bash goostats.sh $datafile stats-$datafile
done
```

Sie speichert dies in einer Datei namens `do-stats.sh`, so dass sie nun die erste Stufe
ihrer Analyse wiederholen kann, indem sie eingibt:

```bash
$ bash do-stats.sh NENE*A.txt NENE*B.txt
```

Sie kann auch dies tun:

```bash
$ bash do-stats.sh NENE*A.txt NENE*B.txt | wc -l
```

enthält, so dass die Ausgabe nur die Anzahl der verarbeiteten Dateien ist und nicht die
Namen der verarbeiteten Dateien.

Eine Sache, die man bei Nelles Skript beachten sollte, ist, dass es die Person, die es
ausführt, entscheiden lässt, welche Dateien verarbeitet werden sollen. Sie hätte es auch
so schreiben können:

```bash
# Calculate stats for Site A and Site B data files.
for datafile in NENE*A.txt NENE*B.txt
do
    echo $datafile
    bash goostats.sh $datafile stats-$datafile
done
```

Der Vorteil ist, dass dabei immer die richtigen Dateien ausgewählt werden: Sie muss
nicht daran denken, die "Z"-Dateien auszuschließen. Der Nachteil ist, dass es *immer*
nur diese Dateien auswählt --- sie kann es nicht auf alle Dateien (einschließlich der
"Z"-Dateien) oder auf die "G"- oder "H"-Dateien anwenden, die ihre Kollegen in der
Antarktis produzieren, ohne das Skript zu bearbeiten. Wenn sie etwas abenteuerlicher
sein wollte, könnte sie ihr Skript so ändern, dass es nach Befehlszeilenargumenten sucht
und `NENE*A.txt NENE*B.txt` verwendet, wenn keine angegeben wurden. Natürlich führt dies
zu einem weiteren Kompromiss zwischen Flexibilität und Komplexität.

::::::::::::::::::::::::::::::::::::::: challenge

## Variablen in Shell-Skripten

Stellen Sie sich vor, Sie haben im Verzeichnis `alkanes` ein Shell-Skript namens
`script.sh`, das die folgenden Befehle enthält:

```bash
head -n $2 $1
tail -n $3 $1
```

Während Sie sich im Verzeichnis `alkanes` befinden, geben Sie den folgenden Befehl ein:

```bash
$ bash script.sh '*.pdb' 1 1
```

Welche der folgenden Ausgaben würden Sie erwarten?

1. Alle Zeilen zwischen der ersten und der letzten Zeile jeder Datei, die auf `.pdb` im
   Verzeichnis `alkanes` endet
2. Die erste und die letzte Zeile jeder Datei, die auf `.pdb` im Verzeichnis `alkanes`
   endet
3. Die erste und die letzte Zeile jeder Datei im Verzeichnis `alkanes`
4. Ein Fehler wegen der Anführungszeichen um `*.pdb`

::::::::::::::: solution

## Lösung

Die richtige Antwort ist 2.

Die speziellen Variablen `$1`, `$2` und `$3` stellen die Kommandozeilenargumente dar,
die dem Skript übergeben werden, so dass die Befehle ausgeführt werden:

```bash
$ head -n 1 cubane.pdb ethane.pdb octane.pdb pentane.pdb propane.pdb
$ tail -n 1 cubane.pdb ethane.pdb octane.pdb pentane.pdb propane.pdb
```

Die Shell expandiert `'*.pdb'` nicht, weil es von Anführungszeichen eingeschlossen ist.
Daher ist das erste Argument des Skripts `'*.pdb'`, das innerhalb des Skripts durch
`head` und `tail` expandiert wird.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Finde die längste Datei mit einer gegebenen Erweiterung

Schreiben Sie ein Shell-Skript namens `longest.sh`, das den Namen eines Verzeichnisses
und eine Dateinamenserweiterung als Argumente annimmt und den Namen der Datei mit den
meisten Zeilen in diesem Verzeichnis mit dieser Erweiterung ausgibt. Zum Beispiel:

```bash
$ bash longest.sh shell-lesson-data/exercise-data/alkanes pdb
```

würde den Namen der Datei `.pdb` in `shell-lesson-data/exercise-data/alkanes` ausgeben,
die die meisten Zeilen hat.

Sie können Ihr Skript auch in einem anderen Verzeichnis testen, z.B.

```bash
$ bash longest.sh shell-lesson-data/exercise-data/writing txt
```

::::::::::::::: solution

## Lösung

```bash
# Shell script which takes two arguments:
#    1. a directory name
#    2. a file extension
# and prints the name of the file in that directory
# with the most lines which matches the file extension.

wc -l $1/*.$2 | sort -n | tail -n 2 | head -n 1
```

Der erste Teil der Pipeline, `wc -l $1/*.$2 | sort -n`, zählt die Zeilen in jeder Datei
und sortiert sie numerisch (die größte zuletzt). Wenn es mehr als eine Datei gibt, gibt
`wc` auch eine abschließende Zusammenfassungszeile aus, die die Gesamtzahl der Zeilen in
*allen* Dateien angibt. Wir benutzen `tail -n 2 | head -n 1`, um diese letzte Zeile zu
verwerfen.

Mit `wc -l $1/*.$2 | sort -n | tail -n 1` sehen wir die abschließende
Zusammenfassungszeile: wir können unsere Pipeline stückweise aufbauen, um sicher zu
sein, dass wir die Ausgabe verstehen.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Skript Leseverstehen

Betrachten wir für diese Frage noch einmal das Verzeichnis
`shell-lesson-data/exercise-data/alkanes`. Dieses enthält eine Reihe von `.pdb`-Dateien
sowie weitere Dateien, die Sie möglicherweise erstellt haben. Erkläre, was jedes der
folgenden drei Skripte tun würde, wenn es als `bash script1.sh *.pdb`, `bash script2.sh
*.pdb` bzw. `bash script3.sh *.pdb` ausgeführt würde.

```bash
# Script 1
echo *.*
```

```bash
# Script 2
for filename in $1 $2 $3
do
    cat $filename
done
```

```bash
# Script 3
echo $@.pdb
```

::::::::::::::: solution

## Lösungen

In jedem Fall expandiert die Shell den Platzhalter in `*.pdb`, bevor sie die
resultierende Liste von Dateinamen als Argumente an das Skript weitergibt.

Skript 1 würde eine Liste aller Dateien ausgeben, die einen Punkt in ihrem Namen
enthalten. Die Argumente, die dem Skript übergeben werden, werden im Skript nirgends
verwendet.

Skript 2 würde den Inhalt der ersten drei Dateien mit der Dateierweiterung `.pdb`
ausgeben.`$1`, `$2` und `$3` beziehen sich jeweils auf das erste, zweite und dritte
Argument.

Skript 3 würde alle Argumente für das Skript ausgeben (d.h. alle `.pdb`-Dateien),
gefolgt von `.pdb`.`$@` bezieht sich auf *alle* Argumente, die einem Shell-Skript
übergeben werden.

```output
cubane.pdb ethane.pdb methane.pdb octane.pdb pentane.pdb propane.pdb.pdb
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Debugging-Skripte

Angenommen, Sie haben das folgende Skript in einer Datei namens `do-errors.sh` in Nelles
Verzeichnis `north-pacific-gyre` gespeichert:

```bash
# Calculate stats for data files.
for datafile in "$@"
do
    echo $datfile
    bash goostats.sh $datafile stats-$datafile
done
```

Wenn Sie es aus dem Verzeichnis `north-pacific-gyre` ausführen:

```bash
$ bash do-errors.sh NENE*A.txt NENE*B.txt
```

die Ausgabe ist leer. Um herauszufinden, warum, führen Sie das Skript mit der Option
`-x` erneut aus:

```bash
$ bash -x do-errors.sh NENE*A.txt NENE*B.txt
```

Was zeigt Ihnen die Ausgabe? Welche Zeile ist für den Fehler verantwortlich?

::::::::::::::: solution

## Lösung

Die Option `-x` bewirkt, dass `bash` im Debug-Modus läuft. Dadurch wird jeder Befehl
während seiner Ausführung ausgedruckt, was Ihnen hilft, Fehler zu finden. In diesem
Beispiel können wir sehen, dass `echo` nichts ausgibt. Wir haben einen Tippfehler im
Namen der Schleifenvariablen gemacht, und die Variable `datfile` existiert nicht und
gibt daher einen leeren String zurück.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::



:::::::::::::::::::::::::::::::::::::::: keypoints

- Speichern Sie Befehle in Dateien (normalerweise Shell-Skripte genannt) zur
  Wiederverwendung.
- `bash [filename]` führt die in einer Datei gespeicherten Befehle aus.
- `$@` bezieht sich auf alle Kommandozeilenargumente eines Shell-Skripts.
- `$1`, `$2`, etc. beziehen sich auf das erste Kommandozeilenargument, das zweite
  Kommandozeilenargument, etc.
- Setzen Sie Variablen in Anführungszeichen, wenn die Werte Leerzeichen enthalten
  könnten.
- Den Benutzer entscheiden zu lassen, welche Dateien verarbeitet werden sollen, ist
  flexibler und konsistenter mit den eingebauten Unix-Befehlen.

::::::::::::::::::::::::::::::::::::::::::::::::::



