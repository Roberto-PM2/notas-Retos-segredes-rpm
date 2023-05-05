# tunn3l v1s10n


## Descripcion
We found this [file](https://mercury.picoctf.net/static/06a5e4ab22ba52cd66a038d51a6cc07b/tunn3l_v1s10n). Recover the flag.
## Pistas
Weird that it won't display right...

## Solucion
descargamos el archivo y vemos su encabezado con el comando xxd
nos damos cuenta al leer el encabezado que se supone que deveria ser un arcivo mbp asi que lo transformamos 
```bash
mv tunn3l_v1s10n tunn3l_v1s10n.bmp
```
con el hex editor modificamos el tamano del archivo para que sea 40 (codigo 28 en hexadecimal) bytes
en la pocicion offset 0E. tambien modificamos el byte que indica la pocicion en la que inicia la informacion que es el offset 0A
```bash
00000000  42 4D 8E 26  2C 00 00 00   00 00 28 00  00 00 28 00                      BM.&,.....(...(.
```
posteriormente modificamos el offset 16 del hexadecimal que representa la altura de la imagen en un archivo mbp en este caso los valores 40 03 (813 pixeles)
```bash
00 00 6E 04  00 00 43 03   00 00 01 00  18 00 00 00                      ..n...C.........
```
finalmente abrimos la imagen y sacamos la bandera
## Bandera
picoCTF{qu1t3_a_v13w_2020}
## Notas adicionales


## Referencias
https://en.wikipedia.org/wiki/BMP_file_format