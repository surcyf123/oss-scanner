FROM python:3.11-bookworm
ENV DEBIAN_FRONTEND=noninteractive PIP_NO_CACHE_DIR=1
RUN apt-get update && apt-get install -y --no-install-recommends ca-certificates build-essential git curl \
    && rm -rf /var/lib/apt/lists/*
COPY . /src
WORKDIR /src
RUN pip install pdm && (pdm install -G :all || pdm install || echo "WARNING: pdm install failed")
RUN for p in packages/*/ ; do [ -f "$p/pyproject.toml" ] && (pip install -e "$p" || echo "WARNING: $p"); done; true
RUN pip install pytest pytest-asyncio && (pdm run pytest -x -q --co >/dev/null || echo "WARNING: test collection failed")
