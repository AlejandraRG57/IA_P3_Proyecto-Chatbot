# IA_P3_Proyecto-Chatbot
# Tutorial Usado: https://pythonprogramming.net/chatbot-deep-learning-python-tensorflow/?authuser=0#google_vignette

# 1. Preparación de la Información
# Use la informacion proporcionada de reddit para crear la database que uso mi chatbot.
# https://www.reddit.com/r/datasets/comments/3bxlg7/i_have_every_publicly_available_reddit_comment/?st=j9udbxta&sh=69e4fee7
# En especifico los siguientes meses en diversas pruebas: '2015-05' , '2007-12', 2012-12, '2010-11'.
# Primero se corre el codigo "chatbot_database" para preparar cada mes individualmente y hacerlo formato Data Base File.
# Después corremos el codigo "create_training_data" en el cual al inicio en "timeframes" escibimos todos los meses que querramos usar.

# 2. Creamos nuestro enviroment
# Yo ultilice el Anaconda Prompt para realizacion del proyecto
# Corremos el siguiente comando para crear el enviroment:
# conda create -n Chatbot python=3.6 
