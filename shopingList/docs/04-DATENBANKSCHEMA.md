# 🗄️ Datenbank-Schema - Geteilte Einkaufsliste

**Version:** 1.0
**Status:** Draft
**DBMS:** PostgreSQL 14+
**Zuletzt aktualisiert:** 2026-03-21

---

## Datenbank-Diagramm (ER)

```
┌─────────────────┐
│     USERS       │
├─────────────────┤
│ id (PK)         │
│ email (U)       │  ◄────┐
│ password_hash   │       │
│ first_name      │       │
│ last_name       │       │
│ profile_pic_url │       │
│ created_at      │       │
│ updated_at      │       │
└─────────────────┘       │
         │                │
         │ 1:N            │ N:1
         │                │
    ┌────┴────────────────┴────────────┐
    │                                   │
┌───▼─────────────┐           ┌─────────┴──────┐
│ GROUP_MEMBERS   │           │      GROUPS    │
├─────────────────┤           ├────────────────┤
│ id (PK)         │           │ id (PK)        │
│ group_id (FK)   │──────┐    │ name           │
│ user_id (FK)    │──────┼──► │ description    │
│ role            │      │    │ created_by(FK) │
│ joined_at       │      │    │ created_at     │
│ U(group_id,    │      │    │ updated_at     │
│   user_id)      │      │    └────────────────┘
└─────────────────┘      │         │
                         │         │ 1:N
                         │         │
                    ┌────┴─────────┬──────┐
                    │              │      │
            ┌───────▼──────┐   ┌───▼──────────────┐
            │SHOPPING_ITEMS│   │    EXPENSES      │
            ├──────────────┤   ├──────────────────┤
            │ id (PK)      │   │ id (PK)          │
            │ group_id(FK) │   │ group_id (FK)    │
            │ name         │   │ amount           │
            │ quantity     │   │ description      │
            │ category     │   │ paid_by (FK)     │
            │ completed    │   │ paid_at          │
            │ added_by(FK) │   │ category         │
            │ created_at   │   │ created_at       │
            │ updated_at   │   │ updated_at       │
            └──────────────┘   └───────┬──────────┘
                                       │
                                       │ 1:N
                                       │
                              ┌────────▼──────┐
                              │EXPENSE_SPLITS │
                              ├───────────────┤
                              │ id (PK)       │
                              │ expense_id    │
                              │ user_id (FK)  │
                              │ amount        │
                              │ created_at    │
                              │U(expense_id,  │
                              │  user_id)     │
                              └───────────────┘

            ┌──────────────────┐
            │  CHAT_MESSAGES   │
            ├──────────────────┤
            │ id (PK)          │
            │ group_id (FK)    │
            │ sender_id (FK)   │
            │ message_text     │
            │ created_at       │
            │ I(group_id,      │
            │   created_at)    │
            └──────────────────┘

            ┌──────────────────┐
            │     BUDGETS      │
            ├──────────────────┤
            │ id (PK)          │
            │ group_id (FK) [U]│
            │ amount           │
            │ period           │
            │ set_by (FK)      │
            │ created_at       │
            │ updated_at       │
            └──────────────────┘

            ┌──────────────────┐
            │    SESSIONS      │
            ├──────────────────┤
            │ id (PK)          │
            │ user_id (FK)     │
            │ token [U]        │
            │ created_at       │
            │ expires_at       │
            └──────────────────┘

Legende:
(PK) = Primary Key
(FK) = Foreign Key
(U) = Unique Constraint
(I) = Index
→ = Foreign Key Relationship
```

---

## SQL DDL (Data Definition Language)

### 1. USERS Tabelle

```sql
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    email VARCHAR(255) NOT NULL UNIQUE,
    password_hash VARCHAR(255) NOT NULL,
    first_name VARCHAR(100) NOT NULL,
    last_name VARCHAR(100) NOT NULL,
    profile_picture_url VARCHAR(500),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE INDEX idx_users_email ON users(email);
```

**Zweck:** Speichert alle Benutzer der Anwendung
**Constraints:**
- Email muss eindeutig sein (Login-Kriterium)
- Passwort wird gehasht gespeichert

