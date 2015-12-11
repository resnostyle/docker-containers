FROM resnostyle/base
MAINTAINER bwp.pearson@gmail.com

ENV CONSUL_VER 0.5.2

RUN yum install -y wget && \
    wget https://releases.hashicorp.com/consul/${CONSUL_VER}/consul_${CONSUL_VER}_linux_amd64.zip && \
    yum purge -y wget 


#VOLUME /config
#VOLUME /data

#EXPOSE 8081

