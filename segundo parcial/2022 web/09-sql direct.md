# Sql direct


## Descripcion
Connect to this PostgreSQL server and find the flag!`psql -h saturn.picoctf.net -p 51657 -U postgres pico`Password is `postgres`
## Pistas
What does a SQL database contain?

## Solucion
con ayuda del comando \? para ver todas las opciones disponibles obtenemos que 
"barra l"
"barra c"
y "barra dt" (obsidian oculta la barra inversa) son comandos que nos ayudan a ingresar a la bandera finalmente ejecutamos "select 'estrella' from flags;" y nos muestra la bandera

## Bandera
picoCTF{L3arN_S0m3_5qL_t0d4Y_73b0678f}
## Notas adicionales
En PostgreSQL, el comando "\l" se utiliza para listar todas las bases de datos disponibles en el servidor actual de PostgreSQL. Este comando es comúnmente utilizado por los administradores de bases de datos para ver una lista de bases de datos y sus propiedades, como sus nombres, propietarios y codificación.

El comando "\c" se utiliza para conectarse a una base de datos específica en PostgreSQL. Se sigue por el nombre de la base de datos a la que desea conectarse. Por ejemplo, "\c midatabase" lo conectará a la base de datos llamada "midatabase".

El comando "\dt" se utiliza para listar todas las tablas en la base de datos actual. Muestra una lista de todas las tablas junto con su esquema asociado y otras propiedades, como su propietario, tipo y tamaño.

## Referencias
