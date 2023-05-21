# Reto


## Descripcion
Can you figure out what is in the `eax` register at the end of the `main` function? Put your answer in the picoCTF flag format: `picoCTF{n}` where `n` is the contents of the `eax` register in the decimal number base. If the answer was `0x11` your flag would be `picoCTF{17}`.Disassemble [this](https://artifacts.picoctf.net/c/512/debugger0_a).
## Pistas
gdb is a very good debugger to use for this problem and many others!
`main` is actually a recognized symbol that can be used with gdb commands.

## Solucion
descargamos el archivo y lo desesamblamos con gdb la funcion main como indica las pistas
```bash
gdb-peda$ disass main
Dump of assembler code for function main:
   0x0000000000001129 <+0>:     endbr64
   0x000000000000112d <+4>:     push   rbp
   0x000000000000112e <+5>:     mov    rbp,rsp
   0x0000000000001131 <+8>:     mov    DWORD PTR [rbp-0x4],edi
   0x0000000000001134 <+11>:    mov    QWORD PTR [rbp-0x10],rsi
   0x0000000000001138 <+15>:    mov    eax,0x86342
   0x000000000000113d <+20>:    pop    rbp
   0x000000000000113e <+21>:    ret
End of assembler dump.
gdb-peda$ 

```
lo mas importante es que 0x86342 se mueve a eax usando el traductor https://miniwebtool.com/es/hex-calculator/  obtenemos la respuesta del hexadecimal es 549698
## Bandera
picoCTF{549698}
## Notas adicionales


## Referencias
