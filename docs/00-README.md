# 📚 Dokumentations-Übersicht - Geteilte Einkaufsliste

**Status:** ✅ Planung Abgeschlossen
**Datum:** 2026-03-21
**Team:** 6 Personen | **Dauer:** 4 Wochen (20 Arbeitstage)

---

## 📋 Was wurde geplant?

### 1️⃣ [01-PROJEKTPLAN.md](./01-PROJEKTPLAN.md)
**Der strategische Master-Plan**
- ✅ Projektziel & Kernwert definiert
- ✅ MVP-Features priorisiert (5 kritisch, 2 wichtig)
- ✅ Was NICHT im MVP ist (Scan/KI, Maps - Phase 2)
- ✅ 4-Wochen-Roadmap mit Meilensteinen
- ✅ Team-Struktur & Rollen (wer macht was)
- ✅ Risiko-Management & Mitigation
- ✅ Erfolgsmetriken

**Für wen?** Product Owner, Project Manager, Stakeholder

---

### 2️⃣ [02-ANFORDERUNGEN.md](./02-ANFORDERUNGEN.md)
**Die User Stories & Akzeptanzkriterien**
- ✅ 7 Feature-Module mit User Stories
- ✅ Klare Akzeptanzkriterien (was bedeutet "fertig"?)
- ✅ Sicherheits- & Performance-Anforderungen
- ✅ Was is optional / später / nicht im Scope

**Für wen?** Entwickler, QA, Designer

---

### 3️⃣ [03-ARCHITEKTUR.md](./03-ARCHITEKTUR.md)
**Die technische Blaupause**
- ✅ System-Diagramm (Frontend ↔ Backend ↔ DB)
- ✅ REST API-Struktur mit Endpoints
- ✅ WebSocket für Echtzeit
- ✅ Java-Modul-Struktur (Services, DAOs, Controller)
- ✅ Frontend-Struktur (HTML/CSS/JS)
- ✅ Authentication-Flow
- ✅ Echtzeit-Datenfluss-Beispiel
- ✅ Security-Implementation
- ✅ Error-Handling

**Für wen?** Backend- & Frontend-Entwickler

---

### 4️⃣ [04-DATENBANKSCHEMA.md](./04-DATENBANKSCHEMA.md)
**Die Datenbank-Spezifikation**
- ✅ ER-Diagramm mit allen Tabellen
- ✅ Complete SQL DDL (CREATE TABLE Statements)
- ✅ Constraints, Indizes, Relationships
- ✅ Normalisierung (3NF)
- ✅ Häufig benutzte Queries
- ✅ Test-Daten für Entwicklung
- ✅ Migration-Strategie

**Für wen?** Database Engineer, Backend-Entwickler

---

## 🚀 Wie geht es jetzt weiter?

### **WOCHE 1 - Sofort-Maßnahmen:**

1. **Repository aufsetzen**
   ```bash
   git clone <your-repo>
   cd Geteilte-Einkaufsliste
   ```

2. **Ordner-Struktur erstellen**
   ```
   Geteilte-Einkaufsliste/
   ├── docs/           (Dokumentation - bereits erstellt!)
   ├── src/
   │   ├── main/java/  (Java Backend)
   │   └── test/java/  (Tests)
   ├── public/         (Frontend HTML/CSS/JS)
   └── db/             (SQL Scripts)
   ```

3. **PostgreSQL aufsetzen**
   - Lokalinstanz starten
   - Datenbank erstellen: `createdb shopping_list`
   - Schema laden: `psql shopping_list < docs/database_init.sql`

4. **Team-Kickoff (2h)**
   - Projektplan präsentieren (01)
   - Rollen verteilen (siehe Tabelle in 01)
   - Architektur durchgehen (03)
   - Questions klären

5. **Team-Setup**
   - Git Workflow festlegen (Feature Branches, PR Reviews)
   - Daily Standup Schedule (z.B. 10:00 Uhr)
   - Communication Channel (Slack, Discord, etc.)
   - Pair Programming Days planen

