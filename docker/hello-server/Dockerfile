# build stage
FROM eclipse-temurin:21-jdk AS builder

WORKDIR /app
COPY . .

RUN javac Main.java

# run stage
FROM eclipse-temurin:21-jre

WORKDIR /app
COPY --from=builder /app/*.class ./

ENTRYPOINT ["java", "Main"]