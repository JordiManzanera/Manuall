# **MANUAL D' INSTALACIÓ OWNCLOUD (lxc/lxd)**

1. Primer tenim que crear un contenidor on instalar `OwnCloud`.

  `lxc launch ubuntu:20.04 [El nombre que le quieras poner a tu contenedor]`

2. Després de que hagis creat el teu contenidor, has d'encendre'l.

  `lxc start [El nombre que le hayas puesto al contenedor]`

3. Ara tenim que comprobar que el contenidor está funcionant correctament.

  `lxc list`

  ```+-----------------+---------+---------------------+------+-----------+-----------+
  |      NAME       |  STATE  |        IPV4         | IPV6 |   TYPE    | SNAPSHOTS |
  +-----------------+---------+---------------------+------+-----------+-----------+
  | contenedor      | STOPPED |                     |      | CONTAINER | 0         |
  +-----------------+---------+---------------------+------+-----------+-----------+
  | elmeucontenidor | RUNNING | 172.16.0.251 (eth0) |      | CONTAINER | 0         |
  +-----------------+---------+---------------------+------+-----------+-----------+
  ```
4. Després de comprobar que el contenidor funciona corectament, procedim a executar-ho.

  `lxc exec [el nom del teu contenidor] -- /bin/bash`

5. Una vegada dins del contenidor, tenim que instalar `apache2, mysql i algunes llibreries`.

  ```apt update
  apt upgrade
  apt install -y apache2
  apt install -y mysql-server
  apt install php libapache2-mod-php
  apt install php-fpm php-common php-mbstring php-xmlrpc php-soap php-gd php-xml php-intl php-mysql php-cli php-ldap php-zip php-curl
  ```

6. Després d'instalar tot de l'apartat anterior, tenim que reiniciar el servidor `apache2`.

  `systemctl restart apache2`

7. Una vegada reiniciat el servidor `apache2`, tindrem que configurar el `MySQL`:

   **7.1** Crear una `base de dades`.

    `CREATE DATABASE [El nom que vulguis per la base de dades];`

    **7.2** Crear un `usuari`.

    `CREATE USER '[el nom d'usuari que vulguis]'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';`

    **7.3** Donar privilegis a l'usuari

    `GRANT ALL ON bbdd.* to '[el teu nom d'usuari]'@'localhost';`

    **7.4** Sortim del `MySQL`.

    `exit`


8. Ara tenim que accedir al directori `/var/www/html`.   

  `cd /var/www/html`

9. Dins del directori, tenim que crear una `clau pública`.

  `cat ~/.ssh/elmeucontenidor.pub`

10. Una vegada generada la clau, la copiem en el contenidor.

  `vim /root/.ssh/authorized_keys`

11. Després tenim que copiar l'enllaç de descarrega de l'OwnCloud i posar-ho amb l'ordre `wget`.

  `wget https://download.owncloud.org/community/owncloud-complete-20210721.zip`

12. Instalem `unzip` si no el tenim a la màquina.

  `apt install unzip`

13. Descomprimim l'arxiu `.zip`.

  `unzip owncloud-complete-20210721.zip`

14. Ara tenim que donar-li permisos del directori `/var/www/html`.

  `chown -R www-data:www-data /var/www/html`

  `chmod -R 775 /var/www/html`

15. Per comprovar que ho hem fet correctament, posem la `IP del nostre conteidor` al nostre Buscador Web i ens tendria que redirigir a l'`OwnCloud`.

  `https:// [la IP del teu contenidor]`

16. Per últim, aturem el contenidor.

  `lxc stop [nom del teu contenidor]`

```  +-----------------+---------+------+------+-----------+-----------+
|      NAME       |  STATE  | IPV4 | IPV6 |   TYPE    | SNAPSHOTS |
+-----------------+---------+------+------+-----------+-----------+
| contenedor      | STOPPED |      |      | CONTAINER | 0         |
+-----------------+---------+------+------+-----------+-----------+
| elmeucontenidor | STOPPED |      |      | CONTAINER | 0         |
+-----------------+---------+------+------+-----------+-----------+
```
