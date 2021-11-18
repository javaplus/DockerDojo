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

