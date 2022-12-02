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

hostname`:
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

All nisses files have names that begins with "." 
# man pages



# ls


The first command you can try is `ls`:





So it turned out that you have a few files already! 

This is the first of an unlimited number of command options that can be added to different command. Which command options that are available for a specific command can be found in the help (more about that also, soon...).

So, just `ls` list files. But adding a command option `-a` modifies the behaviour of the ls command. This is a snippet from the manual pages of the ls command:

```shell
       -a, --all
              do not ignore entries starting with .

```

If you try to run `ls --all` you will see that the output is identical to `ls -a`.
