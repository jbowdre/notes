---
tags:
  - linux
  - bash
---
1.  `!!`
  Repeats the previous command:
```bash
   $ ls
   $ !!
   ls
```
2. `!n`
  Repeats the command at position `n` in the history list:
```bash
$ history
1 ls
2 pwd
3 echo "Hello"
$ !2
pwd
```
3. `!-n`
  Repeats the command that was executed `n` commands ago:
```bash
$ ls
$ pwd
$ echo "Hello"
$ !-3
ls
```
4. `!string`
  Repeats the most recent command *starting with* `string`:
```bash
$ ls -l
$ pwd
$ !ls
ls -l
```
5. `!?string`
 Repeats the most recent command *containing* `string`:
```bash
$ ls -al
$ echo "Test"
$ !?al
ls -al
```
6. `^old^new`
 Repeats the previous command, but substitutes `old` with `new`:
```bash
$ echo "Hello world"
$ ^world^everyone
echo "Hello everyone"
Hello everyone
```
7. `!$`
 Refers to the *last* argument of the previous command:
```bash
$ mkdir new
$ cd !$
cd new
```
8. `!*`
 Refers to *all* the arguments of the previous command:
```bash
$ touch file1.txt file2.txt file3.txt
$ chmod o+r !*
chmod o+r file1.txt file2.txt file3.txt
```
9. `!:^`
 Refers to the *first* argument of the previous command:
```bash
$ cp file1.txt /some/directory/
$ echo !:^
echo file1.txt
file1.txt
```
10.  `!:n-m`
  Refers to a range of arguments to the previous command:
```bash
$ cp file1.txt file2.txt file3.txt /some/directory
$ echo !:1-2
echo file1.txt file2.txt
file1.txt file2.txt
```
11. `!!:p`
 Print the last command without executing it:
```bash
$ echo "Hello, World!"
$ !!:p
echo "Hello, World!"
```