# 🗄️ Schritt 5: Datenbank-Schema implementieren

**Ziel:** SQL-Schema aus 04-DATENBANKSCHEMA.md umsetzen, Test-Daten laden, Queries testen
**Dauer:** 1.5 - 2h
**Wer:** Person 5 (Database-Lead) führt aus, Person 6 prüft, andere lernen mit
**Schwierigkeit:** ⭐⭐ (Mittel)

---

## 🎯 Was macht ihr heute?

Am Ende habt ihr:
- ✅ SQL-Schema ist in der Datenbank
- ✅ Test-Daten sind geladen
- ✅ Queries funktionieren
- ✅ Alle verstehen die Tabellen-Struktur

---

## 📋 Voraussetzungen

- ✅ PostgreSQL läuft
- ✅ Benutzer `developer` kann sich anmelden
- ✅ Datenbank `shopping_list` existiert
- ✅ Datei `04-DATENBANKSCHEMA.md` gelesen

---

## 👥 Team-Setup

| Person | Rolle | Aufgabe |
|--------|-------|---------|
| 5 | Lead | SQL-Dateien erstellen, Queries ausführen |
| 6 | Validator | Test-Queries ausführen, Ergebnisse checken |
| Alle andere | Learning | Zusehen, Fragen stellen |

---

## 🚀 Schritt für Schritt

### **Schritt 1: SQL-Datei erstellen (15 min)**

**Datei:** `db/schema.sql`

Diese Datei enthält alle CREATE TABLE Statements:

```bash
# SQL-Datei erstellen
cat > db/schema.sql << 'EOF'
-- ==========================================
-- GETEILTE EINKAUFSLISTE - DATABASE SCHEMA
-- ==========================================

-- Tabelle 1: USERS
CREATE TABLE IF NOT EXISTS users (
    id SERIAL PRIMARY KEY,
    email VARCHAR(255) NOT NULL UNIQUE,
    password_hash VARCHAR(255) NOT NULL,
    first_name VARCHAR(100) NOT NULL,
    last_name VARCHAR(100) NOT NULL,
    profile_picture_url VARCHAR(500),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
CREATE INDEX IF NOT EXISTS idx_users_email ON users(email);

-- Tabelle 2: GROUPS
CREATE TABLE IF NOT EXISTS groups (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    description TEXT,
    created_by INTEGER NOT NULL REFERENCES users(id) ON DELETE CASCADE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
CREATE INDEX IF NOT EXISTS idx_groups_created_by ON groups(created_by);

-- Tabelle 3: GROUP_MEMBERS
CREATE TABLE IF NOT EXISTS group_members (
    id SERIAL PRIMARY KEY,
    group_id INTEGER NOT NULL REFERENCES groups(id) ON DELETE CASCADE,
    user_id INTEGER NOT NULL REFERENCES users(id) ON DELETE CASCADE,
    role VARCHAR(20) NOT NULL DEFAULT 'member' CHECK (role IN ('admin', 'member')),
    joined_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    UNIQUE(group_id, user_id)
);
CREATE INDEX IF NOT EXISTS idx_group_members_group_id ON group_members(group_id);
CREATE INDEX IF NOT EXISTS idx_group_members_user_id ON group_members(user_id);

-- Tabelle 4: SHOPPING_ITEMS
CREATE TABLE IF NOT EXISTS shopping_items (
    id SERIAL PRIMARY KEY,
    group_id INTEGER NOT NULL REFERENCES groups(id) ON DELETE CASCADE,
    name VARCHAR(200) NOT NULL,
    quantity INTEGER DEFAULT 1 CHECK (quantity > 0),
    category VARCHAR(50) DEFAULT 'Sonstiges',
    completed BOOLEAN DEFAULT FALSE,
    added_by INTEGER NOT NULL REFERENCES users(id) ON DELETE SET NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
CREATE INDEX IF NOT EXISTS idx_shopping_items_group_id ON shopping_items(group_id);
CREATE INDEX IF NOT EXISTS idx_shopping_items_completed ON shopping_items(group_id, completed);

-- Tabelle 5: EXPENSES
CREATE TABLE IF NOT EXISTS expenses (
    id SERIAL PRIMARY KEY,
    group_id INTEGER NOT NULL REFERENCES groups(id) ON DELETE CASCADE,
    amount DECIMAL(10, 2) NOT NULL,
    description VARCHAR(255),
    paid_by INTEGER NOT NULL REFERENCES users(id) ON DELETE SET NULL,
    paid_at DATE NOT NULL,
    category VARCHAR(50) DEFAULT 'Sonstiges',
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
CREATE INDEX IF NOT EXISTS idx_expenses_group_id ON expenses(group_id);
CREATE INDEX IF NOT EXISTS idx_expenses_paid_by ON expenses(paid_by);
CREATE INDEX IF NOT EXISTS idx_expenses_paid_at ON expenses(paid_at);

-- Tabelle 6: EXPENSE_SPLITS
CREATE TABLE IF NOT EXISTS expense_splits (
    id SERIAL PRIMARY KEY,
    expense_id INTEGER NOT NULL REFERENCES expenses(id) ON DELETE CASCADE,
    user_id INTEGER NOT NULL REFERENCES users(id) ON DELETE CASCADE,
    amount DECIMAL(10, 2) NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    UNIQUE(expense_id, user_id)
);
CREATE INDEX IF NOT EXISTS idx_expense_splits_expense_id ON expense_splits(expense_id);
CREATE INDEX IF NOT EXISTS idx_expense_splits_user_id ON expense_splits(user_id);

-- Tabelle 7: CHAT_MESSAGES
CREATE TABLE IF NOT EXISTS chat_messages (
    id SERIAL PRIMARY KEY,
    group_id INTEGER NOT NULL REFERENCES groups(id) ON DELETE CASCADE,
    sender_id INTEGER NOT NULL REFERENCES users(id) ON DELETE SET NULL,
    message_text TEXT NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
CREATE INDEX IF NOT EXISTS idx_chat_messages_group_id_created_at
    ON chat_messages(group_id, created_at DESC);

-- Tabelle 8: BUDGETS
CREATE TABLE IF NOT EXISTS budgets (
    id SERIAL PRIMARY KEY,
    group_id INTEGER NOT NULL UNIQUE REFERENCES groups(id) ON DELETE CASCADE,
    amount DECIMAL(10, 2) NOT NULL,
    period VARCHAR(20) NOT NULL DEFAULT 'monthly'
        CHECK (period IN ('weekly', 'monthly', 'total')),
    set_by INTEGER NOT NULL REFERENCES users(id) ON DELETE SET NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
CREATE INDEX IF NOT EXISTS idx_budgets_group_id ON budgets(group_id);

-- Tabelle 9: SESSIONS
CREATE TABLE IF NOT EXISTS sessions (
    id SERIAL PRIMARY KEY,
    user_id INTEGER NOT NULL REFERENCES users(id) ON DELETE CASCADE,
    token VARCHAR(500) NOT NULL UNIQUE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    expires_at TIMESTAMP NOT NULL
);
CREATE INDEX IF NOT EXISTS idx_sessions_token ON sessions(token);
CREATE INDEX IF NOT EXISTS idx_sessions_user_id ON sessions(user_id);
CREATE INDEX IF NOT EXISTS idx_sessions_expires_at ON sessions(expires_at);

-- ==========================================
-- SCHEMA ERSTELLT!
-- ==========================================
EOF
```

**Vergeichert dass Datei existiert:**

```bash
cat db/schema.sql | head -20
# Sollte CREATE TABLE zeigen
```

---

### **Schritt 2: Schema in die Datenbank laden (10 min)**

**PostgreSQL-Terminal:**

```bash
# Mit developer-Benutzer in shopping_list Datenbank verbinden
psql -h localhost -U developer -d shopping_list

# Jetzt im psql-Terminal:
\i db/schema.sql

# Oder (wenn von Projekt-Root):
\i ../db/schema.sql
```

**Alternative (von Bash aus):**

```bash
# Direkt von Terminal
psql -h localhost -U developer -d shopping_list -f db/schema.sql

# Output sollte zeigen:
# CREATE TABLE
# CREATE INDEX
# ... (9 Tabellen total)
```

