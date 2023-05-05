# Pixelated


## Descripcion
I have these 2 images, can you make a flag out of them? [scrambled1.png](https://mercury.picoctf.net/static/c9593d1d2ac9d850da95bffe0ac3b6c6/scrambled1.png) [scrambled2.png](https://mercury.picoctf.net/static/c9593d1d2ac9d850da95bffe0ac3b6c6/scrambled2.png)
## Pistas
[https://en.wikipedia.org/wiki/Visual_cryptography](https://en.wikipedia.org/wiki/Visual_cryptography)
Think of different ways you can "stack" images

## Solucion
descargamos la herramienta stegsolve que sirve para realizar steneografia sobre 2 imagenes con varias opciones con los siguientes comandos
```shell
sudo wget http://www.caesum.com/handbook/Stegsolve.jar -O stegsolve.jar
chmod +x stegsolve.jar
java -jar /opt/stegsolve.jar
```
con las opciones de combinar imagenes obtenemos la bandera con la opcion "add"
## Bandera
picoCTF{da8fcef8}
## Notas adicionales


## Referencias
