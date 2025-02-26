FROM mcr.microsoft.com/devcontainers/python:3.10

ARG DEBIAN_FRONTEND=noninteractive

# Install system dependencies (removed duplicates from base image)
RUN apt-get update && apt-get install -y --no-install-recommends \
    # Data science specific dependencies
    libblas-dev \
    liblapack-dev \
    libatlas-base-dev \
    gfortran \
    graphviz \
    gdal-bin \
    libgdal-dev \
    poppler-utils \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Check if vscode user exists, if not create it
RUN if ! id -u vscode >/dev/null 2>&1; then \
        useradd -m -s /bin/bash vscode; \
    fi

# Switch to vscode user
USER vscode
ARG HOME="/home/vscode"

# Install poetry (Python is already in base image)
RUN curl -sSL https://install.python-poetry.org | python3 - \
    && export PATH="/home/vscode/.local/bin:$PATH" \
    && poetry config virtualenvs.in-project true

# Set up Jupyter for easier access
RUN mkdir -p ${HOME}/.jupyter \
    && echo "c.NotebookApp.ip = '0.0.0.0'" > ${HOME}/.jupyter/jupyter_notebook_config.py \
    && echo "c.NotebookApp.token = ''" >> ${HOME}/.jupyter/jupyter_notebook_config.py