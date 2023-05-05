# Enhance


## Descripcion
Download this image file and find the flag.

-   [Download image file](https://artifacts.picoctf.net/c/100/drawing.flag.svg)
## Pistas


## Solucion
usando el comando strings drawing.flag.svg para ver si hay algo que se asemeje a una bandera observamos que las lineas
```shell
id="tspan3764">F { 3 n h 4 n </tspan><tspan
         sodipodi:role="line"
         x="107.43014"
         y="132.11588"
         style="font-size:0.00352781px;line-height:1.25;fill:#ffffff;stroke-width:0.26458332;"
         id="tspan3752">c 3 d _ a a b 7 2 9 d d }</tspan></text>

```
tienen formato sospechoso asi que las juntamos y eliminamos espacios
## Bandera
picoCTF{3nh4nc3d_aab729dd}
## Notas adicionales


## Referencias
