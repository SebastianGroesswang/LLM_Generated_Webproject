# Webtechnologie Projekt Sebastian Grösswang

## Einleitung

In dieser Abgabe für das Fach Web3 soll eine Webanwendung mithilfe von LLMs gescriptet werden. Die verwendetet LLMs sind hier frei wählbar und sollen fest in den Arbeitsablauf integriert werden. Da in der Angabe der Aufbau des Webprojekt als <i>klassisch</i> definiert wird, wird davon ausgegangen das das Webprojekt mit Plain HTML und Bootstrap gebaut werden soll. Diese Dokumentation wird in den einzelnen Abschnitten:
* Planung
* Implementierung
* Tests
aufgeteilt. Für das Projekt soll hauptsächlich nur eine LLM verwendet werden - in diesem Projekt wird auf den Github CoPilot Model: GPT-5 mini gesetzt. Dies ist aufgrund der Schülerlizenzfreien Pro Version und der direkten Einbindung in die Entwicklerumgebung. Für den Vergleich wird eine Unterseite als Duplikat angelegt und Gemini wird als LLM verwendet. 

## Planung

Die generelle Planung für so ein kleines Projekt gibt es in der Hinsicht nicht, meiner Meinung nach. Die größte Frage besteht hierbei mit welcher Datensammlung man arbeitet.
In diesem Projekt wurde entschieden mit der `SWAPI Reborn` API zu arbeiten. Diese API beinhaltet verschiedene Restabfragen zu verschiedenen Star Wars Themen. Bei der Suche nach einer API war der größte Fokus darauf zu setzen dass es eine Detailabfrage existiert - sonst wäre die Detailseite schwer zu bauen. Ohne LLM wäre mein Vorgehen folgendes:

1. Indexseite: Erstellen - dann Testen
2. Übersichtseite erstellen: Erstellen - dann Testen
3. Detailseite erstellen: Erstellen - dann Testen
4. Formularseite erstellen: Erstellen dann Testen

Zum Vergleich stelle ich die Angabe in ChatGPT (Besserer Verwendung mit externen PDFs) und lass im einen Planungsvorschlag erstellen.

```
Q: Wie würdest du für diese Angabe die Implementierung planen? Es wurde schon entschieden mit welcher API gearbeitet wird.

A: 

Gut, dann können wir die Planung sehr konkret auf die Umsetzung zuschneiden. Ich würde die Implementierung inkrementell und funktionsorientiert planen, sodass jede Ausbaustufe lauffähig ist und gleichzeitig sauber dokumentiert werden kann.

Im Folgenden eine bewährte Implementierungsplanung, exakt auf diese Angabe optimiert.

Grundprinzip der Planung

Eine Funktionseinheit nach der anderen

Nach jedem Schritt:

testen

Screenshot

LLM-Interaktion dokumentieren

Kein „Big Bang“ am Ende

Phase 0 – Projekt-Setup (sehr wichtig, oft unterschätzt)

Ziel: Saubere Basis, keine Chaos-Struktur.

Implementieren:

Ordnerstruktur festlegen, z.B.:

/css
  style.css
/js
  api.js
  overview.js
  detail.js
  form.js
index.html
overview.html
detail.html (oder Modal)
form.html


Gemeinsame Navigation (kopiert oder per JS geladen)

Basis-CSS (Layout, Tabelle, Buttons)

👉 LLM-Einsatz:
„Schlage mir eine sinnvolle Projektstruktur für ein kleines Vanilla-JS-Webprojekt vor.“

Phase 1 – API-Anbindung isoliert entwickeln

Ziel: API verstehen, bevor UI gebaut wird.

Implementieren:

In api.js:

fetchAll() → Liste der Datensätze

fetchById(id) → Detaildaten

postData(data) → POST (oder httpbin)

Fehlerbehandlung:

try/catch

Statuscodes prüfen

👉 Noch keine UI!
Erst console.log(data).

👉 LLM-Einsatz:
API-Auswertung, JSON-Struktur erklären lassen.

Phase 2 – Übersichtsseite (Kernstück)

Ziel: Funktionale Übersicht mit echtem Mehrwert.

Implementieren:

Seite lädt → fetchAll()

Relevante Attribute filtern

Dynamische Tabelle erzeugen:

thead

tbody

Jede Zeile klickbar:

speichert ID

leitet zur Detailseite weiter oder öffnet Modal

👉 Hier empfehle ich den LLM-Vergleich

LLM A: Tabellen-Rendering

LLM B: alternative Umsetzung

Du entscheidest bewusst

📌 Diese Phase bringt viele Punkte (Übersicht + Dokumentation + Vergleich).

Phase 3 – Detailansicht

Ziel: Klare Trennung Übersicht ↔ Details.

Implementieren:

ID aus URL oder Event übernehmen

fetchById(id) aufrufen

Daten strukturiert anzeigen:

Listen

Abschnitte

Fallback:

„Datensatz konnte nicht geladen werden“

👉 UI erst einfach, kein Overengineering.

👉 LLM-Einsatz:
Strukturierung komplexer JSON-Daten.

Phase 4 – Formularseite (POST)

Ziel: Funktionales Formular, nicht nur optisch.

Implementieren:

Formularfelder passend zu Detaildaten

Client-seitige Validierung

Submit:

Daten sammeln

POST-Request senden

Response anzeigen:

Erfolg

Fehler

👉 Falls echte API kein POST erlaubt → httpbin.org/post.

👉 LLM-Einsatz:
Validierungsregeln, UX-Feedback.

Phase 5 – Fehlerbehandlung & Robustheit

Ziel: Punkte bei den Testfällen sichern.

Implementieren:

API nicht erreichbar:

Benutzerfreundliche Meldung

Leere Antwort

Ungültige ID

Formular mit leeren Feldern

👉 Diese Phase spart dir später viel Stress bei den Tests.

Phase 6 – Tests & Screenshots

Ziel: Systematisch statt improvisiert.

Vorgehen:

Pro Seite:

Normalfall

Fehlerfall

Tests manuell durchspielen

Screenshots sofort machen

Kurz notieren:

Was wurde getestet

Erwartetes Ergebnis

Tatsächliches Ergebnis

👉 LLM-Einsatz:
Testfall-Ideen + Edge-Cases.

Phase 7 – Finalisierung

Ziel: Abgabereife.

Checkliste:

Alle Seiten von index.html erreichbar

Keine toten Links

Keine Konsolenfehler

Ordner sauber

ZIP korrekt benannt

Test unter:

Chrome

Firefox

Windows-Pfadstruktur

Empfohlene Implementierungs-Reihenfolge (kurz)

Projektstruktur

API-Funktionen

Übersicht

Detail

Formular

Fehlerfälle

Tests & Screenshots

ZIP bauen

Warum diese Planung gut zur Angabe passt

Jede Teilanforderung wird isoliert erfüllt

LLM-Einsatz ist nachvollziehbar und gezielt

Dokumentation entsteht parallel

Kein Risiko, am Ende etwas Wesentliches zu vergessen

Wenn du willst, können wir als nächsten Schritt:

die konkreten Funktionen (Signaturen) definieren oder

die Übersichtsseite Schritt für Schritt implementieren (inkl. sinnvollen LLM-Prompts).

```

