# 🏗️ Technische Architektur - Geteilte Einkaufsliste

**Version:** 1.0
**Status:** Draft
**Zuletzt aktualisiert:** 2026-03-21

---

## System Overview

```
┌─────────────────────────────────────────────────────────────────┐
│              🌐 FRONTEND (Browser / Client)                      │
│                   HTML / CSS / JavaScript                        │
│                                                                   │
│  ├─ Pages:                                                      │
│  │  ├─ login.html (Authentifizierung)                          │
│  │  ├─ register.html (Registrierung)                           │
│  │  ├─ dashboard.html (Gruppen, Listen-Übersicht)             │
│  │  ├─ shopping-list.html (Einkaufsliste Editor)              │
│  │  ├─ expenses.html (Ausgabenverteilung)                     │
│  │  ├─ profile.html (Benutzerprofil)                          │
│  │  └─ group-settings.html (Gruppen-Verwaltung)               │
│  │                                                              │
│  └─ JavaScript Modules:                                        │
│     ├─ api-client.js (REST + WebSocket Communication)         │
│     ├─ auth.js (Login/Logout Logic)                           │
│     ├─ utils.js (Helper Functions)                            │
│     └─ websocket-handler.js (Real-Time Updates)               │
└────────────────────┬────────────────────────────────────────────┘
                     │
          REST API (HTTP) + WebSocket
                     │
┌────────────────────▼────────────────────────────────────────────┐
│         🖥️ BACKEND (Server / Application Logic)                 │
│            Vanilla Java (No Frameworks)                         │
│                                                                   │
│  Architecture: Service-Oriented Architecture (SOA)             │
│                                                                   │
│  ├─ HTTP Server (Custom Java)                                  │
│  │  ├─ com.shoppinglist.server.HttpServer                     │
│  │  └─ Request Router & Handler                               │
│  │                                                              │
│  ├─ Controllers / Handlers:                                    │
│  │  ├─ AuthController                                         │
│  │  │  ├─ POST /api/register                                 │
│  │  │  ├─ POST /api/login                                    │
│  │  │  └─ POST /api/logout                                   │
│  │  ├─ UserController                                         │
│  │  │  ├─ GET /api/user/:id                                  │
│  │  │  ├─ PUT /api/user/:id                                  │
│  │  │  └─ GET /api/user/profile (Current User)              │
│  │  ├─ GroupController                                        │
│  │  │  ├─ POST /api/groups (Create)                          │
│  │  │  ├─ GET /api/groups (List User's Groups)               │
│  │  │  ├─ PUT /api/groups/:id                                │
│  │  │  ├─ DELETE /api/groups/:id                             │
│  │  │  ├─ POST /api/groups/:id/invite                        │
│  │  │  └─ DELETE /api/groups/:id/members/:userId             │
│  │  ├─ ShoppingListController                                 │
│  │  │  ├─ POST /api/groups/:id/items (Add Item)              │
│  │  │  ├─ GET /api/groups/:id/items (Get List)               │
│  │  │  ├─ PUT /api/items/:id (Edit)                          │
│  │  │  ├─ DELETE /api/items/:id                              │
│  │  │  ├─ PATCH /api/items/:id/toggle (Mark Done)            │
│  │  ├─ ExpenseController                                      │
│  │  │  ├─ POST /api/groups/:id/expenses (Add Expense)        │
│  │  │  ├─ GET /api/groups/:id/expenses (List)                │
│  │  │  ├─ POST /api/groups/:id/expenses/:id/split            │
│  │  │  └─ GET /api/groups/:id/summary (Balance Overview)     │
│  │  ├─ ChatController                                         │
│  │  │  ├─ POST /api/groups/:id/messages (Send)               │
│  │  │  ├─ GET /api/groups/:id/messages?limit=50              │
│  │  ├─ BudgetController                                       │
│  │  │  ├─ POST /api/groups/:id/budget                        │
│  │  │  └─ GET /api/groups/:id/budget                         │
│  │  └─ WebSocketHandler                                       │
│  │     └─ Handles Real-Time Connections                       │
│  │                                                              │
│  ├─ Services (Business Logic):                                 │
│  │  ├─ UserService                                            │
│  │  │  ├─ register()                                          │
│  │  │  ├─ login()                                             │
│  │  │  ├─ getUserById()                                       │
│  │  │  └─ updateProfile()                                     │
│  │  ├─ GroupService                                           │
│  │  │  ├─ createGroup()                                       │
│  │  │  ├─ getUserGroups()                                     │
│  │  │  ├─ addMember()                                         │
│  │  │  └─ removeMember()                                      │
│  │  ├─ ShoppingListService                                    │
│  │  │  ├─ addItem()                                           │
│  │  │  ├─ getItems()                                          │
│  │  │  ├─ toggleItem()                                        │
│  │  │  └─ deleteItem()                                        │
│  │  ├─ ExpenseService                                         │
│  │  │  ├─ addExpense()                                        │
│  │  │  ├─ splitExpense()                                      │
│  │  │  ├─ calculateBalance()                                  │
│  │  │  └─ getExpenseHistory()                                 │
│  │  ├─ ChatService                                            │
│  │  │  ├─ sendMessage()                                       │
│  │  │  ├─ getMessages()                                       │
│  │  │  └─ broadcastMessage(WebSocket)                         │
│  │  └─ WebSocketService                                       │
│  │     ├─ broadcast()                                         │
│  │     ├─ notify()                                            │
│  │     └─ onConnect/onDisconnect                              │
│  │                                                              │
│  ├─ Data Access Layer (DAO / Repository):                      │
│  │  ├─ UserDAO                                                │
│  │  ├─ GroupDAO                                               │
│  │  ├─ ShoppingItemDAO                                        │
│  │  ├─ ExpenseDAO                                             │
│  │  ├─ ChatMessageDAO                                         │
│  │  ├─ BudgetDAO                                              │
│  │  └─ DatabaseConnection (JDBC)                              │
│  │                                                              │
│  └─ Security & Utilities:                                      │
│     ├─ PasswordHasher (SHA-256 / bcrypt)                       │
│     ├─ SessionManager                                          │
│     ├─ TokenGenerator                                          │
│     └─ AuthInterceptor (Middleware)                            │
└────────────────────┬────────────────────────────────────────────┘
                     │
            JDBC / SQL
                     │
┌────────────────────▼────────────────────────────────────────────┐
│         🗄️ DATENBANK (PostgreSQL)                               │
│                                                                   │
│  ├─ users                   (Benutzer)                         │
│  │  ├─ id (PK)                                               │
│  │  ├─ email (UNIQUE)                                        │
│  │  ├─ password_hash                                         │
│  │  ├─ first_name                                            │
│  │  ├─ last_name                                             │
│  │  ├─ profile_picture_url                                   │
│  │  ├─ created_at                                            │
│  │  └─ updated_at                                            │
│  │                                                              │
│  ├─ groups                  (Einkaufsgruppen)                 │
│  │  ├─ id (PK)                                               │
│  │  ├─ name                                                  │
│  │  ├─ description                                           │
│  │  ├─ created_by (FK → users)                              │
│  │  ├─ created_at                                            │
│  │  └─ updated_at                                            │
│  │                                                              │
│  ├─ group_members           (Gruppen-Mitgliedschaften)       │
│  │  ├─ id (PK)                                               │
│  │  ├─ group_id (FK)                                        │
│  │  ├─ user_id (FK)                                         │
│  │  ├─ role (ENUM: admin, member)                          │
│  │  ├─ joined_at                                             │
│  │  └─ UNIQUE(group_id, user_id)                           │
│  │                                                              │
│  ├─ shopping_items          (Items in der Liste)             │
│  │  ├─ id (PK)                                               │
│  │  ├─ group_id (FK)                                        │
│  │  ├─ name                                                  │
│  │  ├─ quantity                                              │
│  │  ├─ category                                              │
│  │  ├─ completed (Boolean)                                  │
│  │  ├─ added_by (FK → users)                                │
│  │  ├─ created_at                                            │
│  │  └─ updated_at                                            │
│  │                                                              │
│  ├─ expenses                (Ausgaben)                        │
│  │  ├─ id (PK)                                               │
│  │  ├─ group_id (FK)                                        │
│  │  ├─ amount (Decimal 10,2)                                │
│  │  ├─ description                                           │
│  │  ├─ paid_by (FK → users)                                 │
│  │  ├─ paid_at (Date)                                        │
│  │  ├─ category                                              │
│  │  ├─ created_at                                            │
│  │  └─ updated_at                                            │
│  │                                                              │
│  ├─ expense_splits         (Ausgabe-Aufteilung)              │
│  │  ├─ id (PK)                                               │
│  │  ├─ expense_id (FK)                                      │
│  │  ├─ user_id (FK)                                         │
│  │  ├─ amount (Decimal 10,2)                                │
│  │  ├─ created_at                                            │
│  │  └─ UNIQUE(expense_id, user_id)                          │
│  │                                                              │
│  ├─ chat_messages           (Gruppenchat)                    │
│  │  ├─ id (PK)                                               │
│  │  ├─ group_id (FK)                                        │
│  │  ├─ sender_id (FK → users)                               │
│  │  ├─ message_text                                          │
│  │  ├─ created_at                                            │
│  │  └─ INDEX(group_id, created_at DESC)                    │
│  │                                                              │
│  ├─ budgets                 (Gruppen-Budgets)                │
│  │  ├─ id (PK)                                               │
│  │  ├─ group_id (FK)                                        │
│  │  ├─ amount (Decimal 10,2)                                │
│  │  ├─ period (ENUM: weekly, monthly, total)               │
│  │  ├─ set_by (FK → users)                                  │
│  │  ├─ created_at                                            │
│  │  └─ updated_at                                            │
│  │                                                              │
│  └─ sessions                (Session-Management)             │
│     ├─ id (PK)                                               │
│     ├─ user_id (FK)                                          │
│     ├─ token                                                 │
│     ├─ created_at                                            │
│     └─ expires_at                                            │
└─────────────────────────────────────────────────────────────────┘
```

