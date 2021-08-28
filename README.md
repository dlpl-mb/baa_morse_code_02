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
[Programmcode](https://makecode.microbit.org/#pub:_DVe8TrKz3cRU "(target|_blank)")

Eingebaut in das Übertragungsprogramm:
* 

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
	liste_buchstaben = ["A","B","C","D","E","F","G"]
	liste_morsecodes = [".-","-...","-.-.","-..",".","..-.","--."]
	anz_bst = liste_buchstaben.length - 1
```














<br>
**Verbesserungen:**

* Taste A des Micro:bit zeigt die Buchstaben A bis G (Später nehmen wir alle anderen Buchstaben dazu.)
* Taste B zeigt die Morse-Codes für diese Zeichen an 
* Später wirst du dein Programm so ausgebauen, dass du Codes zu anderen micro:bits übertragen und somit Anderen senden kann.
* Probiere das gleich mit dem Button "Dreieck" aus:
<img width="40%" src="https://github.com/dlpl-mb/baa_morse_code_01/blob/master/images/dreieck.png?raw=1">

```blocks
input.onButtonPressed(Button.A, function () {
radio.sendString(".- -. -. .-")
})

radio.onReceivedString(function (receivedString) {
basic.showString(receivedString)
})
radio.setGroup(99)
```


```blocks
input.onButtonPressed(Button.A, () => { 
    basic.showString("A");
});

input.onButtonPressed(Button.B, () => { 
    basic.showString(".-");
});
```
* Schreib nun im Programmeditor (Button **Blöcke**) die kurzen Programme für die anderen Buchstaben B bis G.
* Der Sender darf erst dann wieder senden, wenn er/sie vom Empfänger eine Bestätigungsantwort erhalten hat.
## Programm 2: Alle sechs Buchstaben in ein Programm

Zugegeben: Das war ganz schön aufwändig, für jeden Buchstaben immer ein eigenes Programm zu schreiben.
Wir packen nun alles 7 Buchstaben in ein Programm:
* Wir müssen alle sieben Buchtaben in eine Liste hinein bringen
* Dazu gibt es einen besonderen Variablentyp **Array** oder **Liste** 
* Wähle unter ``|Fortgeschritten Arrays|`` und dort ``||array:setze Text_List ...||``
* Ändere den Variablen auf Buchstabenliste
* Vervollständige die Buchstaben von "A" bis "G"

### Speicherung der Buchstaben 

* Um auf ein Element dieser Liste zuzugreifen, muss du den **Index** (Reihungsnummer ) innerhalb der liste angeben.
* Beachte: Eine Liste beginnt in fast allen Programmiersprachen immer mit dem Element Nr. 0, dann 1 bis zum letzten element, das hat dann die Nummer 6 (unsere Liste von A bis G). Das ist sicher sehr gewöhnungsbedürftig - man sollte sich das möglichst schnell angewöhnen und anwenden. 

### Darstellung der Buchstaben 

* Wir benötigen eine Schleife von 0 bis 6
* Innerhalb der Schleife zeigen wir mit einer **Laufvariable** - wir nennen sie hier **index** auf jeweils ein Element.


## Fertiges Programm: Morse-Alphabet II
Du kannst nun am folgenden fertigen Programms noch experimentiert. 
* Verändere Variable und Zeiten
* Beim Experimentieren an fremden Programmen kannst du viel lernen 

```blocks
input.onButtonPressed(Button.A, function () {
    for (let index = 0; index <= anz_bst; index++) {
        basic.showString("" + (liste_buchstaben[index]))
        basic.pause(500)
    }
})
input.onButtonPressed(Button.B, function () {
    for (let index2 = 0; index2 <= anz_bst; index2++) {
        basic.showString("" + (liste_buchstaben[index2]))
        basic.showString("" + (liste_morsecodes[index2]))
        basic.pause(2000)
        basic.clearScreen()
    }
})
let anz_bst = 0
let liste_morsecodes: string[] = []
let liste_buchstaben: string[] = []
basic.showIcon(IconNames.Yes)
liste_buchstaben = [
"A",
"B",
"C",
"D",
"E",
"F",
"G"
]
liste_morsecodes = [
".-",
"-...",
"-.-.",
"-..",
".",
"..-.",
"--."
]
anz_bst = liste_buchstaben.length - 1
```
#### Metadaten
<script src="https://makecode.com/gh-pages-embed.js"></script><script>makeCodeRender("{{ site.makecode.home_url }}", "{{ site.github.owner_name }}/{{ site.github.repository_name }}");</script>



> Diese Seite bei [https://dlpl-mb.github.io/baa_morse_code_02/](https://dlpl-mb.github.io/baa_morse_code_02/) öffnen

> Öffne das Teilprogramm [Programmabschnitt](https://makecode.microbit.org/#pub:_Ux2V81PmkYMM)

<a href="https://makecode.microbit.org/#pub:_Ux2V81PmkYMM" target="_blank">Hello, world!</a>



[Test mit Blanklink funktionierend](https://makecode.microbit.org/_buWXjXMYkKop){:target="_blank"}

[Test mit neulink2](https://makecode.microbit.org/#pub:_Ux2V81PmkYMM){target="_blank"}

[Link 4](https://makecode.microbit.org/#pub:_Ux2V81PmkYMM "title" target="_blank")

[Go to this page](https://makecode.microbit.org/#pub:_Ux2V81PmkYMM?target=_blank)

[Page Link](https://makecode.microbit.org/#pub:_Ux2V81PmkYMM "(target|_blank)")
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEyMDk1NzMzMjcsLTg2ODM2ODEyMSwxND
U2MzU0MDI5LDE1MTY0MjcyMjcsLTE2MjI2MDIyNjAsMTY0MDAz
NzY2Miw1NTA4MTk0NjAsMTA2MTk1NTcxNCwtNzI3NTY2MzE5LC
0xNjkyNDMyMzQ2LC0yNzA1NzcyNzgsLTE4OTE2NzY4MSwtNjc1
MDgxOTE3LC0xOTA3MDAxMjg1LDEyMTAxMDU4MzcsNjQ2NjQyNj
g4LDE2NDEyMDY1OTMsMTQ2NjMxNTg0NywtMTY2NjQzNzE5MSwt
MjMyNzY3MDUwXX0=
-->