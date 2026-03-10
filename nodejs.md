# 🟢 Node.js — Interview Questions & Answers

> Top Node.js interview questions with theoretical answers and code examples.
> Source: [Intellipaat — Node.js Interview Questions](https://intellipaat.com/blog/interview-question/node-js-interview-questions/)

---

## Basics

### Q1. What is Node.js?

**Node.js** is an open-source, cross-platform JavaScript runtime built on Chrome's **V8 engine**. It allows you to run JavaScript on the server side.

**Key Features:**

- Single-threaded with event-driven, non-blocking I/O
- Uses the V8 JavaScript engine
- Package ecosystem via **npm** (largest in the world)
- Great for I/O-heavy, real-time applications

---

### Q2. How does Node.js work?

Node.js uses a **single-threaded event loop** model:

1. Client sends a request
2. Node places it in the **Event Queue**
3. The **Event Loop** picks it up
4. If non-blocking → processes and returns response
5. If blocking → delegates to a **worker thread** from the thread pool
6. Worker completes → callback placed in event queue → Event Loop returns response

---

### Q3. What is npm?

**npm** (Node Package Manager) is the default package manager for Node.js. It hosts 1.5M+ packages.

```bash
# Install a package locally
npm install express

# Install globally
npm install -g nodemon

# Initialize a project
npm init -y

# Install dev dependency
npm install --save-dev jest
```

---

### Q4. Synchronous vs Asynchronous functions

| Feature     | Synchronous       | Asynchronous        |
| ----------- | ----------------- | ------------------- |
| Execution   | Blocks the thread | Non-blocking        |
| Performance | Slower for I/O    | Faster for I/O      |
| Use case    | Simple scripts    | Server applications |

```javascript
// Synchronous
const fs = require("fs");
const data = fs.readFileSync("file.txt", "utf8");
console.log(data);

// Asynchronous
fs.readFile("file.txt", "utf8", (err, data) => {
  if (err) throw err;
  console.log(data);
});
```

---

### Q5. What is the Event Loop in Node.js?

The **event loop** is the core of Node.js's asynchronous behavior. It continuously checks for pending events/callbacks and executes them.

**Phases:**

1. **Timers** — executes `setTimeout`, `setInterval` callbacks
2. **Pending Callbacks** — I/O callbacks deferred to next iteration
3. **Idle/Prepare** — internal use
4. **Poll** — retrieve new I/O events
5. **Check** — `setImmediate()` callbacks
6. **Close Callbacks** — e.g., `socket.on('close')`

```javascript
console.log("Start");
setTimeout(() => console.log("Timeout"), 0);
setImmediate(() => console.log("Immediate"));
process.nextTick(() => console.log("NextTick"));
console.log("End");

// Output: Start → End → NextTick → Timeout/Immediate (order may vary)
```

---

### Q6. Create a basic HTTP server in Node.js

```javascript
const http = require("http");

const server = http.createServer((req, res) => {
  res.writeHead(200, { "Content-Type": "text/plain" });
  res.end("Hello, World!");
});

server.listen(3000, () => {
  console.log("Server running on http://localhost:3000");
});
```

---

### Q7. Callbacks vs Promises vs Async/Await

```javascript
// 1. Callback
function fetchData(callback) {
  setTimeout(() => callback(null, "Data"), 1000);
}
fetchData((err, data) => console.log(data));

// 2. Promise
function fetchData() {
  return new Promise((resolve, reject) => {
    setTimeout(() => resolve("Data"), 1000);
  });
}
fetchData().then((data) => console.log(data));

// 3. Async/Await
async function getData() {
  const data = await fetchData();
  console.log(data);
}
getData();
```

---

### Q8. What is the purpose of package.json?

`package.json` is the manifest file for a Node.js project. It contains:

- Project metadata (name, version, description)
- **Dependencies** (`dependencies`, `devDependencies`)
- **Scripts** (start, test, build)
- Entry point (`main`)

```json
{
  "name": "my-app",
  "version": "1.0.0",
  "main": "index.js",
  "scripts": {
    "start": "node index.js",
    "dev": "nodemon index.js",
    "test": "jest"
  },
  "dependencies": {
    "express": "^4.18.2"
  },
  "devDependencies": {
    "nodemon": "^3.0.0"
  }
}
```

---

### Q9. Error Handling in Node.js

```javascript
// 1. Try-Catch (synchronous & async/await)
try {
  const data = JSON.parse("invalid json");
} catch (err) {
  console.error("Parse error:", err.message);
}

// 2. Error-first callbacks
fs.readFile("missing.txt", (err, data) => {
  if (err) {
    console.error("File error:", err.message);
    return;
  }
  console.log(data);
});

// 3. Promise .catch()
fetchData()
  .then((data) => console.log(data))
  .catch((err) => console.error(err));

// 4. Global uncaught exception handler
process.on("uncaughtException", (err) => {
  console.error("Uncaught:", err);
  process.exit(1);
});

// 5. Unhandled promise rejection
process.on("unhandledRejection", (reason) => {
  console.error("Unhandled Rejection:", reason);
});
```

---

### Q10. What are Streams in Node.js?

Streams are objects that let you read/write data in chunks, rather than loading everything into memory.

**Types:**
| Type | Description | Example |
|------|-------------|---------|
| **Readable** | Read data | `fs.createReadStream()` |
| **Writable** | Write data | `fs.createWriteStream()` |
| **Duplex** | Read + Write | TCP sockets |
| **Transform** | Modify data while reading/writing | `zlib.createGzip()` |

```javascript
const fs = require("fs");

// Reading a large file using streams
const readStream = fs.createReadStream("largefile.txt", "utf8");
const writeStream = fs.createWriteStream("output.txt");

readStream.pipe(writeStream);

readStream.on("data", (chunk) => {
  console.log(`Received ${chunk.length} bytes`);
});

readStream.on("end", () => console.log("Done reading"));
```

---

### Q11. What is Middleware in Express.js?

Middleware functions execute during the request-response cycle. They have access to `req`, `res`, and `next`.

```javascript
const express = require("express");
const app = express();

// Built-in middleware
app.use(express.json());

// Custom middleware (logging)
const logger = (req, res, next) => {
  console.log(`${req.method} ${req.url} - ${new Date().toISOString()}`);
  next();
};
app.use(logger);

// Route-specific middleware
const auth = (req, res, next) => {
  const token = req.headers["authorization"];
  if (!token) return res.status(401).json({ error: "Unauthorized" });
  next();
};

app.get("/protected", auth, (req, res) => {
  res.json({ message: "Secret data" });
});

// Error-handling middleware (4 params)
app.use((err, req, res, next) => {
  console.error(err.stack);
  res.status(500).json({ error: "Something went wrong" });
});

app.listen(3000);
```

---

### Q12. What is the `require()` function?

`require()` is Node's module system (CommonJS) to import modules.

```javascript
// Built-in modules
const fs = require("fs");
const path = require("path");

// Third-party modules
const express = require("express");

// Local modules
const utils = require("./utils");

// require() vs import (ES Modules)
// CommonJS (require)
const moduleA = require("./moduleA");

// ES Modules (import) — needs "type": "module" in package.json
import moduleA from "./moduleA.js";
```

---

### Q13. What is a RESTful API? Implementation in Node.js

```javascript
const express = require("express");
const app = express();
app.use(express.json());

let users = [
  { id: 1, name: "Alice", email: "alice@example.com" },
  { id: 2, name: "Bob", email: "bob@example.com" },
];

// GET all users
app.get("/api/users", (req, res) => {
  res.json(users);
});

// GET single user
app.get("/api/users/:id", (req, res) => {
  const user = users.find((u) => u.id === parseInt(req.params.id));
  if (!user) return res.status(404).json({ error: "User not found" });
  res.json(user);
});

// POST create user
app.post("/api/users", (req, res) => {
  const user = {
    id: users.length + 1,
    name: req.body.name,
    email: req.body.email,
  };
  users.push(user);
  res.status(201).json(user);
});

// PUT update user
app.put("/api/users/:id", (req, res) => {
  const user = users.find((u) => u.id === parseInt(req.params.id));
  if (!user) return res.status(404).json({ error: "User not found" });
  user.name = req.body.name || user.name;
  user.email = req.body.email || user.email;
  res.json(user);
});

// DELETE user
app.delete("/api/users/:id", (req, res) => {
  users = users.filter((u) => u.id !== parseInt(req.params.id));
  res.status(204).send();
});

app.listen(3000, () => console.log("API running on port 3000"));
```

---

### Q14. What are Event Emitters?

```javascript
const EventEmitter = require("events");

class OrderSystem extends EventEmitter {}

const orders = new OrderSystem();

// Register listener
orders.on("orderPlaced", (order) => {
  console.log(`New order: ${order.item} x${order.qty}`);
});

orders.on("orderPlaced", (order) => {
  console.log(`Sending confirmation email for order #${order.id}`);
});

