# **MANUAL D'INSTALACIÓ NEXTCLOUD (Vagrant)**

1. Primer de tot, tenim que crear  un directori nou per guardar cada projecte que fem amb `Vagrant`.

  `mkdir [nom que vulguis pel directori]`

  `cd [nom que te el directori que has creat]`

2. Tenim que crear el fitxer `Vagranfile` per escriure el projecte en aquest mateix.

  `vagrant init ubuntu/focal64`

  Una vegada ja executada la comanda, comprobem que ha funcionat am la comanda `ll`.

3. Ara amb `vagrant up` podrem iniciar-ho.

  `vagrant up --provider=virtualbox`

  L'ordre després de `vagrant up` serveix per crear una `MV` en `VirtualBox` i així poder fer `ssh`.

  `vagrant ssh`

4. Una vegada dins de la `MV`, ens tenim que fer `root` i instalar `apache2,llibreries,....`

```apt update
apt upgrade
apt install -y apache2
apt install -y mysql-server
apt install php libapache2-mod-php
apt install php-fpm php-common php-mbstring php-xmlrpc php-soap php-gd php-xml php-intl php-mysql php-cli php-ldap php-zip php-curl
```
5. Després tindrem que configurar `MySQL`:

  **5.1** Crear una `base de dades`.

   `CREATE DATABASE [El nom que vulguis per la base de dades];`

   **5.2** Crear un `usuari`.

   `CREATE USER '[el nom d'usuari que vulguis]'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';`

   **5.3** Donar `privilegis` a l'usuari

   `GRANT ALL ON bbdd.* to '[el teu nom d'usuari]'@'localhost';`

   **5.4** Sortim del `MySQL`.

   `exit`

6. Una vegada creada la base de dades, tenim accedir al directori `/var/www/html`.

  `cd /var/www/html`

7. Dins del directori, instalem el `.zip` del `NextCloud`.

    `wget https://download.nextcloud.com/server/releases/nextcloud-22.2.0.zip`

8. Descomprimim l'arxiu `.zip`.

  `unzip nextcloud-22.2.0.zip`

9. Una vegada descomprimit l'arxiu `.zip`, tindrem que eliminar els arxius següents:

        rm index.html    
        rm nextcloud-22.2.0.zip

10. Per finalitzar, li donem permissos al directori on es troba el NextCloud.

        chmod -R 775 .
        chown -R root:www-data .

11. Per poder entrar al NextCloud,tindrem que buscar `localhost:8080`.
