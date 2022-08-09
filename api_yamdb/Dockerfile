FROM python:3.7-slim

WORKDIR /app

# Скопировать с локального компьютера файл зависимостей
# в рабочую директорию 
COPY requirements.txt .

RUN pip3 install -r requirements.txt --no-cache-dir

# Скопировать содержимое директории /api_yamdb c локального компьютера
# в рабочую директорию
COPY ./ .

# Выполнить запуск сервера разработки при старте контейнера.
CMD ["gunicorn", "api_yamdb.wsgi:application", "--bind", "0:8000" ]
