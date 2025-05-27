# Proyecto Reconocimiento Facial y Clasificación de Género

Facilitar el llamado de asitencia

![Banner del Proyecto](https://via.placeholder.com/800x200.png?text=Proyecto+Ciencia+de+Datos)

![Python](https://img.shields.io/badge/Python-3.10-blue)
![pandas](https://img.shields.io/badge/pandas-2.2.3-orange)
![tqdm](https://img.shields.io/badge/tqdm-4.67.0-lightgrey)


**Versión:** 0.0.0
**Autor:** [YEIMY](mailto:yeimyaalmanza@gmail.com)  


## Introducción

El reconocimiento facial es una tecnología cada vez más presente en diversas aplicaciones, desde seguridad hasta análisis biométrico y control de acceso. En este proyecto se desarrolla un sistema integral de reconocimiento facial para identificar estudiantes a partir de sus fotos, complementado con un modelo de clasificación de género basado en redes neuronales convolucionales. Se emplean métodos avanzados para la extracción y comparación de características faciales, incluyendo modelos reconocidos como FaceNet y ArcFace.

Este proyecto aborda todos los pasos desde la descarga y organización automática de imágenes, la generación de embeddings faciales, la detección y reconocimiento en imágenes grupales, hasta la evaluación exhaustiva de los modelos implementados. Además, se incluye la exploración de nuevos modelos para mejorar la precisión y robustez del sistema.

## Objetivos
- Implementar un pipeline automático para la descarga y organización de imágenes faciales desde enlaces en Google Drive.
- Desarrollar y entrenar un modelo CNN para la clasificación de género (hombre/mujer) basado en imágenes faciales.
- Extraer embeddings faciales robustos con FaceNet (MTCNN + InceptionResnetV1) para la identificación individual de estudiantes.
- Detectar y reconocer múltiples rostros en imágenes grupales mediante comparación de embeddings.
- Explorar y evaluar el desempeño de embeddings alternativos generados con el modelo ArcFace (InsightFace).
- Evaluar cuantitativamente la precisión y robustez del sistema completo para identificar oportunidades de mejora.

## Contenido del proyecto

- **Cuadernos**: Contiene un único notebook principal (Modelo face_embedding_facenet_mtcnn.ipynb) que documenta todo el flujo del proyecto: desde la descarga de imágenes y preprocesamiento, hasta la construcción y evaluación de los modelos de reconocimiento facial y clasificación de género. Está diseñado para ser ejecutado de principio a fin en Google Colab.
- **Datos**: Incluye el archivo Excel con los enlaces de Google Drive a las imágenes de los estudiantes, así como las carpetas generadas con las fotos descargadas. Estos datos son esenciales para entrenar, validar y evaluar los modelos desarrollados.
- **Documentación**: Proporciona información detallada sobre el propósito del proyecto, su estructura, las herramientas utilizadas, la metodología aplicada y los resultados obtenidos. Funciona como guía técnica y explicativa del sistema completo.

## Estructura del proyecto 
El proyecto está organizado en varios módulos o partes que abordan diferentes etapas del pipeline de reconocimiento facial y clasificación de género. A continuación se detalla la estructura general y el propósito de cada componente:

1. **Descarga y Preparación de Datos**
**Descripción:**
Este módulo automatiza la obtención de las imágenes faciales necesarias para el proyecto a partir de un archivo Excel. El archivo contiene los nombres completos de los estudiantes y enlaces a sus fotos almacenadas en Google Drive.

**Proceso:**

- Validación y conversión de enlaces para generar URLs directas de descarga.
- Descarga automática de imágenes y almacenamiento ordenado en una carpeta local llamada imagenes_descargadas.
- Normalización y control de calidad, asegurando que las imágenes tengan formatos compatibles (jpg, png, etc.) y que los nombres de archivo estén limpios para evitar errores en pasos posteriores.

2. **Modelo de Clasificación de Género con CNN**
**Descripción:**
Se desarrolla una red neuronal convolucional (CNN) entrenada con TensorFlow/Keras para clasificar las imágenes faciales en dos categorías: "Hombre" y "Mujer".

**Proceso:**

- Preprocesamiento de imágenes (normalización, resizing, data augmentation).
- Arquitectura CNN personalizada o basada en modelos estándar (p.ej., MobileNet, ResNet).
- Entrenamiento con un dataset balanceado y evaluación con métricas como accuracy y F1-score.

**Salida:**
Un modelo entrenado capaz de predecir el género a partir de una imagen facial nueva.

3. **Generación de Embeddings Faciales con MTCNN + FaceNet**
**Descripción:**
Para identificar individualmente a los estudiantes, se extraen vectores numéricos (embeddings) que representan características faciales únicas.

**Proceso:**

- Detección precisa de rostros en imágenes individuales usando MTCNN (Multi-task Cascaded Convolutional Networks).
- Extracción de embeddings faciales con FaceNet, un modelo basado en InceptionResnetV1 entrenado en VGGFace2.
- Almacenamiento de estos vectores en un diccionario serializado (.npy), con el nombre del estudiante como clave.

**Importancia:**
Los embeddings permiten comparar rostros mediante métricas de similitud (p. ej., coseno) de manera eficiente y precisa, clave para el reconocimiento facial.

4. **Reconocimiento Facial en Imágenes Grupales**
**Descripción:**
Este módulo permite detectar y reconocer múltiples rostros dentro de una imagen que contiene a varios estudiantes.

**Proceso:**

- Detectar múltiples rostros en la imagen grupal.
- Extraer embeddings para cada rostro detectado.
- Comparar cada embedding con la base de datos para encontrar el estudiante más parecido.
- Visualizar los resultados mostrando cada rostro con su nombre predicho y la foto de referencia, sin modificar la imagen grupal original.

5. **Exploración con Embeddings ArcFace (InsightFace)**
**Descripción:**
Se implementa un pipeline alternativo de generación de embeddings utilizando ArcFace, un modelo basado en InsightFace que ha demostrado gran efectividad en reconocimiento facial.

**Proceso:**

- Inicialización y configuración del modelo ArcFace con soporte para GPU o CPU según disponibilidad.
- Extracción de embeddings de cada imagen en la carpeta de datos.
- Clasificación basada en similitud coseno con la base de datos de embeddings ArcFace.
- Visualización detallada con etiquetas que muestran nombre real, nombre predicho, puntuación de similitud y estado (correcto o no).

Importancia:
Proporciona una alternativa robusta para mejorar la precisión del sistema y comparar el desempeño frente a FaceNet, facilitando la elección del mejor modelo para el caso de uso.

## Instalación

Para instalar todas las dependencias necesarias, asegúrate de tener Python 3.12 instalado y ejecuta los siguientes comandos:

```bash
pip install numpy
pip install pandas
pip install opencv-python
pip install pillow
pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu118  # o sin CUDA si no tienes GPU
pip install insightface
pip install tensorflow
pip install keras
pip install scikit-learn
pip install matplotlib
pip install tqdm
pip install openpyxl
pip install facenet-pytorch
pip install requests
```

## Uso

A continuación, se muestra cómo puedes ejecutar algunos de los scripts principales del proyecto:

```bash
python src/tu_script.py
```

- Descargar imágenes desde el archivo Excel:
```bash
python src/descargar_imagenes.py
```

- Generar embeddings con FaceNet:
```bash
python src/generar_embeddings_facenet.py
```

- Generar embeddings con FaceNet:
```bash
python src/generar_embeddings_dict.py
```

- Generar embeddings con ArcFace:
```bash
python src/generar_embeddings__dict_arcface.py
```

- Clasificar y mostrar resultados usando ArcFace:
```bash
python src/clasificar_y_mostrar.py --modelo arcface
```


## Requisitos

![Python](https://img.shields.io/badge/Python-3.12-blue)
![pandas](https://img.shields.io/badge/pandas-2.2.2-orange)

## Acceso al Google Colab

Puedes acceder al repositorio completo [aquí](https://colab.research.google.com/drive/1ZPEX9MfHoFJl8TevM-20OUINn0KoyLrw?usp=sharing).

## Contacto

Para cualquier duda o sugerencia, no dudes en contactarnos a través de [YEIMY](yeimyaalmanz@gmail.com), [THOMAS](ts.orjuelam@gmail.com) y [LINA](rozolina20@gmail.com).
