## how to run the cloud-app-demo with an environment variable:

```
docker run -p 8080:8080 -e mymessage="hello there from an environment variable" javaplus/cloud-app-demo

```

Another option is to define a local variable on your machine called "mymessage" and then it will use that value.
So, set an environment variable and then run the container without setting a value for the environment variable like this:

```
C:\Users\Barry>set mymessage=Howdy!

C:\Users\Barry>docker run -p 8080:8080 -e mymessage javaplus/cloud-app-demo

```
For linux or mac, use the "export" command instead of "set".
