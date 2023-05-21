# Reto


## Descripcion
Can you figure out what is in the `eax` register? Put your answer in the picoCTF flag format: `picoCTF{n}` where `n` is the contents of the `eax` register in the decimal number base. If the answer was `0x11` your flag would be `picoCTF{17}`.Download the assembly dump [here](https://artifacts.picoctf.net/c/511/disassembler-dump0_d.txt).
## Pistas
Don't tell anyone I told you this, but you can solve this problem without understanding the compare/jump relationship.
Of course, if you're really good, you'll only need one attempt to solve this problem.

## Solucion
tenemos lo siguiente
```assembly
<+0>:     endbr64 
<+4>:     push   rbp
<+5>:     mov    rbp,rsp
<+8>:     mov    DWORD PTR [rbp-0x14],edi
<+11>:    mov    QWORD PTR [rbp-0x20],rsi
<+15>:    mov    DWORD PTR [rbp-0x4],0x9fe1a
<+22>:    cmp    DWORD PTR [rbp-0x4],0x2710
<+29>:    jle    0x55555555514e <main+37>
<+31>:    sub    DWORD PTR [rbp-0x4],0x65
<+35>:    jmp    0x555555555152 <main+41>
<+37>:    add    DWORD PTR [rbp-0x4],0x65
<+41>:    mov    eax,DWORD PTR [rbp-0x4]
<+44>:    pop    rbp
<+45>:    ret
              
```
analizamos el codigo y notamos que se las acciones importantes son las siguientes:
el código realiza una resta entre el valor 0x9fe1a y 0x65, 

utilizamos la herramienta https://miniwebtool.com/es/hex-calculator/ para realizar operaciones con los valores hexadecimales
9fe1a-65=9fdb5
usando un traductor de hexadecimal obtenemos que el valor es 654773
## Bandera
picoCTF{654773}
## Notas adicionales


## Referencias
