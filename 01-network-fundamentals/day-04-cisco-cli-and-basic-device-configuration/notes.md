# Day 04 Notes — Cisco CLI & Basic Device Configuration

## CCNA 200-301 v1.1

---

# 1. Cisco CLI

**CLI = Command-Line Interface**

Cisco IOS devices can be configured and monitored using commands.

Example:

```text
show ip interface brief
```

The CLI is one of the main tools used by network engineers.

---

# 2. Connecting to a Cisco Device

Initial access can be provided through the **console** connection.

```text
PC
 |
 | Console cable
 v
Cisco Router/Switch
```

Packet Tracer workflow:

```text
1. Connect console cable
2. Open PC
3. Open Terminal
4. Accept terminal settings
5. Press Enter if necessary
6. Access Cisco CLI
```

Console access does not require a working network connection.

---

# 3. Cisco CLI Modes

Main modes:

```text
User EXEC
    ↓
Privileged EXEC
    ↓
Global Configuration
```

## User EXEC

Prompt:

```text
Router>
```

Enter Privileged EXEC:

```text
Router> enable
```

## Privileged EXEC

Prompt:

```text
Router#
```

Enter Global Configuration:

```text
Router# configure terminal
```

## Global Configuration

Prompt:

```text
Router(config)#
```

Used for global configuration.

---

# 4. Mode Navigation

```text
Router>
   |
   | enable
   ↓
Router#
   |
   | configure terminal
   ↓
Router(config)#
```

Return to Privileged EXEC:

```text
Router(config)# end
```

Return one level:

```text
Router(config)# exit
```

Return from Privileged EXEC to User EXEC:

```text
Router# disable
```

---

# 5. Prompt Cheat Sheet

| Prompt | Mode |
|---|---|
| `Router>` | User EXEC |
| `Router#` | Privileged EXEC |
| `Router(config)#` | Global Configuration |

Remember:

```text
>         = User EXEC

#         = Privileged EXEC

(config)# = Global Configuration
```

---

# 6. Enable Password

Command:

```text
Router(config)# enable password cisco
```

Purpose:

> Protect entry into Privileged EXEC mode.

It is an older/less preferred method.

---

# 7. Enable Secret

Command:

```text
Router(config)# enable secret MySecret
```

Purpose:

> Protect entry into Privileged EXEC mode using a stronger password protection mechanism.

Preferred over:

```text
enable password
```

If both are configured, `enable secret` takes precedence for Privileged EXEC authentication.

---

# 8. Service Password Encryption

Command:

```text
Router(config)# service password-encryption
```

Purpose:

> Obscure certain plaintext passwords in the configuration.

Important:

```text
service password-encryption
≠
strong modern password hashing
```

It is mainly useful for preventing passwords from appearing plainly in configuration output.

---

# 9. Running Configuration

Running configuration:

> The configuration currently active on the device.

Command:

```text
show running-config
```

Short form:

```text
show run
```

Think:

```text
RUNNING = CURRENT
```

---

# 10. Startup Configuration

Startup configuration:

> The saved configuration used when the device boots.

Command:

```text
show startup-config
```

Short form:

```text
show start
```

Think:

```text
STARTUP = SAVED
```

---

# 11. Running vs Startup

| Running | Startup |
|---|---|
| Current | Saved |
| Active | Used at boot |
| RAM | NVRAM on traditional Cisco IOS |
| Changes immediately apply | Persists across reload |
| `show running-config` | `show startup-config` |

---

# 12. Saving Configuration

Command:

```text
copy running-config startup-config
```

When prompted:

```text
Destination filename [startup-config]?
```

Press:

```text
Enter
```

Other historical shortcuts:

```text
write memory
wr
```

Know the full command for CCNA:

```text
copy running-config startup-config
```

---

# 13. Basic Configuration Workflow

```text
Router>
  ↓
enable
  ↓
Router#
  ↓
configure terminal
  ↓
Router(config)#
  ↓
Make configuration changes
  ↓
end
  ↓
Router#
  ↓
show running-config
  ↓
copy running-config startup-config
```

---

# 14. Basic Lab Configuration

Example:

```text
Router> enable
Router# configure terminal
Router(config)# hostname R1
R1(config)# enable secret class
R1(config)# service password-encryption
R1(config)# end
R1# show running-config
R1# copy running-config startup-config
```

Verify:

```text
R1# show startup-config
```

---

# 15. Important Concept

If you make a configuration change:

```text
Router(config)# hostname R1
```

the change is immediately part of:

```text
running-config
```

It is not automatically saved to:

```text
startup-config
```

Save it:

```text
R1# copy running-config startup-config
```

---

# 16. Troubleshooting Mindset

Always ask:

> **What mode am I in?**

Look at the prompt.

```text
Router>
```

→ User EXEC

```text
Router#
```

→ Privileged EXEC

```text
Router(config)#
```

→ Global Configuration

This simple habit prevents many CLI errors.

---

# 17. CCNA Memory Points

```text
> = User EXEC

# = Privileged EXEC

(config)# = Global Configuration

enable
→ enter Privileged EXEC

configure terminal
→ enter Global Configuration

end
→ return to Privileged EXEC

show running-config
→ current configuration

show startup-config
→ saved configuration

copy running-config startup-config
→ save current configuration

enable secret
→ preferred privileged-mode password

service password-encryption
→ obscure certain plaintext passwords
```

---

# 18. Quick Self-Test

### Q1. You see `R1>`. What mode?

**Answer:** User EXEC.

### Q2. How do you reach `R1#`?

```text
enable
```

### Q3. How do you reach `R1(config)#`?

```text
configure terminal
```

### Q4. Which configuration is currently active?

```text
running-config
```

### Q5. Which configuration is loaded at boot?

```text
startup-config
```

### Q6. How do you save running configuration?

```text
copy running-config startup-config
```

### Q7. Which is preferred for Privileged EXEC protection?

```text
enable secret
```

---

# 19. Final Summary

The key Day 04 flow:

```text
User EXEC
    ↓ enable
Privileged EXEC
    ↓ configure terminal
Global Configuration
```

And:

```text
Running Config
    ↓ save
Startup Config
```

Remember:

> **Running configuration = what the device is using now.**

> **Startup configuration = what the device will use after boot.**
