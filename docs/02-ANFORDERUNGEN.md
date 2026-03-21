# 📋 Anforderungsspezifikation - Geteilte Einkaufsliste

**Version:** 1.0
**Status:** Draft
**Zuletzt aktualisiert:** 2026-03-21

---

## 🎯 User Stories & Anforderungen

### Feature 1: Authentifizierung (Registrierung & Login)

#### US-1.1: Benutzer-Registrierung
```
Als: Neuer Benutzer
Ich möchte: Mich mit Email und Passwort registrieren
Damit: Ich Zugang zur App bekomme

Akzeptanzkriterien:
✓ Registrierungsformular mit Email, Passwort, Passwort-Wiederholung
✓ Validierung: Email-Format, Passwort-Länge (min. 8 Zeichen)
✓ Fehlerbehandlung: Email existiert bereits, Passwort zu schwach
✓ Nach erfolgreicher Registrierung: Auto-Login oder Umleitung zu Login
✓ Passwort wird gehasht (SHA-256 oder bcrypt)
```

#### US-1.2: Benutzer-Login
```
Als: Registrierter Nutzer
Ich möchte: Mich mit Email und Passwort anmelden
Damit: Ich meine Einkaufslisten sehe

Akzeptanzkriterien:
✓ Login-Formular (Email, Passwort)
✓ Session-Management (Token oder Session-ID)
✓ Fehlerbehandlung: Ungültige Credentials, Account gesperrt
✓ "Passwort vergessen?" - Link (Optional für MVP)
✓ Sitzung bleibt 30 Tage erhalten oder bis Logout
```

---

### Feature 2: Benutzerprofil

#### US-2.1: Profil anschauen & bearbeiten
```
Als: Angemeldeter Nutzer
Ich möchte: Mein Profil sehen und bearbeiten
Damit: Meine Daten korrekt sind

Erforderliche Felder:
✓ Vorname (erforderlich)
✓ Nachname (erforderlich)
✓ Email (erforderlich, unveränderbar)
✓ Profilbild (optional, max. 5MB)
✓ Gesamtsaldo (angezeigt, nicht editierbar)

Akzeptanzkriterien:
✓ Profil-Seite zeigt aktuelle Daten
✓ Bearbeitung nur durch eigene Person
✓ Änderungen sofort gespeichert
✓ Profilbild-Upload mit Validierung
```

---

### Feature 3: Gruppen-Management

#### US-3.1: Gruppe erstellen
```
Als: Nutzer
Ich möchte: Eine neue Einkaufsgruppe erstellen
Damit: Ich mit Freunden/Familie einkaufen kann

Akzeptanzkriterien:
✓ Gruppen-Name eingeben (erforderlich, max. 50 Zeichen)
✓ Optionale Beschreibung
✓ Creator ist automatisch Admin
✓ Eindeutige Gruppen-ID generieren
✓ Gruppe ist nur für Mitglieder sichtbar
```

#### US-3.2: Nutzer zu Gruppe einladen
```
Als: Gruppen-Admin
Ich möchte: Andere Nutzer zur Gruppe einladen
Damit: Sie bei der Einkaufsliste mitwirken

Akzeptanzkriterien:
✓ "Mitglied einladen" Button
✓ Email-Adressen eingeben (eine oder mehrere)
✓ Einladungs-Link generieren oder Notification senden
✓ Eingeladene Nutzer sehen Gruppe erst nach Akzeptanz
✓ Admin kann Invitation auch stornieren
```

#### US-3.3: Gruppenmitglieder verwalten
```
Als: Gruppen-Admin
Ich möchte: Mitglieder entfernen oder Rollen ändern
Damit: Nur die richtigen Personen Zugriff haben

Rollen (MVP):
✓ Admin (kann Mitglieder verwalten, Gruppe löschen)
✓ Member (kann Items hinzufügen, Ausgaben teilen)

Akzeptanzkriterien:
✓ Liste aller Mitglieder mit Rollen
✓ Mitglied entfernen
✓ Optional: Entfernen erfordert Bestätigung
```

---

