FROM debian

RUN apt-get update -y && apt-get upgrade -y
RUN apt-get install curl -y
RUN apt-get install bzip2 -y

EXPOSE 9987/udp
EXPOSE 30033
EXPOSE 10011
EXPOSE 41144

RUN useradd ts3
WORKDIR /home/t3

RUN curl http://dl.4players.de/ts/releases/3.0.13.6/teamspeak3-server_linux_amd64-3.0.13.6.tar.bz2 > teamspeak-server.tar.bz2 
RUN tar -xjvf teamspeak-server.tar.bz2
WORKDIR teamspeak3-server_linux_amd64
COPY ts3server.ini /home/ts3/teamspeak3-server_linux_amd64/ts3server.ini
USER ts3
ENTRYPOINT ["sh","ts3server_minimal_runscript.sh", "inifile=ts3server.ini"]
# 
# build docker image with:
# 		docker build -t ex01 path/to/dockerfile
# 
# then start the dockerised image with:
# 		docker run -it --rm -p 9987:9987/udp -p 10011:10011 -p 30033:30033 -p 41144:41144 ex01
# ADD copy command to expose port for Teamspeak
#