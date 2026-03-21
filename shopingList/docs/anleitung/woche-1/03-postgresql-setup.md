# 🗄️ Schritt 3: PostgreSQL Installation & Setup

**Ziel:** PostgreSQL läuft lokal, Datenbank "shopping_list" existiert, alle können sich verbinden
**Dauer:** 1.5h - 2h (je nach Betriebssystem)
**Wer:** Person 5 (Database-Lead) mit Team-Unterstützung
**Schwierigkeit:** ⭐⭐ (Mittel, aber kritisch!)

---

## 🎯 Was macht ihr heute?

Am Ende haben:
- ✅ PostgreSQL ist installiert
- ✅ Datenbank `shopping_list` existiert
- ✅ Testbenutzer `developer` mit Passwort existiert
- ✅ Alle können sich mit der DB verbinden (lokal)
- ✅ Test-Verbindung funktioniert

---

## 📋 Voraussetzungen

- Administrator-Zugriff auf euren Computer
- ~500 MB freier Platz (PostgreSQL)
- Internet-Verbindung (für Download)

---

## 👥 Wer macht das?

| Person | Rolle | Aktion |
|--------|-------|--------|
| 5 | Lead | Installation & Configuration |
| 6 | Support | Testing & Dokumentation |
| 3+4 | Learning | Parallel: Java-Setup (sie brauchen nicht zu warten) |
| 1+2 | Learning | Parallel: Frontend-Setup |

---

## 🚀 Installation nach Betriebssystem

### **Windows 10/11**

#### **Schritt 1: PostgreSQL Download (5 min)**

1. Besucht: https://www.postgresql.org/download/windows/
2. Klickt auf "Download the installer"
3. Wählt die **neueste stabile Version** (z.B. PostgreSQL 15 oder 16)
4. Speichert die Installer-Datei
5. Öffnet die heruntergeladene `.exe` Datei

#### **Schritt 2: Installation (10-15 min)**

Installer öffnet sich. Folgt diesen Schritten:

```
1. "Setup - PostgreSQL" Dialog
   → Next

2. Select Installation Directory
   → Default-Pfad belassen (C:\Program Files\PostgreSQL\)
   → Next

3. Select Components
   → PostgreSQL Server (MUSS checked sein)
   → pgAdmin 4 (optional, aber hilfreich)
   → Command Line Tools (MUSS checked sein)
   → Next

4. Data Directory
   → Default: C:\Program Files\PostgreSQL\16\data
   → MERKEN FÜR SPÄTER
   → Next

5. Password
   → Enter Password: dev_password
   → Re-enter Password: dev_password
   → Next (WICHTIG: "superuser" wird mit diesem Passwort erstellt)

6. Port
   → Default: 5432
   → MERKEN
   → Next

7. Locale
   → Default (z.B. [Default locale])
   → Next

8. Ready to Install
   → Install

9. Setup Complete
   → Du kannst pgAdmin 4 Launch jetzt abchecken → Finish
```

#### **Schritt 3: Umgebungsvariablen aktualisieren (5 min) - WINDOWS ONLY**

Nach Installation:

```
1. Windows-Taste drücken
2. "Environment Variables" suchen
3. "Edit the system environment variables" öffnen
4. "Environment Variables..." Button klicken
5. Im System variables Bereich "Path" auswählen
6. Edit → New
7. Füge hinzu: C:\Program Files\PostgreSQL\16\bin
8. OK, OK, OK
9. Terminal NEU öffnen
```

**Jetzt sollte das funktionieren:**
```bash
psql --version
# Output: psql (PostgreSQL) 16.x
```

---

### **macOS**

#### Mit Homebrew (empfohlen):

```bash
# Homebrew installieren (falls nicht vorhanden)
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# PostgreSQL installieren
brew install postgresql@16

# PostgreSQL starten (Hintergrund)
brew services start postgresql@16

# Prüfen ob läuft
pg_isready
# Output: accepting connections
```

---

### **Linux (Ubuntu/Debian)**

```bash
# Update package list
sudo apt update

# PostgreSQL installieren
sudo apt install postgresql postgresql-contrib -y

# Service starten (sollte automatisch laufen)
sudo systemctl start postgresql
sudo systemctl enable postgresql

# Prüfen
pg_isready
# Output: accepting connections
```

---

## 🗄️ Schritt 2: Datenbank & Benutzer erstellen

**Zeit:** 10 min

### **Terminal-Befehle (ALL OS):**

```bash
# Als PostgreSQL-Benutzer anmelden (SuperUser)
# Windows/Mac: psql -U postgres
# Linux: sudo -u postgres psql

psql -U postgres
```

**Das solltet ihr sehen:**
```
psql (16.1)
Type "help" for help.

postgres=#
```

**Jetzt im PostgreSQL-Terminal:**

```sql
-- Neue Datenbank erstellen
CREATE DATABASE shopping_list;

-- Neuer Benutzer (für Development)
CREATE USER developer WITH PASSWORD 'dev_password';

-- Rechte geben
ALTER USER developer CREATEDB;
GRANT ALL PRIVILEGES ON DATABASE shopping_list TO developer;

-- Anschauen, was wir erstellt haben
\l
-- Sollte shopping_list in der Liste sehen

-- Ausloggen
\q
```

