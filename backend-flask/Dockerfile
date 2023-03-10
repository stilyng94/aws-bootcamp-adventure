# Use explicit image reference
FROM python:3.10-slim-buster@sha256:497b91c87ca7d8bf5e0d07d59db1c3e5f29d36ccca1f9878719123e9fbc8f144

ENV PYTHONFAULTHANDLER=1 \
    PYTHONUNBUFFERED=1 \
    PYTHONHASHSEED=random \
    PIP_NO_CACHE_DIR=off \
    PIP_DISABLE_PIP_VERSION_CHECK=on \
    PIP_DEFAULT_TIMEOUT=100 \
    LC_ALL=C.UTF-8 \
    LANG=C.UTF-8 \
    FLASK_ENV=development \
    PORT=4567


# Install curl to use for health check and dumb-init as process manager to forward signals
RUN apt-get update -y && apt-get install --no-install-recommends -y curl && apt-get install --no-install-recommends -y dumb-init \
&& apt-get clean \
&& rm -rf /var/lib/apt/lists/*

WORKDIR /backend-flask

COPY requirements.txt requirements.txt
RUN pip3 install -r requirements.txt

COPY . .

# Never run application as root user
RUN adduser flask && chown -R flask /backend-flask

EXPOSE ${PORT}

USER flask

ENTRYPOINT ["/usr/bin/dumb-init", "--"]

CMD ["/bin/bash", "-c","python3 -m flask run --host=0.0.0.0 --port=4567"]