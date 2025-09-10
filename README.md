# Secure QR Generator (JS-only, GitHub Pages)

Ein leichter, statischer QR-Code-Generator mit AES‑GCM‑verschlüsselten Redirect-Links.

## Features
- **JS-only** (kein Backend), ideal für GitHub Pages
- **AES‑GCM**-Verschlüsselung des Payloads (?r=...)
- **Optionales Passwort** + Ablaufdatum pro Link
- **Admin UI** unter `/#/missioncontrol` mit Login-View (lokaler SHA‑256‑Hash)
- **QR‑Preview** und **Downloads** (PNG/JPG/WEBP, frei wählbare Größe)
- **Kein sichtbarer Link** von der Passwortseite zum Admin

## Quickstart
1. Repo klonen / auf Pages deployen.
2. Im Code **APP_MASTER_SECRET** durch einen langen, zufälligen Secret-String ersetzen.
3. `/#/missioncontrol` öffnen, Admin-Passwort setzen (Button „Admin‑Passwort setzen“).
4. Ziel‑URL + Optionen wählen → „Link & QR generieren“ → QR herunterladen/kopieren.

## Sicherheit
- Verschlüsselung mit **AES‑GCM (256 bit)** über die WebCrypto API.
- Admin‑Passwort wird als **SHA‑256 (hex)** lokal im `localStorage` gespeichert.
- Die Passwörter für geschützte Links werden als **salted SHA‑256** (Client-seitig) im Payload abgelegt.
- **Wichtig:** `APP_MASTER_SECRET` ist der zentrale Schlüssel für *alle* Payloads. Wähle einen sehr langen, zufälligen Wert und ändere ihn nicht nach Live‑Gang (sonst können alte Links nicht mehr entschlüsselt werden).

## Routen
- **Start:** `/` – Landing
- **Admin:** `/#/missioncontrol` – Login-View → Admin-Konsole
- **Redirect:** `/?r=ENC_PAYLOAD` – öffnet ggf. Passwortdialog und leitet zum Ziel weiter

## Entwicklung
- Lokal mit einem simplen HTTP-Server starten (z. B. `python3 -m http.server`), **nicht** `file://`.
- Der QR-Renderer nutzt **davidshimjs/qrcodejs** per `qrcode.min.js` im selben Ordner.

## Anpassung
- Farben/Themes in `<style>` anpassen.
- Admin-Login-View in `#view-admin-login` (HTML) + Routing in `init()`.
- Downloadformate in `downloadQR(...)`.

## Lizenz
MIT (siehe Original-Lizenz von davidshimjs/qrcodejs für die QR-Render-Bibliothek).
