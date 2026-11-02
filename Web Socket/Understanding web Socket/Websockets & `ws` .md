# WebSockets in Node.js with `ws` (Simple Version)

## The Big Idea

Node.js has **no built-in WebSocket server**. The popular fix is the **`ws`** library: lightweight, fast, and easy to use. It handles the WebSocket protocol so you can focus on sending and receiving messages.

---

## 1. Install It

```bash
npm install ws
```

---

## 2. Create a WebSocket Server

Import `ws` and create a server on a port:

```js
const WebSocket = require("ws");

const server = new WebSocket.Server({
  port: 3000,
});
```

This starts a server listening on port `3000`.

---

## 3. Handle Events

A WebSocket server works by listening for **events**.

| Event | When it fires |
|-------|---------------|
| `connection` | A new client joins |
| `message` | A client sends data |
| `close` | A connection closes |
| `error` | Something goes wrong |

### `connection`: a client joined

```js
server.on("connection", (socket) => {
  console.log("Client connected");
});
```

The `socket` is the connection between the server and **that one client**. You use it to send and receive messages.

### `message`: receiving data

```js
server.on("connection", (socket) => {
  socket.on("message", (message) => {
    console.log(message.toString());
  });
});
```

Messages arrive as raw data, so use `.toString()` to read them as text.

### Sending data back

```js
socket.send("Hello from the server");
```

As long as the connection is open, both sides can keep sending messages in real time.

### `close` and `error`

```js
socket.on("close", () => {
  console.log("Disconnected");
});

socket.on("error", (error) => {
  console.error(error);
});
```

---

## 4. Broadcasting

**Broadcasting** means sending a message to **many clients at once**, not just one.

**Example:** A chat room has John Doe, Jane Doe, and Wes Smith. When John sends a message, the server forwards it to Jane and Wes.

To do this, the server loops through all connected clients whenever a message arrives.

### Check the connection state first

Every connection has a `readyState` property. `WebSocket.OPEN` means the connection is active and ready.

Always check it before sending, so you don't send to clients who already left or are still connecting:

```js
if (client.readyState === WebSocket.OPEN) {
  // safe to send
}
```

### Full broadcast example

```js
server.on("connection", (socket) => {
  socket.on("message", (message) => {
    server.clients.forEach((client) => {
      if (client.readyState === WebSocket.OPEN) {
        client.send(message.toString());
      }
    });
  });
});
```

**How it works:**

1. A client sends a message.
2. The server loops through `server.clients` (everyone connected).
3. For each client that is `OPEN`, it sends the message.

---

## Where Broadcasting Is Used

- Chat messages
- Live notifications
- Sports updates
- Multiplayer game events

---

## Summary

With `ws`, building a WebSocket server takes four steps:

1. Create a server.
2. Listen for events (`connection`, `message`, `close`, `error`).
3. Send and receive messages.
4. Broadcast updates to all connected clients.

These building blocks are the foundation of most real-time apps.
