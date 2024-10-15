FROM alpine/git:latest as source_fetch
RUN git clone https://github.com/ControlSystemStudio/phoebus.git /phoebus
ARG GIT_TAG=master
RUN cd /phoebus && git checkout ${GIT_TAG}

FROM alpine/git:latest as source_bob
RUN git clone https://github.com/rjwills28/phoebus-docker.git /bob
ARG GIT_TAG=performance_tests
RUN cd /bob && git checkout ${GIT_TAG}


FROM maven:3.8.7-eclipse-temurin-17 as builder
COPY --from=source_fetch /phoebus /phoebus
WORKDIR /phoebus
RUN mvn clean verify -f dependencies/pom.xml
RUN mvn -DskipTests clean install


FROM openjdk:17-slim-buster as product
RUN apt-get update && apt-get install -y openjfx libopenjfx-jni libopenjfx-java
COPY --from=builder /phoebus/phoebus-product/target /phoebus
COPY --from=source_bob /bob/bob/ /phoebus/bob
COPY --from=source_bob /bob/settings.ini /phoebus
WORKDIR /phoebus
ENTRYPOINT ["java", "-jar", "/phoebus/product-4.7.4-SNAPSHOT.jar", "-settings", "/phoebus/settings.ini", "-resource", "file:/phoebus/bob/performanceTestPage0.bob?target=window"]
#ENTRYPOINT ["java", "-jar", "/phoebus/product-4.7.4-SNAPSHOT.jar", "-settings", "/phoebus/settings.ini", "-resource", "file:/phoebus/bob/performanceTestPage0.bob?target=window", "-resource", "file:/phoebus/bob/performanceTestPage1.bob?target=window", "-resource", "file:/phoebus/bob/performanceTestPage2.bob?target=window", "-resource", "file:/phoebus/bob/performanceTestPage3.bob?target=window", "-resource", "file:/phoebus/bob/performanceTestPage4.bob?target=window"]
#ENTRYPOINT ["java", "-jar", "/phoebus/product-4.7.4-SNAPSHOT.jar", "-settings", "/phoebus/settings.ini", "-resource", "file:/phoebus/bob/performanceTestPage0.bob?target=window", "-resource", "file:/phoebus/bob/performanceTestPage1.bob?target=window", "-resource", "file:/phoebus/bob/performanceTestPage2.bob?target=window", "-resource", "file:/phoebus/bob/performanceTestPage3.bob?target=window", "-resource", "file:/phoebus/bob/performanceTestPage4.bob?target=window", "-resource", "file:/phoebus/bob/performanceTestPage5.bob?target=window", "-resource", "file:/phoebus/bob/performanceTestPage6.bob?target=window", "-resource", "file:/phoebus/bob/performanceTestPage7.bob?target=window", "-resource", "file:/phoebus/bob/performanceTestPage8.bob?target=window", "-resource", "file:/phoebus/bob/performanceTestPage9.bob?target=window"]