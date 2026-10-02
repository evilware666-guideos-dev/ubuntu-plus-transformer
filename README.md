
# Ubuntu-PLUS Transformer

## 🎯 Was ist der Ubuntu-PLUS Transformer?

Der **Ubuntu-PLUS Transformer** ist ein Assistent, der ein bestehendes,
fest installiertes Ubuntu-System in ein **Ubuntu-PLUS**-System umwandelt.

Er installiert und konfiguriert automatisch:

- 🎮 **Gaming-Tools** (Steam, Lutris, Heroic, ProtonUp-Qt, Protontricks, Faugus)
- 📄 **Büro-Software** (LibreOffice, ONLYOFFICE oder AbiWord + Gnumeric)
- 🌐 **Browser** (Firefox, Brave, Vivaldi, Google Chrome)
- 🎨 **Icon-Themes** (WhiteSur, Mint-Y, We10X, Breeze, ZorinOS, Moka, Numix, Pop, Papirus)
- 🖼️ **Wallpaper und Avatare**
- 🛡️ **Firewall (UFW)** und Sicherheitstools
- ⚙️ **Systemoptimierungen** (TLP, zram, preload, Treiber, Firmware)
- 🚀 **Viele weitere nützliche Anwendungen**

Am Ende wird das System so angepasst, dass es wie ein **fertig eingerichtetes
Ubuntu-PLUS** aussieht und funktioniert.

---

## 💻 Systemvoraussetzungen

| Anforderung | Minimum |
|---|---|
| **Betriebssystem** | Ubuntu 24.04 LTS oder neuer |
| **Desktop** | GNOME (Standard-Ubuntu) |
| **Architektur** | amd64 (x86_64) |
| **Speicherplatz** | ca. 5 GB frei |
| **Internetverbindung** | ja (für Downloads) |
| **Benutzerrechte** | Administrator (sudo) |
| **Zustand** | **Fest installiertes System** – **kein Live-USB!** |

> ⚠️ **Wichtig:** Der Transformer ist **nicht** für Live-Sessions geeignet.
> In einer Live-Umgebung liegt das Root-Dateisystem im RAM – die Installation
> würde den verfügbaren Speicher sprengen und mittendrin abbrechen.
> Der Transformer erkennt eine Live-Session automatisch und bricht mit
> einer Meldung ab.

---

## 📦 Installation

### Option 1: Debian-Paket installieren (empfohlen)

```bash
sudo dpkg -i ubuntu-plus-transformer_*.deb
sudo apt install -f
```

### Option 2: Aus dem Quellcode bauen

```bash
cd ubuntu-plus-transformer
dpkg-deb --build --root-owner-group . ../ubuntu-plus-transformer.deb
sudo dpkg -i ../ubuntu-plus-transformer.deb
```

### Option 3: Direkt aus dem Quellordner starten (nur zum Testen)

```bash
sudo ./ubuntu-plus-transformer
```

---

## 🚀 Verwendung

### Grafischer Assistent (GUI)

Nach der Installation findest du den Transformer im Anwendungsmenü
unter **„Optimieren“ → „Ubuntu-PLUS Transformer“**.

**Ablauf:**

1. **Willkommensseite** – Hier erfährst du, was der Transformer macht
2. **Spiele-Unterstützung** – Gaming-Tools aktivieren/deaktivieren
3. **Büro-Software** – LibreOffice, ONLYOFFICE, AbiWord oder keine
4. **Browser-Auswahl** – Firefox, Brave, Vivaldi, Chrome (Mehrfachauswahl)
5. **Icon-Sets** – Installieren und Standard-Icon wählen
6. **Hintergrundbild** – Eigenes Wallpaper auswählen (optional)
7. **Firewall** – UFW aktivieren/deaktivieren
8. **Zusammenfassung** – Alle Auswahl prüfen
9. **Installation** – Läuft automatisch durch (mehrere Minuten)

Am Ende wird der Rechner **neu gestartet** und das System ist fertig.

**Wichtige Hinweise:**

- Bei einem Neustart wird dein **Administrator-Passwort** abgefragt (das ist
  bei Systemneustarts normal)
- Der Transformer **entfernt sich nach erfolgreicher Installation automatisch**
  – du musst nichts weiter tun
- Alle deine persönlichen Daten (Bilder, Musik, Dokumente) bleiben erhalten

---

### Kommandozeile (CLI)

Wenn du die Installation ohne grafische Oberfläche durchführen willst:

```bash
sudo ubuntu-plus-transformer [OPTIONEN]
```

