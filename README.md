
## Geheimzeichen: Das Morse-Alphabet II
**Halllo, ich bin Robi01 und werde dich beim Programmieren mit micro:bit begleiten. Wir werden bei diesem Projekt nun Morsezeichen zu meiner Freundin Robi02 übertragen.**

<img width="20%" src="https://github.com/dlpl-mb/baa_morse_code_01/blob/master/images/robo_mbit_funk.gif?raw=1">  <img width="20%" src="https://github.com/dlpl-mb/baa_morse_code_01/blob/master/images/SOS.svg.png?raw=1">  <img width="20%" src="https://github.com/dlpl-mb/baa_morse_code_01/blob/master/images/robo_mbit_funk.gif?raw=1">

Wusstest du, dass ein micro:bit mit anderen micro:bit über Funkwellen kommunizieren kann. In diesem Morse-Code-Projekt II werden wir nun den Morsecode zwischen 2 micro:bits versenden. Dazu müssen wir einige Vereinbarungen treffen, damit die Kommunikation auch funktioniert, wenn ich Robi02 nicht sehen und hören kann - etwa, wenn sie sich in einem anderen Raum befindet. Die Vereinbarungen sind:
 * Die Taste A sendet den Morse-Code
 * Die Taste B dient zum Bestätigen der Nachricht 
 * Ein Symbol Herz dient als OK! Dann kann der Sender die nächste Nachricht senden.
 * Ein rauriger Smiley dient als - Nicht OK - bitte noch einmal senden!
 * Natürlich könnt ihr euch beim Programmieren eigene Kommunikationssymbole ausmachen.
 
## Die Zeichen des Morsealphabets
Wir werden nun bereits alle Morsezeichen verwenden, damit ihr auch ordentlich kommunizieren könnt. Diese sind bereits im Programm eingespeilt und ihr könnt damit weiterarbeiten. 
<img width="100%" src="https://github.com/dlpl-mb/baa_morse_code_01/blob/master/images/morse-tab.png?raw=1"> 
**Hier ist der Code mit allen Zeichen:**
```blocks
let morse = [".-","-...","-.-.","-..",".","..-.","--.","....","..",".---","-.-",".-..","--","-.","---",".--.","--.-",".-.","...","-","..-","...-",".--","-..-","-.--","--..",".----","..---","...--","....-",".....","-....","--...","---..","----.","-----"]

let alphabet = ["a","b","c","d","e","f","g","h","i","j","k","l","m","n","o","p","q","r","s","t","u","v","w","x","y","z","1","2","3","4","5","6","7","8","9","0"]
```

```block
basic.showNumber(88)


```


* Wie du aus der Tabelle siehst haben Morsezeichen nur den **Punkte** und den **Striche**. Jeder Buchstabe hat einen bestimmte Kombination von Punkten und Strichen.
* Schreib dir die Buchsstaben ersten ** A bis G ** auf ein Blatt Papier heraus: **Buchstabe** und **Code**
* Beim Übertragen werden zwischen den Buchstaben immer eine kurze Pausenm gemacht, damit der Empfänger weiß, dass nun ein neues Zeichen beginnt.
* Meine Frage an dich: Welcher Buchstabe ist das? -.. oder dieser Buchstabe . 

## Programm 1: Codes anzeigen 

Du baust nun für dem BBC micro:bit ein erstes Programm zum Zeigen der Morse-Codes für A bis G. 

**Die Aufgaben lautet:**

* Taste A des micro:bit zeigt die Buchstaben A bis G (Später nehmen wir alle anderen Buchstaben dazu.)
* Taste B zeigt die Morse-Codes für diese Zeichen an 
* Später wirst du dein Programm so ausgebauen, dass du Codes zu anderen micro:bits übertragen und somit Anderen senden kann.
* Probiere das gleich mit dem Button "Dreieck" aus:
<img width="40%" src="https://github.com/dlpl-mb/baa_morse_code_01/blob/master/images/dreieck.png?raw=1">

```blocks
input.onButtonPressed(Button.A, () => { 
    basic.showString("A");
});

input.onButtonPressed(Button.B, () => { 
    basic.showString(".-");
});
```
* Schreib nun im Programmeditor (Button **Blöcke**) die kurzen Programme für die anderen Buchstaben B bis G.

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


## Fertiges Programm I
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
eyJoaXN0b3J5IjpbMTI2NTY2MDkzNCw5MDE0MDg5MTgsMTI3OT
Q5ODc4MCwxODQ1OTcyOTg0LDE4NzkzMjY1ODFdfQ==
-->