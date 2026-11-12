# RDQRCODE – Datei-Eingang für RetroDesk 2

RDQR.EXE zeigt einen QR-Code mit einer Adresse. Das Smartphone scannt ihn, öffnet im Browser eine kleine Upload-Seite, und die gewählte Datei landet auf dem Retro-PC im Zielordner (Datei > Zielordner, Vorgabe `EINGANG`, gespeichert in RD2.INI unter `[QR] Ordner=`).

- Läuft unter RetroDesk 2 (ab API 2.1) mit Netzwerk (RDTCP.MOD aus RD2).
- Kleiner HTTP-Server auf Port 80, Schlüssel aus 4 Zeichen in der Adresse, neu bei jedem Start.
- Nur HTTP, für das Heimnetz gedacht.

## Installation
`RDQR.EXE` in den RD2-Ordner kopieren (z. B. `C:\RD2`) und per Doppelklick starten.

## Bauen
Quellen in `src/`. Gebaut wird im RetroDesk-2-Baum (github.com/Karre-ops/RetroDesk2) mit Open Watcom:
`src/` nach `apps/net/` kopieren, dann in `build.sh`:
```
wcc -0 -mm -os -s -zq -w4 -bt=dos -zl -i=sdk -fo=obj/qr_QR.obj apps/net/QR.C && APPOBJ=",obj/qr_QR.obj" app apps/net/RDQR.C RDQR.EXE "Datei-Eingang"
```
Tests: `test/qr_kern.sh` (QR-Erzeuger mit gcc und OpenCV), `test/rdqr.sh` (QEMU mit NE2000).

Lizenz: GPL v2 oder später (siehe COPYING).
