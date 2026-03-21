# 📖 Sprint-Anleitungen - Schritt-für-Schritt für Anfänger

**Status:** Für Anfänger-Teams optimiert 🎯
**Zuletzt aktualisiert:** 2026-03-21

---

## Willkommen!

Diese Anleitungen führen dein 6er-Team **Schritt-für-Schritt** durch die Umsetzung der geteilten Einkaufsliste. Jede Anleitung ist so detailliert, dass ihr sicher folgen könnt – auch ohne Framework-Erfahrung.

---

## 📋 Wie du die Anleitungen nutzt

### Für dein Team:

1. **Start der Woche** → Lest die **Wochenübersicht** (z.B. `woche-1/README.md`)
2. **Jeden Tag** → Folgt der **Tages-Anleitung** Schritt-für-Schritt
3. **Bei Fragen** → Schaut in der **FAQ-Section** nach oder fragt den Mentor
4. **Feature fertig?** → Checklist abhaken & Code-Review durchführen

### Das Team sollte sich so organisieren:

```
Morgens (09:00-10:00):
├─ Daily Standup (15 min)
├─ Tages-Übersicht lesen (15 min)
└─ Tasks verteilen (30 min)

Tagsüber (10:00-16:00):
├─ Pair Programming (siehe Anleitung)
├─ Code schreiben (Schritt-für-Schritt folgen)
└─ Testen während ihr entwickelt

Nachmittags (16:00-17:00):
├─ Code-Review & Merge
├─ Learnings dokumentieren
└─ Morgen-Planung
```

---

## 🗂️ Anleitungs-Struktur

### **WOCHE 1: Setup & Grundlagen** ✅ FERTIG

[Woche 1 Übersicht](./woche-1/README.md)

| Datei | Thema | Dauer | Wer |
|-------|-------|-------|-----|
| [01-projekt-setup.md](./woche-1/01-projekt-setup.md) | Git, Ordner-Struktur, Workflow | 1h | Alle |
| [03-postgresql-setup.md](./woche-1/03-postgresql-setup.md) | PostgreSQL Installation & DB Setup | 1.5h | Person 5 + Team |
| [04-java-http-server.md](./woche-1/04-java-http-server.md) | Erster HTTP-Server in Java | 2.5h | Person 3 + Person 4 |
| [05-datenbank-implementieren.md](./woche-1/05-datenbank-implementieren.md) | SQL Schema & Test-Daten | 2h | Person 5 |

🎯 **Meilenstein:** HTTP-Server läuft, Datenbank läuft, Team kann pushen ✅

### **WOCHE 2: Authentifizierung & Grundfeatures** 🔄 IN PLANUNG

[Woche 2 Übersicht](./woche-2/README.md)

| Datei | Thema | Dauer | Wer |
|-------|-------|-------|-----|
| 01-login-backend.md | REST API: Login implementieren | 2h | Person 3 + 4 |
| 02-registrierung-backend.md | REST API: Registrierung | 1.5h | Person 4 |
| 03-login-frontend.md | HTML/JS: Login-Seite | 1.5h | Person 1 + 2 |
| 04-profil-system.md | Backend + Frontend: Profile | 2h | Person 1 + 3 + 5 |
| 05-gruppen-management.md | Groups CRUD + UI | 2h | Person 2 + 4 |
| 06-einkaufsliste-basis.md | Items hinzufügen/löschen | 2h | Person 1 + 4 |

🎯 **Meilenstein:** Login funktioniert, Gruppen & Items sichtbar

---

### **WOCHE 3: Echtzeit & Komplexe Features** 🔄 IN PLANUNG

[Woche 3 Übersicht](./woche-3/README.md)

| Datei | Thema | Dauer | Wer |
|-------|-------|-------|-----|
| 01-websocket-server.md | WebSocket in Java aufsetzen | 2h | Person 3 |
| 02-websocket-client.md | WebSocket Client im Browser | 1.5h | Person 2 |
| 03-echtzeit-synchronisation.md | Real-Time Updates verbinden | 2h | Person 1 + 3 + 2 |
| 04-ausgabenverteilung.md | Expense Tracking & Splitting | 3h | Person 4 + 5 |
| 05-chat-system.md | Gruppenchat implementieren | 1.5h | Person 2 + 4 |
| 06-budget-feature.md | Budget-Tracking | 1.5h | Person 4 |

🎯 **Meilenstein:** Echtzeit funktioniert, Ausgaben verteilt, Chat läuft

---

### **WOCHE 4: Testing, Optimierung & Rollout** 🔄 IN PLANUNG

[Woche 4 Übersicht](./woche-4/README.md)

| Datei | Thema | Dauer | Wer |
|-------|-------|-------|-----|
| 01-unit-tests.md | Java Unit-Tests schreiben | 2h | Person 4 + 6 |
| 02-integration-tests.md | Frontend ↔ Backend Tests | 1.5h | Person 2 + 6 |
| 03-manual-testing.md | Szenarios durchspielen | 1.5h | Person 6 + Team |
| 04-bug-fixes.md | Bugs beheben & optimieren | 2h | Alle |
| 05-sicherheit.md | SQL-Injection, XSS checken | 1.5h | Person 3 + 5 |
| 06-deployment.md | App produktionsbereit | 1h | Person 6 + 3 |

🎯 **Meilenstein:** MVP ist produktionsreif, sicher, getestet

---

## 🎯 Wie eine Anleitung aufgebaut ist

