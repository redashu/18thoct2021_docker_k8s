# Plan of training 

<img src="plan.png">

## day3 schedule

<img src="sch.png">

## REvision 

<img src="rev.png">

### CNA 

<img src="cna.png">

## Webapp COntainerization 

### pulling webapp code 

```

[ashu@ip-172-31-19-234 ashuimages]$ git  clone  https://github.com/mdn/beginner-html-site-styled
Cloning into 'beginner-html-site-styled'...
remote: Enumerating objects: 40, done.
remote: Total 40 (delta 0), reused 0 (delta 0), pack-reused 40
Receiving objects: 100% (40/40), 124.07 KiB | 15.51 MiB/s, done.
Resolving deltas: 100% (10/10), done.
[ashu@ip-172-31-19-234 ashuimages]$ ls
beginner-html-site-styled  helloc1.txt

```

### application server list

<img src="apps.png">

### Dockerfile and .dockerignore 

```
## Dockerfile :-

FROM oraclelinux:8.4 
LABEL email=ashutoshh@linux.com
RUN yum install httpd -y 
COPY . /var/www/html/
# COPY all the data from Dockerfile location to /var/www/html/
ENTRYPOINT httpd -DFOREGROUND
# to start httpd service we use 
#  systemctl start httpd ---> httpd -DFOREGROUND 

## .dockerignroe :-

LICENSE
*.md
Dockerfile
.dockerignore
.git
```

### building image 

```
[ashu@ip-172-31-19-234 ashuimages]$ ls
beginner-html-site-styled  helloc1.txt  python_apps
[ashu@ip-172-31-19-234 ashuimages]$ cd  beginner-html-site-styled/
[ashu@ip-172-31-19-234 beginner-html-site-styled]$ ls
CODE_OF_CONDUCT.md  Dockerfile  images  index.html  LICENSE  README.md  styles
[ashu@ip-172-31-19-234 beginner-html-site-styled]$ docker  build  -t  httpd:20oct2021v1   . 
Sending build context to Docker daemon  63.49kB
Step 1/5 : FROM oraclelinux:8.4
 ---> 521767a68c46
Step 2/5 : LABEL email=ashutoshh@linux.com
 ---> Running in 0f663b94cbf9
Removing intermediate container 0f663b94cbf9
 ---> 6ad9b2c17469
Step 3/5 : RUN yum install httpd -y
 ---> Running in 405a53b154c3
Oracle Linux 8 BaseOS Latest (x86_64)           120 MB/s |  36 MB     00:00    

```

### creating container 

```
docker  run -itd --name  ashuwebc1  -p  2233:80  httpd:20oct2021v1 
94b206d2157e691775d3fe1c2037b69a85a11c9b8598688447c52c4bea3516b0
[ashu@ip-172-31-19-234 beginner-html-site-styled]$ docker  ps
CONTAINER ID   IMAGE               COMMAND                  CREATED         STATUS         PORTS                                   NAMES
94b206d2157e   httpd:20oct2021v1   "/bin/sh -c 'httpd -…"   8 seconds ago   Up 6 seconds   0.0.0.0:2233->80/tcp, :::2233->80/tcp   ashuwebc1
[ashu@ip-172-31-19-234 beginner-html-site-styled]$ 

```


