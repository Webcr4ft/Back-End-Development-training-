# Health Checks and Graceful Shutdowns in Express (Simple Version)

## The Big Idea

Two patterns keep your app stable in production:

- **Health check** = a route that answers "Are you alive?"
- **Graceful shutdown** = stopping the app politely, so no requests get dropped and no data gets corrupted.

---

## 1. Health Checks

A health check is a simple route that says whether your app is running:

```js
app.get('/health', (req, res) => {
  res.status(200).send('OK')
})
```

Tools like load balancers and orchestrators (Kubernetes, AWS Elastic Beanstalk) ping this route regularly.

- Returns `200` → the app is healthy.
- No response → the orchestrator can restart the app automatically.

---

## 2. Graceful Shutdown

A graceful shutdown happens when your app is about to stop (a restart, a deployment, etc.). Instead of cutting everything off, the app **finishes what it's doing first**.

### Listening for shutdown signals

The system tells your app to stop by sending a **signal**:

| Signal | When it's sent |
|--------|----------------|
| `SIGTERM` | A tool like Kubernetes wants your app to stop (production) |
| `SIGINT` | You press `Ctrl + C` (local development) |

Without handling `SIGINT`, pressing `Ctrl + C` kills your app instantly and skips any cleanup. Since both should do the same thing, developers usually listen for both.

Here's the basic example for `SIGTERM`:

```js
process.on('SIGTERM', () => {
  server.close(() => {
    console.log('Server closed. Cleaning up...')
    // Close DB connections or other cleanup here
  })
})
```

`server.close()` means:

1. Stop accepting **new** connections.
2. Let **existing** requests finish.
3. Then run your cleanup code.

---

## 3. Putting It Together

Imagine your app runs in a container and Kubernetes sends a `SIGTERM` to update it.

With a basic graceful shutdown:

1. Your app stops accepting new connections.
2. It finishes current requests.
3. It disconnects from the database and exits cleanly.

No lost data, no corrupted state.

**The problem:** the load balancer doesn't know you're shutting down, so it may keep sending you new traffic.

---

## 4. Bonus: Mark the App as Unhealthy Before Shutdown

The fix is to make your health check return `503` (Service Unavailable) once shutdown begins. The load balancer sees this and stops sending new traffic.

```js
let isShuttingDown = false

app.get('/health', (req, res) => {
  if (isShuttingDown) {
    res.status(503).send('Shutting down')
  } else {
    res.status(200).send('OK')
  }
})

process.on('SIGTERM', () => {
  isShuttingDown = true

  server.close(() => {
    console.log('Graceful shutdown complete')
    // Perform cleanup
  })
})
```

**How it works:**

1. `SIGTERM` arrives and `isShuttingDown` becomes `true`.
2. The health check now returns `503`.
3. The load balancer stops routing new traffic to your app.
4. `server.close()` lets in-progress requests finish.
5. Cleanup runs and the app exits.

---

## Summary

- **Health check:** a `/health` route returning `200` so tools know your app is alive.
- **Graceful shutdown:** listen for `SIGTERM` and `SIGINT`, then use `server.close()` to finish current work before exiting.
- **Bonus:** return `503` from `/health` during shutdown so no new traffic arrives.
