# Reto


## Descripcion
Can you figure out what is in the `eax` register? Put your answer in the picoCTF flag format: `picoCTF{n}` where `n` is the contents of the `eax` register in the decimal number base. If the answer was `0x11` your flag would be `picoCTF{17}`.Download the assembly dump [here](https://artifacts.picoctf.net/c/530/disassembler-dump0_c.txt).
## Pistas
Not everything in this disassembly listing is optimal.

## Solucion
tenemos lo siguiente
```assembly
<+0>:     endbr64 
<+4>:     push   rbp
<+5>:     mov    rbp,rsp
<+8>:     mov    DWORD PTR [rbp-0x14],edi
<+11>:    mov    QWORD PTR [rbp-0x20],rsi
<+15>:    mov    DWORD PTR [rbp-0xc],0x9fe1a
<+22>:    mov    DWORD PTR [rbp-0x8],0x4
<+29>:    mov    eax,DWORD PTR [rbp-0xc]
<+32>:    imul   eax,DWORD PTR [rbp-0x8]
<+36>:    add    eax,0x1f5
<+41>:    mov    DWORD PTR [rbp-0x4],eax
<+44>:    mov    eax,DWORD PTR [rbp-0x4]
<+47>:    pop    rbp
<+48>:    ret

```
analizamos el codigo y notamos que se las acciones importantes son las siguientes:
el código realiza una multiplicación entre el valor 0x9fe1a y 0x4, 
le suma 0x1f5 al resultado y almacena el resultado final en el registro EAX. Por lo tanto, el contenido del registro EAX al final del código sería el resultado de esas operaciones aritméticas.
utilizamos la herramienta https://miniwebtool.com/es/hex-calculator/ para realizar operaciones con los valores hexadecimales
9fe1a*4=27f868
27f868+1f5=27fa5d
usando un traductor de hexadecimal obtenemos que el valor es 2619997
## Bandera
picoCTF{2619997}
## Notas adicionales


## Referencias
