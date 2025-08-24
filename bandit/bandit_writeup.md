# BANDIT

## Level 0 → Level 1
**Username:** bandit0
**Password:** bandit0

Log into the machine using "bandit" as both the username and password. Once logged in, you'll find a file called `readme` in the home directory. This file contains the password for bandit1.

**Solution:**
```bash
ssh bandit0@bandit.labs.overthewire.org -p 2220
cat readme
```
## Level 1 → Level 2
**Password:** ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If

The challenge here involves reading a file named `-`. Using `cat -` directly won't work because the shell interprets `-` as stdin. Instead, use the file path: `cat ./-` to read the file and obtain the password for bandit2.

**Solution:**
```bash
cat ./-
```

## Level 2 → Level 3
**Password:** 263JGJPfgU6LtdEvgfWU1XP5yac29mFx

This level has a file with spaces in its name. To read files with spaces or special characters, you have two options:
- Escape spaces with backslashes: `cat ./file\ with\ spaces`
- Use double quotes: `cat "./file with spaces"`

**Solution:**
```bash
cat "spaces in this filename"
# or
cat spaces\ in\ this\ filename
```

## Level 3 → Level 4
**Password:** MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx

The password is stored in a hidden file (files starting with `.`). Use `ls -a` to show all files, including hidden ones. Navigate using `cd` and locate the hidden file in the directory.

**Solution:**
```bash
cd inhere
ls -la
cat .hidden
```

## Level 4 → Level 5
**Password:** 2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ

The password is in the only human-readable file in the `inhere` directory. You can either:
1. Check each file manually with `cat`
2. Use the `file` command to identify file types: `file ./*`

All files except one will show as "data" type. The human-readable file contains your password. If your terminal gets cluttered, use `reset` or `clear` to clean it up.

**Solution:**
```bash
cd inhere
file ./*
cat ./-file07
```

## Level 5 → Level 6
**Password:** 4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw

This level requires using the `find` command effectively. The password is in a file that is:
- Human-readable
- 1033 bytes in size
- Not executable

Use this command to locate it:

**Solution:**
```bash
cd inhere
find ./ -type f -not -executable -size 1033c
cat ./maybehere07/.file2
```

## Level 6 → Level 7
**Password:** HWasnPhtq9AVKe0dmk45nxy20cvUa6EG

The password is somewhere on the entire system with these properties:
- Owned by user bandit7
- Owned by group bandit6
- 33 bytes in size

Search the entire filesystem using:

**Solution:**
```bash
find / -size 33c -user bandit7 -group bandit6 2>/dev/null
cat /var/lib/dpkg/info/bandit7.password
```

*Note: The `2>/dev/null` redirects error messages (like permission denied) to prevent clutter.*

## Level 7 → Level 8
**Password:** morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj

The password is in a large file next to the word "millionth". Use `grep` to search for specific text within files:

**Solution:**
```bash
cat data.txt | grep millionth
# or
grep millionth data.txt
```

## Level 8 → Level 9
**Password:** dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc

The password is in a large file with many characters, and our password occurs only once in the file. Use `uniq` with the `sort` command to get the password from the file.

**Solution:**
```bash
sort data.txt | uniq -u
```

## Level 9 → Level 10
**Password:** 4CKMh1JI91bUIZZPXDqGanal4xvAg0JM

The password is in a file full of gibberish characters and contains several `=` before it. Use `strings` to read the human-readable characters and combine it with `grep ===` to get the password.

**Solution:**
```bash
strings data.txt | grep ===
```

## Level 10 → Level 11
**Password:** FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey

This password is encoded with base64 encryption this time. Use the `base64` command to decode the encryption and get our password.

**Solution:**
```bash
cat data.txt | base64 -d
```

## Level 11 → Level 12
**Password:** dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr

This password uses ROT13 encryption, meaning the letters both uppercase and lowercase are rotated 13 positions - `a` becomes `n`.
Use the `tr` command with cat to get the password.

**Solution:**
```bash
cat data.txt | tr 'a-zA-Z' 'n-za-mN-ZA-M'
```

## Level 12 → Level 13
**Password:** 7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4

The password is in a file which is compressed repeatedly and is a hexdump. Use `xxd` to reverse the hexdump to a binary file, then check the file type and decompress according to the file type. For safety, we should do this after making a copy of the `data.txt` file. We should create a directory in `/tmp` to work freely.

**Solution:**
```bash
# create directory in tmp
mkdir /tmp/fileOps
# change directory
cd /tmp/fileOps
# Copy hex dump file
cp ~/data.txt dataCopy.txt
# reverse hexdump to binary
xxd -r dataCopy.txt > revHexDump

# check file type
file revHexDump

# then perform decompression accordingly by changing extension using mv command
mv revHexDump revHexDump.bin.gz

# decompress
gzip -d revHexDump.bin.gz

# Repeat file check, rename and decompress as needed
```

## Level 13 → Level 14
**Password:** FO5dwFsc0cbaIiH0h8J2eUks2vdTDwAn

