FROM ubuntu:18.04 AS builder
RUN apt-get update && apt-get -y upgrade
RUN apt-get -y install unzip
WORKDIR /opt
COPY bedrock-server-*.zip bedrock-server.zip
RUN mkdir minecraft && unzip -d minecraft bedrock-server.zip

FROM ubuntu:18.04
RUN apt-get update && apt-get -y upgrade
RUN apt-get -y install libcurl4
COPY --from=builder /opt/minecraft /opt/minecraft/
COPY server.properties whitelist.json permissions.json /opt/minecraft/
WORKDIR /opt/minecraft
ENV LD_LIBRARY_PATH=/opt/minecraft
CMD ["/opt/minecraft/bedrock_server"]
EXPOSE 19132/udp
