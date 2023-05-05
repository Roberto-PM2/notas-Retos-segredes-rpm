# MacroHard WeakEdge


## Descripcion
I've hidden a flag in this file. Can you find it? [Forensics is fun.pptm](https://mercury.picoctf.net/static/52da699e0f203321c7c90ab56ea912d8/Forensics%20is%20fun.pptm)

## Pistas


## Solucion
para este reto debemos descomprimir el archivo con el comando (unzip Forensics\ is\ fun.pptm
) posteriormente examinamos la carpeta creada con el comando tree y analizar si hay algo fuera de lo comun. cosa que encontramos en un archivo sospechoso llamado "hidden"
asi que nos dirigimos al directorio y desciframos su contenido con el comando
```bash
cat hidden| tr -d " " | base64 -d
```
## Bandera
picoCTF{D1d_u_kn0w_ppts_r_z1p5}
## Notas adicionales
-   `cat hidden`: el comando `cat` se utiliza para mostrar el contenido de un archivo, en este caso, el archivo llamado `hidden`.
-   `tr -d " "`: el comando `tr` se utiliza para traducir o eliminar caracteres en un flujo de texto. En este caso, la opción `-d` se utiliza para eliminar el espacio en blanco. Por lo tanto, este comando eliminará todos los espacios en blanco del texto que se pasa a través de él.
-   `base64 -d`: el comando `base64` se utiliza para codificar o decodificar archivos en formato base64. En este caso, la opción `-d` se utiliza para decodificar el texto codificado en base64 que se pasa a través de él.

## Referencias
