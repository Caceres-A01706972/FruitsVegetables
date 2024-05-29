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

## Estructura del Código (Hasta el 26 de mayo de 2024) 📁
- **Conexión a Google Drive y Directorio**
- **Importar Librerías**
- **Directorio de Datos:** Se definen los directorios que contienen los datos tanto de entrenamiento como de prueba (Train, Test)
- **Visualización del Dataset:** Mostrar ejemplos aleatorios de imagenes con sus categorías correspondientes.
- **Data Augmentation:** Se aplica Data Augmentation al conjunto de entrenamiento (Se aplican transformaciones como rotación, zoom,  horizontal_flip)
- **Primera Implementación del Modelo:** Definición y compilación del modelo inicial.
- **Entrenamiento del Modelo:** Entrenar el modelo ocupando el conjunto de Train y el de Validation.
- **Visualización del Rendimiento:** Análisis de los resultados del entrenamiento y evaluación del modelo para detectar overfitting o underfitting.
- **Guardar el Modelo:** Guardar el modelo entrenado para su uso futuro.

## Preprocesamiento y Data Augmentation 📈
Para mejorar el rendimiento del modelo y evitar el sobreajuste, se aplicaron técnicas de preprocesamiento y data augmentation a los datos de entrenamiento. El preprocesamiento y la data augmentation son pasos cruciales en el desarrollo de modelos de deep learning, especialmente en tareas de clasificación de imágenes.

### Normalización
Para la normalización de los valores de los píxeles, se utilizó `ImageDataGenerator` de Keras con el parámetro `rescale=1./255`. Esto escala los valores de los píxeles de [0, 255] a [0, 1], lo cual es beneficioso porque los modelos de redes neuronales tienden a converger más rápido y de manera más estable cuando los valores de entrada están en un rango más pequeño y uniforme.

### Data Augmentation
La data augmentation se implementó usando diversas transformaciones para aumentar la variabilidad del conjunto de entrenamiento. Las transformaciones incluyeron rotación, zoom y volteo horizontal. Estas técnicas ayudan al modelo a generalizar mejor al introducir variaciones que el modelo puede encontrar en datos no vistos durante el entrenamiento.

### Generadores de Datos
Se crearon generadores de datos para los conjuntos de entrenamiento, validación y prueba utilizando ImageDataGenerator. Estos generadores permiten cargar las imágenes en lotes y aplicar las transformaciones definidas en tiempo real, optimizando así el uso de memoria y el rendimiento del entrenamiento.


## Primera Implementación del Modelo 🧠
La implementación del modelo se basó en una arquitectura de red neuronal convolucional (CNN) por su eficiencia en problemas de clasificación de imagenes como lo es en el caso de este proyecto.
En la CNN se implementaron varias capas de convolución y pooling ara extraer las características de las imágenes, seguidas de capas densas para realizar la clasificación final.

### Estructura del Modelo
1. Capas Convolucionales y de Pooling:
    - Se agregaron 3 capas convolucionales. La primera de 32 filtros con una función de activación 'relu' (Rectified Linear Unit) se eligió por su capacidad para introducir no linealidad, permitiendo al modelo aprender características complejas. Esta capa es seguida por una capa de MaxPooling con un tamaño de pool de 2x2 para reducir la dimensionalidad y extraer características de manera más eficiente. Las otras capas convolucionales se aumentaron los filtros para que se puedan aprender características de mayor nivel.
2. Capas Densas y Dropout:
    - Una capa densa con la función de activación "relu". Esta capa ayuda para que en combinación con las características aprendidas en las capas convolucionales, se pueda hacer la clasificación.
    - Se añadio una capa de Dropout seteada en 0.5 para prevenir el sobreajuste, una técnica recomendada en el siguiente research paper: https://jmlr.org/papers/volume15/srivastava14a/srivastava14a.pdf
3. Capa de Salida:
    - En la capa de salida se ocupa la función de activación "Softmax" para proporcionar una distribución de probabilidad sobre las diferentes clases de frutas y vegetales. Referencia Textbook: https://github.com/janishar/mit-deep-learning-book-pdf/blob/master/complete-book-pdf/Ian%20Goodfellow%2C%20Yoshua%20Bengio%2C%20Aaron%20Courville%20-%20Deep%20Learning%20(2017%2C%20MIT).pdf

### Evaluación del Modelo 📊
- **Epoch 1/30**:
  - Loss: 3.4358 - Accuracy: 0.0704
  - Val_Loss: 2.8538 - Val_Accuracy: 0.2062

- **Epoch 30/30**:
  - Loss: 1.4369 - Accuracy: 0.5582
  - Val_Loss: 0.7331 - Val_Accuracy: 0.7937
<p align="center">
  <img src="https://github.com/Caceres-A01706972/FruitsVegetables/assets/83652905/0f0d7a52-2b17-40d7-9772-b7d68b02bdd1" width="45%" />
  <img src="https://github.com/Caceres-A01706972/FruitsVegetables/assets/83652905/e42aff90-14e7-4b58-afd0-53008fa531b4" width="45%" />
</p>

### Análisis del Rendimiento del Modelo
El entrenamiento mostró una mejora continua en la precisión tanto en el conjunto de entrenamiento como en el de validación.
- Inicialmente, se puede observar un underfitting inicial ya que la precisión es muy baja en ambos conjuntos.
- Finalmente, se puede observar un progreso hacia el Overfitting ya que el aumento en la precisión del Train junto con una tasa de mejora más lenta en el conjunto de Validation. Esto significa que el modelo estaba empezando a hacer Overfitting.
    - El Overfitting significa que el modelo se esta ajustando demasiado a lso datos de Training, (podríamos decir que esta memorizando), esto afecta negativamente su rendimientoe en datos no vistos. Lo que en nuestra clasificación final cuando querramos darle una imágen cualquiera (sacada de internet, o una real) tendrá un rendimiento negativo incapaz de clasificar que fruta o vegetal es.

### Posibles Soluciones para Mejorar el Rendimiento 🚀
1. Aumentar el Data Augmentation: Incrementar las transformaciones aplicadas a las imágenes de entrenamiento para que el modelo vea una mayor variedad de datos.
2. Transfer Learning con MobileNet: Usar modelos preentrenados como MobileNet para mejorar el rendimiento del clasificador, aprovechando características ya aprendidas de grandes datasets.
    - **Se explorará esta opción de Solución para mejorar el Modelo**.

## Siguientes Pasos
- **Segunda Implementación del Modelo**: Explorar la implementación de Transfer Learning con MobileNet.
- Implementar Interfaz para facilitar el uso del modelo ya entrenado.

