# Authentication and Authorization (Simple Version)

## The Big Idea

Picture a high-security office building.

1. At the front desk, a guard checks your ID card to confirm **who you are**. You're let into the lobby.
2. You then try the same card on the server room door. It flashes red. You're **not allowed in**.

That's the difference between the two pillars of web security:

- **Authentication** = proving who you are
- **Authorization** = deciding what you're allowed to do

---

## 1. Authentication

**Question it answers:** "Is this person who they claim to be?"

**How it works:**

1. When a user registers, they give an identifier (username or email) and a password. This is stored securely in the database.
2. When they log in later, the backend compares what they typed against what's stored.

### Three types of authentication factors

| Factor | Meaning | Examples |
|--------|---------|----------|
| **Something you know** | Secret information | Password, PIN, security question |
| **Something you have** | A physical item | Phone receiving an SMS code, authenticator app token |
| **Something you are** | Your body | Fingerprint, face scan |

---

## 2. Authorization

**Question it answers:** "What is this person allowed to do?"

Logging in doesn't mean you get full control. Authorization sets the rules, roles, and limits for each user.

### Example roles

| Role | Can do | Cannot do |
|------|--------|-----------|
| **Standard User** | Edit their own profile | View other users' private billing info |
| **Editor** | Write and publish blog posts | Delete the entire website codebase |
| **Admin** | Modify databases, delete users, change system settings | Nothing is off limits |

In backend code, this usually happens in **middleware** that checks the user's role or permissions before allowing access to a page or data.

---

## 3. Why Authentication Comes First

**Authentication always happens before authorization.**

You can't decide what someone is allowed to do until you know who they are.

```
Request → Authentication (Who are you?) → Authorization (What can you do?) → Access
```

---

## Easy Way to Remember

- **Authentication is the key** that opens the front door.
- **Authorization decides which rooms** you can enter once inside.

---

## Summary

- **Authentication** verifies identity (password, phone code, fingerprint).
- **Authorization** controls permissions (user, editor, admin).
- Authentication comes first, then authorization.
