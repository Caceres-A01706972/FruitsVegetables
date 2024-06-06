# 🥭🍎 Clasificador de Frutas y Vegetales 🥦🍌

## Descripción del Proyecto 💻
El objetivo de este proyecto es desarrollar un clasificador de frutas y vegetales utilizando técnicas de aprendizaje automático.

Lo principal es clasificar imágenes estáticas de frutas y vegetales.

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
    - Se agregaron 3 capas convolucionales. La primera de 32 filtros con una función de activación `relu` (Rectified Linear Unit) se eligió por su capacidad para introducir no linealidad, permitiendo al modelo aprender características complejas. Esta capa es seguida por una capa de MaxPooling con un tamaño de pool de 2x2 para reducir la dimensionalidad y extraer características de manera más eficiente. Las otras capas convolucionales se aumentaron los filtros para que se puedan aprender características de mayor nivel.
2. Capas Densas y Dropout:
    - Una capa densa con la función de activación `relu`. Esta capa ayuda para que en combinación con las características aprendidas en las capas convolucionales, se pueda hacer la clasificación.
    - Se añadio una capa de Dropout seteada en 0.5 para prevenir el sobreajuste, una técnica recomendada en el siguiente research paper: https://jmlr.org/papers/volume15/srivastava14a/srivastava14a.pdf
3. Capa de Salida:
    - En la capa de salida se ocupa la función de activación `Softmax` para proporcionar una distribución de probabilidad sobre las diferentes clases de frutas y vegetales. Referencia Textbook: https://github.com/janishar/mit-deep-learning-book-pdf/blob/master/complete-book-pdf/Ian%20Goodfellow%2C%20Yoshua%20Bengio%2C%20Aaron%20Courville%20-%20Deep%20Learning%20(2017%2C%20MIT).pdf

### Evaluación del Modelo 📊
Durante la evaluación del modelo, se ha seguido la métrica de evaluación de `Accuracy`, ya que es la técnica utilizada en el paper de Pathak, Rupali. (2021). CLASSIFICATION OF FRUITS USING CONVOLUTIONAL NEURAL NETWORK AND TRANSFER LEARNING MODELS. https://www.researchgate.net/publication/364254116_CLASSIFICATION_OF_FRUITS_USING_CONVOLUTIONAL_NEURAL_NETWORK_AND_TRANSFER_LEARNING_MODELS


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

- **Conjunto de Test**
    - Accuracy Test Set: 2.79%

### Análisis del Rendimiento del Modelo
El entrenamiento mostró una mejora continua en la precisión tanto en el conjunto de entrenamiento como en el de validación.
- Inicialmente, se puede observar un underfitting inicial ya que la precisión es muy baja en ambos conjuntos.
- Finalmente, se puede observar un progreso hacia el Overfitting ya que el aumento en la precisión del Train junto con una tasa de mejora más lenta en el conjunto de Validation. Esto significa que el modelo estaba empezando a hacer Overfitting.
    - El Overfitting significa que el modelo se esta ajustando demasiado a lso datos de Training, (podríamos decir que esta memorizando), esto afecta negativamente su rendimientoe en datos no vistos. Lo que en nuestra clasificación final cuando querramos darle una imágen cualquiera (sacada de internet, o una real) tendrá un rendimiento negativo incapaz de clasificar que fruta o vegetal es.

### Posibles Soluciones para Mejorar el Rendimiento 🚀
1. Aumentar el Data Augmentation: Incrementar las transformaciones aplicadas a las imágenes de entrenamiento para que el modelo vea una mayor variedad de datos.
2. Transfer Learning con MobileNet: Usar modelos preentrenados como MobileNet para mejorar el rendimiento del clasificador, aprovechando características ya aprendidas de grandes datasets.
    - **Se explorará esta opción de Solución para mejorar el Modelo**.

## Segunda Implementación del Modelo 🧠

### Preprocesado y Data Augmentation 🖼️
El **data augmentation** se aplicó al conjunto de entrenamiento para aumentar la diversidad de las imágenes de entrenamiento y ayudar al modelo a generalizar mejor. Las técnicas aplicadas incluyen:

- **Rescale**: Los valores de los píxeles se escalaron a un rango de [0, 1] dividiendo por 255.
- **Rotation**: Rotación aleatoria de las imágenes en un rango de 30 grados.
- **Zoom**: Zoom aleatorio en un rango de 15%.
- **Width Shift**: Desplazamiento horizontal aleatorio en un rango de 20% del ancho total de la imagen.
- **Height Shift**: Desplazamiento vertical aleatorio en un rango de 20% del alto total de la imagen.
- **Shear**: Transformación de corte (shear) en un rango de 15%.
- **Horizontal Flip**: Inversión horizontal aleatoria de las imágenes.
- **Fill Mode**: Llenado de los píxeles vacíos con el valor más cercano.
  
