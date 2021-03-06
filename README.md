# Why Creating this repository

This repository is derived from [jaspeen/oracle-11g](https://github.com/jaspeen/oracle-11g). Thank jaspeen for his great job!!!
Changes are made for:
* resolving the problem that installation hangs at 76%.
* adding vncserver dependencies to enable oracle dbca.

# Notice

Image for running Oracle Database 11g Standard/Enterprise. Due to oracle license restrictions image is not contain database itself and will install it on first run from external directory.

``This image for development use only``

# Usage

This repository has no registerd image in docker hub. You need to build image by yourself.

## build image
cd into parent directory of _oralce11g_, then run command:
```sh
docker build -t <image_name> oracle11g
```
If succeeding, you will see this new image.
```sh
docker images
```
Note that if you run build in linux, some files may need to be converted to unix format, i.e.
```
dos2unix oracle11g/assets/*
```
## get oracle database packages

Download database installation files from [Oracle site](http://www.oracle.com/technetwork/database/in-memory/downloads/index.html) and unpack them to **install_folder**. For instance, unpacking oracle packages gives you _/home/oracle/install/database_. Then __install_folder__ should be _/home/oracle/install/_ .

## run container
Run container and it will install oracle and create database:

```sh
docker run --privileged --name oracle11g -p 1521:1521 -v <install_folder>:/install <image_name>
```

## build image with oracle

Then you can commit this container to have installed and configured oracle database:
```sh
docker commit oracle11g oracle11g-installed
```

## output image to disk
```sh
docker save oracle11g-installed | gzip > oracle11g-installed.tar.gz
```