Meiner Meinung nach schlägt ChatGPT immer schon eine gute Planung vor welcher auch schon sehr Detailreich ist. Hier ist natürlich die Frage ob das nicht den ganzen Spaß am Coden wegnimmt - natürlich ist sie aber effizienter. Besonders finde ich hier die Abkapselung der API Abfragen spannend. Diese sind für so ein kleineres Projekt unnötig und können in den einzelnen Seiten implementiert werden. Daher wird auf den Vorschlag von ChatGPT verzichtet.

## Implementierung

Kleine Info vorab. Da für die Implementierung mit Github Copilot - Edit gearbeitet wird, wird der Code direkt verändert und in der Ausgabe wird nur eine Zusammenfassung der Änderung bereitgestellt für eine leichtere Ansicht werde ich dieses Projekt auf Github hochladen und für jede Änderung der LLM wird ein Commit gemacht und hier an der Ausgabe mit dem direkten Link angehängt.

### Indexseite

Hierbei starte ich mit der Indexseite für eine grundlegende Basis wurde diese Prompt formultiert:

```
Q: Erstelle mir ein neues HTML Dokument index.html - welche responsive ist und folgende Elemente beinhaltet: Einen Titel abschnitt - "Star Wars Character Selektor" und einen Abschnitt welcher die generelle Seite beschreibt - Inhalt ist nur platzhalter - Auch soll eine Sektion eingefügt werden mit dem Titel "Verwendung von LLMs in diesem Projekt" danach gibt es eine Beschreibung die zurzeit nur mit Lorem Ipsum gefüllt werden soll.

A:
Lösung — Schritte:


Erstelle ein neues responsives HTML-Dokument mit Meta-Viewport und semantischen Sektionen.
Füge ein graues Theme per eingebettetem CSS hinzu (zentrale Breite, Karten-Stil, responsive Typografie).
Implementiere die drei geforderten Sektionen: Titel, allgemeine Beschreibung (Platzhalter) und "Verwendung von LLMs in diesem Projekt" mit Lorem Ipsum.
Dateiänderungen — gruppiert nach Datei:

index.html

Kurze Zusammenfassung: Neue responsive Indexseite mit grauem Theme und den drei gewünschten Abschnitten.
```

Die einzelnen Textboxen werden am Ende des Projektes verändert - um als erstes alles von der KI generieren zu lassen. Was jetzt schon auffällt ist das Problem, dass die einzelnen CSS Definitionen direkt im File definiert werden. Um diese für andere Files erreichbar zu machen schiebe ich diese Elemente in ein anderes File. Auch fällt mir auch das die KI nicht Bootstrap verwendet obwohl Bootstrap in diesem Projekt schon installiert wurde. Im dies direkt zu ändern wird folgende Anfrage an die LLM gestellt:

```
Q: Verwende für das gesamte Projekt die installierte Bootstrap Version und lösche dann nicht benötigte extra CSS Definitionen

A: Lösung — Schritte (kurz):


Entferne das eingebettete, umfangreiche CSS.
Binde die lokal installierte Bootstrap‑CSS und -JS ein (node_modules).
Nutze Bootstrap-Komponenten (container, card, utilities) für Layout, Typo und Farben.
Belasse nur minimale Inline‑Styles für globale Hintergrundfarbe, alles andere über Bootstrap.
Änderungen nach Datei:
index.html
Kurze Zusammenfassung: Ersetze das vorherige HTML/CSS durch eine Bootstrap-basierte, responsive Seite. Entfernte überschüssige CSS‑Definitionen; Layout und Typografie werden jetzt durch Bootstrap gesteuert. Lokale Bootstrap-Dateien werden eingebunden.
```

Nach dem erneuten Öffnen wird gleich bemerkt, dass die verwendete Bootstrap Versionen nicht erreichbar ist (Zeile 9). Der Fehler wurde mit reiner menschlicher Kraft behoben und es wurde der richtige Pfad angegeben.

Als nächstes möchte ich eine Navbar einfügen mit den einzelnen Links und direkt die einzelnen HTML Dokumente erstellen.

```
Q: Füge mir eine passende Navbar ein - auf der linken Seite soll noch Platz für ein kleines Star Wars Logo sein und die Navbar soll auf der rechten Steite einen Link zu folgenden Seiten besitzten (Erstelle gleich für jeden Link ein HTML Dokument mit nur den Namen als Inhalt) "Übersicht Copilot", "Übersicht ChatGPT", "Erschaffe deinen eigenen Character"

Der Erscahffe Link sollte hierbei gehighlited werden.

A:Lösung — Schritte (kurz):


Navbar in index.html einfügen: links Platz für kleines Star Wars-Logo, rechts drei Links; der "Erschaffe..."-Link wird als hervorgehobener Button gestylt.
Drei neue HTML-Dateien anlegen, je eine für jeden Link mit nur dem Seitennamen als Inhalt.
Links in der Navbar auf die neuen Dateien setzen. Bootstrap bleibt eingebunden wie im Projekt.
Änderungen nach Datei: index.html

Kurze Zusammenfassung: Navbar oberhalb des bestehenden Inhalts ergänzt; Links zu den drei neuen Seiten hinzugefügt; "Erschaffe deinen eigenen Character" als hervorgehobener Button.

uebersicht-copilot.html
Kurze Zusammenfassung: Neue Seite mit nur dem Seitennamen als Inhalt.

uebersicht-chatgpt.html
Kurze Zusammenfassung: Neue Seite mit nur dem Seitennamen als Inhalt.

erschaffe-deinen-eigenen-charakter.html
Kurze Zusammenfassung: Neue Seite mit nur dem Seitennamen als Inhalt; Ziel-Link in Navbar ist hervorgehoben.
```

Auf den ersten Blick fallen mir folgende Fehler:
* die Navbar wird bei einem kleineren Bildschirm collapsed und kann mit dem Burgerbutton angezeigt werden - die Anzeige funktioniert nicht
* Das highliten des Create Buttons wird nur während dem Hover Effekt angezeigt

Der zweite Fehler wurde ohne Hilfe von LLM gelöste beim ersten wurde folgende Frage an die LLM gesendet:

