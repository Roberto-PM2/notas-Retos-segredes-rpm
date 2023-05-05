# basicmod1


## Descripcion
We found this weird message being passed around on the servers, we think we have a working decryption scheme.Download the message [here](https://artifacts.picoctf.net/c/129/message.txt).Take each number mod 37 and map it to the following character set: 0-25 is the alphabet (uppercase), 26-35 are the decimal digits, and 36 is an underscore.Wrap your decrypted message in the picoCTF flag format (i.e. `picoCTF{decrypted_message}`)
## Pistas
Do you know what `mod 37` means?
`mod 37` means modulo 37. It gives the remainder of a number after being divided by 37.

## Solucion
siguiendo las pistas proporcionadas podemos crear un script que puede resover el problema
```python
datos = open("message.txt").read().split()
print (datos)

texto = ""

for dato in datos:
    # Convertir dato a número entero
    num = int(dato)
    # Hacer el módulo con 37
    num = num % 37
    
    # Verificar si está entre 0 y 25
    if 0 <= num <= 25:
        # Sumar 65 y convertir a ASCII
        texto += chr(num + 65)
    # Verificar si está entre 26 y 35
    elif 26 <= num <= 35:
        # Sumar 22 y convertir a ASCII
        texto += chr(num + 22)
    # Reemplazar 36 con "_"
    elif num == 36:
        texto += "_"

print(texto)

```
## Bandera
picoCTF{R0UND_N_R0UND_ADD17EC2}
## Notas adicionales


## Referencias
