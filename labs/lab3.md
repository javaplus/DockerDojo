Create a [busybox](https://hub.docker.com/_/busybox) container that [mounts](https://docs.docker.com/storage/volumes/) a **folder** with a text file from your machine that has the following text in it:

```
Star Wars Episode 1 is the best movie of the franchise!

```
You can name this text file **lying.txt** (because obviously it is).  Then when you run your container share the folder that this text file resides in as a volume.

Now use the [sed command](https://www.geeksforgeeks.org/sed-command-in-linux-unix-with-examples/) provided in busybox  to replace the word "best" with "worst" and write it to a new file.

```
  sed 's/best/worst/' lying.txt > truth.txt
```

So, the goal is to use the busybox container to run the sed command in order to read a file from your local machine and write out a new file onto your local machine.  This requires using a volume mount that allows the container to read and write to the folder.

Try doing it two ways:
  1. Using an interactive run session: That is using the docker run command with -it
  1. Using a docker run without an interactive session and passing all the commands on one line.
      1. HINT: using the "sh" command and the "-c" option you can pass a command as a string.
      
      
    

