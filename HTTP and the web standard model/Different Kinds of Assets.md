# What Are the Different Kinds of Assets That Are Returned in an HTTP Response?

In the last lesson, you learned that the server processes an HTTP request and sends back a response. That response includes various assets you see on the web.

The assets returned by an HTTP response include text-based assets, media assets, fonts, and so on. Each of these assets comes with a **`Content-Type` header**, which tells the browser how to process and display the asset correctly.

> **In simple terms:** An **asset** is any file the server sends back to your browser. The `Content-Type` header is like a label on the package that says "this is a picture" or "this is a web page," so the browser knows what to do with it.

> **Think of it like a delivery:**
> When you open a website, the server sends back a box of different items: the page structure, the colors and layout, the pictures, the fonts, and so on. Each item has a label (`Content-Type`) so your browser knows where it goes and how to use it.

## Quick Overview

| Category | What it includes | Examples |
| -------- | ---------------- | -------- |
| **Text-based assets** | The structure, style, behavior, and data of a page | HTML, CSS, JavaScript, JSON, XML |
| **Media assets** | Visual and sound content | Images, videos, audio |
| **Other assets** | Documents, archives, fonts, and programs | PDF, ZIP, WOFF, EXE |

---

## Text-Based Assets

Text-based assets have always been a fundamental part of the web. In fact, the web started as pure text. These days, text-based assets include the following:

| Asset | What it is | In plain words |
| ----- | ---------- | -------------- |
| **HTML** (Hypertext Markup Language) | The basic structure of any webpage. Without HTML, a webpage can't exist. | The **skeleton** of the page: headings, paragraphs, buttons, links. |
| **CSS** (Cascading Stylesheet) | The asset that controls how a webpage looks. With CSS, you apply styles like colors, fonts, and layout to the HTML. | The **appearance**: colors, fonts, spacing, layout. |
| **JavaScript** | JavaScript adds interactivity and dynamic content to HTML and CSS. | The **behavior**: what happens when you click, scroll, or type. |
| **JSON and XML** | These two formats let you transfer structured data between servers and browsers. | The **data**: organized information, like a list of products or a user profile. |

> **A house analogy:** HTML is the walls and rooms, CSS is the paint and decoration, JavaScript is the electricity and moving parts (lights, doors, appliances), and JSON/XML is the information being passed in and out, like mail.

### Example: What JSON and XML Look Like

Both formats carry the same data in different styles:

```json
{
  "name": "Ana",
  "age": 25
}
```

```xml
<user>
  <name>Ana</name>
  <age>25</age>
</user>
```

---

## Media Assets

Media assets include images, audios, and videos. They bring the web to life with visuals and sound.

### Images

Many websites rely on images to communicate visual information. Images come in different formats like JPG, JPEG, PNG, WEBP, and GIF.

### Video

Websites like YouTube and Vimeo serve video content with formats like MP4, MOV, AVI, WebM, and more.

### Audio

Audio is a key part of many platforms as it lets users stream music, podcasts, and other sound content. Common audio formats include MP3, AAC, Ogg, and WAV. Platforms like Spotify and YouTube Music rely on these formats to deliver high-quality audio experiences.

| Media type | Common formats | Where you see it |
| ---------- | -------------- | ---------------- |
| **Images** | JPG, JPEG, PNG, WEBP, GIF | Photos, logos, icons, memes |
| **Video** | MP4, MOV, AVI, WebM | YouTube, Vimeo |
| **Audio** | MP3, AAC, Ogg, WAV | Spotify, YouTube Music, podcasts |

---

## Other Assets

Other assets that are returned in an HTTP response are:

| Type | Formats | In plain words |
| ---- | ------- | -------------- |
| **Documents** | PDF, DOCX, PAGES | Files you read or edit, like reports and letters |
| **Compressed archives** | ZIP, RAR | Many files packed into one smaller file |
| **Font files** | WOFF, WOFF2, TTF | The text styles a website uses |
| **Executables** | EXE | Programs you can run on your computer |

---

## Content-Type Reference Table

Here's a table of these common assets and their content types:

| Asset Type | Content-Type Header |
| ---------- | ------------------- |
| HTML | `text/html` |
| CSS | `text/css` |
| JavaScript | `text/javascript` |
| JPEG | `image/jpeg` |
| PNG | `image/png` |
| GIF | `image/gif` |
| SVG | `image/svg+xml` |
| WebP | `image/webp` |
| WOFF | `font/woff` |
| WOFF2 | `font/woff2` |
| TTF | `font/ttf` |
| OTF | `font/otf` |
| MP4 | `video/mp4` |
| WebM | `video/webm` |
| Ogg (Video) | `video/ogg` |
| MP3 | `audio/mpeg` |
| AAC | `audio/aac` |
| WAV | `audio/wav` |
| Ogg (Audio) | `audio/ogg` |
| JSON | `application/json` |
| XML | `application/xml` |
| PDF | `application/pdf` |
| ZIP | `application/zip` |

### How to Read a Content-Type

A content type has two parts separated by a slash: **type/subtype**.

```
   image  /  png
     │        │
   type    subtype
 (category) (exact format)
```

| Starts with | Meaning |
| ----------- | ------- |
| `text/` | Text-based content (HTML, CSS, JavaScript) |
| `image/` | Pictures |
| `video/` | Videos |
| `audio/` | Sound |
| `font/` | Font files |
| `application/` | Data or files that apps handle (JSON, XML, PDF, ZIP) |

### Example: Content-Type in a Real Response

```http
HTTP/1.1 200 OK
Content-Type: image/png

(image data here)
```

The browser sees `Content-Type: image/png` and knows to display the data as a picture, rather than trying to show it as text.

---

## Putting It All Together

When you load a single web page, the server usually returns many assets, each with its own `Content-Type`:

```
 You visit a website
        │
        ▼
 ┌──────────────────────────────────────────┐
 │ 1. HTML        (text/html)               │ ← page structure
 │ 2. CSS         (text/css)                │ ← styles
 │ 3. JavaScript  (text/javascript)         │ ← interactivity
 │ 4. Fonts       (font/woff2)              │ ← text styles
 │ 5. Images      (image/png, image/jpeg)   │ ← visuals
 │ 6. Data        (application/json)        │ ← dynamic content
 └──────────────────────────────────────────┘
        │
        ▼
 Browser reads each label (Content-Type)
 and displays everything correctly
```
