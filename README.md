    <h1>WordPress-Installation mit Webmin und Adminer in einem LXC-Container</h1>
    
    <p>Diese Anleitung beschreibt die Installation von WordPress, Webmin und Adminer in einem LXC-Container unter Ubuntu 22.04. Die Installation erfolgt in zwei Schritten: zunächst eine lokale Installation für das Netzwerk, gefolgt von einer optionalen Umstellung auf eine öffentliche Domain mit Reverse Proxy Manager.</p>

    <h2>Vorbereitungen</h2>
    <ol>
        <li>Erstellen Sie einen LXC-Container mit Ubuntu 22.04.</li>
    </ol>

    <h2>Installation</h2>

    <h3>Schritt 1: Lokale WordPress-Installation</h3>
    <ol start="2">
        <li>Führen Sie das erste Script für die lokale Installation im neu erstellten LXC-Container aus:
            <pre><code>sudo ./wordpress_local_install.sh</code></pre>
            
            Dieses Script:
            <ul>
                <li>Installiert alle benötigten Komponenten (Apache, MySQL, PHP, Webmin, Adminer)</li>
                <li>Konfiguriert WordPress für den Zugriff im lokalen Netzwerk (z.B. 192.168.178.3)</li>
                <li>Verwendet HTTP und die lokale IP-Adresse</li>
                <li>Erstellt automatisch Datenbank und Benutzer</li>
                <li>Konfiguriert Apache ohne Reverse Proxy Manager</li>
            </ul>
        </li>
    </ol>

    <h3>Schritt 2: Domain-Umstellung (Optional)</h3>
    <ol start="3">
        <li>Falls Sie später auf eine öffentliche Domain umstellen möchten, führen Sie das zweite Script aus:
            <pre><code>sudo ./wordpress_domain_setup.sh</code></pre>
            
            Dieses Script:
            <ul>
                <li>Stellt die bestehende lokale Installation auf eine öffentliche Domain um</li>
                <li>Fragt nach der gewünschten Domain und dem Protokoll (HTTP/HTTPS)</li>
                <li>Fragt ab, ob ein Reverse Proxy Manager verwendet wird</li>
                <li>Konfiguriert Apache entsprechend (mit oder ohne Proxy-Unterstützung)</li>
                <li>Aktualisiert die WordPress-Datenbank mit den neuen URLs</li>
                <li>Erstellt automatisch Backups der alten Konfiguration</li>
            </ul>
        </li>
    </ol>

    <h2>Nachbereitung</h2>
    <ol start="4">
        <li>Notieren und sichern Sie alle Informationen, die am Ende der Installation angezeigt werden.</li>
    </ol>

    <h2>Zugriff</h2>

    <h3>Nach der lokalen Installation:</h3>
    <ul>
        <li><strong>WordPress:</strong> <code>http://[LOKALE-IP]</code></li>
        <li><strong>WordPress Admin:</strong> <code>http://[LOKALE-IP]/wp-admin</code></li>
        <li><strong>Adminer:</strong> <code>http://[LOKALE-IP]/adminer</code></li>
        <li><strong>Webmin:</strong> <code>http://[LOKALE-IP]:10000</code></li>
    </ul>

    <h3>Nach der Domain-Umstellung:</h3>
    <ul>
        <li><strong>WordPress:</strong> <code>https://[IHRE-DOMAIN]</code> (oder HTTP, je nach Konfiguration )</li>
        <li><strong>WordPress Admin:</strong> <code>https://[IHRE-DOMAIN]/wp-admin</code></li>
        <li><strong>Adminer:</strong> <code>https://[IHRE-DOMAIN]/adminer</code></li>
        <li><strong>Webmin:</strong> <code>http://[LOKALE-IP]:10000</code> (bleibt lokal )</li>
    </ul>

    <h2>Wichtige Hinweise</h2>
    <ul>
        <li><strong>Reihenfolge beachten:</strong> Führen Sie zuerst <code>wordpress_local_install.sh</code> aus, dann optional <code>wordpress_domain_setup.sh</code></li>
        <li><strong>Root-Berechtigung:</strong> Beide Scripts müssen als root ausgeführt werden (sudo)</li>
        <li><strong>Backup:</strong> Das Domain-Setup-Script erstellt automatisch Backups der alten Konfiguration</li>
        <li><strong>SSL-Zertifikate:</strong> Bei HTTPS ohne Reverse Proxy müssen Sie zusätzlich SSL-Zertifikate konfigurieren</li>
        <li><strong>Reverse Proxy:</strong> Das zweite Script unterstützt sowohl Setups mit als auch ohne Reverse Proxy Manager</li>
    </ul>

    <h2>Flexibilität</h2>
    <p>Diese optimierte Installationsmethode ermöglicht:</p>
    <ul>
        <li>Eine sichere lokale Entwicklungsumgebung</li>
        <li>Einfache Umstellung auf Produktionsumgebung</li>
        <li>Flexible Konfiguration mit oder ohne Reverse Proxy</li>
        <li>Effiziente Einrichtung von WordPress mit zusätzlichen Verwaltungstools in einer containerisierten Umgebung</li>
    </ul>
