# LEVEL 21-22

## Objetivo
A program is running automatically at regular intervals from **cron**, the time-based job scheduler. Look in **/etc/cron.d/** for the configuration and see what command is being executed.

## Datos acceso
ssh bandit21 @bandit.labs.overthewire.org -p 2220
NvEJF7oVjkddltPSrdKEFOllh9V1IBcq
## Solucion
```bash
bandit21@bandit:~$ ls /etc/cron.d
cronjob_bandit15_root  cronjob_bandit22  cronjob_bandit24       e2scrub_all  sysstat
cronjob_bandit17_root  cronjob_bandit23  cronjob_bandit25_root  otw-tmp-dir
bandit21@bandit:~$ ls /etc/cron.d/cronjob_bandit22
/etc/cron.d/cronjob_bandit22
bandit21@bandit:~$ cat /etc/cron.d/cronjob_bandit22
@reboot bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
* * * * * bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
bandit21@bandit:~$ cat /usr/bin/cronjob_bandit22.sh
#!/bin/bash
chmod 644 /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
cat /etc/bandit_pass/bandit22 > /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
bandit21@bandit:~$ cat /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
WdDozAdTM2z9DiFEQ2mGlwngMfj4EZff
bandit21@bandit:~$
```

## Notas adicionales
El comando "ls /etc/cron.d" se utiliza para listar el contenido del directorio "/etc/cron.d" en Linux.

En Linux, el directorio "/etc/cron.d" es utilizado por el servicio "cron", que es un programa que permite programar tareas para que se ejecuten automáticamente en un momento específico o con una frecuencia determinada. En este directorio se almacenan los archivos de configuración de las tareas programadas en "cron".
## Referencias
https://www.redeszone.net/tutoriales/servidores/cron-crontab-linux-programar-tareas/
