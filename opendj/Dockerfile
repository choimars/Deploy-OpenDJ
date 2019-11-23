FROM jboss/base-jdk:8
  
LABEL maintainer="CMARS <cmars@triangles.co.kr>"

USER root

ENV TZ=Asia/Seoul
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

ENV INSTALL_PATH=/opt/opendj
ENV ROOT_USER_DN=cn=DirectoryManager
ENV ROOT_PASSWORD=ghktjddl9337
ENV HOST_NAME=localhost
ENV BASE_DN=dc=triangles,dc=co,dc=kr
ENV LDAPS_ADMIN_PORT=4444
ENV LDAP_PORT=1389
ENV LDAPS_PORT=1636
ENV HTTPS_PORT=8443
ENV SAMPLE_DATA=30
ENV VERSION=6.5.0

RUN yum update -y
RUN yum upgrade -y
RUN yum install -y wget unzip


WORKDIR /opt

RUN wget http://share.triangles.kr/FILES/OpenDJ/opendj-$VERSION.zip && \
  unzip opendj-$VERSION.zip && \
  rm -r opendj-$VERSION.zip


RUN  /opt/opendj/setup directory-server \
          --instancePath $INSTALL_PATH \
          --rootUserDn $ROOT_USER_DN \
          --rootUserPassword $ROOT_PASSWORD \
          --hostname $HOST_NAME \
          --baseDn $BASE_DN \
          --adminConnectorPort $LDAPS_ADMIN_PORT \
          --ldapPort $LDAP_PORT \
          --ldapsPort $LDAPS_PORT \
          --httpsPort $HTTPS_PORT \
          --sampleData $SAMPLE_DATA \
          --enableStartTls \
          --acceptLicense

EXPOSE 4444
EXPOSE 389
EXPOSE 1636
EXPOSE 8443

CMD ["/opt/opendj/bin/start-ds", "--nodetach"]
