---
title: Finding Things
teaching: 25
exercises: 20
---


::::::::::::::::::::::::::::::::::::::: objectives

- Verwenden Sie `grep`, um Zeilen aus Textdateien auszuwählen, die einfachen Mustern
  entsprechen.
- Verwenden Sie `find`, um Dateien und Verzeichnisse zu finden, deren Namen einfachen
  Mustern entsprechen.
- Verwenden Sie die Ausgabe eines Befehls als Befehlszeilenargument(e) für einen anderen
  Befehl.
- Erläutern Sie, was mit "Text-" und "Binärdateien" gemeint ist und warum viele gängige
  Tools mit letzteren nicht gut umgehen können.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- Wie kann ich Dateien finden?
- Wie kann ich Dinge in Dateien finden?

::::::::::::::::::::::::::::::::::::::::::::::::::

Genauso wie viele von uns heute "Google" als Verb für "finden" verwenden, benutzen
Unix-Programmierer oft das Wort "grep". grep" ist eine Abkürzung für "global/regulärer
Ausdruck/Drucken", eine übliche Abfolge von Operationen in frühen Unix-Texteditoren. Es
ist auch der Name eines sehr nützlichen Befehlszeilenprogramms.

`grep` findet und druckt Zeilen in Dateien, die einem Muster entsprechen. Für unsere
Beispiele werden wir eine Datei verwenden, die drei Haiku enthält, die aus einem [1998er
Wettbewerb](https://web.archive.org/web/19991201042211/http://salon.com/21st/chal/1998/01/26chal.html)
in der Zeitschrift *Salon* stammen (Dank an die Autoren Bill Torcaso, Howard Korder und
Margaret Segall. Siehe Haiku-Fehlermeldungen im Archiv [Seite
1](https://web.archive.org/web/20000310061355/http://www.salon.com/21st/chal/1998/02/10chal2.html)
und [Seite
2](https://web.archive.org/web/20000229135138/http://www.salon.com/21st/chal/1998/02/10chal3.html)
.). Für diese Reihe von Beispielen arbeiten wir im Unterverzeichnis writing:

```bash
$ cd
$ cd Desktop/shell-lesson-data/exercise-data/writing
$ cat haiku.txt
```

```output
The Tao that is seen
Is not the true Tao, until
You bring fresh toner.

With searching comes loss
and the presence of absence:
"My Thesis" not found.

Yesterday it worked
Today it is not working
Software is like that.
```

Suchen wir nach Zeilen, die das Wort "nicht" enthalten:

```bash
$ grep not haiku.txt
```

```output
Is not the true Tao, until
"My Thesis" not found
Today it is not working
```

Hier ist `not` das Muster, nach dem wir suchen. Der Befehl grep durchsucht die Datei
nach Übereinstimmungen mit dem angegebenen Muster. Geben Sie dazu `grep` ein, dann das
gesuchte Muster und schließlich den Namen der Datei (oder der Dateien), in der Sie
suchen.

Ausgegeben werden die drei Zeilen in der Datei, die die Buchstaben "not" enthalten.

Standardmäßig sucht grep nach einem Muster, wobei die Groß- und Kleinschreibung beachtet
wird. Außerdem muss das von uns gewählte Suchmuster kein vollständiges Wort bilden, wie
wir im nächsten Beispiel sehen werden.

Suchen wir nach dem Muster: 'The'.

```bash
$ grep The haiku.txt
```

```output
The Tao that is seen
"My Thesis" not found.
```

Diesmal werden zwei Zeilen ausgegeben, die die Buchstaben "The" enthalten, von denen
eine unser Suchmuster innerhalb eines größeren Wortes, "Thesis", enthält.

Um die Treffer auf Zeilen zu beschränken, die das Wort "The" allein enthalten, können
wir die Option `grep` mit `-w` versehen. Dadurch werden die Treffer auf Wortgrenzen
beschränkt.

Später in dieser Lektion werden wir auch sehen, wie wir das Suchverhalten von grep in
Bezug auf die Groß- und Kleinschreibung ändern können.

```bash
$ grep -w The haiku.txt
```

```output
The Tao that is seen
```

Beachten Sie, dass eine "Wortgrenze" den Anfang und das Ende einer Zeile umfasst, also
nicht nur von Leerzeichen umgebene Buchstaben. Manchmal wollen wir nicht nach einem
einzelnen Wort suchen, sondern nach einer Phrase. Wir können dies auch mit `grep` tun,
indem wir die Phrase in Anführungszeichen setzen.

```bash
$ grep -w "is not" haiku.txt
```

```output
Today it is not working
```

Wir haben jetzt gesehen, dass Sie einzelne Wörter nicht in Anführungszeichen setzen
müssen, aber es ist sinnvoll, Anführungszeichen zu verwenden, wenn Sie nach mehreren
Wörtern suchen. Dies erleichtert auch die Unterscheidung zwischen dem Suchbegriff oder
der Phrase und der gesuchten Datei. In den folgenden Beispielen werden wir
Anführungszeichen verwenden.

Eine weitere nützliche Option ist `-n`, die die Zeilen nummeriert, die übereinstimmen:

```bash
$ grep -n "it" haiku.txt
```

```output
5:With searching comes loss
9:Yesterday it worked
10:Today it is not working
```

Hier kann man sehen, dass die Zeilen 5, 9 und 10 die Buchstaben "it" enthalten.

Wir können Optionen (d.h. Flags) wie bei anderen Unix-Befehlen kombinieren. Ein
Beispiel: Wir wollen die Zeilen finden, die das Wort "the" enthalten. Wir können die
Option `-w` kombinieren, um die Zeilen zu finden, die das Wort 'the' enthalten, und
`-n`, um die entsprechenden Zeilen zu nummerieren:

```bash
$ grep -n -w "the" haiku.txt
```

```output
2:Is not the true Tao, until
6:and the presence of absence:
```

Jetzt wollen wir die Option `-i` verwenden, um die Groß- und Kleinschreibung zu
ignorieren:

```bash
$ grep -n -w -i "the" haiku.txt
```

```output
1:The Tao that is seen
2:Is not the true Tao, until
6:and the presence of absence:
```

Jetzt wollen wir die Option `-v` verwenden, um unsere Suche zu invertieren, d.h. wir
wollen die Zeilen ausgeben, die das Wort 'the' nicht enthalten.

```bash
$ grep -n -w -v "the" haiku.txt
```

```output
1:The Tao that is seen
3:You bring fresh toner.
4:
5:With searching comes loss
7:"My Thesis" not found.
8:
9:Yesterday it worked
10:Today it is not working
11:Software is like that.
```

Wenn wir die Option `-r` (rekursiv) verwenden, kann `grep` nach einem Muster rekursiv
durch eine Menge von Dateien in Unterverzeichnissen suchen.

Lassen Sie uns rekursiv nach `Yesterday` im Verzeichnis
`shell-lesson-data/exercise-data/writing` suchen:

```bash
$ grep -r Yesterday .
```

```output
./LittleWomen.txt:"Yesterday, when Aunt was asleep and I was trying to be as still as a
./LittleWomen.txt:Yesterday at dinner, when an Austrian officer stared at us and then
./LittleWomen.txt:Yesterday was a quiet day spent in teaching, sewing, and writing in my
./haiku.txt:Yesterday it worked
```

`grep` hat viele andere Optionen. Um herauszufinden, welche das sind, können wir tippen:

```bash
$ grep --help
```

```output
Usage: grep [OPTION]... PATTERN [FILE]...
Search for PATTERN in each FILE or standard input.
PATTERN is, by default, a basic regular expression (BRE).
Example: grep -i 'hello world' menu.h main.c

Regexp selection and interpretation:
  -E, --extended-regexp     PATTERN is an extended regular expression (ERE)
  -F, --fixed-strings       PATTERN is a set of newline-separated fixed strings
  -G, --basic-regexp        PATTERN is a basic regular expression (BRE)
  -P, --perl-regexp         PATTERN is a Perl regular expression
  -e, --regexp=PATTERN      use PATTERN for matching
  -f, --file=FILE           obtain PATTERN from FILE
  -i, --ignore-case         ignore case distinctions
  -w, --word-regexp         force PATTERN to match only whole words
  -x, --line-regexp         force PATTERN to match only whole lines
  -z, --null-data           a data line ends in 0 byte, not newline

Miscellaneous:
...        ...        ...
```

::::::::::::::::::::::::::::::::::::::: challenge

## Mit `grep`

Welcher Befehl würde zu folgender Ausgabe führen:

```output
and the presence of absence:
```

1. `grep "of" haiku.txt`
2. `grep -E "of" haiku.txt`
3. `grep -w "of" haiku.txt`
4. `grep -i "of" haiku.txt`

::::::::::::::: solution

## Lösung

Die richtige Antwort ist 3, denn die Option `-w` sucht nur nach Übereinstimmungen mit
ganzen Wörtern. Die anderen Optionen passen auch auf "of", wenn es Teil eines anderen
Wortes ist.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::: callout

## Platzhalter

Die eigentliche Stärke von `grep` liegt jedoch nicht in seinen Optionen, sondern in der
Tatsache, dass Muster Platzhalter enthalten können. (Der technische Name dafür ist
**reguläre Ausdrücke**, wofür das 're' in 'grep' steht.) Reguläre Ausdrücke sind sowohl
komplex als auch mächtig; wenn Sie komplexe Suchvorgänge durchführen wollen, sehen Sie
sich bitte die Lektion auf [unserer
Website](https://librarycarpentry.org/lc-data-intro/01-regular-expressions.html) an. Als
Kostprobe können wir Zeilen finden, die ein 'o' an der zweiten Stelle haben, etwa so:

```bash
$ grep -E "^.o" haiku.txt
```

```output
You bring fresh toner.
Today it is not working
Software is like that.
```

Wir verwenden die Option `-E` und setzen das Muster in Anführungszeichen, um zu
verhindern, dass die Shell versucht, es zu interpretieren. (Wenn das Muster z.B. ein `*`
enthielte, würde die Shell versuchen, es zu expandieren, bevor sie `grep` ausführt.) Das
`^` im Muster verankert die Übereinstimmung am Anfang der Zeile. Das `.` passt auf ein
einzelnes Zeichen (genau wie `?` in der Shell), während das `o` auf ein tatsächliches
'o' passt.


::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Aufspüren einer Spezies

Leah hat mehrere hundert Datendateien in einem Verzeichnis gespeichert, von denen jede
wie folgt formatiert ist:

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

Sie möchte ein Shell-Skript schreiben, das eine Art als erstes Befehlszeilenargument und
ein Verzeichnis als zweites Argument annimmt. Das Skript soll eine Datei mit dem Namen
`<species>.txt` zurückgeben, die eine Liste von Daten und die Anzahl der an jedem Datum
beobachteten Arten enthält. Mit den oben gezeigten Daten würde `rabbit.txt` zum Beispiel
enthalten:

```source
2012-11-05,22
2012-11-06,19
2012-11-07,16
```

Nachfolgend enthält jede Zeile einen einzelnen Befehl, eine Pipe. Ordnen Sie deren
Reihenfolge in einem Befehl an, um Leahs Ziel zu erreichen:

```bash
cut -d : -f 2
>
|
grep -w $1 -r $2
|
$1.txt
cut -d , -f 1,3
```

Hinweis: Benutzen Sie `man grep`, um nachzuschauen, wie man Text in einem Verzeichnis
rekursiv einfängt und `man cut`, um mehr als ein Feld in einer Zeile auszuwählen.

Ein Beispiel für eine solche Datei findet sich in
`shell-lesson-data/exercise-data/animal-counts/animals.csv`

::::::::::::::: solution

## Lösung

```source
grep -w $1 -r $2 | cut -d : -f 2 | cut -d , -f 1,3 > $1.txt
```

Sie können die Reihenfolge der beiden Schnittbefehle vertauschen und es funktioniert
trotzdem. Versuchen Sie in der Befehlszeile, die Reihenfolge der Schnittbefehle zu
ändern, und sehen Sie sich die Ausgabe der einzelnen Schritte an, um zu sehen, warum
dies der Fall ist.

Sie würden das obige Skript wie folgt aufrufen:

```bash
$ bash count-species.sh bear .
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::: challenge

## Little Women

Sie und Ihr Freund haben gerade *Little Women* von Louisa May Alcott gelesen und
streiten sich. Von den vier Schwestern im Buch, Jo, Meg, Beth und Amy, meint Ihr Freund,
dass Jo am meisten erwähnt wurde. Sie hingegen sind sich sicher, dass es Amy war.
Glücklicherweise haben Sie eine Datei `LittleWomen.txt`, die den vollständigen Text des
Romans enthält (`shell-lesson-data/exercise-data/writing/LittleWomen.txt`). Wie würden
Sie mit Hilfe einer `for`-Schleife die Anzahl der Erwähnungen jeder der vier Schwestern
tabellarisch darstellen?

Hinweis: Eine Lösung könnte die Befehle `grep` und `wc` und ein `|` verwenden, während
eine andere die Optionen `grep` nutzt. Es gibt oft mehr als einen Weg, eine
Programmieraufgabe zu lösen, so dass eine bestimmte Lösung in der Regel auf der
Grundlage einer Kombination von korrektem Ergebnis, Eleganz, Lesbarkeit und
Geschwindigkeit gewählt wird.

::::::::::::::: solution

## Lösungen

```source
for sis in Jo Meg Beth Amy
do
    echo $sis:
    grep -ow $sis LittleWomen.txt | wc -l
done
```

Alternative, etwas schlechtere Lösung:

```source
for sis in Jo Meg Beth Amy
do
    echo $sis:
    grep -ocw $sis LittleWomen.txt
done
```

Diese Lösung ist minderwertig, weil `grep -c` nur die Anzahl der übereinstimmenden
Zeilen meldet. Die Gesamtzahl der Übereinstimmungen, die von dieser Methode gemeldet
wird, ist geringer, wenn es mehr als eine Übereinstimmung pro Zeile gibt.

Aufmerksamen Beobachtern ist vielleicht aufgefallen, dass die Namen der Figuren in den
Kapiteltiteln manchmal in Großbuchstaben erscheinen (z. B. 'MEG GOES TO VANITY FAIR').
Wenn Sie auch diese mitzählen wollten, könnten Sie die Option `-i` zur Unterscheidung
der Groß- und Kleinschreibung hinzufügen (obwohl dies in diesem Fall keinen Einfluss auf
die Antwort auf die Frage hat, welche Schwester am häufigsten erwähnt wird).



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

Während `grep` Zeilen in Dateien findet, findet der Befehl `find` die Dateien selbst.
Auch hier gibt es viele Optionen; um zu zeigen, wie die einfachsten davon funktionieren,
verwenden wir den unten gezeigten `shell-lesson-data/exercise-data`-Verzeichnisbaum.

```output
.
├── animal-counts/
│   └── animals.csv
├── creatures/
│   ├── basilisk.dat
│   ├── minotaur.dat
│   └── unicorn.dat
├── numbers.txt
├── alkanes/
│   ├── cubane.pdb
│   ├── ethane.pdb
│   ├── methane.pdb
│   ├── octane.pdb
│   ├── pentane.pdb
│   └── propane.pdb
└── writing/
    ├── haiku.txt
    └── LittleWomen.txt
```

Das Verzeichnis `exercise-data` enthält eine Datei, `numbers.txt` und vier
Verzeichnisse: `animal-counts`, `creatures`, `alkanes` und `writing`, die verschiedene
Dateien enthalten.

Für unseren ersten Befehl führen wir `find .` aus (denken Sie daran, diesen Befehl aus
dem Ordner `shell-lesson-data/exercise-data` auszuführen).

```bash
$ find .
```

```output
.
./writing
./writing/LittleWomen.txt
./writing/haiku.txt
./creatures
./creatures/basilisk.dat
./creatures/unicorn.dat
./creatures/minotaur.dat
./animal-counts
./animal-counts/animals.csv
./numbers.txt
./alkanes
./alkanes/ethane.pdb
./alkanes/propane.pdb
./alkanes/octane.pdb
./alkanes/pentane.pdb
./alkanes/methane.pdb
./alkanes/cubane.pdb
```

Wie immer steht `.` für das aktuelle Arbeitsverzeichnis, in dem wir unsere Suche
beginnen wollen. die Ausgabe von `find` sind die Namen aller Dateien **und**
Verzeichnisse unterhalb des aktuellen Arbeitsverzeichnisses. Dies kann zunächst nutzlos
erscheinen, aber `find` hat viele Optionen, um die Ausgabe zu filtern, und in dieser
Lektion werden wir einige davon entdecken.

Die erste Option in unserer Liste ist `-type d`, was "Dinge, die Verzeichnisse sind"
bedeutet. Natürlich ist die Ausgabe von `find` die Namen der fünf Verzeichnisse
(einschließlich `.`):

```bash
$ find . -type d
```

```output
.
./writing
./creatures
./animal-counts
./alkanes
```

Beachten Sie, dass die Objekte, die `find` findet, nicht in einer bestimmten Reihenfolge
aufgelistet sind. Wenn wir `-type d` in `-type f` ändern, erhalten wir stattdessen eine
Auflistung aller Dateien:

```bash
$ find . -type f
```

```output
./writing/LittleWomen.txt
./writing/haiku.txt
./creatures/basilisk.dat
./creatures/unicorn.dat
./creatures/minotaur.dat
./animal-counts/animals.csv
./numbers.txt
./alkanes/ethane.pdb
./alkanes/propane.pdb
./alkanes/octane.pdb
./alkanes/pentane.pdb
./alkanes/methane.pdb
./alkanes/cubane.pdb
```

Versuchen wir nun den Abgleich nach Namen:

```bash
$ find . -name *.txt
```

```output
./numbers.txt
```

Wir haben erwartet, dass sie alle Textdateien findet, aber sie gibt nur `./numbers.txt`
aus. Das Problem ist, dass die Shell Platzhalterzeichen wie `*` expandiert, *bevor*
Befehle ausgeführt werden. Da `*.txt` im aktuellen Verzeichnis zu `./numbers.txt`
expandiert, war der Befehl, den wir tatsächlich ausgeführt haben:

```bash
$ find . -name numbers.txt
```

`find` hat getan, worum wir gebeten haben; wir haben nur um das Falsche gebeten.

Um das zu bekommen, was wir wollen, machen wir das, was wir mit `grep` gemacht haben:
wir setzen `*.txt` in Anführungszeichen, um zu verhindern, dass die Shell den
Platzhalter `*` erweitert. Auf diese Weise erhält `find` tatsächlich das Muster `*.txt`,
nicht den erweiterten Dateinamen `numbers.txt`:

```bash
$ find . -name "*.txt"
```

```output
./writing/LittleWomen.txt
./writing/haiku.txt
./numbers.txt
```

::::::::::::::::::::::::::::::::::::::::: callout

## Auflistung vs. Auffinden

`ls` und `find` können mit den richtigen Optionen ähnliche Dinge tun, aber unter
normalen Umständen listet `ls` alles auf, was es kann, während `find` nach Dingen mit
bestimmten Eigenschaften sucht und sie anzeigt.


::::::::::::::::::::::::::::::::::::::::::::::::::

Wie wir bereits gesagt haben, liegt die Stärke der Kommandozeile in der Kombination von
Werkzeugen. Wir haben gesehen, wie man das mit Pipes macht; sehen wir uns eine andere
Technik an. Wie wir gerade gesehen haben, gibt uns `find . -name "*.txt"` eine Liste
aller Textdateien im oder unterhalb des aktuellen Verzeichnisses. Wie können wir das mit
`wc -l` kombinieren, um die Zeilen in all diesen Dateien zu zählen?

Am einfachsten ist es, den Befehl `find` in `$()` einzufügen:

```bash
$ wc -l $(find . -name "*.txt")
```

```output
  21022 ./writing/LittleWomen.txt
     11 ./writing/haiku.txt
      5 ./numbers.txt
  21038 total
```

Wenn die Shell diesen Befehl ausführt, wird als erstes das ausgeführt, was in `$()`
steht. Dann ersetzt sie den Ausdruck `$()` durch die Ausgabe dieses Befehls. Da die
Ausgabe von `find` aus den drei Dateinamen `./writing/LittleWomen.txt`,
`./writing/haiku.txt` und `./numbers.txt` besteht, konstruiert die Shell den Befehl:

```bash
$ wc -l ./writing/LittleWomen.txt ./writing/haiku.txt ./numbers.txt
```

das ist das, was wir wollten. Diese Expansion ist genau das, was die Shell macht, wenn
sie Platzhalter wie `*` und `?` expandiert, aber sie lässt uns jeden beliebigen Befehl
als unseren eigenen 'Platzhalter' verwenden.

Es ist sehr üblich, `find` und `grep` zusammen zu verwenden. Die erste findet Dateien,
die einem Muster entsprechen; die zweite sucht nach Zeilen innerhalb dieser Dateien, die
einem anderen Muster entsprechen. Hier können wir zum Beispiel txt-Dateien finden, die
das Wort "searching" enthalten, indem wir nach der Zeichenfolge "searching" in allen
`.txt`-Dateien im aktuellen Verzeichnis suchen:

```bash
$ grep "searching" $(find . -name "*.txt")
```

```output
./writing/LittleWomen.txt:sitting on the top step, affected to be searching for her book, but was
./writing/haiku.txt:With searching comes loss
```

::::::::::::::::::::::::::::::::::::::: challenge

## Zuordnen und Subtrahieren

Die Option `-v` für `grep` kehrt den Mustervergleich um, so dass nur Zeilen gedruckt
werden, die *nicht* dem Muster entsprechen. Welcher der folgenden Befehle findet dann
alle .dat-Dateien in `creatures` außer `unicorn.dat`? Sobald Sie sich Ihre Antwort
überlegt haben, können Sie die Befehle im Verzeichnis `shell-lesson-data/exercise-data`
testen.

1. `find creatures -name "*.dat" | grep -v unicorn`
2. `find creatures -name *.dat | grep -v unicorn`
3. `grep -v "unicorn" $(find creatures -name "*.dat")`
4. Keiner der oben genannten Fälle.

::::::::::::::: solution

## Lösung

Option 1 ist richtig. Das Einschließen des Match-Ausdrucks in Anführungszeichen
verhindert, dass die Shell ihn expandiert, so dass er an den Befehl `find` übergeben
wird.

Option 2 funktioniert auch in diesem Fall, weil die Shell versucht, `*.dat` zu
expandieren, aber es gibt keine `*.dat` Dateien im aktuellen Verzeichnis, also wird der
Platzhalterausdruck an `find` übergeben. Wir sind dem zum ersten Mal in [Episode
3](03-create.md) begegnet.

Option 3 ist falsch, weil sie den Inhalt der Dateien nach Zeilen durchsucht, die nicht
mit "unicorn" übereinstimmen, anstatt die Dateinamen zu durchsuchen.



:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::: callout

## Binäre Dateien

Wir haben uns ausschließlich auf die Suche nach Mustern in Textdateien konzentriert. Was
ist, wenn Ihre Daten als Bilder, in Datenbanken oder in einem anderen Format gespeichert
sind?

Eine Handvoll Werkzeuge erweitern `grep`, um einige Nicht-Text-Formate zu verarbeiten.
Ein verallgemeinerungsfähigerer Ansatz ist jedoch die Konvertierung der Daten in Text
oder die Extraktion der textähnlichen Elemente aus den Daten. Auf der einen Seite sind
damit einfache Dinge leicht zu erledigen. Auf der anderen Seite sind komplexe Dinge in
der Regel unmöglich. Es ist zum Beispiel einfach genug, ein Programm zu schreiben, das
X- und Y-Maße aus Bilddateien extrahiert, um damit zu spielen, aber wie würden Sie etwas
schreiben, um Werte in einem Arbeitsblatt zu finden, dessen Zellen Formeln enthalten?

Eine letzte Möglichkeit ist, zu erkennen, dass die Shell und die Textverarbeitung ihre
Grenzen haben, und eine andere Programmiersprache zu verwenden. Wenn es an der Zeit ist,
dies zu tun, seien Sie nicht zu streng mit der Shell. Viele moderne Programmiersprachen
haben viele Ideen von ihr übernommen, und Nachahmung ist auch die schönste Form des
Lobes.


::::::::::::::::::::::::::::::::::::::::::::::::::

Die Unix-Shell ist älter als die meisten Menschen, die sie benutzen. Sie hat so lange
überlebt, weil sie eine der produktivsten Programmierumgebungen ist, die je geschaffen
wurden --- vielleicht sogar *die* produktivste. Ihre Syntax mag kryptisch sein, aber wer
sie beherrscht, kann interaktiv mit verschiedenen Befehlen experimentieren und dann das
Gelernte zur Automatisierung seiner Arbeit nutzen. Grafische Benutzeroberflächen mögen
anfangs einfacher zu bedienen sein, aber einmal gelernt, ist die Produktivität der Shell
unschlagbar. Und wie Alfred North Whitehead 1911 schrieb: "Die Zivilisation schreitet
voran, indem sie die Zahl der wichtigen Operationen erweitert, die wir ausführen können,
ohne darüber nachzudenken

::::::::::::::::::::::::::::::::::::::: challenge

## `find` Pipeline Reading Comprehension

Schreiben Sie einen kurzen erklärenden Kommentar für das folgende Shell-Skript:

```bash
wc -l $(find . -name "*.dat") | sort -n
```

::::::::::::::: solution

## Lösung

1. Alle Dateien mit der Erweiterung `.dat` rekursiv im aktuellen Verzeichnis suchen
2. Zählen Sie die Anzahl der Zeilen, die jede dieser Dateien enthält
3. Sortieren Sie die Ausgabe aus Schritt 2. numerisch

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::



:::::::::::::::::::::::::::::::::::::::: keypoints

- `find` findet Dateien mit bestimmten Eigenschaften, die dem Muster entsprechen.
- `grep` wählt Zeilen in Dateien aus, die dem Muster entsprechen.
- `--help` ist eine Option, die von vielen Bash-Befehlen und Programmen unterstützt
  wird, die von der Bash aus ausgeführt werden können, um weitere Informationen über die
  Verwendung dieser Befehle oder Programme anzuzeigen.
- `man [command]` zeigt die Handbuchseite für einen bestimmten Befehl an.
- `$([command])` fügt die Ausgabe eines Befehls an dessen Stelle ein.

::::::::::::::::::::::::::::::::::::::::::::::::::



