# Safe Opener 2
## Descripcipción
What can you do with this file?I forgot the key to my safe but this [file](https://artifacts.picoctf.net/c/290/SafeOpener.class) is supposed to help me with retrieving the lost key. Can you help me unlock my safe?
## Pistas
- Download and try to decompile the file..
## Solucion
```
SOLUCIÓN 1
Usando una pagina web que nos permite decodificar lo que se encuentra dentro de la imagen

SOLUCIÓN 2
┌──(kali㉿kali)-[~/Documents/forense/safe]
└─$ strings SafeOpener.class | grep "picoCTF"
,picoCTF{SAf3_0p3n3rr_y0u_solv3d_it_7db9fb8c}
┌──(kali㉿kali)-[~/Documents/forense/safe]
└─$
```
## Bandera
picoCTF{SAf3_0p3n3rr_y0u_solv3d_it_7db9fb8c}
## Notas adicionales
## Referencias
