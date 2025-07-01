# TAK Server YunoHost App

## Features
- Vollautomatische Installation inkl. PKI, CoreConfig und Reverse Proxy
- LDAP-Parameter werden am Ende des Setups angezeigt, sodass du TAK über das Webinterface mit dem internen YunoHost-LDAP koppeln kannst.
- Zugang zur Web-UI über https://deinedomain.tld/ (nach Installation)

## Installation
**Vorbereitung:**
1. .deb-Paket auf den Server legen (z.B. nach /root/)
2. App über YunoHost WebUI oder CLI installieren und alle Parameter angeben

## Zugang zur TAK WebUI als Administrator – Schritt-für-Schritt-Anleitung

Nach der Installation des TAK Servers sind folgende Schritte notwendig, um dich sicher als Administrator an der Weboberfläche (`Marti`) anzumelden.

---

### 1. Zertifikatsdateien vom Server herunterladen

Du benötigst **zwei Dateien** aus dem Server-Verzeichnis `/opt/tak/certs/files/`:
- `webadmin.p12` (dein persönliches Admin-Zertifikat)
- `truststore-<CACommonName>.p12` (dein CA-Zertifikat, z.B. `truststore-TAK-ID-CA-01.p12`)

**So lädst du die Dateien auf deinen PC:**

#### A. Mit WinSCP (empfohlen für Windows):
1. [WinSCP herunterladen](https://winscp.net/)
2. Mit dem Server verbinden (`SFTP`, Benutzername + Passwort)
3. Zu `/opt/tak/certs/files/` navigieren
4. Beide Dateien (`webadmin.p12` und das passende `truststore-*.p12`) per Drag&Drop auf deinen PC kopieren

#### B. Mit scp im Terminal (Linux/macOS/WSL):
```bash
scp benutzername@server:/opt/tak/certs/files/webadmin.p12 .
scp benutzername@server:/opt/tak/certs/files/truststore-TAK-ID-CA-01.p12 .
