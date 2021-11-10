In this exercise, you will use a simple linux container with some text utilites pre-installed to do some file manipulation.  The goal here is to see how using Docker volume mounts you can expose folders and files from your file system (or other file systems) to the Docker container.  One valuable use case this allows you to take advantage is the ability to use tools/utilities that work with local files, without having to install anything permanently.

Create a [busybox](https://hub.docker.com/_/busybox) container that [mounts](https://docs.docker.com/storage/volumes/) a **folder** with a text file named **lying.txt** from your machine that has the following text in it:

```
Star Wars Episode 1 is the best movie of the franchise!

```
This text file is named **lying.txt** because obviously it is.  When you run your container and volume mount the folder containing this file, then this folder is accessible in the container.

Now use the [sed command](https://www.geeksforgeeks.org/sed-command-in-linux-unix-with-examples/) provided in busybox  to replace the word "best" with "worst" and write it to a new file.

```
  sed 's/best/worst/' lying.txt > truth.txt
```

So, the goal is to use the busybox container to run the sed command in order to read a file from your local machine and write out a new file onto your local machine.  This requires using a volume mount that allows the container to read and write to the folder.

Try doing it two ways:
  1. Using an interactive run session: That is using the docker run command with -it
  1. Using a docker run without an interactive session and passing all the commands on one line.
      1. HINT: using the "sh" command and the "-c" option you can pass a command as a string.
      
      
    

