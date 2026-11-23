# PDF Extractext — Interfaz Gráfica (GUI)

![Python](https://img.shields.io/badge/Python-3.14+-blue.svg?logo=python&logoColor=white)
![Tkinter](https://img.shields.io/badge/UI-Tkinter-lightgrey)
![python-dotenv](https://img.shields.io/badge/dotenv-1.0+-yellow.svg)

---

## Descripción

Interfaz de escritorio (Tkinter) para **PDF Extractext**. Permite seleccionar un archivo PDF, extraer su texto o convertirlo a Markdown, descargar el resultado en `.txt` o `.md`, y consultar el historial de documentos procesados.

La GUI se conecta al backend de PDF Extractext a través de variables de entorno (`API_URL`, `EXTRACT_API_URL`, `DOCUMENTS_API_URL`), siguiendo el **Factor 3 (Config)** de la metodología 12-Factor App.

---

## Funcionalidades

- Seleccionar un archivo PDF desde el explorador de archivos.
- Extraer texto plano del PDF (`POST /documents/upload`).
- Convertir el PDF a Markdown detectando títulos por tamaño de fuente (`POST /extract`).
- Descargar el texto extraído en formato `.txt` o `.md`.
- Ver el historial de documentos ya procesados.
- Renombrar y eliminar documentos del historial (borrado lógico).

---

## Requisitos del sistema

1. **Python 3.14+**
2. **uv** (gestor de dependencias): `pip install uv`
3. Un backend de PDF Extractext corriendo y accesible (local o remoto).

---

## Instalación

```bash
uv sync
```

Esto instala las dependencias declaradas en `pyproject.toml` (`requests`, `python-dotenv`, etc.).

---

## Configuración (Factor 3 — Config)

Copia el archivo de ejemplo y ajusta los valores para tu entorno:

```bash
cp .env.example .env
```

Luego edita `.env` con las URLs de tu backend:

| Variable | Descripción | Valor por defecto |
|----------|-------------|-------------------|
| `API_URL` | URL del gateway o backend único | `http://127.0.0.1:8000` |
| `EXTRACT_API_URL` | URL del servicio de extracción (sin gateway) | `http://127.0.0.1:8001` |
| `DOCUMENTS_API_URL` | URL del servicio de documentos (sin gateway) | `http://127.0.0.1:8002` |

> El archivo `.env` **no se sube al repositorio** (está en `.gitignore`). Cada desarrollador despliega su propio `.env` local.

---

## Uso

Ejecuta la interfaz gráfica desde la raíz del proyecto:

```bash
uv run python interface.py
```

O, si prefieres usar el entorno virtual activado por `uv`:

```bash
uv run python interface.py
```

La ventana principal te permitirá:

1. Seleccionar un PDF.
2. Extraer texto o Markdown.
3. Descargar el resultado.
4. Consultar el historial de documentos.

---

## Estructura del repositorio

```
.
├── interface.py          # Interfaz gráfica Tkinter
├── pyproject.toml        # Dependencias y configuración del proyecto
├── uv.lock               # Lockfile de dependencias (uv)
├── tests/
│   └── test_interface.py # Pruebas de la interfaz
├── .env.example          # Ejemplo de variables de entorno
├── .gitignore            # Archivos ignorados por Git
├── LICENSE
└── README.md
```

---

## Pruebas

```bash
uv run pytest
```

---

## Notas de despliegue

Esta carpeta contiene **únicamente el frontend (GUI)**. El backend (microservicios `extract` y `documents`, nginx, MongoDB, docker-compose) vive en un repositorio separado. Para ejecutar el sistema completo necesitas ambos repositorios desplegados y las URLs del backend configuradas en tu `.env` local.
