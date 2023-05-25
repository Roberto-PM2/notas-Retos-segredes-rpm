# Reto


## Descripcion
Can you figure out how this program works to get the flag?Connect to the program with netcat:`$ nc saturn.picoctf.net 57610`The program's source code can be downloaded [here](https://artifacts.picoctf.net/c/527/picker-IV.c). The binary can be downloaded [here](https://artifacts.picoctf.net/c/527/picker-IV).
## Pistas
With Python, there are no binaries. With compiled languages like C, there is source code, and there are binaries. Binaries are created from source code, they are a conversion from the human-readable source code, to the highly efficient machine language, in this case: x86_64.
How can you find the address that `win` is at?

## Solucion
descargamos los archivos examinamos el codigo fuente y encontramos
```c
int main() {
  signal(SIGSEGV, print_segf_message);
  setvbuf(stdout, NULL, _IONBF, 0); // _IONBF = Unbuffered

  unsigned int val;
  printf("Enter the address in hex to jump to, excluding '0x': ");
  scanf("%x", &val);
  printf("You input 0x%x\n", val);

  void (*foo)(void) = (void (*)())val;
  foo();
}

```
nos pide que ingresemos una direccion de memoria hex si seguimos las pistas nos dice que hay que encontrar la direccion de la funcion win
esto se puede realizar usando gdb y desensamblando dicha funcion y el primer resultado corresponde a la direccion
```bash
gdb-peda$ disass win
Dump of assembler code for function win:
   0x000000000040129e <+0>:     endbr64
   0x00000000004012a2 <+4>:     push   rbp
   0x00000000004012a3 <+5>:     mov    rbp,rsp

```
en este caso es el <0> eliminando los 0 innecesarios nos da que la direccion hex es 40129e
usamos el netcat proporcionado y introducimos dicha direccion hex dando la bandera
## Bandera
picoCTF{n3v3r_jump_t0_u53r_5uppl13d_4ddr35535_01672a61}

## Notas adicionales


## Referencias
