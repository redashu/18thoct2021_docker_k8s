# Plan of training 

<img src="plan.png">


## agenda day 2

<img src="day2.png">

## TIPs 

### remove all the contaienrs

```
 docker rm $(docker ps -aq) -f
5c6c0228043b
6c0e36f56ba9

```

### remove one or all the images

```
 77  docker  rmi  33f742df6215
   78  docker  rmi $(docker images -q) -f
   
```



## app containerization 

### Building images 

<img src="build.png">

### Building python based code to image 

<img src="py.png">

### Dockerfile for python code 

```
FROM python
# i am using python image from docker hub image 
# it will be automatically pulled by Docker engine if not present
LABEL name=ashutoshh
LABEL email=ashutoshh@linux.com
# optional field but good to share info 
RUN  mkdir  /mycode 
# RUN to get shell during image build time 
COPY  hello.py  /mycode/hello.py 
# copy code during image build time but make Dockerfile and code Location are
# same  / respective  
CMD  ["python","/mycode/hello.py"]
# CMD is to define default process for this Docker image
# here We are having python code run format as my default process

```

### Buiding image

```
[ashu@ip-172-31-19-234 python_apps]$ docker  build  -t  ashupython:v1  .  
Sending build context to Docker daemon  3.584kB
Step 1/6 : FROM python
latest: Pulling from library/python
bb7d5a84853b: Pull complete 
f02b617c6a8c: Pull complete 
d32e17419b7e: Pull complete 
c9d2d81226a4: Pull complete 
3c24ae8b6604: Pull complete 
8a4322d1621d: Pull complete 
2412fd0e5000: Pull complete 
0c700e8025db: Pull complete 
6e1cb03c0153: Pull complete 
Digest: sha256:d0075399d5663b0d8619d0260dddccee7b2ee8e6c66be441ba088607d3cc7e05
Status: Image is up to date for python:latest
 ---> c05c608cfa20
Step 2/6 : LABEL name=ashutoshh
 ---> Running in a97ccf6e3cf7
Removing intermediate container a97ccf6e3cf7
 ---> 5facd7b1e843
Step 3/6 : LABEL email=ashutoshh@linux.com
 ---> Running in 98d3a10bb39a
Removing intermediate container 98d3a10bb39a
 ---> f404f7b785f1
Step 4/6 : RUN  mkdir  /mycode
 ---> Running in 292b50c52075
Removing intermediate container 292b50c52075
 ---> 0dccb084f41c
Step 5/6 : COPY  hello.py  /mycode/hello.py
 ---> cbfed823dbfe
Step 6/6 : CMD  ["python","/mycode/hello.py"]
 ---> Running in a17a32fa0f89
Removing intermediate container a17a32fa0f89
 ---> 42f66a00af17
Successfully built 42f66a00af17
Successfully tagged ashupython:v1

```

### checking images

```
[ashu@ip-172-31-19-234 python_apps]$ docker  images
REPOSITORY         TAG       IMAGE ID       CREATED          SIZE
megha              v1        140d3ae1444c   22 seconds ago   915MB
nischalpython      v1        6f1ab2082b50   49 seconds ago   915MB
ashupython         v1        42f66a00af17   49 seconds ago   915MB

```

### creating and checking container 

```
[ashu@ip-172-31-19-234 python_apps]$ docker  run  -it  -d --name ashuc11  ashupython:v1  
351d28007c4b7f5149ef023857b91606b35e3d7c843a0db82c79192ed917b07f
[ashu@ip-172-31-19-234 python_apps]$ docker  ps
CONTAINER ID   IMAGE              COMMAND                  CREATED         STATUS         PORTS     NAMES
5215649c1a4e   manipython:v1      "python /mycode/hell…"   2 seconds ago   Up 1 second              manic2
319c45a141dd   dine:v1            "python /din/hello.py"   3 seconds ago   Up 2 seconds             din_container
2cde63ee598e   nischalpython:v1   "python /code/hello.…"   3 seconds ago   Up 2 seconds             nischalc1
351d28007c4b   ashupython:v1      "python /mycode/hell…"   5 seconds ago   Up 3 seconds             ashuc11

```

### checking output of code execution 

```
[ashu@ip-172-31-19-234 python_apps]$ docker logs -f  ashuc11
Hello all , welcome to python..!!
Welcome to Oracle Team..
Welcome to Containers ..!!
______________________
Hello all , welcome to python..!!
Welcome to Oracle Team..
Welcome to Containers ..!!

```

### checking resources of a container 

