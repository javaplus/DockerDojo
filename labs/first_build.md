# ~~ The Mission ~~

You are responsible for taking applications other teams have developed and making them runnable as a Docker container.  The coding is already completed and the app can be packaged and run locally.  You must use the packaged code and the knowledge of how it runs to build a Dockerfile in order to build a Docker image for each app.

---

## Make your first Docker Image

Before you create your first Dockerfile, go to the official [Dockerfile reference documentation](https://docs.docker.com/engine/reference/builder/) and read the introduction(first paragraph) and the **Usage** sections to get a basic understanding of how a Dockerfile works.

Every Dockerfile should begin with a **FROM** instruction that tells Docker what image to start with when building your custom image.  According to the [official documentation](https://docs.docker.com/engine/reference/builder/#from), the **FROM** instruction also "initializes a new build stage and sets the Base Image for subsequent instructions.  So, it is not uncommon to see multiple **FROM** instructions in a Dockerfile, but we won't get that advanced with our lab examples.  Using mulitple **FROM** instructions is a key concept in [multi-stage builds](https://docs.docker.com/develop/develop-images/multistage-build/) which allow you to shrink your final image size.

#### If you build it they will come

Before we jump into containerizing application code, we will start by creating a simple custom Docker image.  This first Docker image will simply package some custom HTML into an NGINX server.  NGINX is a web server as well as other things, but we will use it to simply serve up our own static HTML pages.  So, the idea is that we will create one custom HTML file and build an image that has our custom HTML file served by NGINX.  

So, what are you waiting for... make your first Dockerfile... below are the general steps to follow

#### Steps
 - Create a new folder for your work
 - Create your own custom HTML file called **index.html**. 
 - Edit the **index.html** to have your own custom message. (It can simply have the text "HELLO WORLD" if you want.) It does not have to be valid HTML.
 - Create a simple file named "Dockerfile" with no extension. 
 - Edit the Dockerfile in an editor (like VS Code, Notepad++, etc..) and set the base of nginx (that is **FROM nginx**)
 - Use the [COPY](https://docs.docker.com/engine/reference/builder/#copy) command to copy your custom HTML file into the image (The destination inside the image can be determined from the nginx "How to use ths image" section on [hub.docker.com](https://hub.docker.com/_/nginx)
 - Once your Dockerfile is complete (yes there's only two lines required: the **FROM** line and the **COPY** line), you can build your image with the following command:  
   ```
     docker build -t mynginx:1 .
   ``` 
    NOTE: There is a period at the end of that command and it is important!
 - Ultimately, when finished buiding your image, you should be able to do a simple docker run with only the "-p 8080:80" option to publish your port and your custom image name. ex: **docker run -p 8080:80 mynginx:1**
  
#### Testing Your Custom Image

Once your docker container is running you can just open a browser to [http://localhost:8080](http://localhost:8080) and if everything worked right you should see your custom index.html displayed.

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

## Build a Java SpringBoot Application
 
For this exercise, we will be creating a Dockerfile for a SpringBoot app that can be found in this repo: **TO BE ADDED**

This app should be familar as it was used during the Developer Mindset and Java Tooling pre-requisite class.

#### General Advice for Dockerizing an Application
To Dockerize any application, it's critical to understand the requirements to run the app.  

The following items need to be identified(NOTE: This is not an exhaustive list):
1. **Required Software**: Software, app, tools, etc that are required to run the app. What would you have to install on your machine or a server to run the app?  
    - Examples: For a java app: do you need an app server like Tomcat or simply need a JDK or JRE. A Python app may need Python and Pip.
1. **Configs**: Are there any configuration files that need added to the system? If so, where do they need to go. 
    - Examples: Configuring an [httpd server](https://hub.docker.com/_/httpd) may require a custom httpd.conf file. An nginx server may require you to add your own nginx.conf file.  A custom application may require it's own configs;however, our applications should be following the [Config](https://12factor.net/config) methodology of "The Twelve-Factor App" that states: **"The twelve-factor app stores config in environment variables"**
1. **Application Code**: Where do we get the bundled app code and where does it need to be installed.
    - Examples: For a Java web app running on tomcat it may need to be in the catalina home webapps folder.  For a Python app or SpringBoot executable jar, it could go most anywhere.
1. **Startup Command**: What command do I need to issue to start my application.
    - Examples:  For a Java web app on tomcat, you only need to start the tomcat server which the base image handles for you.  For a SpringBoot executable jar, you simply need a **java -jar \<myjar.jar>** command.  A Python app may just need a **python \<myapp.py>** command.
    
#### Dockerizing Our SpringBoot Demo App

For our SpringBoot app here's the list of important items for Dockerizing the app:

1. **Required Software**: For a [SpringBoot executable jar](https://docs.spring.io/spring-boot/docs/current/reference/html/appendix-executable-jar-format.html), only a JDK is necessary.  
1. **Configs**: For our simple SpringBoot we do not have any special configs.
1. **Application Code**:  Our application, once packaged, consists of a single jar file that needs copied into the image.  The application was built through Maven following the [instructions]() you most likely did as a pre-requisite for this training.  You do not have to build the application for this lab, but instead you will pull the already built jar file from [Artifactory]() where the packaged jar has already been published. A common location and naming convention is to just put the jar in the **/usr/app/** directory and call it **app.jar**.
1. **Startup Command**:  Our app will just require the **java -jar <path_to_jar/jarname.jar>** to start the applicaiton

**Getting Started**
To start on creating the Dockerfile for this app, go ahead and copy the [Dockerfile from here]() to your local machine into an empty folder.  This Dockerfile will have more details and even the link to the jar in **.

Edit the Dockerfile to properly produce an image that will run our application.  Remember you can copy the jar locally before building the image or have the docker build pull the jar from ** directly.

Once you have your Dockerfile completed you can open a terminal/command prompt at the location of the Dockerfile and run this command to build a local image:
```
    docker build -t java-app:1 .
```
NOTE: Again remember the '.' at the end of the command which tells docker it can find the Dockerfile in the current directory.

Once your image is successfully built, you can run a container with this command:
```
    docker run -p 8080:8080 java-app:1
```

##### Testing the Application

To test the application you can either open this link [http://localhost:8080/hello](http://localhost:8080/hello) in a browser or curl the url like this:

```
curl http://localhost:8080/hello
```
Either way, you should see the output
```
Hello From Your Super Duper Spring Boot app!
```

## Additional Resources:

 - Official [Dockerfile Reference docs](https://docs.docker.com/engine/reference/builder/)
 - Help control the Docker image sizes by understanding [Multi-stage builds](https://docs.docker.com/develop/develop-images/multistage-build/)
 
