# Frontendinator

Framework zur Unterstützung für 
* Draft - statische HTML Version
* Dokumentation
* Integration in ein CMS
* Report

## Anforderungen

* Einfach zu benutzen (nodejs, java)
* generiert keinen Unsinn 
* Developmentstand kommt dem Produkt sehr nah
* Generierung 
    * Draft
    * UI Metainformation wie UI Pattern 
    * CMS Integrationsinformationen
    * Template (Vorlagen für Integration)
    * Konzeptionelle Informationen (welche Module ineinander gesteckt werden können etc.)
* schneller, einfacher Developmentcycle
* Flexibel in Formaten und Plugins (z. B. Bildformate, JS Frameworks, ...)
* Unabhängig 
    * vom Zielsystem: Liferay, FirstSpirit, Magnolia, OpenText, OpenCMS, etc.
    * vom Zielformaten: HTML, FTL, VM, FirstSpirit, JSP, JSF, ...
* Informationen liegen nah beieinander
    * z.B. Template mit CSS mit JS inkl. Namensraum
    * Tempalte benötigt CSS und JS, dann sind sie dabei oder was da liegt, wird eingebunden
* Dependency Management 
    * CSS (Bootstrap, Grid, Mixins, ...)
    * JS (JQuery, Angular, Polymer, JQuery Plugins...)
* Developmentstruktur entspricht 1:1 dem Zielsystem
    * Es kann sein, dass im Draft Dateien angelegt werden, die nur für ein Ziel notwendig sind (sei es Draft oder CMS)

## Base/ Core
* Dateibaum einlesen
* Metainformationen einlesen
* Generierung Exporte

## File Struktur

Alle Dateien sollen auch direkt mit einem Editor bearbeitbar sein. Dh. der Server merkt sich nur den 
Dateibaum, der Rest wird live gelesen.

* Datei mit Metadaten (json oder yaml)
    * By naming conventions "file.suffix" with meta data "file.suffix.json"
    * Zielformat kann beliebig gewählt werden (Generell pro Dateityp und Speziell pro Datei überschrieben)
    * Informationen
        * Zieldateityp
        * Integrationsinformationen 
* resources/: images...
* css/: css, sass, less
* js/: js, coffeescript, typescript
    * Minify
    * Dependeny Management
    * Zusammenfassen von mehreren Dateien, wenn gewollt
* content/: json struktur mit daten und benutzten templates
* templates/
    * groovy? mit include, loop, output
        * Jedes mit einem eigenen Generierungstemplate für die Zielformate
    * pageTemplates (Seite), contentTemplates (Elemente), tinyTemplates (Blöcke)


## Export (generiert nur Export - Aufruf durch Main Klasse)
* export/index -> 
    * Übersicht (geführt und generisch)  
    * statistische Informationen
        * Anzahl und Bytes
    * Version (Nummer und Abstimmung) 
    * Datum der Generierung sowie Abstimmungsdatum
* export/uiPattern -> übersicht aller Templates mit Metainformationen
* export/draft -> statischer Dienst
* export/templates -> Templates in entsprechender Sprache (vm, ftl, jsp, ...)

## Development (Lokaler Server für direkte Ansicht)
* Filesystem-Listener für Änderungen
* Dateien werden erst generiert und dann durch den lokalen Webserver ausgegeben
* Frontend zuschaltbare Meta-Information
    * Javascript mit Websockets um automatisch ein Reload durchzuführen, sofern eine Änderung der dargestellten Elemente durchgeführt wurde
    * Alles leicht veränderbar -> Dateien liegen alle im Sourcecode vor (JSP?)
* UI Pattern übersicht kann eingesehen werden
    * Titel
    * Beschreibung
    * Tabs
        * Codeblock
        * Less
        * ...
        * Eventuell

## Report
* Bilder
    * Größenangaben
    * Übersicht der Formate 
    * Übersicht der Größenangaben und wo sie benutzt werden
    * Vorschlag für Optimierungen
        * Versuch durch direkte Generierung mit Preview (Analog ImageReady)
        * jpg (in verschiedenen %-Stufen), png (8 und 16), gif (bei Animation), webm (Animation)

## Technologie
* bower etc. für Dependencies
* Einstellungen für besondere Befehle (was nicht in Java existiert): sass, coffeescript, ....
* kumuluzEE für lokalen Server
* Eventuell MAVEN als Basis für
    * Server Komponenten
    * Webjars 
        ```XML
        <dependency>
            <groupId>org.webjars</groupId>
            <artifactId>angularjs</artifactId>
            <version>1.4.8</version>
        </dependency>
        ```

## Notizen
* Server (lokale Entwicklung)
    * springBoot
    * kumuluzEE https://ee.kumuluz.com
* Frontendinator Templates in JSP oder Groovy
* Information (entweder oder)
    * JSON
    * YAML
        * http://yamlbeans.sourceforge.net
    * HOCON
        * https://github.com/typesafehub/config
        * https://github.com/typesafehub/config/blob/master/HOCON.md
 