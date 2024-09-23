# Usa l'immagine JDK come base
FROM adoptopenjdk:21-jdk-hotspot as builder

# Imposta la directory di lavoro
WORKDIR /app

# Copia il file pom.xml e le dipendenze
COPY pom.xml .
COPY src ./src

# Costruisci il progetto
RUN ./mvnw package -DskipTests

# Crea l'immagine finale
FROM adoptopenjdk:11-jre-hotspot
COPY --from=builder /app/target/*-runner /app/application

# Espone la porta dell'applicazione
EXPOSE 8080

# Comando di avvio
CMD ["java", "-jar", "/app/application"]
