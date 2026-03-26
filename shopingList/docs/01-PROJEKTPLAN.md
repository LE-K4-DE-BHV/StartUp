# 📋 Geteilte Einkaufsliste - Projektplan

**Version:** 1.0
**Status:** Planung genehmigt
**Datum:** 2026-03-21
**Projekt-Dauer:** 4 Wochen (20 Arbeitstage)
**Team-Größe:** 6 Personen (Alle Anfänger, gemeinsames Lernen)

---

## 🎯 Projektziel

Wir entwickeln eine **Echtzeit-Einkaufslisten-Anwendung**, die es Freundesgruppen, Familien und Partnern ermöglicht:
- Einkaufslisten in Gruppen zu erstellen und zu verwalten
- Ausgaben zu tracken und gerecht untereinander zu verteilen
- In Echtzeit zusammenzuarbeiten (WebSocket-basiert)
- Gruppiertes Einkaufen zu organisieren

**Kernwert:** Transparente, faire Kostenaufteilung bei gemeinsamem Einkaufen.

---

## 📦 MVP (Minimum Viable Product)

### Was ist IM MVP enthalten?

| Feature | Prio | Grund | TW* |
|---------|------|-------|-----|
| **Registrierung & Login** | 🔴 Kritisch | Basis-Authentifizierung | 2d |
| **Benutzerprofil** | 🔴 Kritisch | Name, Email, Foto (optional) | 1d |
| **Gruppen-Management** | 🔴 Kritisch | Einkaufsgruppen erstellen & verwalten | 2d |
| **Einkaufsliste** | 🔴 Kritisch | Items hinzufügen, abhaken, löschen | 2d |
| **Ausgabenverteilung** | 🔴 Kritisch | Wer zahlt wie viel? Fair teilen. | 3d |
| **Echtzeit-Synchronisation** | 🔴 Kritisch | WebSocket-Verbindung | 3d |
| **Chat** | 🟡 Wichtig | Gruppenchat für Koordination | 2d |
| **Budget (Optional)** | 🟡 Wichtig | Ausgabenlimit setzen | 1d |

**TW* = Geschätzte Arbeitstage**

### Was ist NICHT im MVP?

- ❌ Abrechnung (Scannen/KI) → **Phase 2**
- ❌ Map mit Supermärkten → **Phase 2**
- ❌ Offline-Funktionalität
- ❌ Mobile App (native)

---

## 🏗️ Technische Architektur (Übersicht)

```
┌─────────────────────────────────────────────────────────┐
│               🖥️ FRONTEND (Browser)                      │
│    HTML/CSS/JavaScript (Responsive Design)             │
│  • Login-Seite                                          │
│  • Dashboard (Gruppen, Listen)                         │
│  • Einkaufslisten-Editor                              │
│  • Ausgabenverteilung-Kalkulator                      │
│  • Chat-Interface                                      │
└────────────────┬────────────────────────────────────────┘
                 │
         🔗 WebSocket + REST API
                 │
┌────────────────▼────────────────────────────────────────┐
│              🖥️ BACKEND (Java)                           │
│        Vanilla Java HTTP Server                         │
│  • Authentication-Service                              │
│  • User-Service                                        │
│  • Group-Service                                       │
│  • ShoppingList-Service                               │
│  • Expense-Service                                     │
│  • Chat-Service                                        │
│  • WebSocket-Handler                                   │
└────────────────┬────────────────────────────────────────┘
                 │
            🔄 JDBC
                 │
┌────────────────▼────────────────────────────────────────┐
│          🗄️ DATENBANK (PostgreSQL)                       │
│  • users (Benutzer)                                    │
│  • groups (Einkaufsgruppen)                           │
│  • shopping_items (Items in Listen)                    │
│  • expenses (Ausgaben & Verteilung)                   │
│  • chat_messages (Gruppenchat)                        │
└─────────────────────────────────────────────────────────┘
```

---

## 🧑‍💼 Team-Struktur & Rollen

Alle 6 Personen arbeiten **cross-funktional**, haben aber Schwerpunkte:

| Name | Schwerpunkt | Verantwortung | Lernziel |
|------|------------|---------------|----------|
| Person 1 | Frontend-Lead | HTML/CSS/JS UI | Web-Entwicklung von Grund auf |
| Person 2 | Frontend | JavaScript/WebSocket-Client | Interaktive Oberflächen |
| Person 3 | Backend-Lead | Java Architecture | Server-Entwicklung & Design Patterns |
| Person 4 | Backend | Java Services | REST API & Business-Logic |
| Person 5 | Database-Lead | PostgreSQL Schema & Queries | Datenbank-Design |
| Person 6 | Integration & QA | Testing, Deployment | Full-Stack Verständnis |

**Wichtig:** Jeder arbeitet auch in anderen Bereichen. Das ist ein **Learning-Projekt**!

---

## 📊 Sprint & Aufgaben Übersicht (auf einen Blick)

