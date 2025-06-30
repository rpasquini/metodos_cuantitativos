# Instalación de librerías de R en Colab

Para trabajar con R en el ambiente Colab existen al menos dos opciones: 1) Trabajar en una maquina virtual que entiende R o 2) Trabajar en una maquina virtual que entiende Python. Trabajar en la maquina virtual de R es directo, pero requiere instalar (como parte del proceso) varias de las liberias, y algunas tardan mucho tiempo en ser descargadas (e.g. 15 minutos).  La solución que encontré hasta el momento es  usar el ambiente de python e instalar las librerías en Google Drive, de manera de poder llamar luego directamente a las librerías instaladas allí.  

Aquí va el procedimiento paso a paso:



## Instalación de librerías R (por única vez)

1. Trabajaremos sobre el Runtime de Python, ya que el Runtime de R de Google Colab todavía no permite vincular el Google Drive. Comenzamos por permitir el uso de las celdas mágicas de R en Python: 

``` python
%load_ext rpy2.ipython
```

2. Permitir a Colab el acceso a su Google Drive   

```python
from google.colab import drive

drive.mount('/content/drive/')
```

​	   Luego, en el icono de files 📂 en la barra izquierda encontrarán su drive como una carpeta adicional.

2. Crear una carpeta en su google drive que van a usar para guardar las librerias de R. 

   En mi caso la llamé "r-notebooks" 

3. Setear la nueva carpeta como ubicación default para las librerías de R 

```python
%%R
.libPaths("/content/drive/MyDrive/r-notebooks")
```

4. Instalar las librerias. Cuidado, la descarga de **sf** tarda como 15 minutos.

   ```
   %%R
   # Instalamos y cargamos las librerías necesarias
   if (!require("sf")) install.packages("sf")
   if (!require("dplyr")) install.packages("dplyr")
   if (!require("ggplot2")) install.packages("ggplot2")
   
   ```

   

## Carga de librerías R (una vez instaladas)
1. Permitir R en runtime de Python
1. Montar su drive
1. Setear el librarypath donde ya tienen instaladas las librerias 

```python
%%R
.libPaths("/content/drive/MyDrive/r-notebooks")
```
4. Importar las librerias

 ```
   %%R
   # Carga de liberías
    library(sf)
    library(dplyr)
    library(ggplot2)
   
 ```