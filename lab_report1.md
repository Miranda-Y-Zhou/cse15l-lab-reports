# Lab Report 1 
[Miranda Zhou](https://github.com/Miranda-Y-Zhou)

Date: 10/09/2023

---

## FileSystem (Week 1)
This lab is about the basic filesystem commands:

* Change Directory Command: `cd`
* List Command: `ls`
* Concatenate Command: `cat`

---

### Change Directory Command: `cd`

#### 1. `cd` with no arguments

When the command `cd` is used without any arguments, no visiable output is given by the terminal, as shown below.

```
[user@sahara ~]$ cd 
[user@sahara ~]$
```

But the user will be taken to the user's home directory, if the current directory is not `/home`. 

As shown in the example below, the working directory before running the command is `/home/lecture1`, and after running the command it became `/home`.

```
[user@sahara ~/lecture1]$ pwd
/home/lecture1
[user@sahara ~]$ cd 
[user@sahara ~]$ pwd
/home
```

When no argument is provided by the user, it defaults to taking the user to their home directory. This output is not an error but a feature designed to quickly get back to the home directory.

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
If the directory given as an argument does not exist, an error will be produced as the computer cannot find such directory. 

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

#### `ls` with no arguments

#### `ls` with a path to a directory as an argument

#### `ls` with a path to a file as an argument

---

### Concatenate Command: `cat`

#### `cat` with no arguments

#### `cat` with a path to a directory as an argument

#### `cat` with a path to a file as an argument


