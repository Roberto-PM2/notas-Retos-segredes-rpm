# MatchTheRegex


## Descripcion
How about trying to match a regular expressionThe website is running [here](http://saturn.picoctf.net:59168/).
## Pistas
Access the webpage and try to match the regular expression associated with the text field

## Solucion
inspeccionar codigo fuente de la pagina y analizar el fragmento de codigo que contiene regex

function send_request() { let val = document.getElementById("name").value; // ^p.....F!? fetch(`/flag?input=${val}`) .then(res => res.text()) .then(res => { const res_json = JSON.parse(res); alert(res_json.flag) return false; }) return false; }
## Bandera
picoCTF{succ3ssfully_matchtheregex_8ad436ed}
## Notas adicionales
El regex `^p.....F!?`  busca una cadena que comience con "p", seguida de cualquier otro carácter cinco veces, seguida de "F" seguida de "!"

## Referencias
