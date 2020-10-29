FROM payara/micro:5.2020.5 as build

FROM gcr.io/distroless/java:8
LABEL maintainer="qaware-oss@qaware.de"

ENV PAYARA_PATH /opt/payara
ENV DEPLOY_DIR $PAYARA_PATH/deployments
ENV AUTODEPLOY_DIR $PAYARA_PATH/deployments

RUN ["java", "-Xshare:dump"]

COPY --from=amd64/busybox:1.31.1 /bin/busybox /busybox/busybox
RUN ["/busybox/busybox", "--install", "/bin"]

COPY --from=build /etc/passwd /etc/passwd
COPY --from=build /etc/group /etc/group

COPY --from=build $PAYARA_PATH $PAYARA_PATH

USER payara
WORKDIR $PAYARA_PATH

# Default payara ports to expose
EXPOSE 8080 8443 6900

ENTRYPOINT ["java", "-server", "-Xshare:auto", "-XX:+UseContainerSupport", "-XX:MaxRAMPercentage=50.0", "-XX:ThreadStackSize=256", "-XX:MaxMetaspaceSize=128m", "-XX:+UseG1GC", "-XX:MaxGCPauseMillis=250", "-XX:+UseStringDeduplication", "-jar", "/opt/payara/payara-micro.jar"]
CMD ["--nocluster", "--disablephonehome", "--deploymentDir", "/opt/payara/deployments"]
