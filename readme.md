## Урок 1. Компиляция и интерпретация кода

## Создать docker-контейнер для формирования полной документации по проекту

Dockerfile:

```Dockerfile
# Используем базовый образ с JDK 11
FROM openjdk:11

# Устанавливаем рабочую директорию
WORKDIR /app

# Копируем исходный код проекта в контейнер
COPY . /app

# Установка необходимых зависимостей
RUN apt-get update && \
    apt-get install -y git

# Генерация документации
RUN javadoc -d /docs -sourcepath src -subpackages ru

# Указываем точку входа по умолчанию
CMD ["bash"]
```

Команды в терминале:

```bash
docker build -t javadoc-generator .
```

```bash
docker run --rm -v $(pwd)/docs:/docs javadoc-generator
```
