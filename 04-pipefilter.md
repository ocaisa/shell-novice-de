---
title: Pipes und Filter
teaching: 25
exercises: 10
---


::::::::::::::::::::::::::::::::::::::: objectives

- Erklären Sie den Vorteil der Verknüpfung von Befehlen mit Pipes und Filtern.
- Kombiniere Sequenzen von Befehlen, um eine neue Ausgabe zu erhalten
- Leiten Sie die Ausgabe eines Befehls in eine Datei um.
- Erkläre, was normalerweise passiert, wenn ein Programm oder eine Pipeline keine
  Eingaben zu verarbeiten hat.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- Wie kann ich bestehende Befehle kombinieren, um eine gewünschte Ausgabe zu erzeugen?
- Wie kann ich nur einen Teil der Ausgabe anzeigen?

::::::::::::::::::::::::::::::::::::::::::::::::::

Nachdem wir nun ein paar grundlegende Befehle kennen, können wir uns endlich der
mächtigsten Eigenschaft der Shell zuwenden: der Leichtigkeit, mit der sie uns erlaubt,
bestehende Programme auf neue Weise zu kombinieren. Wir beginnen mit dem Verzeichnis
`shell-lesson-data/exercise-data/alkanes`, das sechs Dateien enthält, die einige
einfache organische Moleküle beschreiben. Die Erweiterung `.pdb` zeigt an, dass diese
Dateien im Protein Data Bank Format sind, einem einfachen Textformat, das den Typ und
die Position jedes Atoms im Molekül angibt.

```bash
$ ls
```

```output
cubane.pdb    methane.pdb    pentane.pdb
ethane.pdb    octane.pdb     propane.pdb
```

Lassen Sie uns einen Beispielbefehl ausführen:

```bash
$ wc cubane.pdb
```

```output
20  156 1158 cubane.pdb
```

`wc` ist der 'word count' Befehl: er zählt die Anzahl der Zeilen, Wörter und Zeichen in
Dateien (und gibt die Werte in dieser Reihenfolge von links nach rechts zurück).

Wenn wir den Befehl `wc *.pdb` ausführen, stimmt das `*` in `*.pdb` mit null oder mehr
Zeichen überein, also verwandelt die Shell `*.pdb` in eine Liste aller `.pdb` Dateien im
aktuellen Verzeichnis:

```bash
$ wc *.pdb
```

```output
  20  156  1158  cubane.pdb
  12  84   622   ethane.pdb
   9  57   422   methane.pdb
  30  246  1828  octane.pdb
  21  165  1226  pentane.pdb
  15  111  825   propane.pdb
 107  819  6081  total
```

Beachten Sie, dass `wc *.pdb` auch die Gesamtzahl aller Zeilen in der letzten Zeile der
Ausgabe anzeigt.

Wenn wir `wc -l` statt nur `wc` ausführen, zeigt die Ausgabe nur die Anzahl der Zeilen
pro Datei:

```bash
$ wc -l *.pdb
```

```output
  20  cubane.pdb
  12  ethane.pdb
   9  methane.pdb
  30  octane.pdb
  21  pentane.pdb
  15  propane.pdb
 107  total
```

Die Optionen `-m` und `-w` können auch mit dem Befehl `wc` verwendet werden, um nur die
Anzahl der Zeichen bzw. die Anzahl der Wörter anzuzeigen.

::::::::::::::::::::::::::::::::::::::::: callout

## Why Isn't Doing Anything?

Was passiert, wenn ein Befehl eine Datei verarbeiten soll, wir ihm aber keinen
Dateinamen geben? Was passiert zum Beispiel, wenn wir eingeben:

```bash
$ wc -l
```

liest, aber nach dem Befehl nicht `*.pdb` (oder irgendetwas anderes) einträgt? Da es
keine Dateinamen hat, geht `wc` davon aus, dass es Eingaben an der Eingabeaufforderung
verarbeiten soll, also sitzt es einfach da und wartet darauf, dass wir ihm interaktiv
Daten geben. Von außen sehen wir jedoch nur, wie es dasitzt, und der Befehl scheint
nichts zu tun.

