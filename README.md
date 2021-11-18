# Docker Dojo
Hands-on Tutorial for learning Docker!  This is a collection of tutorials and exercises that help you get familar with Docker.
All interaction with Docker is done using the Docker CLI through the command-line/terminal. There are tutorials which walk you through what to do and there are labs which  provide challenges to test out what you've learned.  Don't worry there are solutions if you get stuck or want to check if you came up with the same way of solving the problem as us.

If you'd like to have me guide you or your team through this training feel free to reach out to me @ btarlton@gmail.com.

## Pre-requisites:

Generally speaking you need to have the Git client and Docker installed locally (see links and details below).

#### A console or shell environment

Some basic skills working with command line tooling are required to complete this tutorial as you will interact with the CLI often throughout.  Windows Command prompt or Powershell is recommended for Window's users.  MacOS and Linux users can use their shell of choice.  It will be called out where there is a difference in CLI statements for Windows vs MacOS/Linux users.


#### Git
If you don't already have a Git Client, you can download the Git tools from here:
 - https://git-scm.com/downloads


#### Docker:

Here are links and instructions per operating system:


##### Windows
- Windows 10 64-bit: Pro, Enterprise, or Education (Build 15063 or later)
    - Docker Desktop Download which Includes Kubernetes: https://www.docker.com/products/docker-desktop
    - Docker Desktop Install Guide - https://docs.docker.com/docker-for-windows/install/

##### Mac
  - Docker Desktop for Mac : https://hub.docker.com/editions/community/docker-ce-desktop-mac

### Testing your Installation

Run the **docker version** command and you should see something like this:
```
C:\Users\barry>docker version
Client: Docker Engine - Community
 Version:           19.03.5
 API version:       1.40
 Go version:        go1.12.12
 Git commit:        633a0ea
 Built:             Wed Nov 13 07:22:37 2019
 OS/Arch:           windows/amd64
 Experimental:      false

Server: Docker Engine - Community
 Engine:
  Version:          19.03.5
  API version:      1.40 (minimum version 1.12)
  Go version:       go1.12.12
  Git commit:       633a0ea
  Built:            Wed Nov 13 07:29:19 2019
  OS/Arch:          linux/amd64
  Experimental:     false
 containerd:
  Version:          v1.2.10
  GitCommit:        b34a5c8af56e510852c35414db4c1f4fa6172339
 runc:
  Version:          1.0.0-rc8+dev
  GitCommit:        3e425f80a8c931f88e6d94a8c831b9d5aa481657
 docker-init:
  Version:          0.18.0
  GitCommit:        fec3683
 Kubernetes:
  Version:          v1.14.8
  StackAPI:         v1beta2
```

#### Optional Pre-reqs (all OS's)
##### Install Visual Studio Code

You will be editing text files and viewing Python code during the course of this exercise.  You can use any text editor, but Visual Studio Code has many good extensions(aka plugins) and it's free.

[Download and install VS Code](https://code.visualstudio.com/)


##### Install the JSON Formatter Chrome Extension

This is a useful, but not required, Chrome extension for viewing JSON output in your browser.

[Install using a Chrome browser](https://chrome.google.com/webstore/detail/json-formatter/bcjindcccaagfpapjjmafapmmgkkhgoa)

---

# ~~ Content: Where the Fun Begins! ~~

Below is the recommended order of going through the training.  Those marked as "Tutorial" provide step-by-step instructions on what to do.  The "Lab" sections describe scenarios which you must use Docker to complete.

1. [Intro to Docker and Containers(Tutorial)](labs/intro.md)

1. [Volume Mounts with Nginx (Lab)](labs/nginx_volume_mount.md)

1. [Changing Local Files with Docker (Lab) ](labs/starwars_volume_mount.md)

1. [Using Environment Variables (Lab)](labs/run_webapp.md)

1. [Building Your Custom Image (Tutorial)](labs/first_build.md)

1. [Building Python Custom Image (Tutorial)](labs/build_python.md)

1. [Building Java Custom Image (lab)](labs/build_java.md)

1. [Make Cow Talk (Lab)](labs/cow_talk_1.md)

1. [Make Cow Talk 2 (Lab)](labs/cow_talk_2.md)




---




# ~~ Conclusion ~~


