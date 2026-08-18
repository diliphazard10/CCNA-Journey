# Day 04 — Cisco CLI & Basic Device Configuration

> **CCNA 200-301 v1.1 · Network Fundamentals / Network Access**

![CCNA](https://img.shields.io/badge/CCNA-200--301-blue)
![Day](https://img.shields.io/badge/Day-04-green)
![Topic](https://img.shields.io/badge/Topic-Cisco%20CLI-orange)
![Lab](https://img.shields.io/badge/Lab-Cisco%20Packet%20Tracer-red)

---

## 📌 Day 04 Overview

Today I learned the basics of the **Cisco Command-Line Interface (CLI)** and how network engineers interact with Cisco devices.

I practiced:

- Connecting to a Cisco device.
- Understanding Cisco CLI modes.
- Moving between User EXEC, Privileged EXEC, and Global Configuration modes.
- Configuring device passwords.
- Understanding `enable password` and `enable secret`.
- Understanding `service password-encryption`.
- Understanding running configuration and startup configuration.
- Saving configuration changes so they survive a reboot.

These are foundational Cisco IOS skills that I will use throughout my CCNA journey.

---

# 🎯 Learning Objectives

By the end of Day 04, I should be able to:

- Explain what the Cisco CLI is.
- Identify Cisco IOS command modes.
- Connect to a Cisco device through the console.
- Recognize User EXEC, Privileged EXEC, and Global Configuration prompts.
- Move between CLI modes.
- Configure an `enable secret`.
- Explain the difference between `enable password` and `enable secret`.
- Explain what `service password-encryption` does.
- Understand running configuration.
- Understand startup configuration.
- Save running configuration to startup configuration.
- Explain why unsaved changes can be lost after a reload.

---

# 🖥️ 1. What Is the Cisco CLI?

CLI stands for:

> **Command-Line Interface**

Cisco IOS devices can be configured and monitored by entering commands into the CLI.

Examples:

```text
show ip interface brief
```

```text
configure terminal
```

The CLI is one of the most important tools for a network engineer because it provides direct access to device configuration and operational information.

---

# 🔌 2. Connecting to a Cisco Device

A common way to initially access a Cisco router or switch is through the **console connection**.

Basic Packet Tracer workflow:

```text
PC
 |
 | Console cable
 v
Cisco Switch/Router
```

### Steps

1. Add a PC.
2. Add a Cisco router or switch.
3. Select the console cable.
4. Connect the PC to the device's Console port.
5. Open the PC.
6. Open **Terminal**.
7. Accept the default terminal settings.
8. Press Enter if necessary.
9. The Cisco CLI appears.

A physical network connection is not required for initial console access.

---

# ⌨️ 3. Cisco CLI Modes

Cisco IOS uses different command modes.

The three major modes learned today are:

```text
User EXEC
    ↓
Privileged EXEC
    ↓
Global Configuration
```

Each mode provides different commands and permissions.

---

# 🟢 4. User EXEC Mode

User EXEC mode is the initial mode after connecting to a Cisco device.

Typical prompt:

```text
Router>
```

or:

```text
Switch>
```

The `>` symbol indicates:

> **User EXEC mode**

User EXEC provides limited monitoring and basic commands.

To enter Privileged EXEC mode:

```text
Router> enable
```

Prompt changes to:

```text
Router#
```

---

# 🔴 5. Privileged EXEC Mode

Privileged EXEC mode is identified by:

```text
Router#
```

or:

```text
Switch#
```

The `#` symbol indicates:

> **Privileged EXEC mode**

This mode provides access to more powerful monitoring commands and allows entry into configuration modes.

Example:

```text
Router# show running-config
```

Enter Global Configuration mode:

```text
Router# configure terminal
```

or:

```text
Router# conf t
```

Prompt becomes:

```text
Router(config)#
```

---

# 🟡 6. Global Configuration Mode

Global Configuration mode is identified by:

```text
Router(config)#
```

This mode is used to make configuration changes that affect the device globally.

Examples:

```text
Router(config)# hostname R1
```

```text
Router(config)# enable secret MySecret
```

```text
Router(config)# service password-encryption
```

---

# 🔄 7. Moving Between Modes

Basic navigation:

```text
User EXEC
Router>
     |
     | enable
     ↓
Privileged EXEC
Router#
     |
     | configure terminal
     ↓
Global Configuration
Router(config)#
```

Return to Privileged EXEC:

```text
Router(config)# end
```

Move back one level:

```text
Router(config)# exit
```

Return from Privileged EXEC to User EXEC:

```text
Router# disable
```

---

# 🧭 8. CLI Mode Quick Reference

| Mode | Prompt | Purpose |
|---|---|---|
| User EXEC | `Router>` | Basic access and monitoring |
| Privileged EXEC | `Router#` | Advanced monitoring and configuration access |
| Global Configuration | `Router(config)#` | Global device configuration |

### Easy memory trick

```text
>          = User EXEC

#          = Privileged EXEC

(config)#  = Global Configuration
```

---

# 🔐 9. Enable Password

The `enable password` command can configure a password for entering Privileged EXEC mode.

Example:

```text
Router(config)# enable password cisco
```

Then:

```text
Router(config)# end
Router# disable
Router> enable
Password:
```

However, `enable password` is an older and less secure method compared with `enable secret`.

---

# 🔒 10. Enable Secret

The preferred command is:

```text
Router(config)# enable secret MySecret
```

This protects access to Privileged EXEC mode.

Example:

```text
Router(config)# enable secret class
```

Then:

```text
Router# disable
Router> enable
Password:
```

The configured secret is required to enter Privileged EXEC mode.

---

# ⚖️ 11. Enable Password vs Enable Secret

| Feature | `enable password` | `enable secret` |
|---|---|---|
| Purpose | Protect Privileged EXEC | Protect Privileged EXEC |
| Security | Older/weaker | Stronger |
| Preferred | ❌ Generally not preferred | ✅ Preferred |
| Configuration protection | Less secure | Stronger password protection |

### Important

If both are configured, Cisco IOS uses the **enable secret** for Privileged EXEC authentication.

For CCNA:

> **Use `enable secret` rather than `enable password` when protecting Privileged EXEC mode.**

---

# 🔐 12. Service Password-Encryption

Cisco IOS can obscure plaintext passwords in the configuration using:

```text
Router(config)# service password-encryption
```

Then:

```text
Router# show running-config
```

Relevant passwords that would otherwise appear in plaintext are displayed in an obscured form.

### Important security note

`service password-encryption` is **not strong modern password hashing**. It primarily prevents passwords from being displayed plainly in the configuration.

Do not confuse it with the stronger protection used for `enable secret`.

---

# 📋 13. Running Configuration

The **running configuration** is the configuration currently active on the device.

It represents what the device is currently using.

View it with:

```text
Router# show running-config
```

Short form:

```text
Router# show run
```

Think:

> **Running = Current**

---

# 💾 14. Startup Configuration

The **startup configuration** is the saved configuration stored in nonvolatile memory.

It is used when the device boots.

View it with:

```text
Router# show startup-config
```

Short form:

```text
Router# show start
```

Think:

> **Startup = Saved**

---

# ⚠️ 15. Running vs Startup Configuration

| Running Config | Startup Config |
|---|---|
| Active configuration | Saved configuration |
| Stored in RAM | Stored in NVRAM on traditional Cisco IOS terminology |
| Changes immediately affect device | Used during boot |
| Can be lost after reload if not saved | Persists across reloads |
| `show running-config` | `show startup-config` |

Think:

```text
Running Config
     ↓
Current working configuration

Startup Config
     ↓
Saved configuration for next boot
```

---

# 💾 16. Saving Configuration

After making configuration changes, save them:

```text
Router# copy running-config startup-config
```

You may see:

```text
Destination filename [startup-config]?
```

Press:

```text
Enter
```

Other shortcuts you may encounter:

```text
Router# write memory
```

```text
Router# wr
```

For CCNA, understand and remember:

```text
copy running-config startup-config
```

---

# 🔄 17. Configuration Workflow

A typical workflow is:

```text
Connect to device
       ↓
User EXEC
       ↓
enable
       ↓
Privileged EXEC
       ↓
configure terminal
       ↓
Global Configuration
       ↓
Make changes
       ↓
end
       ↓
Privileged EXEC
       ↓
show running-config
       ↓
copy running-config startup-config
       ↓
Saved
```

---

# 🧪 18. Day 04 Basic Configuration Lab

Example lab objective:

Configure a Cisco device with:

- A hostname
- An enable secret
- Password encryption
- A saved configuration

### Step 1 — Enter Privileged EXEC

```text
Router> enable
```

### Step 2 — Enter Global Configuration

```text
Router# configure terminal
```

### Step 3 — Configure hostname

```text
Router(config)# hostname R1
```

Prompt becomes:

```text
R1(config)#
```

### Step 4 — Configure enable secret

```text
R1(config)# enable secret class
```

### Step 5 — Enable password encryption

```text
R1(config)# service password-encryption
```

### Step 6 — Exit configuration mode

```text
R1(config)# end
```

### Step 7 — Verify running configuration

```text
R1# show running-config
```

### Step 8 — Save configuration

```text
R1# copy running-config startup-config
```

Press Enter when asked for the destination filename.

---

# 🔎 19. Verification

After saving, verify:

```text
R1# show running-config
```

and:

```text
R1# show startup-config
```

The saved configuration should contain the configuration you intended to keep.

---

# 🧠 20. Important CCNA Concepts

### `enable`

Moves from:

```text
Router>
```

to:

```text
Router#
```

### `configure terminal`

Moves from:

```text
Router#
```

to:

```text
Router(config)#
```

### `end`

Returns from configuration mode to:

```text
Router#
```

### `disable`

Returns from:

```text
Router#
```

to:

```text
Router>
```

### `show running-config`

Displays the active configuration.

### `show startup-config`

Displays the saved configuration.

### `copy running-config startup-config`

Saves the active configuration.

---

# 🧩 21. Useful CLI Commands Learned

| Command | Purpose |
|---|---|
| `enable` | Enter Privileged EXEC |
| `disable` | Return to User EXEC |
| `configure terminal` | Enter Global Configuration |
| `end` | Return to Privileged EXEC |
| `exit` | Move back one configuration level |
| `hostname R1` | Change device hostname |
| `enable password X` | Configure enable password |
| `enable secret X` | Configure enable secret |
| `service password-encryption` | Obscure plaintext passwords in configuration |
| `show running-config` | Display active configuration |
| `show startup-config` | Display saved configuration |
| `copy running-config startup-config` | Save active configuration |

---

# 🧪 22. Recommended Packet Tracer Evidence

Add screenshots from your actual lab:


```text
lab/
└── day-04-cisco-cli.pkt
```



---

# 🧠 23. Common Mistakes

### Mistake 1 — Forgetting `enable`

If you are here:

```text
Router>
```

use:

```text
Router> enable
```

---

### Mistake 2 — Forgetting configuration mode

You cannot use global configuration commands from User EXEC.

Use:

```text
Router# configure terminal
```

---

### Mistake 3 — Not saving configuration

You configure the device:

```text
Router(config)# hostname R1
```

The change exists in the running configuration.

But if you do not save it and the device reloads, the change may be lost.

Save:

```text
R1# copy running-config startup-config
```

---

### Mistake 4 — Confusing running and startup configuration

Remember:

```text
Running = currently active

Startup = saved for boot
```

---

### Mistake 5 — Treating `service password-encryption` as strong password security

It obscures certain plaintext passwords in the configuration, but it is not equivalent to modern strong password hashing.

---

# 📚 24. Revision Questions

1. What does CLI stand for?
2. How can you initially connect to a Cisco device?
3. What does the `>` prompt mean?
4. What does the `#` prompt mean?
5. What does `(config)#` mean?
6. How do you enter Privileged EXEC mode?
7. How do you enter Global Configuration mode?
8. How do you return from Global Configuration to Privileged EXEC?
9. What does `enable password` do?
10. What does `enable secret` do?
11. Which should normally be preferred: `enable password` or `enable secret`?
12. What does `service password-encryption` do?
13. What is the running configuration?
14. What is the startup configuration?
15. Where is the running configuration stored?
16. Where is the startup configuration stored?
17. How do you display the running configuration?
18. How do you display the startup configuration?
19. How do you save running configuration to startup configuration?
20. What can happen if you configure a device but do not save the configuration?

---

# 📈 25. Day 04 Reflection

## What I Learned

- Cisco CLI
- Console access
- User EXEC mode
- Privileged EXEC mode
- Global Configuration mode
- CLI navigation
- `enable password`
- `enable secret`
- `service password-encryption`
- Running configuration
- Startup configuration
- Saving configurations

## What I Need to Practice

- Moving between CLI modes without hesitation
- Remembering the difference between `enable password` and `enable secret`
- Understanding when configuration changes affect the running configuration
- Remembering to save important configuration changes
- Reading `show running-config` and `show startup-config`

## Main Takeaway

> **A Cisco network engineer must be comfortable with the CLI and must understand the difference between the active running configuration and the saved startup configuration.**

---

# 🚀 Day 04 Status

**Completed ✅**

- [x] Cisco CLI
- [x] Connecting to a Cisco device
- [x] User EXEC mode
- [x] Privileged EXEC mode
- [x] Global Configuration mode
- [x] CLI navigation
- [x] Enable password
- [x] Enable secret
- [x] Service password encryption
- [x] Running configuration
- [x] Startup configuration
- [x] Saving configuration
- [x] Basic Packet Tracer configuration lab

---

**Next:** Day 05 — 
