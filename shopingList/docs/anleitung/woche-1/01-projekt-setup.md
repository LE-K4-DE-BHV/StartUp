# 📂 Schritt 1: Projekt-Setup & Ordner-Struktur

**Ziel:** Repository-Struktur aufbauen, Ordner erstellen, alles organisiert
**Dauer:** 45 min - 1h
**Wer:** Alle zusammen (Person 6 leitet)
**Schwierigkeit:** ⭐ (Einfach)

---

## 🎯 Was macht ihr heute?

Am Ende habt ihr:
- ✅ Git-Repo geklont
- ✅ Alle Ordner für Backend/Frontend/Database erstellt
- ✅ README.md & Gitignore konfiguriert
- ✅ Erste Branch erstellt
- ✅ Alle können im Team-Repo arbeiten

---

## 📋 Voraussetzungen

- Git installiert: `git --version`
- Zugang zu GitHub/GitLab (je nachdem wo das Repo ist)
- Terminal/PowerShell offen
- Text-Editor oder IDE vorbereitet

---

## 👥 Team-Setup

```
Bildschirm-Sharing: Person 6 zeigt die Schritte
Alle folgen auf ihrem Laptop mit
```

Macht regelmäßig Pausen zum Fragen stellen!

---

## 🚀 Schritt-für-Schritt

### **Schritt 1: Repository klonen**

**Zeit:** 5 min

#### Terminal-Befehle:

```bash
# Zu eurem Projekt-Ordner navigieren
cd /c/Users/kevin/Desktop/LTS_PJT/StartUp/shopingList

# Falls noch nicht dort - checken ob wir im richtigen Ordner sind
pwd

# Git status anschauen (sollte bereits ein Git-Repo sein)
git status
```

**Was solltet ihr sehen?**
```
On branch main
Your branch is up to date with 'origin/main'.
nothing to commit, working tree clean
```

**Problem?** "Not a git repository"
→ Dann: `git init` im shopingList Ordner

---

### **Schritt 2: Ordner-Struktur erstellen**

**Zeit:** 10 min

Das Projekt sollte so aussehen:

```
shopingList/
├── docs/                    ← Dokumentation (bereits da)
│   └── anleitung/          ← Diese Anleitungen
├── src/                     ← Source Code
│   ├── main/
│   │   └── java/
│   │       └── com/shoppinglist/  ← Java Packages
│   │           ├── server/
│   │           ├── controller/
│   │           ├── service/
│   │           ├── repository/
│   │           ├── model/
│   │           ├── security/
│   │           └── util/
│   └── test/
│       └── java/
│           └── com/shoppinglist/   ← Tests
├── public/                  ← Frontend (HTML/CSS/JS)
│   ├── pages/              ← HTML Dateien
│   ├── js/                 ← JavaScript
│   └── css/                ← Stylesheets
├── db/                      ← Datenbank-Skripte
│   ├── schema.sql          ← Tabellen-Definition
│   ├── seed-data.sql       ← Test-Daten
│   └── migrations/         ← Schema-Updates
├── config/                  ← Konfigurationsdateien
│   └── application.properties
├── .gitignore              ← Git-Ignore Datei
├── README.md               ← Projekt-Beschreibung (oben im Root)
└── pom.xml (später)        ← Maven Config (wenn ihr Maven nutzt)
```

#### Terminal-Befehle zum Erstellen:

```bash
# Frontend-Ordner
mkdir -p public/pages
mkdir -p public/js
mkdir -p public/css

# Backend-Ordner
mkdir -p src/main/java/com/shoppinglist/{server,controller,service,repository,model,security,util}
mkdir -p src/test/java/com/shoppinglist/{service,repository}

# Datenbank-Ordner
mkdir -p db/migrations

# Config-Ordner
mkdir -p config

# Überprüfen - sollte alles da sein
tree -L 3 .
# oder wenn tree nicht installiert:
find . -type d | head -20
```

**Was sollte passieren?**
- Ordner werden erstellt ✅
- Keine Fehler im Terminal ✅

---

### **Schritt 3: Wichtige Dateien erstellen**

**Zeit:** 10 min

#### **A) .gitignore - Was Git ignorieren soll**

```bash
# Neue Datei erstellen
cat > .gitignore << 'EOF'
# IDE
.idea/
.vscode/
*.swp
*.swo
*~
.DS_Store

# Java
*.class
*.jar
*.war
target/
out/
*.log

# Database
*.db
*.sqlite
local_db/
database_backup/

# Secrets & Environment
.env
.env.local
application-local.properties
secrets/

# Node/Frontend (wenn nötig)
node_modules/
dist/
build/

# OS
Thumbs.db
.DS_Store
EOF
```

**Checken:**
```bash
cat .gitignore
# Sollte alles oben Stehen sehen
```

