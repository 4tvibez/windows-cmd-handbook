# Windows CMD Command Handbook

A practical beginner's guide to Windows Command Prompt (CMD). Each section explains what a command does, how to run it, and any important precautions.

> **How to use this guide:** Open Command Prompt, copy one command at a time, paste it, and press **Enter**. Read the notes first. A command may behave differently depending on your Windows edition, permissions, installed software, and hardware.

## Command safety labels

- **[SAFE CHECK]** Reads information or performs a diagnostic check.
- **[ADMIN]** May require opening CMD with **Run as administrator**.
- **[CHANGES SETTINGS]** Changes Windows or network settings.
- **[DESTRUCTIVE]** Can delete data or make the system unusable if misused. Do not run unless you understand the consequences.

## 1. Getting started and help

| Command | Purpose | How to use / expected result |
|---|---|---|
| `help` | Lists many CMD commands. | Type `help`; CMD displays command names and brief descriptions. |
| `command /?` | Shows help for a command. | Replace `command` with a command, e.g. `ipconfig /?`. |
| `cls` | Clears the CMD window. | Type it when you want a clean screen. |
| `exit` | Closes Command Prompt. | Saves no special state; closes the current CMD window. |
| `doskey /history` | Shows commands typed in the current CMD session. | Displays the session's command history. |
| `ver` | Shows Windows version information. | Prints a Windows version string. |
| `hostname` | Shows the computer name. | Prints the PC's network name. |
| `whoami` | Shows the signed-in account. | Prints the current user name. |

**Useful keyboard keys:** Up/Down arrows recall previous commands; **Tab** completes file and folder names; **Ctrl+C** interrupts many running commands.

## 2. PC and Windows information

| Command | Purpose | How to use / expected result |
|---|---|---|
| `systeminfo` | **[SAFE CHECK]** Displays a broad system summary. | Look for OS Name, OS Version, System Manufacturer, System Model, Processor, and Total Physical Memory. |
| `winver` | **[SAFE CHECK]** Opens the Windows version dialog. | A small window shows Windows edition/version and OS build. |
| `msinfo32` | **[SAFE CHECK]** Opens System Information. | Review System Summary for processor, memory, BIOS, and system type. |
| `dxdiag` | **[SAFE CHECK]** Opens DirectX Diagnostic Tool. | Check the System tab and Display/Render tabs for graphics details. |
| `driverquery` | **[SAFE CHECK]** Lists installed drivers. | CMD prints driver names and types. |
| `systempropertiesadvanced` | Opens Advanced System Properties. | Opens a Windows settings dialog. |

## 3. Processor (CPU)

Older Windows installations may support these WMIC commands. WMIC is deprecated and may not be installed on current Windows releases.

| Command | Purpose | How to use / expected result |
|---|---|---|
| `wmic cpu get name` | Shows CPU model. | Prints the processor name, if WMIC is available. |
| `wmic cpu get numberofcores` | Shows physical core count. | Prints the reported number of CPU cores. |
| `wmic cpu get numberoflogicalprocessors` | Shows logical processor count. | Prints logical processors/threads. |
| `wmic cpu get maxclockspeed` | Shows reported maximum clock speed. | Prints a value in MHz; actual speed varies with workload and power settings. |

**Alternative:** Run `msinfo32` and inspect **Processor**, or open Task Manager with `taskmgr`, choose **Performance**, then **CPU**.

## 4. Memory (RAM)

| Command | Purpose | How to use / expected result |
|---|---|---|
| `systeminfo` | Shows total and available physical memory. | Find **Total Physical Memory** and **Available Physical Memory**. |
| `wmic memorychip get capacity,speed,manufacturer` | Shows RAM module capacity, speed, and maker (if WMIC exists). | Each row represents a memory module. Capacity is shown in bytes. |
| `taskmgr` | Opens Task Manager. | Choose **Performance → Memory** to see installed RAM, speed, and slots used when available. |
| `resmon` | Opens Resource Monitor. | Select the Memory tab to inspect memory use. |

## 5. Graphics and display

| Command | Purpose | How to use / expected result |
|---|---|---|
| `dxdiag` | **[SAFE CHECK]** Shows graphics and DirectX details. | Open the Display and Render tabs, if present. |
| `start ms-settings:display` | Opens Display settings. | Review resolution, scaling, and available display options. |
| `taskmgr` | Opens Task Manager. | Choose **Performance → GPU** if Windows exposes GPU monitoring. |

