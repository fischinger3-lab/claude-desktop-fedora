# Claude Desktop für Fedora

Inoffizieller Fedora-44-x86_64-Build der originalen Claude-Desktop-Anwendung.
Angepasste Paketierung auf Grundlage von [aaddrick/claude-desktop-debian](https://github.com/aaddrick/claude-desktop-debian).

## Downloads

[Neueste RPM- und AppImage-Dateien](https://github.com/fischinger3-lab/claude-desktop-fedora/releases/latest)
werden nach einem erfolgreichen automatischen Build veröffentlicht.

RPM im Downloadordner installieren:

```bash
sudo dnf install ./claude-desktop-unofficial-*.rpm
xdg-mime default claude-desktop-unofficial.desktop x-scheme-handler/claude
```

Das lokale RPM ist nicht signiert. Kein eigenes DNF-Repository ist eingerichtet;
Updates werden als neue Release-Downloads bereitgestellt.

## Update-Automatik

GitHub Actions prüft alle sechs Stunden und kann über **Actions → Fedora Updates → Run workflow** manuell gestartet werden.
Der Build lädt das neueste amd64-Debian-Originalpaket von `downloads.claude.ai`,
prüft Größe und SHA-256, wendet die vorhandenen Linux-Anpassungen an und erstellt
RPM und AppImage auf Fedora 44. Bereits veröffentlichte vollständige Versionen
werden übersprungen. Bei Fehlern bleibt die letzte veröffentlichte Version erhalten.

Vor Veröffentlichung werden Resolver-Tests, bestehende gezielte Shell-Tests,
RPM-Inhalt und Sandbox-Rechte sowie der AppImage-Versionsaufruf geprüft.
Ein erfolgreicher Build garantiert keine funktionierende GUI-Anmeldung oder
Cowork-Sitzung. Änderungen an der Originalanwendung können manuelle Anpassungen
der Patches erfordern.

## Quellcode

`fedora-build-source-v2.zip` enthält die Buildskripte, Anpassungen, Tests und die
MIT-/Apache-Lizenztexte der Buildskripte. Das proprietäre Claude-Programm ist
nicht im Quellarchiv enthalten; es wird beim Build vom Hersteller geladen.
Der Workflow prüft vor dem Entpacken die SHA-256-Prüfsumme dieses Archivs.
Die Quellcode-Lizenz gilt nicht für die proprietäre Claude-Anwendung.

Lokal bauen: Archiv in ein Verzeichnis ohne Leerzeichen entpacken,
`sudo dnf install rpm-build wget curl binutils tar xz zstd findutils nodejs npm`,
dann `bash build-fedora.sh`. Node mindestens 22.12; sonst wird ein lokaler
Node-Build heruntergeladen. Der npm-asar-Buildhelfer ist noch nicht fest
versioniert; vollständige bitgenaue Reproduzierbarkeit wird nicht zugesagt.

Geplante GitHub-Läufe können verzögert sein und bei längerer Repository-
Inaktivität deaktiviert werden. Der Workflow muss dann auf GitHub wieder
aktiviert werden. Keine Weitergabe persönlicher Tokens an die Buildskripte.

AppImage-Updates werden über die Release-Downloads verteilt; es ist keine automatische AppImage-Updatequelle eingebettet.