---

## Kommunikations-Architektur

### REST API

**Authentifizierung:** Token-basiert (in `Authorization` Header)

```
Request Header:
Authorization: Bearer <session-token>
Content-Type: application/json

Response:
{
  "success": true,
  "data": {...},
  "error": null
}
```

### WebSocket

**Verbindung:** `ws://localhost:8080/ws?token=<session-token>`

**Message Format:**

```json
{
  "type": "item_added",
  "group_id": 1,
  "data": {
    "item_id": 42,
    "name": "Milch",
    "quantity": 2
  }
}
```

**Ereignis-Typen:**
- `item_added` - Neues Item hinzugefügt
- `item_updated` - Item bearbeitet
- `item_deleted` - Item gelöscht
- `item_completed` - Item als erledigt markiert
- `expense_added` - Neue Ausgabe
- `expense_split` - Ausgabe aufgeteilt
- `user_joined` - Nutzer tritt Gruppe bei
- `user_left` - Nutzer verlässt Gruppe
- `chat_message` - Neue Chat-Nachricht
- `balance_updated` - Saldo hat sich geändert

---

## Modul-Struktur (Java)

```
src/
├── main/
│   └── java/
│       └── com/
│           └── shoppinglist/
│               ├── server/
│               │   ├── HttpServer.java (Türöffner)
│               │   ├── RequestHandler.java (Router)
│               │   └── WebSocketServer.java
│               │
│               ├── controller/
│               │   ├─ AuthController.java
│               │   ├─ UserController.java
│               │   ├─ GroupController.java
│               │   ├─ ShoppingItemController.java
│               │   ├─ ExpenseController.java
│               │   ├─ ChatController.java
│               │   └─ BudgetController.java
│               │
│               ├── service/
│               │   ├─ UserService.java
│               │   ├─ GroupService.java
│               │   ├─ ShoppingListService.java
│               │   ├─ ExpenseService.java
│               │   ├─ ChatService.java
│               │   ├─ BudgetService.java
│               │   └─ WebSocketService.java
│               │
│               ├── repository/
│               │   ├─ UserRepository.java
│               │   ├─ GroupRepository.java
│               │   ├─ ShoppingItemRepository.java
│               │   ├─ ExpenseRepository.java
│               │   ├─ ChatRepository.java
│               │   ├─ BudgetRepository.java
│               │   └─ Database.java (JDBC Connection Pool)
│               │
│               ├── model/
│               │   ├─ User.java
│               │   ├─ Group.java
│               │   ├─ ShoppingItem.java
│               │   ├─ Expense.java
│               │   ├─ ExpenseSplit.java
│               │   ├─ ChatMessage.java
│               │   ├─ Budget.java
│               │   └─ Session.java
│               │
│               ├── security/
│               │   ├─ PasswordHasher.java
│               │   ├─ SessionManager.java
│               │   ├─ TokenGenerator.java
│               │   └─ AuthInterceptor.java
│               │
│               ├── util/
│               │   ├─ JsonParser.java
│               │   ├─ ValidationUtil.java
│               │   ├─ DateUtil.java
│               │   └─ Logger.java
│               │
│               └── Main.java (App Entry Point)
│
└── test/
    └── java/
        └── com/
            └── shoppinglist/
                ├── service/
                │   ├─ UserServiceTest.java
                │   ├─ ExpenseServiceTest.java
                │   └─ ...
                └── repository/
                    └─ UserRepositoryTest.java
```

