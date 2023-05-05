# corrupt


## Descripcion
We found this [file](https://jupiter.challenges.picoctf.org/static/ab30fcb7d47364b4190a7d3d40edb551/mystery). Recover the flag.
## Pistas
Try fixing the file header

## Solucion
```bash
corregimos el encabezado (magic bytes) para que coincida con el formato png y el IHDR
┌──(kali㉿kali)-[~/forensic]
└─$ hexeditor mystery
 89 50 4E 47  0D 0A 1A 0A   00 00 00 0D  49 48 44 52                      .PNG........IHDR

└─$ pngcheck mystery
mystery  CRC error in chunk pHYs (computed 38d82c82, expected 495224f0)
ERROR: mystery

corregir el phys
┌──(kali㉿kali)-[~/forensic]
└─$ hexeditor mystery
00 09 70 48  59 73 00 00   16 25 00 00  16 25 01 49                      ..pHYs...%...%.I

corregir el idat y tamano del chunk
└─$ pngcheck mystery 
mystery  invalid chunk length (too large)
ERROR: mystery

52 24 F0 00  00 FF A5 49   44 41 54 78  5E EC BD 3F                      R$.....IDATx^..?
```
al corregir podremos abrir la imagen que nos da a bandera

## Bandera
picoCTF{c0rrupt10n_1847995}
## Notas adicionales
Los "magic bytes" (bytes mágicos, en español) son una secuencia de bytes en los archivos binarios que se utilizan para identificar el tipo de archivo. También se les conoce como "magic numbers" (números mágicos), "file signatures" (firmas de archivo) o "file headers" (encabezados de archivo).

## Referencias
https://en.wikipedia.org/wiki/PNG
https://en.wikipedia.org/wiki/List_of_file_signatures