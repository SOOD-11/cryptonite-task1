# cryptonite-task1
# OverTheWire Bandit CTF Writeup

## Level 0 to Level 1

In this first challenge, we need to log into the server using SSH. The command to do this is:

```bash
ssh bandit0@bandit.labs.overthewire.org -p 2220
```

We use the password `bandit0` when prompted. Once logged in, we need to find the password for the next level. The password is stored in a file called `readme` in the home directory. We can use the `ls` command to list the files in the directory and `cat` to read the file:

```bash
ls
cat readme
```
This command will display the contents of the `readme` file, which is the password for the next level.

Password: `NH2SXQwcBdpmTEzi3bvBHMM9H66vVXjL`



## Level 1 to Level 2

To progress to the next level, we need to exit the current level using the `exit` command and log in again using SSH, but this time to `bandit1`. We use the password we obtained from the `readme` file in the previous level.

The password for this level is stored in a file called `-`. To read the file, we use the `cat` command with `./` prefix:

```bash
ls
cat ./-
```
The `./` prefix is used to specify that the file is in the current directory. This is necessary because `-` is also an option in many commands.

Password: `NH2SXQwcBdpmTEzi3bvBHMM9H66vVXjL`



## Level 2 to Level 3

We log in to the server as `bandit2` using the password obtained from the previous level. The password for this level is stored in a file called `spaces in this filename`. To read this file, we can use the `cat` command with backslashes to escape the spaces or use tab to autocomplete the file name [or we can just type cat spaces and press the TAB button to autocomplete the filename]:

```bash
ls
cat spaces\ in\ this\ filename
```
The backslashes are used to escape the spaces in the filename, allowing the `cat` command to interpret it as a single argument rather than separate ones.

Password: `aBZ0W5EmUfAf7kHTQeOwd8bauFJ2lAiG`



## Level 3 to Level 4

We log in to the server as `bandit3` using the password obtained from the previous level. The password for this level is stored in a hidden file in the `inhere` directory. We can use the `ls -lah` command to list all files, including hidden ones, and `cat` to read the file:

```bash
ls
cd inhere/
cat .hidden
```
The `ls -lah` command lists all files, including hidden ones, in a human-readable format.

Password: `2EW7BBsr6aMMoJ2HjW067dm8EgX26xNe`



## Level 4 to Level 5

We log in to the server as `bandit4` using the password obtained from the previous level. The password for this level is stored in one of the files in the `inhere` directory. We can use the `ls` command to list the files and `cat` to read each file one by one. The password is in the `-file07` file:

```bash
ls
cd inhere
find     . -typef|Xargsfile
man xargs
cat ./-file07
```
The `./` prefix is used again here to specify that the file is in the current directory.

Password: `lrIWWI6bB37kxfiCQZqUdOIYfr6eEeqR`



## Level 5 to Level 6

In this level, we need to find a file in the `inhere` directory that is human-readable, 1033 bytes in size, and not executable. We can use the `find` command to do this:

```bash
ls
cd inhere
find . -type f -size 1033c ! -executable
```
The `find` command is used to search for files in a directory hierarchy. The `-type f` option specifies that we re looking for files, `-size 1033c` specifies that the file size should be 1033 bytes, and `! -executable` specifies that the file should not be executable.

This command will give the output `./maybehere07/.file2`. We can then read the file to get the password:

```bash
cat ./maybehere07/.file2
```
The `cat` command is used to read the contents of a file.

Password: `P4L4vucdmLnm8I7Vl7jG1ApGSfjYKqJU`



## Level 6 to Level 7

In this level, we need to find a file on the server owned by `bandit7` and `bandit6`, and 33 bytes in size. We can use the `find` command again to do this:

```bash
find / -user bandit7 -group bandit6 -size 33c 2>/dev/null
```
The `find` command is used to search for files in a directory hierarchy. The `-user` option specifies that we re looking for files owned by `bandit7`, the `-group` option specifies that the file should belong to the group `bandit6`, `-size 33c` specifies that the file size should be 33 bytes, and `2>/dev/null` redirects error messages to `/dev/null` to avoid cluttering the output.

This command will give the output `/var/lib/dpkg/info/bandit7.password`. We can then read the file to get the password:

```bash
cat /var/lib/dpkg/info/bandit7.password
```
The `cat` command is used to read the contents of a file.

Password: `z7WtoNQU2XfjmMtWA8u5rN4vzqu4v99S`



## Level 7 to Level 8

In this level, we need to find the password in the `data.txt` file next to the word `millionth`. We can use the `cat` command to read the file and `grep` to find the line containing `millionth`:

```bash
ls
cat data.txt | grep 'millionth'
```
The `grep` command is used to search for a specific pattern in the input. In this case, we re searching for the word `millionth`.

Password: `TESKZC0XvTetK0S9xNwm25STk5iWrBvP`



## Level 8 to Level 9

