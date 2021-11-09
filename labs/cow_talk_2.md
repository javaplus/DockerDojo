## Make the Cow Say Whatever the user wants.

In the previous lab, you created an image that installed the **cowsay** game/package and said something when the container was run.


Now you need to modify that image slightly to allow the user to provide an argument when they run the container that will allow the cow to speak what they want.

The easiest way to do this is to understand the difference between [CMD](https://docs.docker.com/engine/reference/builder/#cmd) and [ENTRYPOINT](https://docs.docker.com/engine/reference/builder/#entrypoint).

In the end, you should be able to run the new cowsay image like this:

```
$ docker run cowsay:2
 ________________________
< This can be overridden >
 ------------------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||

```

Or run it like this:

```
$ docker run cowsay:2 "Hello Bobby!"
 ______________
< Hello Bobby! >
 --------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||

```

Notice that if you run it without any argument after the docker run command it print's out a default message "This can be overridden".  
But if you pass an argument to the docker run, the cow will say your message.

You best get mooooving on this assignment!
