
# Pull base image.
FROM ubuntu:16.04

# 国内环境中使用时加上这个配置,可以提高后续的速度
# 在国外的vps主机上使用时,则没有必要使用镜像站,可以注释掉
RUN echo "deb http://mirrors.ustc.edu.cn/ubuntu/ xenial main restricted universe multiverse" > /etc/apt/sources.list 
RUN echo "deb http://mirrors.ustc.edu.cn/ubuntu/ xenial-updates main restricted universe multiverse" >> /etc/apt/sources.list 
RUN echo "deb http://mirrors.ustc.edu.cn/ubuntu/ xenial-backports main restricted universe multiverse" >> /etc/apt/sources.list 
RUN echo "deb http://mirrors.ustc.edu.cn/ubuntu/ xenial-security main restricted universe multiverse" >> /etc/apt/sources.list 

RUN  apt-get update && \
  apt-get -y upgrade && \
  apt-get install -y build-essential && \
  apt-get install -y software-properties-common && \
  apt-get install -y byobu curl git  procps htop man unzip vim wget tree  apt-transport-https && \
  rm -rf /var/lib/apt/lists/*

# Install Python.
RUN \
  apt-get update && \
  apt-get install -y python python-dev python-pip python-virtualenv ipython && \
  rm -rf /var/lib/apt/lists/*

# Install any missing dependencies for enhanced language service
RUN apt-get install -y libicu[0-9][0-9]

RUN pip install -i https://mirrors.ustc.edu.cn/pypi/web/simple --upgrade pip
COPY .devcontainer/requirements.txt /tmp/requirements.txt
RUN pip install -i https://mirrors.ustc.edu.cn/pypi/web/simple -r /tmp/requirements.txt

#设置语言支持中文
ENV LC_ALL C.UTF-8






RUN mkdir /workspace
WORKDIR /workspace


# Expose port 5000 as the default web port
EXPOSE 5000

# Clean up
RUN apt-get autoremove -y \
    && apt-get clean -y \
    && rm -rf /var/lib/apt/lists/*
