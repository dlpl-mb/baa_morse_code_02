<style>.page-header {font-size:1rem;height:10vh;padding-top:1.5rem}</style>
## Geheimzeichen: Das Morse-Alphabet II
**Hallo, ich bin Robi01 und werde dich beim Programmieren mit Micro:bit begleiten. Wir werden bei diesem Projekt nun Morsezeichen zu meiner Freundin Robi02 übertragen.**

<img width="20%" src="https://github.com/dlpl-mb/baa_morse_code_01/blob/master/images/robo_mbit_funk.gif?raw=1">  <img width="20%" src="https://github.com/dlpl-mb/baa_morse_code_01/blob/master/images/SOS.svg.png?raw=1">  <img width="20%" src="https://github.com/dlpl-mb/baa_morse_code_01/blob/master/images/robo_mbit_funk.gif?raw=1">

Wusstest du, dass ein Micro:bit mit anderen Micro:bit über Funkwellen kommunizieren kann. In diesem Morse-Code-Projekt II werden wir nun den Morsecode zwischen 2 micro:bits versenden. Dazu müssen wir einige Vereinbarungen treffen, damit die Kommunikation auch funktioniert, wenn ich Robi02 nicht sehen und hören kann - etwa, wenn sie sich in einem anderen Raum befindet. Die Vereinbarungen sind:
 * Die Taste A sendet den Morse-Code
 * Die Taste B dient zum Bestätigen der Nachricht 
 * Ein Symbol Herz dient als OK! Dann kann der Sender die nächste Nachricht senden.
 * Ein rauriger Smiley dient als - Nicht OK - bitte noch einmal senden!
 * Natürlich könnt ihr euch beim Programmieren eigene Kommunikationssymbole ausmachen.
 
## Die Zeichen des Morsealphabets
 
<img width="100%" src="https://github.com/dlpl-mb/baa_morse_code_01/blob/master/images/morse-tab.png?raw=1"> 
Drucke Dir die Tabelle aller Morsecodes aus (Rechte Maustaste - Bild kopieren und dann mit Word ausdrucken)

**Wir arbeiten aus Gründen der Übersichtlichkeit weiter mit der Trainingsliste von 9 Buchstaben, später, wenn das Programm fertig ist, werden wir alle Zeichen verwenden**
```
let liste_buchstaben = ["A","B","C","D","E","F","G","S","O"]
let liste_morsezeichen = [".-","-...","-.-.","-..",".","..-.","--.","...","---"]
```
* Eines der wichtigsten Morse-Worte solltest du  merken - es ist für Notfälle gedacht: 
* SOS ("save our ship"): drei kurz, drei lang, drei kurz - ... --- ... 
* Beachte dabei, dass nach jdem Bustaben **"dreimal kurz"** (=S) ein kurze Pause gemacht wird und erst dann **"dreimal lang"** (=O) gesendet wird. Später wird noch wichtig, dass nach einem gesamten Wort ebenso eine längere Pause (etwa 1 Sekunde) gemacht wird.
* Schreibt auf Papier, wir nun das folgende Wort heißt:  <img src="https://github.com/dlpl-mb/baa_morse_code_01/blob/master/images/anna.png?raw=1">

## Programmteil 1: Verbindung von 2 micro:bit

Um nachher Morsecodes und Buchstaben senden zu können, müssen zwei Micro:bit durch ein kurzes Programm verbunden werden - suche dir also eine zweite Person als Kontaktpartner. Arbeitet zu zweit weiter.
**Grundregeln dazu sind:**
* Wähle mit deinem/r Kommunikationspartner/in einen Funkkanal von 1 bis 255 aus - niemand anderer im Raum darf denselben verwenden, sonst gibt es Kommunikationssalat - in unserem Beispiel wählen wir **99**.
* Es muss genau definiert werden, wer ist **Sender** und wer ist **Empfänger**: Es muss auch genau vereinbart werden, wann soll gesendet werden, wann meldet sich der Empfänger.
* Beide micro.bit müssen über denselben Funkkanal verfügen - siehe ``||radio: radio.setGroup(1)||``
* Beide Partner können in unserem Beispiel auch dasselbe Programm auf den Micro:bit spielen.
 ```blocks
	radio.setGroup(99)
 ```
<br>

**Der erster Test zur Übertragung:** 
* Wir werden mit `Taste A` senden und mit `Taste B` immer antworten. 
* Was heißt die Aufgabenstellung? 
	* Der Sender sendet einmal den Buchstaben A und den dazugehörigen Morsecode
	* Der Empfänger bekommt den Morsecode angezeigt und muss den empfangenen Morsecode in den Buchstaben übersetzen.
	* Programmtechnik: wir benötigen aus dem Menü `Funk` zwei Befehle:
		* Daten senden: `radio: radio.sendString("A")`
		* Daten empfangen: `radio: radio.onReceivedString(function (receivedString))`
	* Der Empfänger sollte die Papierliste zum Entschlüsseln verwenden

