# Secure QR Generator (JS‑only)

Ein schlanker, statischer QR‑Code‑Generator mit geschützten Weiterleitungs‑Links.


## Nutzung

1. **Admin‑Login**: `/#/missioncontrol` öffnen, einloggen.
2. **QR erstellen**: Generator‑URL (Standard: aktuelle URL), Ziel‑URL, Passwort (optional), Ablaufdatum (optional) setzen.
3. **Link kopieren** und **QR herunterladen** (Format/Größe nach Bedarf).
4. Beim Scannen führt der Link zur Generator‑Seite, fragt ggf. ein Passwort ab und leitet dann zum Ziel weiter.

---

## Features (Kurzüberblick)

* Admin‑Bereich unter `/#/missioncontrol`
* Links mit optionalem Passwort & Ablaufdatum
* QR‑Vorschau, Größenwahl, Download (PNG/JPG/WEBP/SVG)
* Für statisches Hosting optimiert (Hash‑Routing)

---

## Schnellstart

1. **Repository klonen** (lokal oder GitHub Pages).
2. Datei öffnen und im Kopf des Skripts folgende Werte anpassen:

   * `APP_MASTER_SECRET` → langer zufälliger String (mind. 64 hex Zeichen) - Generieren z.B. über https://jwtsecrets.com/#generator mit 512 Bits.
   * (Optional) `DEFAULT_ADMIN_PASS_SHA256` → SHA‑256 Hash des gewünschten Admin‑Passworts - Generator: https://emn178.github.io/online-tools/sha256.html
3. Seite aufrufen und `/#/missioncontrol` öffnen.
4. Im Admin‑Bereich ggf. „**Admin‑Passwort setzen**“ verwenden um ein Wunschpasswort festzulegen -> danach neu einloggen. ABER: Das gilt nur lokal und nur solange der Local Storage Eintrag existiert!
5. Ziel‑URL eintragen, optional Passwort/Ablauf, **„Link & QR generieren“** klicken.

> **Tipp:** Für stabil scannbare Codes kurze Generator‑URL verwenden (z. B. eigene Kurzdomain) und den Export‑QR **mind. 320 px** bzw. **25–30 mm** Kantenlänge drucken.

---

> **Hinweis zur Sicherheit**
>
> Die Daten werden clientseitig verschleiert und vor Manipulation geschützt. Da der Code öffentlich auslieferbar ist, kann der Schlüsselableitungsprozess grundsätzlich nachvollzogen werden.

---

## Anpassen

### Branding & UI

* Farben/Schrift im `<style>`‑Block ändern (`--brand`, `--brand-2`, Hintergrundverläufe).
* Logo/Badge oben links sind reine SVG/HTML – frei austauschbar.
* QR‑Theme ist auf **schwarz/weiß** voreingestellt (beste Scanbarkeit). Wenn dunkle Themes gewünscht sind, bitte starken Kontrast sicherstellen.

### Routing & Pfade

* Admin‑Bereich: `/#/missioncontrol` (Hash‑Route, funktioniert auf statischem Hosting).
* Direkter Aufruf `/missioncontrol` wird automatisch auf die Hash‑Route umgeschrieben.

### QR‑Größe & Lesbarkeit

* Vorschaugröße ist **dynamisch** abhängig von der Linklänge.
* Fehlerkorrektur-Level ist bewusst niedrig gehalten, um weniger Module zu erzeugen (bessere Erkennung auf manchen Android‑Scannern).
* Exportgrößen unter „Live‑Vorschau → Größe“ (Standardeinstellung 512 px) wählbar.

### Downloads

* PNG/JPG/WEBP/SVG verfügbar.

---

## Fehlerbehebung

* **QR wird auf manchen Android‑Geräten schlecht erkannt**: QR größer exportieren (≥ 320 px), ausreichende Beleuchtung, Druckqualität prüfen, **starker Kontrast (schwarz/weiß)** nutzen, zu lange Links vermeiden (Kurzdomain verwenden).
* **„qrcode is not defined“**: Prüfen, ob `qrcode.min.js` im selben Ordner liegt und in der Seite vor dem App‑Script geladen wird.
* **Beim Generieren: „Fehler … (Verschlüsselung/Render)“**: `APP_MASTER_SECRET` gesetzt? Browser‑Konsole prüfen.
* **Admin‑Login erscheint nicht**: Seite über Hash‑Route `/#/missioncontrol` öffnen, nicht über `/missioncontrol`.

---

## Lizenz

* Frontend‑Code: MIT
* QR‑Renderer: basiert auf **qrcode.js** (MIT) – Datei `qrcode.min.js`