```
Q: die Navbar wird bei einem kleineren Bildschrim nur collapsed aber der Toggle funktioniert nicht


A:
Wahrscheinliche Ursache: das Bootstrap-JS wird im Browser nicht geladen (häufig, weil node_modules nicht per HTTP erreichbar). Prüfe die Console / Network-Tab. Lösung: entweder das Bundle per CDN einbinden oder die Datei in einen öffentlich erreichbaren Ordner (z.\ B. ./js) kopieren.
Kurz erklärt: das folgende Snippet bindet das offizielle Bootstrap-Bundle per CDN ein und bietet einen lokalen Fallback, falls das CDN nicht geladen werden kann.

`
<!-- html -->
<!-- CDN (schneller Fix) -->
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/js/bootstrap.bundle.min.js"></script>

<!-- Optional: lokaler Fallback (kopiere node_modules/bootstrap/dist/js/bootstrap.bundle.min.js nach ./js/) -->
<script>
  if (typeof bootstrap === 'undefined') {
    var s = document.createElement('script');
    s.src = './js/bootstrap.bundle.min.js';
    document.head.appendChild(s);
  }
</script>
`
```

In der Console wurden auch dann verschiedene Error sichtbar die alle mit den quickfix behoben worden sind - Dabei wird aber nicht mehr die lokale Bootstrap Version verwendet und die lokale Version wurde dann gelöscht im Directory.

Für die Implementierung wurden hier alle benötigten Elemente eingebaut und es fehlen nur noch Inhaltliche Texte die gesondert eingefügt werden. 

### Übersichtseite Github Copilot

Für diese Aufgabe werden die LLMs verglichen - diese Seite wird mit CoPilot generiert. Für den ersten Schritt möchte die gleiche Navbar mit dem Logo und der Möglichkeit wieder zur Homeseite zu kommen

```
Q: Erstelle mir für diese Seite die Gleiche Navbar wie in index nur mit den Unterschied das in der Navbar nur das Logo ist und der Link zurück zur Home zu bekommen, also index.html

A: Lösung — Schritte:


Navbar-Markup oben in die vorhandene Datei einfügen (Bootstrap-Navbar).
Link/Logo links platzieren (verweist auf index.html), rechts einen einfachen Link zurück zur Startseite hinzufügen.
Sicherstellen, dass das vorhandene Bootstrap-Stylesheet und bestehende Styles beibehalten werden.
Änderungen nach Datei: üebrsicht-copilot.html

Kurze Zusammenfassung: Navbar oben ergänzt — links Logo (verweist auf index.html), rechts ein Link "Home" zurück zu index.html. Bestehende Styles bleiben erhalten.
```

Leider wurde hierbei nicht die Navbar im dunklen Design verwendet wie in der Index.html sonst passt alles.

```
Q: Auf dieser Seite möchte ich nun eine Tabelle bekommen aus den Daten dieses API Calls https://swapi.info/api/people In Tabelle möchte ich nur folgende Daten eines Eintrages sehen: name, heigt, birth_year, a link to the homeworld und einen link mit dem Titel Details welcher noch nicht gesetzt wird

A: Lösung — Schritte:


Tabelle im vorhandenen Inhalt ergänzen (Bootstrap-Card + responsive table).
Mit Fetch die API https://swapi.info/api/people abrufen, Daten parsen und Zeilen für name, height, birth_year, Homeworld-Link und einen noch nicht gesetzten "Details"-Link erzeugen.
Ladezustand (Spinner) und Fehlerbehandlung anzeigen. Minimaler XSS-Schutz über eine escape-Funktion.
Änderungen nach Datei: übersicht-copilot.html

Kurze Zusammenfassung: Ergänzung einer Bootstrap-Tabelle und eines kleinen Skripts, das die SWAPI-Daten lädt und darstellt.
```

Hier gibt es eine Error Meldung in der Console. Wie funktioniert der Call nicht gewollt und der Server gibt eine Fehlermeldung zurück. Um dieses Problem zu lösen wurde ein Beispiel der Docs der LLM übermittelt

```
Q:fetch("https://swapi.info/api/people") .then((res) => res.json()) .then((json) => console.log(json)) .catch((error) => console.error(error))

ändere die script block auf diesen Call dein Vorschlag funktioniert nicht


A: Lösung — Schritte:


Ersetze den fehlerhaften Script‑Block durch eine saubere Fetch‑Kette (then/catch), wie vom Nutzer vorgegeben.
Nutze das geladene JSON, um die Tabellenzeilen zu bilden (name, height, birth_year, Homeworld-Link, Details‑Button).
Behalte einfachen XSS‑Escape und Fehleranzeige bei.
Änderungen nach Datei:

C:\Users\sgroe\Documents\FH\3. Semester\Webtechnologie\Webtechnologie Projekt\LLM_Generated_Webproject\uebersicht-copilot.html

Kurze Zusammenfassung: Ersetze den bestehenden fehlerhaften Script‑Block durch eine funktionierende Fetch‑then‑Kette, die die API aufruft und die Tabelle füllt.
```

Mittels console log konnte überprüft werden das die Daten richtig ankommen. Bisher können sie aber nicht nicht richtig verarbeitet werden. Hierbei konnte die LLM den Response nur falsch einschätzen und der Fehler wurde schnell behoben.

### Übersichtseite Gemini

Um einen guten Vergleich zu schaffen, bekommt ChatGPT genau den gleichen Anfangsstand wit CoPilot.

