FROM java

MAINTAINER Hayk Avetisyan

RUN wget https://www.atlassian.com/software/bamboo/downloads/binary/atlassian-bamboo-5.14.3.1.tar.gz

RUN tar xzvf atlassian-bamboo-5.14.3.1.tar.gz -C /srv/ && rm -rf atlassian-bamboo-5.14.3.1.tar.gz

ENV BAMBOO_INSTALL_DIR /srv/atlassian-bamboo
ENV BAMBOO_HOME_DIR /srv/atlassian/bamboo-home
ENV EC2_HOME /srv/ec2-api-tools
ENV EC2_CERT /srv/atlassian/bamboo-home/xml-data/configuration/20141030_090850_ebsCertificate.pem
ENV EC2_PRIVATE_KEY /srv/atlassian/bamboo-home/xml-data/configuration/20141030_090850_ebsPrivateKey.pem

RUN apt-get update && \
    apt-get install -y --force-yes --no-install-recommends \
    vim \
    less \
    net-tools

RUN ln -s /srv/atlassian-bamboo-5.14.3.1 /srv/atlassian-bamboo

COPY ./configurationData/bamboo-init.properties /srv/atlassian-bamboo/atlassian-bamboo/WEB-INF/classes/bamboo-init.properties

RUN mkdir -p /srv/atlassian/bamboo-home

WORKDIR  /srv/atlassian-bamboo/bin

#RUN wget https://jdbc.postgresql.org/download/postgresql-9.4.1212.jre6.jar -O /srv/atlassian-bamboo/lib/postgresql-9.4.1212.jre6.jar 

RUN wget http://s3.amazonaws.com/ec2-downloads/ec2-api-tools.zip && \
    unzip ec2-api-tools.zip -d /srv/ && \
    ln -s /srv/ec2-api-tools-1.7.5.1 /srv/ec2-api-tools && \
    rm -rf ec2-api-tools.zip

VOLUME /srv/atlassian/bamboo-home

EXPOSE 8085

CMD ["./start-bamboo.sh", "-fg"]