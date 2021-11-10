# Docker and Kubernetes Dojo
Tutorial on Using Docker

## Presentation

This is provided to those that attended an in-person workshop who wish to reference back to topics discussed.  Much of the context is missing for those that did't attend, however it is not required material in order to proceed with the rest of the workshop below.

## Pre-requisites:

Generally speaking you need to have the Git client and Docker installed locally.

#### A console or shell environment

Some basic skills working with command line tooling are required to complete this tutorial as you will interact with the CLI often throughout.  Windows Command prompt or Powershell is recommended for Window's users.  MacOS and Linux users can use their shell of choice.  It will be called out where there is a difference in CLI statements for Windows vs MacOS/Linux users.


#### Git
If you don't already have a Git Client, you can download the Git tools from here:
 - https://git-scm.com/downloads


#### Docker & Kubernetes:

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

# ~~ Labs ~~

1. [Intro to Docker and Containers](labs/docker_intro.md)

1. [Docker with Cloud Native App](labs/docker_cloud_app.md)

1. [Docker for Tooling](labs/docker_tools_container.md)




---




# ~~ Conclusion ~~

This exercise has introduced you to some of the most commonly used features of Kubernetes for configuring and hosting applications using declarative, Infrastructure as Code techniques.  Even what we've shown here only begins to scratch the surface.  Here are other topics you'll want to dig deeper on as you continue your Kubernetes journey.

* [Managing Compute Resources for Containers](https://kubernetes.io/docs/concepts/configuration/manage-compute-resources-container/)
* [Declaring and using ConfigMaps to configure a Deployment](https://kubernetes.io/docs/tasks/configure-pod-container/configure-pod-configmap/)
* [Declaring and using Secrets to configure a Deployment](https://kubernetes.io/docs/concepts/configuration/secret/)