In this level, the password is the only line of text that occurs only once in the `data.txt` file. We can use the `sort` and `uniq` commands to find this line:

```bash
ls
sort data.txt | uniq -c | grep '1 '
```
The `sort` command is used to sort the lines in the file, `uniq -c` is used to count the number of occurrences of each line, and `grep '1 '` is used to find the lines that only occur once. There is a space after '1 ' so that it does not print the lines which repeat 1x or 1xx times.

Password: `EN632PlfYiZbn3PhVK3XOGSlNInNE00t`



## Level 9 to Level 10

In this level, the password is stored in the `data.txt` file and is surrounded by equal signs. We can use the `strings` command to extract the lines containing printable characters, and `grep` to find the line containing `=`:

```bash
ls
strings data.txt | grep '='
```
The `strings` command is used to extract printable strings from a file, and `grep` is used to search for a specific pattern, in this case, the equal sign.

Password: `G7w8LIi6J3kTb8A7j9LgrywtEUlyyp6s`



#### Level 10 → Level 11
Logged in with the username `bandit10` and the aforementioned password.

Ran `ls`. Got `data.txt` again. The clue says that it contains base64 encoded data, which I could decode using `cat data.txt | base64 --decode`.

```bash
ls
base64 --decode data.txt
```

The output was `The password is 6zPeziLdR2RKNdNYFNb6nVCKzphlXHBM`.

Password: `6zPeziLdR2RKNdNYFNb6nVCKzphlXHBM`



## Level 11 to Level 12

In this level, the password is stored in the `data.txt` file and is encrypted using rot13 encryption. We can use the `cat` command to read the file and `tr` command to decode the rot13 encrypted password:

