# Reto


## Descripcion
Our data got corrupted on the way here. Luckily, nothing got replaced, but every block of 3 got scrambled around! The first word seems to be three letters long, maybe you can use that to recover the rest of the message.Download the corrupted message [here](https://artifacts.picoctf.net/c/192/message.txt).
## Pistas
Split the message up into blocks of 3 and see how the first block is scrambled

## Solucion
obtenemos la siguiente cadena
heTfl g as iicpCTo{7F4NRP051N5_16_35P3X51N3_V091B0AE}2
 al segir la pista y separamos en tres caracteres nos damos cuenta que la regla de encriptado es que en cada bloque hay que poner el 3 caracter como el primero ejemplo
 het-the
 creamos el siguiente script python para obtener la bandera
```python
def separar_cadena(cadena):

    bloques = []

    for i in range(0, len(cadena), 3):

        bloque = cadena[i:i+3]

        bloque_modificado = bloque[-1] + bloque[:-1]

        bloques.append(bloque_modificado)

    nuevo_string = ''.join(bloques)

    return nuevo_string

  

cadena = "heTfl g as iicpCTo{7F4NRP051N5_16_35P3X51N3_V091B0AE}2"

resultado = separar_cadena(cadena)

print("bandera:", resultado)
```
## Bandera
picoCTF{7R4N5P051N6_15_3XP3N51V3_109AB02E}
## Notas adicionales


## Referencias