```
Q: <!doctype html> <html lang="de"> <head> <meta charset="utf-8"> <meta name="viewport" content="width=device-width,initial-scale=1"> <title>Übersicht Copilot</title> <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.8/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-sRIl4kxILFvY47J16cr9ZwB07vP4J8+LH7qKQnuqkuIAvNWLzeN8tE5YBujZqJLB" crossorigin="anonymous"> <link href="style.css" rel="stylesheet"> <style>body { background: #f2f3f5 }</style> </head> <body> <div class="container py-5"> <h1>Übersicht Copilot</h1> </div> </body> </html> Ich benötige für dieses HTML Script ein paar Änderungen: Erstelle mir für diese Seite eine bootstrap Navbar die auf der linken Seite ein Starwars Logo bekommnt und noch einen zweiten link erhält mit der man zurück zu index.html kann

A: Das ist ein guter Startpunkt für deine Seite. Um die Navigation hinzuzufügen, nutzen wir die Standard-Bootstrap-Navbar-Komponente.

Hier sind die spezifischen Änderungen für deinen Code:

Navbar-Struktur: Ich habe einen dunklen Hintergrund (navbar-dark bg-dark) gewählt, da dies gut zum Star Wars-Thema passt.

Logo: Ich habe einen Platzhalter für das Star Wars Logo eingefügt. Du kannst dort die URL zu deinem eigenen Bild einsetzen.

Link zur Startseite: Ein einfacher Link, der auf index.html verweist.

Aktualisierter HTML-Code
HTML

<!doctype html>
<html lang="de">
<head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width,initial-scale=1">
    <title>Übersicht Copilot</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
    <style>
        body { background: #f2f3f5; }
        .navbar-brand img { height: 40px; } /* Größe des Logos anpassen */
    </style>
</head>
<body>

    <nav class="navbar navbar-expand-lg navbar-dark bg-dark mb-4">
        <div class="container">
            <a class="navbar-brand" href="#">
                <img src="https://upload.wikimedia.org/wikipedia/commons/6/6c/Star_Wars_Logo.svg" alt="Star Wars Logo">
            </a>
            
            <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav">
                <span class="navbar-toggler-icon"></span>
            </button>

            <div class="collapse navbar-collapse" id="navbarNav">
                <ul class="navbar-nav ms-auto">
                    <li class="nav-item">
                        <a class="nav-link" href="index.html">Zurück zur Startseite</a>
                    </li>
                </ul>
            </div>
        </div>
    </nav>

    <div class="container py-5">
        <h1>Übersicht Copilot</h1>
        <p>Willkommen auf der Copilot-Übersichtsseite.</p>
    </div>

    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>
</body>
</html>
Was wurde genau gemacht?
navbar-brand: Hier sitzt das Logo. Ich habe eine offizielle SVG-Vorschau von Wikipedia als Platzhalter genutzt.

ms-auto: Diese Bootstrap-Klasse ("margin-start: auto") sorgt dafür, dass die Navigations-Links auf die rechte Seite geschoben werden, während das Logo links bleibt.

Responsivität: Der navbar-toggler sorgt dafür, dass das Menü auf dem Smartphone zu einem "Burger-Menü" zusammengeklappt wird.

Bootstrap Version: Ich habe die URL auf die stabile Version 5.3.0 korrigiert, da in deinem Snippet ein kleiner Tippfehler in der Integritätsprüfung vorliegen könnte.

Soll ich die Farben der Navbar noch weiter anpassen, zum Beispiel in einem spezifischen "Jedi-Blau" oder "Sith-Rot"?

```

Technisch gesehen funktioniert alles der Vergleich kommt erst später.

```
Q: Auf dieser Seite möchte ich nun eine Tabelle bekommen aus den Daten dieses API Calls https://swapi.info/api/people In Tabelle möchte ich nur folgende Daten eines Eintrages sehen: name, heigt, birth_year, a link to the homeworld und einen link mit dem Titel Details welcher noch nicht gesetzt wird

A: Hier ist der aktualisierte Code. Um die Daten von der Star Wars API (swapi.info) abzurufen und in der Tabelle anzuzeigen, habe ich ein kleines JavaScript-Snippet hinzugefügt.

Ich habe die Tabelle mit Bootstrap-Klassen gestylt, damit sie modern aussieht.

HTML

<!doctype html>
<html lang="de">
<head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width,initial-scale=1">
    <title>Übersicht Copilot</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
    <style>
        body { background: #f2f3f5; }
        .navbar-brand img { height: 40px; }
        .table-container { background: white; padding: 20px; border-radius: 8px; box-shadow: 0 2px 4px rgba(0,0,0,0.1); }
    </style>
</head>
<body>

    <nav class="navbar navbar-expand-lg navbar-dark bg-dark mb-4">
        <div class="container">
            <a class="navbar-brand" href="#">
                <img src="https://upload.wikimedia.org/wikipedia/commons/6/6c/Star_Wars_Logo.svg" alt="Star Wars Logo">
            </a>
            <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav">
                <span class="navbar-toggler-icon"></span>
            </button>
            <div class="collapse navbar-collapse" id="navbarNav">
                <ul class="navbar-nav ms-auto">
                    <li class="nav-item">
                        <a class="nav-link" href="index.html">Zurück zur Startseite</a>
                    </li>
                </ul>
            </div>
        </div>
    </nav>

    <div class="container py-5">
        <h1>Übersicht Copilot</h1>
        
        <div class="table-container mt-4">
            <table class="table table-hover">
                <thead class="table-light">
                    <tr>
                        <th>Name</th>
                        <th>Größe (cm)</th>
                        <th>Geburtsjahr</th>
                        <th>Heimatwelt</th>
                        <th>Aktion</th>
                    </tr>
                </thead>
                <tbody id="characters-table">
                    <tr>
                        <td colspan="5" class="text-center">Daten werden geladen...</td>
                    </tr>
                </tbody>
            </table>
        </div>
    </div>

    <script>
        async function fetchCharacters() {
            try {
                const response = await fetch('https://swapi.info/api/people');
                const data = await response.json();
                
                const tableBody = document.getElementById('characters-table');
                tableBody.innerHTML = ''; // Lade-Text entfernen

                data.forEach(person => {
                    const row = document.createElement('tr');
                    
                    row.innerHTML = `
                        <td>${person.name}</td>
                        <td>${person.height}</td>
                        <td>${person.birth_year}</td>
                        <td>
                            <a href="${person.homeworld}" target="_blank" class="btn btn-sm btn-outline-secondary">Link zur Welt</a>
                        </td>
                        <td>
                            <a href="#" class="btn btn-sm btn-primary disabled">Details</a>
                        </td>
                    `;
                    
                    tableBody.appendChild(row);
                });
            } catch (error) {
                console.error('Fehler beim Abrufen der Daten:', error);
                document.getElementById('characters-table').innerHTML = '<tr><td colspan="5" class="text-danger">Fehler beim Laden der Daten.</td></tr>';
            }
        }

        // Funktion beim Laden der Seite ausführen
        fetchCharacters();
    </script>

    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>
</body>
</html>
Erklärungen zu den Änderungen:
Tabellen-Struktur: Ich habe eine HTML-Tabelle mit der ID characters-table erstellt. Dort "injiziert" das JavaScript die Zeilen.

Fetch API: Das Script nutzt fetch(), um die Daten von der URL https://swapi.info/api/people abzurufen.

Spalten:

name, height, birth_year werden direkt angezeigt.

Heimatwelt: Ein Button-Link, der direkt auf die URL der Heimatwelt führt (öffnet sich in einem neuen Tab).

Details: Ein blauer Button, der aktuell die Klasse disabled hat und als Linkziel nur # besitzt, da er noch nicht funktional gesetzt werden sollte.

Design: Die Tabelle ist mit table-hover (Zeile wird beim Drüberfahren markiert) und einem weißen Container mit leichtem Schatten versehen.
```

Hierbei schlägt Gemini direkt schon die richtige Lösung vor und benötigt keinen zweiten Call mehr.

### Detailseite

Als nächstes muss eine Detailseite erstellt werden für die Details Seite benötigen wir eine mitgegebene ID welcher als Parameter extra im Link angegeben werden soll. In React würde diese einfach mithilfe einer Komponente weitergegeben werden. 

