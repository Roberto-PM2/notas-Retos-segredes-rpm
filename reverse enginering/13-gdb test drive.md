# Gdb test drive


## Descripcion
Can you get the flag?Download this [binary](https://artifacts.picoctf.net/c/86/gdbme).Here's the test drive instructions:

-   `$ chmod +x gdbme`
-   `$ gdb gdbme`
-   `(gdb) layout asm`
-   `(gdb) break *(main+99)`
-   `(gdb) run`
-   `(gdb) jump *(main+104)`
## Pistas
ejecutamos en orden los comandos proporcionados en la descripcion y obtenemos la bandera

## Solucion

## Bandera
picoCTF{d3bugg3r_dr1v3_72bd8355}
## Notas adicionales


## Referencias