| Woche | Meilenstein | Hauptaufgaben | Owner | Deliverables | Status |
|-------|-------------|---------------|-------|--------------|--------|
| **1** | **Setup & Infrastruktur** | Git Setup, PostgreSQL, Java HTTP-Server, DB-Schema, Seed-Daten | P6 (Dev-Ops), P5 (DB), P3/P4 (Backend), P1/P2 (Frontend) | Repository mit Struktur, 9 DB-Tabellen, Server auf Port 8080, Frontend Skeleton | 🔲 To-Do |
| **2** | **Authentifizierung & Basis** | User Registration, Login, Sessions, Group CRUD, Items CRUD | P3/P4 (Backend), P1/P2 (Frontend), P5 (DB) | Login funktioniert, Gruppen können erstellt werden, Items hinzufügbar | 🔲 To-Do |
| **3** | **Echtzeit & Features** | WebSocket, Expense-Splits, Chat-System, Schulden-Berechnung | P3/P4 (Backend), P1/P2 (Frontend), P6 (QA) | Live-Updates funktionieren, Ausgaben werden verteilt, Chat läuft | 🔲 To-Do |
| **4** | **Testing, Docs & Release** | Unit-Tests, Integration-Tests, Performance, Dokumentation, Deployment | P6 (QA Lead), Alle | Tests geschrieben, API-Docs vollständig, MVP produktionsbereit | 🔲 To-Do |

### **Aufgaben pro Woche (Task-Verteilung)**

| Woche | Task-ID | Aufgabentitel | Owner | Dauer | Abhängigkeiten |
|-------|---------|---------------|-------|-------|-----------------|
| **Woche 1** | T1.1.1 | Git Repository einrichten & klonen | P6 | 45 min | — |
| | T1.1.2 | Feature-Branch Konvention etablieren | P6 | 30 min | T1.1.1 |
| | T1.1.3 | Ordner-Struktur anlegen | P6 | 1h | T1.1.1 |
| | T1.1.4 | Config-Dateien erstellen | P5, P4 | 30 min | T1.1.3 |
| | T1.2.1 | PostgreSQL installieren & starten | P5 | 1,5h | — |
| | T1.2.2 | Admin-Passwort setzen | P5 | 30 min | T1.2.1 |
| | T1.2.3 | Datenbank erstellen | P5 | 15 min | T1.2.2 |
| | T1.2.4 | Schema erstellen (9 Tabellen) | P5 | 1,5h | T1.2.3 |
| | T1.2.5 | Seed-Daten laden | P5 | 45 min | T1.2.4 |
| | T1.3.1 | HTTP-Server Hello World | P3, P4 | 2h | — |
| | T1.3.2 | JSON Response statt Text | P3, P4 | 1,5h | T1.3.1 |
| | T1.3.3 | URL-Routing | P3, P4 | 1,5h | T1.3.2 |
| | T1.3.4 | Request-Parsing (Query-Parameter) | P4 | 1,5h | T1.3.3 |
| | T1.4.1 | JDBC Driver einbinden | P3, P4 | 30 min | — |
| | T1.4.2 | Connection String & Auth | P5, P3 | 45 min | T1.4.1, T1.2.3 |
| | T1.4.3 | SELECT Query ausführen | P3, P4 | 1h | T1.4.2 |
| | T1.4.4 | GET /api/users mit DB-Daten | P3, P4 | 1,5h | T1.4.3 |
| | T1.5.1 | Frontend ruft Backend auf | P1, P2 | 1h | T1.3.1 |
| | T1.5.2 | Integration Test Frontend→Backend→DB | P6 | 1,5h | T1.4.4, T1.5.1 |
| | T1.5.3 | Dokumentation aktualisieren | P6 | 1h | T1.5.2 |
| | T1.5.4 | Code-Reviews & Merge | P6 | 1h | Alle Tasks |
| **Woche 2** | T2.1.x | User Registration & Login | P3/P4, P1/P2 | 2d | T1.5.4 |
| | T2.2.x | Session Management | P3/P4, P5 | 1d | T2.1.x |
| | T2.3.x | Gruppen CRUD (Create/Read/Update/Delete) | P3/P4 | 1,5d | T2.2.x |
| | T2.4.x | Gruppen-Management UI | P1/P2 | 1,5d | T2.3.x |
| | T2.5.x | Shopping Items CRUD | P3/P4 | 1,5d | T2.2.x |
| | T2.6.x | Shopping Items UI | P1/P2 | 1,5d | T2.5.x |
| **Woche 3** | T3.1.x | WebSocket-Server implementieren | P3/P4 | 1,5d | T1.5.4 |
| | T3.2.x | WebSocket Client (Frontend) | P1/P2 | 1,5d | T3.1.x |
| | T3.3.x | Expense-Tracking API | P3/P4 | 1,5d | T2.5.x |
| | T3.4.x | Expense-Splits Berechnung | P3/P4, P5 | 1d | T3.3.x |
| | T3.5.x | Expense-UI & Kalkulator | P1/P2 | 1,5d | T3.4.x |
| | T3.6.x | Chat-API & UI | P3/P4, P1/P2 | 2d | T3.1.x |
| **Woche 4** | T4.1.x | Unit-Tests schreiben | P3/P4, P5, P6 | 1d | Alle Woche 3 |
| | T4.2.x | Integration-Tests | P6 | 1d | T4.1.x |
| | T4.3.x | Performance & Security Review | P3/P4, P6 | 1d | T4.2.x |
| | T4.4.x | Dokumentation finalisieren | P6 | 1d | T4.3.x |
| | T4.5.x | Deployment & Rollout | P6, Alle | 1d | T4.4.x |

