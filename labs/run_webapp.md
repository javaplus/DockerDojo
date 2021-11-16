## Using Environment Variables

Now you will run a simple Java web app that displays a message based on an environment variable.  

To pull from this registry instead of Docker hub on the internet, you simple prefix the image name with the registry.

So, the image you will be working with is: **hello-message**

The beginning part, **""** is the registry host.  The next part, **""**, is an organization or user account within that registry.
Then finally the last part is the image name, **"hello-message"**.

When you run this image it will start a java webapplication (via SpringBoot) to listen for requests on port 8080 on the url "/hello".

So, run a container with this image **hello-message** (latest tag) so that you can connect to http://localhost:8080/hello and see the message: **Message from Properties File**

The message you see is being read from a properties file, but can be overridden by an enviornment variable named **mymessage**.

Your mission is to run the image and set the environment variable **mymessage** into the container so, that you see your custom message when you hit the "/hello" endopoint.

Here is the [Docker run reference material on how to set environment variables](https://docs.docker.com/engine/reference/run/#env-environment-variables).

Try setting the environment variable directly in the run line, both with a hard coded value inline as well as taking the value from a local environment variable (local- meaning on your machine).
