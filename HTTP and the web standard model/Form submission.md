# What Happens When a Form Is Submitted and How Do the Different Form Submissions Work?

> **Think of it like a paper form at a doctor's office:**
> You fill in the blanks (**input fields**), the receptionist checks that nothing is missing (**validation**), and the form is sent to the right department (**action**) in a specific way (**method**). The department processes it and gives you an answer (**server response**).

---

## Why Use Forms?

Websites and apps need to collect data and process it, or generate something the user needs such as search results. So, just like text, forms are also a fundamental part of the web.

With forms, users can register and log in to a site, send messages, and search for items. For instance, you get access to the Google search results page by typing your query in the most popular form on the web, the Google search input.

| What users do | Form example |
| ------------- | ------------ |
| Register | Sign-up form |
| Log in | Username and password form |
| Send messages | Contact form |
| Search for items | Google search input |

---

## What Makes Up a Form?

Let's look at what makes up a form, like input fields, the action attribute, form methods, and most importantly, what happens when you submit a form.

| Part | What it does |
| ---- | ------------ |
| **`<form>` element** | The container that wraps all the input fields |
| **Input fields** | The boxes where users type or choose information |
| **`name` attribute** | Labels each field so the server knows which data belongs to which field |
| **`action` attribute** | Where the data is sent |
| **`method` attribute** | How the data is sent |

### The Form Element and Input Elements

Forms are embedded on a web page with the `form` element, but to get inputs to show up, you also need the `input` elements, based on your need. Some of those input elements are text, email, password, selection, file, hidden inputs, and more.

To use these input fields, you have to wrap them with the `form` element. Each of the inputs needs a `name` attribute so the server knows what data corresponds to each field.

Here is an example:

```html
<form>
   <input type="text" name="username" />
   <input type="email" name="email" />
   <input type="file" name="profilePicture" />
   <input type="radio" name="gender" />
   <input type="checkbox" name="subscribe" />
   <input type="hidden" name="userId" />
</form>
```

| Input type | What the user sees |
| ---------- | ------------------ |
| `text` | A box for typing any text |
| `email` | A box for an email address |
| `file` | A button to choose a file to upload |
| `radio` | A round button to pick one option |
| `checkbox` | A square box to tick on or off |
| `hidden` | Nothing. It sends data without showing it on screen |

> **Why is `name` so important?** When the form is sent, the server receives pairs like `username = Ana`. Without a `name`, the server wouldn't know what the value `Ana` belongs to.

---

## Form Validation

The input fields also need to be validated to ensure the user enters the correct information.

This validation can happen on both the **client-side** and the **server-side**. HTML lets you do basic client-side validation with the `required` and `pattern` attributes. Even so, you should also validate server-side for added security, as HTML validation is mostly for user experience and immediate feedback.

| Where | Who checks | Purpose |
| ----- | ---------- | ------- |
| **Client-side** | The browser | Fast feedback for the user (user experience) |
| **Server-side** | The server | Real security, because the browser's checks can be bypassed |

The `required` attribute specifies that the input field must be filled out, while the `pattern` attribute lets you enter regular expressions that force the user to type in the information the way you need it.

Here's an example of that for a username field:

```html
<input type="text" name="username" required pattern="[A-Za-z0-9]{3,}" />
```

> **What this means:** The username field can't be empty (`required`), and it must contain only letters (A-Z, a-z) and numbers (0-9), with at least 3 characters (`pattern="[A-Za-z0-9]{3,}"`).

| Username typed | Valid? | Why |
| -------------- | ------ | --- |
| `ana123` | Yes | Letters and numbers, 3+ characters |
| `ab` | No | Fewer than 3 characters |
| `ana_123` | No | The underscore isn't allowed |
| *(empty)* | No | The field is `required` |

---

## Form Submission

After the input fields are validated, submission should take place. So what happens when the form is submitted?

First, for submission to happen, the form needs to have an `action` attribute that specifies **where** the browser should send the values of the input fields to and a `method` attribute that specifies **how** the form data is submitted. More on the `method` attribute later.

Here's what an `action` attribute could look like:

```html
<form action="/register">
	<!-- input fields -->
</form>
```

> **What this means:** When this form is submitted, the browser sends the data to the `/register` address on the server.

### The `method` Attribute

The `method` attribute can either be `GET`, `POST`, `PUT`, `PATCH`, or `DELETE`:

