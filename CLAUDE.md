# HTWerk-Website

Übergabe-Notiz für Claude Code. Sprache mit dem Nutzer: Deutsch.

## Was das ist

Statische Website für HTWerk, eine studentische Initiative an der HTW Berlin, die
Werksbesichtigungen und Büro-Touren bei Unternehmen organisiert. Zielgruppen:
Studierende (Anmeldung zu Touren) und Unternehmen (Tour ausrichten).

Reines HTML und CSS mit wenig JavaScript, kein Build-Schritt, kein Framework.
Gehostet werden soll über GitHub Pages aus dem Branch `main`, Ordner `/` (root).

## Dateien

| Datei | Inhalt |
| --- | --- |
| `index.html` | Startseite: Titel, About us, Core Team, Hosting, Past visits, Ablauf, Anmeldung, Kontakt |
| `1komma5.html`, `siemens-energy.html`, `formlabs.html`, `bmw-motorrad.html` | Je eine Unterseite pro Tour, gedacht als Blog-Rückblick. Aktuell nur Platzhaltertext |
| `images/` | 12 Fotos aus der Partner-Präsentation (JPG, max. 1400 px) |
| `htwerk.html` | Älteres Konzeptpapier für die Student EXPO Berlin 2027. Gehört nicht zur Website, ist nirgends verlinkt |

## Design

Vorlage ist die Partner-Präsentation „HTWerk Partner Proposal 2026“:

- Schwarz-weiß, keine Akzentfarbe. Tokens in `:root`: `--black`, `--white`, `--grey`, `--line`
- Geteilte Flächen aus Text und Foto (`.split`), Fotos randlos
- Überschriften in Marcellus (Serif), Fließtext in IBM Plex Sans, beide über Google Fonts
- Firmennamen unter „Past visits“ stehen hochkant neben dem Foto, in Großbuchstaben
- Reihenfolge der Abschnitte und der Fotos folgt der Präsentation. Nicht umsortieren, ohne zu fragen
- Unter „Past visits“ stehen nur die Firmennamen plus „Read the recap“, keine weiteren Angaben

## Zweisprachigkeit (DE/EN)

- Jeder sichtbare Text steht doppelt: `<span lang="en">…</span><span lang="de">…</span>`
  im selben Element. Auf den Tour-Seiten gibt es für den Blog-Text zwei Blöcke
  `<div lang="en">` und `<div lang="de">`.
- CSS blendet die jeweils andere Sprache aus: `html[lang="de"] [lang="en"]{display:none}` und umgekehrt.
- Die Sprache wird im `<head>` gesetzt: erst `?lang=de|en` aus der Adresse, dann
  `localStorage` (`htwerk-lang`), sonst Browsersprache (Deutsch bei `de`, sonst Englisch).
- Der Umschalter (`[data-setlang]`) und das Skript am Seitenende sind in allen fünf Seiten identisch.
  Es setzt auch `document.title` (aus `data-title-de/en` am `<html>`), die Alt-Texte
  (`data-alt-de`) und hängt `?lang=` an interne Links.
- Neue Texte immer in beiden Sprachen anlegen. Unternehmen werden gesiezt, Studierende geduzt.

## Anmeldung

Der Link zum Anmeldeformular steht an genau einer Stelle: in `index.html` im Abschnitt
`#signup` beim Kommentar `TODO: HIER den Link zum Anmeldeformular einsetzen`.
Alle anderen „Join the next tour“-Buttons, auch auf den Tour-Seiten, führen zu `index.html#signup`.
Geplant ist ein Notion-Formular.

## Tour-Unterseiten

- Der editierbare Bereich liegt zwischen den Kommentaren `AB HIER SCHREIBST DU DEINEN BLOG-TEXT`
  und `ENDE DEINES TEXTES`. Dort stehen auch Bausteine zum Kopieren.
- Die vier Seiten sind bis auf Name, Titelfoto und „Next visit“-Link identisch.
  Änderungen am Gerüst in allen vier Dateien nachziehen.
- Neue Tour: eine bestehende Tour-Seite kopieren, Name, Foto und Alt-Texte anpassen,
  in `index.html` unter `#visits` einen weiteren `<a class="visit">`-Block ergänzen
  und die „Next visit“-Kette anpassen (aktuell 1KOMMA5° → Siemens Energy → Formlabs → BMW Motorrad → 1KOMMA5°).

## Offene Punkte

1. Link zum Anmeldeformular fehlt (Button zeigt noch auf `#signup`).
2. `impressum.html` und `datenschutz.html` existieren nicht, sind aber im Footer verlinkt.
   Ein Impressum ist Pflicht, sobald die Seite öffentlich beworben wird.
3. Blog-Texte und Tour-Daten auf den vier Tour-Seiten sind Platzhalter.
4. Einwilligung der abgebildeten Personen und Freigabe der Unternehmen für die Fotos klären.
5. Im Kontakt steht eine persönliche Hochschul-Adresse. Eine eigene HTWerk-Adresse wäre besser.
6. Die deutschen Texte der Startseite sind eine Übersetzung und noch nicht gegengelesen.
7. GitHub Pages ist noch nicht eingeschaltet (Settings > Pages > Branch `main`, Ordner `/`).

## Prüfen

Kein Test-Setup. Nach Änderungen die Seiten im Browser in beiden Sprachen und in
Handybreite (ca. 390 px) öffnen und auf horizontales Scrollen achten.