Wenn Sie einen solchen Fehler machen, können Sie sich aus diesem Zustand befreien, indem
Sie die Steuerungstaste (<kbd>Ctrl</kbd>) gedrückt halten und einmal den Buchstaben
<kbd>C</kbd> drücken: <kbd>Strg</kbd>\+<kbd>C</kbd>. Lassen Sie dann beide Tasten los.


::::::::::::::::::::::::::::::::::::::::::::::::::

## Erfassen der Ausgabe von Befehlen

Welche dieser Dateien enthält die wenigsten Zeilen? Diese Frage ist leicht zu
beantworten, wenn es nur sechs Dateien gibt, aber was wäre, wenn es 6000 wären? Unser
erster Schritt zur Lösung besteht darin, den Befehl auszuführen:

```bash
$ wc -l *.pdb > lengths.txt
```

Das Größer-als-Symbol, `>`, weist die Shell an, die Ausgabe des Befehls in eine Datei
**umzuleiten**, anstatt sie auf dem Bildschirm auszugeben. Dieser Befehl gibt keine
Bildschirmausgabe aus, da alles, was `wc` gedruckt hätte, stattdessen in die Datei
`lengths.txt` gelangt ist. Wenn die Datei vor der Ausgabe des Befehls nicht existiert,
wird die Shell die Datei erstellen. Wenn die Datei bereits existiert, wird sie
stillschweigend überschrieben, was zu Datenverlusten führen kann. Daher ist bei
**redirect**-Befehlen Vorsicht geboten.

`ls lengths.txt` bestätigt, dass die Datei existiert:

```bash
$ ls lengths.txt
```

```output
lengths.txt
```

Wir können jetzt den Inhalt von `lengths.txt` mit `cat lengths.txt` auf den Bildschirm
schicken. Der Befehl `cat` hat seinen Namen von 'concatenate', d.h. zusammenfügen, und
er gibt den Inhalt von Dateien nacheinander aus. In diesem Fall gibt es nur eine Datei,
also zeigt uns `cat` nur, was sie enthält:

```bash
$ cat lengths.txt
```

```output
  20  cubane.pdb
  12  ethane.pdb
   9  methane.pdb
  30  octane.pdb
  21  pentane.pdb
  15  propane.pdb
 107  total
```

::::::::::::::::::::::::::::::::::::::::: callout

## Ausgabe Seite für Seite

Aus Gründen der Bequemlichkeit und Konsistenz werden wir in dieser Lektion weiterhin
`cat` verwenden, aber es hat den Nachteil, dass es immer die gesamte Datei auf den
Bildschirm ausgibt. In der Praxis ist der Befehl `less` (z.B. `less lengths.txt`)
nützlicher. Dieser Befehl zeigt einen Bildschirminhalt der Datei an und hält dann an.
Sie können mit der Leertaste einen Bildschirm vorwärts oder mit `b` einen Bildschirm
zurück gehen. Drücken Sie `q` zum Beenden.


::::::::::::::::::::::::::::::::::::::::::::::::::

## Filtern der Ausgabe

Als nächstes werden wir den Befehl `sort` benutzen, um den Inhalt der Datei
`lengths.txt` zu sortieren. Aber zuerst werden wir eine Übung machen, um etwas über den
Sortierbefehl zu lernen:

::::::::::::::::::::::::::::::::::::::: challenge

## Was macht `sort -n`?

Die Datei `shell-lesson-data/exercise-data/numbers.txt` enthält die folgenden Zeilen:

```source
10
2
19
22
6
```

Wenn wir `sort` auf dieser Datei ausführen, ist die Ausgabe:

```output
10
19
2
22
6
```

Wenn wir `sort -n` in der gleichen Datei ausführen, erhalten wir stattdessen dies:

```output
2
6
10
19
22
```

Erkläre, warum `-n` diesen Effekt hat.

::::::::::::::: solution

## Lösung