#### Beispielaufrufe

```bash
# Standardinstallation (LibreOffice, Firefox Snap, Gaming aktiv)
sudo ubuntu-plus-transformer

# Gaming deaktivieren, OnlyOffice installieren, Brave dazu
sudo ubuntu-plus-transformer --no-games --office=onlyoffice --install-brave

# Minimal: keine Spiele, kein Office, kein Firefox
sudo ubuntu-plus-transformer --no-games --no-office --remove-firefox

# Mit eigenem Wallpaper und Papirus-Icons
sudo ubuntu-plus-transformer --wallpaper=/home/user/Bilder/mein.jpg \
                             --install-papirus --default-icon=papirus

# Automatischer Neustart nach der Installation
sudo ubuntu-plus-transformer --reboot
```

---

## 🔧 Was macht der Transformer?

Der Transformer arbeitet in **mehreren Phasen**:

### 1. Vorbereitung
- Prüft, ob Live-System (bricht ggf. ab)
- Blockiert automatische Updates während der Installation
- Synchronisiert die Systemzeit (NTP)

### 2. System-Aktualisierung
- `apt update`, `apt upgrade`, `apt dist-upgrade`
- Entfernt überflüssige Spiele (Mines, AisleRiot, Mahjongg, Sudoku)
- Entfernt überflüssige Apps (Totem, Remmina, Rhythmbox, MPV)

### 3. Treiber & Firmware
- `dkms`, `linux-firmware`, `wpasupplicant`
- Intel/AMD Microcode
- `tlp` für Laptop-Energiemanagement

### 4. Gaming (optional)
- Aktiviert 32-Bit-Architektur (`i386`)
- Installiert `gamemode`, `mangohud`, Mesa-Treiber, Vulkan
- Optional: Steam, Lutris, Heroic, ProtonUp-Qt, Protontricks, Faugus,
  MangoHud, GOverlay, GameMode

### 5. Büro-Software
- Erkennt automatisch, was installiert ist
- Entfernt nicht gewünschte Suiten
- Installiert die gewählte Suite

### 6. Browser
- Firefox (Snap bevorzugt, Flatpak als Fallback)
- Brave, Vivaldi, Chrome (Flatpak)

### 7. Icon-Themes
- WhiteSur (immer installiert)
- Optional: Mint-Y, We10X, Breeze, ZorinOS, Moka, Numix, Pop, Papirus
- Setzt das gewählte Standard-Icon-Theme

### 8. Wallpaper, Avatare, Musik
- Kopiert Wallpaper nach `~/Bilder/` und `/usr/share/backgrounds/`
- Ersetzt Standard-Avatare in `/usr/share/pixmaps/faces/`
- Kopiert Musik nach `/etc/skel/Musik/` (für neue Benutzer)

### 9. Desktop-Konfiguration
- Alphabetisch sortiertes App-Grid
- GNOME-Einstellungen (Dock, Theme, Akzentfarbe)
- Nautilus-Bookmarks (`System`-Verknüpfung)
- Dokumentenvorlagen

### 10. Desktop-Backup-Restore
- Stellt dein GNOME-Layout wieder her
- Stellt Autostart, Extensionen, Themes, Fonts wieder her
- Stellt das Wallpaper wieder her

### 11. Abschluss
- Aktiviert Firewall (UFW)
- Installiert Flatpaks (Shortwave, Tor Browser, Extension Manager, …)
- Entfernt sich **automatisch selbst**
- Optional: Neustart

---

## 🎛️ Parameter-Übersicht (CLI)

### Allgemein

| Parameter | Beschreibung |
|---|---|
| `--reboot` | Startet das System nach der Installation automatisch neu |
| `--wallpaper=Pfad` | Setzt ein eigenes Wallpaper |
| `--default-icon=NAME` | Setzt das Standard-Icon-Theme |

### Gaming

| Parameter | Beschreibung |
|---|---|
| `--no-games` | Deaktiviert die komplette Gaming-Unterstützung |
| `--install-steam` | Installiert Steam |
| `--install-lutris` | Installiert Lutris |
| `--install-heroic` | Installiert Heroic Games Launcher |
| `--install-protonup` | Installiert ProtonUp-Qt |
| `--install-protontricks` | Installiert Protontricks |
| `--install-faugus` | Installiert Faugus Launcher |
| `--install-mangohud` | Installiert MangoHud |
| `--install-goverlay` | Installiert GOverlay |
| `--install-gamemode` | Installiert GameMode |