| Method | What it does | Example |
| ------ | ------------ | ------- |
| `GET` | Retrieves something from the server | Search results |
| `POST` | Sends something to the server | Login or register information entered through the input fields |
| `PUT` | Modifies something on the server | Replacing a whole profile |
| `PATCH` | Partially modifies something on the server | Changing only your email |
| `DELETE` | Removes something from the server | Deleting an account |

Note that HTML doesn't support the `PUT`, `PATCH`, and `DELETE` methods directly, but there are workarounds. If you work with vanilla JavaScript, you can use the **Fetch API** to specify the method, and in Node.js and Express, you can use the **`method-override`** package.

| Situation | Workaround |
| --------- | ---------- |
| Vanilla JavaScript | Use the Fetch API to specify the method |
| Node.js and Express | Use the `method-override` package |

### GET Form Example

Here's what a form making a `GET` request could look like:

```html
<form action="/search" method="GET">
   <input type="text" name="q">
   <button type="submit">Search</button>
</form>
```

> **What this means:** If you type `cats` and click Search, the browser requests `/search` and sends your text along as `q=cats`. With `GET`, this data is usually visible in the page address, like `/search?q=cats`.

### POST Form Example

And here's what a form making a `POST` request could look like:

```html
<form action="/submit" method="POST">
   <input type="text" name="username" required pattern="[A-Za-z0-9]{3,}" />
   <input type="password" name="password" />
   <button type="submit">Submit</button>
</form>
```

> **What this means:** When you click Submit, the browser first checks the username rules, then sends the username and password to `/submit`. With `POST`, the data travels inside the request body instead of the address bar, which is why it's used for logins and registrations.

### GET vs. POST at a Glance

| | `GET` | `POST` |
| --- | ----- | ------ |
| **Purpose** | Retrieve something | Send something |
| **Typical use** | Search | Login, register |
| **Where the data goes** | Usually in the URL | In the request body |

---

## What Happens When a Form Is Submitted?

After the `GET` or `POST` request, the server checks for server-side validation and either processes or rejects the input values.

If the validation is successful, the server sends out the requested information or throws an error if the validation is unsuccessful.

If the validation is successful, the response from the server could be a redirect in case of authentication or search, or a success message confirming the action.

| Server-side validation | What the server does |
| ---------------------- | -------------------- |
| **Successful** | Processes the data and sends out the requested information. This could be a redirect (for authentication or search) or a success message confirming the action |
| **Unsuccessful** | Rejects the data and throws an error |

### Recap: The Full Journey of a Form

Here's a recap of what happens when a form is submitted:

1. The user fills out the form fields.
2. The browser checks for client-side validation (if any) and proceeds if the validation is successful.
3. The browser sends the form data to the server based on the `action` and `method` attributes.
4. The server receives the data and processes it (storing it in a database, registering a user, logging in a user, sending out search query, and so on).
5. If there's a server-side validation, the server rechecks the data before processing.
6. The server responds with a success message, error, or redirects the user based on the validation state (success or failure).
7. The user sees feedback based on the server response.

### Visual Summary

```
 ┌────────────────────────┐
 │ 1. User fills the form │
 └───────────┬────────────┘
             ▼
 ┌────────────────────────────────┐
 │ 2. Browser checks validation   │──── fails ──▶ User sees a message
 │    (required, pattern)         │               and fixes the input
 └───────────┬────────────────────┘
             │ passes
             ▼
 ┌────────────────────────────────┐
 │ 3. Browser sends the data      │
 │    (uses action + method)      │
 └───────────┬────────────────────┘
             ▼
 ┌────────────────────────────────┐
 │ 4. Server receives the data    │
 │ 5. Server validates again      │──── fails ──▶ Error response
 │    and processes it            │
 └───────────┬────────────────────┘
             │ passes
             ▼
 ┌────────────────────────────────┐
 │ 6. Server responds:            │
 │    success message or redirect │
 └───────────┬────────────────────┘
             ▼
 ┌────────────────────────────────┐
 │ 7. User sees the feedback      │
 └────────────────────────────────┘
```

### Real Example: Logging In

| Step | What happens |
| ---- | ------------ |
| 1 | You type your username and password |
| 2 | The browser checks that the fields are filled in and the username matches the pattern |
| 3 | The browser sends the data with `POST` to the `action` address |
| 4 | The server receives the data and checks it against the database |
| 5 | The server rechecks that the data is valid before processing |
| 6 | If correct, the server redirects you to your dashboard. If not, it sends an error |
| 7 | You see your dashboard, or an error message |
