## Containerize a Python app

For this exercise, you will take an existing Python application and use the Dockerfile within it to build a Docker image from it and run it.

#### Clone this repository

You'll be working with this repository and configuration contanied within.  Clone it to a location of your choosing and open the directory in VS Code.

> TIP: Run the following command from a directory containing no paths with spaces or backed up by Onedrive.

```bash
git clone https://github.com/javaplus/DockerDojo.git
```

After cloning the repo locally, take a look at the Dockerfile at the root of the project.

Look at the Dockerfile:

```
FROM python:3

WORKDIR /usr/src/app

COPY requirements.txt ./
RUN pip install --no-cache-dir -r requirements.txt

COPY . .

CMD [ "python", "./app.py" ]
```

This docker file simply starts with a pre-existing image that has python installed and then copies the local source code and requirements to the image and states that the command to run when the container starts is "python ./app.py".  That is start the python app.

These are the instructions that tell docker how to build this image.  We will now use this file to create a Docker image with our app.

Now open a command prompt to the root of the project where the Dockerfile resides.
Run the docker build command like this:

```

docker build -t python-demo:1 .

```
NOTE: There is a period at the end of that command and it is important!

The -t tells Docker to tag this image with the name "python-demo" and create version "1".  The '.' at the very end tell docker where to find the Dockerfile.  In our case, this is the current directory, thus the '.'.

You should see something like this(NOTE: the output below is abbreviated):

```
D:\workspaces\DockerKubesDojo>docker build -t python-demo:1 .
Sending build context to Docker daemon  118.3kB
Step 1/7 : FROM python:3
3: Pulling from library/python
8f0fdd3eaac0: Pull complete
...
644b4ceca849: Pull complete
50f0ac11639a: Pull complete
Digest: sha256:58666f6a49048d737eb24478e8dabce32774730e2f2d0803911a2c1f61c1b805
Status: Downloaded newer image for python:3
 ---> 038a832804a0
Step 2/7 : WORKDIR /usr/src/app
 ---> Running in baed9580915a
Removing intermediate container baed9580915a
 ---> e1dda44d0516
Step 3/7 : COPY requirements.txt ./
 ---> 378440b0c12f
Step 4/7 : RUN pip install --no-cache-dir -r requirements.txt
 ---> Running in 665a20dc436e
Step 6/7 : COPY . .
 ---> bff7b9c68fd1
Step 7/7 : CMD [ "python", "./app.py" ]
 ---> Running in a4cdc2564677
Removing intermediate container a4cdc2564677
 ---> ef5bc3de4d4f
Successfully built ef5bc3de4d4f
Successfully tagged python-demo:1
SECURITY WARNING: You are building a Docker image from Windows against a non-Windows Docker host. All files and directories added to build context will have '-rwxr-xr-x' permissions. It is recommended to 
double check and reset permissions for sensitive files and directories.
```
Now if you run a **docker images** command, you should see your newly created image:
```
D:\workspaces\DockerKubesDojo>docker images
REPOSITORY                           TAG                 IMAGE ID            CREATED             SIZE
python-demo                    1                   ef5bc3de4d4f        17 minutes ago      943MB
nginx                                latest              f7bb5701a33c        5 days ago          126MB
python                               3                   038a832804a0        5 days ago          932MB

```


## Run the python-demo image and expose its port

Now we are ready to run our newly created image.  To do that we are going back to the Docker run command you should be familar with.

> HINT: The string `python-demo:1` captures the coordinates of the Docker/OCI image.  It follows the pattern `{hostname to retrieve image}/{repository name}/{image name}:{tag}`.  Since we have it locally we don't specify a hostname to retrieve the image.

> HINT: The `--rm` just cleans up any remaining bits after this application runs.  It's completely stateless, so we don't need to remember anything about its execution in this scenario.

> HINT: The `-p` switch exposes the port the container listens on to your localhost interface.

```bash
docker run --rm -it -p 5000:5000 python-demo:1
```

## Validate the application container is running

In your browser, navigate to the URL [http://localhost:5000](http://localhost:5000).  You should see a JSON response with some information about the running application.  If not, double check the `docker run ...` command you issued and look for any errors in the console output.

If it's working, celebrate!  You successfully built and ran your own image!

## Stop the container

In the window where you issued the `docker run ...` command, type `CTRL+C` to stop the container.
Previously hitting `CTRL+C` in the command prompt wouldn't stop the container.  However, if you run the **docker ps** command now, you shouldn't see any containers running.  This is because when we issued the run command this time we added the `--rm` which stops the container automatically when you break.
