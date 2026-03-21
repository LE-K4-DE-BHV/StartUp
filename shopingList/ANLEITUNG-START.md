# 🚀 START HIER - Schritt-für-Schritt Anleitungen für dein Team

**Erstellt:** 2026-03-21  
**Status:** Woche 1 komplett, Wochen 2-4 in Planung  
**Ziel:** Anfänger-Team sicher zur produktiven App führen

---

## 📖 Wo finde ich die Anleitungen?

```
shopingList/
├── docs/
│   ├── anleitung/                    ← DU BIST HIER
│   │   ├── 00-ANLEITUNG-UEBERSICHT.md  ← ZUGEHÖRIGE Navigation
│   │   ├── woche-1/
│   │   │   ├── README.md              ← Wochenplan
│   │   │   ├── 01-projekt-setup.md    ← Tag 1
│   │   │   ├── 03-postgresql-setup.md ← PostgreSQL
│   │   │   ├── 04-java-http-server.md ← Java Server
│   │   │   └── 05-datenbank-implementieren.md ← DB Schema
│   │   ├── woche-2/
│   │   ├── woche-3/
│   │   └── woche-4/
│   ├── 00-README.md
│   ├── 01-PROJEKTPLAN.md
│   ├── 02-ANFORDERUNGEN.md
│   ├── 03-ARCHITEKTUR.md
│   └── 04-DATENBANKSCHEMA.md
└── ANLEITUNG-START.md  ← Diese Datei
```

---

## 🎯 Schnelle Navigation

### **Ich bin neu im Projekt - wo fange ich an?**
1. Lese: `docs/00-README.md` (10 min)
2. Lese: `docs/01-PROJEKTPLAN.md` (30 min)
3. Starte: `docs/anleitung/woche-1/README.md` (Montag Morgen)

### **Ich bin Developer - welche Anleitung brauche ich?**

**Frontend-Dev (Person 1 + 2):**
- Start: [Woche 1: Projekt-Setup](./woche-1/README.md)
- Mit Fokus auf: `01-projekt-setup.md`
- Dann: Woche 2 Login-Frontend

**Backend-Dev (Person 3 + 4):**
- Start: [Woche 1: Projekt-Setup](./woche-1/README.md)
- Mit Fokus auf: `04-java-http-server.md`
- Dann: Woche 2 Login-Backend

**Database-Dev (Person 5):**
- Start: [Woche 1: PostgreSQL](./woche-1/03-postgresql-setup.md) (Dienstag)
- Dann: [Schema implementieren](./woche-1/05-datenbank-implementieren.md) (Mittwoch)

**QA/Integration (Person 6):**
- Start: [Woche 1: Projekt-Setup](./woche-1/README.md)
- Überwachen: Alle Schritte & Dokumentieren

### **Ich stecke fest - was tun?**
1. **In der Anleitung:** Schaut die "❓ Häufige Probleme" Sektion
2. **GitHub:** Sucht nach dem Fehler auf Stack Overflow
3. **Team:** Fragt in der Slack/Discord
4. **Mentor:** Letzter Ausweg - der Mentor ist da!

---

## 📅 Ablauf je Tag

```
09:00 - 09:15  → Daily Standup (15 min)
                 "Was macht ihr heute? Wo steckt ihr fest?"

09:15 - 09:30  → Tages-Plan
                 Schaut die Anleitung für heute durch

09:30 - 16:30  → Entwicklung
                 FOLGT DIE ANLEITUNG SCHRITT FÜR SCHRITT!
                 Test jedes Prüfpunkt
                 Pair-Programming wenn nötig

16:30 - 17:00  → Standup & Planung für morgen
                 Was ist fertig? Was kommt morgen?
```

---

## ✅ Checklisten pro Tag

### **MONTAG (Projekt-Setup)**
- [ ] Repository geklont / im richtigen Ordner
- [ ] Ordner-Struktur erstellt (src/, public/, db/, docs/)
- [ ] .gitignore & application.properties erstellt
- [ ] Erstes Commit gepusht
- [ ] Jeder kann `git status` ausführen ohne Fehler
- [ ] **Testergebnis:** Git-Flow funktioniert ✅

### **DIENSTAG (PostgreSQL)**
- [ ] PostgreSQL installiert (`psql --version` funktioniert)
- [ ] Datenbank `shopping_list` erstellt
- [ ] Benutzer `developer` erstellt
- [ ] Jeder kann `psql -h localhost -U developer -d shopping_list` ausführen
- [ ] **Testergebnis:** Alle können sich mit DB verbinden ✅

