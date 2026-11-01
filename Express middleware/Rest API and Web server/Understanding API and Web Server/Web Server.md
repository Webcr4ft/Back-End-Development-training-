# How Do Web Services Work?

## The Big Picture

Web services and REST APIs power most of the apps and websites you use. They let different applications **talk to each other and share data** over a network, usually the internet.

## API vs Web Service

- **API (Application Programming Interface)**: any way for software to communicate with other software.
- **Web service**: a specific kind of API that uses web technologies like HTTP to exchange data over a network.

> Every web service is an API, but not every API is a web service.

Think of a web service as a **bridge between software**. It has no user interface. People don't use it directly; apps do.

## Characteristics of a Web Service

| Characteristic | What it means |
|---|---|
| Runs on a server | Hosted online like a website, but exposes data or functionality instead of pages |
| Machine-to-machine | Built for apps to consume, not for humans to view directly |
| Language-agnostic | Can be written in any language (Java, C#, JavaScript), and apps in other languages can still use it |
| Platform-agnostic | Works across systems (a Linux server can talk to a Windows device) |
| Standard web protocols | Uses HTTP/HTTPS for data, FTP for file transfer, SMTP for email |

## Types of Web Services

The best-known are **REST** and **SOAP**. Others exist, like XML-RPC and UDDI.

## REST APIs

**REST** stands for **Representational State Transfer**. It is by far the most widely used type because it is simple, flexible, and fits naturally with the web.

### How it works

REST APIs expose **resources**, represented by URL paths:

- `/users` : all users
- `/users/20` : the user with ID 20

When a client requests a resource, the server returns a **representation** of it, usually JSON (but it can also be XML or plain text).

### Choosing the format

The client uses the `Accept` header to say what format it wants:

```http
Accept: application/json
```

```http
Accept: application/xml
```

### JSON response

```json
{
  "id": 20,
  "name": "John Doe",
  "email": "john@example.com",
  "role": "admin",
  "createdAt": "2025-09-22T10:30:00Z"
}
```

### XML response (same data)

```xml
<user>
  <id>20</id>
  <name>John Doe</name>
  <email>john@example.com</email>
  <role>admin</role>
  <createdAt>2025-09-22T10:30:00Z</createdAt>
</user>
```

## SOAP APIs

**SOAP** stands for **Simple Object Access Protocol**.

- Uses **only XML**
- Common in **enterprise systems** that need strict standards and strong security
- More rigid and verbose than REST

Example request:

```xml
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/">
   <soapenv:Body>
      <getUser>
         <userId>20</userId>
      </getUser>
   </soapenv:Body>
</soapenv:Envelope>
```

## Other Web Services

- **XML-RPC**: encodes requests and responses in XML. Lightweight, but less flexible than REST.
- **UDDI**: not for exchanging data. It is an XML-based **directory** where businesses list, discover, and describe their web services.

## REST vs SOAP

| | REST | SOAP |
|---|---|---|
| Data format | JSON, XML, plain text | XML only |
| Complexity | Simple and flexible | Strict and verbose |
| Common use | Most modern apps | Enterprise systems |

## Key Points

- A web service lets **software talk to software** over the web.
- REST is the most popular choice today.
- REST works with **resources** (URLs) and returns **representations** (usually JSON).
- The `Accept` header lets the client choose the response format.
- SOAP is XML-only and used where strict standards and security matter.
