### Using sed within BusyBox and read and write to host file system

Assuming your lying.txt file is in c:\tmp\starwars

```dos
docker run -it -v C:\tmp\starwars:/usr/starwars busybox sh

/# sed 's/best/worst/' /usr/starwars/lying.txt > /usr/starwars/truth.txt


```


This answer is for the part 2... that is a one liner.

## Windows 

###### using windows Command Prompt
```
docker run -v C:\tmp\starwars:/usr/starwars busybox sh -c "sed 's/best/worst/' /usr/starwars/lying.txt > /usr/starwars/truth.txt"

```


###### using Windows git bash
```
docker run -v C:/tmp/starwars:/usr/starwars busybox sh -c "sed 's/best/worst/' /usr/starwars/lying.txt > /usr/starwars/truth.txt"

```

### linux or Mac

assuming lying.txt is in /tmp/starwars
```
docker run -v /tmp/starwars:/usr/starwars busybox sh -c "sed 's/best/worst/' /usr/starwars/lying.txt > /usr/starwars/truth.txt"

```