### **MITTWOCH (HTTP-Server)**
- [ ] Java-Projekt-Struktur (src/java/com/shoppinglist/)
- [ ] HttpServer.java kompiliert
- [ ] ClientHandler.java kompiliert
- [ ] Server startet: `java com.shoppinglist.Main`
- [ ] curl Tests funktionieren (3/3 Routes)
- [ ] **Testergebnis:** Server antwortet auf Requests ✅

### **DONNERSTAG (Datenbank-Schema)**
- [ ] db/schema.sql existiert
- [ ] db/seed-data.sql existiert
- [ ] Alle 9 Tabellen erstellt (prüft mit `\dt`)
- [ ] Test-Daten geladen (3 Users, 1 Group, etc.)
- [ ] 5 Test-Queries funktionieren
- [ ] **Testergebnis:** Datenbank ist populiert ✅

### **FREITAG (Integration & Wochenabschluss)**
- [ ] Alles zusammen funktioniert
- [ ] Keine Fehler in Git-Log
- [ ] Wochenabschluss-Meeting (15:00)
  - [ ] Was lernten wir?
  - [ ] Was war schwierig?
  - [ ] Vorbereitung für Woche 2?

---

## 🎓 Lernprinzipien während der Woche

### 🚫 NICHT machen:
- Nur Code kopieren und nicht verstehen
- Rush durch Features ohne zu testen
- Nicht fragen wenn man nicht versteht
- Einzelkämpfer-Mentality

### ✅ BESSER:
- **Verstehen > Speed:** Lieber langsamer und gründlich
- **Testen parallel:** Nicht erst am Ende testen
- **Fragen früh:** Nicht nach 2h auf der Stelle rumfahren
- **Knowledge-Sharing:** Jeder erklärt seinen Bereich
- **Pair-Programming:** 2er-Teams für komplexe Sachen

---

## 📞 Schnelle Hilfe

**Die Anleitung ist zu schnell?**
→ Die Schritte sind designed für 30-60 min. Wenn ihr langsamer seid → OK! Lieber gründlich!

**Ich verstehe Java nicht?**
→ Das ist normal! Lest die Kommentare im Code. Google die Concept separat.

**Ich verstehe SQL nicht?**
→ "Introduction to SQL" Videos gucken parallel. Links in den Anleitungen.

**Wir brauchen länger als Woche 1?**
→ Kein Problem! Verlängert um 1-2 Tage. Die Planung hat Puffer.

---

## 🚀 Los geht's!

**Bereit für Montag?**

1. **Alle zusammen:**
   - Diese Datei lesen ✅
   - [Woche 1 Übersicht](./woche-1/README.md) lesen (20 min)
   - Fragen klären

2. **Montag Morgen:**
   - Starten mit [01-projekt-setup.md](./woche-1/01-projekt-setup.md)
   - Person 6 leitet
   - Alle folgen

3. **Daily Standups:**
   - Kurz halten (15 min)
   - "Was? Wer? Bis wann?"
   - Blockers aufzeigen

---

## 📊 Erfolgs-Metriken

Am **Freitag 17:00** sollte Folgendes wahr sein:

```
✅ MINDESTENS:
   - Git-Workflow funktioniert
   - PostgreSQL läuft lokal
   - Java-HTTP-Server funktioniert
   - Datenbank-Schema populiert

✅ IDEAL:
   - Alle obigen Punkte
   + Code-Reviews laufen
   + Paar-Programming war produktiv
   + Team versteht Architektur
```

---

## 🎯 Mentale Vorbereitung

**Das erwartet euch:**
- 5 Tage intensives Lernen
- Viele neue Konzepte (HTTP, SQL, Java)
- Frustration an Tag 2-3 (normal!)
- Großes Aha-Moment am Freitag 😄

**Das garantiere ich:**
- Die Anleitungen sind TESTBAR
- Jeder Schritt ist PRAKTISCH
- Fehler sind DOKUMENTIERT
- Mentor antwortet auf FRAGEN

---

## 📚 Zusätzliche Ressourcen

Diese Seite: **Orientierung geben**
- Links zu freien Online-Kursen
- YouTube-Channels
- Dokumentation

Siehe: `docs/anleitung/woche-1/README.md` → "Weiterführende Ressourcen"

---

**🚀 VIEL ERFOLG!**

Fragen? → Stellt sie sofort!
Stuck? → Haltet an und fragt dem Team!
Gutes Gefühl? → Das ist normal, ihr schafft es!

---

**Started:** 2026-03-21  
**Status:** 🟢 Ready to Go  
**Next:** Montag 09:00 - Woche 1 Kickoff!
