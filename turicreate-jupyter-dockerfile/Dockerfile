# Usar una imagen base de Python 3.7 para x86_64
FROM --platform=linux/amd64 python:3.7-slim

# Establecer el directorio de trabajo
WORKDIR /app

# Instalar dependencias del sistema
RUN apt-get update && apt-get install -y \
    libgl1-mesa-glx \
    libglib2.0-0 \
    && rm -rf /var/lib/apt/lists/*

# Actualizar pip
RUN pip install -U pip

# Instalar TuriCreate y Jupyter Notebook
RUN pip install turicreate jupyter

# Exponer el puerto 8888 para Jupyter Notebook
EXPOSE 8888

# Configurar Jupyter Notebook
CMD ["jupyter", "notebook", "--ip=0.0.0.0", "--port=8888", "--no-browser", "--allow-root", "--NotebookApp.token=''", "--NotebookApp.password=''"]