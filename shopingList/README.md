# Geteilte Einkaufsliste - Projekt

Eine Echtzeit-Einkaufslisten-App für Freunde, Familien und Partner zum fairen Teilen von Ausgaben.

## 🚀 Quick Start für das Team

**Alle sollten anfangen mit:** [`docs/00-README.md`](./docs/00-README.md)

### Dokumentation nach Rolle:

| Rolle | Start-Datei | Fokus |
|-------|------------|-------|
| **Project Manager** | [01-PROJEKTPLAN.md](./docs/01-PROJEKTPLAN.md) | MVP, Timeline, Risiken |
| **Frontend-Dev** | [03-ARCHITEKTUR.md](./docs/03-ARCHITEKTUR.md) | API-Endpoints, UI-Struktur |
| **Backend-Dev** | [03-ARCHITEKTUR.md](./docs/03-ARCHITEKTUR.md) + [02-ANFORDERUNGEN.md](./docs/02-ANFORDERUNGEN.md) | Services, REST API |
| **Database-Dev** | [04-DATENBANKSCHEMA.md](./docs/04-DATENBANKSCHEMA.md) | Schema, Queries, Indizes |
| **QA/Tester** | [02-ANFORDERUNGEN.md](./docs/02-ANFORDERUNGEN.md) | Akzeptanzkriterien, Test-Szenarien |

## 📚 Dokumentation (docs/)

1. **[00-README.md](./docs/00-README.md)** - Dokumentations-Übersicht & Planung
2. **[01-PROJEKTPLAN.md](./docs/01-PROJEKTPLAN.md)** - Strategie, MVP, 4-Wochen-Roadmap
3. **[02-ANFORDERUNGEN.md](./docs/02-ANFORDERUNGEN.md)** - User Stories
4. **[03-ARCHITEKTUR.md](./docs/03-ARCHITEKTUR.md)** - System-Design, API
5. **[04-DATENBANKSCHEMA.md](./docs/04-DATENBANKSCHEMA.md)** - SQL, Indizes

## 🎯 MVP Features

✅ Registrierung & Login
✅ Profil-Management
✅ Einkaufsgruppen-Management
✅ Einkaufsliste (Items)
✅ Ausgabenverteilung (gerecht teilen)
✅ Echtzeit-Synchronisation (WebSocket)
✅ Gruppenchat
✅ Budget-Tracking

## 🛠️ Tech-Stack

- **Frontend:** HTML5, CSS3, Vanilla JavaScript
- **Backend:** Java (Vanilla, no Frameworks)
- **Database:** PostgreSQL 14+
- **Communication:** REST API + WebSocket

## 📅 Timeline

| Woche | Focus | Features |
|-------|-------|----------|
| 1 | Setup & Grundlagen | DB, HTTP-Server, Project Setup |
| 2 | Authentifizierung & Basis | Login, Profile, Gruppen, Items |
| 3 | Echtzeit & Komplexes | WebSocket, Ausgaben, Chat |
| 4 | Testing & Rollout | Bugs fixen, Dokumentation, Deploy |

## 👥 Team & Rollen

**6 Personen, alle Anfänger** → Gemeinsames Lernen

- **Person 1:** Frontend-Lead (HTML/CSS/JS)
- **Person 2:** Frontend (JavaScript/UI)
- **Person 3:** Backend-Lead (Java Architecture)
- **Person 4:** Backend (Services, Business Logic)
- **Person 5:** Database-Lead (Schema, JDBC)
- **Person 6:** QA & Integration (Testing, Deployment)

(Details: siehe `docs/01-PROJEKTPLAN.md`)

## 🏗️ Projekt-Struktur

```
Geteilte-Einkaufsliste/
├── docs/              ← Dokumentation (wichtig!)
│   ├── 00-README.md
│   ├── 01-PROJEKTPLAN.md
│   ├── 02-ANFORDERUNGEN.md
│   ├── 03-ARCHITEKTUR.md
│   └── 04-DATENBANKSCHEMA.md
├── src/               ← Quellcode (kommt in Woche 1)
│   ├── main/java/
│   └── test/java/
├── public/            ← Frontend (HTML/CSS/JS)
│   ├── pages/
│   ├── js/
│   └── css/
├── db/                ← Database Scripts
└── README.md          ← Diese Datei
```

## 🔧 Setup Checklist (Woche 1)

- [ ] README und Projektplan gelesen
- [ ] Rollen verteilt
- [ ] PostgreSQL lokal installiert
- [ ] Git-Repository eingerichtet
- [ ] IDE konfiguriert (VSCode/IntelliJ)
- [ ] Daily Standup geplant
- [ ] Pair Programming Sessions geplant

## 💬 Häufige Fragen

**F: Warum kein Framework?**
A: Learning Purpose! Versteht die Grundlagen statt Magic.

**F: Ist 4 Wochen realistisch?**
A: Ja mit agiler Arbeitsweise, Daily Standups und guter Priorisierung.

**F: Wer ist der Mentor?**
A: Claude Code - verfügbar für Fragen, Reviews, Debugging

## 📞 Support

- Fragen zur Planung → siehe `docs/00-README.md`
- Architektur-Fragen → siehe `docs/03-ARCHITEKTUR.md`
- Datenbank-Design → siehe `docs/04-DATENBANKSCHEMA.md`
- Features verstehen → siehe `docs/02-ANFORDERUNGEN.md`

---

**Status:** Planung ✅ | Entwicklung 🔄 (startet Woche 1)
**Last Updated:** 2026-03-21