```
docker  stats  ashuc11


CONTAINER ID   NAME      CPU %     MEM USAGE / LIMIT    MEM %     NET I/O      BLOCK I/O     PIDS
351d28007c4b   ashuc11   0.01%     5.359MiB / 7.69GiB   0.07%     1.1kB / 0B   0B / 9.22kB   1
^C

===
C
[ashu@ip-172-31-19-234 python_apps]$ docker  stats  

781499279a3   vidhic1         0.01%     5.309MiB / 7.69GiB   0.07%     920B / 0B    0B / 12.8kB   1
112cc990c0ad   raju            0.00%     5.332MiB / 7.69GiB   0.07%     990B / 0B    0B / 18.4kB   1
912ff1508c77   umancont11      0.00%     5.418MiB / 7.69GiB   0.07%     990B / 0B    0B / 9.22kB   1
5215649c1a4e   manic2          0.00%     5.273MiB / 7.69GiB   0.07%     920B / 0B    0B / 19.5kB   1
319c45a141dd   din_container   0.00%     5.066MiB / 7.69GiB   0.06%     920B / 0B    0B / 11.8kB   1
2cde63ee598e   nischalc1       0.01%     3.047MiB / 7.69GiB   0.04%     710B / 0B    0B / 0B       1
351d28007c4b   ashuc11         0.00%     5.359MiB / 7.69GiB   0.07%     1.1kB / 0B   0B / 9.22kB   1

```


### access container 

```
[ashu@ip-172-31-19-234 python_apps]$ docker  exec -it   ashuc11   bash 
root@351d28007c4b:/# 
root@351d28007c4b:/# 
root@351d28007c4b:/# 
root@351d28007c4b:/# cat  /etc/os-release 
PRETTY_NAME="Debian GNU/Linux 11 (bullseye)"
NAME="Debian GNU/Linux"
VERSION_ID="11"
VERSION="11 (bullseye)"
VERSION_CODENAME=bullseye
ID=debian
HOME_URL="https://www.debian.org/"
SUPPORT_URL="https://www.debian.org/support"
BUG_REPORT_URL="https://bugs.debian.org/"
root@351d28007c4b:/# cd  /mycode/
root@351d28007c4b:/mycode# ls
hello.py
root@351d28007c4b:/mycode# 
root@351d28007c4b:/mycode# exit
exit

```

### Docker build image history 

```
83  docker  build  -t  ashupython:v1  .  
   84  history 
   85  docker  images
   86  ls
   87  docker  images
   88  docker  run  -it  -d --name ashuc11  ashupython:v1  
   89  docker  ps
   90  history 
   91  docker  ps
   92  docker  inspect  ashupython:v1 
   93  history 
   94  docker ps
   95  docker logs -f  ashuc11
   96  history 
   97  docker  ps
   98  history 
   99  docker  ps
  100  docker  info 
  101  docker  ps
  102  docker  stats  ashuc11
  103  docker  stats  
  104  history 
  105  docker  exec -it   ashuc11   bash 
  106  history 
  
  ```
  
  
### killing all running containers

```
[ashu@ip-172-31-19-234 python_apps]$ docker kill  $(docker ps  -q)
3c645a5cc4a4
30661233c34c
0a76cfcda5e4
f8caf0660cd5
7a3da97424d9
f28d5616e6e4

```

### removing all containers 

```
docker rm  $(docker ps  -aq)
```

### ANSwer to first Question 

```
[ashu@ip-172-31-19-234 ashuimages]$ docker  run -itd --name ashuc1 alpine ping localhost 
328b3e709419028baa88f480fb6c7985b9542d49bbc2ccace03e8f11aa34e5f6
[ashu@ip-172-31-19-234 ashuimages]$ docker  run -itd --name ashuc2 alpine ping localhost 
0c694b4bc342fcdcc84967fda9e96ba799e5c9b7e8ea83d74dcd9e2c81995e3a
[ashu@ip-172-31-19-234 ashuimages]$ docker  exec -it ashuc1 sh 
/ # ls
bin    etc    lib    mnt    proc   run    srv    tmp    var
dev    home   media  opt    root   sbin   sys    usr
/ # echo  hello  >helloc1.txt 
/ # ls
bin          helloc1.txt  media        proc         sbin         tmp
dev          home         mnt          root         srv          usr
etc          lib          opt          run          sys          var
/ # exit
[ashu@ip-172-31-19-234 ashuimages]$ docker  cp   ashuc1:/helloc1.txt  . 
[ashu@ip-172-31-19-234 ashuimages]$ ls
helloc1.txt  python_apps
[ashu@ip-172-31-19-234 ashuimages]$ docker  cp  helloc1.txt  ashuc2:/
[ashu@ip-172-31-19-234 ashuimages]$ docker  exec -it  ashuc2 sh 
/ # ls
bin          helloc1.txt  media        proc         sbin         tmp
dev          home         mnt          root         srv          usr
etc          lib          opt          run          sys          var
/ # exit

```

