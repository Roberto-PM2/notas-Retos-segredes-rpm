# Reto


## Descripcion
Smash the stackCan you overflow the buffer and modify the other local variable? The program is available [here](https://artifacts.picoctf.net/c/517/local-target). You can view source [here](https://artifacts.picoctf.net/c/517/local-target.c). And connect with it using:`nc saturn.picoctf.net 65013`
## Pistas
Do anything you can to change `num`.
When you change `num`, view the value as hexadecimal.

## Solucion
usamos prueba y error hasta encontrar el punto de quiebre (23 caracteres)
AAAAAAAAAAAAAAAAAAAAAAAAA
ponemos dos AA adicionales y obtenemos la bandera


## Bandera
picoCTF{l0c4l5_1n_5c0p3_fee8ef05}
## Notas adicionales


## Referencias
