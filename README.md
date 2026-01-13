# ABT-480_CS-485G
**Applied Bioinformatics Class Materials**

---

<details>
<summary><strong><strong>Module 1 – Part I: Essential Unix/Linux</strong></strong></summary>

---

### 1.1 Getting Connected and Reconnected

The steps for connecting to your virtual machine (VM) differ depending on your operating system. Follow the instructions for your system.

#### 1.1.1 On a PC

##### PowerShell

Open PowerShell and connect to your VM (replace `myName` and `XX.XXX.XXX.XX`):

```bash
ssh myName@
```

Enter your password when prompted. After login, the prompt looks like:

```bash
myName@myName.cs.uky.edu:~$
```

To logout:

```bash
exit
```

#### 1.1.2 On a Mac

Open Terminal (Applications → Utilities) and connect:

```bash
ssh myName@myName.cs.uky.edu
```

Enter your password. After login, the prompt looks like:

```bash
myName@myName.cs.uky.edu:~$
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
</details>

---

<details>
<summary><strong><strong>Advanced Command Line Tools</strong></strong></summary>

## Automating Repetitive Tasks Using a Bash/Powershell Profile

### On a Mac

Ensure you are using the bash shell:

1. Open Terminal
2. Go to Terminal → Settings
3. Under General, select Shells open with → Command and add the following:

```bash
/bin/bash
```

4. Close Settings
5. Exit Terminal and restart it
6. While in your home directory, open/create a file named `.bash_profile`:

```bash
nano .bash_profile
```

7. Edit the file to contain the following lines:

```bash
# aliases
alias myVM="ssh myName@myName.cs.uky.edu"
```
*(Replace `myName` with your LinkBlue ID)*

8. Close the file (Ctrl+X) and save it under the original name (`.bash_profile`)
9. Activate the file using:

```bash
source .bash_profile
```

10. Connect to your VM with the alias you just created:

```bash
myVM
```

---

### On a PC

1. Open a PowerShell terminal
2. Create a profile file:

```powershell
New-Item $profile -Type File
```

3. Open the profile file in Notepad:

```powershell
notepad $profile
```

4. Add the following text:

```powershell
function connectToVM {
    ssh myName@myName.cs.uky.edu
}

Set-Alias myVM connectToVM
```
*(Replace `myName` with your LinkBlue ID)*

5. Save the file and refresh the session:

```powershell
. $profile
```

6. Connect to your VM:

```powershell
myVM
```

---

## Advanced Searching with `grep`

1. Search for lines containing the pattern in any case (`-i`):

```bash
grep -i t example/yeast.nt
```

2. Search for either/or pattern:

```bash
grep 'V\|X' example/yeast.nt
```

3. Search for lines containing any of a set of characters:

```bash
grep [AGTC5] example/yeast.nt
```

4. Search for lines starting or ending with a character/word:

```bash
# Lines starting with 'GATC'
grep ^GATC example/yeast.nt

# Lines ending with 'GATC'
grep GATC$ example/yeast.nt
```

5. Search for lines containing words from a separate file:

```bash
grep -f list_of_words.txt example/yeast.nt
```

6. Return only the matching characters/words:

```bash
grep -o [AGTCagtc] example/yeast.nt
```

---

## Working with Bash Variables

Assigning variables and using them is a key part of advanced scripting:

```bash
myVariable='Something I want to work on later'
```

1. Check the variable's value:

```bash
echo $myVariable
```

2. Perform substitution (e.g., change "Some" → "Any"):

```bash
echo ${myVariable/Some/Any}
```

3. Save the modified value as a new variable:

```bash
myNewVariable=${myVariable/Some/Any}
echo $myNewVariable
```

4. Save the output of a function as a variable:

```bash
firstLine=$(head -1 example/yeast.nt)
echo $firstLine
```

5. Incorporate variable assignment/substitution into a pipeline:

```bash
for jan16files in $(ls -l | awk '$6 == "Jan" && $7 == 16 {print $9}'); do
    echo cp $jan16files ${jan16files}_backup
done
```

---
</details>
