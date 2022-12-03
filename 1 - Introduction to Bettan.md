If you read this you are problably attending one of my Linux-courses and just logged in to the Bettan lab server. Welcome! Be nice to Bettan and she will be nice to you!

If you have been working with Linux before, you can probably skip major parts of this text since the target audience is you that have never seen or worked with a Linux CLI (command line interface) before.

# ssh

You have been told to login to bettan using a ssh client. There are many different graphical ssh clients for all major operating systems, such as Putty, Teraterm, Hyper Terminal  and SecureCRT. They are all more and less great! However, in this course we will use the built in ssh client. 

As of 2022 when this is written, a built in ssh client is available in all Linux, Macs and even(!) windows OS:s. A few years ago there was not SSH client built into Windows but from Windows 10 (correct me if I am wrong) there is a CLI-based SSH-client built in. So the process of finding it is the same in all OS:es. You start up a terminal (Command prompt in Windows) and enter the command `ssh username@10.0.5.254`. You must replace "username" with the username provided to you. Next step, enter the password you have been given and you are logged in!

```shell
Jimmys MbP ~ % ssh nisse@10.0.5.254
=======================================================================
= Welcome to Bettan. This the main server for Linux-courses.          =
= Bettan is not part of any hacking activities. You are not           =
= allowed to pentest this machine.                                    =
=                                                                     =
= Unauthorized logins are prohibited and logins.                      =
= You have been warned.                                               =
=                                                                     =
= However, if you have been told to login to Bettan, please continue. =
=======================================================================
nisse


nisse@10.0.5.254's password:
nisse@bettan:~$
```

>If nothing happens when you run the ssh-command it´s probably a network issue. You need to connect your VPN client first in order to reach Bettan. Can you ping 10.0.0.1? If not, troubleshoot VPN.

The first thing you will see when you log in to Bettan the first time is this:

```shell
nisse@bettan:~$
```

If you press enter you will just see more similar lines. This called a prompt and it tells you:

1) You are logged in as nisse (or at least I am when writing this)
2) The server name is bettan
3) The current directory is ~ (more about this later).



# passwd

The first thing to do is to change your password. The command for this is `passwd`. Just enter the command and press `Enter`. You wil be prompted for your current password (the password you just used to login to Bettan) and then a new password, twice.

>About choosing a good password
>A good password is something that is:
>* Random
>* Not guessable
>* Unique
>I recommend a random string of both numbers and letters, at least 10 characters long. Store it somewhere securely, because you will need it again.


If you get a "Token manipulation Error" it probably means that you have failed to enter the same new password twice, or failed to enter the current password correctly. Try again!

# A few sample commands

Here are a few commands that you can try:

`who`:
```shell
nisse@bettan:~$ who
jimmy    pts/0        2022-12-02 14:14 (10.192.128.5)
jimmy    pts/1        2022-12-02 13:55 (10.192.128.5)
nisse@bettan:~$
```


`whoami`:
```shell
nisse@bettan:~$ whoami
nisse
nisse@bettan:~$
```

`hostname`:
```shell
nisse@bettan:~$ hostname
bettan
nisse@bettan:~$
```

`date`:
```shell
nisse@bettan:~$ date
Fri Dec  2 14:31:32 UTC 2022
nisse@bettan:~$
```

`id`:
```shell
nisse@bettan:~$ id
uid=1001(nisse) gid=1002(nisse) groups=1002(nisse)
nisse@bettan:~$
```

`cal`:
```shell
nisse@bettan:~$ cal
   December 2022
Su Mo Tu We Th Fr Sa
             1  2  3
 4  5  6  7  8  9 10
11 12 13 14 15 16 17
18 19 20 21 22 23 24
25 26 27 28 29 30 31

nisse@bettan:~$
```


`pwd`:
```shell
nisse@bettan:~$ pwd
/home/nisse
nisse@bettan:~$
```

We wil talk more about a few of these commands later on. But can you guess the purpose of each of these commands?

# command options

Most command have several different command options that modifies the behaviour of that command. Which command options that are available for a specific command is up to the developer(s) to decide. 

Let´s have a look at the `ls` command and two command options: `-a` and `-l`:

Just running `ls` lists files in the current directory. You might get a different output but this is how it looks when nisse runs the command:

```shell
nisse@bettan:~$ ls
nisse@bettan:~$
```

Nothing happened? Don´t worry, thats because nisse has no files yet. Try to run the command `ls -a`:

```shell
nisse@bettan:~$ ls -a
.  ..  .bash_history  .bashrc  .local  .profile
nisse@bettan:~$
```

So, there were a few files anyway. If we look at the man pages (more about that in the next section) we can read this about the `-a` option:

```shell
       -a, --all
              do not ignore entries starting with .

```

All nisses files have names that begins with ".", that´s why there is no output from the ls command.

Another option: `-l`:
```shell
nisse@bettan:~$ ls -l
total 0
nisse@bettan:~$
```

Again, no files. But this time we get a "summary" telling us a total of 0 files.

We can combine multiple options. Let´s run `ls -l -a`:

