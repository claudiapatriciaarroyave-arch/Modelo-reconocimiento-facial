# Modelo-reconocimiento-facial
MODELO PARA REALIZAR RECONOCIMIENTO DE ROSTROS HUMANOS
# 🧠 FaceID — Reconocimiento Facial con Deep Learning

[![Streamlit App](https://static.streamlit.io/badges/streamlit_badge_black_white.svg)](https://share.streamlit.io)
[![Python 3.10+](https://img.shields.io/badge/python-3.10+-blue.svg)](https://www.python.org)
[![TensorFlow](https://img.shields.io/badge/TensorFlow-2.15-FF6F00?logo=tensorflow)](https://tensorflow.org)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

Sistema de reconocimiento facial entrenado con **Transfer Learning** sobre MobileNetV2, usando el dataset **LFW (Labeled Faces in the Wild)**. Desplegado como aplicación web interactiva con **Streamlit**.

---

## 🖥️ Demo en vivo

> **[👉 Abrir la app en Streamlit Cloud](https://share.streamlit.io)**
> *(Reemplaza este enlace con el tuyo después del despliegue)*

---

## 📁 Estructura del proyecto

```
face-recognition-app/
├── app.py                              ← Aplicación Streamlit
├── reconocimiento_facial.ipynb         ← Notebook de entrenamiento (Google Colab)
├── modelo_reconocimiento_facial.keras  ← Modelo entrenado*
├── clases.json                         ← Nombres de las clases*
├── requirements.txt                    ← Dependencias
└── README.md
```

> *Estos archivos se generan ejecutando el notebook en Colab.

---

## 🚀 Instalación y ejecución local

### 1. Clonar el repositorio
```bash
git clone https://github.com/TU_USUARIO/face-recognition-app.git
cd face-recognition-app
```

### 2. Crear entorno virtual e instalar dependencias
```bash
python -m venv venv
source venv/bin/activate        # Linux/Mac
# venv\Scripts\activate         # Windows

pip install -r requirements.txt
```

### 3. Entrenar el modelo
Abre `reconocimiento_facial.ipynb` en **Google Colab** (recomendado con GPU activada):

1. `Entorno de ejecución → Cambiar tipo → GPU`
2. Ejecutar todas las celdas
3. Descargar `modelo_reconocimiento_facial.keras` y `clases.json`
4. Colocarlos en la raíz del proyecto

### 4. Ejecutar la app
```bash
streamlit run app.py
```

---

## ☁️ Despliegue en Streamlit Cloud (gratis)

1. **Fork** este repositorio en GitHub
2. Ve a [share.streamlit.io](https://share.streamlit.io) e inicia sesión con GitHub
3. Haz clic en **"New app"** y selecciona tu repositorio
4. Configura:
   - **Main file path:** `app.py`
   - **Python version:** 3.10
5. Haz clic en **"Deploy"**

> ⚠️ **Importante:** Los archivos del modelo (`.keras` y `.json`) deben estar en el repositorio para que la app funcione en Streamlit Cloud. Si son muy grandes, considera usar [Git LFS](https://git-lfs.github.com/).

---

## 🏗️ Arquitectura del modelo

```
Input (96×96×3)
    │
    ▼
MobileNetV2 (ImageNet, congelado fase 1)
    │
    ▼
GlobalAveragePooling2D
    │
    ▼
BatchNormalization
    │
    ▼
Dense(256, relu) + Dropout(0.4)
    │
    ▼
Dense(128, relu) + Dropout(0.3)
    │
    ▼
Dense(N_clases, softmax)
```

**Entrenamiento en 2 fases:**
- **Fase 1:** Solo la cabeza de clasificación (lr=1e-3, ~30 épocas)
- **Fase 2:** Fine-tuning de las últimas 30 capas de MobileNetV2 (lr=1e-5, ~40 épocas)

---

## 📊 Dataset — LFW (Labeled Faces in the Wild)

| Característica | Valor |
|---|---|
| Fuente | `sklearn.datasets.fetch_lfw_people` |
| Filtro | ≥ 20 imágenes por persona |
| Resolución | 96×96 px (redimensionadas) |
| Split | 70% train / 15% val / 15% test |
| Augmentation | Rotación, flip, zoom, shifts |

---

## 💡 Funcionalidades de la app

- 📤 **Carga de imagen propia** (JPG, PNG, WEBP)
- 🎲 **Modo Demo** con imágenes aleatorias del dataset LFW
- 📊 **Ranking visual** con barras de confianza
- ⚙️ **Umbral de confianza** configurable
- 🔢 **Top-K predicciones** ajustable

---

## 🔧 Tecnologías

| Capa | Tecnología |
|---|---|
| Modelo | TensorFlow 2.x / Keras |
| Base | MobileNetV2 (ImageNet) |
| Dataset | scikit-learn (LFW) |
| Frontend | Streamlit |
| Visualización | Matplotlib, Seaborn |
| CV | OpenCV |

---

## 📌 Próximos pasos

- [ ] Detección automática de rostros con MTCNN
- [ ] Soporte para webcam en tiempo real
- [ ] Exportar a TFLite para mobile
- [ ] Agregar tu propio dataset personalizado

---

## 📄 Licencia

MIT © 2024 — Proyecto académico UNILASALLE