// Emit event
orders.emit("orderPlaced", { id: 1, item: "Laptop", qty: 1 });
```

---

### Q15. What are Worker Threads?

Worker threads enable parallel execution for **CPU-intensive tasks** without blocking the event loop.

```javascript
const { Worker, isMainThread, parentPort } = require("worker_threads");

if (isMainThread) {
  const worker = new Worker(__filename);
  worker.on("message", (result) => {
    console.log(`Result from worker: ${result}`);
  });
  worker.postMessage(40); // Send data to worker
} else {
  parentPort.on("message", (n) => {
    // CPU-intensive task
    function fibonacci(n) {
      if (n <= 1) return n;
      return fibonacci(n - 1) + fibonacci(n - 2);
    }
    parentPort.postMessage(fibonacci(n));
  });
}
```

---

### Q16. Clustering in Node.js

```javascript
const cluster = require("cluster");
const http = require("http");
const os = require("os");

if (cluster.isMaster) {
  const numCPUs = os.cpus().length;
  console.log(`Master ${process.pid} forking ${numCPUs} workers`);

  for (let i = 0; i < numCPUs; i++) {
    cluster.fork();
  }

  cluster.on("exit", (worker) => {
    console.log(`Worker ${worker.process.pid} died. Restarting...`);
    cluster.fork();
  });
} else {
  http
    .createServer((req, res) => {
      res.end(`Handled by worker ${process.pid}`);
    })
    .listen(3000);
}
```

---

### Q17. What is the V8 Engine?

V8 is Google's open-source, high-performance JavaScript and WebAssembly engine written in C++. Node.js uses V8 to execute JavaScript outside the browser.

**Key features:** JIT compilation, garbage collection, hidden classes for fast property access.

---

### Q18. How do you handle Authentication in Node.js?

```javascript
const jwt = require("jsonwebtoken");
const SECRET = "your-secret-key";