Die einzelne IDs werden über den link direkt mitgegeben und können in details.html damit ausgelesen werden -> details.html?id=4

```
Q: Erstelle als nächstes eine detail.html welche alle Einträge dieses API calls anzeigt https://swapi.info/api/people/1

die id wird hierbei über den html link mitgegeben bsp: detail.html?id=4

Alle Einträge sollen hierbei schön formattiert angezeigt werden als beispiel hier ein ganzen json dokument

{ "name": "Luke Skywalker", "height": "172", "mass": "77", "hair_color": "blond", "skin_color": "fair", "eye_color": "blue", "birth_year": "19BBY", "gender": "male", "homeworld": "https://swapi.info/api/planets/1", "films": [ "https://swapi.info/api/films/1", "https://swapi.info/api/films/2", "https://swapi.info/api/films/3", "https://swapi.info/api/films/6" ], "species": [], "vehicles": [ "https://swapi.info/api/vehicles/14", "https://swapi.info/api/vehicles/30" ], "starships": [ "https://swapi.info/api/starships/12", "https://swapi.info/api/starships/22" ], "created": "2014-12-09T13:50:51.644000Z", "edited": "2014-12-20T21:17:56.891000Z", "url": "https://swapi.info/api/people/1" }

A: Lösung — Schritte:


Erstelle detail.html im Projektordner.
Parst die Query‑Parameter und liest id (Standard 1).
Ruft https://swapi.info/api/people/{id} per fetch (then/catch) ab.
Zeigt alle Felder formatiert als Schlüssel/Wert‑Liste an; Arrays als Listen (bei URLs als Links).
Zeigt Ladezustand und Fehler an; minimale Styles via installiertes Bootstrap.
Änderungen nach Datei:

C:\Users\sgroe\Documents\FH\3. Semester\Webtechnologie\Webtechnologie Projekt\LLM_Generated_Webproject\detail.html

Kurze Zusammenfassung: Neue Detailseite, die den Eintrag für die angegebene id von SWAPI lädt und alle Felder attraktiv darstellt.
```

Auch hier beim Generieren wurde der selbe Fehler gemacht mit der Einbindung des Bootstraps Packages. Sonst wurde hier eine einfache Darstellung der einzelnen Felder gut generiert.

Um diese Layout noch zu verschönern werden noch ein paar Änderungen vorgenommen

```
Q: Verstecke die Rohdaten in einen Dropdown box - um sie aufklappen zu können wenn nötig

A: Lösung — Schritte:


Rohdaten-Bereich in eine zusammenklappbare Bootstrap-Collapse-Box verschieben.
Einen Toggle-Button hinzufügen, der die Rohdaten ein-/ausblendet.
Bestehendes JS beibehalten (schreibt weiterhin in das pre#raw).
Änderungen nach Datei: detail.html

Kurze Zusammenfassung: Ersetze den festen Rohdaten-Block durch einen Collapse-Container mit einem Button zum Auf-/Zuklappen.
```

Hat es gut gemacht
Als nächstes eine schönere Struktur aller Daten:

```
Q: Erstelle nun ein raster Layout um die einzelnen Felder zu Gruppieren mit folgenden Gruppen

Persönliche Daten: name, birth_year, gender, species (nur wenn nicht leer) Aussehen: height, mass, hair_color, skin_color, eye_color Filme: Auflistung der Filme - statt dem Link soll aber nur die letzte Zahl extrahiert werden und der nummerische Werte soll dann mit folgenden Titel ausgetauscht werden (1 - A New Hope, 2 - The Empire Strikes Back, 3- Return of the Jedi, 4 - The Phantom Menace, 5 - Attack of the Clones, 6- Revenge of the Sith) Raumschiffe und Fahrzeuge: Summe der Einträge von vehicles und starships und einer dropdown auflistung aller links

A: Lösung — Schritte:


Ersetze die Felder‑Darstellung durch ein Bootstrap‑Raster mit vier Gruppen (Persönliche Daten, Aussehen, Filme, Raumschiffe & Fahrzeuge).
Passe das JS an: nach dem Fetch die JSON‑Daten in die Gruppen aufbereiten (Filmtitel‑Mapping, IDs extrahieren, Summe für Fahrzeuge/Raumschiffe, Collapse für Auflistung).
Behalte das Rohdaten‑Collapse und Lade/Fehler‑Handling bei.
Änderung nach Datei:

C:\Users\sgroe\Documents\FH\3. Semester\Webtechnologie\Webtechnologie Projekt\LLM_Generated_Webproject\detail.html

Kurze Zusammenfassung: Ersetze den bisherigen Felder‑Block durch ein responsive Grid (id="groups") und tausche den Script‑Block gegen eine Version, die die geforderten Gruppierungen rendert.
```

Da jetzt alle Daten schön gruppiert wurden ist mir noch eine Sache aufgefallen zwecks der Anzeige, die Rohdaten sollen unter den restlichen Daten angezeigt werden nicht darüber.

```
Q: Ändere die Person - Detail Card noch und schreibe nur Details hinein ohne beschreibung - ändere auch bitte dass die daten als eigene karte agezeigt werden und unter den eigenlichen formatierten daten stehen

A: Lösung — Schritte:


Entferne die Beschreibungs-Zeile in der oberen Card — dort bleibt nur noch die Überschrift "Person — Detail".
Verschiebe den Rohdaten-Collapse unter das formatierte Grid; zeige die Rohdaten in einer eigenen Card, die unter den formatieren Datengruppen liegt.
Stelle sicher, dass jede Gruppe weiterhin als eigene Karte gerendert wird (JS bleibt unverändert).
Änderungen nach Datei:

C:\Users\sgroe\Documents\FH\3. Semester\Webtechnologie\Webtechnologie Projekt\LLM_Generated_Webproject\detail.html

Kurze Zusammenfassung: Entferne die Beschreibung im Header-Card und verlege den Rohdaten-Collapse in eine eigene Card unterhalb des Grid mit den Gruppen.
```

Nach diesem Schritt musste ich noch eine kleine Änderung machen weil die ID trotzdem noch dynamisch immer hinzugefügt worden ist.

Als nächstes Schritt fehlt noch die Einbindung in die Übersichtsseiten - diese wird händisch vorgenommen das es länger dauert die Anfrage der KI auszuformulieren als es persönlich zu ändern.

### Formularseite

Als erstes soll einmal die grobe Struktur eines Formulars erstellt werden- manche Felder können dabei schon eingeschränkt werden welche daten eingegeben werden können

