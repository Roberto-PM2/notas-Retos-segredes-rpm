# Mind your Ps and Qs


## Descripcion
In RSA, a small `e` value can be problematic, but what about `N`? Can you decrypt this? [values](https://mercury.picoctf.net/static/3cfeb09681369c26e3f19d886bc1e5d9/values)
## Pistas
Bits are expensive, I used only a little bit over 100 to save money

## Solucion
al usar las formulas podemos obtener la bandera pero nos faltan valores
primero factorizamos n para obtener los valores de p y q con la herramienta http://www.factordb.com
una vez obtenidos ejecutamos el siguiente script de python que a partir de las formulas desencripta el mensaje
```python
#!/usr/bin/env python
from Crypto.Util.number import inverse
from Crypto.Util.number import long_to_bytes
from gmpy2 import *

c=8533139361076999596208540806559574687666062896040360148742851107661304651861689
n=769457290801263793712740792519696786147248001937382943813345728685422050738403253
e=65537   
p=1617549722683965197900599011412144490161
q=475693130177488446807040098678772442581573

tn= (p-1)*(q-1)
d=inverse(e,tn)
m=pow(c,d,n)
print(long_to_bytes(m))

```

## Bandera
picoCTF{sma11_N_n0_g0od_45369387}
## Notas adicionales


## Referencias
