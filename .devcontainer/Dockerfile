# Dev Container para GitHub Spec Kit - Leitor RSS
# Base image com suporte a .NET
FROM mcr.microsoft.com/devcontainers/dotnet:8.0-ubuntu-22.04

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
    # Docker CLI (para executar containers dentro do dev container)
    docker.io \
    # Caso necessite SSL/TLS
    ca-certificates \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Verificar versão do Git
RUN git --version

# Instalar uv (gerenciador de pacotes Python)
RUN pip3 install uv

# Instalar Specify CLI globalmente
RUN npm install -g @github-spec-kit/specify-cli

# Verificar instalações
RUN dotnet --version && python3 --version && node --version && npm --version

# Configurar Python 3.11 como padrão
RUN update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.11 1 \
    && update-alternatives --install /usr/bin/python python /usr/bin/python3.11 1

# Criar usuário vscode (já existe na imagem base)
# Apenas garantir que o usuário possua permissões adequadas
RUN usermod -aG docker vscode || true

# Definir diretório de trabalho
WORKDIR /workspace

# Comando padrão
CMD ["/bin/bash"]
