## Make the Cow Talk

We are going to install a funny linux program into an ubuntu container to make an ASCII art cow say whatever we want.

At first we will walk through the steps of doing this manually and then you will create a Dockerfile to build a container that does all the steps.

Start by running an ubuntu container that's interactive and runs the bash or sh command.

```
docker run -it ubuntu bash
```

To install our **cowsay** package, we first need to update apt-get.

```
apt-get update
```

Next we will use apt-get to install the **cowsay** package/game.

```
apt-get install -y cowsay
```

By default this installs cowsay under **/usr/games** so we will add this to the **PATH** environment variable
```
export PATH=/usr/games:$PATH
```

Now we should be able to just run **cowsay** like this:
```
  cowsay "Let's keep MOOOOOving"
```

You should see something like this
```
root@c22bcbb191b9:/# cowsay "Let's keep MOOOOOving"
 _______________________
< Let's keep MOOOOOving >
 -----------------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||
root@c22bcbb191b9:/#
```

## Build the Docker image

Now that you know the steps to setup and run **cowsay** on ubuntu, create a Dockerfile and build an image from that file that when ran it will have the cow speak.

For example, **once you have created your Dockerfile**, you should be able to run the following command from the location of your Dockerfile:

```
  docker build -t cowsay:1 .
```
This will build and tag your image as **cowsay:1**.  After it has been successfully built, you should be able to run it like this:

```
docker run cowsay:1
```
And see this:

```
docker run cowsay:1
 _______________________
< Let's keep MOOOOOving >
 -----------------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||

```


