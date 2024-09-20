---
title: Introducing the Shell
teaching: 5
exercises: 0
---


::::::::::::::::::::::::::::::::::::::: objectives

- Erläutern Sie, wie die Shell mit der Tastatur, dem Bildschirm, dem Betriebssystem und
  den Programmen der Benutzer zusammenhängt.
- Erklären Sie, wann und warum Befehlszeilenschnittstellen anstelle von grafischen
  Schnittstellen verwendet werden sollten.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::::: questions

- Was ist eine Befehlsshell und warum sollte ich sie benutzen?

::::::::::::::::::::::::::::::::::::::::::::::::::

### Hintergrund

Menschen und Computer interagieren in der Regel auf viele verschiedene Arten, z. B. über
eine Tastatur und eine Maus, über Touchscreen-Schnittstellen oder über
Spracherkennungssysteme. Die am weitesten verbreitete Art der Interaktion mit
Personalcomputern wird als **grafische Benutzeroberfläche** (GUI) bezeichnet. Bei einer
GUI geben wir Anweisungen durch Mausklicks und menügesteuerte Interaktionen.

Während die visuelle Hilfe einer grafischen Benutzeroberfläche das Erlernen intuitiv
macht, ist diese Art, Anweisungen an einen Computer zu übermitteln, sehr schlecht
skalierbar. Stellen Sie sich folgende Aufgabe: Für eine Literaturrecherche müssen Sie
die dritte Zeile von eintausend Textdateien in eintausend verschiedenen Verzeichnissen
kopieren und in eine einzige Datei einfügen. Mit einer grafischen Benutzeroberfläche
würden Sie nicht nur stundenlang an Ihrem Schreibtisch herumklicken, sondern
möglicherweise auch einen Fehler bei der Erledigung dieser sich wiederholenden Aufgabe
begehen. An dieser Stelle kommt die Unix-Shell zum Einsatz. Die Unix-Shell ist sowohl
eine **Befehlszeilenschnittstelle** (CLI) als auch eine Skriptsprache, mit der solche
sich wiederholenden Aufgaben automatisch und schnell erledigt werden können. Mit den
richtigen Befehlen kann die Shell Aufgaben mit oder ohne Änderungen so oft wiederholen,
wie wir wollen. Mit der Shell kann die Aufgabe im Literaturbeispiel in Sekundenschnelle
erledigt werden.

### Die Muschel

Die Shell ist ein Programm, in das Benutzer Befehle eingeben können. Mit der Shell ist
es möglich, komplizierte Programme wie Klimamodellierungssoftware aufzurufen oder
einfache Befehle, die ein leeres Verzeichnis mit nur einer Zeile Code erstellen. Die
populärste Unix-Shell ist Bash (die Bourne Again SHell --- so genannt, weil sie von
einer Shell abgeleitet ist, die von Stephen Bourne geschrieben wurde). Bash ist die
Standard-Shell in den meisten modernen Unix-Implementierungen und in den meisten
Paketen, die Unix-ähnliche Werkzeuge für Windows bereitstellen. Beachten Sie, dass "Git
Bash" eine Software ist, die es Windows-Benutzern ermöglicht, eine Bash-ähnliche
Schnittstelle für die Interaktion mit Git zu verwenden.

Der Umgang mit der Shell ist mühsam und erfordert einige Zeit des Lernens. Während eine
grafische Benutzeroberfläche (GUI) Ihnen Auswahlmöglichkeiten anbietet, werden diese bei
der Befehlszeilenschnittstelle (CLI) nicht automatisch angeboten, so dass Sie einige
Befehle lernen müssen wie neue Vokabeln in einer Sprache, die Sie gerade lernen. Anders
als bei einer gesprochenen Sprache reicht jedoch eine kleine Anzahl von "Wörtern" (d. h.
Befehlen) aus, um weit zu kommen, und wir werden uns heute mit diesen wenigen wichtigen
Wörtern beschäftigen.

