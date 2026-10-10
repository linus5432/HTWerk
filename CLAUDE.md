# HTWerk-Website

Übergabe-Notiz für Claude Code. Sprache mit dem Nutzer: Deutsch.

## Was das ist

Statische Website für HTWerk, eine studentische Initiative an der HTW Berlin, die
Werksbesichtigungen und Büro-Touren bei Unternehmen organisiert. Zielgruppen:
Studierende (Anmeldung zu Touren) und Unternehmen (Tour ausrichten).

Reines HTML und CSS mit wenig JavaScript, kein Build-Schritt, kein Framework.

## Hosting

- Live unter https://htwerk.de über GitHub Pages, Branch `main`, Ordner `/` (root).
  Jeder Push auf `main` geht nach ein bis zwei Minuten online.
- Die Datei `CNAME` legt die Domain fest. Nicht löschen.
- Domain registriert bei INWX, DNS bei Cloudflare (vier A-Einträge auf GitHub Pages,
  CNAME `www` auf `linus5432.github.io`, alle „DNS only“).

## Dateien

| Datei | Inhalt |
| --- | --- |
| `index.html` | Startseite: Titel, About us, Core Team, Hosting, Past visits, Ablauf, Anmeldung, Kontakt |
| `1komma5.html`, `siemens-energy.html`, `formlabs.html`, `bmw-motorrad.html` | Je eine Unterseite pro Tour mit einem kurzen Rückblick. Von der Startseite unter `#visits` verlinkt |
| `images/` | 12 Fotos aus der Partner-Präsentation (JPG, max. 1400 px), der Ordner `formlabs/` mit den Galerie-Fotos der Formlabs-Tour, `og-image.jpg` (Vorschaubild 1200 x 630 für geteilte Links, mit Logo) und das Logo als Datei: `logo-htwerk.svg` (Wortmarke) und `logo-htwerk-monogramm.svg` (H mit Helm), beide schwarz |
| `fonts/` | Schriftdateien (woff2), `fonts.css` mit den `@font-face`-Regeln, Lizenztexte (SIL OFL) |
| `favicon.svg`, `favicon.png`, `apple-touch-icon.png` | Icon: weißes Monogramm (H mit Helm) auf Schwarz |
| `CNAME` | Domain für GitHub Pages |

## Design

Vorlage ist die Partner-Präsentation „HTWerk Partner Proposal 2026“:

- Schwarz-weiß, keine Akzentfarbe. Tokens in `:root`: `--black`, `--white`, `--grey`, `--line`
- Geteilte Flächen aus Text und Foto (`.split`), Fotos randlos
- Überschriften in Marcellus (Serif), Fließtext in IBM Plex Sans (400, 600, 700).
  Beide liegen lokal in `fonts/` und werden über `fonts/fonts.css` eingebunden.
  Keine Schriften oder Skripte von fremden Servern laden (Datenschutz).
- Firmennamen unter „Past visits“ stehen hochkant neben dem Foto, in Großbuchstaben
- Reihenfolge der Abschnitte und der Fotos folgt der Präsentation. Nicht umsortieren, ohne zu fragen
- Unter „Past visits“ stehen nur die Firmennamen, keine weiteren Angaben
- Alle Fotos außer dem ersten haben `loading="lazy"`

## Logo

Entwurf „Helm“ aus der Canva-Datei „HTWerk – Logo-Entwürfe“: Das H der Wortmarke trägt einen Schutzhelm.
Es gibt zwei Fassungen, beide als ein einziger Vektorpfad aus den Marcellus-Umrissen:

- **Wortmarke** „HTWerk“ mit Helm: steht als Inline-SVG im `<h1>` der Startseite und in `.brand`
  in der Kopfzeile der vier Tour-Seiten. Farbe über `fill:currentColor`, also weiß auf Schwarz.
  Im `<h1>` steht zusätzlich unsichtbar der Text „HTWerk“ (`.vh`) für Screenreader und Suchmaschinen.
- **Monogramm** (H mit Helm): Favicon, Touch-Icon und klein in der Fußzeile aller Seiten (`.mark`).

Der Pfad steht in allen fünf HTML-Dateien identisch. Bei einer Änderung am Logo überall ersetzen,
dazu `favicon.svg`, die beiden PNG-Icons, `images/og-image.jpg` und die zwei SVG-Dateien in `images/`.
Die Größe der Wortmarke im Titel regelt `.hero h1 svg` (Breite), in der Kopfzeile `.brand svg` (Höhe).

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
- Deutsche Begriffe einheitlich halten: „Tour“ für das Format, „Besuch“ für den einzelnen Termin,
  „Rückblick“ für den Blog-Text. Der deutsche Claim lautet
  „Studentische Initiative für Werks- und Unternehmensbesuche“.
