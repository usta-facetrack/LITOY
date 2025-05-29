<div align="center">

# Proyecto Reconocimiento Facial y Clasificación de Género

**Autores:**  
_Yeimy Katherine Alarcón Almanza_, _Thomas Santiago Orjuela Martínez_ y _Lina Manuela Rozo Clavijo_

**Universidad Santo Tomás**  
_Pregrado Estadística_  
**Redes Neuronales**  
_Profesor: Isaac Zainea_

</div>

Este proyecto integra redes neuronales convolucionales, modelos de embeddings faciales y técnicas para construir un sistema que clasifica el género de un rostro humano y reconoce a estudiantes en imágenes grupales, con fines como el registro de asistencia automatizado.

![Python](https://img.shields.io/badge/Python-3.10-blue)
![pandas](https://img.shields.io/badge/pandas-2.2.3-orange)
![tqdm](https://img.shields.io/badge/tqdm-4.67.0-lightgrey)


## Introducción

El reconocimiento facial es una tecnología cada vez más presente en diversas aplicaciones, desde seguridad hasta análisis biométrico y control de acceso. En este proyecto se desarrolla un sistema integral de reconocimiento facial para identificar estudiantes a partir de sus fotos, complementado con un modelo de clasificación de género basado en redes neuronales convolucionales. Se emplean métodos avanzados para la extracción y comparación de características faciales, incluyendo modelos reconocidos como FaceNet y ArcFace.

Este proyecto aborda todos los pasos desde la descarga y organización automática de imágenes, la generación de embeddings faciales, la detección y reconocimiento en imágenes grupales, hasta la evaluación exhaustiva de los modelos implementados. Además, se incluye la exploración de nuevos modelos para mejorar la precisión y robustez del sistema.

## Objetivo General
Desarrollar un sistema de reconocimiento facial que clasifique el género y reconozca estudiantes por medio de imágenes, utilizando deep learning y embeddings, para automatizar el registro de asistencia y evaluar su precisión en contextos reales.

## Objetivos Específicos 
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

**Importancia:**

Este proceso establece una base de datos estructurada y confiable que puede ser reutilizada a lo largo de todo el pipeline. Además, permite escalar fácilmente el sistema a nuevos estudiantes, ya que nuevas imágenes pueden ser añadidas y procesadas automáticamente sin necesidad de intervención manual adicional.

2. **Modelo de Clasificación de Género con CNN**
   
**Descripción:**
Se desarrolla una red neuronal convolucional (CNN) entrenada con TensorFlow/Keras para clasificar las imágenes faciales en dos categorías: "Hombre" y "Mujer".

**Proceso:**

- Preprocesamiento de imágenes (normalización, resizing, data augmentation).
- Arquitectura CNN personalizada o basada en modelos estándar (p.ej., MobileNet, ResNet).
- Entrenamiento supervisado con etiquetas de género previamente definidas.
- Evaluación del modelo utilizando métricas como: Accuracy(porcentaje de clasificaciones correctas) y Precision, Recall, y F1-score (para entender el equilibrio entre clases).

**Salida:**
Un modelo entrenado capaz de predecir el género a partir de una imagen facial nueva.

3. **Modelo de Reconocimiento Facial con CNN (TensorFlow/Keras)**

**Descripción:**
Se implementa un sistema de reconocimiento facial basado en una red neuronal convolucional (CNN) entrenada con TensorFlow/Keras, que identifica directamente a los estudiantes a partir de sus imágenes faciales. Este modelo no utiliza embeddings ni comparaciones, sino que clasifica cada rostro en una de las clases (estudiantes) disponibles.

**Proceso:**

- Carga y descarga automática de imágenes desde enlaces en Excel, organizadas por estudiante.
- Preprocesamiento: redimensionado, normalización y codificación de etiquetas con LabelEncoder.
- Creación de tf.data.Dataset, dividido en entrenamiento (70%) y validación (30%).
- Arquitectura CNN con capas Conv2D, MaxPooling, Flatten y Dense con softmax.
- Entrenamiento con sparse_categorical_crossentropy, optimizador Adam y EarlyStopping.
- Evaluación y visualización de predicciones junto a etiquetas reales.

**Aplicaciones:**
Este modelo es útil para sistemas rápidos de identificación facial donde se cuenta con imágenes bien etiquetadas. Además, puede complementar sistemas basados en embeddings como FaceNet o ArcFace, proporcionando una segunda vía para reconocimiento directo.

4. **Generación de Embeddings Faciales con MTCNN + FaceNet**

**Descripción:**
Para identificar individualmente a los estudiantes, se extraen vectores numéricos (embeddings) que representan características faciales únicas.

**Proceso:**

- Detección precisa de rostros en imágenes individuales usando MTCNN (Multi-task Cascaded Convolutional Networks).
- Extracción de embeddings faciales con FaceNet, un modelo basado en InceptionResnetV1 entrenado en VGGFace2.
- Almacenamiento de estos vectores en un diccionario serializado (.npy), con el nombre del estudiante como clave.

**Importancia:**
Los embeddings permiten comparar rostros mediante métricas de similitud (p. ej., coseno) de manera eficiente y precisa, clave para el reconocimiento facial.

5. **Reconocimiento Facial en Imágenes Grupales**
   
**Descripción:**
Este módulo permite detectar y reconocer múltiples rostros dentro de una imagen que contiene a varios estudiantes.

**Proceso:**

- Detectar múltiples rostros en la imagen grupal.
- Extraer embeddings para cada rostro detectado.
- Comparar cada embedding con la base de datos para encontrar el estudiante más parecido.
- Visualizar los resultados mostrando cada rostro con su nombre predicho y la foto de referencia, sin modificar la imagen grupal original.

**Importancia:**

Facilita la automatización de tareas como el registro de asistencia en clases o eventos mediante reconocimiento en fotos grupales.

6. **Exploración con Embeddings ArcFace (InsightFace)**
   
**Descripción:**
Se implementa un pipeline alternativo de generación de embeddings utilizando ArcFace, un modelo basado en InsightFace que ha demostrado gran efectividad en reconocimiento facial.

**Proceso:**

- Inicialización y configuración del modelo ArcFace con soporte para GPU o CPU según disponibilidad.
- Extracción de embeddings de cada imagen en la carpeta de datos.
- Clasificación basada en similitud coseno con la base de datos de embeddings ArcFace.
- Visualización detallada con etiquetas que muestran nombre real, nombre predicho, puntuación de similitud y estado (correcto o no).

**Importancia:**
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

Este proyecto está diseñado para ser usado principalmente mediante un **notebook interactivo en Google Colab** llamado:

- `Modeloface_embedding_facenet_mtcnn.ipynb`

Luego:
1. Abre el notebook `Modelo face_embedding_facenet_mtcnn.ipynb` en Google Colab.  
   Luego puedes clonarlo en tu máquina local o montarlo en tu Google Drive.

2. Ejecuta las celdas de instalación de requisitos (librerías y configuraciones necesarias) para que el código funcione correctamente.

3. Conecta tu cuenta de Google Drive en el entorno de Colab.  
   Asegúrate de que en tu Drive esté la carpeta con las fotos de los estudiantes y también el archivo Excel que contiene los nombres y enlaces a las imágenes almacenadas en Drive.

4. Ejecuta las celdas paso a paso para realizar todo el pipeline.

5. Visualiza y analiza los resultados generados en las celdas finales.

6. Puedes modificar parámetros y probar nuevas configuraciones directamente en el notebook para experimentar con el pipeline.

## Requisitos

![Python](https://img.shields.io/badge/Python-3.12-blue)
![pandas](https://img.shields.io/badge/pandas-2.2.2-orange)

## Conclusiones

Como se mostró en el resto del trabajo, presentamos dos distintos enfoques para el análisis comparativo de reconocimiento facial, con el fin de poder llevar un control de la asistencia presencial a clase por parte del estudiantado del curso. Explorando desde modelos clásicos de redes neuronales convolucionales (como lo son CNN). Hasta otras técnicas más modernas basadas en embeddings faciales. Después de realizar esto, con quedan las siguientes conclusiones:


1. **Construcción de un sistema integral de reconocimiento facial**

El trabajo logró integrar de manera exitosa múltiples modelos y metodologías en un sistema completo de reconocimiento facial. Este sistema abarca desde la detección de rostros y su preprocesamiento, hasta la extracción de características y la identificación de personas. La arquitectura modular desarrollada facilita su extensión y adaptación a distintos escenarios, lo cual es fundamental para su aplicabilidad en diversos contextos reales.

2. **Evaluación de enfoques clásicos y modernos de identificación facial**

Como fue mencionado, se compararon enfoques tradicionales basados en redes neuronales convolucionales entrenadas desde cero, con métodos modernos que emplean embeddings faciales generados por modelos pre-etrenados como FaceNet y ArcFace. Esta comparación permitió evidenciar cómo los modelos de última generación ofrecen ventajas sustanciales en precisión, escalabilidad y capacidad de generalización frente a métodos más simples. En particular, los modelos basados en embeddings demostraron ser más robustos ante variaciones en la posición de los estudiantes en las fotos, iluminación o sus expresiones faciales.

3. **Uso de herramientas accesibles y replicables**

El proyecto fue desarrollado completamente en Google Colab, utilizando bibliotecas de código abierto como facenet-pytorch, insightface, TensorFlow, y scikit-learn, lo cual lo hace accesible para otros investigadores o instituciones con recursos limitados. Este enfoque democratiza el acceso a tecnologías avanzadas de inteligencia artificial, fomentando su aplicación en distintos ámbitos sociales y educativos.

4. **Limitaciones Técnicas**
   
Capacidad de procesamiento computacional:
El entrenamiento de redes neuronales convolucionales (CNN) requiere recursos computacionales significativos, especialmente en tareas como la verificación facial. La falta de acceso a GPU o hardware especializado limitó la complejidad del modelo, el tamaño de los lotes y la cantidad de épocas que pudimos explorar, lo cual pudo afectar negativamente el desempeño.

Escasez y calidad de datos:
El tamaño reducido del conjunto de datos, así como la limitada diversidad de las imágenes (en términos de iluminación, poses, expresiones, etc.), restringieron la capacidad del modelo para generalizar. En tareas de verificación, la falta de suficientes imágenes por persona dificultó una comparación robusta entre pares de rostros.

5. **Errores Frecuentes Observados**
   
Sobreajuste en clasificación de género:
Se observó un alto rendimiento en entrenamiento pero una caída notable en validación, indicando que el modelo memorizó patrones específicos sin generalizar bien a datos nuevos.

Mal rendimiento en verificación facial (ROC-AUC < 0.5):
Los modelos de verificación (FaceNet + MTCNN y ArcFace) presentaron resultados equivalentes o peores que el azar. Esto puede atribuirse a errores en la detección de rostros, embeddings poco representativos o una mala configuración en la comparación de vectores.

Clasificaciones erróneas repetidas:
Algunos individuos fueron clasificados de forma incorrecta de manera sistemática, posiblemente por compartir características visuales similares con otra clase o por baja calidad de sus imágenes.

6. **Aspectos Éticos**
   
Sesgos en los datos y el modelo:
Si el dataset tiene una distribución desbalanceada de género, etnias o edades, los modelos pueden aprender sesgos implícitos y reproducirlos en sus predicciones. Esto es especialmente delicado en tareas de reconocimiento facial, donde los errores pueden tener consecuencias serias (por ejemplo, falsos positivos en sistemas de vigilancia).

Privacidad y consentimiento:
El uso de imágenes faciales implica el tratamiento de datos personales sensibles. Es fundamental contar con el consentimiento informado de las personas cuyas imágenes se utilizan, así como garantizar el almacenamiento seguro y ético de dicha información.

Aplicaciones malintencionadas:
Las tecnologías de reconocimiento facial pueden ser empleadas en contextos que vulneren los derechos humanos, como vigilancia masiva o discriminación automatizada. Por tanto, el desarrollo y aplicación de estos modelos debe regirse por principios éticos sólidos y marcos legales claros.

## Acceso al Google Colab

Puedes acceder al repositorio completo [aquí](https://colab.research.google.com/drive/1ZPEX9MfHoFJl8TevM-20OUINn0KoyLrw?usp=sharing).

## Contacto

Para cualquier duda o sugerencia, no dudes en contactarnos a través de [Yeimy Alarcón](yeimyaalmanz@gmail.com), [Thomas Orjuela](ts.orjuelam@gmail.com) y [Lina Rozo](rozolina20@gmail.com).