### Feature 4: Einkaufsliste

#### US-4.1: Items zu Liste hinzufügen
```
Als: Gruppen-Mitglied
Ich möchte: Items zu unserer Einkaufsliste hinzufügen
Damit: Wir nicht vergessen, was zu kaufen ist

Akzeptanzkriterien:
✓ Item-Name eingeben
✓ Quantity eingeben (Standard: 1)
✓ Kategorie wählen (Lebensmittel, Haushalt, Sonstiges)
✓ Item wird sofort in der Liste sichtbar
✓ Item zeigt wer es hinzugefügt hat + Zeitstempel
```

#### US-4.2: Items abhaken / erledigt markieren
```
Als: Gruppen-Mitglied
Ich möchte: Items abhaken, wenn sie gekauft sind
Damit: Wir wissen, was noch zu kaufen ist

Akzeptanzkriterien:
✓ Checkbox neben jedem Item
✓ Abhaken markiert Item als "gekauft"
✓ Abgehakte Items grau darstellen
✓ Option: Abgehakte Items verstecken
```

#### US-4.3: Items bearbeiten / löschen
```
Als: Gruppenmitglied
Ich möchte: Meine Items bearbeiten oder löschen
Damit: Fehler korrigiert werden

Akzeptanzkriterien:
✓ Edit-Button pro Item (nur Ersteller oder Admin darf)
✓ Delete-Button (Bestätigung erforderlich)
✓ Änderungen in Echtzeit für alle sichtbar
```

---

### Feature 5: Ausgabenverteilung (Kritisch!)

#### US-5.1: Ausgabe erfassen
```
Als: Gruppenmitglied (z.B. der Einkäufer)
Ich möchte: Erfassen, wieviel ich ausgegeben habe
Damit: Die Kosten fair verteilt werden

Akzeptanzkriterien:
✓ "Ausgabe hinzufügen" Button
✓ Felder: Betrag, Beschreibung, Zahldatum, Kategorie
✓ Wer hat gezahlt (Dropdown, default = aktueller Nutzer)
✓ Ausgabe wird gespeichert mit Timestamp
```

#### US-5.2: Ausgabe auf Gruppe aufteilen
```
Als: Nutzer nach Ausgabe-Erfassung
Ich möchte: Diese Ausgabe auf alle Mitglieder aufteilen
Damit: Jeder seinen Anteil kennt

Aufteilungs-Methoden:
✓ Gleichmäßig teilen (auf X Personen aufteilen)
✓ Custom-Teilen (pro Person unterschiedlich)

Akzeptanzkriterien:
✓ "Auf Gruppe teilen" Dialog
✓ Checkbox für jede Person (wer beteiligt?)
✓ Automatische Berechnung (Gesamtbetrag ÷ Personen)
✓ Jede Person sieht ihren Anteil
```

#### US-5.3: Ausgabenübersicht
```
Als: Gruppenmitglied
Ich möchte: Sehen wer wem wieviel schuldet
Damit: Ich weiß wer bezahlen muss

Anzeige:
✓ Tabelle: "Ausgaben-Übersicht"
✓ Spalten: Item, Betrag, Zahler, Aufteilung, Status
✓ Filter: Nach Zeitraum, Nach Person
✓ Summe: Mein aktueller Saldo (positiv = mir wird Geld geschuldet)

Akzeptanzkriterien:
✓ Übersicht lädt sofort
✓ Aktualisiert in Echtzeit (WebSocket)
```

---

### Feature 6: Chat (Gruppenchat)

#### US-6.1: Nachricht schreiben
```
Als: Gruppenmitglied
Ich möchte: Eine Nachricht im Gruppenchat schreiben
Damit: Ich mit anderen koordinieren kann

Akzeptanzkriterien:
✓ Chat-Input am unteren Rand
✓ Nachricht mit Enter senden oder Button
✓ Nachricht zeigt: Absender, Zeit, Text
✓ Nachricht wird für alle in Echtzeit sichtbar
```

