---
title: Diskussion
---


## Alphabetische Suppe

Wenn der Befehl, um herauszufinden, wer wir sind, `whoami` heißt, sollte der Befehl, um
herauszufinden, wo wir sind, `whereami` heißen, warum heißt er dann `pwd`? Die übliche
Antwort lautet, dass in den frühen 1970er Jahren, als Unix entwickelt wurde, jeder
Tastenanschlag zählte: Die damaligen Geräte waren langsam, und die Rückwärtsbewegung auf
einer Fernschreibmaschine war so schmerzhaft, dass die Verringerung der Anzahl der
Tastenanschläge, um die Anzahl der Tippfehler zu verringern, eigentlich ein Gewinn für
die Benutzerfreundlichkeit war. Die Realität sieht so aus, dass die Befehle nach und
nach zu Unix hinzugefügt wurden, ohne einen Gesamtplan, von Leuten, die in den
Fachjargon eingetaucht waren. Das Ergebnis ist so uneinheitlich wie die roolz uv
englische Schreibweise, aber wir müssen uns jetzt damit abfinden.

## Job Control Codes

Die Shell akzeptiert ein paar spezielle Befehle, die es dem Benutzer ermöglichen, mit
laufenden Prozessen oder Programmen zu interagieren. Sie können jeden dieser
"Steuercodes" eingeben, indem Sie die Taste `Ctrl` gedrückt halten und dann eines der
Steuerzeichen drücken. In anderen Tutorien wird vielleicht der Begriff `Control` oder
`^` für die Taste `Ctrl` verwendet (z.B. sind die folgenden alle gleichwertig: `Ctrl-C`,
`Ctrl+C`, `Control-C`, `Control+C`, `^C`).

- `Ctrl-C`: unterbricht und bricht ein laufendes Programm ab. Dies ist nützlich, wenn
  Sie einen Befehl abbrechen wollen, der zu lange zur Ausführung braucht.

- `Ctrl-D`: zeigt das Ende einer Datei oder eines Zeichenstroms an, den Sie in die
  Befehlszeile eingeben. Wir haben zum Beispiel gesehen, dass der Befehl `wc` Zeilen,
  Wörter und Zeichen in einer Datei zählt. Wenn wir einfach `wc` eingeben und die
  Eingabetaste drücken, ohne einen Dateinamen anzugeben, dann nimmt `wc` an, dass wir
  alles analysieren wollen, was wir als nächstes eingeben. Nachdem wir unser Hauptwerk
  direkt in die Eingabeaufforderung getippt haben, können wir Ctrl-D eingeben, um `wc`
  mitzuteilen, dass wir fertig sind und die Ergebnisse der Wortzählung sehen möchten.

- `Ctrl-Z`: Suspendiert einen Prozess, beendet ihn aber nicht. Sie können dann den
  Befehl `fg` verwenden, um den Job im Vordergrund neu zu starten.

Für neue Shell-Benutzer können diese Kontrollcodes alle die gleiche Wirkung haben: Sie
lassen Dinge "verschwinden" Aber es ist hilfreich, die Unterschiede zu verstehen. Im
Allgemeinen ist es besser, `Ctrl-C` zu benutzen, wenn etwas schief gelaufen ist und Sie
einfach nur Ihren Shell-Prompt zurückbekommen wollen.

## Andere Shells

Bevor Bash Ende der neunziger Jahre populär wurde, benutzten Wissenschaftler häufig eine
andere Shell, die C-Shell oder Csh (und einige benutzen sie immer noch). Bash und Csh
haben einen ähnlichen Funktionsumfang, aber ihre Syntaxregeln sind unterschiedlich, was
sie inkompatibel zueinander macht. Sie sind größtenteils mit der Bash kompatibel, und
die Bash ist die Standard-Shell der meisten modernen Unix-Implementierungen
(einschließlich der meisten Pakete, die Unix-ähnliche Werkzeuge für Windows
bereitstellen), aber wenn Sie seltsame Fehler in Shell-Skripten erhalten, die von
Kollegen geschrieben wurden, sollten Sie überprüfen, für welche Shell sie geschrieben
wurden.

## Bash-Konfigurationen

Möchten Sie Pfade, Umgebungsvariablen, Aliase und andere Verhaltensweisen Ihrer Shell
anpassen? Dieser ausgezeichnete Blogbeitrag "[Bash Configurations
Demystified][bash-demystified]" von Dalton Hubble behandelt Tipps, Tricks und wie man
Gefahren vermeidet.

[bash-demystified]:
https://blog.dghubble.io/posts/.bashprofile-.profile-and-.bashrc-conventions/