---

## 📅 4-Wochen Sprint-Plan (Detailliert)

### **WOCHE 1: Setup & Grundlagen**

#### Mo-Di: Projekt-Kickoff & Environments
- [X] Git-Repository aufsetzen
- [ ] Projekt-Struktur erstellen
- [ ] Java-Project initialisieren
- [ ] PostgreSQL lokale Instanz aufsetzen
- [ ] Frontend-Projektstruktur (HTML/CSS/JS)
- [ ] Team-Kickoff-Meeting (Architektur, Workflow)

#### Mi-Do: Datenbank-Schema Design
- [ ] ER-Diagramm erstellen
- [ ] Tabellen-Design (users, groups, shopping_items, expenses, chat_messages)
- [ ] SQL-Skripte schreiben
- [ ] Testdaten laden

#### Fr: Grundlagen Java HTTP-Server
- [ ] Einfachen HTTP-Server in Java bauen (Vanilla, kein Framework)
- [ ] Request/Response-Handling verstehen
- [ ] Grundstruktur für Services

**Meilenstein:** Datenbank läuft, Java-Server antwortet auf Requests

---

### **WOCHE 2: Authentifizierung & Grundfeatures**

#### Mo-Di: Authentication System
- [ ] Login-API (Java)
- [ ] User-Registration (Java)
- [ ] Password-Hashing (Sicherheit!)
- [ ] Session-Verwaltung
- [ ] Login-UI (HTML/CSS/JavaScript)

#### Mi: Benutzerprofil & Gruppen
- [ ] User-Profil-API
- [ ] Groups-API (CRUD)
- [ ] Profil-UI
- [ ] Groups-Verwaltungs-UI

#### Do-Fr: Einkaufslisten Basis
- [ ] Shopping-Items-API
- [ ] Datenbank-Queries für Items
- [ ] Shopping-List-UI (HTML/CSS)
- [ ] Add/Delete/Update Items (Frontend)

**Meilenstein:** Login funktioniert, Gruppen können erstellt werden, Items können hinzugefügt werden

---

### **WOCHE 3: Echtzeit & Komplexe Features**

#### Mo-Di: WebSocket-Integration
- [ ] WebSocket-Server in Java implementieren
- [ ] Clients verbinden (Frontend WebSocket Client)
- [ ] Message-Broadcast (Items, Status-Updates)
- [ ] Error-Handling & Reconnection-Logic

#### Mi-Do: Ausgabenverteilung
- [ ] Expense-Tracking API
- [ ] Expense-Entities in Datenbank
- [ ] Splitting-Logik (Beiträge verteilen)
- [ ] Ausgabenkalkulator-UI
- [ ] Expense-History anzeigen

#### Fr: Chat-System
- [ ] Chat-API (Java)
- [ ] Chat-UI (HTML/CSS/JavaScript)
- [ ] WebSocket für Live-Chat
- [ ] Message-History laden

**Meilenstein:** Echtzeit-Updates funktionieren, Ausgaben werden verteilt, Chat läuft

---

### **WOCHE 4: Testing, Optimierung & Rollout**

#### Mo-Di: Testing & Bug-Fixes
- [ ] Unit-Tests für Java-Services
- [ ] Integration-Tests (Frontend ↔ Backend)
- [ ] Manual-Testing (Szenarios durchspielen)
- [ ] WebSocket-Connection-Tests
- [ ] Bug-Fixes basierend auf Tests

#### Mi: Performance & Sicherheit
- [ ] SQL-Injection-Prävention überprüfen
- [ ] XSS-Prävention im Frontend
- [ ] Datenbankindizes optimieren
- [ ] Frontend-Performance (Caching, Minification)

#### Do: Dokumentation & Deployment
- [ ] API-Dokumentation (alle Endpoints)
- [ ] Installation-Guide
- [ ] User-Anleitung
- [ ] Deployment-Skripte (Production-Ready)

#### Fr: Demo & Abschluss
- [ ] Finale Demo für Stakeholder
- [ ] Lessons Learned dokumentieren
- [ ] Nächste Schritte (Phase 2) planen

**Meilenstein:** MVP ist produktionsbereit, vollständig dokumentiert, getestet

---

## 🎯 DETAILLIERTE SPRINT-PLANUNG FÜR WOCHE 1

### **Wochenübersicht**
Die erste Woche ist die **Infrastruktur-Woche**. Am Freitag sollen alle kritischen Systeme laufen: Git, PostgreSQL, Java HTTP-Server, Datenbank-Schema, und erste Frontend-Struktur.

**Gesamtdauer Woche 1:** 5 Tage × 8h = 40 Stunden
**Team:** 6 Personen = 240 Personenstunden verfügbar
**Workload pro Person:** ~8h/Tag (2-3 Aufgaben parallel möglich)

---

### **Montag: Git Setup & Projekt-Struktur**
**Owner:** Person 6 (Integration & QA Lead)
**Dauer:** 3-4 Stunden
**Kategorie:** DevOps / Infrastructure

