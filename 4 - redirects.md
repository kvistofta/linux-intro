Most programs, commands and scripts prints info on the screen. But what it really does is that it sends text to a stream that is called stdout (standard output, sometimes called stream 1). Internally it uses a function that is often called "echo", "print" or something similar. But that function does not send text directly to the screen but to the standards output stream 1, stdout.

By default, everything that is sent to stdout is sent to the screen for us to see. However, we can redirect this text to a file with the ">" sign (greater than, pointing towards right). An example:

```shell
jimmy@bettan:~$ echo "Jimmy was here"
Jimmy was here
jimmy@bettan:~$
```

The `echo`-command is the "print"-command in bash. It prints the text to the screen. this is useful in scripts and as you can see the text echoed is printed on the screen on the next line, above.

If we however do like this:

```shell
jimmy@bettan:~$ echo "Jimmy was here" > jimmysfile
jimmy@bettan:~$
```

Nothing is echoed. However, there is a newly created file:

```shell
jimmy@bettan:~$ ls -l jimmysfile
-rw-rw-r-- 1 jimmy jimmy 15 Dec  9 16:47 jimmysfile
jimmy@bettan:~$
jimmy@bettan:~$ cat jimmysfile
Jimmy was here
jimmy@bettan:~$
```

We can clearly see that ">" redirects the output to the command on the left side to a file specified to the right of the command:

```shell
jimmy@bettan:~$ anycommand > anoutputfile
```

If you try to do this repeatedly you will notice that the output file will be truncated every time. The existing content will be overwritten and lost:

```shell
jimmy@bettan:~$ echo "Jimmy was here" > jimmysfile
jimmy@bettan:~$ echo "Jimmy was here" > jimmysfile
jimmy@bettan:~$ echo "Jimmy was here" > jimmysfile
jimmy@bettan:~$ cat jimmysfile
Jimmy was here
jimmy@bettan:~$
```

Sometimes you want another effect: appending. Scenario: You want to write something to a log file. In that case it makes no sense overwriting the file which will give you a life with a log file containing always only one line, the last one.

To append text instead of overwriting the file you can use the ">>" combination (two larger than signs without any space or anything else between them):

```shell
jimmy@bettan:~$ echo "Jimmy was here once" > jimmysfile
jimmy@bettan:~$ echo "Jimmy was here twice" >> jimmysfile
jimmy@bettan:~$ echo "Jimmy was here again..." >> jimmysfile
jimmy@bettan:~$ cat jimmysfile
Jimmy was here once
Jimmy was here twice
Jimmy was here again...
jimmy@bettan:~$
```

(In a later section I will explain the stderr stream, standard stream 2. You can redirect stderr to a file with `command 2> file`  or `command 2>> file` aswell.)

