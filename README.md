# IA_P3_Proyecto-Chatbot
_Seguimos el tutorioal de Sentdex para crear un chatbot con Python y TensorFlow._
_Tutorial Usado: https://pythonprogramming.net/chatbot-deep-learning-python-tensorflow/?authuser=0#google_vignette_

## 1. Preparación de la Información
###Informacion
_Use la informacion proporcionada de reddit para crear la database que uso mi chatbot._
_https://www.reddit.com/r/datasets/comments/3bxlg7/i_have_every_publicly_available_reddit_comment/?st=j9udbxta&sh=69e4fee7_
_En especifico los siguientes meses en diversas pruebas: '2015-05' , '2007-12', 2012-12, '2010-11'._
###Codigos para preparar la info
_Primero se corre el codigo [chatbot_database.py](https://github.com/AlejandraRG57/IA_P3_Proyecto-Chatbot/blob/main/chatbot_database.py) para preparar cada mes individualmente y hacerlo formato Data Base File, se va modificando la variable timeframe (linea 6) por cada mes, tabmbién se tiene que modificar la linea 96 para que de a la carpeta de nuestra info la tienen que tener de la siguiente forma:_
```
#Ejemplo(Asi lo puse yo)
(r'F:/2. Sexto Semestre/Inteligencia Artificial/Proyecto IA/reddit_data/{}/RC_{}'
#Las ultimas 3 partes no las tienen que cambiar "reddit_data/{}/RC_{}"
#1.Tienen que crear una carpeta llamada "reddit_data"
#2.Dentro de la carpeta "reddit_data" se tienen que crear carpetas de los años que usaron.
#Ej: "2010", "2015","2007","2012"
#3.Dentro de cada respectivo año poner los archivos de mes que querramos (no tienen que estar comprimidos).
#Ej de nombre que traen los archivos: "RC_2012-12"
```
```
#Linea 6
timeframe = '2010-11' #Meses usados: '2015-05' , '2007-12', 2012-12, '2010-11'
```
_Una vez finalizado el otro, corremos el codigo [create_training_data.py](https://github.com/AlejandraRG57/IA_P3_Proyecto-Chatbot/blob/main/create_training_data.py) en el cual al inicio en "timeframes" escibimos todos los meses que querramos usar, los archivos que nos genero el codigo [chatbot_database.py](https://github.com/AlejandraRG57/IA_P3_Proyecto-Chatbot/blob/main/chatbot_database.py) deben de estar en la misma carpeta que este nuevo codigo._
```
timeframes = ['2015-05','2010-11','2007-12','2012-12'] #Estos son los que yo use en uno de mis entrenamientos.
```
_Se nos van a generar 4 archivos, mas adelante vamos a usar el "train.to" y el "train.from"._
## 2. Creamos nuestro enviroment
Yo ultilice el Anaconda Prompt para realizacion del proyecto. Lo realice en un Enviroment ya que para varias instalaciones se necesitan en versiones especificas y podrian haber problemas de compatibilidad.
###Comandos
_Corremos el siguiente comando para crear el enviroment:_
```
conda create -n Chatbot python=3.6 
```
_Activamos nuestro Enviroment_
```
conda activate Chatbot
```
## 3. Preparamos nuestro enviroment
Primero con el anaconda prompt nos vamos a donde queremos que se guarde el repositorio que vamos a clonar.
_Yo cree una carpeta en midisco local F: llamada nmt-chatbot-master._
###Moverse en el Anaconda Prompt
Nos vamos a mover a ciertas carpetas dentro del mismo prompt.
_Por ejemplo asi es como yo me movi a la carpeta donde queria que se guardara el repositorio._
```
#Ejemplo(las direcciones en su computadora pueden variar)
F: #Primero me movi al disco F: ya que por default estaba en el C:
cd F:\nmt-chatbot-master #Despues me movi a la dirección de la carpeta que queria
```
###Clonar el repositorio
Estos son los comandos que vas a necesitar correr.
_Primero instalamos git en el repositorio (es una libreria necesaria)._
```
conda install git
```
_Procedemos a clonar el repositorio._
```
git clone --recursive https://github.com/daniel-kukiela/nmt-chatbot
```
###Instalar requerimientos
_Una vez que clonamos el repositorio nos movemos dentro de la carpeta que se creo._
```
cd nmt-chatbot
```
_Una dentro instalamos los requerimentos necesarios corriendo el siguiente comando._
```
pip install -r requirements.txt
```

## 4. Configuración del proyecto antes de entrenar
###Colocacion de archivos.
_Primero vamos a poner los archivos generados "train.to" y "train.from" en la carpeta "new_data"._

###Procesando la información.
_En este momento recomiendo entrar a la carpeta setup e ir al codigo "settings"_
Esto es lo que yo modifique pero dependera de la capacidad de su computadora y lo que quieran hacer lo que ustedes harán:
```
'vocab_size': 170000, #Linea 28, yo lo aumente a 170000 para que el chatbo tuviera un mayor léxico, pero seria mejor aun mas.
'batch_size': 128, #Este lo puedes bajar para aguantar un numero mayor de vocab_size pero depende de su computadora (posibles valores: 64, 32, 16, 8, 4).
```
_Ya que estamos agusto con nuestras settings nos vamos a la carpeta setup desde el anaconda prompt_
```
cd setup
```
_Una vez dentro de la carpeta corremos el siguiente comando:_
```
python prepare_data.py
```
_Una vez finalizado, nos salimos de la carpeta setup_
```
cd setup
```
## 5. Entrenamiento
_Ya que tenemos todo preparado corremos el siguiente comando para empezar el entrenamiento._
```
python train.py
```
###Contexto de lo que se imprime en el anaconda mientras se entrena
_Es bueno el ir supervisando el entrenamiento, cada 1000 steps nos mostrara un ejemplo de como se comporta nuestro chatbot, podemos ver si va progresando o si en entrenamiento no fue el mejor._
```
step: El número de pasos de entrenamiento completados.
lr: La tasa de aprendizaje (learning rate) utilizada en este paso.
step-time: El tiempo que toma completar un paso de entrenamiento.
wps: Palabras por segundo procesadas.
ppl (perplexity): Una medida de cuán bien el modelo predice una muestra. Valores más bajos son mejores.
gN (gradient norm): La norma del gradiente. Valores muy altos pueden indicar que el modelo está experimentando gradientes explosivos.
bleu: La puntuación BLEU, que mide la precisión de la traducción. Una puntuación de 0.00 significa que las traducciones generadas por el modelo no coinciden bien con las referencias.
```
###Tensorflow
_Mientras se esta entrenando podemos abrir otro anaconda prompt, activar nuestro enviroment, irnos a la carpeta del repositorio y correr el siguiente codigo para poder visualizar las estadisticas de nuestro entrenamiento._
```
tensorboard --logdir=train_log/
```
## 6. Interactuar con nuestro chatbot
_Una vez que terminamos podemos interactuar con nuestro chatbot, se tiene que correr el siguiente comando y nos dejara conversar con el._
```
python inference.py
```

## 7. Extras
_Ya cada quien puede ir probando y modificando cosas a su gusto._
Para poder correr un chatbot en especifico, si lo quisieramos mover de computadora o compartir, los archivos que necesitas son:
* El repositorio nmt
* De la carpeta model que se creo:
** [checkpoint](https://github.com/AlejandraRG57/IA_P3_Proyecto-Chatbot/blob/main/checkpoint) #Modificarlo para el step de los 3 archivos que decidimos usar mas adelante (Ej: 11000)
** [hparams](https://github.com/AlejandraRG57/IA_P3_Proyecto-Chatbot/blob/main/hparams)
** Los tres archivos que correspondan al step en el que iba tu chatbot que quieras usar.
***Ejemplo:
***1. [translate.ckpt-11000.data-00000-of-00001]()  #No subido porque pesaba mucho
***2. [translate.ckpt-11000.index](https://github.com/AlejandraRG57/IA_P3_Proyecto-Chatbot/blob/main/translate.ckpt-11000.index)
***3. [translate.ckpt-11000.meta](https://github.com/AlejandraRG57/IA_P3_Proyecto-Chatbot/blob/main/translate.ckpt-11000.meta)

##Agradecimientos
_Gracias por leer!_
Tambien muchas gracias a Sentdex y Daniel-kukiela por este gran tutorial!