Jede Anleitung folgt diesem Muster:

```
# Feature Name

## 🎯 Ziel dieser Anleitung
Was werdet ihr am Ende können?

## ⏱️ Geschätzte Zeit
30 min - 2h

## 📋 Voraussetzungen
Was muss schon fertig sein?

## 👥 Wer macht was?
Rollen und Pair-Programming Setup

---

## Schritt-für-Schritt Anleitung

### Schritt 1: [Was tun wir hier?]
**Wer:** Person X & Y
**Zeit:** 10 min

Detaillierte Erklärung...

**Terminal-Befehle zum Kopieren:**
```bash
git checkout -b feature/xyz
```

**Code-Beispiel:**
```java
public class MyClass {
    // Code hier
}
```

**Resultat: Was sollten wir sehen?**
- ✓ Das sollte passieren
- ✓ Das sollte sichtbar sein

---

### Schritt 2: [Nächster Schritt]
...

## ✅ Fertig? Checklist

- [ ] Code geschrieben
- [ ] Lokal getestet
- [ ] Git pushed (eigener Branch)
- [ ] Code-Review angefordert
- [ ] Feedback eingebaut
- [ ] In main gemerged

## ❓ Häufige Probleme

**Problem:** Fehler beim Start
**Lösung:** ...

## 🔗 Weiterführende Links

- Link zu Video
- Link zu Doku
```

---

## 🚀 Sofort-Einsatz

### Montag Morgen (Kickoff):

1. **Team versammeln** (15 min)
2. **Diese Übersicht lesen** (10 min)
3. **Rollen verteilen:** Wer macht was in Woche 1?
4. **Erste Anleitung starten:** [woche-1/01-projekt-setup.md](./woche-1/01-projekt-setup.md)

### Pro Tag:

- Morgens: Anleitung für heute lesen (10 min)
- Tagsüber: Schritt-für-Schritt folgen & Code schreiben
- Nachmittags: Code-Review & Merge

---

## 💡 Tipps für erfolgreiches Lernen

### 1️⃣ Verstehen > Kopieren
Nicht einfach Code kopieren! Versteht jeden Schritt.

```
❌ "Ich kopier die Lösung" → Nicht gut
✅ "Ich verstehe, warum dieser Schritt nötig ist" → Gut!
```

### 2️⃣ Fehler sind Lernchancen
```
Fehler tritt auf
    ↓
Googlen, nachdenken, fragen
    ↓
Verstehen, warum es so ist
    ↓
Merken für nächstes mal ✅
```

### 3️⃣ Pair Programming ist euer Superpower
- 2 Personen, 1 Code
- Eine person tippt, andere schaut/denkt
- Jede halbe Stunde wechseln
- **Das machen die besten Teams so!**

### 4️⃣ Dokumentiert eure Learnings
Jeden Tag: "Was habe ich gelernt?"
→ Hilft der nächsten Person

---

## ❓ FAQ zur Struktur

**F: Was wenn wir schneller sind?**
A: Awesome! Startet die nächste Anleitung oder macht Code-Reviews für andere.

**F: Was wenn wir langsamer sind?**
A: Normal! Anfänger brauchen Zeit. Das ist wichtiger als schnell zu sein.
Macht statt Features lieber Unit-Tests oder Documentation.

**F: Können alle zusammen an einer Anleitung arbeiten?**
A: JA! Pair Programming für komplexe Themen ist perfekt.
3-4 Personen, 1 Screen, passend zum Team.

**F: Was wenn wir "steckenbleiben"?**
A: 1. Dokumentation lesen (Schritt nochmal)
   2. Google/Stack Overflow
   3. Team fragen
   4. Mentor fragen (letzte Option)

---

## 📅 Zeitplan für die 4 Wochen

```
Mo-Fr in jeder Woche:
09:00 - 09:15 → Daily Standup
09:15 - 09:30 → Tages-Planung (welche Anleitungen?)
09:30 - 16:30 → Entwicklung (alle folgen Anleitungen)
16:30 - 17:00 → Code-Reviews & Planung für morgen

Freitag 15:00 → Wochenabschluss & Rückblick
```

---

## 🎓 Learning-Pathways

Je nachdem, in welchem Bereich ihr arbeitet:

### Frontend-Entwickler (Person 1 + 2)
1. Git Workflow verstehen
2. HTML/CSS Basics
3. JavaScript DOM
4. Fetch API & WebSocket
5. Form Handling & Validation

### Backend-Entwickler (Person 3 + 4)
1. Git Workflow verstehen
2. Java Grundlagen (OOP)
3. HTTP/REST API verstehen
4. JDBC & Datenbank-Queries
5. WebSocket-Server
6. Service-Pattern & Business-Logic

### Database-Entwickler (Person 5)
1. Git Workflow verstehen
2. SQL Basics (DDL, DML)
3. ER-Modellierung
4. Normalisierung & Indizes
5. JDBC & Connection-Pooling
6. Performance-Tuning

### QA & Integration (Person 6)
1. Git Workflow verstehen
2. Testing-Pyramide (Unit/Integration/E2E)
3. JUnit & Java-Tests
4. Debugging (Browser DevTools, IDE)
5. Manual-Testing-Szenarien
6. Deployment-Checklisten

---

**Bereit? Los geht's! 🚀**

→ Starten mit: **[Woche 1 - Projekt Setup](./woche-1/01-projekt-setup.md)**