Die Option `-n` legt eine numerische statt einer alphanumerischen Sortierung fest.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

Wir werden auch die Option `-n` verwenden, um anzugeben, dass die Sortierung numerisch
statt alphanumerisch ist. Dadurch wird die Datei *nicht* verändert; stattdessen wird das
sortierte Ergebnis auf dem Bildschirm ausgegeben:

```bash
$ sort -n lengths.txt
```

```output
  9  methane.pdb
 12  ethane.pdb
 15  propane.pdb
 20  cubane.pdb
 21  pentane.pdb
 30  octane.pdb
107  total
```

Wir können die sortierte Liste von Zeilen in eine andere temporäre Datei namens
`sorted-lengths.txt` schreiben, indem wir `> sorted-lengths.txt` nach dem Befehl
einfügen, so wie wir `> lengths.txt` benutzt haben, um die Ausgabe von `wc` in
`lengths.txt` zu schreiben. Wenn wir das getan haben, können wir einen weiteren Befehl
namens `head` ausführen, um die ersten Zeilen in `sorted-lengths.txt` zu erhalten:

```bash
$ sort -n lengths.txt > sorted-lengths.txt
$ head -n 1 sorted-lengths.txt
```

```output
  9  methane.pdb
```

Die Verwendung von `-n 1` mit `head` sagt ihm, dass wir nur die erste Zeile der Datei
wollen; `-n 20` würde die ersten 20 bekommen, und so weiter. Da `sorted-lengths.txt` die
Längen unserer Dateien in der Reihenfolge vom kleinsten zum größten Wert enthält, muss
die Ausgabe von `head` die Datei mit den wenigsten Zeilen sein.

::::::::::::::::::::::::::::::::::::::::: callout

## Umleitung auf dieselbe Datei

Es ist eine sehr schlechte Idee, zu versuchen, die Ausgabe eines Befehls, der auf eine
Datei wirkt, in dieselbe Datei umzuleiten. Zum Beispiel:

```bash
$ sort -n lengths.txt > lengths.txt
```

Wenn Sie so etwas tun, kann das zu falschen Ergebnissen führen und/oder den Inhalt von
`lengths.txt` löschen.


::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Was bedeutet `>>`?

Wir haben die Verwendung von `>` gesehen, aber es gibt einen ähnlichen Operator `>>`,
der etwas anders funktioniert. Wir werden die Unterschiede zwischen diesen beiden
Operatoren kennenlernen, indem wir einige Zeichenketten ausgeben. Mit dem Befehl `echo`
können wir Zeichenketten ausgeben, z.B.

```bash
$ echo The echo command prints text
```

```output
The echo command prints text
```

Testen Sie nun die folgenden Befehle, um den Unterschied zwischen den beiden Operatoren
herauszufinden:

```bash
$ echo hello > testfile01.txt
```

und:

```bash
$ echo hello >> testfile02.txt
```

Tipp: Versuchen Sie, jeden Befehl zweimal hintereinander auszuführen und dann die
Ausgabedateien zu untersuchen.

::::::::::::::: solution

## Lösung

Im ersten Beispiel mit `>` wird die Zeichenkette 'hello' nach `testfile01.txt`
geschrieben, aber die Datei wird jedes Mal überschrieben, wenn wir den Befehl ausführen.

Im zweiten Beispiel sehen wir, dass der `>>`-Operator auch 'hallo' in eine Datei
schreibt (in diesem Fall `testfile02.txt`), aber die Zeichenkette an die Datei anhängt,
wenn sie bereits existiert (d.h. wenn wir es zum zweiten Mal ausführen).



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Daten anhängen

Wir haben bereits den Befehl `head` kennengelernt, der Zeilen vom Anfang einer Datei
ausgibt. der Befehl `tail` ist ähnlich, druckt aber stattdessen Zeilen vom Ende einer
Datei aus.

Betrachten Sie die Datei `shell-lesson-data/exercise-data/animal-counts/animals.csv`.
Wählen Sie nach diesen Befehlen die Antwort aus, die der Datei `animals-subset.csv`
entspricht:

```bash
$ head -n 3 animals.csv > animals-subset.csv
$ tail -n 2 animals.csv >> animals-subset.csv
```

1. Die ersten drei Zeilen von `animals.csv`
2. Die letzten beiden Zeilen von `animals.csv`
3. Die ersten drei Zeilen und die letzten zwei Zeilen von `animals.csv`
4. Die zweite und dritte Zeile von `animals.csv`

::::::::::::::: solution

## Lösung

Option 3 ist richtig. Damit Option 1 richtig ist, würden wir nur den Befehl `head`
ausführen. Damit Option 2 richtig ist, würden wir nur den Befehl `tail` ausführen. Damit
Option 4 richtig ist, müssen wir die Ausgabe von `head` in `tail -n 2` leiten, indem wir
`head -n 3 animals.csv | tail -n 2 > animals-subset.csv` ausführen



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

## Übergabe der Ausgabe an einen anderen Befehl

In unserem Beispiel, die Datei mit den wenigsten Zeilen zu finden, benutzen wir zwei
Zwischendateien `lengths.txt` und `sorted-lengths.txt`, um die Ausgabe zu speichern. Das
ist eine verwirrende Arbeitsweise, denn selbst wenn man einmal verstanden hat, was `wc`,
`sort` und `head` tun, machen es diese Zwischendateien schwer zu verstehen, was vor sich
geht. Wir können es einfacher machen, indem wir `sort` und `head` zusammen ausführen:

```bash
$ sort -n lengths.txt | head -n 1
```

```output
  9  methane.pdb
```

Der vertikale Balken, `|`, zwischen den beiden Befehlen wird **pipe** genannt. Er sagt
der Shell, dass wir die Ausgabe des Befehls auf der linken Seite als Eingabe für den
Befehl auf der rechten Seite verwenden wollen.

Damit ist die Datei `sorted-lengths.txt` überflüssig geworden.

## Kombinieren mehrerer Befehle

Nichts hindert uns daran, Pipes hintereinander zu schalten. Wir können z.B. die Ausgabe
von `wc` direkt an `sort` schicken, und dann die resultierende Ausgabe an `head`. Dies
macht Zwischendateien überflüssig.

Wir beginnen damit, eine Pipe zu benutzen, um die Ausgabe von `wc` nach `sort` zu
schicken:

```bash
$ wc -l *.pdb | sort -n
```

```output
   9 methane.pdb
  12 ethane.pdb
  15 propane.pdb
  20 cubane.pdb
  21 pentane.pdb
  30 octane.pdb
 107 total
```

Wir können diese Ausgabe dann durch eine weitere Pipe nach `head` schicken, so dass die
komplette Pipeline daraus wird:

```bash
$ wc -l *.pdb | sort -n | head -n 1
```

```output
   9  methane.pdb
```

Das ist genau so, als würde ein Mathematiker Funktionen wie *log(3x)* verschachteln und
sagen 'der Logarithmus von dreimal *x*'. In unserem Fall ist der Algorithmus "Kopf der
Sortierung der Zeilenzahl von `*.pdb`".

Die Umleitung und die Pipes, die in den letzten Befehlen verwendet wurden, sind unten
dargestellt:

