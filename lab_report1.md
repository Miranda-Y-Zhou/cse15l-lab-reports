# Lab Report 1 
[Miranda Zhou](https://github.com/Miranda-Y-Zhou)

Date: 10/09/2023

---

## FileSystem (Week 1)
This lab is about the basic filesystem commands:

* [Change Directory Command: `cd`](https://miranda-y-zhou.github.io/cse15l-lab-reports/lab_report1.html#change-directory-command-cd)
* [List Command: `ls`](https://miranda-y-zhou.github.io/cse15l-lab-reports/lab_report1.html#list-command-ls)
* [Concatenate Command: `cat`](https://miranda-y-zhou.github.io/cse15l-lab-reports/lab_report1.html#concatenate-command-cat)

---

### Change Directory Command: `cd`

#### 1. `cd` with no arguments

When the command `cd` is used without any arguments, no visiable output is given by the terminal, as shown below.

```
[user@sahara ~]$ cd 
[user@sahara ~]$
```

But the user will be taken to the user's home directory, if the current directory is not already the home directory. 

As shown in the example below, the working directory before running the command is `/home/lecture1`, and after running the command it became `/home`.

```
[user@sahara ~/lecture1]$ pwd
/home/lecture1
[user@sahara ~]$ cd 
[user@sahara ~]$ pwd
/home
```

When no argument is provided by the user, it defaults to taking the user to their home directory. It is a feature designed to quickly get back to the home directory. The output is not an error.

&nbsp;

#### 2. `cd` with a path to a directory as an argument

When the command `cd` is given a directory as an argument, `cd` will change the current working directory to the specified directory path, and no visiable output is given by the terminal.

As shown in the example below, the terminal does not give an output but the working directory changed from the current working directory `/home` to the specified directory `/home/lecture1/messages`.

```
[user@sahara ~]$ pwd
/home
[user@sahara ~]$ cd lecture1/messages
[user@sahara ~/lecture1/messages]$ pwd
/home/lecture1/messages
```

If the directory exists, there won't be any error.
If the argument given is a directory that does not exist, an error will be produced as the computer cannot find such directory.

Error example:

```
[user@sahara ~]$ cd lecture1/messag
bash: cd: lecture1/messag: No such file or directory
```

&nbsp;

#### 3. `cd` with a path to a file as an argument

When the command `cd` is given a path to a file as an argument, the working directory will not change and the terminal will output an error message. 

As shown in the example below, the working directory stayed as `/home`, and an error message `bash: cd: lecture1/messages/fr-ca.txt: Not a directory` was given. 

```
[user@sahara ~]$ pwd
/home
[user@sahara ~]$ cd lecture1/messages/fr-ca.txt
bash: cd: lecture1/messages/fr-ca.txt: Not a directory
[user@sahara ~]$ pwd
/home
```

An error is given because the `cd` command expects a directory path. If a file path was provided, it will return an error since the user cannot change the working directory to a file.

&nbsp;

---

### List Command: `ls`

#### 1. `ls` with no arguments

When the command `ls` is used without any arguments, `ls` lists the contents of the current working directory. 

In the example below, the current working directory is `/home`, thus `ls` outputs the content of `/home`, which is a folder named `lecture1`. 

```
[user@sahara ~]$ pwd
/home
[user@sahara ~]$ ls
lecture1
```

When no argument is provided by the user, it defaults to current working directory. The output is not an error. 

&nbsp;

#### 2. `ls` with a path to a directory as an argument

When the command `ls` is used with a path to a directory as an argument, `ls` lists the contents of the specified working directory.

In the example below, `ls` outputs the content of the directory `messages`, which are four `.txt` files. The current directory will not be affected. 

```
[user@sahara ~]$ pwd
/home
[user@sahara ~]$ ls lecture1/messages
en-us.txt  es-mx.txt  fr-ca.txt  zh-cn.txt
[user@sahara ~]$ pwd
/home
```
If the directory exists, there won't be any error.
If the argument given is a directory that does not exist, an error will be produced as the computer cannot find such directory. 

Error example:

```
[user@sahara ~]$ ls lecture1/messag
ls: cannot access 'lecture1/messag': No such file or directory
```

&nbsp;

#### 3. `ls` with a path to a file as an argument

When the command `ls` is used with a path to a file as an argument, it will just echo back the file path if the file exists. This is because `ls`'s primary function is to list the contents of a directory. When the user provide it a directory path, it does just that —- it lists everything inside that directory. 

However, when the user give `ls` a specific file path, there's technically only the file itself at that location. Therefore, `ls` only needs to confirm the existence of that one file. So, it "lists" that one file, which in practice means echoing back the file path.

As shown in the example below, when the file path to `fr-ca.txt` is given as an argument, the terminal outputs the file path of the specified file as given, which is `lecture1/messages/fr-ca.txt` in this case, confirming its existence. Again, `ls` does not affect the working directory, which stays `/home`.

```
[user@sahara ~]$ pwd
/home
[user@sahara ~]$ ls lecture1/messages/fr-ca.txt
lecture1/messages/fr-ca.txt
[user@sahara ~]$ pwd
/home
```

If the file path specified exists, there won't be any error.
If the argument given is a file path that does not exist, an error will be produced as the computer cannot find such file following the provided path. 

Error example:

```
[user@sahara ~]$ ls lecture1/messages/a.txt
ls: cannot access 'lecture1/messages/a.txt': No such file or directory
```

&nbsp;

---

### Concatenate Command: `cat`

#### 1. `cat` with no arguments 

When the `cat` command is used with no argument, the terminal waits for user input from the keyboard. 

As shown in the example below (working directory: `/home`), after `cat` command is given with no argument. The command will appear to wait. It's not frozen. 

```
[user@sahara ~]$ pwd
/home
[user@sahara ~]$ cat
▋
```

Anything typed is immediately echoed back to the terminal upon pressing Enter. 

```
[user@sahara ~]$ pwd
/home
[user@sahara ~]$ cat
apple
apple
orange
orange
▋
```

To exit this input state and return to the command prompt, the user can signal an end-of-file by pressing Ctrl + D. 

```
[user@sahara ~]$ pwd
/home
[user@sahara ~]$ cat
apple
apple
orange
orange
[user@sahara ~]$
```

This mode allows users to provide content directly from the terminal. The output is not an error.

#### 2. `cat` with a path to a directory as an argument

#### 3. `cat` with a path to a file as an argument



