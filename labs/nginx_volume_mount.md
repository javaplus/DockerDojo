**It's recommended to read ALL the directions before starting!**

Your mission if you choose to accept it, is to run an nginx container that hosts your own created HTML file.
You will accomplish this by using the docker run command as you did earlier to create an nginx container, but this time you will use a [volume mount](https://docs.docker.com/storage/volumes/) to mount a local **folder** that contains an HTML file into the running container.

To know where to mount the file so that nginx will serve it up (and see an example), read the documenation for the nginx image.  You can find it by going to http://hub.docker.com and then searching for the nginx image.  Click on the Official nginx image and scroll to the bottom to find the "How to use this image" section.  The first example is of how to host simple static content.

So, first create your own HTML file and save it to a preferably simple/short path on your hard drive (i.e. C:\dev\dojo\index.html).

Now you will need to run the nginx container with the '-v' option and replace the "/some/content" with the path to the **folder** containing your newly created HTML.  NOTE: the example from hub.docker.com doesn't add the -p (publish port) option, so if you use it as is, you won't be able to access your nginx container... so add the "-p 8080:80" option to it along with the new volume option.  

**Note for Windows users:**  Older versions of Docker Desktop could run using Hyper-V technology, however, now it's recommended to use the newest version of Docker Desktop with WSL (Windows Subsystem for Linux) if that option is avaible for you.  If you are using an older version of Docker Desktop with Hyper-V, then in order for Docker desktop to access your local hard drive for the volume mount, you need to grant it permissions to your folder where your HTML exists.  You can do this by going to the Docker Desktop Settings and then go under Resources->File Sharing.  Then add the folder that contains your HTML.  

**NOTE:** If you are on Windows, you are best to run this command from the basic command prompt or powershell. Using something like git bash can confuse things since it typically expect linux style paths.

Also, be aware of the docker run syntax...
```
docker run [OPTIONS] IMAGE [COMMAND] [ARG...]
```

#### Stretch Goal

What would you have to do if you wanted to change the index.html?  Try adding new text to it.  Do you need to restart the container or can you just refresh the browser?

Volume mounts are an important concept to grasp especially anytime you need data to persist beyond the life of a container.
