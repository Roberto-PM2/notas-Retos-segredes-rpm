# Reto


## Descripcion

## Pistas


## Solucion
```bash
picoplayer@challenge:~$ crontab -l
no crontab for picoplayer
picoplayer@challenge:~$ ls
picoplayer@challenge:~$ ls /etc/cron.d
e2scrub_all
picoplayer@challenge:~$ cat e2scrub_all
cat: e2scrub_all: No such file or directory
picoplayer@challenge:~$ cd /etc/cron.d
picoplayer@challenge:/etc/cron.d$ ls
e2scrub_all
picoplayer@challenge:/etc/cron.d$ cat e2scrub_all
30 3 * * 0 root test -e /run/systemd/system || SERVICE_MODE=1 /usr/lib/x86_64-linux-gnu/e2fsprogs/e2scrub_all_cron
10 3 * * * root test -e /run/systemd/system || SERVICE_MODE=1 /sbin/e2scrub_all -A -r
picoplayer@challenge:/etc/cron.d$ cd /sbin/e2scrub_all
-bash: cd: /sbin/e2scrub_all: Not a directory
picoplayer@challenge:/etc/cron.d$ cd /sbin/
```

buscamos los "cron" que existen en el archivo al ingresar a la carpeta /etc/cron.d
al leer el cron con el cat nos damos cuenta que hay algo ejecutandose en la carpeta /sbin/ asi que ingresamos a ella
```bash
picoplayer@challenge:/sbin$ ls
cfdisk         e2scrub            grpck          mkfs.minix             rmt                update-mime
chcpu          e2scrub_all        grpconv        mkhomedir_helper       rmt-tar            
picoplayer@challenge:/sbin$ cat e2scrub_all
#!/bin/bash

#  Copyright (C) 2018 Oracle.  All Rights Reserved.
#
#  Author: Darrick J. Wong <darrick.wong@oracle.com>
#
#  This program is free software; you can redistribute it and/or
#  modify it under the terms of the GNU General Public License
#  as published by the Free Software Foundation; either version 2
#  of the License, or (at your option) any later version.
#
#  This program is distributed in the hope that it would be useful,
#  but WITHOUT ANY WARRANTY; without even the implied warranty of
#  MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
#  GNU General Public License for more details.
#
#  You should have received a copy of the GNU General Public License
#  along with this program; if not, write the Free Software Foundation,
#  Inc.,  51 Franklin St, Fifth Floor, Boston, MA  02110-1301, USA.

PATH=/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin

if (( $EUID != 0 )); then
    echo "e2scrub_all must be run as root"
    exit 1
fi

periodic_e2scrub=0
scrub_all=0
snap_size_mb=256
reap=0
conffile="/etc/e2scrub.conf"

test -f "${conffile}" && . "${conffile}"

scrub_args=""

print_help() {
        echo "Usage: $0 [OPTIONS]"
        echo " -n: Show what commands e2scrub_all would execute."
        echo " -r: Remove e2scrub snapshots."
        echo " -A: Scrub all ext[234] filesystems even if not mounted."
        echo " -V: Print version information and exit."
}

print_version() {
        echo "e2scrub_all 1.45.5 (07-Jan-2020)"
}

exitcode() {
        ret="$1"

        # If we're being run as a service, the return code must fit the LSB
        # init script action error guidelines, which is to say that we
        # compress all errors to 1 ("generic or unspecified error", LSB 5.0
        # section 22.2) and hope the admin will scan the log for what
        # actually happened.

        if [ -n "${SERVICE_MODE}" -a "${ret}" -ne 0 ]; then
                test "${ret}" -ne 0 && ret=1
        fi

        exit "${ret}"
}

while getopts "nrAV" opt; do
        case "${opt}" in
        "n") DBG="echo Would execute: " ;;
        "r") scrub_args="${scrub_args} -r"; reap=1;;
        "A") scrub_all=1;;
        "V") print_version; exitcode 0;;
        *) print_help; exitcode 2;;
        esac
done
shift "$((OPTIND - 1))"

# If we're in service mode and the service is not enabled via config file...
if [ -n "${SERVICE_MODE}" -a "${periodic_e2scrub}" -ne 1 ]; then
        # ...don't start e2scrub processes.
        if [ "${reap}" -eq 0 ]; then
                exitcode 0
        fi

        # ...and if we don't see any leftover e2scrub snapshots, don't
        # run the reaping process either, because lvs can be slow.
        if ! readlink -q -s -e /dev/mapper/*.e2scrub* > /dev/null; then
                exitcode 0
        fi
fi

# close file descriptor 3 (from cron) since it causes lvm to kvetch
exec 3<&-

# If some prerequisite packages are not installed, exit with a code
# indicating success to avoid spamming the sysadmin with fail messages
# when e2scrub_all is run out of cron or a systemd timer.

if ! type mapfile >& /dev/null ; then
    test -n "${SERVICE_MODE}" && exitcode 0
    echo "e2scrub_all: can't find mapfile --- is bash 4.xx installed?"
    exitcode 1
fi

if ! type lsblk >& /dev/null ; then
    test -n "${SERVICE_MODE}" && exitcode 0
    echo "e2scrub_all: can't find lsblk --- is util-linux installed?"
    exitcode 1
fi

if ! type lvcreate >& /dev/null ; then
    test -n "${SERVICE_MODE}" && exitcode 0
    echo "e2scrub_all: can't find lvcreate --- is lvm2 installed?"
    exitcode 1
fi

# Find scrub targets, make sure we only do this once.
ls_scan_targets() {
    local devices=$(lvs -o lv_path --noheadings -S "lv_active=active,lv_role=public,lv_role!=snapshot,vg_free>=${snap_size_mb}")

    if [ -z "$devices" ]; then
        return 0;
    fi
    lsblk -o NAME,MOUNTPOINT,FSTYPE,TYPE -P -n -p $devices | \
        grep FSTYPE=\"ext\[234\]\" | grep TYPE=\"lvm\" | \
        while read vars ; do
                eval "${vars}"

                if [ "${scrub_all}" -eq 1 ] || [ -n "${MOUNTPOINT}" ]; then
                    echo ${MOUNTPOINT:-${NAME}}
                fi
        done
}

# Find leftover scrub snapshots
ls_reap_targets() {
    lvs -o lv_path -S lv_role=snapshot -S lv_name=~\(e2scrub$\) \
        --noheadings | sed -e 's/.e2scrub$//'
}

# Figure out what we're targeting
ls_targets() {
        if [ "${reap}" -eq 1 ]; then
                ls_reap_targets
        else
                ls_scan_targets
        fi
}

# systemd doesn't know to do path escaping on the instance variable we pass
# to the e2scrub service, which breaks things if there is a dash in the path
# name.  Therefore, do the path escaping ourselves if needed.
#
# systemd path escaping also drops the initial slash so we add that back in so
# that log messages from the service units preserve the full path and users can
# look up log messages using full paths.  However, for "/" the escaping rules
# do /not/ drop the initial slash, so we have to special-case that here.
escape_path_for_systemd() {
        local path="$1"

        if [ "${path}" != "/" ]; then
                echo "-$(systemd-escape --path "${path}")"
        else
                echo "-"
        fi
}

# Scrub any mounted fs on lvm by creating a snapshot and fscking that.
mapfile -t targets < <(ls_targets)
for tgt in "${targets[@]}"; do
        # If we're not reaping and systemd is present, try invoking the
        # systemd service.
        if [ "${reap}" -ne 1 ] && type systemctl > /dev/null 2>&1; then
                tgt_esc="$(escape_path_for_systemd "${tgt}")"
                ${DBG} systemctl start "e2scrub@${tgt_esc}" 2> /dev/null
                res=$?
                if [ "${res}" -eq 0 ] || [ "${res}" -eq 1 ]; then
                        continue;
                fi
        fi

        # Otherwise use direct invocation
        ${DBG} "/sbin/e2scrub" ${scrub_args} "${tgt}"
done
```
ingresamos a la carpeta y hacemos cat al archivo ejecutandose ahi encontramos una pista que indica que en la direccion "/" hay algo asi que
```bash
picoplayer@challenge:/sbin$ cd /
picoplayer@challenge:/$ ls
bin   challenge  etc   lib    lib64   media  opt   root  sbin  sys  usr
boot  dev        home  lib32  libx32  mnt    proc  run   srv   tmp  var
picoplayer@challenge:/$  cd challenge/
picoplayer@challenge:/challenge$ ls
metadata.json
picoplayer@challenge:/challenge$ cat metadata.json
{"flag": "picoCTF{Sch3DUL7NG_T45K3_L1NUX_9d5cb744}", "username": "picoplayer", "password": "ekj2GJuiv4"}picoplayer@challenge:/challenge$ Connection to saturn.picoctf.net closed by remote host.
Connection to saturn.picoctf.net closed.
```
al ingresar vamos hacia la carpeta challenge ya que suena a ser la mas probable de tener algo que ver con el reto de encontrar la bandera supocicion que afortunadamente fue correcta
## Bandera
picoCTF{Sch3DUL7NG_T45K3_L1NUX_9d5cb744}
## Notas adicionales


## Referencias
