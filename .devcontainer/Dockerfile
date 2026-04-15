# Dev Container para GitHub Spec Kit - Leitor RSS
# Base image com suporte a .NET
FROM mcr.microsoft.com/devcontainers/dotnet:8.0-ubuntu-22.04

ARG SPECIFY_VERSION=v0.7.0
ENV UV_LINK_MODE=copy

# Atualizar pacotes
RUN apt-get update && apt-get upgrade -y \
    && apt-get install -y --no-install-recommends \
    # Git (versão >= 2.48)
    git \
    # Python 3.11 e pip
    python3.11 \
    python3-pip \
    python3-venv \
    # Node.js e npm (para Specify CLI)
    nodejs \
    npm \
    # Ferramentas de desenvolvimento
    build-essential \
    curl \
    wget \
    jq \
    zip \
    unzip \
    # Editor
    nano \
    vim \
    # Caso necessite SSL/TLS
    ca-certificates \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Verificar versão do Git
RUN git --version

# Instalar uv (gerenciador de pacotes Python)
RUN pip3 install --no-cache-dir uv

# Instalar Specify CLI via uv usando uma release estável do Spec Kit
RUN uv tool install --python python3.11 specify-cli --from git+https://github.com/github/spec-kit.git@${SPECIFY_VERSION} \
    && ln -sf /root/.local/bin/specify /usr/local/bin/specify

# Verificar instalações
RUN dotnet --version && python3 --version && node --version && npm --version && specify version

# Configurar Python 3.11 como padrão
RUN update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.11 1 \
    && update-alternatives --install /usr/bin/python python /usr/bin/python3.11 1

# Definir diretório de trabalho
WORKDIR /workspaces

# Comando padrão
CMD ["/bin/bash"]
