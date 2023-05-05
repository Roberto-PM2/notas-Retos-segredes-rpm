# Local Authority


## Descripcion
Can you get the flag?Go to this [website](http://saturn.picoctf.net:51108/) and see what you can discover.
## Pistas
How is the password checked on this website?

## Solucion
acedemos cualquier nombre de usuario y contrasena 
usando las herramientas de desarrollador de nuestro navegador podemos observar los archivos que componen la pagina en la que se encuentra "secure.js" al abrirlo encontramos esta linea
if( username === 'admin' && password === 'strongPassword098765' )

asi que simplemente ingresamos estos datos y obtenemos la bandera
## Bandera
picoCTF{j5_15_7r4n5p4r3n7_05df90c8}
## Notas adicionales


## Referencias
