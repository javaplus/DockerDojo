##### Windows git terminal

Assuming the index.html file is in the C:\tmp\html folder.
```bash
docker run -p 8080:80 -v c:/tmp/html:/usr/share/nginx/html nginx
```

### Windows command prompt/powershell
```dos
docker run -p 8080:80 -v c:\tmp\html:/usr/share/nginx/html nginx
```
