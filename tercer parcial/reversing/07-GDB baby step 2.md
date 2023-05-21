# Reto


## Descripcion
Can you figure out what is in the `eax` register at the end of the `main` function? Put your answer in the picoCTF flag format: `picoCTF{n}` where `n` is the contents of the `eax` register in the decimal number base. If the answer was `0x11` your flag would be `picoCTF{17}`.Debug [this](https://artifacts.picoctf.net/c/520/debugger0_b).
## Pistas
You could calculate `eax` yourself, or you could set a breakpoint for after the calculcation and inspect `eax` to let the program do the heavy-lifting for you.

## Solucion
descargamos el archivo y lo desesamblamos con gdb la funcion main como indica las pistas
```bash
gdb-peda$ disass main
   0x0000000000401106 <+0>:     endbr64
   0x000000000040110a <+4>:     push   rbp
   0x000000000040110b <+5>:     mov    rbp,rsp
   0x000000000040110e <+8>:     mov    DWORD PTR [rbp-0x14],edi
   0x0000000000401111 <+11>:    mov    QWORD PTR [rbp-0x20],rsi
   0x0000000000401115 <+15>:    mov    DWORD PTR [rbp-0x4],0x1e0da
   0x000000000040111c <+22>:    mov    DWORD PTR [rbp-0xc],0x25f
   0x0000000000401123 <+29>:    mov    DWORD PTR [rbp-0x8],0x0
   0x000000000040112a <+36>:    jmp    0x401136 <main+48>
   0x000000000040112c <+38>:    mov    eax,DWORD PTR [rbp-0x8]
   0x000000000040112f <+41>:    add    DWORD PTR [rbp-0x4],eax
   0x0000000000401132 <+44>:    add    DWORD PTR [rbp-0x8],0x1
   0x0000000000401136 <+48>:    mov    eax,DWORD PTR [rbp-0x8]
   0x0000000000401139 <+51>:    cmp    eax,DWORD PTR [rbp-0xc]
   0x000000000040113c <+54>:    jl     0x40112c <main+38>
   0x000000000040113e <+56>:    mov    eax,DWORD PTR [rbp-0x4]
   0x0000000000401141 <+59>:    pop    rbp
   0x0000000000401142 <+60>:    ret
gdb-peda$ 

```
usando el comando 
gdb-peda$ xuntil 0x000000000040113e
para que el programa se detenga justo antes de el calculo final del valor de eax
ejecutamos next para que calcule esa linea y ejecutamos p $eax para consultar el contenido del registro eax obtenemos que
```bash
gdb-peda$ next
[----------------------------------registers-----------------------------------]
RAX: 0x4af4b 
RBX: 0x7fffffffdf58 --> 0x7fffffffe2a2 ("/home/kali/reversing/debugger0_b")
RCX: 0x7ffff7f9e820 --> 0x7ffff7fa02e0 --> 0x0 
RDX: 0x7fffffffdf68 --> 0x7fffffffe2c3 ("COLORFGBG=15;0")
RSI: 0x7fffffffdf58 --> 0x7fffffffe2a2 ("/home/kali/reversing/debugger0_b")
RDI: 0x1 
RBP: 0x7fffffffde40 --> 0x1 
RSP: 0x7fffffffde40 --> 0x1 
RIP: 0x401141 (<main+59>:       pop    rbp)
R8 : 0x4011c0 (<__libc_csu_fini>:       endbr64)
R9 : 0x7ffff7fcf6a0 (<_dl_fini>:        push   rbp)
R10: 0x7ffff7fcb878 --> 0xc00120000000e 
R11: 0x7ffff7fe18c0 (<_dl_audit_preinit>:       mov    eax,DWORD PTR [rip+0x1b552]        # 0x7ffff7ffce18 <_rtld_global_ro+888>)
R12: 0x0 
R13: 0x7fffffffdf68 --> 0x7fffffffe2c3 ("COLORFGBG=15;0")
R14: 0x0 
R15: 0x7ffff7ffd020 --> 0x7ffff7ffe2e0 --> 0x0
EFLAGS: 0x10246 (carry PARITY adjust ZERO sign trap INTERRUPT direction overflow)
[-------------------------------------code-------------------------------------]
   0x401139 <main+51>:  cmp    eax,DWORD PTR [rbp-0xc]
   0x40113c <main+54>:  jl     0x40112c <main+38>
   0x40113e <main+56>:  mov    eax,DWORD PTR [rbp-0x4]
=> 0x401141 <main+59>:  pop    rbp
   0x401142 <main+60>:  ret
   0x401143:    cs nop WORD PTR [rax+rax*1+0x0]
   0x40114d:    nop    DWORD PTR [rax]
   0x401150 <__libc_csu_init>:  endbr64
[------------------------------------stack-------------------------------------]
0000| 0x7fffffffde40 --> 0x1 
0008| 0x7fffffffde48 --> 0x7ffff7df318a (<__libc_start_call_main+122>:  mov    edi,eax)
0016| 0x7fffffffde50 --> 0x0 
0024| 0x7fffffffde58 --> 0x401106 (<main>:      endbr64)
0032| 0x7fffffffde60 --> 0x100000000 
0040| 0x7fffffffde68 --> 0x7fffffffdf58 --> 0x7fffffffe2a2 ("/home/kali/reversing/debugger0_b")
0048| 0x7fffffffde70 --> 0x7fffffffdf58 --> 0x7fffffffe2a2 ("/home/kali/reversing/debugger0_b")
0056| 0x7fffffffde78 --> 0x23f078c709299b51 
[------------------------------------------------------------------------------]
Legend: code, data, rodata, value
0x0000000000401141 in main ()




gdb-peda$ p $eax
$2 = 0x4af4b
gdb-peda$ 

```
$2 = 0x4af4b es el valor de eax usamos la herramienta  https://miniwebtool.com/es/hex-calculator/  para sacar el valor de la bandera
## Bandera
picoCTF{307019}
## Notas adicionales


## Referencias