```
Q:erstelle eine formular mit diesen feldern um einen datenobject zu definieren welches dann an den link # geschickt wird

{ "name": "Luke Skywalker", - "height": "172", - nur zahl "mass": "77",- nur zahl "hair_color": "blond", "skin_color": "fair", "eye_color": "blue", - select aus möglichen augenfarben "birth_year": "19BBY", "gender": "male", - select aus male, female, other "homeworld": "https://swapi.info/api/planets/1", "films": [ "https://swapi.info/api/films/1", "https://swapi.info/api/films/2", "https://swapi.info/api/films/3", "https://swapi.info/api/films/6" ], "species": [], "vehicles": [ "https://swapi.info/api/vehicles/14", "https://swapi.info/api/vehicles/30" ], "starships": [ "https://swapi.info/api/starships/12", "https://swapi.info/api/starships/22" ],

die bootstrap version soll nicht geändert werden!

A:
Lösung — Schritte (kurz):


Ergänze das Formular mit den geforderten Eingabefeldern (Name, Height, Mass, Hair/Skin, Eye color select, Birth year, Gender select, Homeworld, Films/Species/Vehicles/Starships als je eine URL pro Zeile).
Validierung: height und mass müssen Zahlen sein; required-Felder prüfen.
Beim Submit JSON-Objekt bauen, Vorschau anzeigen und per fetch an '#' senden (POST, application/json). Fehler/Succes anzeigen.
Bootstrap-Version nicht ändern; nur lokale Form- und Script-Änderungen.
Änderungen nach Datei:

C:\Users\sgroe\Documents\FH\3. Semester\Webtechnologie\Webtechnologie Projekt\LLM_Generated_Webproject\erschaffe-deinen-eigenen-character.html

Kurze Zusammenfassung: Ersetze/ergänze den Formularbereich und das zugehörige Script. Bootstrap-Verlinkungen bleiben unverändert.
```
 Diese Anfrage musste zweimal gestellt werden - da beim ersten Mal Sachen verändert wurden, welche nicht gefördert waren.

Da verschiedene Elemente nur mit der URL angegeben werden würde ich gerne Probieren alles Elemente zu fetchen und diese über ein Select auszuwählen, diese Möglichkeit ist viel benutzerfreundlicher.

Für den Anfang probiere ich es mit den Planeten

```
Q:Ändere nun die Eingabe Art des Feldes Homeworld zu einem Select das Select bekomment die Möglichen Antwortungsmöglichkeiten aus diesem API Call:

fetch("https://swapi.info/api/planets") .then((res) => res.json()) .then((json) => console.log(json)) .catch((error) => console.error(error))

Der Rückgabewert sieht folgend aus:

[ { "name": "Tatooine", .. "url": "https://swapi.info/api/planets/1" }, { "name": "Alderaan", ... }

das select soll alle name beinhalten aber die Daten welche dann gespeichert werden soll das Feld url sein

A: Lösung — Schritte (kurz):


Ersetze das Homeworld-Input durch ein Select-Element.
Lade die Planeten per fetch von https://swapi.info/api/planets und fülle das Select mit name (Label) und url (value).
Behandle Ladefehler und behalte das bestehende Submit-Verhalten (gesendeter Wert ist die URL).
Dateiänderung:

C:\Users\sgroe\Documents\FH\3. Semester\Webtechnologie\Webtechnologie Projekt\LLM_Generated_Webproject\erschaffe-deinen-eigenen-character.html

Kurz: Homeworld-Feld in ein Select geändert und JS ergänzt, das die Planeten lädt und das Select befüllt.

```

Da dies so einfach funktioniert hat soll das gleiche auch bei den restlichen feldern gemacht werden

```
Q:Ändere die restlichen Inputs auch nocht um der delder films, species, vehicles, starships

die URL muss nur geändert werden - funktioniert mit dem selber prinzip nur können hier mehr als eine ausgewählt werden

A: Lösung — Schritte (kurz):


Ersetze die Textareas für films, species, vehicles und starships durch multi-selects.
Ergänze ein generisches Loader-Skript, das die jeweiligen API-Endpunkte lädt und Select-Optionen (label=name|title, value=url) erstellt.
Lese beim Submit die ausgewählten Optionen als Arrays aus und baue das JSON wie gehabt.
Behalte Bootstrap-Version unverändert und die bestehende Planeten-Logik.
Änderungen nach Datei:

C:\Users\sgroe\Documents\FH\3. Semester\Webtechnologie\Webtechnologie Projekt\LLM_Generated_Webproject\erschaffe-deinen-eigenen-character.html

Kurze Zusammenfassung: Ersetze die vier Textareas durch multi-selects und erweitere das Script um das Befüllen dieser Selects und das Auslesen der gewählten URLs.
```

Dies hat wirklich gut funktioniert und die Lösung ist auch akzeptabel direkt das richtige Multi - Select verwendet.

Das einzige was noch fehlt ist den Post Request zu senden - da die Star Wars API nur eine Datenquelle ist die nicht bearbeitet werden darf, muss der Post Request an https://httpbin.org/post gesendet werden. Dieser Response beinhaltet dann die Daten um zu zeigen, dass der Server es richtig bekommen hat. Folgende Aufgabe wurde an die KI gesendet:

```
Q: sende einen REST Post Nachricht auf diese Adresse https://httpbin.org/post

A:
Lösung — Schritte:


Ersetze die Ziel-URL im fetch von '#' zu 'https://httpbin.org/post'.
Parste die Antwort als JSON und zeige die Antwort kurz in der Vorschau/Alert an.
Fehlerbehandlung beibehalten.
Änderungen nach Datei: erschaffe-deinen-eigenen-charakter.html

Kurze Zusammenfassung: Austausch der fetch-Ziel-URL und Anpassung der Response-Verarbeitung (JSON statt Text), Anzeige der Antwort im Preview.
```

Über die Console des Browsers konnte überprüft werden, dass die Nachricht richtig übermittelt wurde - mehr dazu in den Testfällen.

Fehlende Navbar: zum Schluss ist noch aufgefallen, dass man im Formular nicht mehr zur Index zurückkommt daher wurde diese Änderung ebenfalls von der LLM gelöst:

```
Q: Füge wie in den anderen Dokumenten noch die Navigationsbar ein mit der man auf die Indexseite oder auf die Übersichtsseiten zurück kommt

A: Lösung — Schritte (kurz):


Füge oben im Body eine Bootstrap-Navbar ein mit kleinem Logo links (verlinkt auf index.html) und Rechts-Links zu den Übersichtsseiten.
Platziere die Navbar vor dem bestehenden Container; der Rest der Seite bleibt unverändert.
Keine Änderung der Bootstrap-Version.
Änderungen nach Datei:erschaffe-deinen-eigenen-charakter.html

Kurze Zusammenfassung: Navbar oberhalb des bestehenden Inhalts ergänzt — links ein kleines Logo (verweist auf index.html), rechts Links zu Home und den beiden Übersichtsseiten.
```

### Generelle Änderungen

Im gesamten Projekt ist die Navbar immer leicht unterschiedlich, obwohl der LLM immer gesagt wurde die gleiche navbar zu verwenden. 

