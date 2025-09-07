# WordPress-Installation mit Webmin und Adminer in einem LXC-Container

Diese Anleitung beschreibt die Installation von WordPress, Webmin und Adminer in einem LXC-Container unter Ubuntu 22.04. Die Installation erfolgt in zwei Schritten: zunächst eine lokale Installation für das Netzwerk, gefolgt von einer optionalen Umstellung auf eine öffentliche Domain mit Reverse Proxy Manager.

## Vorbereitungen

1. Erstellen Sie einen LXC-Container mit Ubuntu 22.04.

## Installation

### Schritt 1: Lokale WordPress-Installation

2. Führen Sie das erste Script für die lokale Installation im neu erstellten LXC-Container aus:
   ```bash
   sudo ./main.sh
   ```
   
   Dieses Script:
   - Installiert alle benötigten Komponenten (Apache, MySQL, PHP, Webmin, Adminer)
   - Konfiguriert WordPress für den Zugriff im lokalen Netzwerk
   - Verwendet HTTP und die lokale IP-Adresse
   - Erstellt automatisch Datenbank und Benutzer
   - Konfiguriert Apache ohne Reverse Proxy Manager

### Schritt 2: Domain-Umstellung (Optional)

3. Falls Sie später auf eine öffentliche Domain umstellen möchten, führen Sie das zweite Script aus:
   ```bash
   sudo ./domain_setup.sh
   ```
   
   Dieses Script:
   - Stellt die bestehende lokale Installation auf eine öffentliche Domain um
   - Fragt nach der gewünschten Domain und dem Protokoll (HTTP/HTTPS)
   - Fragt ab, ob ein Reverse Proxy Manager verwendet wird
   - Konfiguriert Apache entsprechend (mit oder ohne Proxy-Unterstützung)
   - Aktualisiert die WordPress-Datenbank mit den neuen URLs
   - Erstellt automatisch Backups der alten Konfiguration

## Nachbereitung

4. Notieren und sichern Sie alle Informationen, die am Ende der Installation angezeigt werden.

## Zugriff

### Nach der lokalen Installation:
- **WordPress:** `http://[LOKALE-IP]`
- **WordPress Admin:** `http://[LOKALE-IP]/wp-admin`
- **Adminer:** `http://[LOKALE-IP]/adminer`
- **Webmin:** `http://[LOKALE-IP]:10000`

### Nach der Domain-Umstellung:
- **WordPress:** `https://[IHRE-DOMAIN]` (oder HTTP, je nach Konfiguration)
- **WordPress Admin:** `https://[IHRE-DOMAIN]/wp-admin`
- **Adminer:** `https://[IHRE-DOMAIN]/adminer`
- **Webmin:** `http://[LOKALE-IP]:10000` (bleibt lokal)

## Wichtige Hinweise

- **Reihenfolge beachten:** Führen Sie zuerst `main.sh` aus, dann optional `domain_setup.sh`
- **Root-Berechtigung:** Beide Scripts müssen als root ausgeführt werden (sudo)
- **SSL-Zertifikate:** Bei HTTPS ohne Reverse Proxy müssen Sie zusätzlich SSL-Zertifikate konfigurieren
