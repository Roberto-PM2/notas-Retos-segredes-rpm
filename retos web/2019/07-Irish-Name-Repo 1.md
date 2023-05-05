# Irish-Name-Repo 1


## Descripcion
There is a website running at `https://jupiter.challenges.picoctf.org/problem/39720/` ([link](https://jupiter.challenges.picoctf.org/problem/39720/)) or http://jupiter.challenges.picoctf.org:39720. Do you think you can log us in? Try to see if you can login!

## Pistas
There doesn't seem to be many ways to interact with this. I wonder if the users are kept in a database?
Try to think about how the website verifies your login.
## Solucion
se realiza una inyeccion sql al login de la pagina poniendo como usuario o contrasena ' or 1=1;
## Bandera
Your flag is: picoCTF{s0m3_SQL_c218b685}
## Notas adicionales


## Referencias
https://www.w3schools.com/sql/sql_injection.asp