## ⚙️ **Stage 1 — Core Server Foundation**

### 🧩 **Milestone 1: Project Skeleton & Bootstrapping**

**Goal:** Build the scaffolding; ensure everything compiles and runs.

* Run your PowerShell script to generate the directory tree.
* Initialize Git + `.gitignore`.
* Create a minimal `pom.xml` (Maven build + dependencies for Jackson and SLF4J).
* Implement a simple `Main.java` that starts the server on port 8080 and prints “Server running”.

**Deliverable:**
Running `java -jar target/LiteHttpServer.jar` starts the server and prints a startup message.

---

### 🌐 **Milestone 2: Accept Connections & Return Static Response**

**Goal:** Make the server respond to requests on a socket.

* Implement `HttpServer` using `ServerSocket` + a thread pool.
* Implement `ClientHandler` to read a raw request and send back:

  ```
  HTTP/1.1 200 OK
  Content-Type: application/json

  {"message": "Hello from LiteHttpServer!"}
  ```
* Verify via browser or `curl http://localhost:8080`.

**Deliverable:**
Client requests receive a valid HTTP response with headers and body.

---

### 🧠 **Milestone 3: HTTP Request Parsing**

**Goal:** Read and interpret actual request data.

* Implement `RequestParser` to extract:

  * HTTP method (`GET`, `POST`, etc.)
  * Path (`/users`, `/status`)
  * Headers (into a `Map<String,String>`)
  * Body (for POST/PUT)
* Create an `HttpRequest` class to represent parsed requests.
* Add simple logging in `Logger.java` for each request received.

**Deliverable:**
Logs show correct parsed data for any incoming HTTP request.

---

### 🪄 **Milestone 4: Structured Responses**

**Goal:** Standardize replies using reusable logic.

* Implement `HttpResponse` and `ResponseBuilder`.
* Add methods like `ResponseBuilder.ok(Object data)` or `ResponseBuilder.notFound()`.
* Convert objects to JSON using `JsonUtils` (wrap Jackson).

**Deliverable:**
Controllers can easily return JSON objects using a clean API.

---

### 🗺️ **Milestone 5: Routing System**

**Goal:** Let the server handle multiple endpoints dynamically.

* Implement `Router` and `RouteHandler`:

  ```java
  router.register("GET", "/users", new UserController()::getAllUsers);
  ```
* Modify `ClientHandler` to forward parsed requests to the router.
* Implement `UserController` and `ProductController` returning mock JSON.

**Deliverable:**
`GET /users` and `GET /products` return different JSON payloads.

---

### 🧵 **Milestone 6: Thread Safety & Concurrency**

**Goal:** Make the server handle multiple simultaneous clients.

* Test with multiple `curl` requests concurrently.
* Use a fixed thread pool (`Executors.newFixedThreadPool`) to avoid thread explosion.
* Handle exceptions gracefully—return `500` instead of crashing.

**Deliverable:**
Server responds correctly to concurrent requests without blocking.

---

### 📋 **Milestone 7: Logging & Basic Error Handling**

**Goal:** Gain observability and robustness.

* Add structured logs for every request and response.
* Return proper status codes (`404`, `400`, `500`).
* Log stack traces in dev mode but hide details in prod mode.

**Deliverable:**
Readable, timestamped logs for each request and error.

---

### 🧪 **Milestone 8: Testing**

**Goal:** Confirm stability before expansion.

* Unit test:

  * `RequestParserTest.java` (header/body parsing)
  * `RouterTest.java` (route registration)
* Manual test endpoints with `curl` and Postman.
* Measure latency for small load test (optional but informative).

**Deliverable:**
Green test results; server runs for hours without memory leaks or hangs.

---

## 🏁 **Stage 1 Completion Criteria**

By the end of Stage 1, your server should:

* Accept and parse HTTP/1.1 requests
* Route them correctly
* Return JSON responses
* Handle multiple concurrent clients
* Be stable, logged, and testable

---

Once that’s solid, **Stage 2 (Expansion)** could bring:

* URL parameters and query string parsing
* Middleware (CORS, compression, logging)
* HTTPS (SSL)
* Config file support
* Non-blocking I/O (NIO / Reactor model)
* Database integration
* WebSocket support
