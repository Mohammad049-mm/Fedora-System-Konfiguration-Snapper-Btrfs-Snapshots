# Fedora System-Konfiguration: Snapper Btrfs-Snapshots

Anleitung zur Einrichtung von Snapper unter Fedora für automatische und manuelle System-Wiederherstellungspunkte auf Btrfs-Dateisystemen.

---

## 🗄️ Snapper für Btrfs-Snapshots einrichten

Mit Snapper lassen sich unter Fedora automatische und manuelle Snapshots des Btrfs-Dateisystems erstellen. Durch das DNF-Plugin wird zudem vor und nach jeder Paketinstallation automatisch ein Wiederherstellungspunkt generiert.

### 1. Installation
Installiere Snapper zusammen mit dem passenden Plugin für den DNF-Paketmanager:
```bash
sudo dnf install snapper python3-dnf-plugin-snapper
```

### 2. Konfiguration erstellen
Erstelle eine neue Snapper-Konfiguration mit dem Namen `root` für das Hauptverzeichnis (`/`):
```bash
sudo snapper -c root create-config /
```

### 3. Btrfs Quotas aktivieren
Aktiviere die Speicherplatz-Quoten (Quotas) für Btrfs. Dies ist zwingend erforderlich, damit Snapper den belegten Speicherplatz der einzelnen Snapshots korrekt berechnen und verwalten kann:
```bash
sudo btrfs quota enable /
```

### 4. Ersten Snapshot erstellen
Erstelle manuell deinen ersten permanenten System-Wiederherstellungspunkt mit einer passenden Beschreibung:
```bash
sudo snapper -c root create -d "Mein erster Wiederherstellungspunkt"
```

### 5. Snapshots überprüfen
Liste alle aktuell auf dem System vorhandenen Snapshots auf, um zu sehen, ob die Erstellung erfolgreich war:
```bash
sudo snapper ls
```
