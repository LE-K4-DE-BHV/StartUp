# 🌐 Schritt 4: Erster Java HTTP-Server

**Ziel:** Einfacher HTTP-Server in Java ohne Frameworks, versteht HTTP-Handling, antwortet auf Requests
**Dauer:** 2 - 2.5h
**Wer:** Person 3 (Backend-Lead) + Person 4 (mit Pair-Programming)
**Schwierigkeit:** ⭐⭐⭐ (Herausfordernd, aber wichtig!)

---

## 🎯 Was macht ihr heute?

Am Ende habt ihr:
- ✅ Verstanden wie HTTP-Server funktionieren (kein Magic!)
- ✅ Java-Server läuft auf `localhost:8080`
- ✅ Server antwortet auf GET-Request mit JSON
- ✅ Server schreibt Logs in die Console
- ✅ Grundstruktur für zukünftige Controller

---

## 📋 Voraussetzungen

- ✅ PostgreSQL läuft (von gestern)
- ✅ Java JDK 11+ installiert: `java -version`
- ✅ IDE aufgesetzt (IntelliJ IDEA oder VSCode mit Java Extension)
- ✅ `src/main/java/com/shoppinglist/` Ordner existiert

---

## 👥 Pair-Programming Setup

```
Person 3: Erklärt Konzepte, schreibt 50%
Person 4: Tippt mit, stellt Fragen, schreibt 50%

Alle 30 min: Rollen wechseln!
```

---

## 🚀 Los geht's!

### **Schritt 1: Projekt-Struktur verstehen (10 min)**

Bevor wir Code schreiben: **Warum brauchen wir das?**

HTTP-Server = Programm, das:
1. Auf Port 8080 *lauscht*
2. Client-Request *empfängt* (GET, POST, etc.)
3. *Verarbeitet* den Request
4. *Antwortet* mit HTTP Response (HTML, JSON, etc.)

```
Client (Browser/Frontend)
    ↓ HTTP Request
    │ GET /api/status
    ↓
Server (Java)
    ↓ Verarbeitung
    │ - Request parsen
    │ - Business Logic
    │ - Response generieren
    ↓
Client (Browser/Frontend)
    ↑ HTTP Response
    │ {"status": "ok"}
    ↑
```

### **Schritt 2: Main-Server-Klasse erstellen (30 min)**

**Datei:** `src/main/java/com/shoppinglist/server/HttpServer.java`

```bash
# Falls noch nicht created, Datei erstellen
mkdir -p src/main/java/com/shoppinglist/server
cd src/main/java/com/shoppinglist/server
```

**Code schreiben:**

```java
package com.shoppinglist.server;

import java.io.*;
import java.net.*;

/**
 * Einfacher HTTP-Server ohne Frameworks
 * Lauscht auf http://localhost:8080
 */
public class HttpServer {
    private static final int PORT = 8080;
    private ServerSocket serverSocket;

    public static void main(String[] args) {
        HttpServer server = new HttpServer();
        server.start();
    }

    public void start() {
        try {
            // Erstelle ServerSocket (lauscht auf Port 8080)
            serverSocket = new ServerSocket(PORT);
            System.out.println("🚀 HTTP-Server läuft auf http://localhost:" + PORT);
            System.out.println("📝 Für Test öffnen: http://localhost:8080/api/status");

            // Schleife: Akzeptiere Connections
            while (true) {
                // Warte auf Client-Connection
                Socket clientSocket = serverSocket.accept();

                // Verarbeite in separatem Thread
                new ClientHandler(clientSocket).start();
            }

        } catch (IOException e) {
            System.err.println("❌ Server Fehler: " + e.getMessage());
            e.printStackTrace();
        }
    }

    public void stop() {
        try {
            if (serverSocket != null && !serverSocket.isClosed()) {
                serverSocket.close();
                System.out.println("🛑 Server gestoppt");
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

**Was bedeutet dieser Code?**

```java
ServerSocket serverSocket = new ServerSocket(PORT);
// → Erstellt einen Socket, der auf Port 8080 lauscht

