# shark on wire 2


## Descripcion
We found this [packet capture](https://jupiter.challenges.picoctf.org/static/b506393b6f9d53b94011df000c534759/capture.pcap). Recover the flag that was pilfered from the network.
## Pistas


## Solucion
utilizamos la herramienta wireshark para analizar los paquetes "siguiendo" los paquetes en formato udp nos damos cuenta que existen dos textos en las pistas "start" y "end" nos damos cuenta que ambs tienen en comun estar en el puerto 22 como destino
asi que filtramos con ese. tras analizar de nuevo nos damos cuenta que si eliminamos el 5000 del puerto de origen nos da la bandera en codigo acii una manera de obenerla es manualmente traducir cada codigo y juntarlo todo en un solo texto o con el siguiente script python

```bash
┌──(kali㉿kali)-[~/forensic/shark]
└─$ cat script.py     
from scapy.all import *

packets = rdpcap('capture.pcap')

flag = ''

for p in packets:
        if UDP in p and p[UDP].dport == 22:
                if p[UDP].sport > 5000:
                        flag += chr(p[UDP].sport - 5000)

print (flag)
                                                                                                   
┌──(kali㉿kali)-[~/forensic/shark]
└─$ python script.py            
picoCTF{p1LLf3r3d_data_v1a_st3g0}

```

## Bandera
picoCTF{p1LLf3r3d_data_v1a_st3g0}
## Notas adicionales


## Referencias