#### **Meilenstein Ende Montag:**
Alle 6 Team-Mitglieder können Code committen, Feature-Branches funktionieren, Projekt-Ordnerstruktur ist angelegt.

#### **Aufgaben (Task-ID: T1.1.x)**

##### **T1.1.1 - Git Repository einrichten & klonen**
**Owner:** Person 6
**Dauer:** 45 min

**Was ist DONE?**
- [ ] Git Repository ist auf dem Server/GitHub erreich
- [ ] .gitignore ist konfiguriert (Java, IDE, Secrets, OS-Dateien)
- [ ] README.md existiert mit Projekt-Beschreibung
- [ ] Alle 6 Team-Mitglieder können erfolgreich klonen

**Konkrete Schritte:**
1. Repository initialisieren (lokal oder GitHub klonen)
2. `.gitignore` mit diesen Rules erstellen (Java + IDE):
   ```
   *.class, *.jar, *.war, target/, out/, .idea/, .vscode/, *.swp, .DS_Store, .env, secrets/
   ```
3. `README.md` schreiben: Projekt-Name, Ziel, Architektur-Übersicht, Quick-Start
4. Erstes Commit: `git add -A && git commit -m "Initial: Repository setup"`
5. Alle klonen die Repo und führen `git status` aus

**Ressourcen:**
- Siehe: `docs/anleitung/woche-1/00-sonstigesanleitung.md` (Git-Kapitel)

---

##### **T1.1.2 - Feature-Branch Konvention etablieren**
**Owner:** Person 6
**Dauer:** 30 min

**Was ist DONE?**
- [ ] Branch-Naming-Konvention dokumentiert im README
- [ ] Jedes Team-Mitglied hat einen Feature-Branch erstellt
- [ ] Mindestens 1 Pull Request pro Person eingereicht

**Naming-Konvention:**
```
feature/[beschreibung]     # z.B. feature/postgresql-setup
fix/[bug-name]            # z.B. fix/login-button-responsive
docs/[doc-name]           # z.B. docs/api-endpoints
refactor/[component]      # z.B. refactor/services-structure
```

**Konkrete Schritte:**
```bash
git checkout -b feature/woche-1-setup
# Macht eure erste Änderung (z.B. eine Datei hinzufügen)
git add .
git commit -m "Feat: [Was]: [Warum]"
git push origin feature/woche-1-setup
# Pull Request auf GitHub erstellen
```

---

##### **T1.1.3 - Ordner-Struktur anlegen**
**Owner:** Person 6 (koordinieren) + Alle (parallel)
**Dauer:** 1 Stunde

**Was ist DONE?**
- [ ] `src/main/java/com/shoppinglist/` existiert mit Unter-Ordnern
- [ ] `src/test/java/com/shoppinglist/` existiert
- [ ] `public/` Ordner mit `pages/`, `js/`, `css/` existiert
- [ ] `db/` Ordner mit `migrations/` existiert
- [ ] `config/` Ordner existiert
- [ ] Alle Ordner sind in Git trackbar (mit `.gitkeep` oder ersten Dateien)

**Bash-Befehle zum Ausführen:**
```bash
# In Repo-Root ausführen:
mkdir -p src/main/java/com/shoppinglist/{server,controller,service,repository,model,security,util}
mkdir -p src/test/java/com/shoppinglist/{service,repository}
mkdir -p public/{pages,js,css}
mkdir -p db/migrations
mkdir -p config

# Git muss leere Ordner nicht tracken, also .gitkeep Dateien erstellen:
find . -type d -empty -exec touch {}/.gitkeep \;

# Überprüfe, dass alles da ist:
tree -L 3 . # oder: find . -type d | sort
```

**Verifikation:**
```bash
git status # sollte neue Ordner anzeigen
```

---

##### **T1.1.4 - Config-Dateien erstellen**
**Owner:** Person 5 (Database) + Person 4 (Backend)
**Dauer:** 30 min

**Was ist DONE?**
- [ ] `config/application.properties` existiert mit DB-Konfiguration
- [ ] `config/application.properties` ist in .gitignore für local-Varianten
- [ ] Placeholder-Werte im Produktions-Config (werden in T1.2.2 befüllt)

**Dateiinhalt (config/application.properties):**
```properties
# Server
server.port=8080
server.host=localhost

# Database (wird in Woche 1 Dienstag gefüllt)
db.url=jdbc:postgresql://localhost:5432/shopping_list
db.user=developer
db.password=dev_password

# Logging
log.level=INFO
```

**Checkpoint:**
```bash
cat config/application.properties # sollte Inhalt zeigen
```

---

#### **Monday Checkpoint (17:00 Uhr):**
- [ ] Alle können `git clone` ausführen
- [ ] 6 Feature-Branches existieren
- [ ] Ordner-Struktur ist da
- [ ] Mindestens 6 Commits im Repo (je 1 pro Person)
- [ ] README ist klar & hilfreich

---

### **Dienstag: PostgreSQL Installation & Datenbankschema**
**Owner:** Person 5 (Database Engineer)
**Dauer:** 4-5 Stunden
**Kategorie:** Database / Infrastructure

