# forbidden paths


## Descripcion
Can you get the flag?Here's the [website](http://saturn.picoctf.net:55287/).We know that the website files live in `/usr/share/nginx/html/` and the flag is at `/flag.txt` but the website is filtering absolute file paths. Can you get past the filter to read the flag?
## Pistas


## Solucion
una manera de burlar al sistema que bloquea direcciones absolutas es usar direcciones relativas con ../../../../flag.txt
## Bandera
picoCTF{7h3_p47h_70_5ucc355_e5a6fcbc}
## Notas adicionales
Cuando se especifica una dirección en una ruta de archivo o en una URL, se puede hacer de dos formas diferentes: utilizando una dirección absoluta o una dirección relativa.

-   Una dirección absoluta es una ruta completa que comienza desde la raíz del sistema de archivos o del servidor web, y va hasta el archivo o recurso deseado. Por ejemplo, una dirección absoluta para un archivo en un sistema de archivos Unix podría ser "/usr/local/bin/miarchivo.txt", mientras que en un servidor web, una dirección absoluta para una página web podría ser "[http://www.ejemplo.com/mipagina.html](http://www.ejemplo.com/mipagina.html)".
    
-   Por otro lado, una dirección relativa es una ruta que se especifica en relación con la ubicación actual del archivo o recurso que se está utilizando. Por ejemplo, si se está trabajando en un directorio "proyecto" que contiene un subdirectorio "datos", y se desea acceder a un archivo llamado "datos.txt" que está ubicado en el directorio padre de "proyecto", se podría utilizar la dirección relativa "../../datos.txt".
    

La principal diferencia entre ambas formas de especificar la dirección es que una dirección absoluta siempre llevará al mismo archivo o recurso, independientemente de la ubicación actual del usuario o del archivo que la esté utilizando, mientras que una dirección relativa dependerá de la ubicación actual del usuario o archivo.

En resumen, si se sabe que la ubicación del archivo o recurso siempre será la misma, se puede utilizar una dirección absoluta, mientras que si se desea que la ruta sea relativa a la ubicación actual, se deberá utilizar una dirección relativa.

## Referencias