while (true) {
    Socket clientSocket = serverSocket.accept();
    // → Wartet, bis ein Client sich verbindet
    // → accept() blockiert! (wartet)

    new ClientHandler(clientSocket).start();
    // → Verarbeite den Client in separatem Thread
    // → So können mehrere Clients gleichzeitig verbunden sein
}
```

**Kompilieren zum Testen:**

```bash
# Navigiere zum src-Ordner
cd src/main/java

# Kompiliere
javac com/shoppinglist/server/HttpServer.java

# Check
ls -la com/shoppinglist/server/
# Sollte HttpServer.class sehen
```

### **Schritt 3: ClientHandler-Klasse erstellen (40 min)**

**Datei:** `src/main/java/com/shoppinglist/server/ClientHandler.java`

Die ClientHandler-Klasse verarbeitet **einen Client-Request**:

```java
package com.shoppinglist.server;

import java.io.*;
import java.net.Socket;

/**
 * Behandelt einen einzelnen HTTP-Request
 * Läuft in separatem Thread
 */
public class ClientHandler extends Thread {
    private Socket socket;

    public ClientHandler(Socket socket) {
        this.socket = socket;
    }

    @Override
    public void run() {
        try {
            // Schritt 1: Request vom Client lesen
            BufferedReader reader = new BufferedReader(
                new InputStreamReader(socket.getInputStream())
            );

            // Erste Zeile: z.B. "GET /api/status HTTP/1.1"
            String requestLine = reader.readLine();
            System.out.println("📥 Request: " + requestLine);

            // Lese Headers (bis leere Zeile)
            String headerLine;
            while ((headerLine = reader.readLine()) != null && !headerLine.isEmpty()) {
                System.out.println("  Header: " + headerLine);
            }

            // Schritt 2: Request parsen
            String[] parts = requestLine.split(" ");
            String method = parts[0];      // GET, POST, etc.
            String path = parts[1];         // /api/status, /api/users, etc.

            // Schritt 3: Response generieren
            String response = handleRequest(method, path);

            // Schritt 4: HTTP-Response schreiben
            PrintWriter writer = new PrintWriter(
                socket.getOutputStream(), true
            );

            // HTTP Headers
            writer.println("HTTP/1.1 200 OK");
            writer.println("Content-Type: application/json");
            writer.println("Access-Control-Allow-Origin: *");
            writer.println("Content-Length: " + response.getBytes().length);
            writer.println();

            // Body
            writer.println(response);
            writer.flush();

            System.out.println("📤 Response gesendet");

        } catch (IOException e) {
            System.err.println("❌ ClientHandler Fehler: " + e.getMessage());
        } finally {
            try {
                socket.close();
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    }

    /**
     * Bestimmte Requests verschiedene Responses
     */
    private String handleRequest(String method, String path) {
        System.out.println("🔍 Handling: " + method + " " + path);

        // Route 1: Status-Check
        if (path.equals("/api/status")) {
            return "{\"status\": \"ok\", \"message\": \"Server läuft!\"}";
        }

        // Route 2: Health-Check
        if (path.equals("/api/health")) {
            return "{\"healthy\": true, \"timestamp\": \"" + System.currentTimeMillis() + "\"}";
        }

        // Default: Not Found
        return "{\"error\": \"Path nicht gefunden: " + path + "\"}";
    }
}
```

**Was tut dieser Code?**

```java
BufferedReader reader = new BufferedReader(...);
String requestLine = reader.readLine();
// → Liest erste Zeile: "GET /api/status HTTP/1.1"

String[] parts = requestLine.split(" ");
String method = parts[0];  // "GET"
String path = parts[1];     // "/api/status"
// → Parst den Request

String response = handleRequest(method, path);
// → Generiert JSON-Response aufgrund des Paths

writer.println("HTTP/1.1 200 OK");
writer.println("Content-Type: application/json");
// → HTTP Headers
writer.println(response);
// → Body (JSON)
```

**Kompilieren:**

```bash
javac com/shoppinglist/server/ClientHandler.java
```

### **Schritt 4: Main-Entry-Point (5 min)**

**Datei:** `src/main/java/com/shoppinglist/Main.java`

```java
package com.shoppinglist;

import com.shoppinglist.server.HttpServer;

/**
 * App Entry Point
 * So starten wir die ganze Anwendung später
 */
public class Main {
    public static void main(String[] args) {
        System.out.println("🚀 Starte Shopping-List API...");

        HttpServer server = new HttpServer();
        server.start();
    }
}
```

---

### **Schritt 5: Kompilieren & Testen (30 min)**

#### **Alles kompilieren:**

```bash
# Im Projekt-Root
cd shopingList/src/main/java

# Kompiliere alles
javac com/shoppinglist/Main.java
javac com/shoppinglist/server/*.java

# Check - sollte .class Dateien sehen
ls -la com/shoppinglist/server/
```

#### **Server starten:**

```bash
# Still im src/main/java Verzeichnis
java com.shoppinglist.Main

# Output sollte sein:
# 🚀 Starte Shopping-List API...
# 🚀 HTTP-Server läuft auf http://localhost:8080
# 📝 Für Test öffnen: http://localhost:8080/api/status
```

#### **Testen (in neuem Terminal/Tab):**

```bash
# Test 1: curl
curl http://localhost:8080/api/status
# Output: {"status": "ok", "message": "Server läuft!"}

# Test 2: Health-Check
curl http://localhost:8080/api/health
# Output: {"healthy": true, "timestamp": "1234567890"}

# Test 3: Unbekannter Path
curl http://localhost:8080/api/unknown
# Output: {"error": "Path nicht gefunden: /api/unknown"}

# Test 4: Im Browser
# Öffne: http://localhost:8080/api/status
# Sollte JSON anzeigen
```

---

## ✅ Checkliste - Server läuft?

- [ ] HttpServer.java kompiliert ohne Fehler
- [ ] ClientHandler.java kompiliert
- [ ] Main.java kompiliert
- [ ] Server startet: `java com.shoppinglist.Main`
- [ ] curl Test funktioniert (alle 3 Routes)
- [ ] Browser zeigt JSON
- [ ] Console zeigt Requests/Responses
- [ ] Server stoppt mit Ctrl+C

---

## 🎓 Was ihr gelernt habt

1. **Socket-Programmierung:** ServerSocket, accept()
2. **HTTP-Request-Parsing:** Methode, Path auslesen
3. **HTTP-Response-Generierung:** Headers + Body
4. **Multi-Threading:** Mehrere Clients gleichzeitig
5. **JSON-Responses:** einfache JSON-Strings

---

## ❓ Häufige Probleme

### **Problem 1: "Address already in use"**

```bash
# Port 8080 ist bereits in Verwendung
# Beende alten Server oder nutze anderen Port

# Windows: netstat -ano | findstr :8080
# Mac/Linux: lsof -i :8080

# Alternative Port: Ändere PORT = 8080 zu PORT = 8081
```

### **Problem 2: "Class nicht gefunden"**

```bash
# Java kann die Klasse nicht finden

# Stellt sicher, dass ihr im richtigen Verzeichnis seit
pwd
# Sollte zeigen: .../shopingList/src/main/java

# Dann kompilieren + Ziel richtig
java -cp . com.shoppinglist.Main
```

### **Problem 3: HTTP-Response-Body wird nicht angezeigt**

```bash
# curl -v zeigt mehr Details
curl -v http://localhost:8080/api/status

# Schaue ob Content-Length richtig ist
# Oder nutze long Strings in JSON
```

---

## 🚀 Nächste Schritte

Diese grundlegende Server ist der Start! Nächste Woche:
- [ ] REST API erweitern (mehr Routes)
- [ ] Datenbank-Verbindung hinzufügen
- [ ] Service-Layer (Business Logic) schreiben

---

**✅ Server läuft? Großartig!**

→ Nächstes: [Schritt 5: Datenbank-Schema implementieren](./05-datenbank-implementieren.md)