#### **Meilenstein Ende Dienstag:**
PostgreSQL läuft lokal auf jedem Rechner, die Datenbank `shopping_list` wurde erstellt, Schema mit 9 Tabellen existiert, Seed-Daten sind geladen.

#### **Aufgaben (Task-ID: T1.2.x)**

##### **T1.2.1 - PostgreSQL installieren & starten**
**Owner:** Person 5 (mit Hilfe für andere)
**Dauer:** 1,5 Stunden

**Was ist DONE?**
- [ ] PostgreSQL `systemctl status postgresql` gibt "active (running)"
- [ ] `psql --version` zeigt PostgreSQL 14+
- [ ] Lokal connecten funktioniert: `sudo -u postgres psql -c "SELECT 1;"`
- [ ] TCP-Port 5432 ist erreichbar: `telnet localhost 5432`

**Installation (Ubuntu/Debian):**
```bash
sudo apt update
sudo apt install postgresql postgresql-client postgresql-contrib
sudo systemctl start postgresql
sudo systemctl enable postgresql  # beim Startup starten
sudo systemctl status postgresql
```

**Test:**
```bash
sudo -u postgres psql -c "SELECT 1;"
# Output: ?column?
#    1
```

**Falls nicht läuft:** Logs zeigen:
```bash
sudo journalctl -u postgresql -n 50
```

---

##### **T1.2.2 - Administratoren-Passwort setzen**
**Owner:** Person 5
**Dauer:** 30 min

**Was ist DONE?**
- [ ] postgres User hat sicheres Passwort
- [ ] Local login mit Passwort funktioniert
- [ ] `config/application.properties` wurde aktualisiert

**SQL zum Ausführen:**
```bash
sudo -u postgres psql
```
Dann im psql-Prompt:
```sql
ALTER USER postgres WITH ENCRYPTED PASSWORD 'DEIN_SICHERES_PASSWORT';
CREATE USER developer WITH ENCRYPTED PASSWORD 'dev_password';
GRANT ALL PRIVILEGES ON ALL DATABASES TO developer;
\q
```

**Test Login:**
```bash
psql -U developer -h localhost -p 5432 -d template1 -c "SELECT 1;"
# (wird nach Passwort fragen)
```

---

##### **T1.2.3 - Datenbank erstellen**
**Owner:** Person 5
**Dauer:** 15 min

**Was ist DONE?**
- [ ] Datenbank `shopping_list` existiert
- [ ] User `developer` hat GRANT auf diese DB
- [ ] `\l` Befehl zeigt die Datenbank

**SQL:**
```bash
sudo -u postgres psql
```
```sql
CREATE DATABASE shopping_list;
GRANT ALL PRIVILEGES ON DATABASE shopping_list TO developer;
GRANT USAGE ON SCHEMA public TO developer;
GRANT ALL PRIVILEGES ON ALL TABLES IN SCHEMA public TO developer;
\l  # sollte shopping_list zeigen
\q
```

---

##### **T1.2.4 - Datenbank-Schema erstellen (9 Tabellen)**
**Owner:** Person 5 (mit allen zum Verstehen)
**Dauer:** 1,5 Stunden

**Was ist DONE?**
- [ ] 9 Tabellen: users, groups, group_members, shopping_items, expenses, expense_splits, chat_messages, budgets, sessions
- [ ] Alle Constraints, Foreign Keys, und Indizes sind gesetzt
- [ ] `\dt shopping_list` zeigt alle Tabellen

**Schema-Datei:** `db/schema.sql` (siehe 01-projekt-setup.md oder 05-datenbank-implementieren.md)

**Ausführen:**
```bash
psql -U developer -d shopping_list -f db/schema.sql
```

**Test:**
```bash
psql -U developer -d shopping_list
# Im Prompt:
\dt  # sollte alle Tabellen zeigen
\d users  # zeigt Schema der users Tabelle
```

---

##### **T1.2.5 - Seed-Daten laden**
**Owner:** Person 5
**Dauer:** 45 min

**Was ist DONE?**
- [ ] Mindestens 3 Test-User existieren
- [ ] Mindestens 1 Test-Group mit 2+ Members
- [ ] 3+ Test-Items
- [ ] 1+ Test-Expenses mit Splits
- [ ] `SELECT COUNT(*) FROM users;` gibt 3 zurück

**Seed-Datei:** `db/seed-data.sql` (Details in 05-datenbank-implementieren.md)

```bash
psql -U developer -d shopping_list -f db/seed-data.sql
```

**Verifikation:**
```bash
psql -U developer -d shopping_list
# Im Prompt:
SELECT COUNT(*) FROM users;      # sollte 3 geben
SELECT * FROM groups;            # sollte 1 Gruppe zeigen
SELECT * FROM shopping_items;    # sollte Items zeigen
\q
```

---

#### **Dienstag Checkpoint (17:00 Uhr):**
- [ ] PostgreSQL läuft auf jedem Rechner
- [ ] Datenbank `shopping_list` existiert
- [ ] 9 Tabellen mit Daten
- [ ] Seed-Daten sind geladen
- [ ] Alle können sich connecten: `psql -U developer -d shopping_list`

---

### **Mittwoch: Java HTTP-Server Grundgerüst**
**Owner:** Person 3 & 4 (Backend)
**Dauer:** 5-6 Stunden
**Kategorie:** Backend

