# what lies whitin


## Descripcion
There's something in the [building](https://jupiter.challenges.picoctf.org/static/011955b303f293d60c8116e6a4c5c84f/buildings.png). Can you retrieve the flag?
## Pistas
There is data encoded somewhere... there might be an online decoder.

## Solucion
descargamos el archivo y posteriormente lo subimos a la pagina del decodificador de steneografia en referencias y nos muestra la bandera otra solucion es descargar el paquete en kali "zsteg" que esta programado en ruby con el comando "sudo gem install zsteg" y ejecutamos el siguiente comando
┌──(kali㉿kali)-[~/forensic]
└─$ zsteg -a buildings.png | grep pico
b1,rgb,lsb,xy       .. text: "picoCTF{h1d1ng_1n_th3_b1t5}"

## Bandera
picoCTF{h1d1ng_1n_th3_b1t5}
## Notas adicionales


## Referencias
- steganography [https://www.simplilearn.com/what-is-s...](https://www.youtube.com/redirect?event=video_description&redir_token=QUFFLUhqbUZEUTRzM3VwbVNJZ3Q4XzFyLU1XTTkwbkRNZ3xBQ3Jtc0trNXVlLUtVQjl5d3NIZlRmTm1OVWZoZW9MeDdVdWdFdHNid202UHpzRG8wNUxmMHdsTXRsNTlYN2VRQUVsRU12UGYtZlJIbGJhdC1TbnMtOV9XOHhxNWo4TThkYTVPd1dxMXROdEE0bmVOdzZjNU9IZw&q=https%3A%2F%2Fwww.simplilearn.com%2Fwhat-is-steganography-article&v=bFUB-USG3sw) 
- steganography online: [https://stylesuxx.github.io/steganogr...](https://www.youtube.com/redirect?event=video_description&redir_token=QUFFLUhqbG5LdkxrVUV4ZXpjaUpsUlJJQUpwdXZWWXVOd3xBQ3Jtc0tsTWJ2cGlXU3pmcDR2QmUwWVRjVGtPWkllbW9XNlBKbWlibXZCUzktR0dqcmJVb0tIRXd6SF92eVdkb3hyVUQ1eXJLbFpaNnVvMWNSQi03NDJCeWhoYUowTWREM0N2NGtJeEFIMnhweHpiaWpFSWlrQQ&q=https%3A%2F%2Fstylesuxx.github.io%2Fsteganography%2F&v=bFUB-USG3sw)