```
Q:Füge in allen html Dokumenten das BILD Star_wars_Logo in die navbar links oben statt dem Text ein

A:Lösung — Schritte (kurz):


Ersetze im Navbar-Brand den Text/Badge durch ein img-Element, das das Bild assets/Star_wars_Logo.png lädt.
Verwende ein alt-Attribut und passende Höhe (z.B. 34px) sowie Bootstrap-Klasse me-2 für Abstand.
(Hinweis) Lege das Bild unter assets/Star_wars_Logo.png ab oder passe den Pfad entsprechend an.
Änderungen nach Datei:

C:\Users\sgroe\Documents\FH\3. Semester\Webtechnologie\Webtechnologie Projekt\LLM_Generated_Webproject\erschaffe-deinen-eigenen-character.html

Kurze Zusammenfassung: Navbar links oben: Text-Badge durch Bild ersetzt.
```

Hier wurde nicht direkt erkannt welches Bild ich verwendet wollte und es wurde nur in einem File verändert. Daher nochmal ein neuer Versuch mit dem ganzen Namen des Files und umstellung für globale Veränderung.

```
Q: Füge in all diesen Files das Star Wars Logo in die Navbar ein (assets/Star_Wars_Logo.svg.png) ebenfalls sollen alle Links gleich benannt werden index -> home uebersicht-copilot -> Übersicht Copilot detail benötigt keinen link in der navbar

A:Lösung — Schritte (kurz):


Ersetze in allen betroffenen Dateien das Navbar-Brand‑Element durch das Bild assets/Star_Wars_Logo.svg.png (nur img, kein Text).
Vereinheitliche die Navbar‑Links (Home, Übersicht Copilot, Übersicht ChatGPT, Hervorgehobener "Erschaffe..."-Link) in allen Dateien außer detail.html.
Entferne in detail.html alle rechten Links (nur Logo in der Navbar).
Belasse sonstigen Code unverändert.
Änderungen nach Datei: erschaffe-deinen-charakter.html

Kurze Zusammenfassung: Navbar-Brand auf das gewünschte Bild geändert; Link‑Texte vereinheitlicht (Home, Übersicht Copilot, Übersicht ChatGPT).

index.html
Kurze Zusammenfassung: Navbar-Brand durch Bild ersetzt; Link‑Labels vereinheitlicht (Home etc.).

uerbersicht-copilot.html
Kurze Zusammenfassung: Navbar-Brand geändert; Navbar jetzt konsistent (Home, Übersicht Copilot, Übersicht ChatGPT)

detail.html
Kurze Zusammenfassung: Navbar-Brand geändert und alle rechten Links entfernt (detail: nur Logo in Navbar).
```

Generell wurde alles richtig übernommen in der Beschreibung meines Änderungsvorschlages hat sich leider ien Fehler eingebaut, dass alle Links aus Detail gelöscht werden.
Dabei möchte ich noch Änderen, dass Alle navbar das gleiche Ausehen haben (dunkle Farbe) und in der detail seite es einen zurückbutton gibt um auf die letzte seite zu kommen (Übersicht)

```
Q:Alle Navbars sollen hier das gleiche dunkle design haben und in der detail.html soll in der linken unteren ecke ein runder zurück button eingefügt (gefixt in der ecke) werden um wieder auf die Überischtsseite zu gelangen (übersicht chagpt oder überischt copilot)

A: Lösung — Schritte:


Vereinheitliche die Navbar-Klassen auf navbar-dark bg-dark shadow-sm in allen HTML-Dateien.
Gleiche Bildpfade zum Logo auf "./assets/Star_Wars_Logo.svg.png" an.
Füge in detail.html eine feste, runde Rückkehr-Button-Gruppe unten links ein, die zu den Übersichtsseiten führt.
Belasse übrigen Code unverändert.
Änderungen nach Datei:

erschaffe-deinen-charakter.html
Kurze Zusammenfassung: Navbar auf konsistentes dunkles Design bringen (shadow-sm hinzufügen) und Logo-Pfad vereinheitlichen.

uebersicht-copilot.html
Kurze Zusammenfassung: Navbar auf dunkles einheitliches Design umstellen (navbar-dark bg-dark shadow-sm) und Logo-Pfad vereinheitlichen.

detail.html
Kurze Zusammenfassung: Navbar in dunkles Design ändern, Logo-Pfad vereinheitlichen und feste, runde Rückkehr-Buttons (unten links) hinzufügen, die zu den Übersichtsseiten führen.

```

Damit ist die NavBar jetzt einheitlich bis auf die Übersicht von ChatGPT

Ebenfalls wurde der Text in der Indexseite persönlich geschrieben.

## Einsatz von LLM für die Programmierung

Insgesamt war die Arbeit mit dem Github Copilot zusammen sehr gut, ich habe versucht so wenig wie möglich während der Implementierung zu machen. Da es aber zu keinen größeren Fehlern kam konnte ich nur durch kurze Fixe das problem lösen. Durch die Einbindung des Copilots direkt im Projekt konnte die LLM den Code auch selber Formatieren ordnen. Dies war sehr hilfreich

Für das generelle Arbeiten in der FrontEnd Ebene finde ich die Unterstützung der LLM sehr gut auch wenn sich kleinere Fehler einschleichen steigt die effizienz sehr. Dies kann aber nur geschehen wenn die Problemstellung richtig beschrieben wird. Desto genauer diese beschrieben wird desto besser kann die LLM das gewünschte Ergebnis erreichen. 
Besonders in der Front End Schiene wobei das Ergebnis direkt zu betrachten ist können gleich Fehler leichter erkannt werden. In der Backend Programmierung kann dies sehr schwer werden. Da hier der Code nur durch Test-Cases überprüft werden kann. Besonders im Umgang mit neuen Technologien ist aber vorischt geboten. Fehler können sich sehr schnell einschleichen welche nicht vom der LLM erkannt werden und dann selber durch den Code zu Blicken erschwert es sehr. 

Durch schon persönliche Erfahrung in der Arbeit, ist das Verhalten einer LLM leichter als Unterstützung zu sehen mit kleinenen Arbeitspacketen. -> Immer kleine Änderung die sehr gut beschrieben werden helfen zu einem guten Projekt. 

Dies Erspart auch eingies an Arbeit. Dieser Ansatz ist effizienter als die Aufforderung: Baue mir ein Website mit folgenden Komponenten...

Im Nachhinein würde dies mehr arbeit kosten als man einspart.

Für die Plannung kommt es rein auf das Projekt an ob der Einsatz von LLMs Sinn macht. Für solch ein kleines Projekt besonders mit so einem kleinen UseCase ist die Verwendung Plannung ziemlich offensichtlich. In einem größeren Projekt kann ich mir das gut Vorstellen, besonders im Bezug auch Gegenkontrolle. IMO: Sind die LLMs ziemlich hilfreich ob man selber etwas vergessen hat zum Überprüfen.

