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
| `index.html` | Startseite, Aufbau nach dem Vorbild von brisa-robotics.de (Oktober 2026, Wunsch von Linus): Titel mit Leitsatz „Raus aus dem Hörsaal, rein ins Werk.“ und den Buttons „Wer wir sind“ / „Mitmachen“; 01 Mission (`#mission`, drei Säulen Sehen, Fragen, Vernetzen); 02 Team (`#team`, nummerierte Karten); 03 Touren (`#touren`, Kasten „Nächste Tour“ mit Luma = `#signup`, darunter „Bisherige Besuche“ als Slider = `#visits`); 04 Partner (`#partner`, nur der dunkle Kasten = `#host` mit „Tour anfragen“ und Link „Mehr zum Ablauf einer Tour“ auf `unternehmen.html`); Fußzeile mit Schlusssatz, Kontakt, LinkedIn, Luma (`#contact`). Nur Struktur übernommen, Gestaltung bleibt HTWerk |
| `unternehmen.html` | Seite für Unternehmen, durchgehend gesiezt: Titel mit „Tour anfragen“, Past visits, Hosting (`#host`), Ablauf, Kontakt. Link für Anfragen an Firmen. Kopfzeile mit Wortmarke |
| `images/` | 12 Fotos aus der Partner-Präsentation (JPG, max. 1400 px), die Ordner `bmw-motorrad/`, `formlabs/` und `1komma5/` mit den Galerie-Fotos der Touren, `HTWerk/` mit den hochgeladenen Originalen, `og-image.jpg` (Vorschaubild 1200 x 630 für geteilte Links, mit Logo) und das Logo als Datei: `logo-htwerk.svg` (Wortmarke) und `logo-htwerk-monogramm.svg` (H mit Helm), beide schwarz |
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
- „Bisherige Touren“ (früher „Past visits / Bisherige Besuche“) ist auf `index.html` und `unternehmen.html` ein Slider
  (`.slider` > `.track` mit den `a.visit`). Zwei Pfeile liegen mittig über dem Slider (`.sarrow.prev`, `.sarrow.next`,
  der Weiter-Pfeil schwarz gefüllt). Wischen geht über CSS-Scroll-Snap auch ohne JavaScript; das kleine Skript vor dem
  Sprachskript steuert Pfeile und Pfeiltasten und springt nach der letzten Tour wieder zur ersten
- Alle Fotos außer dem ersten haben `loading="lazy"`

## Logo

Entwurf „Helm“ aus der Canva-Datei „HTWerk – Logo-Entwürfe“: Das H der Wortmarke trägt einen Schutzhelm.
Es gibt zwei Fassungen, beide als ein einziger Vektorpfad aus den Marcellus-Umrissen:

- **Wortmarke** „HTWerk“ mit Helm: steht als Inline-SVG im `<h1>` der Startseite und in `.brand`
  in der Kopfzeile von `unternehmen.html`, `impressum.html` und `datenschutz.html`. Farbe über `fill:currentColor`, also weiß auf Schwarz.
  Im `<h1>` steht zusätzlich unsichtbar der Text „HTWerk“ (`.vh`) für Screenreader und Suchmaschinen.
- **Monogramm** (H mit Helm): Favicon, Touch-Icon und klein in der Fußzeile aller Seiten (`.mark`).

Der Pfad steht in allen fünf HTML-Dateien identisch. Bei einer Änderung am Logo überall ersetzen,
dazu `favicon.svg`, die beiden PNG-Icons, `images/og-image.jpg` und die zwei SVG-Dateien in `images/`.
Die Größe der Wortmarke im Titel regelt `.hero h1 svg` (Breite), in der Kopfzeile `.brand svg` (Höhe).

## Zweisprachigkeit (DE/EN)

- Jeder sichtbare Text steht doppelt: `<span lang="en">…</span><span lang="de">…</span>`
  im selben Element.
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

## Navigation

- Startseite: Mission, Team, Touren, Partner. Unter 23,5rem ohne „Team“.
- `unternehmen.html`: Bisherige Touren, So läuft es ab, Für Studierende (→ `index.html`), Kontakt.
  Unter 34rem nur „So läuft es ab“ und „Kontakt“, unter 26rem nur „Kontakt“.
- Die Leisten sollen einzeilig bleiben. Beim Ändern der Links die `nth-child`-Regeln anpassen.

## Anmeldung

Der Link zur Anmeldung steht an genau einer Stelle: in `index.html` im Abschnitt `#signup`
(Button „Register on Luma“). Er zeigt auf `https://luma.com/user/LinusRuesseler`.
Alle anderen Anmelde-Buttons führen zu `index.html#signup`.

## Bisherige Touren

- Die vier Rückblick-Seiten (`1komma5.html`, `siemens-energy.html`, `formlabs.html`, `bmw-motorrad.html`) wurden im
  Oktober 2026 auf Wunsch von Linus gelöscht (im Git-Verlauf noch vorhanden). Die Touren erscheinen nur noch im Slider.
- Jede Tour ist im Slider ein `<div class="visit">` mit Foto (`.photo`) und Firmenname (`.name h3`), ohne Link.
- Neue Tour: in `index.html` und `unternehmen.html` je einen weiteren `div.visit` in `.track` ergänzen.
- Die Galerie-Fotos der gelöschten Seiten liegen weiter in `images/bmw-motorrad/`, `images/formlabs/` und `images/1komma5/`,
  die Originale in `images/HTWerk/`. Sie werden nirgends verlinkt, sind aber öffentlich abrufbar.

## Offene Punkte

1. `impressum.html` und `datenschutz.html` sind live (Kopfzeile mit Wortmarke, `noindex`).
   Verantwortlich: Linus Rüsseler, Haubachstraße 40, 10585 Berlin, linus@htwerk.de (je Seite an zwei bzw. einer Stelle).
   Die Datenschutzerklärung beschreibt genau das, was die Seite tut: GitHub Pages, Cloudflare-DNS, keine Cookies,
   lokale Schriften, `htwerk-lang` nur nach Klick auf DE/EN, Links zu Luma und LinkedIn. Wenn sich daran etwas ändert
   (Formular, Analyse, eingebettete Inhalte) oder HTWerk ein Verein oder eine UG wird, beide Seiten anpassen.
2. (entfällt, Rückblick-Seiten gelöscht)
3. Einwilligung der abgebildeten Personen und Freigabe der Unternehmen für die Fotos klären.
4. Kontaktadresse auf allen Seiten: linus@htwerk.de (Oktober 2026, ersetzt die Hochschul-Adresse).
5. Logos oder Firmennamen unter „Partner“ erst nach schriftlicher Zustimmung der Firmen (Namensraster im Oktober 2026 auf Wunsch von Linus entfernt).
6. Die deutschen Texte wurden im Oktober 2026 überarbeitet. Linus sollte sie einmal gegenlesen,
   vor allem den neuen Claim und die Rollenbezeichnungen im Team.
6. Der Anmeldelink führt auf ein persönliches Luma-Profil. Ein eigener HTWerk-Kalender auf Luma
   oder der Link zur jeweils nächsten Veranstaltung wäre direkter.
7. Die nächste Tour (Firma, Datum, Plätze) wird auf der Seite noch nicht konkret genannt.
8. Im Team fehlt ein Mitglied, das nicht in der Präsentation stand. Teamfotos fehlen.

## Prüfen

Kein Test-Setup. Nach Änderungen die Seiten im Browser in beiden Sprachen und in
Handybreite (ca. 390 px) öffnen und auf horizontales Scrollen achten.
