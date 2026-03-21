# Sonstige Anleitungen

## PostgreSQL Installation & Fernzugriff-Konfiguration

Diese Anleitung führt dich durch die grundlegende Einrichtung von PostgreSQL auf einem Ubuntu/Debian-Server und erklärt, wie du den Fernzugriff (Remote Access) sicher konfigurierst.

---

### 1. Installation

Installiere das PostgreSQL-Paket und den Client:

```bash
sudo apt update
sudo apt install postgresql postgresql-client
```

### 2. Administrator-Passwort setzen

Standardmäßig hat der Benutzer postgres kein Passwort für Datenbankverbindungen.

- Logge dich lokal in die Konsole ein:

```bash
sudo -u postgres psql
```

- Setze ein sicheres Passwort:

```sql
ALTER USER postgres WITH ENCRYPTED PASSWORD 'DEIN_SICHERES_PASSWORT';
```

- Verlasse die Konsole:

```sql
\q
```

### 3. Fernzugriff erlauben (Networking)

#### Schritt A: Netzwerk-Schnittstellen öffnen

PostgreSQL muss wissen, dass es auf Anfragen von außen hören soll.

- Datei öffnen:

```bash
sudo nano /etc/postgresql/$(psql -V | egrep -o '[0-9]{1,2}' | head -1)/main/postgresql.conf
```

- Änderung: Suche die Zeile `#listen_addresses = 'localhost'`
- Neu: `listen_addresses = '*'`

#### Schritt B: Zugriffsrechte festlegen (Whitelist)

Du musst festlegen, wer sich verbinden darf.

- Datei öffnen:

```bash
sudo nano /etc/postgresql/$(psql -V | egrep -o '[0-9]{1,2}' | head -1)/main/pg_hba.conf
```

- Eintrag am Ende hinzufügen:

```plaintext
# Erlaubt Zugriff für den User 'postgres' aus dem gesamten lokalen Netzwerk
hostssl  all  postgres  0.0.0.0/0  scram-sha-256
```

**Hinweis:** Ersetze `0.0.0.0/0` durch dein spezifisches Subnetz, z.B. `192.168.178.0/24`, für mehr Sicherheit.

#### Schritt C: Dienst neu starten

```bash
sudo systemctl restart postgresql
```

### 4. Firewall konfigurieren

PostgreSQL nutzt standardmäßig den Port 5432. Dieser muss in der Firewall geöffnet werden:

```bash
sudo ufw allow 5432/tcp
sudo ufw reload
```

### 5. Verbindung testen

Um herauszufinden, welche IP dein Server hat, nutze:

```bash
hostname -I
```

Führe von einem anderen Rechner im Netzwerk diesen Befehl aus (ersetze `192.168.x.x` durch die IP deines Servers):

```bash
psql --host 192.168.x.x --username postgres --password --dbname template1
```

---

---

# 🔀 GIT WORKFLOW ANLEITUNG

---

---

## Git Workflow: Branch erstellen, arbeiten, pushen und Pull Request

Diese Anleitung zeigt dir den kompletten Workflow für die Zusammenarbeit in Git: Wie du einen Branch erstellst, darin arbeitest, die Änderungen pushst und schließlich einen Pull Request erstellst.

---

### Schritt 1: Branch erstellen

Zunächst musst du sicherstellen, dass du auf dem `main`-Branch (oder der aktuellen Hauptbranch) bist und diesen aktualisiert hast:

```bash
git checkout main
git pull origin main
```

Erstelle einen neuen Branch mit einem aussagekräftigen Namen. Verwende Bindestriche und Kleinschreibung:

```bash
git checkout -b feature/meine-neue-funktion
```

Beispiele für gute Branch-Namen:
- `feature/user-authentifizierung`
- `fix/login-bug`
- `docs/update-readme`
- `refactor/api-endpoints`

### Schritt 2: Änderungen vornehmen und committen

Arbeite in deinem Branch und nehme die notwendigen Änderungen vor.

