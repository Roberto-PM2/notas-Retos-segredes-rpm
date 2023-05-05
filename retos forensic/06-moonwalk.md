# moonwalk


## Descripcion
Decode this [message](https://jupiter.challenges.picoctf.org/static/fc1edf07742e98a480c6aff7d2546107/message.wav) from the moon.
## Pistas
How did pictures from the moon landing get sent back to Earth?
What is the CMU mascot?, that might help select a RX option

## Solucion
```bash
$ git clone https://github.com/colaclanth/sstv.git

$ python setup.py install
```
instalamos el decifrador de sstv y posteriormente ejecutamos el comando que lo decifra y convierte a imagen
```bash
$ sstv -d message.wav -o result.png
```

## Bandera
picoCTF{beep_boop_im_in_space}
## Notas adicionales


## Referencias
- steganography [https://www.simplilearn.com/what-is-s...](https://www.youtube.com/redirect?event=video_description&redir_token=QUFFLUhqbUZEUTRzM3VwbVNJZ3Q4XzFyLU1XTTkwbkRNZ3xBQ3Jtc0trNXVlLUtVQjl5d3NIZlRmTm1OVWZoZW9MeDdVdWdFdHNid202UHpzRG8wNUxmMHdsTXRsNTlYN2VRQUVsRU12UGYtZlJIbGJhdC1TbnMtOV9XOHhxNWo4TThkYTVPd1dxMXROdEE0bmVOdzZjNU9IZw&q=https%3A%2F%2Fwww.simplilearn.com%2Fwhat-is-steganography-article&v=bFUB-USG3sw) 
- steganography online: [https://stylesuxx.github.io/steganogr...](https://www.youtube.com/redirect?event=video_description&redir_token=QUFFLUhqbG5LdkxrVUV4ZXpjaUpsUlJJQUpwdXZWWXVOd3xBQ3Jtc0tsTWJ2cGlXU3pmcDR2QmUwWVRjVGtPWkllbW9XNlBKbWlibXZCUzktR0dqcmJVb0tIRXd6SF92eVdkb3hyVUQ1eXJLbFpaNnVvMWNSQi03NDJCeWhoYUowTWREM0N2NGtJeEFIMnhweHpiaWpFSWlrQQ&q=https%3A%2F%2Fstylesuxx.github.io%2Fsteganography%2F&v=bFUB-USG3sw)