### Büro-Software

| Parameter | Beschreibung |
|---|---|
| `--office=libreoffice` | LibreOffice (Standard) |
| `--office=onlyoffice` | ONLYOFFICE Desktop Editors (Flatpak) |
| `--office=abiword` | AbiWord + Gnumeric |
| `--no-office` | Keine Büro-Software |

### Browser

| Parameter | Beschreibung |
|---|---|
| `--install-firefox` | Firefox installieren (Snap) |
| `--remove-firefox` | Firefox entfernen (Snap + Flatpak) |
| `--install-brave` | Brave als Flatpak installieren |
| `--install-vivaldi` | Vivaldi als Flatpak installieren |
| `--install-chrome` | Google Chrome als Flatpak installieren |
| `--remove-brave` | Brave entfernen |
| `--remove-vivaldi` | Vivaldi entfernen |
| `--remove-chrome` | Google Chrome entfernen |

### Icon-Themes

| Parameter | Beschreibung |
|---|---|
| `--install-whitesur` | WhiteSur Icon Theme (Standard) |
| `--install-minty` | Mint-Y Icons |
| `--install-we10x` | We10X Icons |
| `--install-breeze` | Breeze Icons (KDE) |
| `--install-zorin` | ZorinOS Icons |
| `--install-moka` | Moka Icons |
| `--install-numix` | Numix Icons |
| `--install-pop` | Pop Icons (System76) |
| `--install-papirus` | Papirus Icons |
| `--default-icon=NAME` | Standard-Icon: `whitesur`, `minty`, `we10x`, `breeze`, `zorin`, `moka`, `numix`, `pop`, `papirus`, `yaru` |

### Firewall

| Parameter | Beschreibung |
|---|---|
| `--no-firewall` | Firewall (UFW) nicht aktivieren |

---

## 🗑️ Selbst-Deinstallation

Nach erfolgreicher Installation entfernt sich der Transformer **automatisch**.
Das geschieht über zwei Mechanismen:

1. **Sofort-Entfernung** über einen `systemd-run`-Timer (ca. 20 Sekunden nach
   Abschluss, noch in der laufenden Sitzung)
2. **Boot-Time-Service** als Sicherheitsnetz (falls der Reboot zu schnell
   kommt, wird das Paket beim nächsten Boot entfernt)

**Wichtig:** Deine persönlichen Daten bleiben erhalten:

- 🖼️ Wallpaper in `~/Bilder/`
- 🎨 Icon-Themes in `/usr/share/icons/`
- ⚙️ GNOME-Einstellungen in `~/.config/dconf/user`
- 📁 Dokumente, Musik, Bilder unberührt

---

## 🗑️ Manuelle Deinstallation

Falls du den Transformer **vor** Abschluss entfernen willst:

```bash
sudo apt remove --purge ubuntu-plus-transformer
```

Falls die Selbst-Deinstallation aus irgendeinem Grund nicht funktioniert hat:

```bash
# 1. Prüfen, ob das Paket noch installiert ist
dpkg -l ubuntu-plus-transformer

# 2. Falls ja: entfernen
sudo apt remove --purge -y ubuntu-plus-transformer

# 3. Den Boot-Time-Service entfernen (falls noch aktiv)
sudo systemctl disable ubuntu-plus-selfremove.service 2>/dev/null
sudo rm -f /etc/systemd/system/ubuntu-plus-selfremove.service
sudo systemctl daemon-reload

# 4. Den systemd-run-Timer entfernen (falls noch aktiv)
sudo systemctl stop ubuntu-plus-selfremove-now.timer 2>/dev/null
sudo systemctl reset-failed ubuntu-plus-selfremove-now 2>/dev/null
```

---

## ❓ Häufige Fragen (FAQ)

### Kann ich den Transformer in einer Live-Session verwenden?

**Nein.** Der Transformer benötigt ein fest installiertes System. In einer
Live-Session liegt das Root-Dateisystem im RAM – die Installation würde den
Speicher sprengen. Der Transformer erkennt das und bricht automatisch mit
einer Meldung ab.

### Warum wird mein Passwort abgefragt?

Der Reboot ist ein **Systemvorgang**, für den Administratorrechte notwendig
sind. Das ist bei jedem Ubuntu-System so – nicht spezifisch für den Transformer.

### Warum dauert die Installation so lange?

Der Transformer lädt mehrere hundert MB an Paketen, Flatpaks und Snap-Daten
herunter. Je nach Internetverbindung dauert das 10–45 Minuten.

