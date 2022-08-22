# Reconocimiento de gestos usando mediapipe
El proyecto consiste en la predicción de los gestos que se puede realizar con las manos <br> 
En este programa de ejemplo se reconoce los gestos de la mano con machine learning usando la detección la detección de los puntos clave(key_points).<br>
<br>
Entrenamiento del modelo, pruebalo en collab-> [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/ZeroHoushou/ProjectManin/blob/master/detectorDeGestosv5.ipynb)

![mqlrf-s6x16](https://drive.google.com/uc?export=view&id=1xAjEOxZ7WMAe1NspahosqGcw4mjFiCUF)

El repositorio contiene lo siguiente:
* Programa de ejemplo
* Modelo de reconocimientos de gestos de las manos(TFLite)
* Aprendizaje de datos para el reconocimiento de gestos y notebooks para el aprendizaje

# Requerimientos
* mediapipe 
* OpenCV 3.4.2 or Later
* Tensorflow 2.3.0 or Later<br>
* scikit-learn 0.23.2 or Later (Solo si va a mostrar la matriz de confusión) 
* matplotlib 3.3.2 or Later

# Demo 
Para corre la aplicación de prueba utilice dentro de la carpeta del proyecto
```bash
python app.py
```
Se pueden configurar las siguientes opciones para ejecutar la demo.

* --device<br>Especificar el dispotivo de la cámara (Default：0)
* --width<br>Anho de la ventana(Default：960)
* --height<br>Alto de la ventana (Default：540)
* --use_static_image_mode<br>Whether to use static_image_mode option for MediaPipe inference (Default：Unspecified)
* --min_detection_confidence<br>
Detection confidence threshold (Default：0.5)
* --min_tracking_confidence<br>
Tracking confidence threshold (Default：0.5)

# Directorio (funcional)
<pre>
│  app.py
│  detectorDeGestosv5.ipynb 
│  
├─model
│  ├─keypoint_classifier
│    │  datasetDeGestos_v4.1.csv
│    │  datasetDeGestos_v4.1.hdf5
│    │  keypoint_classifier.py
│    │  keypoint_classifier.tflite
│    └─ keypoint_classifier_label.csv
│                 
└─utils
    └─cvfpscalc.py
</pre>
### app.py
Es el programa de prueba<br>


### detectorDeGestosv5.ipynb
Este es script para el modelo de entrenamiento para el reconocimiento de gestos.


### model/keypoint_classifier
This directory stores files related to hand sign recognition.<br>
The following files are stored.
* Training data(keypoint.csv)
* Trained model(keypoint_classifier.tflite)
* Label data(keypoint_classifier_label.csv)
* Inference module(keypoint_classifier.py)


### utils/cvfpscalc.py
Modulo para calcular los fps.

# Entrenamiento 💪 💪
Agregar y cambiar data de entrenamiento para el reconocimiento de gestos de manos.

### Entrenamiento del reconocimiento de gestos de manos
#### 1.Aprendiendo de colección de datos
Presionamos para para guardar los puntos clave（Se muestra como  「MODE:Logging Key Point」）<br>
![mqlrf-s6x16](https://drive.google.com/uc?export=view&id=1xAjEOxZ7WMAe1NspahosqGcw4mjFiCUF)
<br><br>
Si se presiona 0 hasta el 9, los puntos clave se agregaran al archivo csv "model/keypoint_classifier/keypoint.csv" <br>
1st columna: Numero presionado (usado como clase ID), 2nd y siguientes columnas: Coordenadas de puntos clave.<br>
<img src="https://user-images.githubusercontent.com/37477845/102345725-28d26280-3fe1-11eb-9eeb-8c938e3f625b.png" width="80%"><br><br>
Los puntos clave coordinados 
Las coordenadas del punto clave son las que han sido sometidas al siguiente preprocesamiento hasta 5.<br>
<img src="https://user-images.githubusercontent.com/37477845/102242918-ed328c80-3f3d-11eb-907c-61ba05678d54.png" width="80%">
<img src="https://user-images.githubusercontent.com/37477845/102244114-418a3c00-3f3f-11eb-8eef-f658e5aa2d0d.png" width="80%"><br><br>
Como estado inicial, hay tres 5 tipos de datos de aprendizaje los cuales inclue:mano abierto(Clase ID:0), mano cerrada(Clase ID:1), apuntando (Class ID: 2),Me gusta (Class Id:3) y U pose (Class ID:4).
<img src="https://drive.google.com/uc?export=view&id=1sF026ejrKxjeMp-9tXWPtiUcCr2VKmAZ" width="25%">　<img src="https://drive.google.com/uc?export=view&id=10KVPd7ATAD0F5gDwXGvFgCmmAb_nt_uJ" width="25%">　

#### 2.Modelo de entrenamiento
Abrir "[detectorDeGestosv5.ipynb](detectorDeGestosv5.ipynb)" en Jupyter Notebook y ejecutar todas las fuciones<br>
Para cambiar el numero de clases de entramiento cambie el valor de la variable "NUM_CLASSES = 4" <br>y modifique el label "model/keypoint_classifier/keypoint_classifier_label.csv" al que corresponde.<br><br>

#### X.Estructura de Modelo
La imagen del modelo "[detectorDeGestosv5.ipynb](detectorDeGestosv5.ipynb)" es la siguiente:<br>
<img src="https://drive.google.com/uc?export=view&id=1zgsnd6gSyXKCfW3BJd6e3SkbU3MpWcti" height="10%" width="10%"><br><br>

# Referencia
* [MediaPipe](https://mediapipe.dev/)
* [Mediapipe a framework for building perception(Paper)](https://cs.paperswithcode.com/paper/mediapipe-a-framework-for-building-perception)

 
# Licencia
Este proyecto está bajo [Apache v2 license](LICENSE).
