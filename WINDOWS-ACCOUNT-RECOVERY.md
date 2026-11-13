# Windows 10 User Account Recovery and Password Help

A beginner-friendly guide for helping a computer owner regain access to a Windows 10 PC. Use these steps only with the owner's permission. The goal is to restore legitimate access while protecting personal files.

## Before doing anything

1. Confirm that the person is the PC owner or is authorized to request help.
2. Ask whether the sign-in uses an email address (usually a Microsoft account) or a local username.
3. Ask whether important files are backed up.
4. Check whether BitLocker/device encryption is enabled. Recovery may require the owner's recovery key.
5. Do not guess passwords, use another person's credentials, or try to bypass authentication.

## 1. Identify the account type

- **Microsoft account:** The sign-in screen usually shows an email address. Reset the password using Microsoft's official page: https://account.live.com/password/reset
- **Local account:** The sign-in screen usually shows a local username. Use the **Reset password** link and security questions if they were configured.
- **Work or school account:** Contact the organization's IT administrator; its password policy may be centrally managed.

## 2. Recovery options for a local account

Use these in order:

1. On the sign-in screen, choose **Reset password** and answer the security questions, if offered.
2. If the owner previously created a password reset disk, connect it and follow the Password Reset Wizard.
3. If another administrator account is available on the same PC, the owner or authorized administrator can sign in and use Windows account-management settings to reset the affected local account.
4. If none of these options works, review Microsoft's **Reset this PC** recovery options. Back up files first whenever possible. **Keep my files** is intended to preserve personal files but removes apps and settings; it is not a substitute for a backup. **Remove everything** erases personal files.

Microsoft's Windows recovery guidance: https://support.microsoft.com/windows/recovery-options-in-windows

## 3. Useful CMD commands when you can sign in

Open Command Prompt. These commands inspect accounts; they do not reveal passwords or unlock a forgotten account.

| Command | What it does | Safety |
|---|---|---|
| `whoami` | Shows the account currently signed in. | [SAFE CHECK] |
| `whoami /all` | Shows the current account's groups and privileges. | [SAFE CHECK] Avoid sharing output publicly. |
| `net user` | Lists local user accounts. | [SAFE CHECK] |
| `net user "%username%"` | Shows information about the current local account. | [SAFE CHECK] |
| `net accounts` | Shows local password and account policy settings. | [SAFE CHECK] |
| `net localgroup administrators` | Lists members of the local Administrators group. | [SAFE CHECK] |

### Changing a local account password (authorized administrator only)

If the owner can sign in to an administrator account and has authorized the change, an administrator can use:

```cmd
net user "ACCOUNT_NAME" *
```

Replace `ACCOUNT_NAME` with the exact local username. Windows prompts for a new password without displaying the characters as you type. Run Command Prompt as administrator if required.

**Important:** This is for changing a known local account's password with administrator authorization. It is not a way to recover a Microsoft account password. Resetting another local account's password can cause loss of access to some EFS-encrypted files, personal certificates, and stored credentials. Prefer the account's own recovery questions or password reset disk when available. Never change a user's password without their permission.

## 4. If the PC is locked and no one can sign in

CMD commands such as `whoami` and `net user` cannot be run from the normal sign-in screen to reveal or recover a forgotten password.

Do not use online "password bypass" scripts or untrusted boot tools. They can damage Windows, expose private data, or defeat security protections.

Instead:
- Microsoft account: use Microsoft's online password reset, then connect the PC to the internet and sign in.
- Local account: use security questions or the reset disk.
- Managed work/school PC: contact the organization's IT administrator.
- No recovery method: use official Windows Recovery options after considering backups, BitLocker recovery, and the risk of losing apps or data.

## 5. Technician checklist

- [ ] Confirm owner permission and identity.
- [ ] Identify Microsoft, local, or work/school account.
- [ ] Ask about backups and important encrypted files.
- [ ] Check for BitLocker and make sure the owner has the recovery key if needed.
- [ ] Try the account's official recovery method first.
- [ ] Explain data-loss risks before resetting Windows.
- [ ] Confirm the owner can sign in and can access their files afterward.
- [ ] Encourage the owner to create a password reset disk for a local account and keep recovery information somewhere secure.

## Practice questions

1. Does `net user` show a user's actual password? **No.** It lists local accounts.
2. Can `whoami` recover a forgotten password? **No.** It identifies the signed-in account.
3. What should you try first for a Microsoft account? **Microsoft's official password reset process.**
4. Why should you check backups before Reset this PC? **Some reset choices remove personal files, apps, and settings.**
5. Should a technician reset someone else's password without permission? **No.**

---

**Learning goal:** Diagnose Windows sign-in problems, use official account recovery, and protect the computer owner's data.