Die Grammatik einer Shell ermöglicht es Ihnen, vorhandene Werkzeuge zu leistungsfähigen
Pipelines zu kombinieren und große Datenmengen automatisch zu verarbeiten.
Befehlssequenzen können in ein *Skript* geschrieben werden, was die Reproduzierbarkeit
von Arbeitsabläufen verbessert.

Darüber hinaus ist die Kommandozeile oft die einfachste Möglichkeit, mit entfernten
Rechnern und Supercomputern zu interagieren. Die Vertrautheit mit der Shell ist nahezu
unverzichtbar, um eine Vielzahl von spezialisierten Tools und Ressourcen, einschließlich
Hochleistungsrechnersystemen, zu nutzen. Da Cluster und Cloud-Computing-Systeme für die
wissenschaftliche Datenverarbeitung immer beliebter werden, wird die Fähigkeit, mit der
Shell zu interagieren, zu einer notwendigen Fähigkeit. Wir können auf den hier
behandelten Kommandozeilenfähigkeiten aufbauen, um eine breite Palette
wissenschaftlicher Fragen und rechnerischer Herausforderungen zu bewältigen.

Fangen wir an.

Wenn die Shell zum ersten Mal geöffnet wird, erscheint ein **Prompt**, das anzeigt, dass
die Shell auf eine Eingabe wartet.

```bash
$
```

Die Shell verwendet normalerweise `$ ` als Prompt, kann aber auch ein anderes Symbol
verwenden. In den Beispielen dieser Lektion zeigen wir den Prompt als `$ `. Am
wichtigsten ist, dass Sie *nicht den Prompt* eingeben, wenn Sie Befehle eingeben. Geben
Sie nur den Befehl ein, der auf die Eingabeaufforderung folgt. Diese Regel gilt sowohl
in dieser Lektion als auch in Lektionen aus anderen Quellen. Beachten Sie auch, dass
Sie, nachdem Sie einen Befehl eingegeben haben, die <kbd>Eingabetaste</kbd> drücken
müssen, um ihn auszuführen.

Auf die Eingabeaufforderung folgt ein **Textcursor**, ein Zeichen, das die Position
angibt, an der Ihre Eingaben erscheinen werden. Der Cursor ist normalerweise ein
blinkender oder fester Block, kann aber auch ein Unterstrich oder eine Pipe sein. Sie
haben ihn vielleicht schon einmal in einem Texteditor-Programm gesehen, zum Beispiel

Beachten Sie, dass Ihre Eingabeaufforderung ein wenig anders aussehen könnte.
Insbesondere setzen die meisten gängigen Shell-Umgebungen standardmäßig Ihren
Benutzernamen und den Rechnernamen vor das `$`. Eine solche Eingabeaufforderung könnte
z.B. wie folgt aussehen

```bash
nelle@localhost $
```

Die Eingabeaufforderung kann auch mehr als das enthalten. Machen Sie sich keine Sorgen,
wenn Ihr Prompt nicht nur ein kurzes `$ ` ist. Diese Lektion hängt nicht von dieser
zusätzlichen Information ab und sie sollte Sie auch nicht behindern. Der einzige
wichtige Punkt, auf den Sie sich konzentrieren müssen, ist das Zeichen `$ ` selbst. Wir
werden später sehen, warum.

Probieren wir also unseren ersten Befehl aus, `ls`, die Abkürzung für Listing. Mit
diesem Befehl wird der Inhalt des aktuellen Verzeichnisses aufgelistet:

```bash
$ ls
```

```output
Desktop     Downloads   Movies      Pictures
Documents   Library     Music       Public
```

::::::::::::::::::::::::::::::::::::::::: callout

## Befehl nicht gefunden

Wenn die Shell kein Programm finden kann, dessen Name dem eingegebenen Befehl
entspricht, gibt sie eine Fehlermeldung aus, wie z.B:

```bash
$ ks
```

```output
ks: command not found
```

Dies kann passieren, wenn der Befehl falsch eingegeben wurde oder wenn das entsprechende
Programm nicht installiert ist.


::::::::::::::::::::::::::::::::::::::::::::::::::

## Nelle's Pipeline: Ein typisches Problem

Nelle Nemo, eine Meeresbiologin, ist gerade von einer sechsmonatigen Untersuchung des
[Nordpazifischen Wirbels](https://en.wikipedia.org/wiki/North_Pacific_Gyre)
zurückgekehrt, wo sie Proben von gallertartigen Meereslebewesen im [Great Pacific
Garbage Patch](https://en.wikipedia.org/wiki/Great_Pacific_Garbage_Patch) genommen hat.
Sie hat 1520 Proben, die sie durch ein Testgerät laufen ließ, um die relative Häufigkeit
von 300 Proteinen zu messen. Sie muss diese 1520 Dateien durch ein imaginäres Programm
namens `goostats.sh` laufen lassen. Zusätzlich zu dieser riesigen Aufgabe muss sie die
Ergebnisse bis Ende des Monats aufschreiben, damit ihr Artikel in einer Sonderausgabe
der *Aquatic Goo Letters* erscheinen kann.

Wenn Nelle sich dafür entscheidet, `goostats.sh` von Hand über eine grafische
Benutzeroberfläche auszuführen, muss sie eine Datei 1520 Mal auswählen und öffnen. Wenn
`goostats.sh` für die Ausführung jeder Datei 30 Sekunden benötigt, nimmt der gesamte
Prozess mehr als 12 Stunden von Nelles Aufmerksamkeit in Anspruch. Mit der Shell kann
Nelle stattdessen ihrem Computer diese banale Aufgabe übertragen, während sie sich auf
das Schreiben ihrer Arbeit konzentriert.

In den nächsten Lektionen wird untersucht, wie Nelle dies erreichen kann. Genauer
gesagt, wird in den Lektionen erklärt, wie sie eine Befehlsshell verwenden kann, um das
Programm `goostats.sh` auszuführen, wobei Schleifen verwendet werden, um die sich
wiederholenden Schritte der Eingabe von Dateinamen zu automatisieren, so dass ihr
Computer arbeiten kann, während sie ihre Arbeit schreibt.

Ein weiterer Vorteil ist, dass sie, sobald sie eine Verarbeitungspipeline erstellt hat,
diese bei jeder weiteren Datenerfassung wieder verwenden kann.

Um ihre Aufgabe erfüllen zu können, muss Nelle wissen, wie man:

- zu einer Datei/Verzeichnis navigieren
- eine Datei/Verzeichnis erstellen
- Prüfen der Länge einer Datei
- Befehle aneinanderreihen
- eine Reihe von Dateien abrufen
- iteriert über Dateien
- führt ein Shell-Skript mit ihrer Pipeline aus

:::::::::::::::::::::::::::::::::::::::: keypoints

- Eine Shell ist ein Programm, dessen Hauptzweck es ist, Befehle zu lesen und andere
  Programme auszuführen.
- Diese Lektion verwendet Bash, die Standard-Shell in vielen Unix-Implementierungen.
- Programme können in der Bash durch Eingabe von Befehlen an der Eingabeaufforderung
  ausgeführt werden.
- Die Hauptvorteile der Shell sind ihr gutes Verhältnis von Aktion zu Tastendruck, ihre
  Unterstützung bei der Automatisierung sich wiederholender Aufgaben und ihre Fähigkeit,
  auf vernetzte Maschinen zuzugreifen.
- Eine große Herausforderung bei der Verwendung der Shell kann darin bestehen, zu
  wissen, welche Befehle ausgeführt werden müssen und wie man sie ausführt.

::::::::::::::::::::::::::::::::::::::::::::::::::



