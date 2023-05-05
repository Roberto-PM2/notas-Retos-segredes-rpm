# GET aHEAD


## Descripcion
Find the flag being held on this server to get ahead of the competition [http://mercury.picoctf.net:53554/](http://mercury.picoctf.net:53554/)

## Pistas
Maybe you have more than 2 choices
Check out tools like Burpsuite to modify your requests and look at the responses

## Solucion
al llegar a la pagina utilizmos las herramientas que ofrece firefoz para inspeccionar los elementos.
posterormente nod dirigimos a la pestana de network y presionamos uno de los dos botones disponibles en la pagina (rojo o azul) posteriormente seleccionamos el index.php que se nos genero en network y presionamos resend.
en la parte izquierda presionamos el metodo a usar y lo remplazamos por HEAD asi obtendremos la bandera como respuesta

o usando consola linux el comando
curl -I http://mercury.picoctf.net:53554/index.php
## Bandera
picoCTF{r3j3ct_th3_du4l1ty_2e5ba39f}

otra opcion es conectar un plugin de firefox llamado foxyproxy con la herramienta burp y editar la peticion desde ese software
## Notas adicionales


## Referencias