#### **Meilenstein Ende Mittwoch:**
Java HTTP-Server läuft auf Port 8080, antwortet auf GET /api/health mit JSON, antwortet auf GET /api/items, kennt JSON-Responses und URL-Routing.

#### **Aufgaben (Task-ID: T1.3.x)**

##### **T1.3.1 - Vanilla Java HTTP-Server (Hello World)**
**Owner:** Person 3 & 4
**Dauer:** 2 Stunden

**Was ist DONE?**
- [ ] `HttpServer.java` existiert in `src/main/java/com/shoppinglist/server/`
- [ ] Server kompiliert fehler
- [ ] Server läuft auf Port 8080: `java -cp src/main/java com.shoppinglist.server.HttpServer`
- [ ] `curl http://localhost:8080/` gibt "Hello, World!" zurück
- [ ] Log zeigt: "Server läuft auf Port 8080"

**Code-Vorlage:** Siehe T1.3.1 in 01-projekt-setup.md Aufgabendefinition oder 04-java-http-server.md

---

##### **T1.3.2 - JSON Response statt Plaintext**
**Owner:** Person 3 & 4
**Dauer:** 1,5 Stunden

**Was ist DONE?**
- [ ] GET /api/health gibt `{"status": "ok"}` zurück
- [ ] Content-Type Header ist `application/json`
- [ ] Status-Code ist 200
- [ ] `curl -H "Accept: application/json" http://localhost:8080/api/health` gibt valides JSON

**Test:**
```bash
curl http://localhost:8080/api/health
# Output: {"status":"ok"}
```

---

##### **T1.3.3 - URL-Routing (unterschiedliche Endpoints)**
**Owner:** Person 3 & 4
**Dauer:** 1,5 Stunden

**Was ist DONE?**
- [ ] GET /api/health gibt `{"status": "ok"}`
- [ ] GET /api/items gibt `{"items": []}`
- [ ] GET /api/groups gibt`{"groups": []}`
- [ ] GET /unknown gibt 404 mit `{"error": "Not Found"}`

**Tests:**
```bash
curl http://localhost:8080/api/health       # {"status":"ok"}
curl http://localhost:8080/api/items        # {"items":[]}
curl http://localhost:8080/api/groups       # {"groups":[]}
curl http://localhost:8080/unknown          # HTTP/1.1 404...{"error":"Not Found"}
```

---

##### **T1.3.4 - Request Parsing (GET Parameter optionen)**
**Owner:** Person 4
**Dauer:** 1,5 Stunden

**Was ist DONE?**
- [ ] Request-Zeile wird geparst: z.B. `GET /api/items?limit=10 HTTP/1.1`
- [ ] Query-Parameter können ausgelesen werden
- [ ] GET /api/items?limit=5 gibt unterschiedliche Antwort als GET /api/items

**Beispiel URL:**
```bash
curl "http://localhost:8080/api/items?limit=5"
# Könnte in Zukunft: {"items": [...], "limit": 5}
```

---

#### **Mittwoch Checkpoint (17:00 Uhr):**
- [ ] httpServer.jar/class existiert
- [ ] Server läuft stabil auf Port 8080
- [ ] 4+ Endpoints sind erreichbar
- [ ] JSON wird korrekt formatiert
- [ ] Alle HTTP-Status Codes sind korrekt (200, 404, etc.)

---

### **Donnerstag: JDBC Datenbank Verbindung & Integration**
**Owner:** Person 3 & 4 (Backend) + Person 5 (Database)
**Dauer:** 4-5 Stunden
**Kategorie:** Backend + Database

#### **Meilenstein Ende Donnerstag:**
Java Backend kann Datenbank-Queries ausführen und via API zurückgeben. GET /api/users gibt echte User-Daten aus der Datenbank.

#### **Aufgaben (Task-ID: T1.4.x)**

##### **T1.4.1 - PostgreSQL JDBC Driver einbinden**
**Owner:** Person 3 & 4
**Dauer:** 30 min

**Was ist DONE?**
- [ ] `postgresql-42.x.x.jar` ist in dem Projekt oder im Klassenpfad
- [ ] Java kann die Klasse `org.postgresql.Driver` finden
- [ ] Kompilation erfolgt ohne JDBC-Fehler

**Installation:**
```bash
# Download the JDBC driver
cd lib/  # (oder in Projektroot)
wget https://jdbc.postgresql.org/download/postgresql-42.6.0.jar
```

**Compile mit JAR im Pfad:**
```bash
javac -cp lib/postgresql-42.6.0.jar src/main/java/com/shoppinglist/repository/DatabaseConnection.java
```

---

##### **T1.4.2 - Connection String & Authentifizierung**
**Owner:** Person 5 + Person 3
**Dauer:** 45 min

**Was ist DONE?**
- [ ] Connection String aus application.properties geladen
- [ ] Benutzer `developer` kann authentifizieren
- [ ] "✅ Verbindung erfolgreich!" wird ausgegeben
- [ ] Keine SQL-Fehler im Logs

**Code zu schreiben:** `src/main/java/com/shoppinglist/repository/DatabaseConnection.java`

