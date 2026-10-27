# How to Install Node.js with NVM

This guide shows you how to install **NVM (Node Version Manager)** and use it to install and manage Node.js on macOS, Linux, and Windows.

## Table of Contents

* [Why Use NVM?](#why-use-nvm)
* [Installing on macOS/Linux](#installing-on-macoslinux)
  * [Install NVM](#install-nvm-on-macoslinux)
  * [Install Node.js with NVM](#install-nodejs-with-nvm-on-macoslinux)
* [Installing on Windows](#installing-on-windows)
  * [Install nvm-windows](#install-nvm-windows)
  * [Install Node.js with nvm-windows](#install-nodejs-with-nvm-windows)
* [Basic Commands](#basic-commands)
* [Command Cheat Sheet](#command-cheat-sheet)
* [Key Takeaways](#key-takeaways)

---

## Why Use NVM?

Before installing Node.js, it is recommended to install **NVM**, a tool that manages **multiple versions of Node.js** on the same computer.

Setting it up from the start helps because different projects may need different Node.js versions. With NVM, switching between them is easy.

---

## Installing on macOS/Linux

### Install NVM on macOS/Linux

On macOS and Linux, NVM is installed through a shell script.

#### Step 1: Install Xcode command line tools (macOS only)

The official NVM documentation says you must install the Xcode command line tools **before** running the install script, otherwise it will fail.

```bash
xcode-select --install
```

Once the installation is finished, verify it:

```bash
xcode-select --version
```

#### Step 2: Run the NVM install script

Use **one** of these commands:

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.3/install.sh | bash
```

```bash
wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.3/install.sh | bash
```

> **Tip:** To get the latest version number, check the [official NVM documentation](https://github.com/nvm-sh/nvm?tab=readme-ov-file#install--update-script).

#### Step 3: Restart your terminal

You might need to restart your terminal to load the new command and configuration.

#### Step 4: Verify the installation

```bash
nvm -v
```

You should see your NVM version in the output.

---

### Install Node.js with NVM on macOS/Linux

#### Install the latest LTS version

```bash
nvm install --lts
```

The `--lts` flag installs the current **Long-Term Support (LTS)** version of Node.js. It is usually recommended because it:

* Prioritizes **stability, reliability, and security** over new or experimental features
* Is thoroughly tested and **ready for production**
* Has a **longer support period** with bug fixes and security patches

#### Install a specific version

```bash
nvm install <version>
```

For example, to install Node.js v20:

```bash
nvm install 20
```

#### Switch to a version

```bash
nvm use <version>
```

For example:

```bash
nvm use 20
```

#### Check your current Node.js version

```bash
node -v
```

---

## Installing on Windows

### Install nvm-windows

Official NVM only supports Windows in specific cases.

* **If you have WSL (Windows Subsystem for Linux):** follow the [macOS/Linux guide](#installing-on-macoslinux) above.
* **If you are using Windows directly:** use **nvm-windows**.

**nvm-windows** is a Node.js version management utility for Windows. It is a **completely separate project** from the official NVM, but it has the same purpose: working with multiple Node.js versions on one device.

> **Warning:** The official repository recommends **uninstalling any existing Node.js installation** before installing nvm-windows. If this is your first time installing Node.js, you should be fine.

#### Steps

1. Go to the [Releases page](https://github.com/coreybutler/nvm-windows/releases) of the official repository.
2. Download the latest installer.
3. Follow the instructions.
4. Restart your terminal if the `nvm` command is not available right away.

#### Verify the installation

```bash
nvm -v
```

---

### Install Node.js with nvm-windows

#### Install the latest LTS version

```bash
nvm install lts
```

> **Note:** On Windows the command is `lts`, without the `--` prefix.

#### Install a specific version

```bash
nvm install <version>
```

For example:

```bash
nvm install 20
```

#### Switch to a version

```bash
nvm use <version>
```

For example:

```bash
nvm use 20
```

#### Check your current Node.js version

```bash
node -v
```

---

## Basic Commands

These commands work with NVM on macOS/Linux (including WSL). Some may work differently, or not at all, with **nvm-windows**. Alternatives are listed where possible.

### Adjust PowerShell's Execution Policy (Windows only)

If you use **PowerShell** with **nvm-windows**, you may need to change the execution policy. The default policy is `Restricted`, a security measure that prevents scripts from running.

1. Right-click **PowerShell** and choose **Run as Administrator**.
2. Check the current execution policy:

   ```powershell
   Get-ExecutionPolicy
   ```

3. Set the policy to `RemoteSigned`, which allows local scripts and npm to run:

   ```powershell
   Set-ExecutionPolicy RemoteSigned
   ```

4. Close the administrator window and open a **non-admin** PowerShell window.

### List All Versions

Lists all installed Node.js versions and shows which one is in use:

```bash
nvm ls
```

### Set the Default Node.js Version (macOS/Linux only)

Sets the version used for new terminal sessions:

```bash
nvm alias default <version>
```

For example:

```bash
nvm alias default 22.20.0
```

### Create a Custom Alias (macOS/Linux only)

Give a version a more meaningful name:

```bash
nvm alias <new_name> <version>
```

For example:

```bash
nvm alias new-api 18.20.8
```

Then switch to it using the alias:

```bash
nvm use new-api
```

### Remove a Version of Node.js

```bash
nvm uninstall <version>
```

For example:

```bash
nvm uninstall 20.19.5
```

**On macOS/Linux**, you can also uninstall using just a major version:

```bash
nvm uninstall 20
```

If you have multiple releases of that major version (for example `20.14.0` and `20.12.2`), the **latest one is removed first**. In this case, `20.14.0` would be removed.

### Check Your Node.js Version

```bash
node -v
```

### Check Your npm Version

**npm** is a package manager for Node.js that lets you install, publish, and manage software packages. It is installed automatically with Node.js.

```bash
npm -v
```

### Run a JavaScript File

Runs the specified file using the active Node.js version:

```bash
node <file.js>
```

For example:

```bash
node app.js
```

---

## Command Cheat Sheet

| Task | macOS/Linux (NVM) | Windows (nvm-windows) |
| --- | --- | --- |
| Check NVM version | `nvm -v` | `nvm -v` |
| Install latest LTS | `nvm install --lts` | `nvm install lts` |
| Install a version | `nvm install <version>` | `nvm install <version>` |
| Switch version | `nvm use <version>` | `nvm use <version>` |
| List versions | `nvm ls` | `nvm ls` |
| Set default version | `nvm alias default <version>` | Not supported |
| Create custom alias | `nvm alias <name> <version>` | Not supported |
| Uninstall a version | `nvm uninstall <version>` | `nvm uninstall <version>` |
| Check Node.js version | `node -v` | `node -v` |
| Check npm version | `npm -v` | `npm -v` |
| Run a file | `node <file.js>` | `node <file.js>` |

---

## Key Takeaways

* **NVM** lets you install and switch between multiple Node.js versions.
* On **macOS**, install the Xcode command line tools before installing NVM.
* On **Windows**, use **nvm-windows** (or NVM through **WSL**).
* Use the **LTS** version for stability and security.
* Use `nvm use <version>` to switch versions and `node -v` to confirm.
* Use `node <file.js>` to run your JavaScript files.
