# TAK Server (YunoHost App)

**Tactical Assault Kit Server (TAK Server)** als App für YunoHost –  
mit integrierter PKI, Reverse Proxy & Web-UI für Zertifikate.

---

## Was ist der TAK Server?

Der TAK Server ist eine Plattform zur Echtzeit-Kollaboration (Lagekarte, Chat, Missionsplanung)  
und kommt bei Behörden, Militär, BOS und Security-Projekten zum Einsatz.  
Er kommuniziert über das Cursor-On-Target-Protokoll (CoT) und setzt auf starke PKI-Authentifizierung.

---

## Voraussetzungen

- YunoHost v12+
- Eigener Server/VPS (Debian 12 empfohlen)
- **TAK Server .deb**: Download via [tak.gov](https://tak.gov) (Account erforderlich)
- Root-Zugang zum Server

---

## Installation (Schritte)

1. **TAK .deb herunterladen**  
   Registriere dich unter https://tak.gov und lade das aktuelle `.deb`-Paket herunter.

2. **App installieren (YunoHost-UI oder CLI):**  
   - Domain wählen (`tak.deinedomain.tld`)
   - Pfad zur `.deb` angeben (`/root/takserver.deb`)
   - Werte für `Country`, `State`, `City`, `Organization`, `OU`, CA-Namen, Passwörter festlegen

3. **Automatisiert erledigt das Skript:**  
   - Abhängigkeiten installieren
   - Systemuser `tak` anlegen
   - TAK Server + PKI initialisieren (Root-CA, Intermediate-CA, Serverzertifikat)
   - Webadmin-Clientzertifikat generieren
   - Nginx-Proxy einrichten
   - TAK starten

4. **Nach der Installation:**
   - **`/opt/tak/certs/files/webadmin.p12`** herunterladen (z.B. mit scp):
     ```powershell
     # Beispiel für Windows (mit PowerShell & scp aus Windows 10/11)
     scp root@yourserver:/opt/tak/certs/files/webadmin.p12 C:\Users\%USERNAME%\Downloads\
     ```
   - Zertifikat im Browser importieren  
     - Unter Windows/Mac: Doppelklick, Import-Assistent folgen
     - Bei Firefox: Einstellungen → Datenschutz & Sicherheit → Zertifikate anzeigen → Importieren

5. **Login am TAK WebUI:**  
   - Rufe `https://tak.deinedomain.tld/` im Browser auf
   - Wähle das **Webadmin-Zertifikat** aus (PIN: das im Setup gewählte Passwort)
   - Nun kannst du Admin-Nutzer, Gruppen, Zertifikate und Policies verwalten.

---

## Hinweise

- **Passwort-Änderung:**  
  Die CA- und Zertifikats-Passwörter kannst du direkt bei der Installation im YNH-Formular festlegen.
- **Support:**  
  TAK ist komplex – orientiere dich immer an der offiziellen [TAK Doku](https://tak.gov), die App folgt strikt deren Best Practices.
- **Updates:**  
  Einfach neue `.deb`-Datei herunterladen und das Update-Skript ausführen.

---

## Troubleshooting

- Wenn TAK-WebUI nicht lädt:  
  Prüfe, ob der Service läuft: `systemctl status takserver`
- Fehler bei PKI:  
  Lösche `/opt/tak/certs` **nur**, wenn du weißt, was du tust! (CA dann neu initialisieren)
- Fragen?  
  Issues gerne im [GitHub Repo](https://github.com/GUMMIIII/takserver_ynh) oder im [TAK Forum](https://github.com/deptofdefense/AndroidTacticalAssaultKit-CIV/issues)

---

## TODO

- [ ] Matrix/Element Bridge implementieren  
- [ ] Verbesserte WebUI-Integration (YunoHost-SSO etc.)
- [ ] Optionale automatische Updates des TAK-Servers
- [ ] PKI-UI für User-Self-Service
- [ ] Anbindung an LDAP von YunoHost
- [ ] Mehrsprachigkeit der App

---

**Made with ❤️ for the TAK Community.**