**Essentieller Code-Teil:**
```java
String url = "jdbc:postgresql://localhost:5432/shopping_list";
String user = "developer";
String password = "dev_password";

Connection conn = DriverManager.getConnection(url, user, password);
System.out.println("✅ Verbindung zu PostgreSQL erfolgreich!");
```

---

##### **T1.4.3 - SELECT Query ausführen**
**Owner:** Person 3 & 4 (mit Person 5 Support)
**Dauer:** 1 Stunde

**Was ist DONE?**
- [ ] SELECT COUNT(*) FROM users; wird ausgeführt
- [ ] Ergebnis wird angezeigt (sollte 3 sein von Seed-Daten)
- [ ] SELECT * FROM groups; zeigt Test-Gruppe an
- [ ] Keine SQL-Fehler

**Test-Output:**
```
✅ Verbindung zu PostgreSQL erfolgreich!
Anzahl User: 3
Anzahl Gruppen: 1
User: [
  {id: 1, email: alice@example.com, ...},
  ...
]
```

---

##### **T1.4.4 - GET /api/users kehrt Datenbank-Daten zurück**
**Owner:** Person 3 & 4
**Dauer:** 1,5 Stunden

**Was ist DONE?**
- [ ] GET /api/users gibt alle Users aus der Datenbank als JSON
- [ ] GET /api/groups gibt alle Gruppen aus der Datenbank
- [ ] Die API-Response enthält echte Daten (nicht hardcodiert [])

**API Response:**
```bash
curl http://localhost:8080/api/users
# Gibt aus:
{"users": [
  {"id": 1, "email": "alice@example.com", "firstName": "Alice", "lastName": "Miller"},
  {"id": 2, "email": "bob@example.com", "firstName": "Bob", "lastName": "Johnson"},
  {"id": 3, "email": "charlie@example.com", "firstName": "Charlie", "lastName": "Davis"}
]}
```

---

#### **Donnerstag Checkpoint (17:00 Uhr):**
- [ ] Alle Java-Services starten ohne Fehler
- [ ] Datenbank-Connection ist stabil
- [ ] GET /api/users gibt echte Daten
- [ ] GET /api/groups gibt echte Daten
- [ ] Keine SQL-Injection Vulnerabilities offensichtlich

---

### **Freitag: Integration Test & Wochenabschluss**
**Owner:** Person 6 (Integration & QA)
**Dauer:** 3-4 Stunden
**Kategorie:** QA / DevOps

#### **Meilenstein Ende Freitag:**
Alle Systeme funktionieren zusammen: Frontend kann Backend aufrufen, Backend liest aus Datenbank, Dokumentation ist aktualisiert, Woche 1 ist im Rückblick klar.

#### **Aufgaben (Task-ID: T1.5.x)**

##### **T1.5.1 - Frontend kann Backend aufrufen (HTTP Request)**
**Owner:** Person 1 & 2 (Frontend)
**Dauer:** 1 Stunde

**Was ist DONE?**
- [ ] `public/pages/index.html` existiert
- [ ] HTML hat einen Button "Test API"
- [ ] JavaScript fetch() ruft GET /api/health auf
- [ ] Browser-Console zeigt: `✅ Backend antwortet: {status: "ok"}`
- [ ] Keine CORS-Fehler (sollte lokal auf Port 5500 laufen)

**Minimal HTML:**
```html
<!DOCTYPE html>
<html>
<body>
  <button id="btn">Test Backend</button>
  <pre id="result"></pre>
  <script>
    document.getElementById("btn").addEventListener("click", async () => {
      const res = await fetch("http://localhost:8080/api/health");
      const data = await res.json();
      document.getElementById("result").textContent = JSON.stringify(data, null, 2);
    });
  </script>
</body>
</html>
```

---

##### **T1.5.2 - Integration Test: Frontend → Backend → Datenbank**
**Owner:** Person 6 (mit Teams-Support)
**Dauer:** 1,5 Stunden

**Was ist DONE?**
- [ ] Alle 3 Layer sind ereichbar
- [ ] Datenfluss: Frontend hat Daten von Backend hat Daten von DB
- [ ] Keine Fehler in der Kette

**Test-Szenario:**
```
1. Frontend öffnet http://localhost:5500/pages/index.html
2. Button "Load Users" wird geklickt
3. JavaScript sendet: GET http://localhost:8080/api/users
4. Backend ließt: SELECT * FROM users;
5. Backend antwortet mit JSON: {"users": [id:1, email: alice@...]}
6. Frontend zeigt in der UI: "3 User geladen"
```

---

##### **T1.5.3 - Dokumentation aktualisieren & finalisieren**
**Owner:** Person 6
**Dauer:** 1 Stunde

**Was ist DONE?**
- [ ] README.md wurde aktualisiert mit "Woche 1 Ergebnisse"
- [ ] ARCHITECTURE.md wurde erstellt oder aktualisiert (Schichten-Diagramm)
- [ ] API-Endpoints sind dokumentiert (alle GET/POST Endpoints mit Beispiel-Calls)
- [ ] Installation-Guide ist aktuell (wie startet man alles lokal?)
- [ ] Setup-Guide funktioniert für neuen Developer

