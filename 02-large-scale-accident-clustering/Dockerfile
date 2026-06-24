FROM python:3.10-slim

# --- Args para user no-root (puedes sobreescribir desde compose) ---
ARG USERNAME=user3
ARG USER_UID=1008
ARG USER_GID=1008

ENV PYTHONDONTWRITEBYTECODE=1 \
    PYTHONUNBUFFERED=1 \
    MPLBACKEND=Agg

# Dependencias del sistema (scipy / numpy / tensorflow suelen requerir estas libs)
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
 && rm -rf /var/lib/apt/lists/*

WORKDIR /app

# Instala dependencias Python
COPY requirements.txt /app/requirements.txt
RUN pip install --no-cache-dir -r /app/requirements.txt

# Copia tu script
COPY Proyecto_Final.ipynb /app/Proyecto_Final.ipynb

# Crea usuario/grupo no-root
RUN groupadd --gid ${USER_GID} ${USERNAME} \
 && useradd --uid ${USER_UID} --gid ${USER_GID} -m ${USERNAME} \
 && mkdir -p /app/output /app/tuner \
 && chown -R ${USER_UID}:${USER_GID} /app

USER ${USERNAME}

CMD ["jupyter", "execute", "Proyecto_Final.ipynb"]