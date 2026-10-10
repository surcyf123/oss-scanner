FROM python:3.11-bookworm
ENV DEBIAN_FRONTEND=noninteractive PIP_NO_CACHE_DIR=1
RUN apt-get update && apt-get install -y --no-install-recommends ca-certificates build-essential git curl \
    && rm -rf /var/lib/apt/lists/*
COPY . /src
WORKDIR /src
RUN git submodule update --init --recursive || echo "WARNING: submodules not fetched (no .git in context)"
RUN [ -d libs/forge-std/src ] || (rm -rf libs/forge-std libs/openzeppelin-contracts libs/openzeppelin-contracts-upgradeable \
    && git clone --depth 1 https://github.com/foundry-rs/forge-std libs/forge-std \
    && git clone --depth 1 https://github.com/OpenZeppelin/openzeppelin-contracts libs/openzeppelin-contracts \
    && git clone --depth 1 https://github.com/OpenZeppelin/openzeppelin-contracts-upgradeable libs/openzeppelin-contracts-upgradeable)
RUN curl -L https://foundry.paradigm.xyz | bash && /root/.foundry/bin/foundryup
ENV PATH="/root/.foundry/bin:${PATH}"
RUN (forge build || echo "WARNING: forge build failed") && (forge test || echo "WARNING: forge tests reported failures")
RUN pip install -r requirements.txt pytest && pip install -e . || echo "WARNING: python install failed"
