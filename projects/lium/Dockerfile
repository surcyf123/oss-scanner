FROM python:3.11-bookworm
ENV DEBIAN_FRONTEND=noninteractive PIP_NO_CACHE_DIR=1
RUN apt-get update && apt-get install -y --no-install-recommends ca-certificates build-essential git curl \
    && rm -rf /var/lib/apt/lists/*
COPY . /src
WORKDIR /src
ENV SETUPTOOLS_SCM_PRETEND_VERSION=0.0.0
RUN pip install uv && uv sync --frozen
ENV PATH="/src/.venv/bin:${PATH}"
RUN uv pip install pytest && (pytest -q test || echo "WARNING: tests reported failures")
