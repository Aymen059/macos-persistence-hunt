# MacOs-persistence-hunt
A project demonstrating macOS persistence using LaunchAgents, detection techniques, and cleanup.

# Objective
Demonstrate a real-world macOS persistence technique using a LaunchAgent .plist to auto-launch an app at user login.

# What This Shows
- How attackers achieve persistence without root access

- How to simulate and detect LaunchAgents

- How to clean and audit persistence mechanisms

# Tools Used
- macOS Terminal

- launchctl

- nano, grep, log

- osascript (for login item enumeration)


# Step-by-Step Execution
**STEP 1: Create the LaunchAgents Directory (if it doesn’t exist)**<img width="1012" alt="Screenshot 2025-05-10 at 11 09 37 AM" src="https://github.com/user-attachments/assets/63f91e54-5bda-4ac1-a54f-a93f274e640a" />

**Breakdown:**
- mkdir: stands for “make directory.”

- -p: means “create parent directories if they don’t exist.”

- ~/Library/LaunchAgents: is the folder where user-specific launch agents are stored.


# STEP 2: Create a .plist File
<img width="1012" alt="Screenshot 2025-05-10 at 11 14 14 AM" src="https://github.com/user-attachments/assets/a6d7fcd8-f914-4d62-abb1-dc72989d921e" />
**Breakdown:**

- nano: is a text editor inside the terminal.

- I created a file called com.aymen.noteslauncher.plist.

**CONTENT OF THE .plist FILE**
<img width="1012" alt="Screenshot 2025-05-10 at 11 13 51 AM" src="https://github.com/user-attachments/assets/565746a7-2d6a-49f3-9b64-837ef672446c" />

This file makes macOS automatically open Notes.app every time my user logs in, without needing root or prompting me.

# STEP 3: Load the Agent
<img width="1012" alt="Screenshot 2025-05-10 at 11 15 30 AM" src="https://github.com/user-attachments/assets/eec6bea9-ff85-4c26-8d2c-74e6d3ff23ad" />
**Breakdown:**
- launchctl: is the macOS service that manages launch agents/daemons.

- load: registers the .plist file with the system.

- The file gets loaded for the current user session.

- Even though I've loaded it, it won't open the notes app until I log out and log back into my user.

# STEP 4: Log Out and Log Back In
<img width="950" alt="Screenshot 2025-05-10 at 11 17 30 AM" src="https://github.com/user-attachments/assets/e3076dfd-906f-4190-b802-7e3cc955385a" />

- Even though it’s hard to demonstrate visually here, this LaunchAgent successfully achieves persistence: every time I log out and log back into my macOS user account, the Notes app automatically launches — even if I had previously quit it. This behavior proves that the system is executing the agent at login, exactly as configured.

- This is the same technique that real-world malware and advanced attackers use to maintain access after a reboot or logoff, without requiring root privileges. By leveraging native macOS features like LaunchAgents and launchctl, attackers can stay hidden in plain sight — unless defenders know exactly where and how to look.

- In this project, I’ve simulated that behavior safely, and demonstrated my ability to both deploy and detect such persistence mechanisms, giving me experience on both sides of the attack-defense equation.


# STEP 5
<img width="950" alt="Screenshot 2025-05-10 at 11 29 08 AM" src="https://github.com/user-attachments/assets/c780bc7e-7ff7-471c-9ac9-0a49884571d3" />

**Breakdown:**

unload: tells the system to stop using that LaunchAgent

rm: deletes the .plist file from disk