**Das sollte aussehen:**
```
postgres=# CREATE DATABASE shopping_list;
CREATE DATABASE
postgres=# CREATE USER developer WITH PASSWORD 'dev_password';
CREATE USER
postgres=# ALTER USER developer CREATEDB;
ALTER ROLE
postgres=# GRANT ALL PRIVILEGES ON DATABASE shopping_list TO developer;
GRANT
postgres=# \l
                                   List of databases
        Name        |  Owner  | Encoding |  Collate   |    Ctype    |
-------------------+---------+----------+------------+-------------+
 shopping_list     | postgres| UTF8     | C.UTF-8    | C.UTF-8     |
 postgres          | postgres| UTF8     | ...        | ...         |
...
postgres=# \q
```

---

## 🧪 Test-Verbindung: Kann jeder sich anmelden?

**Zeit:** 10 min

### Jeder im Team sollte das testen:

```bash
# Mit dem neuen Benutzer verbinden
psql -h localhost -U developer -d shopping_list

# Passwort eingeben: dev_password
```

**Erfolgreich wenn:**
```
psql (16.1)
Type "help" for help.

shopping_list=>#
```

### Kleine Test-Query:

```sql
-- Test: Erstelle eine Test-Tabelle
CREATE TABLE test (
    id SERIAL PRIMARY KEY,
    message VARCHAR(255)
);

-- Daten einfügen
INSERT INTO test (message) VALUES ('It works!');

-- Abfragen
SELECT * FROM test;

-- Sollte anzeigen:
-- id | message
-- ----+----------
-- 1 | It works!

-- Aufräumen
DROP TABLE test;

-- Ausloggen
\q
```

---

## 📝 Konfigurationsdatei speichern

Jetzt speichert die wichtigsten Informationen in `config/application.properties`:

```bash
cd shopingList
cat > config/application.properties << 'EOF'
# Database Configuration
db.url=jdbc:postgresql://localhost:5432/shopping_list
db.user=developer
db.password=dev_password
db.driver=org.postgresql.Driver

# Server Configuration
server.port=8080
server.host=localhost

# Logging
log.level=INFO
EOF

cat config/application.properties
```

---

## ✅ Checkliste - PostgreSQL ist ready?

- [ ] PostgreSQL installiert (`psql --version` funktioniert)
- [ ] Datenbank `shopping_list` existiert
- [ ] Benutzer `developer` mit Passwort existiert
- [ ] Alle im Team können `psql -h localhost -U developer -d shopping_list` ausführen
- [ ] Test-Query (`SELECT 1;`) funktioniert bei jedem
- [ ] `config/application.properties` existiert mit korrekten Werten
- [ ] Person 6 hat alles dokumentiert (eigenes Notebook)

---

## ❓ Häufige Probleme

### **Problem 1: "command not found: psql"**

```bash
# Umgebungsvariablen nicht aktualisiert
# Lösung: Terminal NEUÖFFNEN

# Oder manueller Pfad:
/usr/local/bin/psql --version  # macOS
C:\Program Files\PostgreSQL\16\bin\psql --version  # Windows
```

### **Problem 2: "FATAL: Ident authentication failed"**

```bash
# Linux-Problem mit pg_hba.conf
# Lösung: Mit sudo arbeiten

sudo -u postgres psql
```

### **Problem 3: "fe_sendauth: no password supplied"**

```bash
# Passwort wird nicht akzeptiert
# Lösung: Benutzer neu erstellen mit korrektem Passwort

# Als postgres-USER:
psql -U postgres
# Dann:
ALTER USER developer WITH PASSWORD 'dev_password';
```

### **Problem 4: Port 5432 ist bereits in Verwendung**

```bash
# Jemand anderes nutzt PostgreSQL

# Check wer Port nutzt:
# Windows: netstat -ano | findstr :5432
# Mac/Linux: lsof -i :5432

# Lösung: Port in Installer oder später schreiben als 5433, 5434, etc.
```

### **Problem 5: "Permission denied" beim Installer (Windows)**

```bash
# Installer mit Admin-Rechten ausführen
# 1. Rechts-Klick auf .exe
# 2. "Run as Administrator"
```

---

## 🎓 Was ihr gelernt habt

1. **Datenbank-Verwaltung:** CREATE DATABASE/USER
2. **Authentifizierung:** Benutzer & Passwörter
3. **Connection-Strings:** Wie man sich verbindet
4. **SQL Basics:** CREATE, INSERT, SELECT, DROP

---

## 📞 Nächste Schritte

Wenn PostgreSQL läuft:
- ✅ **Backend-Team (Person 3+4)** kann mit Java-Setup starten
- ✅ **Frontend-Team (Person 1+2)** kann weiter mit HTML/CSS
- ✅ **Person 5** bereitet das Datenbank-Schema vor (nächster Schritt)

---

## 🔗 Weiterführende Ressourcen

- PostgreSQL Docs: https://www.postgresql.org/docs/
- psql Befehle: https://www.postgresql.org/docs/current/app-psql.html

---

**✅ PostgreSQL läuft? Großartig!**

→ Nächstes: [Schritt 5: Datenbank-Schema implementieren](./05-datenbank-implementieren.md)