Para los conjuntos de validación y prueba, no se aplicaron técnicas de data augmentation. Solo se **reescalaron** los valores de los píxeles a un rango de [0, 1] para asegurar que las imágenes de validación y prueba tengan la misma escala que las de entrenamiento.

### Estructura del Modelo

1. **Capas Convolucionales y de Pooling**:
    - **Primera Capa Convolucional**:
        - `Conv2D(32, (3, 3), activation="relu", input_shape=(224, 224, 3))`: La primera capa convolucional tiene 32 filtros de tamaño 3x3 y utiliza la función de activación `relu` (Rectified Linear Unit), que introduce no linealidad, permitiendo al modelo aprender características complejas. La capa de entrada espera imágenes de tamaño 224x224 con 3 canales de color (RGB).
        - `MaxPooling2D((2, 2))`: Esta capa de pooling reduce las dimensiones espaciales de la imagen (224x224 a 112x112), disminuyendo la complejidad computacional y ayudando a controlar el sobreajuste.
    - **Segunda Capa Convolucional**:
        - `Conv2D(64, (3, 3), activation="relu")`: La segunda capa convolucional tiene 64 filtros de tamaño 3x3 y utiliza la función de activación `relu`.
        - `MaxPooling2D((2, 2))`: Otra capa de pooling para reducir las dimensiones espaciales (112x112 a 56x56).
    - **Tercera Capa Convolucional**:
        - `Conv2D(128, (3, 3), activation="relu")`: La tercera capa convolucional tiene 128 filtros de tamaño 3x3 y utiliza la función de activación `relu`.
        - `MaxPooling2D((2, 2))`: La capa de pooling reduce aún más las dimensiones espaciales (56x56 a 28x28).
    - **Cuarta Capa Convolucional**:
        - `Conv2D(256, (3, 3), activation="relu")`: La cuarta capa convolucional tiene 256 filtros de tamaño 3x3 y utiliza la función de activación `relu`.
        - `MaxPooling2D((2, 2))`: La última capa de pooling reduce las dimensiones espaciales a (28x28 a 14x14).

2. **Capas Densas**:
    - `Flatten()`: Aplana la salida tridimensional de la última capa convolucional, preparándola para las capas densas.
    - `Dense(512, activation="relu")`: Una capa densa con 512 unidades y la función de activación `relu`. Esta capa aprende de las características extraídas por las capas convolucionales y ayuda en la clasificación.

3. **Capa de Salida**:
    - `Dense(36, activation="softmax")`: La capa de salida tiene 36 unidades (correspondientes a las 36 clases de frutas y vegetales) y utiliza la función de activación `softmax` para proporcionar una distribución de probabilidad sobre las diferentes clases. Referencia Textbook: https://github.com/janishar/mit-deep-learning-book-pdf/blob/master/complete-book-pdf/Ian%20Goodfellow%2C%20Yoshua%20Bengio%2C%20Aaron%20Courville%20-%20Deep%20Learning%20(2017%2C%20MIT).pdf
      
### Evaluación del Modelo 📊
Durante la evaluación del modelo, se ha seguido la métrica de evaluación de `Accuracy`, ya que es la técnica utilizada en el paper de Pathak, Rupali. (2021). CLASSIFICATION OF FRUITS USING CONVOLUTIONAL NEURAL NETWORK AND TRANSFER LEARNING MODELS. https://www.researchgate.net/publication/364254116_CLASSIFICATION_OF_FRUITS_USING_CONVOLUTIONAL_NEURAL_NETWORK_AND_TRANSFER_LEARNING_MODELS

- **Epoch 1/15**:
  - Loss: 3.1972 - Accuracy: 0.1128
  - Val_Loss: 2.5543 - Val_Accuracy: 0.2232

- **Epoch 15/15**:
  - Loss: 1.5531 - Accuracy: 0.5148
  - Val_Loss: 1.2925 - Val_Accuracy: 0.5884

- **Test Set**:
    - Loss: 1.2927 - Accuracy: 0.5892 

<p align="center">
  <img src="https://github.com/Caceres-A01706972/FruitsVegetables/assets/83652905/09681f3c-97e5-478d-be42-1c2d87969547" width="45%" />
  <img src="https://github.com/Caceres-A01706972/FruitsVegetables/assets/83652905/dedc6e0f-d88c-4711-9ff1-4b0c80816f41" width="45%" />
</p>

### Análisis del Rendimiento del Modelo
Observamos que la brecha entre el Accuracy del conjunto de Train y del conjunto de Validation se ha reducido en comparación con la implementación del primer modelo. Esto sugiere que el modelo ha mejorado su capacidad para generalizar a datos nuevos y no está sobreajustando tanto como antes.