**Mindestens dokumentieren:**
- Setup-Schritte (Git clone, PostgreSQL, Java Compile, Run)
- 5+ API Endpoints mit curl-Beispielen
- Fehlerbehandlung (Was tun wenn X nicht läuft?)

---

##### **T1.5.4 - Code-Review aller Branches & Merge in main**
**Owner:** Person 6
**Dauer:** 1 Stunde

**Was ist DONE?**
- [ ] Mindestens 5 Pull Requests wurden reviewed
- [ ] Alle PRs haben Feedback erhalten (oder gebilligt)
- [ ] Alle 6 Feature-Branches wurden in main merget
- [ ] Kein Conflict ungelöst

**Review-Checklist für jede PR:**
- [ ] Code folgt Style-Guides (Java/JavaScript)
- [ ] Keine hardcodierten Passwörter oder Secrets
- [ ] Tests passen oder Tests schon existieren
- [ ] Commit-Message ist aussagekräftig
- [ ] Keine Breaking Changes ohne Dokumentation

---

#### **Freitag Checkpoint & **WOCHE 1 FERTIG:**

✅ **Infrastructure:**
- [ ] Git-Repository mit 25+ Commits
- [ ] 9 Datenbank-Tabellen
- [ ] Java HTTP-Server läuft stabil
- [ ] Frontend-Skeleton existiert

✅ **Team-Erfolg:**
- [ ] Alle Team-Mitglieder haben wenigstens 5 Commits
- [ ] Alle verstehen die Architektur
- [ ] Code-Review Kultur etabliert
- [ ] Daily Standups finden statt

✅ **Quality:**
- [ ] Keine kritischen Fehler bekannt
- [ ] Dokumentation ist aktualisiert
- [ ] Setup-Guide funktioniert für andere
- [ ] Keine Secrets im Repo

✅ **Next Week Ready:**
- [ ] Liste von Tasks für Woche 2 ist bereit
- [ ] Team hat gelernt: Git, Java Basics, SQL Basics, HTTP Basics
- [ ] Mood: "Wir können das!" 🚀

---

---

## 📚 Dokumentations-Struktur

```
docs/
├── 01-PROJEKTPLAN.md (dieser Datei)
├── 02-ANFORDERUNGEN.md
├── 03-ARCHITEKTUR.md
├── 04-DATENBANKSCHEMA.md
├── 05-API-DOKUMENTATION.md
├── 06-FRONTEND-GUIDE.md
├── 07-INSTALLATION-DEPLOYMENT.md
├── 08-BENUTZERHANDBUCH.md
└── 09-LEARNINGS.md (wird am Ende gefüllt)
```

---

## 🎓 Learning-Fokus

Weil das ein **Lern-Projekt** ist, konzentrieren wir uns auf:

1. **Vanilla Development** → Frameworks später verstehen
2. **Architecture Patterns** → Service-Layer, Separation of Concerns
3. **Database Design** → Normalisierung, Indexierung, Queries
4. **Security Basics** → Authentication, SQL-Injection, XSS, CSRF
5. **Real-Time Kommunikation** → WebSockets verstehen
6. **Testing** → Warum Tests wichtig sind
7. **Git & Collaboration** → Branching, Code-Reviews, Merging

**Knowledge Sharing:** Jede Person erklärt ihre Komponente den anderen (Pair-Programming Days!)

---

## ⚠️ Risiken & Mitigation

| Risiko | Wahrscheinlichkeit | Impact | Mitigation |
|--------|-------------------|--------|-----------|
| Wenig Erfahrung → Zu ambitioniert | 🔴 Hoch | 🔴 Hoch | MVP streng einhalten, regelmäßige Reviews |
| Datenbank-Design falsch | 🟡 Mittel | 🔴 Hoch | Schema-Design vor Coding abnehmem |
| WebSocket-Komplexität | 🟡 Mittel | 🟡 Mittel | Einfach starten (Polling → WebSocket) |
| Team-Koordination schwierig | 🟡 Mittel | 🟡 Mittel | Daily Standups, klare Task-Verteilung |
| Zeit-Druck am Ende | 🔴 Hoch | 🔴 Hoch | Testing & Docs schon einplanen, nicht am Ende |

---

## 📊 Erfolgs-Kriterien

Das Projekt ist erfolgreich, wenn:

- ✅ MVP vollständig implementiert
- ✅ Alle kritischen Features funktionstüchtig
- ✅ Echtzeit-Synchronisation stabil läuft
- ✅ Vollständige Dokumentation verfügbar
- ✅ Sicherheitsaspekte berücksichtigt
- ✅ Team hat Kompetenzen aufgebaut
- ✅ Code ist wartbar & dokumentiert
- ✅ Keine kritischen Bugs im MVP

---

## 🚀 Nächste Schritte

1. **Projektplan-Review:** Feedback vom Team zu Zeitschätzungen?
2. **Anforderungen detaillieren** (Datei 02)
3. **Architektur präzisieren** (Datei 03)
4. **Datenbank-Schema entwerfen** (Datei 04)
5. **Team-Rollen offiziell zuweisen**
6. **Git-Repository aufsetzen** (WOCHE 1)
7. **Erstes Daily Standup** (Mo in Woche 1)

---

**Fragen zum Plan? Rückmeldungen?**
