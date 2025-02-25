FROM mcr.microsoft.com/devcontainers/python:3.10

ARG DEBIAN_FRONTEND=noninteractive

# Install system dependencies
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

# Install poetry (Python is already in base image)
RUN curl -sSL https://install.python-poetry.org | python3 - \
    && poetry config virtualenvs.in-project true

# Set up Jupyter for easier access
RUN mkdir -p /root/.jupyter \
    && echo "c.NotebookApp.ip = '0.0.0.0'" > /root/.jupyter/jupyter_notebook_config.py \
    && echo "c.NotebookApp.token = ''" >> /root/.jupyter/jupyter_notebook_config.py