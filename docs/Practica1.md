# ASIR2-IAW-Practica01
## Practica 01 - IAW Pila L.A.M.P.

*L.A.M.P.* Es el acrónimo utilizado para describir un sistema de infraestructura de Internet que usa las siguientes herramientas:
  - Linux
  - Apache
  - MySQL/MariaDB
  - PHP

![portada](/resti-iaw.github.io/site/assets/images/portada.jpg)
## Linux 

Los siguientes comandos básicos son los utilizados en la práctica , es recomendable e incluso obligatorio utilzar sudo:

- #### apt update
Actualiza la lista de paquetes

```sudo apt update ```

- #### apt upgrade
Actualiza los paquetes instalados a sus ultimas versiones disponibles

```sudo apt upgrade ```

- #### apt install 
Instala un paquete determinado

```sudo apt install ```

- #### apt remove
Desinstala un paquete

 ```sudo apt remove ```

#### (OPCIONAL) Instalación de interfaz gráfica

Unity -> ``` sudo apt install ubuntu-desktop ```

GNOME -> ``` sudo apt install ubuntu-gnome-desktop ```

KDE -> ``` sudo apt install kubuntu-desktop ```


- ### Instalación del servidor SSH

``` sudo apt install ssh ```

#### Como iniciar , parar y consultar el servicio SSH

``` sudo systemctl start/stop/status ssh ```

## Apache

- #### Instalación Apache

``` sudo apt install apache2```

#### Como iniciar , parar, reiniciar , recargar y consultar el servicio Apache

```sudo systemctl start/stop/restart/reload/status apache2```

#### Archivos de configuración de Apache

```
/* Archivos */
├── apache2.conf
├── envvars
├── magic
└── ports.conf

/* Directorios */
├── conf-available
├── conf-enabled
├── mods-available
├── mods-enabled
├── sites-available
└── sites-enabled
```

### Archivos de log de Apache

#### access.log
El servidor almacena en el registro de accceso información sobre todas las peticiones que procesa

#### error.log
El registro de errores del servidor

#### Mensajes de error más detallados
Necesitamos cambiar o añadir la linea LogLevel en el archivo de /etc/apache2/apache2.conf , los argumentos posibles son:

emerg: Emergencias, no se puede utilizar el servidor.
alert: Require acción inmediata.
crit: Condiciones críticas.
error: Condiciones de error.
warn: Condiciones de advertencia. (Por defecto)
notice: Condicón normal pero significativa.
info: Informativa.
debug: Mensajes de corrección de errores.

## MySQL Server

- ### Instalación de MySQL Server

```
sudo apt install mysql-server
```

#### Como iniciar, parar y consultar el estado de MySQL

```
sudo systemctl start/stop/restart/status mysql
```

### Archivos de configuración de MySQL Server
El principal /etc/mysql/mysql.cnf

Existen otros archivos de configuración:

- /etc/mysql/conf.d
- /etc/mysql/mysql.conf.d/

### Archivos de log de MySQL Server

- /var/log/mysql/error.log

### Como acceder a MySQL Server desde consola con root

```
sudo su 
mysql -u root
```
### Como cambiar la contraseña del usuario root
Accedemos a la consola de MySQL como root y seleccionamos la base de datos mysql para ver los usuarios y el tipo de autenticación que tienen.

Para cambiar la contraseña de root cambiamos el método de autenticación

``` ALTER USER 'root'@'localhost' IDENTIFIED WITH caching_sha2_password BY 'nueva_contraseña';```

A continuación ejecutamos el siguiente comando para actualizar la contraseña

```FLUSH PRIVILEGES;```

### Ejecutar un script.sql desde consola

Desde consola linux: 

```
mysql -u -p < script.sql
```

Desde la consola de MySQL:

```
mysql> source script.sql 
```

### Usuarios y permisos en MySQL Server desde consola
-  ##### Tipos de permisos que podemos aplicar
```ALL PRIVILEGES: permite a un usuario de MySQL acceder a todas las bases de datos asignadas en el sistema.
CREATE: permite crear nuevas tablas o bases de datos.
DROP: permite eliminar tablas o bases de datos
DELETE: permite eliminar registros de tablas.
INSERT: permite insertar registros en tablas.
SELECT: permite leer registros en las tablas.
UPDATE: permite actualizar registros seleccionados en tablas.
GRANT OPTION: permite asignar privilegios a otros usuarios.
```
 #### Crear un nuevo usuario
 
 ```
 CREATE USER 'nombre_usuario'@'localhost' IDENTIFIED BY 'contraseña';
 ```
 
 #### Eliminar un usuario
 
``` 
DROP USER 'nombre_usuario'@'localhost';
```
 #### Asignar permisos a un usuario
 
 ```
 GRANT [permiso] ON [nombre_base_de_datos].[nombre_tabla] TO 'nombre_usuario'@'localhost';
 ```
 
 Después de este comando habrá que ejecutar el siguiente comando para refrescar todos los privilegios
 
 ```
 FLUSH PRIVILEGES;
 ```
 
 #### Eliminar permisos a un usuario
 
```
REVOKE [permiso] ON [nombre_base_de_datos].[nombre_tabla] FROM 'nombre_usuario'@'localhost';
```

## PHP

- ### Instalación de módulos PHP

```
sudo apt install php libapache2-mod-php php-msyql
```

## Otras herramientas relacionadas con la pila LAMP

- ### Instalar phpMyAdmin para acceder vía web a MySQL

#### Instalación de phpMyAdmin con apt

```
sudo apt install phpmyadmin php-mbstring php-zip php-gd php-json php-curl
```

- ### Instalación de GoAccess

Para instalar la ultima versión de GoAccess añadimos los repositorios oficiales del proyecto

```
echo "deb http://deb.goaccess.io/ $(lsb_release -cs) main" | sudo tee -a /etc/apt/sources.list.d/goaccess.list

wget -O - https://deb.goaccess.io/gnugpg.key | sudo apt-key add -

sudo apt-get update

sudo apt-get install goaccess
```
