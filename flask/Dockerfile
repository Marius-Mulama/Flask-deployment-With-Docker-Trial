# FROM python:3.9.5-alpine3.13
FROM python:3.9.5-slim-buster

#Installing curl
RUN apt-get update && apt-get install -y curl && rm -rf /var/lib/apt/lists/*


WORKDIR /app

COPY requirements.txt .

RUN pip install -r requirements.txt


COPY app.py .


CMD ["gunicorn", "--bind", "0.0.0.0:8080", "--access-logfile", "-", "--error-logfile", "-", "app:app"]