* Folgendes Programm soll nun auf beiden Micro:bit programmiert werden, damit könnt ihr schon einmal einige Tests machen. 
```blocks
	input.onButtonPressed(Button.A, function () {
		basic.showString("A") //damit siehst du als Sender den Buchstaben auch auf deinem Display
		radio.sendString(".-")
	})
	radio.onReceivedString(function (receivedString) {
		basic.showString(receivedString) // Beim Emfänger werden die empfangenen Daten angezeigt
	})
	radio.setGroup(99)
```
[Programmcode](https://makecode.microbit.org/_3dh6h5JKqHkJ "(target|_blank)")

* Schreibe das Programm auf eure beiden Micro:bit (oder wählt Programmcode) und macht erste Tests
* Tausch die Rollen des Senders und Empfängers
* Achtet unbedingt darauf, dass nicht andere Gruppen in eurem Raum denselben Kommunikationskanal benutzen
* * Schreibt auf, was noch nicht gut funktioniert

**Verbesserungsüberlegungen:**
* Wenn du einen neuen Buchstaben senden will, musst du das Sender-Programm immer umschreiben.
* Es wäre gut, könnte man den Buchstaben auswählen (es fehlt leider eine Tastatur auf dem Micro:bit zum Eingeben eines neuen Buchstabens).
 - Wie könnte man aus den Buchstaben auswählen?
	- a) Entweder durch Zufallsgenerator oder 
	- b) mit einer virtuellen (=gedachten) Tastatur
<hr>

**Lösung a:** Ein Auswahl eines Buchstabens per Zufall
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
* Überlege auch warum ein leeres Feld eingebaut wurde
* [Der Programmcode](https://makecode.microbit.org/#pub:_DVe8TrKz3cRU "(target|_blank)")

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
	liste_buchstaben = ["A","B","C","D","E","F","G","S","O"]
	liste_morsecodes = [".-","-...","-.-.","-..",".","..-.","--.","...","---"]
	anz_bst = liste_buchstaben.length - 1
```
* [Der Programmcode](https://makecode.microbit.org/---codeembed#pub:_VE2dfFHrwDi9 "(target|_blank)")

<hr>

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

[Programmcode](https://makecode.microbit.org/#pub:_55zbeHhRTa2o "(target|_blank)")
- Immer wenn `Taste A` gedrückt wird, zeigt es den augenblicklichen Kippwinkel (x) an. 
- Spiele das Programm auf den Micro:bit und teste.
- Auch dieses folgende Sequenz zeigt dir den Kippwinkel x (links-Rechts) an - aber hier werden ständig neue Winkelwerte angezeigt, dadurch entstehen sehr viele Zahlen, ...
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
[Programmcode](https://makecode.microbit.org/#pub:_UXKHMAL1pFWp "(target|_blank)")
+ Hier lässt sich sehr gut beobachten, wie man die Sensoren (Beschleunigungs- und Lagesensor) nutzen kann, um Messwerte zu verwenden.
+ Damit sind nun die Voraussetzungen geschaffen, die Hilfstastatur (Auswahltastatur) zu testen.
 
```blocks
	input.onButtonPressed(Button.A, function () {
	    radio.sendString("" + (auswahl_morsecode))
	})
	let auswahl_buchstabe = ""
	let index = 0
	let neigung = 0
	let auswahl_morsecode = ""
	liste_buchstaben = ["A","B","C","D","E","F","G","S","O"]
	liste_morsecodes = [".-","-...","-.-.","-..",".","..-.","--.","...","---"]
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
[Programmcode](https://makecode.microbit.org/---codeembed#pub:_PHiaYDfFzD83 "(target|_blank)")
+ Teste bei diesem Teilprogramm vor allem die Auswahltastatur
+ Erst wenn diese Funktionen "verdaut" sind - hat es Sinn


<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE1MTU5ODQzNDEsMTQzMjc5NjM2OSwtMT
ExNDU0MzI4MSw1NjA4NjkxMjAsLTE3MDU0NzI3NiwtNDA5MDYz
NDk0LC01NzkyNjc0NDIsLTk2NjgzNTU5Nyw1NDYzOTg0OTEsLT
g2ODM2ODEyMSwxNDU2MzU0MDI5LDE1MTY0MjcyMjcsLTE2MjI2
MDIyNjAsMTY0MDAzNzY2Miw1NTA4MTk0NjAsMTA2MTk1NTcxNC
wtNzI3NTY2MzE5LC0xNjkyNDMyMzQ2LC0yNzA1NzcyNzgsLTE4
OTE2NzY4MV19
-->