# Morse-Alphabet senden

## Geheimzeichen: Das Morse-Alphabet II

**Hallo, wir sind Robi-x01 und Robi-x02 und werden dich beim Programmieren mit Micro:bit begleiten. Wir sind jetzt zu zweit, weil wir bei diesen Übungen dann Buchstaben an jeweils den anderen Micro:bit senden werden.**

<img width="20%" src="https://github.com/dlpl-mb/baa_morse_code_01/blob/master/images/robo_mbit_funk.gif?raw=1">  <img width="20%" src="https://github.com/dlpl-mb/baa_morse_code_01/blob/master/images/SOS.svg.png?raw=1">  <img width="20%" src="https://github.com/dlpl-mb/baa_morse_code_01/blob/master/images/robo_mbit_funk.gif?raw=1">

Wusstest du, dass ein Micro:bit mit anderen Micro:bits über Funkwellen kommunizieren kann. In dieser Morsecode-Lektion werden wir nun Nachrichten zwischen 2 Micro:bits versenden. Dazu müssen wir einige Vereinbarungen treffen, damit die Kommunikation auch funktioniert. Wenn sich etwa Robi-x01 (Sender) und Robi-x02 (Empfänger) in verschiedenen Räumen befinden und sich weder hören noch sehen können.

## Die Zeichen des Morsealphabets

<img width="100%" src="https://github.com/dlpl-mb/baa_morse_code_01/blob/master/images/morse-tab.png?raw=1">

* Drucke dir die Tabelle aller Morsecodes aus (rechte Maustaste - Bild kopieren und dann in Word einfügen und ausdrucken)

Damit unser Demonstrationsprogramm übersichtlich bleibt, arbeiten wir weiter mit einer kleinen Buchstabenliste (A bis G, nun auch das S und O), später, wenn das Programm fertig ist, werden wir alle Zeichen einbauen.

<img width="50%" src="https://github.com/dlpl-mb/baa_morse_code_01/blob/master/images/l2_prg_bst.png?raw=1">

* Fügt man mehrere Morsezeichen zu einem Wort zusammen, muss beachtet werden, dass nach jedem Morsebuchstaben ein Leerplatz bzw. ein Pause eingelegt wird, damit der Empfänger weiß, dass nun ein neues Wort beginnt.

### Eine Leseübung

* Sieht dir dieses kurze Morsewort an: ...  ---  ...
* Es besteht aus drei Buchstaben - finde die Buchstaben heraus!
* Dieses wichtigste Morse-Wort musst du dir merken - es ist für Notfälle gedacht:
* SOS ("save our ship"): drei kurz, drei lang, drei kurz: ...  ---  ...
* Beachte dabei, dass nach jedem Buchstaben **drei kurz** (=S) ein kurze Pause gemacht wird und erst dann **dreimal lang** (Buchstabe O) gesendet wird
* Wenn man das nun weiter denkt, so muss natürlich auch das Satzende erkannt werden: Dort fällt die Pause noch länger aus (etwa 1 Sekunde)
* Schreibt auf Papier, wie nun das folgende Wort heißen kann:  <img src="https://github.com/dlpl-mb/baa_morse_code_01/blob/master/images/anna.png?raw=1">

## Verbindung von 2 Micro:bits

* Um Sender und Empfänger spielen zu können, müssen zwei Micro:bits **verbunden** werden
* Arbeite auch hier mit deinem Partner/deiner Partnerin zusammen.

### Grundregeln zur Verbindung von Micro:bits sind

* Wählt gemeinsam einen Funkkanal von 1 bis 255 für eure Kommunikation aus
* Kein anderes Spielerpaar im Raum darf denselben Kanal verwenden, sonst gibt es Kommunikationssalat
* Wir wählen für unser Beispiel **99**
* Jetzt muss abgemacht werden, wer ist **Sender** und wer ist **Empfänger**:
* Es muss auch genau vereinbart werden, **wann und was soll gesendet werden**, **wie reagiert der Empfänger auf die Nachricht**, ...
* Das ist deshalb wichtig, weil später in getrennten Räumen gearbeiten wird und die sprachliche Verständigung nicht mehr möglich ist.
* Um beide Micro:bits über denselben Funkkanal verbinden - benötig man einen Befehl 

