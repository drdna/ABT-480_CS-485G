# ABT-480_CS-485G
Applied Bioinformatics Class Materials

## 1.1 Getting connected and reconnected

The steps for connecting to your virtual machine (VM) differ depending on your operating system. Follow the instructions below for your system.

---

## 1.1.1 On a PC

The instructions below describe two methods for connecting to your VM from a PC:

- **OpenSSH / PowerShell**
- **PuTTY**

You only need to follow **one** method.

- OpenSSH requires no additional installation on recent versions of Windows.
- PuTTY requires installation but may be more user-friendly.

---

### OpenSSH / PowerShell

1. Open **PowerShell**.

2. Use the OpenSSH client `ssh` (secure shell) to connect to your VM.  
   Type the command below, replacing `myName` and the `Xs` with the credentials you received via email:

   ```bash
   ssh myName@XX.XXX.XXX.XX
