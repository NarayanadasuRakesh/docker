FROM maven As build
WORKDIR /opt/shipping
COPY pom.xml /opt/shipping
RUN mvn dependency:resolve
COPY src /opt/shipping/src/
RUN mvn package


FROM openjdk:8-jre-alpine3.9
EXPOSE 8080
ENV CART_ENDPOINT=cart:8080
ENV DB_HOST=mysql
WORKDIR /opt/shipping
COPY --from=build /opt/shipping/target/shipping-1.0.jar shipping.jar
CMD [ "java", "-Xmn256m", "-Xmx768m", "-jar", "shipping.jar" ]