# Morse-Alphabet senden

## Geheimzeichen: Das Morse-Alphabet II

**Hallo, wir sind Robi-x01 und Robi-x02 und werden dich beim Programmieren mit Micro:bit begleiten. Wir sind jetzt zu zweit, weil wir bei diesen Übungen dann Buchstaben an jeweils den anderen Micro:bit senden werden.**

<img width="20%" src="https://github.com/dlpl-mb/baa_morse_code_01/blob/master/images/robo_mbit_funk.gif?raw=1">  <img width="20%" src="https://github.com/dlpl-mb/baa_morse_code_01/blob/master/images/SOS.svg.png?raw=1">  <img width="20%" src="https://github.com/dlpl-mb/baa_morse_code_01/blob/master/images/robo_mbit_funk.gif?raw=1">

Wusstest du, dass ein Micro:bit mit anderen Micro:bit über Funkwellen kommunizieren kann. In diesem Morsecode-Lektion II werden wir nun Nachrichten zwischen 2 Micro:bits versenden. Dazu müssen wir einige Vereinbarungen treffen, damit die Kommunikation auch funktioniert. Wenn sich etwa Robi-x01 und Robi-x02 in verschiedenen Räumen sind und sich nicht sehen und hören können.

**Die Vereinbarungen sind:**

* **Beim Sender:** Die `|Taste A|` sendet den Morsecode

* **Beim Empfänger:**
  * Dieser Micro:bit wartet nur auf Nachrichten - erhält er eine sso muss diese bestätigt werden.
  * Die `|Taste A|` dient zum Bestätigen der Nachricht (in unserem Programm wird ein Plus gesendet) - erst dann darf der Sender den nächsten Buchstaben senden
  * Die `|Taste B|` sendet ein Minus `-` - damit erkennt der Sender, dass noch einmal gesendet werden muss!
  * Natürlich könnt ihr euch beim Programmieren eigene Kommunikationsvereinbarungen treffen

## Die Zeichen des Morsealphabets (zum Nachschlagen und Ausdrucken)

<img width="100%" src="https://github.com/dlpl-mb/baa_morse_code_01/blob/master/images/morse-tab.png?raw=1">

Drucke Dir die Tabelle aller Morsecodes aus (Rechte Maustaste - Bild kopieren und dann mit Word ausdrucken)

### Übersichtlichkeit

Damit unser Demonstrationsprogramm übersichtlich bleibt, arbeiten wir weiter mit der Buchstabenliste von 9 Buchstaben (A bis G, nun auch das S und O), später, wenn das Programm fertig ist, werden wir alle Zeichen einbauen.

<img width="50%" src="https://github.com/dlpl-mb/baa_morse_code_01/blob/master/images/l2_prg_bst.png?raw=1">

* Fügt man mehrere Morsezeichen zu einem Wort zusammen, muss beachtet werden, dass nach jedem Morsebuchstaben ein Leerplatz bzw. ein Pause eingelegt wird, damit der Empfänger weiß, dass nun ein neues Wort beginnt.
* Sieht dir dieses kurze Morsewort an: ... --- ...
* Es besteht aus drei Buchstaben - finde die Buchstaben heraus! 
* Dieses wichtigste Morse-Worte solltest du dir merken - es ist für Notfälle gedacht:
* SOS ("save our ship"): drei kurz, drei lang, drei kurz: ... --- ...
* Beachte dabei, dass nach jedem Buchstaben **dreimal kurz** (S) ein kurze Pause gemacht wird und erst dann **dreimal lang** (Buchstabe O) gesendet wird.
* Wenn man das nun weiter denkt, so ist natürlich auch das Satzende wichtig. Dort fällt die Pause noch länger aus (etwa 1 Sekunde)
* Schreibt auf Papier, wie nun das folgende Wort heißen kann:  <img src="https://github.com/dlpl-mb/baa_morse_code_01/blob/master/images/anna.png?raw=1">

## Programmcode 1: Verbindung von 2 Micro:bits

Um nachher Morsecodes und Buchstaben senden zu können, müssen zwei Micro:bit **verbunden** werden - arbeite auch hier mit deinem Partner/deiner Partnerin zusammen.

### Grundregeln zur Verbindung von 2 Micro:bit sind

* Wählt einen Funkkanal von 1 bis 255 aus - kein anderes Spielpaar im Raum darf denselben Kanal verwenden, sonst gibt es Kommunikationssalat
* Wir wählen für diese Beispiel **99** (bedenkt: einen noch freien Funkkanal verwenden)
* Jetzt muss abgemacht werden, wer ist **Sender** und wer ist **Empfänger**:
* Es muss auch genau vereinbart werden, `wann soll gesendet werden`, `wie reagiert der Empfänger` mit seinem Mirco:bit, ...
* Das ist deshalb wichtig, weil später in getrennten Räumen gearbeiten wird und die sprachliche Verständigung nicht mehr möglich ist.
* Beide Micro:bits nun über denselben Funkkanal verbinden - siehe ``||radio: radio.setGroup(1)||``
* Beide Partner können in unserem Beispiel dasselbe Programm auf dem jeweiligen Micro:bit benutzen.

```blocks
radio.setGroup(99)
```

### Der erster Test zur Übertragung

* Wir werden mit `Taste A` senden und mit `Taste B` immer antworten.
* **Die Aufgabenstellung heißt:**
  * Der Sender sendet den Buchstaben **A**
  * Der Empänger zeigt den erhaltenen Buchstaben an
* Das Programm dazu könnte so aussehen:

```blocks
input.onButtonPressed(Button.A, function () {
    radio.sendString("A")
})
radio.onReceivedString(function (receivedString) {
    basic.showString(receivedString)
})
radio.setGroup(99)
```