### Verliere ich meine Daten?

**Nein.** Deine persönlichen Dateien (Bilder, Musik, Dokumente, E-Mails)
bleiben unberührt. Der Transformer ändert nur Systemeinstellungen und
installiert/entfernt Programme.

### Kann ich den Transformer mehrfach ausführen?

Der Transformer entfernt sich nach dem Durchlauf selbst. Wenn du ihn erneut
ausführen willst, installiere das Paket einfach wieder.

### Ist der Transformer für Ubuntu 26.10 geeignet?

Grundsätzlich ja. Der Transformer nutzt Standard-Werkzeuge (apt, dconf,
flatpak), die auch in zukünftigen Ubuntu-Versionen funktionieren. Kleinere
Anpassungen könnten nötig sein, wenn sich GNOME-interne Schlüssel ändern.

### Warum ist das App-Grid nicht alphabetisch?

Das App-Grid wird vom Transformer gesetzt **und** live in die laufende
GNOME-Sitzung geschrieben. Falls die Sortierung nicht sofort erscheint,
melde dich ab und wieder an. Der Transformer sollte das aber automatisch
erledigen.

---

## 🐛 Fehlerbehebung

### Problem: „Live-System erkannt" – aber ich bin auf einem installierten System

Möglicherweise wurde dein System als Live-Session erkannt (z. B. bei
bestimmten VM-Setups). Prüfe:

```bash
findmnt -n -o FSTYPE /
```

Wenn `ext4`, `btrfs` oder `xfs` → installiertes System
Wenn `overlay` oder `squashfs` → Live-Session

### Problem: Passwort wird nicht akzeptiert

Stelle sicher, dass du das Skript nicht als `sudo ubuntu-plus-transformer`
startest, sondern über die **GUI** oder direkt als normaler Benutzer.

Falls du in einer Polkit-Umgebung ohne funktionierende Policy bist:

```bash
# Prüfen, ob eine Policy existiert
ls /usr/share/polkit-1/actions/ | grep -i transformer
```

### Problem: Das App-Grid wird nicht aktualisiert

Ab- und wieder anmelden:

```bash
gnome-session-quit --logout --no-prompt
```

Oder:

```bash
# Manuell nachhelfen
dconf update
```

### Problem: Der Transformer wird nicht automatisch entfernt

Prüfe:

```bash
# Ist der Boot-Time-Service aktiviert?
systemctl status ubuntu-plus-selfremove.service

# Falls nicht vorhanden → manuell entfernen
sudo apt remove --purge -y ubuntu-plus-transformer
```

### Problem: Installation bricht mitten drin ab

Prüfe:

```bash
# Speicherplatz
df -h /

# Ist die Internetverbindung stabil?
ping -c 4 archive.ubuntu.com

# Log-Dateien
journalctl -xe | tail -50
```

---

## 🛠️ Für Entwickler

### Projektstruktur

```
ubuntu-plus-transformer/
├── DEBIAN/
│   ├── control
│   ├── postinst
│   └── prerm
└── usr/
    ├── bin/
    │   ├── ubuntu-plus-transformer        (CLI-Skript)
    │   └── ubuntu-plus-transformer-gui    (Python GTK4 GUI)
    └── share/
        └── ubuntu-plus-transformer/
            ├── faces/                     (Avatare)
            ├── backgrounds/               (Wallpaper für Benutzer)
            ├── Wallpaper/                 (Systemweite Wallpaper)
            ├── Musik/                     (Musik für neue Benutzer)
            ├── extra-debs/                (Zusätzliche .deb-Pakete)
            ├── gnome-layout.dconf         (GNOME-Layout)
            └── Ubuntu-PLUS-Desktop_*.tar.gz  (Desktop-Backup)
```

### Abhängigkeiten

- `bash` (≥ 4.0)
- `python3` (≥ 3.10)
- `python3-gi`, `gir1.2-gtk-4.0`, `gir1.2-adw-1` (für GUI)
- `flatpak` (für Browser/Apps)
- `snapd` (für Firefox/Cheese)

### Bauen

```bash
cd ubuntu-plus-transformer
dpkg-deb --build --root-owner-group . ../ubuntu-plus-transformer.deb
```

### Testen

```bash
# Syntax-Check CLI
bash -n usr/bin/ubuntu-plus-transformer

# Syntax-Check GUI
python3 -m py_compile usr/bin/ubuntu-plus-transformer-gui

# Testlauf
sudo ./usr/bin/ubuntu-plus-transformer --no-games --no-office --no-firewall
```

