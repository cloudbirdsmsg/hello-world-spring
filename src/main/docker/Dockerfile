FROM adoptopenjdk/openjdk11:x86_64-alpine-jre-11.0.11_9

LABEL maintainer="nico.rogalski@msg-david.de" \
        ${project.groupId}.${project.artifactId}.project="cloudbirds" \
        ${project.groupId}.${project.artifactId}.version="${project.version}" \
        ${project.groupId}.${project.artifactId}.description="${project.description}"

ARG ARG_JAVA_APPLICATION=${project.build.finalName}.jar
ARG ARG_JAVA_APPLICATION_HOME=/home/spring

ENV JAVA_APPLICATION=${ARG_JAVA_APPLICATION} \
    JAVA_APPLICATION_HOME=${ARG_JAVA_APPLICATION_HOME} \
    JAVA_OPTS="" \
    DOCKER_JAVA_OPTS="" \
    SPRING_JAVA_OPTS=""

RUN echo "adding run user spring to system" \
    && addgroup -S spring -g 1000 \
    && adduser -S spring -u 1000 -G spring

COPY docker-entrypoint.sh /
COPY *.jar ${ARG_JAVA_APPLICATION_HOME}/

RUN chown spring:spring /docker-entrypoint.sh && \
    chmod u+x /docker-entrypoint.sh && \
    chown -R spring:spring ${ARG_JAVA_APPLICATION_HOME}

USER 1000

EXPOSE 8080

ENTRYPOINT ["/docker-entrypoint.sh"]
CMD ["java"]