# Node.js Stream Module: A Simple Guide

## What Is the Stream Module?

`stream` is a core Node.js module for handling data **efficiently**, especially when the data is too big to load all at once (like a large text file or a video).

Instead of waiting for all the data to load, streams process it **in small chunks as it arrives**. It's like watching a YouTube video before it has fully downloaded.

---

## Types of Streams

| Type | What it does | Example |
| --- | --- | --- |
| **Readable** | Reads data in chunks | Reading a large file |
| **Writable** | Writes data in chunks | Saving a file |
| **Duplex** | Both reads and writes | A network connection |
| **Transform** | A duplex stream that **changes** data as it passes through | Compressing a file |

You can import the stream classes you need like this:

```js
const { Readable, Writable, Transform } = require("stream");
```

---

## Built-In File Streams

Most of the time you don't need to build custom streams. For everyday file work, these two methods are enough:

- `fs.createReadStream()` reads a file in chunks
- `fs.createWriteStream()` writes a file in chunks

Both take a **file path**, so you'll usually need the `fs` and `path` modules too.

---

## Reading Data With a Readable Stream

Say you have a file called `input.txt`:

```js
const fs = require("fs");
const path = require("path");

const inputFilePath = path.join(__dirname, "input.txt");

// Readable stream
const readInputFileStream = fs.createReadStream(inputFilePath);
console.log(readInputFileStream);
```

This **doesn't read anything yet**. You need to listen to the stream's **events** to get the data.

### The `data` Event

This event fires each time a **chunk** of data arrives:

```js
readInputFileStream.on("data", (chunk) => {
  console.log(`Received ${chunk.length} bytes of data`);
}); // Received 622 bytes of data
```

If you log the chunk itself, you get a **Buffer** (raw bytes):

```js
readInputFileStream.on("data", (chunk) => {
  console.log(`Received ${chunk.length} bytes of data`);
  console.log("Received data:", chunk);
});

/*
Received 622 bytes of data
Received data: <Buffer 4c 6f 72 65 6d 20 69 70 73 75 6d 20 64 6f 6c 6f 72 ... 572 more bytes>
*/
```

### Converting Buffers to Text

Use `toString()` to turn the buffer into readable text:

```js
const fs = require("fs");
const path = require("path");

const inputFilePath = path.join(__dirname, "input.txt");

// Readable stream
const readInputFileStream = fs.createReadStream(inputFilePath);

readInputFileStream.on("data", (chunk) => {
  console.log(`Received ${chunk.length} bytes of data`);
  console.log("Received data:", chunk.toString());
});

/*
Received 622 bytes of data
Received data: Lorem ipsum dolor sit amet consectetur adipisicing elit. Ducimus sint facilis
aliquid. Odio voluptatibus veniam saepe consectetur alias modi non fuga in,
tempore explicabo numquam maiores quod inventore quibusdam! ...
*/
```

---

## Writing Data With a Writable Stream

To copy from one file to another, create the **read stream first**, then the **write stream**:

```js
const fs = require("fs");
const path = require("path");

const inputFilePath = path.join(__dirname, "input.txt");
const outputFilePath = path.join(__dirname, "output.txt");

// Create the read stream first
const readInputFileStream = fs.createReadStream(inputFilePath);

// Create the write stream
const writeOutputFileStream = fs.createWriteStream(outputFilePath);
```

### Connecting Streams With `pipe()`

`.pipe()` connects the readable stream to the writable stream. Node.js then automatically reads from the source and writes to the destination, **chunk by chunk**.

```js
// Pipe the read stream to the write stream
readInputFileStream.pipe(writeOutputFileStream);
```

Think of it like a pipe carrying water from one tank to another.

### Handling `finish` and `error` Events

Listen to these events on the **writable stream** to know what happened:

| Event | Meaning |
| --- | --- |
| `finish` | Streaming is complete and there's no more data to write |
| `error` | Something went wrong (like permission issues or a missing folder) |

Full example:

```js
const fs = require("fs");
const path = require("path");

const inputFilePath = path.join(__dirname, "input.txt");
const outputFilePath = path.join(__dirname, "output.txt");

// Create the read stream first
const readInputFileStream = fs.createReadStream(inputFilePath);

// Create the write stream
const writeOutputFileStream = fs.createWriteStream(outputFilePath);

readInputFileStream.pipe(writeOutputFileStream);

writeOutputFileStream.on("finish", () => {
  console.log("All data has been written to the file");
});

writeOutputFileStream.on("error", (err) => {
  console.error("Error writing to file:", err);
});
```

---

## Quick Summary

| Goal | Use |
| --- | --- |
| Read a file in chunks | `fs.createReadStream()` |
| Write a file in chunks | `fs.createWriteStream()` |
| Get each chunk of data | `.on("data", ...)` |
| Convert a chunk to text | `chunk.toString()` |
| Connect two streams | `.pipe()` |
| Know when writing is done | `.on("finish", ...)` |
| Catch problems | `.on("error", ...)` |

**Why streams matter:** they use less memory and start working right away, because they never need to load an entire file at once.