---

## Frontend-Struktur (HTML/CSS/JavaScript)

```
public/
├── index.html (Einstiegspunkt)
├── css/
│   ├─ styles.css (Global Styles)
│   ├─ responsive.css (Mobile/Tablet)
│   └─ theme.css (Colors, Typography)
├── js/
│   ├─ main.js (App Initialization)
│   ├─ api-client.js (REST + WebSocket)
│   ├─ auth.js (Login/Register Logic)
│   ├─ router.js (Seiten-Navigation)
│   ├─ store.js (Client-Side State)
│   ├─ websocket-handler.js (Real-Time)
│   ├─ utils.js (Helper Functions)
│   └─ validation.js (Form Validation)
├── pages/
│   ├─ login.html
│   ├─ register.html
│   ├─ dashboard.html
│   ├─ shopping-list.html
│   ├─ expenses.html
│   ├─ profile.html
│   ├─ group-settings.html
│   └─ 404.html
└── assets/
    ├─ icons/
    ├─ images/
    └─ fonts/
```

---

## Authentifizierungs-Flow

```
1. Registrierung:
   User gibt Email + Passwort ein
   → Frontend: POST /api/register {email, password, firstName, lastName}
   → Backend: Hash Passwort, speichere in DB
   → Response: success + Session-Token
   → Frontend: Speichere Token (localStorage), redirect zu Dashboard

2. Login:
   User gibt Email + Passwort ein
   → Frontend: POST /api/login {email, password}
   → Backend: Verifiziere Passwort, erstelle Session
   → Response: Session-Token + Expire-Date
   → Frontend: Speichere Token, redirect zu Dashboard

3. Nachfolgende Requests:
   Frontend: Authorization Header: "Bearer <token>"
   Backend: Verifiziere Token vor jedem Request
   Wenn ungültig → 401 Unauthorized → Frontend: redirect zu Login
```

