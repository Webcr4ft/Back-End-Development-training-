# What Are Microservices?

## The Old Way: Monoliths

A **monolith** is one giant codebase that contains **everything** in the app: the UI, the API, and the database logic.

Imagine an online store like Amazon where all of these live in one codebase:

- Product pages
- Checkout
- Payment processing
- Authentication and authorization
- The API and databases behind them

### Pros and cons

Monoliths work well for **small apps and early-stage startups**. But as the app grows, problems appear:

- Harder to maintain
- Slower to update
- Difficult to scale
- A small change can force you to **redeploy the entire system**
- Scaling one feature means **scaling the whole app**

## The New Way: Microservices

**Microservices** are an architectural approach that fixes the limits of monoliths.

A large app is broken into **smaller, independent services**. Each service handles one specific business capability, such as:

- Products
- Orders
- Authentication
- Payments

Each service often has:

- Its own codebase
- Its own database
- Its own team

The services talk to each other through **APIs** or **message-based systems**, so together they work as one application.

## Monolith vs Microservices

| | Monolith | Microservices |
|---|---|---|
| Structure | One codebase | Many small services |
| Deployment | Redeploy everything | Deploy each service separately |
| Scaling | Scale the whole app | Scale only what you need |
| Technology | One stack | Different stack per service |
| Complexity | Simple at first | More complex overall |
| Best for | Small apps, startups | Large, growing apps |

## Example: E-commerce Platform

Separate services for:

- Products
- Carts
- Users
- Orders
- Payments

Each can be **built, deployed, and scaled independently** without affecting the others. If payments get heavy traffic, you scale only the payment service.

## Different Languages Per Service

Each service can use the tool that fits it best:

- Search service: Java
- Product service: Node.js
- Authentication service: .NET

## Advantages

- **Faster development**: teams work on separate services at the same time
- **Better fault isolation**: if one service fails, the others can keep running
- **Greater flexibility**: choose different languages and frameworks per service
- **Independent scaling and deployment**

## Challenges

- **Harder debugging**: one issue can span multiple services
- **Complex deployment and infrastructure**: many services to manage
- **Network overhead**: services communicate constantly, which adds latency

## Key Points

- A monolith is **one codebase**; microservices are **many small, independent services**.
- Monoliths are great to start with; microservices help when an app **grows large**.
- Services communicate through **APIs or messages**.
- Microservices bring flexibility and scalability, but also **more complexity**.