We get an SSH key for the next level which we can use to log into the level 14 machine. Copy the key to our machine and change permissions to read-only with the chmod command.

**Solution:**
```bash
# change permission
chmod 0600 key

# log in
ssh -i key bandit14@machine -p 2220

# after connecting we can read the password at
cat /etc/bandit_pass/bandit14
```

## Level 14 → Level 15
**Password:** MU4VWeTyJk8ROof1qqmcBPaLh7lDCPvS

The password is on localhost port 30000 according to the description. Use `nc` to connect and enter the password of the current level to get the password for the next level.

**Solution:**
```bash
nc localhost 30000

# enter password
MU4VWeTyJk8ROof1qqmcBPaLh7lDCPvS # it returns password for next level
```

## Level 15 → Level 16
**Password:** 8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo

We need to connect with an SSL/TLS secure connection. For that we can use `openssl`. To send and receive data we can use `s_client` with `openssl`.

**Solution:**
```bash
openssl s_client -connect localhost:30001
```

## Level 16 → Level 17
**Password:** kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx

To find the port number of the servers, we can use the port enumeration tool `nmap`. You'll know which one to connect to when you see the nmap results. But openssl gave me a lot of useless information and nothing worked. But when I was about to lose my mind, I tried `ncat` with the `--ssl` attribute and passed the password and got the flag. After reading a little, I found one explanation for the `openssl` behavior: that SSL version differences can cause this, but I'm not sure. If you know, please let me know. I'm also learning.

**Solution:**
```bash
nmap -p31000-32000 -sV

ncat --ssl localhost 31790
```

## Level 17 → Level 18
**Password:** EReVavePLFHtFlFsjn3hyzMlvSuSAcRD

We can check the difference between files using the `diff` tool, which shows the difference between file1 and file2.

**Solution:**
```bash
diff passwords.old passwords.new
```

## Level 18 → Level 19
**Password:** x2gLTTjFwMOhQ8oWNbMN362QKxfRqGlO

This is going to blow some people's minds. We cannot log in normally, but we can execute commands when logging in via SSH. So we cannot get a complete session with our user but can execute commands as the user we are trying to log in as. This one is really crazy, I know.

**Solution:**
```bash
ssh bandit18@host -p 2220 ls
# list the files in current directory

ssh bandit18@host -p 2220 cat readme
# outputs our password
```

## Level 19 → Level 20
**Password:** cGWpMaKXVwDUNgPAVJbWYuGHVn9zl3j8

We have a binary file which is a program. If we try to run it, we can see it executes `id` and shows `setuid`, meaning we can execute commands using this program. Try `whoami` and it shows bandit20, meaning this program executes commands as user `bandit20`. We can read the password of bandit20 using this binary.

**Solution:**
```bash
./bandit20-do cat /etc/bandit_pass/bandit20
```

## Level 20 → Level 21
**Password:** 0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO

In this level we have a binary like the last one, but this time it makes a connection and listens for an incoming string. If the string is our current user's password, it will send the password for the next one. We can start a server using `nc` and then background it. Then connect using the binary `./suconnect <port_nc>`, then background this connection and foreground the `nc` connection. Paste the password and send it, make the connection background. Foreground the binary connection - if everything works, it shows a message that it sent the password. Background it or close it, then foreground the `nc` connection and our password will be there.

**Solution:**
```bash
nc -l -p 8080 & # & to start the server in background
./suconnect 8080  # Hit Ctrl+Z to make it background
# our background processes have IDs like 1, 2 and more
fg 1 # this will bring the nc connection process back to terminal
# paste password, hit enter
# again CTRL+Z
fg 2
# Read message, hit CTRL+Z or CTRL+C to close connection
fg 1
# Copy password and stop nc listener
```

## Level 21 → Level 22
**Password:** EeoULMCra2q0dSkYj561DX7s1CpBuOBt

According to the description, we have a cron job running, so to look into it we should visit the `cron.d` folder in `/etc`. It has a job named `cronjob_bandit22` that we can read. By reading it, we find that it executes a script at `/usr/bin/cronjob_bandit22.sh`. If we check permissions, we can read it too. After reading, we discover that it stores the bandit22 password in `/tmp` in a file with a gibberish name. We can read that too.

**Solution:**
```bash
cd /etc/cron.d

cat cronjob_bandit22

cat /usr/bin/cronjob_bandit22.sh

cat /tmp/<filename>
```

## Level 22 → Level 23
**Password:** tRae0UfB9v0UzbCdn9cY0gQnds9GF58Q

Again we have a cronjob. We can read the script - the password file is getting copied, but this time the name is generated by a command. To find the name of the file, execute the command.

**Solution:**
```bash
echo I am user bandit23 | md5sum | cut -d ' ' -f 1 # change $myname with bandit23

cat /tmp/<filename>
```

## Level 23 → Level 24
**Password:** 0Zf11ioIjMVN551jX3CmStKLYqjk54Ga

In this level we have a cron job which executes a script like the last one. But the catch here is that the script executes and deletes all the scripts inside a directory. We can create a script which reads the bandit24 user password and copies it to a file. The script will be executed as bandit24, so we need to provide proper permissions for the script which is getting executed, the file where the password is getting written, and the directory in which the password file is present.