```blocks
radio.setGroup(99)
```

* Beide Partner werden in unserem Beispiel dasselbe Programm auf ihren Micro:bits benutzen.

### Der erster Test zur Übertragung

* **Die Aufgabenstellung heißt:**
  * Der Sender sendet eine Buchstaben
  * Der Empfänger zeigt den erhaltenen Buchstaben an
* Das Programm dazu könnte so aussehen:

```block
input.onButtonPressed(Button.A, function () {
    radio.sendString("X")
})
radio.onReceivedString(function (receivedString) {
    basic.showString(receivedString)
})
radio.setGroup(99)
```

[Programmcode **Senden eines Buchstabens**](https://makecode.microbit.org/_URKakefgfccf){:target="_blank"}

* Experimentiert mit diesem kleine Programm und ihr werdet merken, dass das nicht gut funktioniert, weil man bald nicht mehr weiß, wer, wann, was gesendet hat.
* Ihr müsst euch organisieren und verabreden, wer sendet und wer wartet.

### Wir müssen organisieren

* Versucht nun folgende Abmachung:
  * Nur ein Micro:bit ist **Sender** - der andere ist **Empfänger**
  * Gesendet wird mit der ``|Taste A|`` - geantwortet (bestätigt) wird mit ``|Taste B|`` (man sendet ein "ok")
  * Möchte man als Empfänger die Nachricht noch einmal - dann drückt man die ``|Tastenkombination A+B|`` (man sendet ein "no")
  * Das versuchen wir nun ein Programm zu fassen:

```blocks
input.onButtonPressed(Button.A, function () {
    radio.sendString("Hallo")
})
radio.onReceivedString(function (receivedString) {
    basic.showString(receivedString)
})
input.onButtonPressed(Button.B, function () {
    radio.sendString("ok")
})
input.onButtonPressed(Button.AB, function () {
    radio.sendString("no")
})
radio.setGroup(99)
```

[Programmcode **Bestätigen mit Antwort**](https://makecode.microbit.org/_RVzCKyPbCbg3){:target="_blank"}

* So mit dieser Abmachung können wir nun weiterarbeiten 
* Ihr könnt versuchen, die Sendennachricht zu ändern - der Empfänger bestätigt, ob der es bekommen hat und lesen konnte.
* Wechselt dann die Rollen
* Ganz besonders schwierig und realitätsnahe wird es, wenn ihr in verschiedene Räume geht
* Man sieht an diesem einfachen Beispiel, dass es extrem schwierig ist, eine Kommunikation aufzubauen, wenn Sender und Empfänger nicht in sprech- und sichtweite sind
* Sehr oft entstehen dann Probleme bei der Datenübertragung, wenn die Regeln nicht genau vereinbart wurden.
* Der Fachbegriff für diese Vereinbarungen heißt **Handshake** (wer sendet wie, wer antwortet wie, wann, ...)

* Erweitert das Senden auf ein ganzes Wort oder auch einen Satz 
* Der Empfänger muss die Nachricht immer zuerst lesen und auch erst bestätigen, dann darf der Sender wieder senden
* Merke: Es ist erst dann eine "perfekte Datenübertragung", wenn sie auch funktioniert, wenn man sich in verschiedenen Räumen befindet
* Schwierige Überlegung: Wie könnte man dem Empfänger im anderen Raum mitteilen, dass er jetzt der Sender sein soll?
  * Diskutiert Möglichkeiten dazu

## Eine aktuelle Anwendung der Profis

* Amerikanische Weltraummission:
  * Derzeit befindet sich auf dem Mars ein Roboter, dieser wird mit Befehlen von der Erde gesteuert
  * Ein Befehl dauert vom Absenden von der Erde bis zum Empfänger auf dem Mars acht Minuten.
  * Man kann sich vorstellen, dass hier sehr exakte Abmachungen getroffen werden müssen, wann sendet wer, wie ist die Antwort, ...
  * Auch alle Fotos vom Mars werden mit genauen Regel Zeichen-für-Zeichen zur Erde geschickt
  
<img width="50%" src="https://github.com/dlpl-mb/baa_morse_code_01/blob/master/images/rover.png?raw=1">

## Senden von Morsecodes

* Wir versuchen nun, zwischen den Micro:bit Morsecode zu senden (also eine Kombination aus Punkten und Strichen)
* Wir brauchen den bisherigen Nachrichtentext nur gegen Morsecodes auszutauschen

```blocks
input.onButtonPressed(Button.A, function () {
    radio.sendString("-..")
})
radio.onReceivedString(function (receivedString) {
    basic.showString(receivedString)
})
radio.setGroup(99)
```

* Mit Hilfe der Morsetabelle können die Empfänger das Zeichen decodieren (entschlüsseln)
* Wir bauen nun unser Kommunikationsprogramm so um, dass wir Morsezeichen senden können

[Programmcode **Morsezeichen senden**](https://makecode.microbit.org/_57W03beWCVrw){:target="_blank"}

* Experimentiert mit diesem einfachen Programm, indem ihr die Morsezeichen wechselt

### Übung: In einem Durchgang mehrere Morsezeichen übertragen

```blocks
input.onButtonPressed(Button.A, function () {
   radio.sendString("... --- ...")
})
radio.onReceivedString(function (receivedString) {
   basic.showString(receivedString) 
})
radio.setGroup(99)
```

* Dabei kann man nun schon gut erkennen, wie extrem schwierig es für den Empfänger ist, bei der Geschwindigkeit mit dem Lesen mithalten zu können
* Daher wurden die Zeichen früher bei sehr schnellen Übertragung auf Papier aufgezeichnet und im Nachhinein dann gelesen
* Es gab aber auch sehr geübte Angestellte bei der Postbehörde, die bei der Schnelligkeit der Übertragung mitgeschrieben haben
* In manchen alten Filmen sieht man noch, wie die Morsedaten verschickt oder empfangen worden sind.

<img width="50%" src="https://github.com/dlpl-mb/baa_morse_code_01/blob/master/images/Morseschreiber.jpg?raw=1">

### Einige Überlegungen zur Übung

* Bei der letzten Übung unser obiges **Handshake** einzubauen (= Bestätigen mit "ok" und wiederholte sendung anfordern mit "no")

* Eine ganze Zeile ist zu lesen: Der Vereinfachung halber sind nur die Wortgrenzen mit einem Schrägstrich markiert.
* [Programmcode **Senden einer Nachrichtenzeile**](https://makecode.microbit.org/_hhVeobX87KwU){:target="_blank"}

* Verwende diesen einfachen Programmcode und ändere die Übertragungsnachricht.
* Was könnte man beim Empfänger noch gestalten, damit dieser mehr Zeit hat zum Lesen? Oder die Nachricht noch einmal ansehen kann?
* Diskutiert: Was hat noch nicht gut funktioniert, was ist zu verbessern?

### Erweiterungen und Programmausbau

* Ein derartiges Programm kann man fast unendlich erweitern und mit neuen Funktionen versehen
* Versucht nun selber weiterzubauen
* Man könnte Morsecode in Lichtsignale umwandeln
* Man könnte Morsecode in soundsignale umwandeln

Einiges von dem werden wir im dritten Teil, dem Erweiterungsteil bearbeiten.

## [Aufruf des dritten Projektteils: **Morsecode professionell**](https://dlpl-mb.github.io/baa_morse_code_03)

<style>.page-header {font-size:1rem;height:0vh;padding-top:1.5rem}</style>
<script src="https://makecode.com/gh-pages-embed.js"></script><script>makeCodeRender("{{ site.makecode.home_url }}", "{{ site.github.owner_name }}/{{ site.github.repository_name }}");</script>
