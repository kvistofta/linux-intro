The file system in Linux quite similar to other file systems: They are hierarcically organized with file and directories within directories. 

One major difference between Linux file system and the file system in Windows-computers is that in Linux are **all** files and directories in one single tree structure. In Windows you probably have a C: and maybe a D:. And if you insert a USB thumb drive or external hard drive they will show up as E:, K: or X: (or something else). All partitions have different drive letters.

In Linux you always have **one*** file hierarchy. Parts of that hierarchy can be one hard drive and another part another hard drive. If you insert an external storage, those files will show up in a subdirectory of **the same** hierarchy. There is only one tree, and one root.

The root directory is... the root. It is referenced to as "/", slash. (Note, that´s a front slash, **not** a back slash!). in the root there are different subdirectories: mnt, home, bin and so on. Since they are directly beneath the root, they are referenced as /mnt, /home and /bin respectively.

# path

A path is a way to explain a location in the directory tree. A path can be either absolute or relative.

## absolute paths

An absolute path begins with / and starts from the root. Examples:

* /home
* /usr/lib/hdparm/hdparm-functions
* /root/.ssh/authorized_keys

Since all absolute path starts from the root (begins with /) there will never be any doubts which file or directory we wants to point out.

# relative paths

A relative path is any path that does not start with a /. Examples:

* *.ssh/authorized_keys
* afile
* root/.ssh/authorized_keys

When we use relative paths the location of the file or directory is always relative to the current directory (see below).

# file or directory?

It can be a bit confusing when looking at a path: does it point to a file or directory? This is true for all examples above. If we examine the absolute path "/root/.ssh/authorized_keys", it tells us that:

* Beginning from the root (/) there is a subdirectory called "root"
* In that /root directory there is a subdirectory called .ssh
* In that .ssh subdirectory there is something called authorized_keys

But is that "authorized_keys" something a file or a subdirectory? Just by looking at the absolute path "/root/.ssh/authorized_keys" we cannot tell. 

One way to be specific about a path and state that is is a directory and **not** a file is to end the path with a slash:  "/root/.ssh/authorized_keys/". This means that "authorized_keys" is a directory and not a file.

In practice we can use the command `ls -l` to find out:

```shell
root@bettan:~# ls -l /root/.ssh/
total 12
-rw------- 1 root root    0 Mar 14  2022 authorized_keys
-rw------- 1 root root 2590 May 25  2022 id_rsa
-rw-r--r-- 1 root root  565 May 25  2022 id_rsa.pub
-rw-r--r-- 1 root root  666 Jun  1  2022 known_hosts
root@bettan:~#
```

authorized_keys is a file since the first character to the left is a dash "-" and not a "d". 


# current directory

When logged in at a shell you "are" always in a specific directory in the file system. At start you normally resides in the home directory for the logged in user. Which directory you "are" in is often shown by the rightmost part of the prompt:

```shell
nisse@bettan:~$
```

~ (tilde, sinus) is a special character that means "the current users home directory". When logged in as an ordinary user this is normally /home/username and for root it is /root.

You can always make sure which directory is current by running the `pwd` command:

```shell
nisse@bettan:~$ pwd
/home/nisse
nisse@bettan:~$
```

The `pwd` command prints the current directory.

# cd

The `cd` command is used to change current directory (cd = "change directory"). If you just run the cd command without any parameter it defaults to ~ and will "move" you to your home directory. If you want to change to another directory, issue the command `cd directory`. Here are a few examples:

```shell
nisse@bettan:~$ cd /usr/lib
nisse@bettan:/usr/lib$ pwd
/usr/lib
nisse@bettan:/usr/lib$ cd /home
nisse@bettan:/home$ pwd
/home
nisse@bettan:/home$ cd
nisse@bettan:~$ pwd
/home/nisse
nisse@bettan:~$
```

As you can see the current directory is shown after the ":" in the prompt and the pwd shows the same.

The path specified with the cd command can be either absolute or relative. If you specify a relative path is it relative to your current directory. So `cd nisse` will move you down one level in the directory structure to a sub-directory called "nisse" relative to **where you are when running the command**.

If there is no subdirectory called nisse you will get an error message:

```shell
nisse@bettan:~$ cd nisse
-bash: cd: nisse: No such file or directory
nisse@bettan:~$
```

However, if we "are" in /home and want to move down to /home/nisse we can either `cd /home/nisse` or use a relative path: `cd nisse`:

```shell
nisse@bettan:~$ cd /home
nisse@bettan:/home$ cd nisse
nisse@bettan:~$
```

# .

A single dot has a special meaning in Linux, it relates to the current directory. If you want to copy a file from somewhere to "here" you can do:

```shell
nisse@bettan:~$ cp /usr/lib/eject/dmcrypt-get-device .
nisse@bettan:~$
```

# ..

Two dots means "one level up". You can use this with the cd command to "move up" in the directory structure. 
```shell
nisse@bettan:~$ cd ..
nisse@bettan:/home$ cd ..
nisse@bettan:/$
```

.. is a relative path since it does not begin with /. That makes sense since .. points to "one level up" from your current directory which is not static.

You can use .. with the cp command to copy a file "one level up":

```shell
nisse@bettan:~$ ls
dmcrypt-get-device
nisse@bettan:~$ cp dmcrypt-get-device ..
cp: cannot create regular file '../dmcrypt-get-device': Permission denied
nisse@bettan:~$
```

Note here that the example above shows a working cp-command but nisse has now permission to write a file "one level up", that is in the /home directory, hence the error message. (More about file permissions later)

# tree

To get a move visual picture of the directory tree, you can use the `tree` command. It will print a hierarcical tree of the current directory and all files/directories in and below that:

```shell
nisse@bettan:~$ tree
.
└── dmcrypt-get-device

0 directories, 1 file
nisse@bettan:~$
```

# hidden files

In DOS/Windows there is a specific file attribute that makes a file hidden. That concept does not exist in Linux. Per se there are no hidden files in Linux. However, there is an agreement between developers that a file whose first character in the name is . (a dot) should not normally be displayed. That´s why you wont see .ssh, .bash_history and more if you use `ls` but with `ls -l` those files are shown.

You can simply "hide" a file by naming it with a dot in the beginning of a name. Simple but elegant.




