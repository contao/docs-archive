## Markdown

Markdown ist eine einfache Auszeichnungssprache, die es erlaubt, Text mittels
einfachem Syntax zu formatieren. Markdown hat den Vorteil, einfach lesbar
zu sein und automatisch in HTML konvertiert werden zu können.

Nachfolgend einige Beispiele für die Markdown-Syntax:

### Syntax

#### Paragrafen

Absätze werden durch eine Leerzeile erstellt:

    Erster Absatz

    Zweiter Absatz 


#### Überschriften

Es sind sechs Ebenen für Überschriften möglich:

    # Überschrift 1
    ## Überschrift 2
    ### Überschrift 3
    #### Überschrift 4
    ##### Überschrift 5
    ###### Überschrift 6


#### Wichtig

Um wichtigen Text zu markieren:

    **strong**
    __strong__

Wird zu folgendem HTML-Code konvertiert: `<strong>strong</strong>`


#### Hervorhebung

Um Text hervor zu heben:

    *emphasize*
    _emphasize_

Wird zu folgendem HTML-Code konvertiert: `<em>emphasize</em>`


#### Code

Um einen Text als Computercode zu markieren:

    `monospaced font`

Wird zu folgendem HTML-Code konvertiert: `<code>monospaced font</code>`


##### Code-Blöcke

Um einen ganzen Absatz in Code zu konvertieren, den Text mit vier
Leerzeichen einrücken.

        Schrift mit fester Laufweite ...
        ... über mehrere Zeilen


#### Zitat-Block

Zitatblöcke können durch eine rechte spitze Klammer am Beginn der
Zeile erstellt werden.

    > Dies ist ein Zitat.


#### Zeilenumbruch

Durch zwei oder mehr Leerzeichen am Ende einer Zeile wird ein Umbruch erzeugt:

    Contao ist ein barrierefreies Open Source  
    content management system.


#### Links

Es gibt zwei Möglichkeiten für Links: **inline** und **als Referenz**.

Ein Inline-Link sieht wie folgt aus:

    [Contao](https://contao.org/de)

oder optional auch mit einem Titel:

    [Contao](https://contao.org/de "Offizielle Contao-Webseite")

Ein Referenz-Link sieht wie folgt aus:

    [Offizielle Contao-Webseite][1]
    
    [1]:https://contao.org/de

Die Referenz kann an beliebiger Stelle im Dokument platziert werden.


#### Bilder

Wie für Links gibt es auch für Bilder zwei Syntax-Möglichkeiten.

Ein Inline-Bild sieht wie folgt aus:

    ![Alt text](/pfad/zum/bild.jpg "Optionaler Titel")

Ein Bild im Referenz-Stil wird durch folgende Syntax erreicht:

    ![Alternativer Text][id]

    [id]: /pfad/zum/bild.jpg "Optionaler Titel"

Die Referenz kann an beliebiger Stelle im Dokument platziert werden.


#### Aufzählungslisten

##### Unsortierte Listen

Unsortierte Listen verwenden Sternzeichen oder Trennstriche:

    * Listeneintrag  
    * Listeneintrag  
        * Verschachtelter Listeneintrag
        * Verschachtelter Listeneintrag
    * Listeneintrag

    - Listeneintrag  
    - Listeneintrag  
    - Listeneintrag


##### Sortierte Listen

Sortierte Listen verwenden Zahlen:

    1. Listeneintrag  
    2. Listeneintrag  
    3. Listeneintrag


### Erweiterter Syntax

Nicht alle HTML-Element wie beispielsweise Tabellen oder Fußnoten können
mit normalem Markdown beschrieben werden. Aus diesem Grund gibt es ein
Projekt für "Markdown Extra" um die Syntax zu erweitern.

Nachfolgend einige Beispiele für die erweiterte Syntax:


#### Tabellen

Eine Tabelle kann wie folgt erstellt werden:

```
Erste Kopfzeile | Zweite Kopfzeile | Dritte Kopfzeile  
--------------- | ---------------- | ----------------  
Zelleninhalt    | Zelleninhalt     | Zelleninhalt  
Zelleninhalt    | Zelleninhalt     | Zelleninhalt  
```

Die Textausrichtung kann durch Doppelpunkte gesteuert werden:

```
Erste Kopfzeile | Zweite Kopfzeile | Dritte Kopfzeile  
:-------------- | :--------------: | ---------------:  
Linksbündig     | Zentriert        | Rechtsbündig  
Linksbündig     | Zentriert        | Rechtsbündig  
```


#### Fußnoten

Fußnoten werden wie folgt erstellt:

    Dies ist ein Text mit Fußnote.[^1]

    [^1]: Und dies ist die Fußnote.

Die Fußnoten-Definition kann an beliebiger Stelle im Dokument platziert werden.


### Weitere Informationen

Für eine komplette Dokumentation zu Markdown, besuchen Sie die offizielle
Webseite unter folgendem [Link][1].

Für eine komplette Dokumentation zu Markdown Extra, besuchen Sie die
offizielle Webseite unter folgendem [Link][2].


[1]: http://daringfireball.net/projects/markdown/syntax
[2]: http://michelf.ca/projects/php-markdown/extra