## Vergleich von ChatGPT und Copilot

Für die Aufgab eder Übersichtsseite wurden zwei verschiedene Übersichtsseiten, beide sind auch über die Webseite zugänglich.
Generell für den Code wurden nur generierte Elemente verglichen und der Copilot wurde nur frü das HTML File erstellen verwendet, danach wurde es nicht mehr vom Copilot verändert.

Kurz gefasst, beide LLMS haben die Aufgabenstellung gelöst, durch die Einbindung des Copilotes muss nichts mehr kopiert werden, dass vereinfacht den Prozess. Generell zeigen sich bei den Responses auch warum welche LLM für was verwendet wird. Copilot ändert nur wie gefordert die Daten hingegen Gemini Änderungsvorschläge anzeigt was es noch alles machen kann. Für ein kreatives Projekt wie dieses hier ist es sicher sehr hilfreich. 

Generell vom visuellen Vergleich sind beide sehr ähnlich. Der Copilot nimm als Spaltennamen direkt den Key namen des JSON Key-Value Pairs - Gemini hingegen zeigt eine Übersetzung des Textes an und nimmt an das die Größe in cm ist. Die Tabelle bei Gemini hat einen kleinen visuellen Fehler das die Headerzeile nicht mit einer anderen Farbe als die Hintergrundfarbe eingebettet wurde. 

Auch die Links in der Table Row sind unterscheidlich während Copilot einen einfachen `href` setzt generiert Gemini einen Button der beim Klicken den Link aufmacht.

### Code Vergleich

Der Code ist sehr ähnlich strukturiert, wie zu erwarten werden meisten verschiedene Bootstrap Attribute verwendet - alleine in der NavBar wird der Resposive Ansatz anders angsehen bei welcher Fenstergrößte die Nabar toggelt. Das verwendete Logo in der Navbar wurde automatisch von Wikipedia verwendet von Gemini im Copilot musste ich es extra setzen.

Auch der Table ist sehr ähnlich aufgebaut beide LLMs bauen einen Ladezustand ein bis die Daten von der API gefetchet werden.

Beim Script wird es schon unterschiedlicher:

Copilot fügt hier einen minimalen XSS Schutz ein.

Die Fetch function wird bei beiden LLMS verwendet Copilot ruft diese direkt auf während Gemini die Funktion extra als async funtion deklariert und später aufruft. 

Copliot versucht über die Fluent APi einen Fehler abzufangen während Gemini es mit einem Try/Catch Block löst.
Ein ersichtlicher Unterschied ist hierbei das aufzeigen von 0 Einträgen. Während Copilot direkt abfragt ob der Resopnse Elemente enthält und dies auch der Webseite ausschreibt würde Gemini nur eine leere Tabelle zeigen. 

Ein weiterer Unterscheid ist auch das setzten der einzelnen Table-Row:

```javascript

 for (const p of json) {
                const tr = document.createElement('tr');

                const nameTd = '<td>' + esc(p.name) + '</td>';
                const heightTd = '<td>' + esc(p.height) + '</td>';
                const birthTd = '<td>' + esc(p.birth_year) + '</td>';
                const homeworldHref = p.homeworld ? esc(p.homeworld) : '#';
                const homeworldTd = '<td>' + (p.homeworld
                    ? '<a href="' + homeworldHref + '" target="_blank" rel="noopener">Homeworld</a>'
                    : '<span class="text-muted">—</span>') + '</td>';
                const link = p.url ? 'detail.html?id=' + encodeURIComponent(p.url.match(/\/(\d+)\/?$/)[1]) : '#';
                const detailsTd = '<td><a class="btn btn-sm btn-outline-secondary " href=" ' + link + '" role="button" aria-disabled="true">Details</a></td>';

                tr.innerHTML = nameTd + heightTd + birthTd + homeworldTd + detailsTd;
                tbody.appendChild(tr);
            }
```

```javascript
data.forEach(person => {
                const row = document.createElement('tr');
                const link = person.url ? 'detail.html?id=' + encodeURIComponent(person.url.match(/\/(\d+)\/?$/)[1]) : '#';

                row.innerHTML = `
                        <td>${person.name}</td>
                        <td>${person.height}</td>
                        <td>${person.birth_year}</td>
                        <td>
                            <a href="${person.homeworld}" target="_blank" class="btn btn-sm btn-outline-secondary">Link zur Welt</a>
                        </td>
                        <td>
                            <a class="btn btn-sm btn-outline-secondary " href="${link}" role="button">Details</a>
                        </td>
                    `;

                tableBody.appendChild(row);
            });
```

Natürlich wird das Gleiche gemacht es sind einfach nur zwei verschiedene Ansätze und Abhängig vom Programierer welcher schöner ist. IMO ist der Ansatz vom Gemini schöner gelöst.

In der Console zeigt die HTML Seite von CoPilot noch einen Error:

`uebersicht-copilot.html:1 Refused to apply style from 'http://localhost:63342/LLM_Generated_Webproject/style.css' because its MIME type ('text/html') is not a supported stylesheet MIME type, and strict MIME checking is enabled.`

Bei Gemini scheint hier nichts auf.

## Testfälle

Hauptsähclich wurde beim Testen der Drunken-Monkey Ansatz verfolgt. -> Überall draufklicken und sehen ob das Ergebnis beabsichtigt war. Was überall wie beabsichtigt funktionierte

### Indexseite 

Die Indexseite zeigt hierbei nur Informationen an und hat noch keinen logischen Testfall die Buttons und Links führen zu den gewünschten Seite weiter.

### Überwsicht Copilot

Alle Links führen zur richtigen Seite hin

API nicht erreichbar - nachgestellt durch falschen URL:

![alt text](image-5.png)

- Seite stürzt nicht ab und zeigt Benützer, dass es einen Fehler gab!

### Übersicht Gemini

Alle Links leiten zur richtigen Seite weiter

![alt text](image-6.png)

### Details

Alle links leiten zur richtigen Seite weiter

Falsche Idee oder Service nicht erreichbar

![alt text](image-7.png)

Da die Id direkt weitergegeben wird und nicht über einen extra Parameter würde es hier keinen Unterschied machen um heruaszufinden ob der Service nicht erreichbar ist oder die ID ungültig - daher gibt es hier keine bessere Lösung

### Create Seite

Alle Links führen zur richtigen Seite hin.

Post Befehl fehlgeschlagen - Nutzer wird benachrichtigt und Elemente werden nicht zurückgesetzt.

![alt text](image-8.png)

Gewisse Felder müssen gefüllt sein um sie zu zeigen

![test](image-4.png)