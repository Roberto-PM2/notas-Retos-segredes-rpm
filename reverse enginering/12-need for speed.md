# Need for speed


## Descripcion
The name of the game is [speed](https://www.youtube.com/watch?v=8piqd2BWeGI). Are you quick enough to solve this problem and keep it above 50 mph? [need-for-speed](https://jupiter.challenges.picoctf.org/static/f9abc386dfb1309e687344783f208b20/need-for-speed).
## Pistas
What is the final key?

## Solucion
descargamos el debuger gbd con sudo apt install gdb
posteriormente abrimos el programa con gdb
creamos un breackpoint en main
llamamos la funcion get_key con el comando
"call (int) get_key()"
y la de la bandera
call (int) print_flag()
```bash
┌──(kali㉿kali)-[~/reversing]
└─$ chmod +x need-for-speed
                                                                                                     
┌──(kali㉿kali)-[~/reversing]
└─$ gdb need-for-speed     
GNU gdb (Debian 13.1-2) 13.1
Copyright (C) 2023 Free Software Foundation, Inc.
License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.
Type "show copying" and "show warranty" for details.
This GDB was configured as "x86_64-linux-gnu".
Type "show configuration" for configuration details.
For bug reporting instructions, please see:
<https://www.gnu.org/software/gdb/bugs/>.
Find the GDB manual and other documentation resources online at:
    <http://www.gnu.org/software/gdb/documentation/>.

For help, type "help".
Type "apropos word" to search for commands related to "word"...
Reading symbols from need-for-speed...
(No debugging symbols found in need-for-speed)
(gdb) break main
Breakpoint 1 at 0x91e
(gdb) Quit
(gdb) disassemble main
Dump of assembler code for function main:
   0x000000000000091a <+0>:     push   %rbp
   0x000000000000091b <+1>:     mov    %rsp,%rbp
   0x000000000000091e <+4>:     sub    $0x10,%rsp
   0x0000000000000922 <+8>:     mov    %edi,-0x4(%rbp)
   0x0000000000000925 <+11>:    mov    %rsi,-0x10(%rbp)
   0x0000000000000929 <+15>:    mov    $0x0,%eax
   0x000000000000092e <+20>:    call   0x8d8 <header>
   0x0000000000000933 <+25>:    mov    $0x0,%eax
   0x0000000000000938 <+30>:    call   0x82f <set_timer>
   0x000000000000093d <+35>:    mov    $0x0,%eax
   0x0000000000000942 <+40>:    call   0x87d <get_key>
   0x0000000000000947 <+45>:    mov    $0x0,%eax
   0x000000000000094c <+50>:    call   0x8ac <print_flag>
   0x0000000000000951 <+55>:    mov    $0x0,%eax
   0x0000000000000956 <+60>:    leave
   0x0000000000000957 <+61>:    ret
--Type <RET> for more, q to quit, c to continue without paging--
End of assembler dump.
(gdb) break main
Note: breakpoint 1 also set at pc 0x91e.
Breakpoint 2 at 0x91e
(gdb) run
Starting program: /home/kali/reversing/need-for-speed 
[Thread debugging using libthread_db enabled]
Using host libthread_db library "/lib/x86_64-linux-gnu/libthread_db.so.1".

Breakpoint 1, 0x000055555540091e in main ()
(gdb) run
The program being debugged has been started already.
Start it from the beginning? (y or n) y
Starting program: /home/kali/reversing/need-for-speed 
[Thread debugging using libthread_db enabled]
Using host libthread_db library "/lib/x86_64-linux-gnu/libthread_db.so.1".

Breakpoint 1, 0x000055555540091e in main ()
(gdb) next
Single stepping until exit from function main,
which has no line number information.
Keep this thing over 50 mph!
============================

Creating key...
Not fast enough. BOOM!
[Inferior 1 (process 9768) exited normally]
(gdb) run
Starting program: /home/kali/reversing/need-for-speed 
[Thread debugging using libthread_db enabled]
Using host libthread_db library "/lib/x86_64-linux-gnu/libthread_db.so.1".

Breakpoint 1, 0x000055555540091e in main ()
(gdb) call (int) (get_key)
$1 = 1430259837
(gdb) call (int) (print_flag)
$2 = 1430259884
(gdb) call (int) get_key()
Creating key...
Finished
$3 = 9
(gdb) call (int) print_flag()
Printing flag:
PICOCTF{Good job keeping bus #190ca38b speeding along!}
$4 = 56
(gdb) 
```
## Bandera
PICOCTF{Good job keeping bus #190ca38b speeding along!}
## Notas adicionales


## Referencias