```bash
ls
cat data.txt
cat data.txt | tr '[A-Za-z]' '[N-ZA-Mn-za-m]'
use cyberchef choose rot 13
```
The `tr` command is used to translate or delete characters. In this case, it is used to rotate the alphabet by 13 places, which is used to decode rot13 encryption. [Source 0](https://medium.com/secttp/overthewire-bandit-level-12-439f655f6fd5)

This command will give the decoded output `The password is JVNBBFSmZwKKOP0XbFXOoW8chDz5yVRv`. 

Password: `JVNBBFSmZwKKOP0XbFXOoW8chDz5yVRv`



## Level 12 to Level 13

In this level, the password is stored in the `data.txt` file which is a hexdump of a file that has been repeatedly compressed. To get the password, we first need to create a temporary directory and copy the `data.txt` file to it. Then, we can use `xxd` to convert the hexdump back to binary, and `file` to identify the type of compression used. We can then decompress the file using the appropriate command, repeating these steps until we get a text file containing the password:

```bash
mkdir /tmp/mytempdir
cp data.txt /tmp/mytempdir/
cd /tmp/mytempdir/
xxd -r data.txt > data
file data
mv data data.gz
gunzip data.gz
file data
mv data data.bz2
bunzip2 data.bz2
file data
tar xvf data
file data5.bin
tar xvf data5.bin
file data6.bin
mv data6.bin data6.bz2
bunzip2 data6.bz2
file data6
tar xvf data6
file data8.bin
mv data8.bin data8.gz
gunzip data8.gz
file data8
cat data8
```
The `xxd` command is used to create a hexdump or do the reverse. The `file` command is used to determine the type of a file. `gunzip`, `bunzip2`, and `tar` are used to decompress files.

Password: `8ZjyCRiBWFYkneahHwxCv3wb2a1ORpYL`

## Level 13 to Level 14

In this level, you are given a private SSH key that can be used to log into the next level. You can use the `ssh` command with the `-i` option to specify the private key:

```bash
ssh -i sshkey.private bandit14@bandit.labs.overthewire.org -p 2220
```

After logging in with the private key, you can read the password for the next level from the `/etc/bandit_pass/bandit14` file.

Password: `4wcYUJFw0k0XLShlDzztnTBHiqxU3b3e`

## Level 14 to Level 15

In this level, the password for the next level can be retrieved by submitting the password of the current level to port 30000 on localhost. You can use the `cat` command to read the password and pipe it to the `nc` (netcat) command:

```bash
cat /etc/bandit_pass/bandit14 | nc localhost 30000
```

Password: `BfMYroe26WYalil77FoDi9qh59eK5xNr`

## Level 15 to Level 16

In this level, the password for the next level can be retrieved by submitting the password of the current level to port 30001 on localhost using SSL encryption. You can use the `openssl` command to establish a SSL connection:

```bash
cat /etc/bandit_pass/bandit15 | openssl s_client -connect localhost:30001 -quiet
```

Password: `cluFn7wTiGryunymYOu4RcffSxQluehd`

## Level 16 to Level 17

In this level, the password for the next level can be retrieved by submitting the password of the current level to a port on localhost in the range 31000 to 32000. You need to first identify the port that is listening and supports SSL. You can use a simple bash loop to check each port:

```bash
for i in {31000..32000}; do
  echo "" | openssl s_client -connect localhost:$i -quiet 2>/dev/null && echo "Port $i supports SSL"
done
```

This command will output the ports that support SSL. You can then submit the password to the correct port:

```bash
cat /etc/bandit_pass/bandit16 | openssl s_client -connect localhost:<port> -quiet
```

Replace `<port>` with the correct port number.

Password: `xLYVMN9WE5zQ5vHacb0sZEVqbrp7nBTn`

## Level 17 to Level 18

In this level, there are 2 files in the home directory: `passwords.old` and `passwords.new`. The password for the next level is in `passwords.new` and is the only line that has been changed between `passwords.old` and `passwords.new`. You can use the `diff` command to compare the two files:

```bash
diff passwords.old passwords.new
```

Password: `kfBf3eYk5BPBRzwjqutbbfE887SVc5Yd`

## Level 19 to Level 20

In this level, you need to use the `bandit20-do` setuid binary in the home directory. This binary will run a command as another user:

```bash
./bandit20-do cat /etc/bandit_pass/bandit20
```

This command will execute the `cat` command as the `bandit20` user, allowing you to read the password for the next level.

Password: `GbKksEFF4yrVs6il55v6gwY5aVje5f0j`

## Level 20 to Level 21

In this level, there is a setuid binary in the home directory that makes a connection to localhost on the port you specify as a commandline argument. It then reads a line of text from the connection and compares it to the password in the previous level (bandit20). If the password is correct, it will transmit the password for the next level (bandit21).

You need to set a listener in one terminal, and then run the binary in another terminal:

Terminal 1:
```bash
nc -lp 31337 < /etc/bandit_pass/bandit20
```

Terminal 2:
```bash
./suconnect 31337
```

The password for the next level should appear in your first terminal.

Password: `gE269g2h3mw3pwgrj0Ha9Uoqen1c9DGr`

Level 21 to Level 22

In this level, a program is running automatically at regular intervals from cron, the time-based job scheduler. If you look in `/etc/cron.d/` for the configuration, you can see what command is being executed:

```bash
cat /etc/cron.d/cronjob_bandit22
```

This reveals that a script named `cronjob_bandit22.sh` is being run. You can view the contents of this script to see what it does:

```bash
cat /usr/bin/cronjob_bandit22.sh
```

The script writes the password for the next level to a file in the `/tmp` directory. You can read the password from this file:

```bash
cat /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
```

Password: `Yk7owGAcWjwMVRwrTesJEwB7WVOiILLI`

## Level 22 to Level 23

Similarly to the previous level, a program is running automatically at regular intervals from cron. If you look in `/etc/cron.d/` for the configuration, you can see what command is being executed:

```bash
cat /etc/cron.d/cronjob_bandit23
```

This reveals that a script named `cronjob_bandit23.sh` is being run. You can view the contents of this script to see what it does:

```bash
cat /usr/bin/cronjob_bandit23.sh
```

The script writes the password for the next level to a file in the `/tmp` directory. The name of the file is a hash of the username. You can calculate the hash of the username `bandit23` and read the password from the corresponding file:

```bash
echo I am user bandit23 | md5sum | cut -d ' ' -f 1
```

This command will output the hash of the username. You can then read the password from the corresponding file in the `/tmp` directory:

```bash
cat /tmp/<hash>
```

Replace `<hash>` with the output of the previous command.

Password: `jc1udXuA1tiHqjIsL8yaapX5XIAI6i0n`

## Level 23 to Level 24

In this level, a program is running automatically at regular intervals from cron, the time-based job scheduler. If you look in `/etc/cron.d/` for the configuration, you can see what command is being executed:

```bash
ls -la /etc/cron.d/
```

This reveals that a script named `cronjob_bandit24.sh` is being run. You can view the contents of this script to see what it does:

```bash
cat /usr/bin/cronjob_bandit24.sh
```

The script executes and deletes all scripts in `/var/spool/bandit24`. We just need to write our own script, copy it in `/var/spool/bandit24` and wait for the result:

```bash
mkdir /tmp/alex1234
cd /tmp/alex1234
vi script.sh
```

Inside the `script.sh`, include the following line:

```bash
#!/bin/sh
cat /etc/bandit_pass/bandit24 >> /tmp/alex1234/bandit24pass
```

Then, change the script permissions, copy it to the `/var/spool/bandit24` directory, and wait for the result:

```bash
chmod 777 script.sh 
cp script.sh /var/spool/bandit24
chmod 777 /tmp/alex1234/
# Wait 1 minute
ls
cat bandit24pass 
```

Password: `UoMYTrfrBFHyQXmg6gzctqAwOmw1IohZ`
 # completed till level 24 enthusiast to be part of awesome sp cryptonite#
# THANKS
