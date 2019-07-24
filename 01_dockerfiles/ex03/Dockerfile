FROM debian

RUN apt-get update -y && apt-get upgrade -y
RUN apt-get install git -y
RUN apt-get install wget -y
RUN apt-get install gcc -y

WORKDIR $HOME/local
RUN wget https://storage.googleapis.com/golang/go1.8.linux-amd64.tar.gz
RUN tar -xzvf go1.8.linux-amd64.tar.gz

ENV GOROOT=$HOME/local/go
ENV GOPATH=$HOME/gogs
ENV PATH=$PATH:$GOROOT/bin:$GOPATH/bin

WORKDIR $GOPATH/src/github.com/gogs

#DOWNLOAD GOGS FROM DEVELOP BRANCH
RUN git clone --depth=1 -b develop https://github.com/gogs/gogs
RUN go get -u -tags "sqlite" github.com/gogs/gogs
WORKDIR $GOPATH/src/github.com/gogs/gogs
RUN go build -tags "sqlite"

RUN mkdir $GOPATH/src/github.com/gogs/logs
RUN mkdir /root/gogs-repositories
RUN mkdir /root/data

EXPOSE 3000

ENV USER=root

ENTRYPOINT ./gogs web

# 
# build docker image with:
# 		docker build -t ex03 path/to/dockerfile
# 
# then start the dockerised image with:
# 		docker run -it --rm -p 3000:3000 ex03
# 
# Use SQLITE FOR GOGS DEV