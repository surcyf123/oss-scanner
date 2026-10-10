FROM python:3.11-bookworm
ENV DEBIAN_FRONTEND=noninteractive PIP_NO_CACHE_DIR=1
RUN apt-get update && apt-get install -y --no-install-recommends ca-certificates build-essential git curl \
    && rm -rf /var/lib/apt/lists/*
COPY . /src
WORKDIR /src
RUN pip install lium.io || echo "WARNING: lium CLI install failed"
