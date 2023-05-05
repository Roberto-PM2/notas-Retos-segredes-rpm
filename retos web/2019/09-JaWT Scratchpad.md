# JaWT Scratchpad


## Descripcion
Check the admin scratchpad! `https://jupiter.challenges.picoctf.org/problem/61864/` or http://jupiter.challenges.picoctf.org:61864
## Pistas
What is that cookie?
Have you heard of JWT?

## Solucion
se genera una cookie al ingresar un usuario cualquiera. copiapos la cookie generada posteriormente con ayuda de la herramienta john de kali pegamos el token para crakear la contrasena.
posteriormente con la herramienta jwt.io modificamos la cookie para que en la parte de enmedio diga "admin" y el la ultima "ilovepico" posteriormente pegamos la cookie en la pagina y salvamos la cookie al refrescar obtenemos la contrasena

```bash
(kali㉿kali)-[~]
└─$ john token -w=/usr/share/wordlists/rockyou.txt
Using default input encoding: UTF-8
Loaded 1 password hash (HMAC-SHA256 [password is key, SHA256 128/128 SSE2 4x])
Will run 2 OpenMP threads
Press 'q' or Ctrl-C to abort, almost any other key for status
ilovepico        (?)     
1g 0:00:00:06 DONE (2023-03-14 15:03) 0.1666g/s 1232Kp/s 1232Kc/s 1232KC/s iloverob4live345..ilovepatri
Use the "--show" option to display all of the cracked passwords reliably
Session completed. 
                                                                             
┌──(kali㉿kali)-[~]
└─$ john token -w=/usr/share/wordlists/rockyou.txt
Using default input encoding: UTF-8
Loaded 1 password hash (HMAC-SHA256 [password is key, SHA256 128/128 SSE2 4x])
No password hashes left to crack (see FAQ)
```
## Bandera
picoCTF{jawt_was_just_what_you_thought_1ca14548}
## Notas adicionales


## Referencias
