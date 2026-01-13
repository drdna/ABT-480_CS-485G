# ABT-480_CS-485G
**Applied Bioinformatics Class Materials**

---

## Module 1 – Part I: Essential Unix/Linux

---

### 1.1 Getting Connected and Reconnected

The steps for connecting to your virtual machine (VM) differ depending on your operating system. Follow the instructions for your system.

#### 1.1.1 On a PC

Two methods for connecting from a PC: **OpenSSH/PowerShell** and **PuTTY**. Only one is needed.

- **OpenSSH**: No additional installation required on modern Windows.
- **PuTTY**: Requires installation, may be more user-friendly.

##### OpenSSH/PowerShell

Open PowerShell and connect to your VM (replace `myName` and `XX.XXX.XXX.XX`):

```bash
ssh myName@XX.XXX.XXX.XX
```

Enter your password when prompted. After login, the prompt looks like:

```bash
myName@ip-XXX-XX-XX-XXX:~$
```

To logout:

```bash
exit
```

#### 1.1.2 On a Mac

Open Terminal (Applications → Utilities) and connect:

```bash
ssh myName@XX.XXX.XXX.XX
```

Enter your password. After login, the prompt looks like:

```bash
myName@ip-XXX-XX-XX-XXX:~$
```

To logout:

```bash
exit
```

---

### 1.2 Exploring and Learning Basic Commands

```bash
pwd
ls
mkdir unix
cd unix
mkdir example
touch myFile.txt
ls -l
man ls
```

Example output of `ls -l`:

```text
total 4
drwxrwxr-x 2 ngsadmin ngsadmin 4096 Jul 26 22:06 example
-rw-rw-r-- 1 ngsadmin ngsadmin 0 Jul 26 22:06 myFile.txt
```

---

### 1.3 "There's No Place Like Home"

```bash
cd /home/myName
cd unix/example
cd ..
cd ..
cd ~
```

---

### 1.4 Using Command History

```bash
history
```

Use up/down arrows to navigate previous commands.

---

### 1.5 Tab Completion

Press **Tab** to auto-complete file/directory names. Double-tab shows all matches.

---

### 1.6 Learning a Text Editor (nano)

```bash
nano example/name.txt
```

Save: `Ctrl+O` then Enter  
Exit: `Ctrl+X`  

View contents:

```bash
cat example/name.txt
less example/name.txt
more example/name.txt
```

---

### 1.7 Using SCP to Transfer Files

```bash
scp example/name.txt myName@XX.XXX.XXX.XX:~/Desktop/myName.txt
scp myName@XX.XXX.XXX.XX:~/Desktop/NGS-message.txt .
```

---

### 1.8 Transfer from VM to Local Machine

```bash
ls blast
scp myName@XX.XXX.XXX.XX:~/unix/blast/MoRepeats.fasta .
ls
```

Open files via Explorer/Finder.

---

### 1.9 Downloading Data from the Internet

```bash
wget https://ftp.ncbi.nlm.nih.gov/genomes/all/GCF/000/146/045/GCF_000146045.2_R64/GCF_000146045.2_R64_genomic.fna.gz -O yeast.nt.gz
head example/yeast.nt.gz
gunzip example/yeast.nt.gz
head example/yeast.nt
```

---

### 1.10 Copying and Moving Files

```bash
cp example/yeast.nt example/yeast_copy.nt
mv example/yeast_copy.nt extra/
mv extra/yeast_copy.nt example/yeast_backup.nt
```

---

### 1.11 Renaming Files

```bash
mv example/yeast_backup.nt example/yeast_copy.fasta
```

---

### 1.12 Removing Files and Directories

```bash
rm example/yeast_copy.fasta
rm -r extra2
```

---

### 1.13 Redirection

```bash
head example/yeast.nt > example/output.txt
cat example/output.txt
```

---

### 1.14 grep

```bash
grep '>' example/yeast.nt
grep '>' example/yeast.nt > example/seqHeaderLines.txt
grep -c '>' example/yeast.nt
```

---

### 1.15 Pipes

```bash
grep '>' example/yeast.nt | head -n 5
grep '>' example/yeast.nt | wc -l
```

---

### 1.16 awk

```bash
grep '>' example/yeast.nt | awk '{print $1}'
grep '>' example/yeast.nt | awk '{print $2}'
grep '>' example/yeast.nt | awk '{print length($0)}'
grep '>' example/yeast.nt | awk '{print substr($1,1,10)}'
```

---

### 1.17 sed

```bash
grep '>' example/yeast.nt | sed 's/>NC_//g'
```
