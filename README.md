# TAK-Server für YunoHost

**TAK-Server** (Team Awareness Kit) ist eine Open-Source-Lösung für verteiltes Lagebild, Mapping, Messaging und Sensorintegration – oft genutzt im BOS-, Militär- oder Outdoor-Umfeld.

Dieses Paket integriert den TAK-Server als private App in YunoHost und erledigt die gesamte Installation, Reverse Proxying sowie die Einbindung ins YunoHost-Ökosystem **vollautomatisch**.

---

## Funktionen

- Vollständige Installation des TAK-Servers (`takserver.deb`)
- Einrichtung eines dedizierten Systembenutzers (`tak`)
- Automatische Generierung von PKI/CA-Zertifikaten (Server/Root)
- Vollautomatische Einrichtung von PostgreSQL-Datenbank & User (inkl. zufälligem Passwort)
- Automatische Erstellung und Abspeicherung der Zugangsdaten im System (für spätere App-Updates oder manuelle Admin-Zugriffe)
- Reverse-Proxy-Einrichtung für `https://<deine-domain>/` via Nginx
- Automatische Rechte- und Limitanpassung
- Einfaches Entfernen (säubert alles inkl. Systemuser, Datenbank, Files und Nginx)
- Zukünftig: LDAP-Anbindung an das YunoHost-Backend

---

## Voraussetzungen

- **TAK Server .deb-Datei** muss vorher per SCP oder Upload auf den Server übertragen werden (siehe Installationsanweisungen unten).
- YunoHost-Server mit Root-Rechten.
- Ausreichend RAM (>2GB empfohlen).

---

## Installation

1. **TAK Server .deb bereitstellen**
    - Übertrage die `.deb`-Datei auf deinen Server, z.B. nach `/root/takserver.deb`.

2. **App installieren**
    - Über das YunoHost-Webinterface oder per CLI:
      ```bash
      yunohost app install /pfad/zum/takserver_ynh
      ```
    - Im Installationsdialog **Pfad zur .deb-Datei** angeben (z.B. `/root/takserver.deb`).

3. **Was passiert während der Installation?**
    - Es wird ein Linux-User `tak` angelegt (sofern nicht vorhanden)
    - Die `.deb` wird installiert
    - PKI/CA wird initialisiert (Root CA, Signing CA, Server-Zertifikat)
    - Eine eigene **PostgreSQL-Datenbank** sowie ein **sicherer DB-User** mit zufälligem Passwort wird automatisch erzeugt (keine Benutzerinteraktion nötig!)
    - Diese Daten werden in `/opt/tak/.dbinfo` sicher abgelegt und bei Bedarf im **YunoHost Hinweisfenster** nach der Installation angezeigt
    - Nginx wird automatisch für Proxy/SNI eingerichtet

4. **Nach der Installation**
    - Rufe die Web-Oberfläche auf: `https://<deine-domain>/`
    - Der TAK-Server läuft jetzt und ist erreichbar.

---

## Hinweise für Admins

- **Datenbankzugang:**  
  Die App erstellt und verwaltet die Datenbankzugänge automatisch.  
  Daten findest du, falls benötigt, unter `/opt/tak/.dbinfo`.

- **Zertifikate:**  
  Die komplette PKI befindet sich unter `/opt/tak/certs`.

- **Reverse Proxy:**  
  Die Nginx-Konfiguration wird im Verzeichnis `/etc/nginx/conf.d/<domain>.d/` angelegt.

- **Update/Upgrade:**  
  Nutze das YunoHost-Upgrade oder ersetze die `.deb` und installiere die App neu.

- **Deinstallation:**  
  Entfernt alle Dateien, den User `tak`, die Nginx-Konfiguration und die Datenbank inklusive User.

---

## Manuelle Eingriffe / Spezialfälle

- **LDAP-Anbindung:**  
  Wird demnächst unterstützt – derzeit sind YunoHost-User und TAK-Server-User noch getrennt.

- **Fehlerbehebung:**  
  Prüfe die Logfiles unter `/opt/tak/logs/` und das YunoHost-Log.

---

## FAQ

**F: Muss ich ein Passwort/Username für die Datenbank vergeben?**  
A: Nein! Das übernimmt die App automatisch. Die Infos findest du ggf. im Hinweis-Fenster nach der Installation und in `/opt/tak/.dbinfo`.

**F: Muss ich Nginx, fail2ban oder DNSmasq selbst konfigurieren?**  
A: Nein, die App erledigt alles automatisch.

---

## Lizenz

Dieses Paket unterliegt der Apache 2.0 Lizenz.  
TAK-Server selbst: [siehe takserver.org](https://www.tak.gov/)

---

## Support/Kontakt

Bug melden, Feature-Requests oder Hilfe:  
[Deine E-Mail oder GitHub-Link]