- Aufzählungen für Unternehmen unter `#host` stehen im Infinitiv („Eine Ansprechperson benennen …“), nicht im Imperativ.

## Anmeldung

Der Link zur Anmeldung steht an genau einer Stelle: in `index.html` im Abschnitt `#signup`
(Button „Register on Luma“). Er zeigt auf `https://luma.com/user/LinusRuesseler`.
Alle anderen „Join the next tour“-Buttons, auch auf den Tour-Seiten, führen zu `index.html#signup`.

## Tour-Unterseiten

- Jede Tour ist in `index.html` unter `#visits` ein `<a class="visit" href="….html">` mit der Zeile
  „Read the recap / Zum Rückblick“ unter dem `<h3>`.
- Auf den Tour-Seiten stehen kurze Rückblicke (Einleitung und zwei Absätze je Sprache). Sie enthalten nur,
  was belegt ist: Reihenfolge der Touren, Teilnehmerzahlen (BMW Motorrad 14, Formlabs 20, Siemens Energy 20),
  beteiligte Hochschulen und was auf den Fotos zu sehen ist. Nichts dazuerfinden; neue Details kommen von Linus.
- Unter dem Namen steht eine Zeile `.meta` (Art des Besuchs, Teilnehmerzahl). Das Datum fehlt bei allen vier Touren.
- Der editierbare Bereich liegt zwischen den Kommentaren `AB HIER SCHREIBST DU DEINEN BLOG-TEXT`
  und `ENDE DEINES TEXTES`. Dort stehen auch Bausteine zum Kopieren.
- Fotos im Text: `<div class="shots">` mit zwei `<figure>` nebeneinander, für beide Sprachen gemeinsam
  (Bildunterschrift zweisprachig, Alt-Text über `data-alt-de`). BMW Motorrad hat zwei Fotos,
  für Siemens Energy und 1KOMMA5° gibt es außer dem Titelfoto keine.
- Galerie: `<div class="gallery">` zeigt viele Fotos zu je drei nebeneinander (am Handy zwei), ohne Bildunterschrift.
  Jedes Bild ist ein Link auf die große Datei. Formlabs hat eine Galerie aus zwölf Fotos: zehn liegen in
  `images/formlabs/` (`01.jpg` groß mit 1400 px, `01-s.jpg` klein mit 640 px für das Raster), dazu
  `hero-formlabs.jpg` und `networking.jpg`. Neue Fotos genauso anlegen und ohne EXIF-Daten speichern.
- Die vier Seiten sind bis auf Name, Texte, Fotos und „Next visit“-Link identisch.
  Änderungen am Gerüst in allen vier Dateien nachziehen.
- Neue Tour: eine bestehende Tour-Seite kopieren, Name, Texte, Fotos und Alt-Texte anpassen,
  in `index.html` unter `#visits` einen weiteren Block ergänzen
  und die „Next visit“-Kette anpassen (aktuell 1KOMMA5° → Siemens Energy → Formlabs → BMW Motorrad → 1KOMMA5°).
  Die Zahl in „So far: 4 tours …“ im Abschnitt `#host` mit anpassen.

## Offene Punkte

1. `impressum.html` und `datenschutz.html` existieren nicht, sind aber im Footer verlinkt.
   Ein Impressum ist Pflicht. Dafür fehlt die Anschrift des Verantwortlichen.
2. Die Rückblicke auf den vier Tour-Seiten sind kurz und von Claude aus wenigen Fakten geschrieben.
   Es fehlen das Datum jeder Tour, die Teilnehmerzahl bei 1KOMMA5° und alles, was nur die Teilnehmenden wissen
   (wer geführt hat, was gezeigt wurde). Linus sollte sie prüfen und ergänzen.
3. Einwilligung der abgebildeten Personen und Freigabe der Unternehmen für die Fotos klären.
4. Im Kontakt steht eine persönliche Hochschul-Adresse. Eine eigene HTWerk-Adresse wäre besser.
5. Die deutschen Texte wurden im Oktober 2026 überarbeitet. Linus sollte sie einmal gegenlesen,
   vor allem den neuen Claim und die Rollenbezeichnungen im Team.
6. Der Anmeldelink führt auf ein persönliches Luma-Profil. Ein eigener HTWerk-Kalender auf Luma
   oder der Link zur jeweils nächsten Veranstaltung wäre direkter.
7. Die nächste Tour (Firma, Datum, Plätze) wird auf der Seite noch nicht konkret genannt.
8. Im Team fehlt ein Mitglied, das nicht in der Präsentation stand. Teamfotos fehlen.

## Prüfen

Kein Test-Setup. Nach Änderungen die Seiten im Browser in beiden Sprachen und in
Handybreite (ca. 390 px) öffnen und auf horizontales Scrollen achten.
