# Proof of Skill - Bäume im Modell

## Szenario
Eine Anwendung verwaltet in Hauptspeicher ein sogenanntes dynamisches Objektmodell, 
d.h. es werden Werte (hier der Einfachheit halber immer Strings) gespeichert,
die irgendwo in einem Baum aufgehängt sind und die fachliche Struktur (Vertrag, Partenr, etc.) 
ist erst zur Laufzeit bekannt, aber nicht während der Programmierung. 

Am Beispiel:

    Vertrag.VSNR = "4711"
    Vertrag.Partner.1.Name = "Wurst"
    Vertrag.Partner.1.Vorname = "Hans"
    Vertrag.Partner.1.Adressen.1.Straße = "Metzgergasse"
    ...
    Vertrag.Partner.2.Name = "Pansa"
    Vertrag.Partner.2.Vorname = "Sancho"
    ...

In diesem Beispiel wird ein Datenmodell mit Entitäten Vertrag, Partner und Adresse dargestellt 
bei dem es durchnummerierte Partner und je Partner durchnummerierte Adressen gibt.

Die Datenmodelle können sehr groß werden (mehrere 10.000 Felder) - deshalb ist eine effiziente Implementierung wichtig.

## Aufgabe

Schreibe eine Java-Klasse oder ein kleines Java-Package, welches die fogend aufgelisteten Funktionen bietet.
Nutze dazu ausschließlich Klassen aus der Java Runtime (JavaSE), keine weiteren Bibliotheken. 

Deine Implementierung soll dabei sicherstellen, dass die Zeit zum Schreiben, Lesen und Löschen eines 
Wertes maximal logarithmisch mit der Anzahl der Elemente im Model wächst, unabhängig von der Struktur des Modells.

### Basis-Funktionsumfang

- Hinzufügen (ggf. überschreiben) eines Wert an einer angegebenen Position
- Löschen eines Wertes
- Löschen einer Entität
- Auslesen eines Wertes über die Pfad _value("Vertrag.Partner.2.Name")_ liefert _"Pansa"_
- Abrufen einer Datenstruktur mit allen Werten einer vorgegebenen Entität, z.B. alle Werte im Objekt Vertrag.Partner.1

### Erweiterter Funktionsumfang

- Implementierung einer Methode Model.visit(Visitor v) zur Navigation über Entitäten und Werte, 
  d.h. Aufruf des Visitor mit 
  - Entität Vertag 
  - Wert Vertrag.VSNR = "4711" 
  - Entität Vertrag.Partner.1 
  - Wert Vertrag.Partner.1.Name = "Wurst" 
  - usw.
- Navigieren über das Datenmodell wobei der Visitor bei jeder Entität steuern kann, ob er sie ignorieren möchte. 
  Falls er sich für Ignorieren entscheidet, dann bekommt er die Werte und Subentitäten nicht mehr zu sehen.
- Implementierung eines Visitor, der aus dem Datenmodell einen langen String mit der Darstellung 
  aus dem Abschnitt "Szenario" macht (Vertrag.VSNR = "4711"\n Vertrag.Partner.1.Name = ...)
