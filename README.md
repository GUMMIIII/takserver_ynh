# TAK Server YunoHost App

## Features
- Vollautomatische Installation inkl. PKI, CoreConfig und Reverse Proxy
- LDAP-Parameter werden am Ende des Setups angezeigt, sodass du TAK über das Webinterface mit dem internen YunoHost-LDAP koppeln kannst.
- Zugang zur Web-UI über https://deinedomain.tld/ (nach Installation)

## Installation
**Vorbereitung:**
1. .deb-Paket auf den Server legen (z.B. nach /root/)
2. App über YunoHost WebUI oder CLI installieren und alle Parameter angeben

**Nach der Installation:**
- Das Admin-Zertifikat findest du unter `/opt/tak/certs/files/`.  
  Importiere es in deinen Browser (z.B. Firefox unter Einstellungen → Zertifikate).
- WebUI aufrufen: `https://<deinedomain>/<pfad>`, z.B. `https://tak.deinedomain.tld/`
- Mit Admin-Zertifikat einloggen

## LDAP/SSO mit YunoHost

TAK Server kann über die WebUI (Menü Verwaltung > Sicherheit > LDAP) an das interne YunoHost-LDAP angebunden werden.

**YunoHost-LDAP Parameter (werden am Ende der Installation angezeigt):**
- Host: `localhost`
- Port: `389`
- BaseDN: `dc=yunohost,dc=org`
- Bind-DN: `cn=admin,dc=yunohost,dc=org`
- Passwort: (in `/etc/ldap.secret`)

Um die Werte später nochmal zu sehen:
```bash
cat /etc/yunohost/ldap.conf | grep '^base'
cat /etc/yunohost/ldap.conf | grep '^binddn'
cat /etc/ldap.secret
