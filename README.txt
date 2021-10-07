Informacion sobre la Red Neuronal

Antes de todo para crear las red neuronal intenta crear una carpeta con el nombre de esta o nombre a gusto.
Dentro de la misma carpeta crear dos carpetas una que se deberia llamar data donde pondremos todas las imagenes que quieras 
(dentro de las carpetas entrenamiento y validacion) y la otra modelo.
Dentro de esta misma carpeta crea otras dos carpetas que una sera para el entrenamiento y la otra validacion
(dependiendo que es lo que quieres que entrene ejemplo: perros y gatos, una carpeta para cada uno, tambien para la carpeta de validacion).
Bueno en la carpeta red neuronal agrega imagenes que no esten en las carpetas de entrenamiento y validacion.

Todas las librerias en si funcionas mientras tanto cumpla que tengas instalada la libreria primordial Tensorflow 
por ende si presentas un error se deba que falta de instalacion de esta(se debe a que las nuevas actualizaciones 
de version de spyder,intenta usar una version anterior, recomiendo la 4.2.5 ) si el problema persite hacer los siguientes pasos para su instalacion.

Pasos para instalar Tensorflow y paquetes:

1.-puedes crear un ambiente en el mismo anaconda 
solo abriendo cmd(simbolos de sistema), si no quieres crear un ambiente puedes usar el que esta por deafult en anaconda
solo brincate en la parte de activacion de esta.

2.-comandos para crear un ambiente:
create --name (Aqui puedes poner el nombre que gustes)
despues te preguntara si quieres proceder(Proceed ([y]/n)) escribes y

3.-comandos para verificar o activar un ambiente:
para verificar si ya esta nuestro ambiente hay que activarlo, escribimos lo siguiente.
activate (nombre que pusiste)
si lo pusiste correctamente debe aparecer asi (nombre de tu ambiente) C:\User\etc\etc juan> 
Pd: dentro de anaconda hay un apartado que se llama root dale click en la flecha hacia abajo y pon tu ambiente que creaste.

4.-comandos para la instalacion de Tensorflow en cmd:
dentro de nuestro ambiente sea nuevo o el default, escribimos (conda install tensorflow)
(pedira algunas validaciones solo es cuestion de darle que si, si es que se requiera,
tarda un tiempo solo es de esperar).
tambien puedes instalar algunas otras librerias desde cmd, otra seria conda install o pip install nltk

5.-para verificar que se instalo correctamente intenta importar Tensorflow (spyder o jupyter),
Pd:en spyder en la parte inferior derecha puedes importar las librerias que requieras. 

import tensorflow
import sklearn 
import nltk

por todo lo demas deberia funcionar correctamente si seguistes lo pasos anteriores.

1.- Entrenamiento 
Primero explicare que hace cada libreria: 

tensorflow.python.keras.preprocessing.image import ImageDataGenerator: ayuda pre-procesar las imagenes que vayamos
a usar para el entrenamiento a nuestro algoritmo.

tensorflow.python.keras import optimizers: es nuestro optimizador de nuestro algortimo que sera entrenado.

tensorflow.python.keras.models import Sequential: es una libreria que nos permite hacer redes neuronales secuenciales.
es decir que cada una de las capas esta en orden.


tensorflow.python.keras.layers import Dropout, Flatten, Dense, Activation: uno viene siendo densidad y el otro es el ajuste o corte de esta para que no 
solo aprende un camino de cada clase si no que tome varios con la finalidad de ser mas acertada.

tensorflow.python.keras.layers import  Convolution2D, MaxPooling2D: estas son importantes ya que son nuestras capas donde haran convoluciones 
y MaxPooling.


tensorflow.python.keras import backend as K: basicamente si tienes keras en disposicion o iniciada hace que todo sera desde cero, 
osea la red neuronal aprenda desde cero(si se utiliza en otro pc iniciar como nuevo).

en esta parte es donde va nuestro directorio de imagenes tanto de entrenar como las de validacion
data_entrenamiento = './data/entrenamiento'
data_validacion = './data/validacion'

Parametros
epocas =  numero de veces que vamos iterar sed de datos de entrenamiento.
logintud,altura =  tamaño que se va procesar nuestras imagenes
batch_size = numero de imagenes que nuestra computadora va a procesar
pasos = es el numero de veces que se va a procesar la informacion en cada epoca.
pasos_validacion= numeros de pasos que se va recorrer para despues ver que esta aprendiendo nuestro algoritmo
filtrosConv1 = tanto este como el filtroConv2 son el numero de filtros que tomara en cada convolucion y la profundida que tomara de cada imagen. 
tamano_filtro1 = tanto este como el tamano_filtro2 son el tamaño de nuestros filtros que contendra cada convoluciones.
tamano_pool = tamaño  del filtro del pooling.
clases = son el numero de clases que utilices (ejemplo de clase : gato y perro)
lr = es el numero de ajuste para que tan optimo sea nuestro resultado.

 
tanto como preparacion de imagenes como cnn=Sequential ya eesta explicado cada accion sien embargo las demas
acciones del codigo solo son para mejorar la red neuronal y que tenga mejor eficacia.

la carpeta de modelo solo sirve para almacenar lo aprendido en la red neuroanl una vez estudiado las clases.


2.-Prediccion
todo esto nos sirve para amndar a llamar la carpeta de modelo que genero el estudio de 
cada una de las clases o imagenes con la misma logintud, altura del entrenamiento. 
longitud, altura = 150, 150
modelo ='./modelo/modelo.h5'
pesos_modelo ='./modelo/pesos.h5'
cnn = load_model(modelo)
cnn.load_weights(pesos_modelo)

en este apartado de codigo solo es para calcular la iamgen en su altura, logintud
tambien para verificar si esta no es muy notoria puede expandirse y ver pixel por pixel
y tenga un resultado optimo cuando mencione una de las clases que se desea alcanzar usando un arreglo. 
def predict(file):
  x = load_img(file, target_size=(longitud, altura))
  x = img_to_array(x)
  x = np.expand_dims(x, axis=0)
  array =cnn.predict(x)
  result = array[0]
  answer = np.argmax(result)
  if answer == 0:
    print("pred: Ferrari")
  elif answer == 1:
    print("pred: Lamborghini")

en este apartado es para que escribas las imagene que deseas, que te diga de que clase proviene y si la red neuronal cumple con su funcion te dara la mejor respuesta.
predict('lamb3.jpg')