// Generate token
app.post("/login", (req, res) => {
  const { username, password } = req.body;
  // Validate credentials...
  const token = jwt.sign({ username, role: "user" }, SECRET, {
    expiresIn: "1h",
  });
  res.json({ token });
});

// Auth middleware
const authenticate = (req, res, next) => {
  const token = req.headers.authorization?.split(" ")[1];
  if (!token) return res.status(401).json({ error: "No token" });

  try {
    const decoded = jwt.verify(token, SECRET);
    req.user = decoded;
    next();
  } catch (err) {
    res.status(403).json({ error: "Invalid token" });
  }
};

app.get("/dashboard", authenticate, (req, res) => {
  res.json({ message: `Welcome, ${req.user.username}` });
});
```

---

### Q19. What is REPL in Node.js?

**REPL** = Read-Eval-Print Loop. An interactive shell to execute JavaScript.

```bash
$ node
> 2 + 3
5
> const x = [1, 2, 3]
> x.map(n => n * 2)
[2, 4, 6]
> .exit
```

---

### Q20. spawn() vs fork() in Node.js

| Feature       | spawn()                | fork()                        |
| ------------- | ---------------------- | ----------------------------- |
| Purpose       | Launch any command     | Launch a new Node.js process  |
| Communication | Streams (stdin/stdout) | IPC channel (message passing) |
| Use case      | Run shell commands     | CPU-intensive Node.js tasks   |

```javascript
const { spawn, fork } = require("child_process");

// spawn - run a shell command
const ls = spawn("ls", ["-la"]);
ls.stdout.on("data", (data) => console.log(`Output: ${data}`));

