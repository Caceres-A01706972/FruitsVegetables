# 🥭🍎 Clasificador de Frutas y Vegetales 🥦🍌

## Descripción del Proyecto 💻
El objetivo de este proyecto es desarrollar un clasificador de frutas y vegetales utilizando técnicas de aprendizaje automático.

Lo principal es clasificar imágenes estáticas de frutas y vegetales. Pero en futuras versiones se planea extender esta capacidad para clasificar en tiempo real utilizando la cámara, permitiendo llevar un registro de la cantidad de cada producto mostrado. 

Esta funcionalidad está diseñada para facilitar el conteo y seguimiento de productos en un entorno de supermercado.

## Dataset 📊
El dataset utilizado contiene imágenes de diversas frutas y vegetales organizadas en carpetas según su categoría. Los datos están divididos en dos conjuntos principales:

- Conjunto de Entrenamiento: Utilizado para entrenar el modelo.
    - (Contiene 36 clases, 100 imagenes en cada clase)
- Conjunto de Prueba: Utilizado para evaluar el rendimiento del modelo.
    - (Contiene 36 clases, 10 imagenes en cada clase)
- Conjunto de Validación: Utilizado para ajustar los hiperparámetros del modelo y evaluar su rendimiento durante el entrenamiento sin influir en las decisiones de diseño del modelo.
    - (Contiene 36 clases, 10 imagenes cada uno)
  
Cada categoría de frutas y vegetales tiene su propia carpeta, y cada carpeta contiene varias imágenes en formatos .png, .jpg o .jpeg.

El dataset se puede descargar desde el siguiente enlace: 
[Dataset de Frutas y Vegetales](https://drive.google.com/drive/folders/1Jkadebp3GhvkF-c1rBmxgevV6G_3diNX?usp=sharing)

El dataset original puede ser encontrado en el siguiente enlace:
[Dataset en Kaggle](https://www.kaggle.com/datasets/kritikseth/fruit-and-vegetable-image-recognition)

## Estructura del Código (Hasta el 18 de mayo de 2024) 📁
- **Conexión a Google Drive y Directorio**
- **Importar Librerías**
- **Directorio de Datos:** Se definen los directorios que contienen los datos tanto de entrenamiento como de prueba (Train, Test)
- **Visualización del Dataset:** Mostrar ejemplos aleatorios de imagenes con sus categorías correspondientes.
- **Data Augmentation:** Se aplica Data Augmentation al conjunto de entrenamiento (Se aplican transformaciones como rotación, zoom,  horizontal_flip)
