FROM openjdk:8-jdk-alpine

ENV PAYARA_PATH /opt/payara

RUN   apk update \                                                                                                                                                                                                                        
 &&   apk add ca-certificates wget \                                                                                                                                                                                                      
 &&   update-ca-certificates && \
 mkdir -p $PAYARA_PATH/deployments && \
 adduser -D -h $PAYARA_PATH payara && echo payara:payara | chpasswd && \
 chown -R payara:payara /opt

ENV PAYARA_PKG payara-micro.jar

ENV PAYARA_VERSION 181
ENV PKG_FILE_NAME payara-micro.jar

#RUN wget --quiet -O $PAYARA_PATH/$PKG_FILE_NAME $PAYARA_PKG
COPY $PAYARA_PKG $PAYARA_PATH/$PKG_FILE_NAME
COPY ROOT.war /opt/payara/deployments
COPY postboot.txt /opt/payara

ENV DEPLOY_DIR $PAYARA_PATH/deployments
ENV AUTODEPLOY_DIR $PAYARA_PATH/deployments
ENV PAYARA_MICRO_JAR=$PAYARA_PATH/$PKG_FILE_NAME

# Default payara ports to expose
EXPOSE 5900 8080

USER payara
WORKDIR $PAYARA_PATH


ENTRYPOINT ["java", "-jar", "/opt/payara/payara-micro.jar"]
CMD ["--deploymentDir", "/opt/payara/deployments", "--postbootcommandfile", "/opt/payara/postboot.txt"]

