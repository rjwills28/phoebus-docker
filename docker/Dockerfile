FROM alpine/git:latest as source_fetch
RUN git clone https://github.com/ControlSystemStudio/phoebus.git /phoebus
ARG GIT_TAG=master
RUN cd /phoebus && git checkout ${GIT_TAG}

FROM alpine/git:latest as source_bob
RUN git clone https://github.com/rjwills28/phoebus-docker.git /bob
ARG GIT_TAG=performance_tests_50
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
ENTRYPOINT ["java", "-jar", "/phoebus/product-4.7.4-SNAPSHOT.jar", "-settings", "/phoebus/settings.ini", "-resource", "file:/phoebus/bob/performanceTestPage0.bob?target=window", "-resource", "file:/phoebus/bob/performanceTestPage1.bob?target=window", "-resource", "file:/phoebus/bob/performanceTestPage2.bob?target=window", "-resource", "file:/phoebus/bob/performanceTestPage3.bob?target=window", "-resource", "file:/phoebus/bob/performanceTestPage4.bob?target=window", "-resource", "file:/phoebus/bob/performanceTestPage5.bob?target=window", "-resource", "file:/phoebus/bob/performanceTestPage6.bob?target=window", "-resource", "file:/phoebus/bob/performanceTestPage7.bob?target=window", "-resource", "file:/phoebus/bob/performanceTestPage8.bob?target=window", "-resource", "file:/phoebus/bob/performanceTestPage9.bob?target=window", "-resource", "file:/phoebus/bob/performanceTestPage10.bob?target=window", "-resource", "file:/phoebus/bob/performanceTestPage11.bob?target=window", "-resource", "file:/phoebus/bob/performanceTestPage12.bob?target=window", "-resource", "file:/phoebus/bob/performanceTestPage13.bob?target=window", "-resource", "file:/phoebus/bob/performanceTestPage14.bob?target=window", "-resource", "file:/phoebus/bob/performanceTestPage15.bob?target=window", "-resource", "file:/phoebus/bob/performanceTestPage16.bob?target=window", "-resource", "file:/phoebus/bob/performanceTestPage17.bob?target=window", "-resource", "file:/phoebus/bob/performanceTestPage18.bob?target=window", "-resource", "file:/phoebus/bob/performanceTestPage19.bob?target=window", "-resource", "file:/phoebus/bob/performanceTestPage20.bob?target=window", "-resource", "file:/phoebus/bob/performanceTestPage21.bob?target=window", "-resource", "file:/phoebus/bob/performanceTestPage22.bob?target=window", "-resource", "file:/phoebus/bob/performanceTestPage23.bob?target=window", "-resource", "file:/phoebus/bob/performanceTestPage24.bob?target=window", "-resource", "file:/phoebus/bob/performanceTestPage25.bob?target=window", "-resource", "file:/phoebus/bob/performanceTestPage26.bob?target=window", "-resource", "file:/phoebus/bob/performanceTestPage27.bob?target=window", "-resource", "file:/phoebus/bob/performanceTestPage28.bob?target=window", "-resource", "file:/phoebus/bob/performanceTestPage29.bob?target=window", "-resource", "file:/phoebus/bob/performanceTestPage30.bob?target=window", "-resource", "file:/phoebus/bob/performanceTestPage31.bob?target=window", "-resource", "file:/phoebus/bob/performanceTestPage32.bob?target=window", "-resource", "file:/phoebus/bob/performanceTestPage33.bob?target=window", "-resource", "file:/phoebus/bob/performanceTestPage34.bob?target=window", "-resource", "file:/phoebus/bob/performanceTestPage35.bob?target=window", "-resource", "file:/phoebus/bob/performanceTestPage36.bob?target=window", "-resource", "file:/phoebus/bob/performanceTestPage37.bob?target=window", "-resource", "file:/phoebus/bob/performanceTestPage38.bob?target=window", "-resource", "file:/phoebus/bob/performanceTestPage39.bob?target=window", "-resource", "file:/phoebus/bob/performanceTestPage40.bob?target=window", "-resource", "file:/phoebus/bob/performanceTestPage41.bob?target=window", "-resource", "file:/phoebus/bob/performanceTestPage42.bob?target=window", "-resource", "file:/phoebus/bob/performanceTestPage43.bob?target=window", "-resource", "file:/phoebus/bob/performanceTestPage44.bob?target=window", "-resource", "file:/phoebus/bob/performanceTestPage45.bob?target=window", "-resource", "file:/phoebus/bob/performanceTestPage46.bob?target=window", "-resource", "file:/phoebus/bob/performanceTestPage47.bob?target=window", "-resource", "file:/phoebus/bob/performanceTestPage48.bob?target=window", "-resource", "file:/phoebus/bob/performanceTestPage49.bob?target=window"]