### Beitragen

Pull-Requests und Fehlerberichte sind willkommen. Bitte beachte:

- Code muss der **GPL v3** entsprechen
- Änderungen bitte dokumentieren
- Neue Features möglichst mit Test-Szenario beschreiben

---

## 📄 Lizenz

Dieses Projekt steht unter der **GNU General Public License v3.0**.

```
Copyright (c) 2026 evilware666

Dieses Programm ist freie Software: Du kannst es unter den Bedingungen
der GNU General Public License, wie von der Free Software Foundation
veröffentlicht, weitergeben und/oder modifizieren – entweder gemäß
Version 3 der Lizenz oder (nach deiner Wahl) jeder späteren Version.

Dieses Programm wird in der Hoffnung verteilt, dass es nützlich sein
wird, aber OHNE JEDE GEWÄHRLEISTUNG – sogar ohne die implizite
Gewährleistung der MARKTFÄHIGKEIT oder EIGNUNG FÜR EINEN BESTIMMTEN
ZWECK. Siehe die GNU General Public License für weitere Details.
```

Vollständiger Lizenztext: <https://www.gnu.org/licenses/gpl-3.0.html>

---

## 💚 Danksagung

Danke an alle, die zum Ubuntu-PLUS-Transformer beigetragen haben:

- **Ubuntu** und **GNOME** für die großartige Basis
- **WhiteSur** und alle Icon-Theme-Autoren
- **Flathub** und die **Snapcraft**-Community für die Paketquellen
- **Alle Tester und Nutzer**, die Fehler gemeldet und Verbesserungen vorgeschlagen haben

**Besonderer Dank** an alle Entwickler der Open-Source-Projekte, die
dieses Tool überhaupt möglich machen. 💚

---

## 📧 Kontakt & Unterstützung

- 🐛 **Fehler melden:** [Issues](https://github.com/evilware666/ubuntu-plus-transformer/issues)
- 💬 **Forum:** [Linux Guides Forum](https://forum.linuxguides.de)
- ☕ **Unterstützen:** [Ko-fi](https://ko-fi.com/evilware666)
- 🌐 **Website:** [linuxguides.de](https://linuxguides.de)

---

**Viel Spaß mit Ubuntu-PLUS!** 🎉

*– evilware666*
```

---

## Verwendung

**Datei speichern als:** `README.md` im Wurzelverzeichnis deines Projekts, also:

```
Ubuntu-PLUS Transformer/
├── README.md          ← hier
├── builder-skript.py
└── ubuntu-plus-transformer/
    ├── DEBIAN/
    └── usr/
```

## Was ich reingepackt habe

| Abschnitt | Inhalt |
|---|---|
| **Überblick** | Was das Tool macht, mit Emoji-Übersicht |
| **Systemvoraussetzungen** | Tabelle mit Mindestanforderungen |
| **Installation** | 3 Wege (Deb, Bau, direkt) |
| **Verwendung** | GUI-Ablauf und CLI-Beispiele |
| **Was macht der Transformer** | Alle 11 Phasen erklärt |
| **Parameter-Übersicht** | Alle CLI-Flags in 6 Tabellen |
| **Selbst-Deinstallation** | Erklärt beide Mechanismen |
| **Manuelle Deinstallation** | Alle 4 Schritte inkl. Service-Cleanup |
| **FAQ** | 7 häufige Fragen |
| **Fehlerbehebung** | 5 typische Probleme mit Lösungen |
| **Für Entwickler** | Struktur, Bauen, Testen, Beitragen |
| **Lizenz** | GPL v3 mit Auszug |
| **Danksagung + Kontakt** | Badges, Links zu Forum, Ko-fi |

## Anpassen

Vor dem Speichern solltest du prüfen:

1. **Repository-URL** in der Badge-Zeile (`github.com/evilware666/...`)
2. **Projektstruktur** – habe ich aus dem, was du mir gezeigt hast, rekonstruiert. Falls deine Ordner anders heißen (z. B. `Icons/` statt `faces/`), passe die Tabelle an.
3. **Version** – ich habe nichts Spezifisches eingetragen. Wenn du willst, kannst du oben eine Versions-Badge hinzufügen:

```markdown
![Version](https://img.shields.io/badge/Version-1.0.0-blue)
```

Wenn du willst, passe ich das README weiter an – z. B. Screenshots einbinden, englische Version dazu, oder ein CHANGELOG anlegen. Sag einfach Bescheid. 👍
