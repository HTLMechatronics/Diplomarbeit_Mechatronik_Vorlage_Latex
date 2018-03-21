# Diplomarbeit Mechatronik Vorlage LaTeX

## Installation

### Windows

+ Miktex Download: https://miktex.org/download
+ Texmaker Download: http://www.xm1math.net/texmaker/download.html
+ JabRef Download: https://www.fosshub.com/JabRef.html

### Ubuntu

+ Miktex Installation

```sh
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys D6BC243565B2087BC3F897C9277A7293F59E4889
echo "deb http://miktex.org/download/ubuntu xenial universe" | sudo tee /etc/apt/sources.list.d/miktex.list
sudo apt update
```

```sh
sudo apt install miktex
```

Schritte auf dieser Website befolgen um Installation abzuschließen: https://miktex.org/howto/install-miktex-unx

+ Texmaker Installation:

```sh
sudo apt install texmaker
```

+ JabRef Installation

```sh
curl -O https://www.fosshub.com/JabRef.html/JabRef-4.1.jar
```

### Generell

1. Miktex updaten
2. Texmaker starten und _main.tex_ übersetzen (alle Pakete installieren lassen)
  + Mehrmals übersetzen
  + Wennn nach 3, 4 Durchgängen immer noch ein Fehler ist, Meldung anschauen (oft hilft Miktex noch einmal nach updates checken)
3. _opening.tex_ anpassen
4. Diplomarbeiten aufteilen in eigene _*.tex_ Files
  + Mit `\include{name}` (ohne Dateiendung) wird das File inkludiert
  + Wenn mehrere am selben Dokument arbeiten sollte man nur sein eigenes File inkludieren, sonst dauert das Bauen ewig und das Geeschriebene ist oft weit hinten im Dokument.

### Dateien

+ __main.tex__: Hauptfile mit Präambel (eng: preamble) - Übersetzen nur in diesem File. `\begin{document}` `\end{document}` sind in dieser Datei - Zone die den kompletten Inhalt enthält. Titel wird hier erzeugt und die anderen _*.tex_ Files werden hier eingebunden. 
+ __opening.tex__: Einleitung der Diplomarbeit (Danksagung, Eidestattliche Erklärung, ...)
+ __appendix.tex__: Anhänge
+ __listings.tex__: Codestyles

### Zitierung

Setup:

+ Im Texmaker: Optionen --> Texmaker konfigurieren --> Reiter: Befehle, bei Bib(la)tex: _biber %_ eingeben
+ Danach: Schnell Übersetzen - BibTeX - Schnell Übersetzen (2x)

Zietieren mit `\cite{buchname}` oder als Fußnote: `\footfullcite{buchname}`

Bücher einfügen in der Datei _Literaturverzeichnis.bib_ (Buchtypen: https://en.wikibooks.org/wiki/LaTeX/Bibliography_Management)

### Akronyme

Abkürzungsverzeichnis in der _appendix.tex_.
In der Zone acronym (\begin{acronym}...\begin{acronym}) werden die Abkürzungen definiert.

```tex
\begin{acronym}
  %Abkürzung hinzufügen: \acro{Kürzel}{Ausgeschrieben}
  \acro{WLAN}{Wireless Local Area Network}
  \acro{WWW}{World Wide Web}
  \acro{uC}[µC]{Mikrocontroller}
\end{acronym}
```

Abkürzungen im Text: `\ac{kürzel}`

### Code Listings

Code innerhalb \begin{lstlisting}..\end{lstlisting}.
Mögliche Optionen:

+ __style:__ Vorher definierter Style (case sensitive)
+ __language:__ Sprache des Codes (case sensitive)
+ __caption:__ Name des Listings
+ __label:__ Label zum Verweisen

Wenn style oder language angegeben ist, muss das andere nicht angegeben werden. Reihenfolge der Optionen ist egal.

```tex
\begin{lstlisting}[style=java,caption=Java Codebeispiel,label=cCode]
  ...
\end{lstlisting}
```

Styles werden definiert in _listings.tex_. Am besten man fragt [Onkel Google](https://google.com) oder liest in der [Dokumentation](http://users.ecs.soton.ac.uk/srg/softwaretools/document/start/listings.pdf) nach. In lstlisting sind folgende Sprachen bereits vordefiniert:

+ C
+ C++
+ HTML
+ Java
+ make
+ Matlab
+ Perl
+ PHP
+ Python
+ SQL
+ TeX
+ XML
+ und viele mehr (siehe [Dokumentation](http://users.ecs.soton.ac.uk/srg/softwaretools/document/start/listings.pdf))

Alle weiteren Sprachen müssen mit `\definelanguage{}` definiert werden. Dazu entweder die [Dokumentation](http://users.ecs.soton.ac.uk/srg/softwaretools/document/start/listings.pdf) lesen, oder [Onkel Google](https://google.com) fragen.

### Aufzählungen

Aufzählungen funktionieren unter LaTeX mit der Zone _itemize_ oder _enumerate_

```tex
\begin{itemize}
  \item Standartmäßig ist ein schwarzer Punkt davor.
  \item Die Länge ist nicht von Bedeutung, Zeilen werden automatisch umgebrochen.
\end{itemize}
```

```tex
\begin{enumerate}
  \item Zählt automatisch.
  \item Kann auch genestet werden.
\end{enumerate}
```

Weitere Informationen in der [Dokumentation](https://www.sharelatex.com/learn/Lists).

### Bilder

Es gibt zwei Arten, wie man Bilder einfügt. Entweder über die ganze Seite, oder mit Textumfluss.

#### Ganze Seite

```tex
\begin{figure}[H]
  \includegraphics[width=1\textwidth]{Dateiname_Ohne_Endung}
  \caption{Name des Bildes}
  \label{Verweis}
\end{figure}
```

In den eckigen Klammern in der ersten Zeile kann man LaTeX mitteilen, wo man sein Bild plaziert haben möchte. H bedeutet _here_ platziert das Bild genau dort, wo es im Text steht. Weitere Informationen dazu in der [Dokumentation](https://www.sharelatex.com/learn/Positioning_of_Figures).

#### Textumfluss

```tex
\begin{wrapfigure}{r}{0.6\textwidth}
\vspace{10pt}
  \begin{center}
    \includegraphics[width=0.55\textwidth]{Dateiname_Ohne_Endung}
  \end{center}
  \caption{Name des Bildes}
  \label{Verweis}
  \vspace{-10pt}
\end{wrapfigure}
```

In der zweiten geschwungenen Klammer in der ersten Zeile gibt man ann, ob man das Bild links (l) oder rechts (r) platziert haben möchte. In der dritten geschwungenen Klammer gibt man die gewünschte Breite des Bildes an. Diese sollte gleich groß oder größer sein, wie die in Zeile 4. Mit dem `\vspace{}` Befehl kann man Abstände vor und nach dem Bild anpassen.

### Verweise

Ein Verweis in LaTeX erfolgt immer auf ein `\label{}`. Deswegen ist es wichtig, dass alle Überschriften, Bilder etc. Labels haben. Zum Verweisen kann man den Befehl `\ref{}` oder den Befehl `autoref{}` verwenden. Bei Ersterem wird nur die Nummerierung dargestellt, beim Anderen auch zusätzlich Abbildung oder Abschnitt.

### Tabellen

[Onlinegenerator](http://lmgtfy.com/?iie=1&q=Latex+Table+Generator)