```shell
nisse@bettan:~$ ls -l -a
total 24
drwxr-xr-x 3 nisse nisse 4096 Dec  2 13:57 .
drwxr-xr-x 8 root  root  4096 Dec  2 13:50 ..
-rw------- 1 nisse nisse  131 Dec  2 14:32 .bash_history
-rw-rw-r-- 1 nisse nisse 3771 Dec  2 13:57 .bashrc
drwxrwxr-x 3 nisse nisse 4096 Dec  2 13:57 .local
-rw-rw-r-- 1 nisse nisse  807 Dec  2 13:57 .profile
nisse@bettan:~$

```


The conclusion we can make is that -l lists files differently than ls without -l. This is from the man pages about the -l option of the ls command:

```shell
      -l     use a long listing format
```

In the next session I will explain about how to find out which options are available for a certain command. 

For ls and some other commands, the options can be stacked in different ways, giving the same result:
* ls -l -a
* ls -a -l
* ls -la
* ls -al

# getting help

So, how do we find out how a command works, which options we can add and what they mean?

The answer is that there are several different ways do do that, and all ways doesn´t work all the time. First of all, we can search the internet. If I Google for "ls long listing option" I will get about 284.000.000 search results! :)

## --help

Often a certain command has an option `--help` that outputs how a command work, which options are available and more. `ls --help` gives the following output:

``shell
Usage: ls [OPTION]... [FILE]...
List information about the FILEs (the current directory by default).
Sort entries alphabetically if none of -cftuvSUX nor --sort is specified.

Mandatory arguments to long options are mandatory for short options too.
  -a, --all                            do not ignore entries starting with .
  -A, --almost-all               do not list implied . and ..
      --author                       with -l, print the author of each file
  -b, --escape                    print C-style escapes for nongraphic characters
  -B, --ignore-backups     do not list implied entries ending with ~
.... many lines removed



## man pages

Another way to get help is to use the manual (remember: Read The Freaking Manual). In Linux the "manual" for all commands are built-in and is called "man pages". If you install a software that is not already installed in your Linux server, chances are good that the installation process also includes adding man pages for the application, to your system.

The man pages can be summoned with the `man` command followed by a space and the command you want to read the man page for. For example `man ls`:

The man pages are often several screen pages long and you can advance to the nex page with the space key. Sometimes you can also scroll the man pages line by line with the up/down arrow keys. To escape the man pages, press "q".

# command parameters

Besides command options that modifies the behaviour of a command, most command also have parameters. A parameter is normally an object-like item that the command needs to know.

As an example, if we want to delete a file (the command is rm) we can´t just tell the system to run that command, but the command needs to know *which* file to delete.

If we want to copy a file, the copy-command (it is called cp in Linux) needs two parameters: 
1) What do you want to copy?
2) Where should I put the copy?

A third example: The ls command lists files. But in which directory? We can tell ls to list all files in the root directory of the file system with the command `ls /` and do we want to see all files in the /dev directory we run `ls /dev`. However the directory parameter of the ls command is optional, which means it is not required. Earlier we ran `ls -la` and since we didn´t specify a directory parameter it defaulted to list the files in the current directory. The directory parameter is not mandatory.

command syntaxes

When looking at the command syntax in man pager, except from explaining each parameter and option it also shows the syntax of the command. Here are a few example of command syntaxes from man pages:

```
gzip [ -acdfhklLnNrtvV19 ] [-S suffix] [ name ...  ]

ls [OPTION]... [FILE]...

  cp [OPTION]... [-T] SOURCE DEST
```

Sooner or later you will probably read man pages for some commands and I will explain how to interprete the strange texts above.

Everything written inside of brackets are optional (not mandatory). That includes all the options for the ls command. Also file (directory to list files in) is optional.

When there are tree dots "..." it means that you can enter more than one. You can list files in multiple directories with the ls command:

```shell
nisse@bettan:~$ ls /home/nisse /dev/dvd /var/log/account/
/dev/dvd

/home/nisse:

/var/log/account/:
pacct
nisse@bettan:~$
```

However, parameters that are not within brackets, like "SOURCE" and "DEST" for the cp command, they are mandatory. 

# command line navigation

When entering a command, you can navigate thru your written command with the arrow keys. Also you can recall your last command with the up-arrow on your keyboard. This saves you a lot of keystrokes if you want to re-run the last command, or want to enter it again but modify it. 

There are many special key strokes for the command line. The most common are:

* CTRL-A moves the cursor to the beginning of the command.
* CTRL-E moves the cursor to the end of the command.

There is one more very useful key stroke for the Linux command line: CTRL-R. It is probably too early to try it right now but next week when you have entered hundreds of commands into the command line, you can go back to this section and try out CTRL-R.

When you press CTRL-R, you will start a search among your previously written command. If you after the CTRL-R enters one or a few characters, the last command that contained that character sequence shows up and can be re-run again. This is very powerful when you enter long and complex commands. Try it, but later!

Your "previous commands" is called command history and it is stored when you logout, so that you can, when logging back in again next monday use the up-arrow or CTRL-R to retreive those commands you wrote last week. "De e najs" as we say in Sweden. :)

# Logging out

One good command to know is `exit`. It will log you out from your current session. If this is the end of the day you can `exit` now.


