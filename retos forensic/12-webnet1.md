# webnet1


## Descripcion
We found this [packet capture](https://jupiter.challenges.picoctf.org/static/fbf98e695555a2a48fe42c9a245de376/capture.pcap) and [key](https://jupiter.challenges.picoctf.org/static/fbf98e695555a2a48fe42c9a245de376/picopico.key). Recover the flag.
## Pistas
Try using a tool like Wireshark.
How can you decrypt the TLS stream?

## Solucion
de manera similar al webnet 0 seguimos todos los pasos hasta el punto de configurar la llave TSL
en este punto nos daremeos cuenta que entre los paquetes desencriptados (destacados por aparecer ahora en verde) existe un http que contiene una imagen
para descargarla nos vamos en wireshark a "file -> export objets -> http" y elegimos la imagen "vulture.jpg" y la guardamos en la ubicacion de nuestra eleccion para finalizar el reto ejecutamos el siguiente comando
```bash
┌──(kali㉿kali)-[~/forensic/web1]
└─$ strings vulture.jpg | grep pico
picoCTF{honey.roasted.peanuts}
                                   
```
## Bandera
picoCTF{honey.roasted.peanuts}
## Notas adicionales


## Referencias
