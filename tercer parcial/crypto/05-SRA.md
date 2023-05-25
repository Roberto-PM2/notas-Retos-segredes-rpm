# Reto


## Descripcion
I just recently learnt about the SRA public key cryptosystem... or wait, was it supposed to be RSA? Hmmm, I should probably check...Connect to the program on our server: `nc saturn.picoctf.net 53876`Download the program: [chal.py](https://artifacts.picoctf.net/c/299/chal.py)
## Pistas


## Solucion
sustituyimos los nombres de variables para que coincidan con el formato tradicional
```python
from Crypto.Util.number import getPrime, inverse, bytes_to_long
from string import ascii_letters, digits
from random import choice
import time

time.clock = time.time

plain = "".join(choice(ascii_letters + digits) for _ in range(16))  # pride
p = getPrime(128)  # gluttony
q = getPrime(128)  # greed

n = p * q  # lust
e = 65537  # sloth
phi = (p - 1) * (q - 1)
d = inverse(e, phi)  # envy
cipher = pow(bytes_to_long(plain.encode()), e, n)  # anger

```
importamos la libreria prime fac con
```bash
pip install git+https://github.com/elliptic-shiho/primefac-fork.git@master

```
y creamos el siguiente script para decifrar el cifrado
```python
from pwn import *
import primefac
from itertools import combinations
from Crypto.Util.number import long_to_bytes

from sympy import isprime

def check_prime_product(product):
    if product.bit_length() == 128 and isprime(product + 1):
        return True
    else:
        return False


# función para generar todas las sublistas
def sub_lists(l):
    # lista vacía inicial
    comb = []

    # iterando hasta la longitud de la lista
    for i in range(1, len(l) + 1):
        # generando sublista
        comb += [list(j) for j in combinations(l, i)]
    # devolviendo la lista
    return comb

def divisors(phi):
    print("Dame los divisores de ", phi-1)
    
    return(eval(input()))

# conectar al servidor
# modificar según sea necesario
r = remote('saturn.picoctf.net', 62752)
# obtener el texto cifrado
r.recvuntil("anger =")
ciphertext = int(r.recvline())
# obtener d
r.recvuntil("envy =")
d = int(r.recvline())
print("cifrado =", ciphertext)
print("d =", d)
print(r.recvuntil("vainglory?"))
r.recvline()
# como d es e^-1 mod (p-1)*(q-1), d*e=k*(p-1)*(q-1)+1
# por lo tanto, (p-1)*(q-1)*k = d*e-1
factors = divisors(d * 65537)
combos = sub_lists(factors)
primes = set()
# probar todos los subconjuntos posibles de la lista de factores como factores de (p-1)
for l in combos:
    product = 1
    # multiplicarlos juntos para obtener p-1
    for k in l:
        product = product * k
    # si la longitud es correcta y agregar 1 produce un primo, entonces tal vez
    if check_prime_product(product):
        primes.add(product + 1)
print(primes)
primelist = list(primes)
# probar todas las posibles parejas de primos
for p in primelist:
    for q in primelist:
        n = p * q
        # decodificar con este posible n
        plain = pow(ciphertext, d, n)
        try:
            plaintext = long_to_bytes(plain)
            # verificar si corresponde al texto y, si es así, probarlo
            print(plaintext.decode())
            r.sendline(plaintext.decode())
            print(r.recvline())
            print(r.recvline())
            print(r.recvline())
        except:
            continue

```

en una parte de la ejecucion nos pedira los divisores de "d x 65537" 
copiamos el numero impreso en pantalla y utilizamos la herramienta online
https://www.dcode.fr/prime-factors-decomposition para obtener los divisores
es una lista separada por comas y la introducimos al programa y a partir de ellos se encargara de encontrar la llave final
## Bandera
picoCTF{7h053_51n5_4r3_n0_m0r3_3858bd66}
## Notas adicionales


## Referencias