---

### 2. GROUPS Tabelle

```sql
CREATE TABLE groups (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    description TEXT,
    created_by INTEGER NOT NULL REFERENCES users(id) ON DELETE CASCADE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE INDEX idx_groups_created_by ON groups(created_by);
```

**Zweck:** Einkaufsgruppen (Familie, Freunde, WG)
**Constraints:**
- created_by muss existierender Nutzer sein
- Wenn Nutzer gelöscht → Gruppe auch gelöscht

---

### 3. GROUP_MEMBERS Tabelle

```sql
CREATE TABLE group_members (
    id SERIAL PRIMARY KEY,
    group_id INTEGER NOT NULL REFERENCES groups(id) ON DELETE CASCADE,
    user_id INTEGER NOT NULL REFERENCES users(id) ON DELETE CASCADE,
    role VARCHAR(20) NOT NULL DEFAULT 'member' CHECK (role IN ('admin', 'member')),
    joined_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    UNIQUE(group_id, user_id)
);

CREATE INDEX idx_group_members_group_id ON group_members(group_id);
CREATE INDEX idx_group_members_user_id ON group_members(user_id);
```

**Zweck:** Verknüpfung zwischen Users und Groups (N:M Beziehung)
**Constraints:**
- Jede Kombination (group_id, user_id) kann nur 1x existieren
- Roles: 'admin' oder 'member'

---

### 4. SHOPPING_ITEMS Tabelle

```sql
CREATE TABLE shopping_items (
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

CREATE INDEX idx_shopping_items_group_id ON shopping_items(group_id);
CREATE INDEX idx_shopping_items_completed ON shopping_items(group_id, completed);
```

**Zweck:** Items in der Einkaufsliste
**Constraints:**
- quantity muss > 0 sein
- completed = Boolean (gekauft oder nicht)
- indexed nach group_id für schnelle Abfragen

---

### 5. EXPENSES Tabelle

```sql
CREATE TABLE expenses (
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

CREATE INDEX idx_expenses_group_id ON expenses(group_id);
CREATE INDEX idx_expenses_paid_by ON expenses(paid_by);
CREATE INDEX idx_expenses_paid_at ON expenses(paid_at);
```

**Zweck:** Ausgaben-Tracking (wer hat wieviel bezahlt?)
**Constraints:**
- amount ist DECIMAL für finanzielle Genauigkeit
- paid_at ist Date (nicht Timestamp)
- indexed nach group_id für Abfragen pro Gruppe

---

### 6. EXPENSE_SPLITS Tabelle

```sql
CREATE TABLE expense_splits (
    id SERIAL PRIMARY KEY,
    expense_id INTEGER NOT NULL REFERENCES expenses(id) ON DELETE CASCADE,
    user_id INTEGER NOT NULL REFERENCES users(id) ON DELETE CASCADE,
    amount DECIMAL(10, 2) NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    UNIQUE(expense_id, user_id)
);

CREATE INDEX idx_expense_splits_expense_id ON expense_splits(expense_id);
CREATE INDEX idx_expense_splits_user_id ON expense_splits(user_id);
```

**Zweck:** Aufschlüsseln einer Ausgabe auf einzelne Personen
**Beispiel:**
```
Ausgabe: Pizza für 40€ von Tina
Splits:
  - Tina: 20€ (sie hat 40€ bezahlt, schuldet aber nur 20€)
  - Bob: 20€ (schuldet 20€)
  → Tina bekommt 20€ zurück von Bob
```

---

### 7. CHAT_MESSAGES Tabelle

```sql
CREATE TABLE chat_messages (
    id SERIAL PRIMARY KEY,
    group_id INTEGER NOT NULL REFERENCES groups(id) ON DELETE CASCADE,
    sender_id INTEGER NOT NULL REFERENCES users(id) ON DELETE SET NULL,
    message_text TEXT NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE INDEX idx_chat_messages_group_id_created_at
    ON chat_messages(group_id, created_at DESC);
```

**Zweck:** Gruppenchat für Koordination
**Constraints:**
- Composite-Index für effiziente Pagination