// fork - run a separate Node.js file
const child = fork("./heavy-computation.js");
child.send({ data: "process this" });
child.on("message", (result) => console.log("Result:", result));
```

---

### Q21. File Operations in Node.js

```javascript
const fs = require("fs");
const fsPromises = require("fs").promises;

// Read file
const content = fs.readFileSync("file.txt", "utf8");

// Write file
fs.writeFileSync("output.txt", "Hello World");

// Append to file
fs.appendFileSync("log.txt", "New log entry\n");

// Check if file exists
if (fs.existsSync("file.txt")) {
  console.log("File exists");
}

// Using promises (modern approach)
async function fileOps() {
  await fsPromises.writeFile("data.json", JSON.stringify({ key: "value" }));
  const data = await fsPromises.readFile("data.json", "utf8");
  console.log(JSON.parse(data));
  await fsPromises.unlink("data.json"); // Delete
}
```

---

### Q22. What is PM2?

**PM2** is a production process manager for Node.js with built-in load balancing.

```bash
# Install
npm install -g pm2

# Start app
pm2 start app.js

# Cluster mode (use all CPUs)
pm2 start app.js -i max

# Monitor
pm2 monit

# View logs
pm2 logs

# Restart / Stop / Delete
pm2 restart app
pm2 stop app
pm2 delete app
```

---

### Q23. WebSocket Server in Node.js

```javascript
const WebSocket = require("ws");
const wss = new WebSocket.Server({ port: 8080 });

wss.on("connection", (ws) => {
  console.log("Client connected");

  ws.on("message", (message) => {
    console.log(`Received: ${message}`);
    // Broadcast to all clients
    wss.clients.forEach((client) => {
      if (client.readyState === WebSocket.OPEN) {
        client.send(`Echo: ${message}`);
      }
    });
  });

  ws.on("close", () => console.log("Client disconnected"));
  ws.send("Welcome to WebSocket server!");
});
```

---

### Q24. Unit Testing in Node.js

```javascript
// math.js
function add(a, b) {
  return a + b;
}
function multiply(a, b) {
  return a * b;
}
module.exports = { add, multiply };

// math.test.js (using Jest)
const { add, multiply } = require("./math");

describe("Math functions", () => {
  test("adds 2 + 3 to equal 5", () => {
    expect(add(2, 3)).toBe(5);
  });

  test("multiplies 3 * 4 to equal 12", () => {
    expect(multiply(3, 4)).toBe(12);
  });

  test("add returns a number", () => {
    expect(typeof add(1, 2)).toBe("number");
  });
});
```

```bash
# Run tests
npx jest
```

---

### Q25. Memory Leak Prevention

```javascript
// BAD: Global array keeps growing
let cache = [];
app.get("/data", (req, res) => {
  cache.push(new Array(1000000)); // Memory leak!
  res.send("OK");
});

// GOOD: Use a bounded cache (e.g., LRU)
const LRU = require("lru-cache");
const cache = new LRU({ max: 500 });

app.get("/data", (req, res) => {
  const key = req.query.id;
  if (cache.has(key)) return res.json(cache.get(key));
  const data = fetchFromDB(key);
  cache.set(key, data);
  res.json(data);
});

// Monitor memory usage
setInterval(() => {
  const usage = process.memoryUsage();
  console.log(`Heap: ${Math.round(usage.heapUsed / 1024 / 1024)} MB`);
}, 10000);
```

---

### Q26. What is GraphQL?

```javascript
const { ApolloServer, gql } = require("apollo-server");

const typeDefs = gql`
  type User {
    id: ID!
    name: String!
    email: String!
  }

  type Query {
    users: [User]
    user(id: ID!): User
  }
`;

const resolvers = {
  Query: {
    users: () => [
      { id: "1", name: "Alice", email: "alice@mail.com" },
      { id: "2", name: "Bob", email: "bob@mail.com" },
    ],
    user: (_, { id }) => ({ id, name: "Alice", email: "alice@mail.com" }),
  },
};

const server = new ApolloServer({ typeDefs, resolvers });
server.listen().then(({ url }) => console.log(`GraphQL at ${url}`));
```

---