## 6. Storage and drives

| Command | Purpose | How to use / expected result |
|---|---|---|
| `dir` | Lists files and folders in the current directory. | Type `dir` or `dir C:\` to list a location. |
| `tree` | Shows a folder tree. | Type `tree` in a folder. |
| `tree /f` | Shows folders and files in a tree. | Can produce a very long output in large folders. |
| `vol C:` | Shows the C: drive label and serial number. | Replace C: with another drive letter if needed. |
| `fsutil volume diskfree C:` | **[SAFE CHECK]** Reports free space on a volume. | Shows available and total bytes; may require elevated permissions on some systems. |
| `wmic diskdrive get model,size` | Shows disk model and reported size (if WMIC exists). | Size is reported in bytes. |
| `chkdsk C: /scan` | **[SAFE CHECK]** Scans the C: file system online. | Review the report for file-system errors. Run as administrator if requested. |
| `defrag C: /A` | **[SAFE CHECK]** Analyzes drive optimization status. | Reports whether optimization is recommended. Windows handles SSD optimization differently from HDD defragmentation. |
| `diskmgmt.msc` | Opens Disk Management. | Use the graphical tool to inspect partitions. Do not delete or format volumes casually. |

**DiskPart warning:** `diskpart` opens a powerful disk-management shell. Commands such as `clean`, `format`, and `delete` can destroy data. Do not run them as experiments. To leave DiskPart, type `exit`.

## 7. Internet and network troubleshooting

| Command | Purpose | How to use / expected result |
|---|---|---|
| `ipconfig` | Shows basic IP configuration. | Look for IPv4 Address, Subnet Mask, and Default Gateway. |
| `ipconfig /all` | Shows detailed adapter configuration. | Includes DNS servers, DHCP status, and adapter details. Avoid publicly sharing the full output because it can reveal network information. |
| `ping google.com` | Tests whether a host responds. | Replies show round-trip times. Some networks block ping, so timeouts do not always mean the internet is down. |
| `ping 8.8.8.8` | Tests connectivity to a public IP address. | Helps distinguish DNS problems from general connectivity issues. |
| `tracert google.com` | Shows network hops toward a host. | Some hops may time out because routers do not respond to traceroute probes. |
| `pathping google.com` | Combines route tracing and packet-loss analysis. | Takes longer than ping; review the final statistics. |
| `nslookup google.com` | Queries DNS for a domain. | Shows the DNS server and returned addresses. |
| `ipconfig /displaydns` | Displays cached DNS records. | Output can be lengthy. |
| `ipconfig /flushdns` | **[CHANGES SETTINGS]** Clears the local DNS resolver cache. | Use for certain DNS troubleshooting cases; it does not erase browser history. |
| `getmac` | Shows network adapter MAC addresses. | Lists physical addresses for network adapters. |
| `netstat -ano` | Shows network connections, listening ports, and process IDs. | Use Task Manager to identify a PID. Do not assume every connection is malicious. |
| `arp -a` | Shows the local ARP cache. | Lists IP-to-hardware-address mappings known to the PC. |
| `netsh wlan show interfaces` | Shows Wi-Fi connection details. | Includes SSID, signal, radio type, and connection state. |
| `netsh wlan show drivers` | Shows Wi-Fi driver capabilities. | Lists supported radio types and authentication options. |

### Network commands that change connectivity

- `ipconfig /release` — **[CHANGES SETTINGS]** Releases the DHCP IPv4 address for adapters.
- `ipconfig /renew` — **[CHANGES SETTINGS]** Requests a new DHCP IPv4 address.
- `netsh winsock reset` — **[ADMIN] [CHANGES SETTINGS]** Resets the Winsock catalog; a restart is generally required. Use only for relevant network troubleshooting.

## 8. Windows health and repair

These checks can take time. Connect a laptop to power before lengthy repairs. Open CMD as administrator when Windows requests it.

| Command | Purpose | How to use / expected result |
|---|---|---|
| `sfc /scannow` | **[ADMIN]** Scans protected Windows system files and repairs issues when possible. | Wait until verification reaches 100%; read the final message. |
| `DISM /Online /Cleanup-Image /CheckHealth` | **[ADMIN]** Checks whether the Windows image has already been flagged as damaged. | Quick health check; not a full scan. |
| `DISM /Online /Cleanup-Image /ScanHealth` | **[ADMIN]** Scans the Windows component store for corruption. | May take several minutes. |
| `DISM /Online /Cleanup-Image /RestoreHealth` | **[ADMIN]** Attempts to repair the Windows image. | May use Windows Update as a repair source and can take time. |
| `chkdsk C: /scan` | Scans the C: file system online. | Review any reported problems before considering further repair. |

A common repair sequence when Windows system-file corruption is suspected is to run DISM RestoreHealth first, then SFC. Do not run repair commands just for routine benchmarking.

## 9. Battery and power (laptops)

| Command | Purpose | How to use / expected result |
|---|---|---|
| `powercfg /batteryreport` | **[SAFE CHECK]** Creates a battery usage and capacity report. | CMD prints the saved HTML report path. Open that file in a browser. Compare Design Capacity with Full Charge Capacity. |
| `powercfg /energy` | Creates an energy efficiency diagnostic report. | Run for about 60 seconds; CMD prints the report path. |
| `powercfg /list` | Lists power schemes. | Shows available power plans. |
| `powercfg /getactivescheme` | Shows the active power scheme. | Prints the currently selected plan. |

## 10. Processes and performance monitoring

| Command | Purpose | How to use / expected result |
|---|---|---|
| `taskmgr` | Opens Task Manager. | Check CPU, Memory, Disk, Network, and GPU usage. |
| `tasklist` | Lists running processes. | Shows process names and process IDs. |
| `tasklist /svc` | Lists processes and associated services. | Useful for troubleshooting service-host processes. |
| `resmon` | Opens Resource Monitor. | Provides more detailed CPU, memory, disk, and network views. |
| `perfmon` | Opens Performance Monitor. | Allows detailed performance monitoring. |
| `perfmon /rel` | Opens Reliability Monitor on supported Windows versions. | Shows a timeline of application and Windows failures. |
| `winsat formal` | Runs Windows System Assessment Tool tests where supported. | Can take several minutes; results and availability vary by Windows version. |

## 11. Files and folders

Run these in a directory where you have permission to work.

| Command | Purpose | Example / expected result |
|---|---|---|
| `cd` | Shows current directory. | Prints the current path. |
| `cd ..` | Moves up one directory. | Goes to the parent folder. |
| `cd \\ ` | Moves to the root of the current drive. | Use `cd \\ ` without the extra space if copying: `cd \\ ` is not needed; simply type `cd \\ `. |
| `cd /d D:\Projects` | Changes drive and directory. | Moves to D:\Projects if it exists. |
| `mkdir MyProject` | Creates a directory. | Creates a folder named MyProject. |
| `rmdir EmptyFolder` | Removes an empty directory. | Fails if the folder is not empty. |
| `copy notes.txt D:\Backup\` | Copies a file. | Copies notes.txt to the destination folder. |
| `move notes.txt D:\Backup\` | Moves a file. | Moves the file to the destination folder. |
| `ren old.txt new.txt` | Renames a file. | Changes the filename in the current folder. |
| `type notes.txt` | Prints a text file's contents. | Displays the file in CMD. |
| `where notepad` | Finds an executable on PATH. | Prints the executable path if found. |
| `echo Hello` | Prints text. | Displays Hello. |
| `tree /f` | Displays a folder tree including files. | Can be very long; run inside a project folder. |

**Path tip:** Put quotation marks around paths containing spaces, e.g. `cd /d "C:\Users\Your Name\Documents"`.

## 12. Opening Windows tools and settings

| Command | Opens |
|---|---|
| `taskmgr` | Task Manager |
| `devmgmt.msc` | Device Manager |
| `diskmgmt.msc` | Disk Management |
| `services.msc` | Services |
| `eventvwr.msc` | Event Viewer |
| `compmgmt.msc` | Computer Management |
| `taskschd.msc` | Task Scheduler |
| `control` | Control Panel |
| `appwiz.cpl` | Programs and Features |
| `ncpa.cpl` | Network Connections |
| `mmsys.cpl` | Sound settings |
| `sysdm.cpl` | System Properties |
| `wf.msc` | Windows Defender Firewall with Advanced Security |
| `regedit` | Registry Editor |
| `start ms-settings:` | Windows Settings |
| `start explorer` | File Explorer |
| `start notepad` | Notepad |
| `start calc` | Calculator |
| `start mspaint` | Paint |

Some tools are not included in every Windows edition. Registry Editor and advanced management tools should be used carefully.

## 13. Developer tools

These commands work only if the relevant software is installed and available on PATH.

| Command | Purpose | Expected result |
|---|---|---|
| `git --version` | Checks Git installation. | Prints Git version. |
| `node -v` | Checks Node.js. | Prints Node.js version. |
| `npm -v` | Checks npm. | Prints npm version. |
| `python --version` | Checks Python. | Prints Python version if the launcher command is configured. |
| `py --version` | Checks Windows Python launcher. | Prints Python version if installed. |
| `code .` | Opens current folder in VS Code. | Requires VS Code and its command-line PATH entry. |
| `where git` | Finds Git executable. | Prints its path if available. |
| `where node` | Finds Node.js executable. | Prints its path if available. |
| `where python` | Finds Python executable. | Prints its path if available. |
| `winget list` | Lists installed packages known to Windows Package Manager. | Shows app names and versions where available. |
| `winget upgrade` | Checks for available package upgrades. | Lists packages with available upgrades; it does not install them by itself. |
| `npm init -y` | Creates a default package.json. | Run inside a project folder; creates a Node project manifest. |
| `npm install` | Installs project dependencies. | Run in a folder with package.json. |
| `npm run` | Lists available npm scripts. | Shows scripts configured in package.json. |
| `npm run dev` | Runs the project's dev script. | Works only if a dev script exists. |
| `git status` | Shows Git working-tree status. | Run inside a Git repository. |
| `git init` | Initializes a Git repository. | Creates a .git folder in the current directory. |
| `git clone REPOSITORY_URL` | Clones a repository. | Replace the placeholder with a real repository URL. |

## 14. User accounts and security information

| Command | Purpose | Notes |
|---|---|---|
| `whoami /all` | Shows current user's groups and privileges. | **[SAFE CHECK]** Avoid sharing the output publicly. |
| `net user` | Lists local user accounts. | **[SAFE CHECK]** |
| `net accounts` | Shows local account policy information. | **[SAFE CHECK]** |
| `manage-bde -status` | Shows BitLocker drive-encryption status. | **[SAFE CHECK]** May require administrator permissions. |
| `mrt` | Opens Microsoft's Malicious Software Removal Tool if available. | Use Windows Security for full security management. |
| `eventvwr` | Opens Windows Event Viewer. | Review system and application events. |

## 15. Shutdown, restart, and sign-out

**[CHANGES SETTINGS / ACTIONS]** Save your work before using these commands.

| Command | Purpose | Notes |
|---|---|---|
| `shutdown /s` | Shuts down Windows. | Closes the session and powers off. |
| `shutdown /r` | Restarts Windows. | Closes the session and restarts. |
| `shutdown /l` | Signs out the current user. | Closes the current session. |
| `shutdown /a` | Aborts a pending timed shutdown. | Only works while a shutdown countdown is active. |
| `shutdown /s /t 60` | Schedules shutdown in 60 seconds. | Save work first; cancel with `shutdown /a` if needed. |

## 16. Beginner practice exercises

Try these in order:

1. Type `hostname` and write down your computer name.
2. Type `systeminfo` and find your Windows version and total physical memory.
3. Type `ipconfig` and find your IPv4 address.
4. Type `ping google.com` and observe whether replies arrive.
5. Type `mkdir CMD-Practice` to create a practice folder.
6. Type `cd CMD-Practice` to enter it.
7. Type `echo Hello from CMD > hello.txt` to create a text file.
8. Type `type hello.txt` to display its contents.
9. Type `dir` to list the file.
10. Type `cd ..` to return to the parent directory.

## 17. Quick diagnostic checklist

Copy and run these **one at a time**:

```cmd
systeminfo
hostname
winver
msinfo32
dxdiag
taskmgr
ipconfig /all
ping google.com
nslookup google.com
driverquery
chkdsk C: /scan
```

For a laptop, also try:

```cmd
powercfg /batteryreport
```

## 18. Important reminders

- Do not paste a whole list of commands into CMD without understanding what each one does.
- Avoid commands that promise to speed up Windows by deleting unknown files or changing the registry.
- Never share passwords, product keys, full network configuration, or sensitive diagnostic output publicly.
- Do not experiment with DiskPart commands that format, clean, or delete partitions.
- A ping timeout does not always mean your internet connection is broken.
- WMIC is deprecated; use Task Manager, System Information, or PowerShell alternatives when it is unavailable.
- Create a backup before significant system repairs or disk operations.

---

**Made for beginners learning Windows, computer maintenance, and software development.**
