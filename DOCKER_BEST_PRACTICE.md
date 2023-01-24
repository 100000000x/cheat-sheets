# Docker Best Practice

_Use only official docker hub images_
_Docker knows: Images, Container, Volumes, Networks_

## All Minimized, No Frills, Resilient, Fractal, Clean and Secure Images
1. Use multi-stage building in Dockerfile FROM>STABLE LAYER>VOLATILE LAYER
2. Do not run layer-redundant Dockerfile commands FROM>ENV>COPY>RUN>COPY
2. No secrets in Docker Container
3. No ROOT in Docker Container
4. Use .dockerignore File
5. Use slimmest "-slim" available working shelf Docker Images
6. Use && Commands
7. Never use ADD
8. Sequentialize ENTRYPOINT and CMD Commands
8. Run one logical process per Docker Container
9. Limit memory and processor per Docker Container
10. Logging to stdout stderr
11. Use docker compose
12. Use docker scan
13. Use docker Content Trust
14. Use supervisord
15. Use docker dive
16. Use CI/CD Git versioning

## Examples
multiple stages dockerfile
```
# temp stage
FROM python:3.9-slim as builder

WORKDIR /app

ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1
DOCKER_CONTENT_TRUST=1

RUN apt-get update && \
    apt-get install -y --no-install-recommends gcc

COPY requirements.txt .
RUN pip wheel --no-cache-dir --no-deps --wheel-dir /app/wheels -r requirements.txt


# final stage
FROM python:3.9-slim

WORKDIR /app

COPY --from=builder /app/wheels /wheels
COPY --from=builder /app/requirements.txt .

RUN pip install --no-cache /wheels/*
```
layer-complementary dockerfile command order
```
FROM python:3.9-slim

WORKDIR /app

COPY requirements.txt .

RUN pip install -r /requirements.txt

COPY sample.py .
```
expressive clear commands
```
RUN apt-get update && apt-get install -y \
    git \
    gcc \
    matplotlib \
    pillow  \
    && rm -rf /var/lib/apt/lists/*
```
```
RUN addgroup --system app && adduser --system --group app

USER app
```
use entrypoint primarily, command supplementary
```
ENTRYPOINT ["gunicorn", "config.wsgi", "-w"]
CMD ["4"]
gunicorn config.wsgi -w 4
```
label docker images distinctively and descriptively
```
Project name: web
Environment name: prod
Git commit hash: a072c4e5d94b5a769225f621f08af3d4bf820a07
Semantic version: 0.1.
docker build -t web-prod-a072c4e5d94b5a769225f621f08af3d4bf820a07-0.1.4 .
```
make use of extensive docker ignorefile
```
.dockerignore
**/.git
**/.gitignore
**/.vscode
**/coverage
**/.env
**/.aws
**/.ssh
Dockerfile
README.md
docker-compose.yml
**/.DS_Store
**/venv
**/env
```
pass secret into docker container when building it
```
docker build --no-cache --progress=plain --secret id=mysecret,src=secrets.txt .
```
limit memory, cpu
```
version: "3.9"
services:
  redis:
    image: redis
    deploy:
      resources:
        limits:
          cpus: 2
          memory: 512M
        reservations:
          cpus: 1
          memory: 256M
```