---

### 8. BUDGETS Tabelle

```sql
CREATE TABLE budgets (
    id SERIAL PRIMARY KEY,
    group_id INTEGER NOT NULL UNIQUE REFERENCES groups(id) ON DELETE CASCADE,
    amount DECIMAL(10, 2) NOT NULL,
    period VARCHAR(20) NOT NULL DEFAULT 'monthly'
        CHECK (period IN ('weekly', 'monthly', 'total')),
    set_by INTEGER NOT NULL REFERENCES users(id) ON DELETE SET NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE INDEX idx_budgets_group_id ON budgets(group_id);
```

**Zweck:** Budgets pro Gruppe
**Constraints:**
- Pro Gruppe nur 1 Budget (UNIQUE)
- period kann weekly/monthly/total sein

---

### 9. SESSIONS Tabelle

```sql
CREATE TABLE sessions (
    id SERIAL PRIMARY KEY,
    user_id INTEGER NOT NULL REFERENCES users(id) ON DELETE CASCADE,
    token VARCHAR(500) NOT NULL UNIQUE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    expires_at TIMESTAMP NOT NULL
);

CREATE INDEX idx_sessions_token ON sessions(token);
CREATE INDEX idx_sessions_user_id ON sessions(user_id);
CREATE INDEX idx_sessions_expires_at ON sessions(expires_at);
```

**Zweck:** Session-Management für Authentifizierung
**Constraints:**
- Tokens sind eindeutig
- Abgelaufene Sessions können gelöscht werden (via CRON)

---

## Datenbank-Constraints Überblick

| Constraint | Typ | Grund |
|------------|-----|-------|
| users.email UNIQUE | Domain | Email muss eindeutig sein |
| group_members (group_id, user_id) UNIQUE | Domain | User kann nur 1x pro Gruppe Mitglied sein |
| shopping_items.quantity > 0 | Check | Quantity muss positiv sein |
| expenses.amount > 0 (optional) | Check | Ausgaben müssen positiv sein |
| budgets.group_id UNIQUE | Domain | Pro Gruppe max. 1 Budget |
| Alle FKs cascade on delete | Referential | Konsistenz bei Löschung |

---

## Normalisierung

Die Datenbank ist in **3. Normalisierungsform (3NF)**:

- ✅ 1NF: Atomare Werte (keine Arrays/Objekte in Spalten)
- ✅ 2NF: Keine partiellen Abhängigkeiten
- ✅ 3NF: Keine transitiven Abhängigkeiten

**Beispiel:**
- `expense_splits` verhindert Denormalisierung (würde alle Splits in einer Spalte speichern)
- Separate `group_members` Tabelle für N:M Beziehung

---

## Beispiel-Daten (Test-Inserts)

```sql
-- Benutzer
INSERT INTO users (email, password_hash, first_name, last_name)
VALUES
  ('tina@example.com', 'hash_tina', 'Tina', 'Müller'),
  ('bob@example.com', 'hash_bob', 'Bob', 'Schmidt'),
  ('alice@example.com', 'hash_alice', 'Alice', 'Weber');

-- Gruppe
INSERT INTO groups (name, description, created_by)
VALUES ('Wochenend-Einkauf', 'WG Einkaufen für die Woche', 1);

-- Gruppenmitglieder
INSERT INTO group_members (group_id, user_id, role)
VALUES
  (1, 1, 'admin'),
  (1, 2, 'member'),
  (1, 3, 'member');

-- Einkaufsliste Items
INSERT INTO shopping_items (group_id, name, quantity, category, added_by)
VALUES
  (1, 'Milch', 2, 'Lebensmittel', 1),
  (1, 'Brot', 1, 'Lebensmittel', 2),
  (1, 'Spülmittel', 1, 'Haushalt', 3);

-- Ausgaben
INSERT INTO expenses (group_id, amount, description, paid_by, paid_at, category)
VALUES
  (1, 45.50, 'Einkauf im Supermarkt', 1, '2026-03-20', 'Lebensmittel');

-- Ausgabe-Splits (gerecht teilen)
INSERT INTO expense_splits (expense_id, user_id, amount)
VALUES
  (1, 1, 15.17),  -- Tina zahlt 1/3
  (1, 2, 15.17),  -- Bob schuldet 1/3
  (1, 3, 15.16);  -- Alice schuldet 1/3 (Rounding)

-- Nachrichten
INSERT INTO chat_messages (group_id, sender_id, message_text)
VALUES
  (1, 1, 'Wer kommt noch mit zum Einkaufen?');

-- Budget
INSERT INTO budgets (group_id, amount, period, set_by)
VALUES
  (1, 100.00, 'weekly', 1);
```

