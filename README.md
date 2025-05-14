# ssh-login-banner
---

# 🎨 Customize the SSH Login Banner on Linux (Ubuntu/Debian)

This guide explains how to **create a custom banner** that is displayed when connecting via SSH. It covers two main methods:

1. Using the **dynamic MOTD system** (`/etc/update-motd.d/`)
2. Editing your shell config files (`.bashrc`, `.zshrc`, etc.)

---

## 🛠 Method 1: Using the Dynamic MOTD System

### 🔎 What is MOTD?

> MOTD = *Message of the Day*. It's a mechanism used to display information to the user right after SSH login.

On **Ubuntu/Debian** systems, the MOTD is **dynamic**, powered by scripts located in `/etc/update-motd.d/`.

---

### ✅ Steps to Create Your Own Banner

#### 1. Disable Existing MOTD Scripts

To disable the existing scripts, simply **remove their execution permission**:

```bash
sudo chmod -x /etc/update-motd.d/*
````

> 🔒 This disables them without deleting them.

---

#### 2. Create Your Custom Script

Create a script with a name **starting with `99-`** (e.g., `99-banner`) to ensure it's run **last**:

```bash
sudo nano /etc/update-motd.d/99-my-banner
```

Simple example:

```bash
#!/bin/bash

echo ""
echo "🎉 Welcome to $(hostname)!"
echo "📅 Current date: $(date)"
echo "👤 User: $(whoami)"
echo ""
```

Make it executable:

```bash
sudo chmod +x /etc/update-motd.d/99-my-banner
```

---

#### 3. Why the `99-` Prefix?

Ubuntu/Debian run scripts in `/etc/update-motd.d/` **in lexicographical order**.
By using `99-`, you ensure your custom script is **executed last**, so your message appears at the bottom — after any other messages (if others are re-enabled later).

---

## 🐚 Alternative Method: Using Shell Config Files (`.bashrc`, `.zshrc`...)

If you prefer a banner that appears **every time a terminal session is opened** (SSH or local), you can add a message to your shell's config file.

### Example for Bash (`~/.bashrc`):

```bash
# Add at the end of ~/.bashrc
echo "✨ Welcome, $(whoami)!"
```

### Example for Zsh (`~/.zshrc`):

```bash
# Add at the end of ~/.zshrc
echo "🧠 Ready to hack on $(hostname)?"
```

> ⚠️ These run on **every interactive shell**, not just SSH logins.

---

## 📌 Summary

| Method                    | Shown at SSH login | Local Terminal | Execution Order Control |
| ------------------------- | ------------------ | -------------- | ----------------------- |
| `/etc/update-motd.d/`     | ✅                  | ❌              | ✅ (via script prefix)   |
| `.bashrc`, `.zshrc`, etc. | ✅ (if interactive) | ✅              | ❌                       |

---

## 🔐 Best Practices

* **Never include sensitive data** (e.g., passwords, tokens, public IPs).
* You can test your script with:

  ```bash
  /etc/update-motd.d/99-my-banner
  ```
* Useful commands: `whoami`, `hostname`, `uptime`, `free`, `df`, etc.

---

## 📦 Advanced Example

A full banner example is available in [`99-gameshell`](./99-gameshell), with borders, emojis, colors (ANSI), and dynamic system info.

---

## 🧙‍♂️ Time to Customize!

Craft your own fantasy terminal! Make your shell feel like a game or a mission control dashboard 🚀

---
