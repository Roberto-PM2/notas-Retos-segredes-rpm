# webnet0


## Descripcion
We found this [packet capture](https://jupiter.challenges.picoctf.org/static/0c84d3636dd088d9fe4efd5d0d869a06/capture.pcap) and [key](https://jupiter.challenges.picoctf.org/static/0c84d3636dd088d9fe4efd5d0d869a06/picopico.key). Recover the flag.
## Pistas
Try using a tool like Wireshark.
How can you decrypt the TLS stream?

## Solucion
descargamos los archivos y abrimos el archivo .pcap con wireshark
posteriormente intentamos "seguir" los paquetes tls sin exito debido a que estan encriptados por lo cual configuramos la llave llendonos a "edit -> preferences" y buscamos el apartado "TLS" agregamos la llave y intentamos buscar el paquete que contenga la palabra "picoCTF" llendonos a "edit -> find next"con las opciones "packet details, narrow and wide, strings"
## Bandera
Pico-Flag: picoCTF{nongshim.shrimp.crackers}
## Notas adicionales


## Referencias
https://en.wikipedia.org/wiki/Transport_Layer_Security