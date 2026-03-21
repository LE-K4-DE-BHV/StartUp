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

## 📅 4-Wochen Sprint-Plan

### **WOCHE 1: Setup & Grundlagen**

#### Mo-Di: Projekt-Kickoff & Environments
- [ ] Git-Repository aufsetzen
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
