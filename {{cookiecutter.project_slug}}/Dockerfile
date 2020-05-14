FROM ubuntu
RUN apt-get update && apt-get -y upgrade
RUN apt-get -y install libcurl4
ADD minecraft.tar.bz2 /opt
COPY server.properties whitelist.json permissions.json /opt/minecraft/
WORKDIR /opt/minecraft
ENV LD_LIBRARY_PATH=/opt/minecraft
CMD /opt/minecraft/bedrock_server
EXPOSE 19132/udp