#### **B) README aktualisieren (im Repo-Root)**

Diese Datei sollte schon dort sein (von letzter Sitzung), aber checkt:

```bash
cat README.md
# Sollte "Geteilte Einkaufsliste" enthalten
```

#### **C) config/application.properties (Platzhalter)**

```bash
cat > config/application.properties << 'EOF'
# Server Configuration
server.port=8080
server.host=localhost

# Database Configuration (wird später gefüllt)
db.url=jdbc:postgresql://localhost:5432/shopping_list
db.user=developer
db.password=dev_password

# Logging
log.level=INFO
EOF
```

**Was sollte passieren?**
- .gitignore Datei existiert ✅
- application.properties existiert ✅
- README zeigt Projekt-Info ✅

---

### **Schritt 4: Erste Dateien committen**

**Zeit:** 10 min

```bash
# Status anschauen
git status

# Alle neuen Dateien hinzufügen
git add .

# Commit-Nachricht
git commit -m "Setup: Projekt-Ordnung und Struktur"

# Zu GitHub pushen (falls remote schon konfiguriert)
git push origin main
```

**Was könnte schiefgehen?**

**Problem:** "fatal: 'origin' does not appear to be a repository"
```bash
# Remote hinzufügen
git remote add origin <deine-repo-url>
git push -u origin main
```

**Problem:** "Branche unterscheidet sich von remote"
```bash
# Pull zuerst, dann Push
git pull origin main
git push origin main
```

---

### **Schritt 5: Feature-Branches verstehen (Wichtig!)**

**Zeit:** 10 min

**In den nächsten Tagen macht ihr das:**

```bash
# Für jedes Feature einen neuen Branch erstellen
git checkout -b feature/postgresql-setup

# Arbeiten...

# Pushen
git push origin feature/postgresql-setup

# Pull Request auf GitHub erstellen (im Browser)

# Nach Review: Branch mergen
git checkout main
git pull origin main
git merge feature/postgresql-setup
git push origin main
```

**Regel für Woche 1:**
-❌ NICHT direkt auf `main` committen!
- ✅ IMMER einen Feature-Branch nutzen!
- ✅ IMMER vor dem Merge einen Code-Review machen!

---

## ✅ Checkliste - Fertig für heute?

- [ ] Repository geklont / Git läuft
- [ ] Alle Ordner existieren (`src/`, `public/`, `db/`, `docs/`, `anleitung/`)
- [ ] .gitignore erstellt
- [ ] application.properties existiert
- [ ] Erstes Commit gepusht
- [ ] Jeder kann `git status` ausführen ohne Fehler
- [ ] Jeder versteht Feature-Branches

---

## ❓ Häufige Probleme

### **Problem 1: "Permission denied" beim Git Push**

```bash
# Mögliche Lösungen:
# 1. SSH-Key generieren
ssh-keygen -t rsa -b 4096 -C "deine@email.com"

# 2. Oder HTTPS mit Personal Access Token nutzen
# Token auf GitHub generieren: Settings → Developer settings → Personal access tokens
git remote set-url origin https://<token>@github.com/username/repo.git
```

### **Problem 2: "fatal: Not a valid object name" beim Commit**

```bash
# Git konfigurieren
git config --global user.name "Dein Name"
git config --global user.email "deine@email.com"

# Dann nochmal committen
git add .
git commit -m "Setup: Projekt-Struktur"
```

### **Problem 3: Verstehe ich die Ordner-Struktur nicht?**

Schau hier nochmal nach:
- 💻 Backend-Code → `src/main/java/com/shoppinglist/`
- 🎨 Frontend-Code → `public/`
- 🗄️ Datenbank-Skripte → `db/`
- 📖 Dokumentation → `docs/`

---

## 🎓 Was ihr heute gelernt habt

1. **Git-Basics:** Clone, Status, Add, Commit, Push
2. **Feature Branches:** Arbeitsweise für Team-Projekte
3. **Ordner-Konventionen:** Wo was hingehört
4. **Code-Review Culture:** Vor dem Merge reviewen!

---

## 🔗 Weiterführende Ressourcen

- Git-Cheat-Sheet: https://github.com/joshnh/Git-Commands
- Git-Branching-Modell: https://git-flow.readthedocs.io/

---

## 📞 Fragen?

- "Ich verstehe Git nicht" → Frag die Gruppe, mach Pair-Programming
- "Mein Ordner sieht anders aus" → Checkt die Struktur oben nochmal
- "Git Push funktioniert nicht" → SSH/HTTPS konfigurieren (siehe Probleme oben)

---

**✅ Fertig? Gute Arbeit!**

→ Nächstes: [Schritt 2: Git-Workflow](./02-git-workflow.md) (Morgen)
