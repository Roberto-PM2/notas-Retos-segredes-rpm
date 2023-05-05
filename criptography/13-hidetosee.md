# hidetosee


## Descripcion
How about some hide and seek heh?Look at this image [here](https://artifacts.picoctf.net/c/237/atbash.jpg).
## Pistas
Download the image and try to extract it.

## Solucion
instalamos la libreria steghide que sirve para analizar encriptaciones con imagenes
sudo apt install steghide
posteriormente extraemos con el comando
steghide extract -sf atbash.jpg
obtenemos un txt que al abrirlo nos da
krxlXGU{zgyzhs_xizxp_05y2z65z}
finalmente con cyberchef usando el cifrado atbash obtenemos la bandera
## Bandera
picoCTF{atbash_crack_05b2a65a}
## Notas adicionales


## Referencias
