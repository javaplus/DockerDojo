
## Build a Java SpringBoot Application
 
For this exercise, we will be creating a Dockerfile for a simple SpringBoot app that exposes a simple Rest API.  This is the same application you ran when using the javaplus/cloud-app-demo image earlier. However, this time you will be building the image yourself.  You will use the built application code to add to an image that will allow the application to run.  We will provide you with a link to the jar file. If intersted, the source code can be found in this repo: https://github.com/javaplus/CloudAppsDemo.
Before we get started, read through the general advice for considerations when building a Docker image.

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
1. **Application Code**:  Our application, once packaged, consists of a single jar file that needs copied into the image. You do not have to build the application for this lab, but instead you will pull the already built jar file from https://github.com/javaplus/CloudAppsDemo/raw/master/target/cloud-app-1.jar where the packaged jar has already been uploaded. A common location and naming convention is to just put the jar in the **/usr/app/** directory and call it **app.jar**.
1. **Startup Command**:  Our app will just require the **java -jar <path_to_jar/jarname.jar>** to start the applicaiton

**Getting Started**
To start on creating the Dockerfile for this app, go ahead and copy the [Dockerfile from here](https://github.com/javaplus/CloudAppsDemo/blob/master/Dockerfile) to your local machine into an empty folder.  This Dockerfile will have more details and even the link to the packaged application jar.

Edit the Dockerfile to properly produce an image that will run our application.  Remember you can copy the jar locally before building the image or have the docker build pull the jar from https://github.com/javaplus/CloudAppsDemo/raw/master/target/cloud-app-1.jar directly.

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
Hello From Your Super Duper Spring Boot app! (Properties file edition)
```

## Additional Resources:

 - Official [Dockerfile Reference docs](https://docs.docker.com/engine/reference/builder/)
 - Help control the Docker image sizes by understanding [Multi-stage builds](https://docs.docker.com/develop/develop-images/multistage-build/)
 
