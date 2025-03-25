Dockerfile para TuriCreate con Jupyter Notebook
(Compatible con macOS M1/M2/M3, Linux x86_64 y Windows WSL)

Este Dockerfile permite ejecutar TuriCreate en un contenedor Docker con Jupyter Notebook, incluso en sistemas Apple Silicon (M1/M2/M3) mediante emulación x86_64.

🐋 Instrucciones de Uso
1. Requisitos
Docker Desktop instalado (Descargar aquí).

En macOS, asegúrate de que Rosetta 2 esté activado (viene por defecto en M1/M2/M3).

2. Construir la Imagen Docker
bash
Copy
docker build -t turicreate-jupyter .
3. Ejecutar el Contenedor
bash
Copy
docker run -p 8888:8888 -v $(pwd):/app turicreate-jupyter
-p 8888:8888: Expone el puerto de Jupyter Notebook.

-v $(pwd):/app: Monta el directorio actual en /app (opcional para guardar notebooks).

📜 Dockerfile Completo
dockerfile
Copy
# Usar imagen base de Python 3.7 para x86_64 (emulación en Apple Silicon)
FROM --platform=linux/amd64 python:3.7-slim

# Configurar el directorio de trabajo
WORKDIR /app

# Instalar dependencias del sistema
RUN apt-get update && apt-get install -y \
    libgl1-mesa-glx \
    libglib2.0-0 \
    && rm -rf /var/lib/apt/lists/*

# Actualizar pip e instalar paquetes
RUN pip install --upgrade pip && \
    pip install turicreate jupyter

# Exponer puerto para Jupyter Notebook
EXPOSE 8888

# Iniciar Jupyter al ejecutar el contenedor
CMD ["jupyter", "notebook", "--ip=0.0.0.0", "--port=8888", "--no-browser", "--allow-root", "--NotebookApp.token=''"]
🔍 Explicación del Dockerfile
FROM --platform=linux/amd64 python:3.7-slim

Fuerza la arquitectura x86_64 (necesaria para TuriCreate en Apple Silicon).

Dependencias de sistema (libgl1-mesa-glx)

Requeridas para el procesamiento de imágenes en TuriCreate.

Instalación de paquetes Python

TuriCreate + Jupyter Notebook.

Configuración de Jupyter

Sin contraseña (--NotebookApp.token='') y accesible desde cualquier IP (--ip=0.0.0.0).

🚨 Solución de Problemas
Error en Apple Silicon (M1/M2/M3)
Si falla la construcción, asegúrate de:

Tener Docker Desktop 4.12+ con Rosetta 2 activado.

Usar el flag --platform=linux/amd64.

Error de GPU en Linux
Si necesitas aceleración GPU, añade:

dockerfile
Copy
RUN apt-get install -y ocl-icd-opencl-dev
📂 Estructura Recomendada del Proyecto
Copy
proyecto/
├── Dockerfile
├── notebooks/          # Carpeta para guardar Jupyter Notebooks
└── data/               # Datos para entrenamiento (opcional)
🎉 ¡Listo!
Accede a Jupyter Notebook en:
👉 http://localhost:8888

Jupyter Demo

¿Necesitas más ayuda?
¡Abre un issue en este repositorio o contribuye mejorando el Dockerfile! 🚀