![](fig/redirects-and-pipes.svg){alt='Redirects und Pipes von verschiedenen Befehlen:
"wc -l \*.pdb" leitet die Ausgabe an die Shell weiter. "wc -l \*.pdb > lengths" leitet
die Ausgabe in die Datei "lengths". "wc -l \*.pdb | sort -n | head -n 1" erstellt eine
Pipeline, bei der die Ausgabe des "wc"-Befehls die Eingabe für den "sort"-Befehl ist,
die Ausgabe des "sort"-Befehls die Eingabe für den "head"-Befehl ist und die Ausgabe des
"head"-Befehls an die Shell geleitet wird'}

::::::::::::::::::::::::::::::::::::::: challenge

## Befehle in Pipes zusammenfassen

In unserem aktuellen Verzeichnis wollen wir die 3 Dateien finden, die die wenigsten
Zeilen haben. Welcher der unten aufgeführten Befehle würde funktionieren?

1. `wc -l * > sort -n > head -n 3`
2. `wc -l * | sort -n | head -n 1-3`
3. `wc -l * | head -n 3 | sort -n`
4. `wc -l * | sort -n | head -n 3`

::::::::::::::: solution

## Lösung

Option 4 ist die Lösung. Das Pipe-Zeichen `|` wird verwendet, um die Ausgabe eines
Befehls mit der Eingabe eines anderen zu verbinden.`>` wird verwendet, um die
Standardausgabe in eine Datei umzuleiten. Probieren Sie es im Verzeichnis
`shell-lesson-data/exercise-data/alkanes` aus!



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

## Werkzeuge, die zusammenarbeiten sollen

Diese Idee, Programme miteinander zu verbinden, ist der Grund, warum Unix so erfolgreich
ist. Anstatt riesige Programme zu erstellen, die versuchen, viele verschiedene Dinge zu
tun, konzentrieren sich die Unix-Programmierer darauf, viele einfache Werkzeuge zu
erstellen, die jeweils eine Aufgabe gut erledigen und gut miteinander arbeiten. Dieses
Programmiermodell wird "Pipes und Filter" genannt. Wir haben bereits Pipes gesehen; ein
**Filter** ist ein Programm wie `wc` oder `sort`, das einen Eingabestrom in einen
Ausgabestrom umwandelt. Fast alle Unix-Standardwerkzeuge können auf diese Weise
arbeiten. Wenn sie nicht anders angewiesen werden, lesen sie von der Standardeingabe,
machen etwas mit dem, was sie gelesen haben, und schreiben auf die Standardausgabe.

Der Schlüssel ist, dass jedes Programm, das Textzeilen von der Standardeingabe liest und
Textzeilen auf die Standardausgabe schreibt, mit jedem anderen Programm kombiniert
werden kann, das sich ebenfalls so verhält. Sie können *und sollten* Ihre Programme auf
diese Weise schreiben, damit Sie und andere Leute diese Programme in Pipes einbinden
können, um ihre Leistung zu vervielfachen.

::::::::::::::::::::::::::::::::::::::: challenge

## Pipe Reading Comprehension

Eine Datei namens `animals.csv` (im Ordner
`shell-lesson-data/exercise-data/animal-counts`) enthält die folgenden Daten:

```source
2012-11-05,deer,5
2012-11-05,rabbit,22
2012-11-05,raccoon,7
2012-11-06,rabbit,19
2012-11-06,deer,2
2012-11-06,fox,4
2012-11-07,rabbit,16
2012-11-07,bear,1
```

Welcher Text durchläuft die einzelnen Pipes und die endgültige Umleitung in der
folgenden Pipeline? Beachten Sie, dass der Befehl `sort -r` in umgekehrter Reihenfolge
sortiert.

```bash
$ cat animals.csv | head -n 5 | tail -n 3 | sort -r > final.txt
```

Tipp: Bauen Sie die Pipeline einen Befehl nach dem anderen auf, um Ihr Verständnis zu
testen

::::::::::::::: solution

## Lösung

Der Befehl `head` extrahiert die ersten 5 Zeilen aus `animals.csv`. Dann werden die
letzten 3 Zeilen mit dem Befehl `tail` aus den vorherigen 5 Zeilen extrahiert. Mit dem
Befehl `sort -r` werden diese 3 Zeilen in umgekehrter Reihenfolge sortiert. Schließlich
wird die Ausgabe in eine Datei umgeleitet: ,`final.txt`. Der Inhalt dieser Datei kann
durch Ausführen von `cat final.txt` überprüft werden. Die Datei sollte die folgenden
Zeilen enthalten:

```source
2012-11-06,rabbit,19
2012-11-06,deer,2
2012-11-05,raccoon,7
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Pipe-Konstruktion

Betrachten Sie für die Datei `animals.csv` aus der vorherigen Übung den folgenden
Befehl:

```bash
$ cut -d , -f 2 animals.csv
```

Der Befehl `cut` wird verwendet, um bestimmte Abschnitte jeder Zeile in der Datei zu
entfernen oder "auszuschneiden", und `cut` erwartet, dass die Zeilen durch ein
<kbd>Tab</kbd>-Zeichen in Spalten getrennt sind. Ein Zeichen, das auf diese Weise
verwendet wird, nennt man ein **Begrenzungszeichen**. Im obigen Beispiel verwenden wir
die Option `-d`, um das Komma als Begrenzungszeichen anzugeben. Wir haben auch die
Option `-f` verwendet, um anzugeben, dass wir das zweite Feld (Spalte) extrahieren
wollen. Dies ergibt die folgende Ausgabe:

```output
deer
rabbit
raccoon
rabbit
deer
fox
rabbit
bear
```

Der Befehl `uniq` filtert benachbarte übereinstimmende Zeilen in einer Datei heraus. Wie
könnte man diese Pipeline (mit `uniq` und einem anderen Befehl) erweitern, um
herauszufinden, welche Tiere die Datei enthält (ohne Duplikate in ihren Namen)?

::::::::::::::: solution

## Lösung

```bash
$ cut -d , -f 2 animals.csv | sort | uniq
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Welche Pipe?

Die Datei `animals.csv` enthält 8 Zeilen mit Daten, die wie folgt formatiert sind:

```output
2012-11-05,deer,5
2012-11-05,rabbit,22
2012-11-05,raccoon,7
2012-11-06,rabbit,19
...
```

Der Befehl `uniq` hat eine Option `-c`, die eine Zählung der Anzahl der Zeilen in der
Eingabe vornimmt. Angenommen, Ihr aktuelles Verzeichnis ist
`shell-lesson-data/exercise-data/animal-counts`. Welchen Befehl würden Sie verwenden, um
eine Tabelle zu erstellen, die die Gesamtzahl der einzelnen Tierarten in der Datei
anzeigt?

1. `sort animals.csv | uniq -c`
2. `sort -t, -k2,2 animals.csv | uniq -c`
3. `cut -d, -f 2 animals.csv | uniq -c`
4. `cut -d, -f 2 animals.csv | sort | uniq -c`
5. `cut -d, -f 2 animals.csv | sort | uniq -c | wc -l`

::::::::::::::: solution

## Lösung

Option 4. ist die richtige Antwort. Wenn Sie Schwierigkeiten haben zu verstehen, warum,
versuchen Sie, die Befehle oder Unterabschnitte der Pipelines auszuführen (stellen Sie
sicher, dass Sie sich im Verzeichnis `shell-lesson-data/exercise-data/animal-counts`
befinden).



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

## Nelle's Pipeline: Prüfen von Dateien

Nelle hat ihre Proben durch die Testmaschinen laufen lassen und 17 Dateien in dem zuvor
beschriebenen Verzeichnis `north-pacific-gyre` erstellt. Zur schnellen Überprüfung tippt
Nelle, ausgehend vom Verzeichnis `shell-lesson-data`, ein:

```bash
$ cd north-pacific-gyre
$ wc -l *.txt
```

Die Ausgabe besteht aus 18 Zeilen, die wie folgt aussehen:

```output
300 NENE01729A.txt
300 NENE01729B.txt
300 NENE01736A.txt
300 NENE01751A.txt
300 NENE01751B.txt
300 NENE01812A.txt
... ...
```

Jetzt tippt sie dies:

```bash
$ wc -l *.txt | sort -n | head -n 5
```

```output
 240 NENE02018B.txt
 300 NENE01729A.txt
 300 NENE01729B.txt
 300 NENE01736A.txt
 300 NENE01751A.txt
```

Hoppla: eine der Dateien ist 60 Zeilen kürzer als die anderen. Als sie zurückgeht und
nachsieht, stellt sie fest, dass sie diesen Versuch um 8 Uhr an einem Montagmorgen
durchgeführt hat - wahrscheinlich hat jemand den Rechner am Wochenende benutzt und sie
hat vergessen, ihn zurückzusetzen. Bevor sie die Probe erneut durchführt, prüft sie, ob
irgendwelche Dateien zu viele Daten haben:

```bash
$ wc -l *.txt | sort -n | tail -n 5
```

```output
 300 NENE02040B.txt
 300 NENE02040Z.txt
 300 NENE02043A.txt
 300 NENE02043B.txt
5040 total
```

Diese Zahlen sehen gut aus --- aber was macht das 'Z' in der drittletzten Zeile? Alle
ihre Proben sollten mit "A" oder "B" gekennzeichnet sein; ihr Labor verwendet
vereinbarungsgemäß "Z", um Proben mit fehlenden Informationen zu kennzeichnen. Um andere
Proben dieser Art zu finden, geht sie folgendermaßen vor:

```bash
$ ls *Z.txt
```

```output
NENE01971Z.txt    NENE02040Z.txt
```

Als sie das Protokoll auf ihrem Laptop überprüft, ist für keine der beiden Proben eine
Tiefe aufgezeichnet. Da es zu spät ist, die Informationen auf andere Weise zu erhalten,
muss sie diese beiden Dateien von ihrer Analyse ausschließen. Sie könnte sie mit `rm`
löschen, aber es gibt tatsächlich einige Analysen, die sie später durchführen könnte,
bei denen die Tiefe keine Rolle spielt. Stattdessen muss sie später darauf achten,
Dateien mit den Platzhalterausdrücken `NENE*A.txt NENE*B.txt` auszuwählen.

::::::::::::::::::::::::::::::::::::::: challenge

## Unnötige Dateien entfernen

Angenommen, Sie wollen Ihre verarbeiteten Datendateien löschen und nur Ihre Rohdateien
und das Verarbeitungsskript behalten, um Speicherplatz zu sparen. Die Rohdateien enden
auf `.dat` und die verarbeiteten Dateien auf `.txt`. Welche der folgenden Möglichkeiten
würde alle verarbeiteten Datendateien und *nur* die verarbeiteten Datendateien löschen?

1. `rm ?.txt`
2. `rm *.txt`
3. `rm * .txt`
4. `rm *.*`

::::::::::::::: solution

## Lösung

1. Dies würde `.txt` Dateien mit einstelligen Namen entfernen
2. Dies ist die richtige Antwort
3. Die Shell würde `*` so erweitern, dass es auf alles im aktuellen Verzeichnis passt,
   also würde der Befehl versuchen, alle passenden Dateien und eine zusätzliche Datei
   namens `.txt` zu entfernen
4. Die Shell expandiert `*.*`, um alle Dateinamen zu finden, die mindestens ein `.`
   enthalten, einschließlich der verarbeiteten Dateien (`.txt`) *und* der Rohdateien
   (`.dat`)

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::



:::::::::::::::::::::::::::::::::::::::: keypoints

- `wc` zählt Zeilen, Wörter und Zeichen in seinen Eingaben.
- `cat` zeigt den Inhalt seiner Eingänge an.
- `sort` sortiert seine Eingaben.
- `head` zeigt die ersten 10 Zeilen seiner Eingabe an.
- `tail` zeigt die letzten 10 Zeilen seiner Eingabe an.
- `command > [file]` leitet die Ausgabe eines Befehls in eine Datei um (und überschreibt
  dabei einen bereits vorhandenen Inhalt).
- `command >> [file]` hängt die Ausgabe eines Befehls an eine Datei an.
- `[first] | [second]` ist eine Pipeline: die Ausgabe des ersten Befehls wird als
  Eingabe für den zweiten verwendet.
- Der beste Weg, die Shell zu benutzen, ist die Verwendung von Pipes, um einfache
  Einzweckprogramme (Filter) zu kombinieren.

::::::::::::::::::::::::::::::::::::::::::::::::::