**Solution:**
```bash
cd $(mktemp -d) # create temporary dir and move to it

# write script
vi bandit24_pass.sh

# #!/bin/bash
# cat /etc/bandit_pass/bandit24 > /tmp/<TmpDirName>/password
chmod 777 bandit24_pass.sh # make the script executable by everyone

touch password
chmod 777 password

chmod 777 /tmp/<TmpDirName> # make the tmp dir permissions so everyone can read, write, and execute

cp bandit24_pass.sh /var/spool/bandit24/foo
```

## Level 24 → Level 25
**Password:** gb8KRRCsshuZXI0tUuR6ypOFjiZbf3G8

The password is on a daemon which takes a password and 4-digit pin. We can use a script to loop from 0000 to 9999 to get our password.

**Solution:**
```bash
#!/bin/bash
password=gb8KRRCsshuZXI0tUuR6ypOFjiZbf3G8
for i in {0000..9999}; do
    echo "$password $i"
done | nc localhost 30002 | grep -v Wrong | grep -v "I am the pincode checker for user bandit25"
```

## Level 25 → Level 26
**Password:** iCi86ttT4KSNe1armKiwbQNmB3YJP3q4

We can read what shell is being used by `bandit26` at `/etc/passwd`. It shows the command being executed at shell start, which is `more`. `more` opens the `text.txt` file of the `bandit26` user, which is just a banner. The size of the banner is not big enough for the more command to go into reading mode. If we resize our terminal small enough, more goes into reading mode. Then we can use `vi`, a text editor which can be used to execute commands, so we can read the password of `bandit26`.

**Solution:**
```bash
# Resize terminal to be very small, then SSH in
# When more is active, press 'v' to enter vi mode
```

## Level 26 → Level 27
**Password:** s0773xxkk0MXfdqOfPRVr9L3jJBUOgCZ

The password for `bandit27` is connected to the previous one. We cannot get a shell by logging in as `bandit26`, so we do the same thing and get to the `vi` editor. If we read more about `vi`, we know that we can set some temporary things. We set `:set shell=/bin/bash` from `vi`. Then we can get a shell using the `:sh` command in `vi`. To get the password for the next machine, there's a binary in the bandit26 home which executes commands as `bandit27`. So we can simply read the password for bandit27.

**Solution:**
```bash
:set shell=/bin/bash

:sh

./bandit27-do cat /etc/bandit_pass/bandit27
```

## Level 27 → Level 28
**Password:** upsNCc7vzaRDx6oZC6GiR6ERwe1MowGB

We have a repo at port `2220`. Go to the tmp directory. Clone the repo and read the `README` file.

**Solution:**
```bash
cd $(mktemp -d)

git clone ssh://bandit27-git@localhost:2220/home/bandit27-git/repo # defining the port is important, otherwise it will try to connect at port 22

cd repo

cat README
```

## Level 28 → Level 29
**Password:** Yz9IpL0sBcCeuG7m9uQFt8ZNpS4HZRcN

Again clone the repo. But this time the password is not there. We can check commits using `git log`, which shows there are a few commits, so we can check file data at different commits by using `git show <commit_hash:filepath>`.

**Solution:**
```bash
git show <hash>:README
```

## Level 29 → Level 30
**Password:** 4pT1t5DENaYuqnqvadYs1oE4QLCdjmJ7

Again clone. But this time the message is that the password is not in production. This can mean that the password is not in the current `branch`. To list all branches we use `git branch -r`. We have a few different branches. We can switch branches using `git switch <branch_name>`.

**Solution:**
```bash
git branch -r

git switch dev

cat README.md
```

## Level 30 → Level 31
**Password:** qp30ex3VLz5MDG1n91YowTv4Q8l7CDZL

Clone repo. Nothing in the file. No branches and no commits this time. So I tried to go and read files inside the `.git` directory. In the `packed-refs` file we can see a ref called `secret`. To list refs use `git show-ref` - there's a ref named `secret`. To read refs use `git show <ref_name>`.

**Solution:**
```bash
git show-ref
git show secret
```

## Level 31 → Level 32
**Password:** fb5S2xb7bRyFmAvQYQGEqsbhVyJqhnDy

Clone repo. Read the file. Create file `key.txt` with content as per the `README`. Then add the file to git tracking, but we can't because in `.gitignore` text files are marked to be ignored, so we change it, add it, commit it, and push it.

**Solution:**
```bash
echo "May I come in?" > key.txt

vi .gitignore # remove *.txt line and save it

git add key.txt

git commit -m "adding_file"

git push
```

## Level 32 → Level 33
**Password:** 3O9RfhqyAlVBEZpVb6LYStshZoqoSx5K

To escape we use $0 which will use `sh` and a shell will spawn.

**Solution:**
```bash
$0
```

## Level 33 → Level 34
**Password:** tQdtbs5D5i2vJwkO8mEyYEyTL8izoeJ0

**Solution:**
```bash

```
