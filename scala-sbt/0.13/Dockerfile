FROM andreptb/oracle-java:8-alpine

ENV SCALA_VERSION 2.11.8
ENV SBT_VERSION 0.13.11
ENV PATH ${PATH}:/usr/share/scala-${SCALA_VERSION}/bin:/usr/share/sbt/bin

RUN apk -U add curl bash \
    && curl --silent --fail http://downloads.lightbend.com/scala/2.11.8/scala-${SCALA_VERSION}.tgz | gunzip | tar x -C /usr/share/ \
    && curl -L --silent --fail https://dl.bintray.com/sbt/native-packages/sbt/${SBT_VERSION}/sbt-${SBT_VERSION}.tgz | gunzip | tar x -C /usr/share/ \
    && rm -rf /usr/share/scala-${SCALA_VERSION}/man \
    && adduser -D -h /sbt sbt \
    && mkdir -p /sbt/app && chown -R sbt. /sbt \
    && apk del build-dependencies \
    && rm -rf /var/cache/apk/*

USER sbt
WORKDIR /sbt/app

VOLUME ["/sbt/app", "/sbt/.ivy2", "/sbt/.sbt"]

ENTRYPOINT ["sbt"]
CMD [ "help" ]