---

## Datenfluss für Echtzeit-Updates (WebSocket)

```
Szenario: Nutzer A fügt Item hinzu

1. Frontend A: Nutzer klickt "Add Item"
   → HTML Form Submission
   → REST API: POST /api/groups/<id>/items

2. Backend:
   → UserService validiert Nutzer
   → ShoppingListService: addItem()
   → ShoppingItemRepository: Insert in DB
   → WebSocketService: broadcast() an alle Clients in der Gruppe

3. WebSocket Broadcast:
   Message: {
     type: "item_added",
     group_id: <id>,
     data: {item_id, name, quantity, ...}
   }

4. Frontend (alle Clients der Gruppe):
   → WebSocket Handler empfängt Message
   → JavaScript update DOM in Echtzeit
   → Nutzer B sieht sofort: "Milch (2x)" in seiner Liste

5. Performance:
   → REST API Response: ~200ms
   → WebSocket Broadcast: ~50ms
   → Gesamtzeit bis Änderung sichtbar: ~250ms
```

---

## Error Handling

**Standardisierte Error-Response:**

```json
{
  "success": false,
  "error": {
    "code": "INVALID_CREDENTIALS",
    "message": "Email oder Passwort ist falsch",
    "details": null
  }
}
```

**HTTP Status Codes:**
- `200 OK` - Erfolgreich
- `201 Created` - Ressource erstellt
- `400 Bad Request` - Ungültige Input
- `401 Unauthorized` - Nicht authentifiziert
- `403 Forbidden` - Keine Berechtigung
- `404 Not Found` - Ressource nicht gefunden
- `500 Internal Server Error` - Server-Fehler

---

## Sicherheits-Implementierung

1. **Passwort-Sicherheit:**
   - Hashing: SHA-256 (mindestens, gerne bcrypt)
   - Salt pro Passwort
   - Niemals Plaintext speichern

2. **SQL Injection Prevention:**
   - Nur PreparedStatements verwenden
   - Keine String-Konkatenation in SQL

3. **XSS Prevention:**
   - Alle User-Inputs sanitizen
   - HTML-Encoding on Output

4. **CSRF Protection:**
   - Token für POST/PUT/DELETE Requests
   - Validierung auf Backend

5. **Session-Sicherheit:**
   - Eindeutige Tokens generieren
   - 30-Tage Expire Time
   - Logout invalidiert Token

6. **Data Privacy:**
   - Gruppen-Daten sind privat (nur Mitglieder)
   - User-Passwörter sind READONLY
   - Profildaten können nur von sich selbst geändert werden

---

## Performance-Optimierungen

1. **Datenbank:**
   - Indexe auf häufig abgerufenen Spalten (group_id, user_id)
   - Lazy Loading für related Data
   - Query-Caching für static Data

2. **Frontend:**
   - Minified CSS/JS in Production
   - Lazy Loading von Bildern
   - Caching von API-Responses (localStorage)

3. **Backend:**
   - Connection Pooling für DB
   - Async I/O für WebSocket
   - Efficient JSON Serialization

---

**Nächster Schritt:** Datenbank-Schema-Spezifikation (04-DATENBANKSCHEMA.md)