* Dann tauscht ihr die Rollen
* Ändert auch die Sendebuchstaben
* Erweitert das Senden auf ein ganzes Wort oder auch einen Satz
* Der Empfänger muss die Nachricht immer lesen und auch bestätigen
* Versucht nun auch einen Morsecode zu senden (also eine Kombination aus Punkten und Strichen)

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
* Eine weitere Variante wäre, der Sender sendet mit `Taste A` und `Taste B` zwei Morsesymbole.

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

<img width="50%" src="https://github.com/dlpl-mb/baa_morse_code_01/blob/master/images/Morseschreiber.jpg?raw=1">

* Zum Abschluss dieses Projektteils nun eine schwierige Aufgabe:
  * Eine ganze Zeile ist zu lesen: Der Vereinfachung halber sind nur die Wortgrenzen mit einem Schrägstrich markiert.
  * [Programmcode **Senden einer Nachrichtenzeile**](https://makecode.microbit.org/_hhVeobX87KwU){:target="_blank"}

* Verwende diesen einfachen Programmcode und ändere die Übertragungsnachricht.
* Was könnte man beim Empfänger noch gestalten, damit dieser mehr Zeit hat zum lesen? Oder die Nachricht noch einmal ansehen kann?
* Diskutiert: Was hat noch nicht gut funktioniert, was ist zu verbeseern?

## Übung: Sendung von verschiedenen Botschaften

* Nehmen wir das obere einfache Programm vom Senden eines Morsezeichens.
* Wenn du einen neuen Morsebuchstaben senden willst, musst du das Sender-Programm immer wieder umschreiben.

### Aufgabe: Sende-Buchstaben per Zufall auswählen

**Lösung a:** Ein Auswahl eines Morsecodes per Zufall

* Man benötigt eine Zufallszahl zwischen 0 und der Anzahl der verfübaren Buchstaben.
* Eine Zufallszahl kann man im Bereich ``|Mathematik|`` erzeugen - der Befehl heißt `Wähle eine zufällige Zahl von 0 bis 10`
* Experimentiere mit der  Zufallsfunktion: Ändere den Wertebereich
* Damit kann man auch das Würfeln mit ienem Spielwürfel simmulieren: Wertebereich 1 - 6

```blocks
input.onButtonPressed(Button.A, function () {
   basic.showLeds(`
      . . . . .
      . . . . .
      . . . . .
      . . . . .
      . . . . .
   `)
   basic.showNumber(randint(0, 10))
})
```

* Überlege warum im Programmcode ein leeres Feld eingebaut wurde
* Wir werden in unserem Programm 26 Buchstaben verwenden - also brauchen wir eine Zufallszahl zwischen 0 und 25.  
* Wir werden mit dem folgenden Testprogramm den Morsecode eines zufälligen Buchstabens senden
* [Programmcode **Zufällige Morsecode senden**](https://makecode.microbit.org/#pub:_1aRd1965T2s5){:target="_blank"}

* Dabei greift man mit dem Befehl ``||array: [liste_morsecodes[zufall]]||`` auf ein Element der Morsecode-Liste zu und zeigt dieses an.
* wie müsste man das Programm änder, damit nicht der Morsecode gesendet wird. sondern ein Buchstabe des Alphabeths.
* Experimentiert weiter mit diesem Befehl.

### Aufgabe: Sende zufällig Morsezeichen - empfange Morsezeichen

* Das zufällig Morsezeichen sollte nicht beim Sender anzeigt werden, sondern auch versendet werden.
* Hier greifen wir auf früheren Programmcode zurück und bauen diesen um.
* [Programmcode **Senden und Empfangen eines zufälligen Morsecodes**](https://makecode.microbit.org/#pub:_F5cKo14UE6oA){:target="_blank"}

## Bestätigung des Empfangs (Fachbegriff: handshake)

* Nun sollte der Empfänger noch Bestätigen, ob der/sie die Nachricht erhalten und verstanden hat.
* Wir wählen für die Antwort die noch freie `Taste B`
* Diese sollte die Nachricht "ok" zurückgeben
* Erst dann darf der Sender wieder eine neue Nachricht senden
* Versucht das einzubauen - das fertig Ergebnis sieht man im nächsten Programmcode.

[Programmcode **Bestätigen des Erhalts der Sendung**](https://makecode.microbit.org/#pub:_6WzcFd4RYfvc){:target="_blank"}

* Eine Zusatzfunktion baut ihr selber noch ein (Micro:bit V2 erforderlich oder ein angeschlossen Kopfhörer):
  * Sobald ein Buchstabe beim Empfänger ankommt, soll eine Ton gespielt werden
  * Genauso, wenn die Antwort bei Sender ankommt, ein Bestätigungston. 

Das waren jetzt die großen Schritte zu einem Sende- und Empfangssystem für Morsezeichen. Nun kann das große Morsezeichen-Training beginnen.

## Erweiterungen und Programmausbau
Ein derartiges Programm kann man fast unendlich erweitern und mit neuen Funktionen versehen - bis hin zu Funktionen bei denen das Empfängerprogramm den Morsecode wieder zurück übersetzt in Buchstaben des Alphabeths. Das wäre dann notwendig, wenn etwas durch Akustik oder durch Lichtsignale über weite Strecken übertragen wird.

## [Aufruf des zweiten Projektteils: Morsecodes versenden](https://dlpl-mb.github.io/baa_morse_code_02)

<style>.page-header {font-size:1rem;height:0vh;padding-top:1.5rem}</style>
<script src="https://makecode.com/gh-pages-embed.js"></script>
<script>makeCodeRender("{{ site.makecode.home_url }}", "{{ site.github.owner_name }}/{{ site.github.repository_name }}");</script>

