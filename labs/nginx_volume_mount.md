**It's recommended to read ALL the directions before starting!**

Your mission if you choose to accept it, is to run an nginx container that hosts your own created HTML file.
You will accomplish this by using the docker run command as you did earlier to create an nginx container, but this time you will use a [volume mount](https://docs.docker.com/storage/volumes/) to mount a local **folder** that contains an HTML file into the running container.

To know where to mount the file so that nginx will serve it up (and see an example), read the documenation for the nginx image.  You can find it by going to http://hub.docker.com and then searching for the nginx image.  Click on the Official nginx image and scroll to the bottom to find the "How to use this image" section.  The first example is of how to host simple static content.

So, first create your own HTML file and save it to a preferably simple/short path on your hard drive (i.e. C:\dev\dojo\index.html).

Now you will need to run the nginx container with the '-v' option and replace the "/some/content" with the path to the **folder** containing your newly created HTML.  NOTE: the example from hub.docker.com doesn't add the -p (publish port) option, so if you use it as is, you won't be able to access your nginx container... so add the "-p 8080:80" option to it along with the new volume option.  

**Note:** In order for Docker desktop to access your local hard drive for the volume mount, you need to grant it permissions to your folder where your HTML exists.  You can do this by going to the Docker Desktop Settings and then go under Resources->File Sharing.  Then add the folder that contains your HTML.  Here's the [official documentation on file sharing](https://docs.docker.com/docker-for-windows/#file-sharing) with Docker Desktop.

NOTE: When you run the command the first time with a volume option, Docker will prompt you to ask you if you want to share the folder with Docker.  So, watch for a pop-up to ask you to share the folder.  Also, if you are on Windows, you are best to run this command from the basic command prompt or powershell. Using something like git bash can confuse things since it typically expect linux style paths.

Also, be aware of the docker run syntax...
```
docker run [OPTIONS] IMAGE [COMMAND] [ARG...]
```


