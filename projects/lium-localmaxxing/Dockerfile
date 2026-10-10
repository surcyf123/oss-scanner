FROM python:3.11-bookworm
ENV DEBIAN_FRONTEND=noninteractive PIP_NO_CACHE_DIR=1
RUN apt-get update && apt-get install -y --no-install-recommends ca-certificates build-essential git curl \
    && rm -rf /var/lib/apt/lists/*
COPY . /src
WORKDIR /src
RUN apt-get update && apt-get install -y --no-install-recommends shellcheck jq && rm -rf /var/lib/apt/lists/*
RUN (find . -name "*.sh" -print0 | xargs -0 -r shellcheck || echo "WARNING: shellcheck findings")
