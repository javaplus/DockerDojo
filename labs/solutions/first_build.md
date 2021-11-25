## Building your first ngnix image with custom html files:

Assuming you have your custom index.html in the same location as your Dockerfile:

#### Dockerfile
```
FROM nginx
COPY index.html /usr/share/nginx/html
```

Run this command to build it:

```
docker build -t mynginx:1 .
```

Then run this command to run it:

```
docker run -p 8080:80 -d mynginx:1
```
