# yolov4_custom_detect_object
Este repositório é fruto de um trabalho da disciplina de Sistemas e Multimídias, da UNEB (Universidade do Estado da Bahia)

Além do trabalho, nosso objetivo é criar um conteúdo em português de aluno para aluno.
Fizemos o trabalho no Google Colab, uma dica, se puder, tente usar o plano de 1 mês, a diferença de GPU é incrível.

NOTA: Irei compartilhar todos os arquivos nesse diretorio. Incluindo os comando no google colab.

##########################################################################################################################

/* Criando uma conexão com o google drive*/

from google.colab import drive
drive.mount('/content/gdrive')
-----------------------------

/*essa funcao serve para criar um link e encurtar o nome para dentro do drive se dirigindo para essa pasta como TreinamentoCustomizadoYOLO*/

!ln -s /content/gdrive/My\ Drive/TreinamentoCustomizadoYOLO/ /TreinamentoCustomizadoYOLO

-----------------------------
/*demonstrando o comando de forma longa*/
!ls /content/gdrive/My\ Drive/TreinamentoCustomizadoYOLO/
----------------------------

/*demonstrando o mesmo comando, mas usando a forma mais curta*/
ls /TreinamentoCustomizadoYOLO/
----------------------------

/*Clonando o Darknet */
!git clone https://github.com/AlexeyAB/darknet
-----------------------------

!cd darknet
----------------------------

!cd data

NOTA:
/*FAÇA UPLOAD PARA A PASTA DATA dentro de DARKNET */
obj.names
obj.data
train.txt
test.txt
---------------------------
/*depois de criar a pasta, faça upload das fts com seus .txt para dentro de valid*/
!mkdir valid
--------------------------
/*depois de criar a pasta, faça upload das fts com seus .txt para dentro de obj*/
!mkdir obj
-----------------------------

/*Voltando para pasta Darknet e fazendo configuração no arquivo Makefile, aqui estou dizendo que irei usar o OPENCV, GPU e CDNN*/
NOTA: Tenha certeza que está dentro da pasta darknet. O comando !pwd verifica qual pasta você se encontra. 
cd ..
----------------------------
!sed -i 's/OPENCV=0/OPENCV=1/' Makefile
!sed -i 's/GPU=0/GPU=1/' Makefile
!sed -i 's/CUDNN=0/CUDNN=1/' Makefile

----------------------
#FAÇA UPLOAD PARA A PASTA .cfg 
yolov4_custom.cfg 

-----------------------
/* DENTRO DA PASTA DARKNET */
!make

--------------------
/*DENTRO DA PASTA DARKNET */

!wget https://github.com/AlexeyAB/darknet/releases/download/darknet_yolo_v3_optimal/yolov4.conv.137
-----------------------------
/*DENTRO DA PASTA DARKNET */

!./darknet detector train data/obj.data cfg/yolov4_custom.cfg yolov4.conv.137 -dont_show -map
----------------------------

NOTA: A ideia é que a cada 100 epocas quando for salvar, salve dentro do driver para não desconectar e perder todo o trabalho

!./darknet detector train data/obj.data cfg/yolov4_custom.cfg /TreinamentoCustomizadoYOLO/yolov4_custom_last.weights -dont_show -map


##########################################################################################################################