La precisión final del modelo en el conjunto de Validation es del 58.84%, lo que indica un rendimiento razonable en la clasificación de frutas y vegetales.
Dado que la precisión del conjunto de Train y del conjunto de Validation son parecidas al final del entrenamiento, no parece haber signos claros de overfitting o underfitting en este punto.

### Posibles Soluciones para Mejorar el Rendimiento 🚀
1. Aumentar el número de épocas en el entrenamiento.
2. Transfer Learning con MobileNet: Usar modelos preentrenados como MobileNet para mejorar el rendimiento del clasificador, aprovechando características ya aprendidas de grandes datasets.
    - **Se explorará esta opción de Solución para mejorar el Modelo**.

## Siguientes Pasos
- Implementación de modelo con Transfer Learning de MobileNetV2

## Implementación Final del Modelo utilizando MobileNetV2 🧠🚀
Para esta implementación, se utilizó el modelo MobileNetV2 preentrenado en ImageNet. Este modelo aprovecha las características aprendidas de grandes datasets y adapta el modelo a la tarea específica de clasificación de frutas y vegetales.

### Preprocesado y Data Augmentation 🖼️
El `preprocesado` y la `data augmentation` se realizaron de la siguiente manera:

- **Rescale**: Los valores de los píxeles se escalaron a un rango de [0, 1].
- **Data Augmentation**: Rotación, zoom, desplazamiento horizontal y vertical, transformación de corte y volteo horizontal.

### Estructura del Modelo

1. **MobileNetV2 como Base:**
    - Se utilizó el modelo MobileNetV2 preentrenado en ImageNet, excluyendo las capas superiores (`include_top=False`). Este modelo se configuró como no entrenable (`trainable=False`) para mantener las características preaprendidas.
2. **Capas Adicionales:**
    - `Dense(128, activation="relu"):` Dos capas densas con 128 unidades y la función de activación relu para aprender nuevas características específicas del dataset.
    - `Dense(36, activation="softmax")`: La capa de salida con 36 unidades y la función de activación softmax para la clasificación de las frutas y vegetales. Referencia Textbook: https://github.com/janishar/mit-deep-learning-book-pdf/blob/master/complete-book-pdf/Ian%20Goodfellow%2C%20Yoshua%20Bengio%2C%20Aaron%20Courville%20-%20Deep%20Learning%20(2017%2C%20MIT).pdf

### Evaluación del Modelo 📊
Durante la evaluación del modelo, se ha seguido la métrica de evaluación de `Accuracy`, ya que es la técnica utilizada en el paper de Pathak, Rupali. (2021). CLASSIFICATION OF FRUITS USING CONVOLUTIONAL NEURAL NETWORK AND TRANSFER LEARNING MODELS. https://www.researchgate.net/publication/364254116_CLASSIFICATION_OF_FRUITS_USING_CONVOLUTIONAL_NEURAL_NETWORK_AND_TRANSFER_LEARNING_MODELS

- **Epoch 1/5**:
  - Loss: 1.6736 - Accuracy: 0.5543
  - Val_Loss: 0.3880 - Val_Accuracy: 0.9014

- **Epoch 5/5**:
  - Loss: 0.1412 - Accuracy: 0.9563
  - Val_Loss: 0.1477 - Val_Accuracy: 0.9623

- **Test Set**:
    - Accuracy on the test set: 96.32%

<p align="center">
    <img src="https://github.com/Caceres-A01706972/FruitsVegetables/assets/83652905/2b98e5e3-37c7-4c8b-abfb-112351083254" width="45%" />
    <img src="https://github.com/Caceres-A01706972/FruitsVegetables/assets/83652905/582bc20c-b358-42a3-a76f-80a112c80794" width="45%" />
</p>

### Análisis del Rendimiento del Modelo
El modelo muestra una mejora constante en la precisión tanto en el conjunto de entrenamiento como en el de validación a lo largo de las épocas. Los resultados indican una mejora significativa en el rendimiento del modelo a lo largo del tiempo. La precisión final en el conjunto de validación fue del 96.23%, lo que indica una capacidad de generalización robusta.

En resumen, el modelo muestra un excelente rendimiento tanto en los datos de entrenamiento como en los de validación, sin indicios significativos de overfitting o underfitting. La alta precisión en el conjunto de prueba (96.32%) confirma la capacidad del modelo para generalizar bien a datos no vistos durante el entrenamiento.

### Matriz de Confusión
![image](https://github.com/Caceres-A01706972/FruitsVegetables/assets/83652905/bb367b7c-12eb-40ef-81bb-fc2797813fb8)

## Clasification Report
![image](https://github.com/Caceres-A01706972/FruitsVegetables/assets/83652905/977bceac-b1f7-4ac4-bda7-fe587b1715ee)


### Utilizar Modelo
![image](https://github.com/Caceres-A01706972/FruitsVegetables/assets/83652905/64cd5897-de39-4195-84ae-982546cae80b)


