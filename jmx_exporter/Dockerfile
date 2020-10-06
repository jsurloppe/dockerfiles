FROM adoptopenjdk/openjdk11

ARG EXPORTER_VERSION=0.14.0
ENV EXPORTER_VERSION ${EXPORTER_VERSION}
ENV EXPORTER_PORT 5556

ADD https://repo1.maven.org/maven2/io/prometheus/jmx/jmx_prometheus_httpserver/${EXPORTER_VERSION}/jmx_prometheus_httpserver-${EXPORTER_VERSION}-jar-with-dependencies.jar /

CMD java -jar /jmx_prometheus_httpserver-${EXPORTER_VERSION}-jar-with-dependencies.jar ${EXPORTER_PORT} /etc/jmx_exporter/jmx_exporter.yaml
