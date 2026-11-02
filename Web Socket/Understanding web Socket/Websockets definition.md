# What are WebSockets and How do They Differ from HTTP?

WebSockets let a client and a server communicate in real time.

Normally, client-side applications such as web and mobile apps use HTTP. With HTTP, the client sends a request, and the server sends back a response. This is called the request and response cycle, as you've learned.

After the connection is established and data is exchanged, the connection closes. This works well for most things, like loading a page, fetching, or posting data. But it becomes slow and unreliable for real-time applications.

For example, think of a chat app. If you decide to go with HTTP for it, the client must keep asking the server for the data from time to time, with the connection opening, the data arriving, and the connection closing after that for each message.

This is the problem WebSockets solve. They create a permanent connection between the client and the server. Once the connection opens, both sides can exchange data anytime in a real-time channel until a closing signal is sent from either of them to the other.

## The Handshake

Even though WebSockets are different from HTTP, every WebSocket connection starts with HTTP, in a process called a **handshake**.

The client then requests the connection be upgraded to WebSocket. Once the server agrees, it sends a `101 Switching Protocols` response that upgrades the connection to WebSocket. After that, the connection stays open, and the real-time communication begins.

The flow looks like this:

1. Client connects to server via HTTP
2. Server accepts and upgrades the connection to WebSocket
3. Connection stays open
4. Both sides exchange data at any time until the connection closes

This flow is **bidirectional**, not request-response like HTTP.

```
Client <---> Server
```

With HTTP, the flow typically follows a request-response model:

```
Client ---> Request
Server ---> Response
```

## HTTP vs WebSocket

HTTP is like exchanging letters, and WebSocket is like a phone call. You write a letter, you wait for a reply, and the conversation ends. But with a phone call, you and the recipient talk in real time.

## Where WebSockets Are Used

WebSockets power real-time apps like:

- Chat apps
- Online multiplayer games
- Live sports updates
- Stock market dashboards
- Collaborative tools like Google Docs