---

## 📊 MVP Feature-Matrix

| Feature | Woche | Team | Status |
|---------|-------|------|--------|
| **Registrierung & Login** | 1-2 | Frontend + Backend | 🔴 To Do |
| **Profil** | 2 | Frontend + Backend | 🔴 To Do |
| **Gruppen-Management** | 2 | Backend + Frontend | 🔴 To Do |
| **Einkaufsliste** | 2-3 | Frontend + Backend | 🔴 To Do |
| **Ausgabenverteilung** | 3 | Backend + Frontend | 🔴 To Do |
| **WebSocket Echtzeit** | 3 | Backend + Frontend | 🔴 To Do |
| **Chat** | 3 | Backend + Frontend | 🔴 To Do |
| **Budget** | 3 | Backend + Frontend | 🔴 To Do |
| **Testing & Bugs** | 4 | Alle | 🔴 To Do |
| **Dokumentation & Deploy** | 4 | Alle | 🔴 To Do |

---

## 🎓 Learning-Fokus pro Person

### Person 1: Frontend-Lead
- **Ziel:** Responsive HTML/CSS/JavaScript Grid
- **Lernziele:**
  - DOM Manipulation mit vanilla JS
  - Form Validierung
  - Real-Time UI Updates (WebSocket)
- **Hauptdateien:** `public/pages/`, `public/js/`

### Person 2: Frontend
- **Ziel:** Alle UI-Komponenten umsetzen
- **Lernziele:**
  - HTML Semantik
  - CSS Flexbox/Grid
  - Asynchrone JavaScript (Fetch API, WebSocket)
- **Hauptdateien:** `public/pages/`, `public/css/`

### Person 3: Backend-Lead
- **Ziel:** Java HTTP-Server & Service-Layer Architecture
- **Lernziele:**
  - Java Streams & Collections
  - OOP Patterns (Service, DAO, Model)
  - REST API Design
  - WebSocket Handling
- **Hauptdateien:** `src/main/java/server/`, `src/main/java/service/`

### Person 4: Backend
- **Ziel:** Services & Business-Logic implementieren
- **Lernziele:**
  - Java Service-Pattern
  - Geschäftslogik (Expense-Splitting, Balance)
  - Error-Handling
  - Unit-Testing
- **Hauptdateien:** `src/main/java/service/`, `src/test/`

### Person 5: Database-Lead
- **Ziel:** Datenbank-Design & JDBC
- **Lernziele:**
  - Datenbank-Normalisierung
  - SQL Queries optimieren
  - JDBC Connection Pooling
  - Index-Strategie
- **Hauptdateien:** `src/main/java/repository/`, `db/schema.sql`

### Person 6: Integration & QA
- **Ziel:** End-to-End-Testing & Deployment
- **Lernziele:**
  - Test-Pyramide (Unit/Integration/E2E)
  - Debugging (Frontend & Backend)
  - Performance-Profiling
  - Deployment & DevOps Basics
- **Hauptdateien:** `src/test/`, `docs/`

---

## 💬 Häufige Fragen während Planung

### F: "Warum keine Frameworks wie Spring Boot oder React?"
**A:** Das ist Absicht! Als Lern-Projekt verstehst ihr die **Grundlagen** besser:
- Spring Boot versteckt viel Magic
- Mit Vanilla Java lernt ihr: HTTP-Handling, JDBC, Service-Pattern
- Mit Vanilla JS lernt ihr: DOM-APIs, Fetch, WebSocket nativ
- Das Verständnis trägt ihr dann zu Frameworks mit!

### F: "4 Wochen für MVP - ist das realistisch?"
**A:** Ja, mit diesen Bedingungen:
- MVP ist schmal (8 Features, davon 5 kritisch)
- Keine Fancy UI (funktional statt schön)
- Agile Working (Testen & Reviewen parallel)
- Daily Standups halten Läufe auf Track
- Pair Programming beschleunigt Lernen

