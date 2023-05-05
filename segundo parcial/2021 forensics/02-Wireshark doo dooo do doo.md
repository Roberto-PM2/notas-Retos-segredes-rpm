# Wireshark doo dooo do doo


## Descripcion
Can you find the flag? [shark1.pcapng](https://mercury.picoctf.net/static/b44842413a0834f4a3619e5f5e629d05/shark1.pcapng).
## Pistas


## Solucion
usamos wireshark para abrir el archivo posteriormente "seguimos la corriente tcp"
al seguirla encontraremos este string cvpbPGS{c33xno00_1_f33_h_qrnqorrs} que parece sospechoso usamos cyberchef para ver si es algo encryptado y efectivamente era la bandera cifrada en este caso con rot 13
## Bandera
picoCTF{p33kab00_1_s33_u_deadbeef}
## Notas adicionales


## Referencias