**Checken ob erfolgreich:**

```bash
psql -h localhost -U developer -d shopping_list

# Im psql-Terminal:
\dt
# Sollte alle 9 Tabellen zeigen:
# - budgets
# - chat_messages
# - expense_splits
# - expenses
# - group_members
# - groups
# - shopping_items
# - sessions
# - users

# Details einer Tabelle:
\d users
# Sollte alle Spalten zeigen mit Types
```

---

### **Schritt 3: Test-Daten laden (20 min)**

**Datei:** `db/seed-data.sql`

```bash
cat > db/seed-data.sql << 'EOF'
-- ==========================================
-- TEST-DATEN FÜR ENTWICKLUNG
-- ==========================================

-- 1. Benutzer (3 Test-User)
INSERT INTO users (email, password_hash, first_name, last_name)
VALUES
    ('tina@example.com', 'hash_tina_12345', 'Tina', 'Müller'),
    ('bob@example.com', 'hash_bob_12345', 'Bob', 'Schmidt'),
    ('alice@example.com', 'hash_alice_12345', 'Alice', 'Weber');

-- 2. Gruppe (Wochenend-Einkauf)
INSERT INTO groups (name, description, created_by)
VALUES ('Wochenend-Einkauf', 'WG Einkaufen für die Woche', 1);

-- 3. Gruppenmitglieder
INSERT INTO group_members (group_id, user_id, role)
VALUES
    (1, 1, 'admin'),
    (1, 2, 'member'),
    (1, 3, 'member');

-- 4. Shopping Items
INSERT INTO shopping_items (group_id, name, quantity, category, added_by, completed)
VALUES
    (1, 'Milch', 2, 'Lebensmittel', 1, false),
    (1, 'Brot', 1, 'Lebensmittel', 2, false),
    (1, 'Spülmittel', 1, 'Haushalt', 3, false),
    (1, 'Käse', 1, 'Lebensmittel', 1, true);

-- 5. Ausgaben
INSERT INTO expenses (group_id, amount, description, paid_by, paid_at, category)
VALUES
    (1, 45.50, 'Einkauf im Supermarkt', 1, CURRENT_DATE, 'Lebensmittel');

-- 6. Ausgabe-Splits (gerecht teilen)
INSERT INTO expense_splits (expense_id, user_id, amount)
VALUES
    (1, 1, 15.17),
    (1, 2, 15.17),
    (1, 3, 15.16);

-- 7. Nachrichten
INSERT INTO chat_messages (group_id, sender_id, message_text)
VALUES
    (1, 1, 'Wer kommt noch mit zum Einkaufen?'),
    (1, 2, 'Ich komme mit!'),
    (1, 3, 'Ich auch, bringt mir bitte Milch mit');

-- 8. Budget
INSERT INTO budgets (group_id, amount, period, set_by)
VALUES
    (1, 100.00, 'weekly', 1);

-- ==========================================
-- TEST-DATEN GELADEN!
-- ==========================================
EOF
```

**Laden:**

```bash
psql -h localhost -U developer -d shopping_list -f db/seed-data.sql

# Output:
# INSERT 0 3 (3 users)
# INSERT 0 1 (1 group)
# INSERT 0 3 (3 members)
# INSERT 0 4 (4 items)
# etc.
```

---

### **Schritt 4: Test-Queries ausführen (30 min)**

**Alle diese Queries sollten funktionieren:**

```bash
psql -h localhost -U developer -d shopping_list
```

**Im psql-Terminal:**