Überprüfe deinen aktuellen Status:

```bash
git status
```

Füge deine Änderungen zum Staging-Bereich hinzu:

```bash
git add .
```

Oder füge nur spezifische Dateien hinzu:

```bash
git add dateiname.txt
```

Erstelle einen aussagekräftigen Commit mit einer klaren Nachricht:

```bash
git commit -m "Beschreibung: Was wurde geändert und warum"
```

Beispiele für gute Commit-Nachrichten:
- `Feat: Benutzer-Registrierung hinzufügen`
- `Fix: Login-Button reagiert nicht mehr`
- `Docs: PostgreSQL-Anleitung aktualisieren`

Wenn du mehrere Commits machen möchtest, wiederhole die `add` und `commit` Schritte.

### Schritt 3: Branch pushen

Pushe deinen Branch zum Remote-Repository (z.B. GitHub):

```bash
git push origin feature/meine-neue-funktion
```

Git zeigt dir einen Link an, über den du direkt einen Pull Request erstellen kannst.

### Schritt 4: Pull Request erstellen

Du hast zwei Möglichkeiten:

#### Option A: Über die GitHub-Weboberfläche

1. Gehe auf die GitHub-Seite deines Repositories
2. Du solltest oben einen Banner mit deinem Branch-Namen und einem „Compare & pull request"-Button sehen
3. Klicke auf „Compare & pull request"
4. Überprüfe die Änderungen im „Changes"-Tab
5. Fülle das Formular aus:
   - **Title:** Kurze, aussagekräftige Beschreibung
   - **Description:** Detaillierte Erklärung, was du geändert hast und warum
6. Klicke auf „Create pull request"

#### Option B: Über die Kommandozeile (GitHub CLI)

Falls du GitHub CLI installiert hast (`gh`):

```bash
gh pr create --title "Meine neue Funktion" --body "Diese PR fügt folgendes hinzu: ..."
```

### Schritt 5: Review und Merge

Nach der Erstellung deines Pull Requests:

1. **Code Review:** Andere Entwickler werden deinen Code überprüfen und eventuell Kommentare hinterlassen
2. **Änderungen vornehmen:** Falls Feedback gegeben wird, nimm die Änderungen in deinem Branch vor:

```bash
git add .
git commit -m "Feedback umgesetzt: ..."
git push origin feature/meine-neue-funktion
```

Der Pull Request wird automatisch aktualisiert.

3. **Merge:** Wenn alles genehmigt ist, klicke auf den „Merge pull request"-Button auf GitHub oder nutze CLI:

```bash
gh pr merge feature/meine-neue-funktion
```

### Schritt 6: Aufräumen (lokal)

Nach dem Merge kannst du deinen lokalen Branch löschen:

```bash
git checkout main
git pull origin main
git branch -d feature/meine-neue-funktion
```

---

## Cheat Sheets

### PostgreSQL Befehle

| Befehl | Beschreibung |
|--------|-------------|
| `sudo systemctl status postgresql` | Prüfen, ob der Dienst läuft |
| `sudo -u postgres psql` | Lokaler Login ohne Passwort (als root) |
| `\l` | Alle Datenbanken auflisten (innerhalb psql) |
| `\du` | Alle Benutzer auflisten (innerhalb psql) |
| `\q` | psql-Konsole verlassen |

### Git Befehle

| Befehl | Beschreibung |
|--------|-------------|
| `git checkout -b branch-name` | Neuen Branch erstellen und wechseln |
| `git status` | Aktuellen Status anzeigen |
| `git add .` | Alle Änderungen hinzufügen |
| `git commit -m "Nachricht"` | Änderungen committen |
| `git push origin branch-name` | Branch zum Remote pushen |
| `git pull origin main` | Aktuelle Änderungen von main pullen |
| `git log` | Commit-Verlauf anzeigen |
| `git branch -d branch-name` | Branch lokal löschen |

---

**Erstellt am:** 21. März 2026
