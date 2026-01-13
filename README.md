# ABT-480_CS-485G
Applied Bioinformatics Class Materials

```markdown
Module 1
Part I: Essential Unix/Linux
1.1 Getting connected and reconnected
The steps for connecting to your virtual machine (VM) will differ depending on what operating system you are running. Follow the steps in the subsection below that corresponds to your system.
On a PC
The instructions below describe two methods of connecting to your VM from a PC—OpenSSH/PowerShell and PuTTY. You only need to follow the instructions for one method.
OpenSSH requires no additional installation on computers running the latest version of Windows.
PuTTY requires installation but may be more user-friendly.
OpenSSH/PowerShell
Open the PowerShell program. You can use the OpenSSH client ssh (secure shell) to connect to your virtual machine:
Let’s try and connect. Type the command below into PowerShell, changing myName and Xs to match the credentials you received via email. myName should match the username you received, and Xs should match the hostname you received. When you have finished typing the command, hit enter to run it.
```bash
ssh myName@XX.XXX.XXX.XX
```
You will be prompted for a password; type the password we sent you in the email. When you start typing your password, nothing will appear, but ssh is reading the characters. Hit enter when done.
After successfully logging in, you should see a prompt similar to:
```bash
myName@ip-XXX-XX-XX-XXX:~$
```
To logout from your VM, just type:
```bash
exit
```
Try logging in again. We will assume that you can do this step in future classes without issue.
PuTTY
PuTTY is a free telnet/SSH client for Windows that predates the native Windows OpenSSH client. Although it is not necessary to install a separate SSH client for this workshop, you may prefer PuTTY for its user-friendly interface. You can download PuTTY from here.
Download and install PuTTY.
Open PuTTY (find it in the Start menu).
Enter the hostname for your VM into the “Host Name (or IP address)” box. Example:
```text
myName@XX.XXX.XXX.XX
```
Leave the default port 22 unchanged.
Click Open to connect to your VM.
Enter your username and password when prompted.
After logging in, you should see a prompt like:
```bash
myName@ip-XXX-XX-XX-XXX:~$
```
To exit PuTTY, type:
```bash
exit
```
1.1.2 On a Mac
If you are working on a Mac, open the Terminal program (found in Applications → Utilities). Use the ssh command to connect to your VM:
```bash
ssh myName@XX.XXX.XXX.XX
```
Enter your password when prompted.
After successfully logging in, you should see a prompt similar to:
```bash
myName@ip-XXX-XX-XX-XXX:~$
```
To logout from your VM, type:
```bash
exit
```
1.2 Exploring and learning basic commands
Display your working directory:
```bash
pwd
```
List the current directory contents:
```bash
ls
```
Example output:
```text
assembly blast genes qiime2 rnaseq sequences variants
```
Create a new directory called unix:
```bash
mkdir unix
```
Change into the new directory:
```bash
cd unix
```
Create a subdirectory called example:
```bash
mkdir example
```
Create an empty file:
```bash
touch myFile.txt
```
Perform a long directory listing:
```bash
ls -l
```
Example output:
```text
total 4
drwxrwxr-x 2 ngsadmin ngsadmin 4096 Jul 26 22:06 example
-rw-rw-r-- 1 ngsadmin ngsadmin 0 Jul 26 22:06 myFile.txt
```
Show the manual for ls:
```bash
man ls
```
1.3 “There's no place like home”
Absolute path example:
```bash
cd /home/myName
```
Relative path example:
```bash
cd unix/example
```
Move back up:
```bash
cd ..
cd ..
```
Go directly home:
```bash
cd ~
```
1.4 Improving productivity – using your command history
Use up and down arrow keys to navigate previous commands.
View full command history:
```bash
history
```
1.5 Minimizing errors with tab completion
Use tab to auto-complete file and directory names.
Double-tab shows all possibilities if multiple matches exist.
1.6 Learning a text editor (nano)
Create and edit a file:
```bash
nano example/name.txt
```
Save the file: ^O (Ctrl+O), then Enter.
Exit nano: ^X (Ctrl+X).
View contents:
```bash
cat example/name.txt
```
For paging through files:
```bash
less example/name.txt
more example/name.txt
```
1.7 Using SCP to transfer files between machines
Send a file to the Admin VM:
```bash
scp example/name.txt myName@XX.XXX.XXX.XX:~/Desktop/myName.txt
```
Fetch a file from the Admin VM:
```bash
scp myName@XX.XXX.XXX.XX:~/Desktop/NGS-message.txt .
```
1.8 Transferring files from a remote VM to your local machine
List the file to check location:
```bash
ls blast
```
Copy from VM to local machine:
```bash
scp myName@XX.XXX.XXX.XX:~/unix/blast/MoRepeats.fasta .
```
Confirm transfer:
```bash
ls
```
Open files on PC or Mac via File Explorer or Finder.
1.9 Downloading data from the internet
Download via wget:
```bash
wget https://ftp.ncbi.nlm.nih.gov/genomes/all/GCF/000/146/045/GCF_000146045.2_R64/GCF_000146045.2_R64_genomic.fna.gz -O yeast.nt.gz
```
Peek at contents:
```bash
head example/yeast.nt.gz
```
Decompress:
```bash
gunzip example/yeast.nt.gz
```
Check contents:
```bash
head example/yeast.nt
```
1.10 Copying and moving files
Copy a file:
```bash
cp example/yeast.nt example/yeast_copy.nt
```
Move and rename:
```bash
mv example/yeast_copy.nt extra/
mv extra/yeast_copy.nt example/yeast_backup.nt
```
1.11 Renaming files and directories
Rename using mv:
```bash
mv example/yeast_backup.nt example/yeast_copy.fasta
```
1.12 Removing files and directories
Remove a file:
```bash
rm example/yeast_copy.fasta
```
Remove a directory:
```bash
rm -r extra2
```
1.13 Redirection
Redirect command output:
```bash
head example/yeast.nt > example/output.txt
cat example/output.txt
```
1.14 grep
Search for pattern:
```bash
grep '>' example/yeast.nt
```
Redirect grep output:
```bash
grep '>' example/yeast.nt > example/seqHeaderLines.txt
```
Count matches:
```bash
grep -c '>' example/yeast.nt
```
1.15 Pipes
Use a pipe to limit output:
```bash
grep '>' example/yeast.nt | head -n 5
grep '>' example/yeast.nt | wc -l
```
1.16 awk
Print first column of sequence headers:
```bash
grep '>' example/yeast.nt | awk '{print $1}'
```
Print second column:
```bash
grep '>' example/yeast.nt | awk '{print $2}'
```
Get line length:
```bash
grep '>' example/yeast.nt | awk '{print length($0)}'
```
Substring example:
```bash
grep '>' example/yeast.nt | awk '{print substr($1,1,10)}'
```
1.17 sed
Substitute pattern:
```bash
grep '>' example/yeast.nt | sed 's/>NC_//g'
```
```
