# # Glory of the Garden


## Descripcion
This [garden](https://jupiter.challenges.picoctf.org/static/4153422e18d40363e7ffc7e15a108683/garden.jpg) contains more than it seems.
## Pistas
What is a hex editor?

## Solucion
roberto-pm-picoctf@webshell:~$ ls
garden.jpg
roberto-pm-picoctf@webshell:~$ hex
hex      hexdump  
roberto-pm-picoctf@webshell:~$ hexeditor garden.jpg 
-bash: hexeditor: command not found
roberto-pm-picoctf@webshell:~$ strings garden.jpg | grep pico
Here is a flag "picoCTF{more_than_m33ts_the_3y33dd2eEF5}"
roberto-pm-picoctf@webshell:~$ 
## Bandera
picoCTF{more_than_m33ts_the_3y33dd2eEF5}
## Notas adicionales


## Referencias