### F: "Was wenn wir Features nicht schaffen?"
**A:** Priorisierung:
```
🔴 MUST-HAVE (Woche 1-3):
  - Auth (Login/Register)
  - Gruppen & Items
  - Ausgabenverteilung

🟡 SHOULD-HAVE (Woche 3-4):
  - Chat
  - WebSocket Integration
  - Budget

🟢 NICE-TO-HAVE (Phase 2):
  - Maps
  - AI-Scan
  - Dark Mode
```

### F: "Wie organisieren wir Code-Reviews?"
**A:** Best-Practice für euer Team:
1. Feature-Branch pro Task (`feature/auth-login`)
2. Code-Review vor Merge (mindestens 2 Personen)
3. Checklist: Tests? Dokumentation? Security?
4. Lernperspektive: "Wie könnten wir das besser machen?"

---

## 📅 Konkrete nächste Schritte [Diese Woche]

- [ ] **Montag 09:00** - Team-Meeting: Projektplan vorstellen
- [ ] **Montag 10:00** - Git-Repo Setup & zugeben
- [ ] **Montag 13:00** - Datenbank lokal aufsetzen (Person 5 leitet)
- [ ] **Dienstag** - Paar-Setup (Frontend, Backend, DB)
- [ ] **Dienstag 14:00** - Architektur Deep-Dive (Person 1-6)
- [ ] **Mittwoch** - Erste Tasks starten
  - Backend-Lead: HTTP-Server Grundlage
  - Frontend-Lead: HTML-Template für Login
  - DB-Lead: SQL-Schema testen

---

## 📖 Wie die Dokumentation nutzen?

```
Situation                           → Lies
"Ich weiß nicht, was das Proj ist" → 01-PROJEKTPLAN.md
"Ich weiß nicht, was Features"     → 02-ANFORDERUNGEN.md
"Wie baue ich die Architektur?"    → 03-ARCHITEKTUR.md
"Welche Tabellen brauche ich?"     → 04-DATENBANKSCHEMA.md
"Wie nutze ich die API?"           → 05-API-DOKUMENTATION.md (kommt)
"Wie installiere ich alles?"       → 07-INSTALLATION-DEPLOYMENT.md (kommt)
"Ich bin User, wie nutze ich?"     → 08-BENUTZERHANDBUCH.md (kommt)
```

---

## ✅ Checkliste vor Start

- [ ] Projektplan-Dokumente gelesen (alle Personen)
- [ ] Rollen sind klar verteilt
- [ ] PostgreSQL läuft lokal
- [ ] Git-Repo ist eingerichtet
- [ ] Erstes Daily Standup ist geplant
- [ ] Pair-Programming Sessions sind geplant
- [ ] Fragen geklärt (QA mit Mentor)

---

## 🎯 Finale Erinnerung an das Team

**Das ist ein LERN-Projekt. Prioritäten:**

1. **Verstehen** > Schnelligkeit
2. **Code-Qualität** > Perfektionismus
3. **Knowledge-Sharing** > Einzelkämpfer
4. **Testing** > "Sieht aus, als würde es funktionieren"
5. **Dokumentation** > Code ohne Erklärung

**Euer Mentor ist da für:**
- Architecture-Fragen
- Code-Reviews
- Debugging-Sessions (wenn festgefahren)
- Learning-Gaps füllen
- Scope-Anpassungen aktualisiera

---

**🚀 Ready to code? Los geht's in Woche 1!**

Fragen zur Planung? Rückmeldungen? Schreib mir Bescheid! 📧

Nächste Dateien kommen später:
- 05-API-DOKUMENTATION.md (Alle Endpoints)
- 06-FRONTEND-GUIDE.md (UI-Komponenten, JS-Patterns)
- 07-INSTALLATION-DEPLOYMENT.md (Setup-Guide)
- 08-BENUTZERHANDBUCH.md (Für Endnutzer)
- 09-LESSONS-LEARNED.md (Am Ende)