#### US-6.2: Chat-Verlauf
```
Als: Nutzer
Ich möchte: Alte Nachrichten sehen
Damit: Ich Konversationen nachvollziehen kann

Akzeptanzkriterien:
✓ Chat lädt die letzten 50 Nachrichten beim Öffnen
✓ Scrollen zeigt ältere Nachrichten
✓ Neue Nachrichten scrolle nach unten
✓ Nachrichten-Zeit anzeigen
```

---

### Feature 7: Budget (Nice-to-Have, aber im MVP)

#### US-7.1: Budget setzen
```
Als: Gruppen-Admin
Ich möchte: Ein Budget für diese Gruppe setzen
Damit: Wir kontrolliert ausgeben

Akzeptanzkriterien:
✓ "Budget setzen" im Gruppen-Settings
✓ Betrag eingeben (z.B. 200€ pro Monat)
✓ Zeitraum: Monatlich / Wöchentlich / Gesamt
✓ Budget wird gespeichert
```

#### US-7.2: Budget-Warnung
```
Als: Gruppenmitglied
Ich möchte: Sehen, ob wir das Budget überschritten haben
Damit: Ich sparsam bin

Akzeptanzkriterien:
✓ Progress-Bar zeigt: Aktuelle Ausgaben vs. Budget
✓ Warnung ab 80% des Budgets
✓ Rote Markierung bei Überschreitung
```

---

## 🔄 Echtzeit-Anforderungen (WebSocket)

### Synchronisations-Szenarien

| Szenario | Trigger | Aktion |
|----------|---------|--------|
| Item hinzufügen | Ein Nutzer klickt "Add" | Alle anderen sehen es sofort |
| Item abhaken | Ein Nutzer klickt Checkbox | Andere sehen den geänderten Status |
| Ausgabe teilen | Ausgabe wird auf Gruppe verteilt | Alle sehen updated Salamdo |
| Nachricht schreiben | Chat-Nachricht send | Alle sind Chat sehen es live |
| Mitglied beitritt | Neue Person tritt Gruppe bei | Alle sehen die Person |

**Priorität:** Diese Szenarien sind Kern der App!

---

## 🛡️ Sicherheitsanforderungen

- [ ] Passwort-Hashing (SHA-256 oder besser)
- [ ] SQL-Injection-Prävention (PreparedStatements)
- [ ] XSS-Prävention (Input-Sanitization)
- [ ] CSRF-Token für POST/PUT/DELETE
- [ ] Session-Timeout nach 30 Tagen
- [ ] Nur Wer authentifiziert ist, darf API aufrufen
- [ ] Nutzer können nur ihre eigenen Daten ändern
- [ ] Gruppen-Daten sind privat (nur Mitglieder sehen)

---

## 📱 UI/UX Anforderungen

- [ ] Responsive Design (Desktop + Tablet)
- [ ] Navigation ist intuitiv
- [ ] Fehler-Messages sind hilfreiche
- [ ] Bestätigungen für kritische Aktionen (Delete)
- [ ] Loading-States während API-Calls
- [ ] Dark Mode (Optional für MVP+)

---

## ⚡ Performance-Anforderungen

- [ ] API-Response < 500ms
- [ ] Chat-Nachricht < 100ms (live)
- [ ] Gleichzeitig: min. 10 Nutzer pro Gruppe
- [ ] Datenbank-Queries optimiert

---

## 🧪 Testing-Anforderungen

- [ ] Unit-Tests für Java-Services (min. 70% Coverage)
- [ ] Integration-Tests (Frontend ↔ Backend)
- [ ] Manual-Testing (User-Scenarios)

---

## Nicht im MVP

- ❌ Abrechnung (Scan/KI)
- ❌ Maps/Supermarkt-Vorschläge
- ❌ Offline-Funktionalität
- ❌ Mobile-App (Native)
- ❌ Multi-Language Support
- ❌ Dark Mode
- ❌ Passwort-Reset
- ❌ Two-Factor Authentication

Diese Features werden in **Phase 2** evaluiert.

---

**Nächster Schritt:** Architektur-Spezifikation (03-ARCHITEKTUR.md)
