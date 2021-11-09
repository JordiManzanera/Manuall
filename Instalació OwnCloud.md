# **MANUAL D' INSTALACIÓ OWNCLOUD**

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

    `CREATE USER 'usuario'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';`

    **7.3** Donar privilegis a l'usuari

    `GRANT ALL ON bbdd.* to 'usuario'@'localhost';`

    **7.4** Sortim del `MySQL`.

    `exit`

    **7.5** Comprobem que el MySQL 


8.  
