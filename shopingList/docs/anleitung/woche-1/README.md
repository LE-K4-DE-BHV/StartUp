# 🚀 WOCHE 1: Setup & Grundlagen

**Status:** Das Fundament aufbauen! 🏗️
**Dauer:** 5 Tage × 8h = 40h
**Team:** Alle 6 Personen
**Ziel:** Entwicklungs-Umgebung ist up, Datenbank läuft, HTTP-Server funktioniert

---

## 📋 Wochenübersicht

```
Montag:     Projekt-Setup, Git konfigurieren
Dienstag:   PostgreSQL aufsetzen
Mittwoch:   Datenbank-Schema implementieren
Donnerstag: Erster HTTP-Server in Java
Freitag:    Alles zusammen testen + Wochenabschluss
```

---

## ✅ Erfolgsmetriken für Woche 1

Am Freitag sollte Folgendes funktionieren:

- ✅ Git-Repo ist eingerichtet, alle können pushen
- ✅ PostgreSQL läuft lokal bei jedem (oder auf gemeinsamen Server)
- ✅ Datenbank-Schema ist erstellt & mit Test-Daten gefüllt
- ✅ Java HTTP-Server startet & antwortet auf Requests
- ✅ Alle können den Server starten & verstehen, wie es funktioniert
- ✅ Daily Standup-Ritual läuft
- ✅ Pair-Programming hat geklappt

---

## 👥 Team-Struktur für Woche 1

| Person | Rolle | Verantwortung | Pairing |
|--------|-------|---------------|---------|
| 1 | Frontend-Lead | UI-Struktur planen | Mit 2 |
| 2 | Frontend | HTML/CSS Vorbereitungen | Mit 1 |
| 3 | Backend-Lead | HTTP-Server, Architecture | Mit 4 |
| 4 | Backend | Java-Code, Services | Mit 3 |
| 5 | Database | PostgreSQL, Schema | Allein (aber Team supportt) |
| 6 | QA/Integration | Testing, Dokumentation | Mit allen |

---

## 📅 Tages-Plan

### **MONTAG: Projekt-Setup & Git**

→ Anleitung: [01-projekt-setup.md](./woche-1/01-projekt-setup.md)

**Morgens (09:00-10:00):**
- Team versammeln
- Diese Wochenübersicht durchgehen (15 min)
- Rollen final bestätigen (10 min)
- Ziele für Montag besprechen (10 min)
- Fragen klären (15 min)

**Tagsüber (10:00-16:30):**
- **Person 6 + Alle:** Projekt-Setup-Anleitung durchgehen (1h)
- **Person 3 + 4:** Git-Workflow lernen (1h)
- **Person 5:** PostgreSQL installation starten (parallel)
- **Person 1 + 2:** Frontend-Ordner-Struktur erstellen

**Nachmittags (16:30-17:00):**
- Code-Reviewy (falls was zu reviewen)
- Morgen-Vorbereitung

---

### **DIENSTAG: PostgreSQL & Git-Workflow**

→ Anleitung: [02-git-workflow.md](./woche-1/02-git-workflow.md) + [03-postgresql-setup.md](./woche-1/03-postgresql-setup.md)

---

### **MITTWOCH: Datenbank-Schema**

→ Anleitung: [05-datenbank-implementieren.md](./woche-1/05-datenbank-implementieren.md)

---

### **DONNERSTAG: Erster HTTP-Server**

→ Anleitung: [04-java-http-server.md](./woche-1/04-java-http-server.md)

---

### **FREITAG: Integration & Wochenabschluss**

- Alles zusammen testen
- Bugs fixen
- Wochenabschluss (15:00-17:00)

---

## 🔗 Weitere Ressourcen

- [Woche 2 Übersicht](../woche-2/README.md)
- [Projekt-Architektur](../01-PROJEKTPLAN.md)
- [FAQ & Troubleshooting](#faq)

---

## ❓ FAQ Woche 1

**F: "Ich bin Windows-User, funktioniert das auch?"**
A: JA! Git Bash & PowerShell unterstützen alle Befehle.

**F: "Kann ich statt PostgreSQL SQLite nutzen?"**
A: NEIN. Stick to PostgreSQL wie in der Planung.

**F: "Brauchen wir IDEs oder reicht ein Editor?"**
A: Für Java: IntelliJ oder VSCode mit Erweiterungen.
   Für Frontend: VSCode ist perfekt.

**F: "Kann Person 5 alleine die Datenbank machen?"**
A: JA! Das ist ihr Fokus. Aber Team sollte das Schema verstehen.

**F: "Wir sind langsamer als geplant!"**
A: Normal & OK! Lieber gründlich als schnell.
   Verlängert Woche 1 um 1-2 Tage, das ist OK.

---

**→ Weiter zu: [01-projekt-setup.md](./woche-1/01-projekt-setup.md)**
