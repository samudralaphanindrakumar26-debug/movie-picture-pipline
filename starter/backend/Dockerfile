FROM public.ecr.aws/docker/library/python:3.10-alpine
ENV FLASK_RUN_HOST=0.0.0.0

WORKDIR /app
RUN adduser -u 1000 -D app

RUN apk update && \
  apk add --no-cache \
  build-base \
  gcc \
  musl-dev \
  linux-headers \
  python3-dev \
  pcre \
  pcre-dev \
  openssl-dev \
  libffi-dev \
  && pip install --no-cache-dir --upgrade pip pipenv

COPY Pipfile Pipfile.lock ./
RUN pipenv install --system --skip-lock

COPY . .

CMD ["uwsgi", "--http", ":5000", "--master", "--enable-threads", "--manage-script-name", "--mount", "/=app:app"]