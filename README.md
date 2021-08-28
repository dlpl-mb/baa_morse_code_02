<style>.page-header {font-size:1rem;height:10vh;padding-top:1.5rem}</style>

## Geheimzeichen: Das Morse-Alphabet II
**Hallo, ich bin Robi01 und werde dich beim Programmieren mit micro:bit begleiten. Wir werden bei diesem Projekt nun Morsezeichen zu meiner Freundin Robi02 übertragen.**

<img width="20%" src="https://github.com/dlpl-mb/baa_morse_code_01/blob/master/images/robo_mbit_funk.gif?raw=1">  <img width="20%" src="https://github.com/dlpl-mb/baa_morse_code_01/blob/master/images/SOS.svg.png?raw=1">  <img width="20%" src="https://github.com/dlpl-mb/baa_morse_code_01/blob/master/images/robo_mbit_funk.gif?raw=1">

Wusstest du, dass ein micro:bit mit anderen micro:bit über Funkwellen kommunizieren kann. In diesem Morse-Code-Projekt II werden wir nun den Morsecode zwischen 2 micro:bits versenden. Dazu müssen wir einige Vereinbarungen treffen, damit die Kommunikation auch funktioniert, wenn ich Robi02 nicht sehen und hören kann - etwa, wenn sie sich in einem anderen Raum befindet. Die Vereinbarungen sind:
 * Die Taste A sendet den Morse-Code
 * Die Taste B dient zum Bestätigen der Nachricht 
 * Ein Symbol Herz dient als OK! Dann kann der Sender die nächste Nachricht senden.
 * Ein rauriger Smiley dient als - Nicht OK - bitte noch einmal senden!
 * Natürlich könnt ihr euch beim Programmieren eigene Kommunikationssymbole ausmachen.
 
## Die Zeichen des Morsealphabets
 
<img width="100%" src="https://github.com/dlpl-mb/baa_morse_code_01/blob/master/images/morse-tab.png?raw=1"> 
Drucke Dir die Tabelle aller Morsecodes aus (Rechte Maustaste - Bild kopieren und dann mit Word ausdrucken)

Wir werden nun bereits alle Morsezeichen verwenden, damit ihr auch gut kommunizieren könnt. Diese sind bereits im Programm eingespielt und ihr könnt damit weiterarbeiten.

**Hier ist der Code mit allen Zeichen:**
* Einige Zeichen hast du ja im ersten Teil diese Projektes schon verwendet - hier nun alle Zeichen.  Untersuche, dass genau jene Zeichen, die in unserer Sprache oft verwendet werden, sehr kurze Morsekombinationen haben und andere, seltene Zeichen längere Morsesymbole.

let liste_buchstaben = 
["A","B","C","D","E","F","G","H","I","J","K","L","M","N","O","P","Q","R","S","T", "U","V","W","X","Y","Z","1","2","3","4","5","6","7","8","9","0"]

let liste_morsezeichen = [".-","-...","-.-.","-..",".","..-.","--.","....","..",".---","-.-",".-..","--","-.","---",".--.","--.-",".-.","...","-","..-","...-",".--","-..-","-.--","--..",".----","..---","...--","....-",".....","-....","--...","---..","----.","-----"]

```block
let liste_buchstaben = ["A","B","C","D","E","F","G","H","I","J","K","L","M","N","O","P","Q","R","S","T","U","V","W","X","Y","Z","1","2","3","4","5","6","7","8","9","0"]

let liste_morsezeichen = [".-","-...","-.-.","-..",".","..-.","--.","....","..",".---","-.-",".-..","--","-.","---",".--.","--.-",".-.","...","-","..-","...-",".--","-..-","-.--","--..",".----","..---","...--","....-",".....","-....","--...","---..","----.","-----"]
```

* Eines der wichtigsten Symbole solltest du die in Zukunft merken - es ist für Notfälle gedacht: 
* SOS (save our ship): drei kurz, drei lang, drei kurz - ... --- ... 
* Beachte dabei, dass nach **drei kurz** ein kurze Pause ist, ebenso nach den nächsten Buchstaben.
* Versuche nun das Wort **???** mit Hilfe der Tabelle zu bauen:  <img src="https://github.com/dlpl-mb/baa_morse_code_01/blob/master/images/anna.png?raw=1">

## Programm 1: Verbinden von 2 micro:bit

Um Daten senden zu können, müssen zwei micro:bit mit einigen Programmzeilen verbunden werden.
**Grundregeln dazu sind:**
* Wähle mit deinem/r Kommunikationspartner/in eine Funkkanal von 1 bis 255 aus - niemand anderer im Raum darf denselben verwenden, sonst gibt es Kommunkationssalat - in unserem Beispiel 99
* Es muss genau definiert werden, wer ist Sender und wer ist Empfänger: Es muss ausgemacht werden, wann soll der Empfänger sich melden - wie soll er sich melden.
* Beide micro.bit müssen über denselben Funkkanal verfügen - siehe ``||radio: radio.setGroup(1)||``
 ```blocks
	radio.setGroup(99)
 ```
* **Abmachung:** 
* Wir werden mit `|Taste A|` senden und mit Taste B immer antworten

* Folgendes Programm soll nun auf beiden micro:bit programmiert werden:

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
* Ladet das Programm auf eure beiden micro:bit und macht erste Tests
* Schreibt auf, was noch nicht gut funktioniert


**Die Aufgaben lautet:**

* Taste A des micro:bit zeigt die Buchstaben A bis G (Später nehmen wir alle anderen Buchstaben dazu.)
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

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTI3NDU3ODE1NSwxOTUxMjM4ODUxLC02NT
g3MzQ4MDUsMjEzMDEzMDkwNyw0MzEzMjg2NTYsNTQ2NTU4OTUs
LTE5OTgwMjIyMjEsMjEwNDgxMDQwNiwxNDg5MDk0Mzk3LDE3Mz
UxMzM5MCw1Njk0MzUxOTQsMjI3MjA1OTE0LDEyNTA2NTYwNTks
MTQyMzQ2ODI3MCw5MDE0MDg5MTgsMTI3OTQ5ODc4MCwxODQ1OT
cyOTg0LDE4NzkzMjY1ODFdfQ==
-->