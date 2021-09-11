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
* Diskutiert auf, was noch nicht gut funktioniert hat

## Übung: Sendung von verschiedenen Botschaften

* Nehmen wir das obere einfache Programm vom Senden eines Morsezeichens.
* Wenn du einen neuen Morsebuchstaben senden willst, musst du das Sender-Programm immer wieder umschreiben.

### Unser Ziel: Man möchte den Sende-Buchstaben per Zufall auswählen lassen

**Lösung a:** Ein Auswahl eines Morsecodes per Zufall

* Man benötigt eine Zufallszahl zwischen 0 und der Anzahl der verfübaren Buchstaben.
* Eine Zufallszahl kann man im Bereich `Mathematik` erzeugen - der Befehl heißt `Wähle eine zufällige Zahl von 0 bis 10`
* Experimentiere mit der  Zufallsfunktion:

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

* Dabei greift man mit dem Befehl ``||Arrays: [liste_morsecodes[zufall]]||`` auf ein Elment der Morsecode-Liste zu und zeigt dieses an.






* [Programmcode 4](https://makecode.microbit.org/#pub:_DVe8TrKz3cRU){:target="_blank"}

Eingebaut in das Übertragungsprogramm:

* Nun wird der Zufallsgenerator in der `Taste A-Funktion` eingebaut:

```blocks
input.onButtonPressed(Button.A, function () {
	index = randint(0, anz_bst)
	auswahl_buchstabe = liste_buchstaben[index]
	// damit siehst du als Sender den Buchstaben auch auf deinem Display
	basic.showString("" + (auswahl_buchstabe))
	radio.sendString("" + (liste_morsecodes[index]))
})
radio.onReceivedString(function (receivedString) {
	// Beim Emfänger werden die empfangenen Daten angezeigt
	basic.showString(receivedString)
})
input.onButtonPressed(Button.B, function () {
	for (let index2 = 0; index2 <= anz_bst; index2++) {
		basic.showString("" + (liste_buchstaben[index2]))
		basic.showString("" + (liste_morsecodes[index2]))
		basic.pause(2000)
		basic.clearScreen()
	}
})
let auswahl_buchstabe = ""
let index = 0
let anz_bst = 0
let liste_morsecodes: string[] = []
let liste_buchstaben: string[] = []
radio.setGroup(99)
// liste_buchstaben = ["A","B","C","D","E","F","G","S","O"]
// liste_morsecodes = [".-","-...","-.-.","-..",".","..-.","--.","...","---"]
anz_bst = liste_buchstaben.length - 1
```

* [Programmcode 3](https://makecode.microbit.org/---codeembed#pub:_VE2dfFHrwDi9){:target="_blank"}

**Lösung b:** Wir bauen eine Auswahltastatur

* Bei dieser Lösung arbeiten wir mit dem Neigungswinkel in Richtung x - eine sehr leistungsfähige Funktion, mit der man viele Spiele gestalten kann.
* Probiere folgende Funktion als Übung und notiere dir einige Werte
* Wichtig ist hier, den Micro:bit nach links und Recht zu kippen:

<img src="https://github.com/dlpl-mb/baa_morse_code_01/blob/master/images/mbit_li_re_x.png?raw=1">

```blocks
input.onButtonPressed(Button.A, function () {
	basic.showNumber(input.acceleration(Dimension.X))
})
```

[Programmcode 4](https://makecode.microbit.org/#pub:_55zbeHhRTa2o){:target="_blank"}

* Immer wenn `Taste A` gedrückt wird, zeigt es den augenblicklichen Kippwinkel (x) an.
* Spiele das Programm auf den Micro:bit und teste.
* Auch dieses folgende Sequenz zeigt dir den Kippwinkel x (links-Rechts) an - aber hier werden ständig neue Winkelwerte angezeigt, dadurch entstehen sehr viele Zahlen, ...
  
```blocks
basic.forever(function () {
	basic.showNumber(input.acceleration(Dimension.X))
})
```

* Beobachte dabei die x-Werte - wir wollen diese Neigung ausnutzen, um später in den Buchstaben zu `blättern`. 
* Experimentiere nun mit der folgenden Funktion zum Hinauf- und Herunterzählen einer Zahl (bitte auf den Micro.bit spielen) - hier sind bereits viele Funktionen beteiligt.

```blocks
let index = 5
let neigung = 0
basic.forever(function () {
	neigung = input.acceleration(Dimension.X)
	if (neigung > 300) {
		index += 1
	}
	if (neigung < -300) {
		index += -1
	}
	basic.showNumber(index)
	basic.pause(1000)
})
```

[Programmcode 5](https://makecode.microbit.org/#pub:_UXKHMAL1pFWp){:target="_blank"}

* Hier lässt sich sehr gut beobachten, wie man die Sensoren (Beschleunigungs- und Lagesensor) nutzen kann, um Messwerte zu verwenden.
* Damit sind nun die Voraussetzungen geschaffen, die Hilfstastatur (Auswahltastatur) zu testen.

```blocks
input.onButtonPressed(Button.A, function () {
	radio.sendString("" + (auswahl_morsecode))
})
let auswahl_buchstabe = ""
let index = 0
let neigung = 0
let auswahl_morsecode = ""
//liste_buchstaben = ["A","B","C","D","E","F","G","S","O"]
//liste_morsecodes = [".-","-...","-.-.","-..",".","..-.","--.","...","---"]
let anz_bst = liste_buchstaben.length - 1
basic.forever(function () {
	neigung = input.acceleration(Dimension.X)
	if (neigung > 300) {
		index += 1
	}
	if (neigung < -300) {
		index += -1
	}
	if (index > anz_bst) {
		index = 0
	}
	if (index < 0) {
		index = anz_bst
	}
	auswahl_buchstabe = liste_buchstaben[index]
	auswahl_morsecode = liste_morsecodes[index]
	basic.showString("" + (auswahl_buchstabe))
	basic.pause(500)
})
```

[Programmcode 5](https://makecode.microbit.org/---codeembed#pub:_PHiaYDfFzD83){:target="_blank"}

+ Teste bei diesem Teilprogramm vor allem die Auswahltastatur
+ Erst wenn diese Funktionen "verdaut" sind - hat es Sinn das gesamte Programm anzusehen.

## Fertiges Programm: Das Morse-Alphabet II
Das fertige Programmgerüst enthält jetzt die wichtigsten Funktionen, damit du zu deinem Spielpartner alle Morsezeichen versenden kannst. Wenn dein Partner/deine Partner das Zeichen gelesen und verstanden hat, wird von dort mit der `Taste B` ein `+` zurückgeschickt.

* Das fertig kleine Übertragungsprogramm für alle Morsezeichen
  
```blocks
input.onButtonPressed(Button.A, function () {
	radio.sendString("" + (auswahl_morsecode))
})
input.onButtonPressed(Button.AB, function () {
	ich_bin_sender = 1
})
radio.onReceivedString(function (receivedString) {
	basic.showString(receivedString)
})
input.onButtonPressed(Button.B, function () {
	radio.sendString("+")
	ich_bin_sender = 0
})
let ich_bin_sender = 0
let auswahl_buchstabe = ""
let index = 0
let neigung = 0
let auswahl_morsecode = ""
basic.showIcon(IconNames.Yes)
/*
let liste_buchstaben = ["A","B","C","D","E","F","G","H","I","J","K","L","M","N","O","P", "Q","R","S","T","U","V","W","X","Y","Z","1","2","3","4","5","6","7","8","9","0"]
let liste_morsecodes = [".-","-...","-.-.","-..",".","..-.","--.","....","..",".---","-.-",".-..","--","-.","---",".--.","--.-",".-.","...","-","..-","...-",".--","-..-","-.--","--..",".----","..---","...--","....-",".....","-....","--...","---..","----.","-----"]
*/
let anz_bst = liste_buchstaben.length - 1
radio.setGroup(99)
basic.forever(function () {
	if (ich_bin_sender == 1) {
		neigung = input.acceleration(Dimension.X)
		if (neigung > 300) {
			index += 1
		}
		if (neigung < -300) {
			index += -1
		}
		if (index > anz_bst) {
			index = 0
		}
		if (index < 0) {
			index = anz_bst
		}
		auswahl_buchstabe = liste_buchstaben[index]
		auswahl_morsecode = liste_morsecodes[index]
		basic.showString("" + (auswahl_buchstabe))
		basic.pause(500)
	}    
})
```

## Reflexion und Erweiterung

In dritten Teil diese Projektes werden nun einzelne Erweiterungen  und Verbesserungen vorgenommen, die mit weiteren neuen Funktionen erreicht werden. Versuche nun selber Funktionen zu entdecken und zu testen - es werden im dritten Teil nur mehr wenige Kommentare gegeben.

* Überlege, welche Erweiterungen/Vereinfachung du hier noch machen möchtest
* Man könnte mit mehreren Empfängern kommunizieren.

**Viel Erfolg auf dem Weg zur kompetenten Programmiererin/zum kompetenten Programmierer.**

**Abschlussbemerkung:**
Der Autor dieses Morse-Beispielprogramms ist selbst seit Jahren Programmierer in einigen Programmiersprachen und kann feststellen, dass er dann am meisten gelernt hat, wenn er fremde Programme analysiert hat und versucht hat, sie zu verstehen und mit kleinen schrittweisen Änderungen alles Unbekannte zu verstehen.

**Neue Funktionen werden sein:**
* Erweiterte Kommunikation zwischen Sender und Empfänger
* Senden von ganzen Wörtern
* Senden von akustischen Signalen

## [Der fertige Programmcode](https://makecode.microbit.org/---codeembed#pub:_8tqijz37gTMw){:target="_blank"}

<br>

## Programmbedienung

<img width="20%" src="https://github.com/dlpl-mb/baa_morse_code_01/blob/master/images/robi_mb.png?raw=1">  Sender und Empfänger <img width="20%" src="https://github.com/dlpl-mb/baa_morse_code_01/blob/master/images/robi_mb.png?raw=1">

* Nach dem Start sehen beide Micro:bit gleich aus
* Nun muss abgemacht werden, wer nun bei diesem Spiel **Sender** ist:
  * Nur der **Sender** drückt dazu beide `|Tasten A+B|` -> nun weiß das System, wer sendet und wer empfängt
* Der **Empfänger** sollte bisher nur warten

### Der Sender

* Jetzt kann der **Sender** durch `||Links-und-rechts-Neigen||` des Micro:bit einen Buchstaben wählen
  * Ist der zu sendende Buchstabe gefunden, wird der Micro:bit wieder waagrecht gehalten und es kann der Buchstabe abgeschickt werden - mit `|Taste A|`
* Es wird dann der Morsecode des Buchstaben an den Empfänger gesendet und dort angezeigt.

### Der Empfänger

* Der **Empfänger** sieht nun das Morsezeichen und sucht über die Morse-Tabelle den richtigen Buchstaben, schreibt diesen auf ein Blatt Papier und gibt Bescheid, ob der Buchstabe erkannt wurde:
  * `|Taste A|` bedeutet: Morsezeichen **erkannt**
  * `|Taste B|` bedeutet: **Nicht erkannt** - bitte noch einmal senden
* Diese Antwort erhält der **Sender** auf sein Micro:bit Display (+ oder-)
* Führt einmal 5 Durchgänge durch und wechselt dann ihr die Rollen.

**Rollen tauschen** (immer in Abstimmung mit dem Partner/der Partnerin)

* Wie wird ein neues Spiel gestartet?
* Bei beiden Micro:bit die `|Reset-Taste|` (Rückseite des Micro.bit) drücken
* Dann den Sender neu bestimmen mit `|Taste A+B|`
* Erfindet selber neue Spielregeln dazu
* Natürlich kann man den Micro:bit auch umprogrammieren:
  * Dabei ist wichtig, dass man im Team die Regeln bespricht.

<img width="20%" src="https://github.com/dlpl-mb/baa_morse_code_01/blob/master/images/robo_mbit_funk.gif?raw=1">  <img width="20%" src="https://github.com/dlpl-mb/baa_morse_code_01/blob/master/images/SOS.svg.png?raw=1">  <img width="20%" src="https://github.com/dlpl-mb/baa_morse_code_01/blob/master/images/robo_mbit_funk.gif?raw=1">
# !!! Danke für eure Mitarbeit !!!

<style>.page-header {font-size:1rem;height:0vh;padding-top:1.5rem}</style>
<script src="https://makecode.com/gh-pages-embed.js"></script>
<script>makeCodeRender("{{ site.makecode.home_url }}", "{{ site.github.owner_name }}/{{ site.github.repository_name }}");</script>


* Es wäre gut, könnte man den Buchstaben auswählen
* es fehlt leider eine Tastatur auf dem Micro:bit zum Eingeben eines neuen Buchstabens).
  * Wie könnte man aus den Buchstaben auswählen?
	a) Entweder durch Zufallsgenerator oder
	b) mit einer virtuellen (=gedachten) Tastatur

<hr>
