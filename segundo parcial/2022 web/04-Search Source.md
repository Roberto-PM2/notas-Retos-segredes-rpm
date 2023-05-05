# Search Source


## Descripcion
The developer of this website mistakenly left an important artifact in the website source, can you find it?The website is [here](http://saturn.picoctf.net:50303/)
## Pistas
How could you mirror the website on your local machine so you could use more powerful tools for searching?

## Solucion
descargamos el sitio web con el comando wget -r  http://saturn.picoctf.net:50303/
posteriormente nos ubicamos en la carpeta creada y ejecutamos "grep -r "pico" que busca de manera recursiva en todos los archivos hasta encontrar la palabra pico
y obtenemos que
css/style.css:/** banner_main picoCTF{1nsp3ti0n_0f_w3bpag3s_587d12b8} **/

## Bandera
picoCTF{1nsp3ti0n_0f_w3bpag3s_587d12b8}
## Notas adicionales
  
La opción `-r` de `grep` permite realizar una búsqueda de manera recursiva en un directorio y sus subdirectorios, mientras que sin ella la búsqueda se realiza solamente en los archivos del directorio especificado.

Si no se usa la opción `-r`, `grep` solo buscará la palabra en los archivos del directorio especificado y no en sus subdirectorios. Por lo tanto, si la palabra que se está buscando se encuentra en algún archivo en un subdirectorio, el comando no la encontrará.

En cambio, si se usa la opción `-r`, `grep` buscará de forma recursiva en el directorio especificado y sus subdirectorios, lo que significa que revisará todos los archivos en todos los niveles del árbol de directorios en busca de la palabra especificada.

## Referencias
