# Plan of training 

<img src="plan.png">


## agenda day 2

<img src="day2.png">


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