```sql
-- QUERY 1: Alle Benutzer
SELECT * FROM users;
-- Sollte 3 Rows zeigen (Tina, Bob, Alice)

-- QUERY 2: Group mit Members
SELECT g.name, gm.role, u.first_name
FROM groups g
JOIN group_members gm ON g.id = gm.group_id
JOIN users u ON gm.user_id = u.id;
-- Output:
-- name                 | role   | first_name
-- Wochenend-Einkauf    | admin  | Tina
-- Wochenend-Einkauf    | member | Bob
-- Wochenend-Einkauf    | member | Alice

-- QUERY 3: Shopping Items (nur unfertig)
SELECT name, quantity, category, completed
FROM shopping_items
WHERE group_id = 1 AND completed = false;
-- Sollte 3 Items zeigen (Milch, Brot, Spülmittel)

-- QUERY 4: User Balance (wer schuldet wem?)
SELECT
    gm.user_id,
    u.first_name,
    SUM(es.amount) as owes,
    (SELECT SUM(amount) FROM expenses WHERE paid_by = gm.user_id AND group_id = 1) as paid
FROM group_members gm
JOIN users u ON gm.user_id = u.id
LEFT JOIN expense_splits es ON es.user_id = gm.user_id
LEFT JOIN expenses e ON e.id = es.expense_id AND e.group_id = 1
WHERE gm.group_id = 1
GROUP BY gm.user_id, u.first_name;
-- Sollte zeigen wer wieviel schuldet

-- QUERY 5: Chat-Nachrichten
SELECT u.first_name, cm.message_text, cm.created_at
FROM chat_messages cm
JOIN users u ON cm.sender_id = u.id
WHERE cm.group_id = 1
ORDER BY cm.created_at DESC;
-- Sollte 3 Nachrichten zeigen
```

---

## ✅ Checkliste - Datenbank fertig?

- [ ] `db/schema.sql` existiert
- [ ] `db/seed-data.sql` existiert
- [ ] Alle 9 Tabellen sind erstellt (siehe `\dt`)
- [ ] Test-Daten sind geladen (3 Users, 1 Group, etc.)
- [ ] QUERY 1-5 funktionieren (alle select funktioniert)
- [ ] Keine Fehler beim Laden

---

## 🎓 Was ihr gelernt habt

1. **SQL DDL:** CREATE TABLE, Constraints, Indizes
2. **SQL DML:** INSERT Daten laden
3. **SQL Queries:** SELECT mit JOINs
4. **ER-Diagramme:** Tabellen-Beziehungen verstehen
5. **Normalisierung:** Warum wir Tabellen so trennen

---

## ❓ Häufige Probleme

### **Problem 1: "ERROR: Syntax error"**

```bash
# SQL-Fehler - Check SQL Datei auf Typos
# Häufig: Fehlende Kommas, Semikolon

# Lese Fehler-Message genau
# Beispiel: "column "gruppem_id" does not exist"
# → Tippfehler: "group_id" statt "gruppem_id"
```

### **Problem 2: "ERROR: Constraint violation"**

```bash
# Foreign Key nicht erfüllt
# Beispiel: group_id 5 existiert nicht

# Checke ob Daten in richtigem Umfang existieren
SELECT * FROM groups; -- Wieviele Groups gibt es?
```

### **Problem 3: Tests funktionieren, aber Queries produzieren Fehler**

```bash
# Überprüfe die Query-Syntax
# Beispiel: JOIN statt LEFT JOIN ausgenutzt → NULL Werte

# Debugge Step-by-Step
SELECT COUNT(*) FROM users;           -- 3?
SELECT COUNT(*) FROM expense_splits;  -- 3?
-- Dann komplexere queries
```

---

## 🔗 Kommende Schritte

- [ ] Backend: Java Service Layer verbindet mit dieser DB (Woche 2)
- [ ] API: REST Endpoints abfragen diese DB
- [ ] Frontend: Zeigt diese Daten Nutzern

---

## 📞 Für Frontend/Backend-Team

Die Datenbank ist **ready to use**!

**Backend-Team:**
- Connection-String: `jdbc:postgresql://localhost:5432/shopping_list`
- User: `developer`
- Password: `dev_password`
- Die Tabellen sind dokumentiert in `docs/04-DATENBANKSCHEMA.md`

**Frontend-Team:**
- Das Backend wird die Daten liefern, ihr zeigt sie an
- API-Endpoints kommen in Woche 2

---

**✅ Datenbank läuft? Perfekt!**

Die Woche 1 ist damit zu 90% fertig! 🎉

→ Freitag: Alles zusammen testen + Wochenabschluss
