# Docker Hub's official 'openjdk' image has been removed - Java's official
# distribution now ships as eclipse-temurin.
#
# HelloWorld.class was compiled for Java 8, but newer JVMs still run older
# class files, so a current JRE is fine.
FROM eclipse-temurin:25-jre

WORKDIR /app
COPY java/HelloWorld.class .

CMD ["java", "HelloWorld"]