---

## Query-Beispiele (Häufig benutzt)

### Q1: Get User's Groups
```sql
SELECT g.*
FROM groups g
JOIN group_members gm ON g.id = gm.group_id
WHERE gm.user_id = $1 AND gm.role = 'member';
```

### Q2: Get Shopping Items for Group
```sql
SELECT *
FROM shopping_items
WHERE group_id = $1 AND completed = FALSE
ORDER BY created_at DESC;
```

### Q3: Calculate User Balance in Group
```sql
SELECT
  COALESCE(SUM(es.amount), 0) as owes_to_user,
  COALESCE(SUM(e.amount), 0) FILTER (WHERE e.paid_by = $1) as paid_by_user
FROM expense_splits es
LEFT JOIN expenses e ON es.expense_id = e.id
WHERE e.group_id = $2 AND es.user_id = $1;

-- Balance = paid_by_user - owes_to_user
```

### Q4: Get Group Members
```sql
SELECT u.*, gm.role
FROM users u
JOIN group_members gm ON u.id = gm.user_id
WHERE gm.group_id = $1
ORDER BY gm.joined_at;
```

### Q5: Get Chat Messages (Latest 50)
```sql
SELECT cm.*, u.first_name, u.last_name
FROM chat_messages cm
JOIN users u ON cm.sender_id = u.id
WHERE cm.group_id = $1
ORDER BY cm.created_at DESC
LIMIT 50;
```

---

## Indexierungs-Strategie

**Wichtige Indizes für Performance:**

| Tabelle | Spalte(n) | Typ | Grund |
|---------|-----------|-----|-------|
| users | email | UNIQUE | Login-Lookups |
| shopping_items | group_id, completed | COMPOSITE | Abfragen für aktive Items |
| expenses | group_id, paid_at | COMPOSITE | Expense-Reports |
| chat_messages | group_id, created_at DESC | COMPOSITE | Pagination |
| sessions | token | UNIQUE | Session-Lookups |
| group_members | user_id | SIMPLE | Gruppen pro User finden |

---

## Backup & Recovery

**Empfohlene Backup-Strategie:**
- Tägliches Full Backup (nachts)
- Transaction Logs für Point-in-Time Recovery
- Test-Recovery regelmäßig üben

**Skript für lokale Entwicklung:**
```bash
# Backup
pg_dump shopping_list > backup_$(date +%Y%m%d).sql

# Restore
psql shopping_list < backup_20260320.sql
```

---

## Migration Strategie

Alle Schema-Änderungen müssen:
1. In einer separaten `.sql` Datei sein
2. Mit Versionsnummer benannt: `V001_initial_schema.sql`, `V002_add_budgets.sql`
3. Idempotent sein (können mehrmals hintereinander ausgeführt werden)
4. Dokumentiert sein

**Beispiel Migration:**
```sql
-- V002_add_budgets.sql
-- Created 2026-03-15
-- Description: Add budget feature

BEGIN;
  CREATE TABLE budgets (
    -- ... columns ...
  );

  -- Add foreign key from groups to budgets via budget table
  ALTER TABLE group_members ADD INDEX ...

COMMIT;
```

---

**Nächste Schritte:**
1. SQL-Schema in PostgreSQL ausführen
2. Test-Daten einfügen
3. Queries testen
4. Java DAO-Layer implementieren (siehe 03-ARCHITEKTUR.md)

**Nächster Schritt:** API-Dokumentation (05-API-DOKUMENTATION.md)
