# Build stage
# Подключение JDK фиксированной версии и создание ступени
FROM eclipse-temurin:21-jdk-jammy AS builder
WORKDIR /app
# Переменная окружения
ENV GRADLE_OPTS="-Dhttps.protocols=TLSv1.2,TLSv1.3"
# Файлы необходимы исключительно для сборки
COPY build.gradle.kts settings.gradle.kts gradlew ./
COPY gradle gradle
# Скачивание зависимостей проекта
RUN ./gradlew dependencies || return 0
# Копирование исходных файлов (код)
COPY src src
# Сборка проекта
RUN ./gradlew clean build -x test -x ktlintKotlinScriptCheck -x ktlintMainSourceSetCheck -x ktlintTestSourceSetCheck

# Runtime stage
# Подключение JRE фиксированной версии
FROM eclipse-temurin:21-jre-jammy
WORKDIR /app
# Создание пользования с минимальными правами
RUN useradd --system --create-home --uid 1001 appuser
USER appuser
# Выполнение команд от лица пользования с минимальными правами
COPY --chown=appuser:appuser --from=builder /app/build/libs/*-SNAPSHOT-plain.jar app.jar
# Run the application
ENTRYPOINT ["java", "-jar", "app.jar"]
