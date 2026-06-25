FROM python:3.10-slim

# Non-root user configuration
ARG USERNAME=appuser
ARG USER_UID=1000
ARG USER_GID=1000

ENV PYTHONDONTWRITEBYTECODE=1 \
    PYTHONUNBUFFERED=1 \
    MPLBACKEND=Agg

# System dependencies required by scientific Python packages
RUN apt-get update && apt-get install -y --no-install-recommends \
    build-essential \
    gcc \
    g++ \
    git \
    curl \
    ca-certificates \
    libglib2.0-0 \
    libsm6 \
    libxext6 \
    libxrender1 \
    libgomp1 \
 && rm -rf /var/lib/apt/lists/*

WORKDIR /app

# Install Python dependencies first to improve Docker layer caching
COPY requirements.txt /app/requirements.txt
RUN pip install --no-cache-dir -r /app/requirements.txt

# Copy project files
COPY notebook/large_scale_accident_clustering.ipynb /app/notebook/large_scale_accident_clustering.ipynb
COPY README.md /app/README.md

# Create non-root user and output directory
RUN groupadd --gid ${USER_GID} ${USERNAME} \
 && useradd --uid ${USER_UID} --gid ${USER_GID} -m ${USERNAME} \
 && mkdir -p /app/outputs \
 && chown -R ${USER_UID}:${USER_GID} /app

USER ${USERNAME}

CMD ["jupyter", "execute", "notebook/large_scale_accident_clustering.ipynb"]