# Install -- WordPress
WordPress &amp; MediaWiki
# Guía para instalar y configurar WordPress en Ubuntu

Esta guía detalla los pasos para instalar y configurar WordPress en un servidor Ubuntu utilizando Apache, MySQL y PHP.

## Requisitos previos

- Tener un servidor Ubuntu funcionando.
- Acceso con permisos de `sudo`.
- Apache, MySQL y PHP ya instalados.

---

## Paso 1: Actualizar el sistema

Primero, actualiza el sistema para asegurarte de que todos los paquetes estén al día.

```bash
sudo apt update
sudo apt upgrade -y


##  Paso 2: Configuración de la base de datos MySQL
1.  Inicia sesión en MySQL como root: sudo mysql -u root -p
2.  Crea la base de datos y el usuario para WordPress:
CREATE DATABASE wordpress;
CREATE USER 'wpuser'@'localhost' IDENTIFIED BY 'password';
GRANT ALL PRIVILEGES ON wordpress.* TO 'wpuser'@'localhost';
FLUSH PRIVILEGES;
EXIT;


##  Paso 3: Instalar PHP y dependencias necesarias
Instala PHP y las extensiones necesarias para WordPress:
sudo apt install php libapache2-mod-php php-mysql php-xml php-mbstring php-curl php-zip php-gd -y
Reinicia Apache para aplicar los cambios:
sudo systemctl restart apache2
Paso 4: Descargar y configurar WordPress

1.  Dirígete al directorio de trabajo de Apache:
cd /var/www/html
2.  Elimina el archivo index.html predeterminado de Apache:
sudo rm index.html
3.  Descarga y descomprime la última versión de WordPress:
sudo tar -xvzf latest.tar.gz
4.  Mueve los archivos de WordPress a la raíz del directorio de Apache:
sudo mv wordpress/* /var/www/html/
5.  Cambia la propiedad de los archivos al usuario www-data (usuario de Apache):
sudo chown -R www-data:www-data /var/www/html/


##  Paso 5: Configurar WordPress
1.  Renombra el archivo de configuración de WordPress:
sudo mv /var/www/html/wp-config-sample.php /var/www/html/wp-config.php
2.  Abre el archivo de configuración para editarlo:
sudo nano /var/www/html/wp-config.php
3.  Modifica las siguientes líneas para reflejar los detalles de tu base de datos:
define( 'DB_NAME', 'wordpress' );
define( 'DB_USER', 'wpuser' );
define( 'DB_PASSWORD', 'password' );
define( 'DB_HOST', 'localhost' );


##  Paso 6: Finalizar la instalación de WordPress

1.  Abre tu navegador y ve a la dirección de tu servidor:
http://localhost/wp-admin/
2.  En la pantalla de configuración de WordPress, elige el idioma y completa el formulario con la información requerida (nombre del sitio, usuario, contraseña, etc.).
3.  Configuración de contraseña:

  Si te piden configurar un nivel de seguridad para la contraseña, puedes elegir entre:
  0 = LOW: Baja seguridad.
  1 = MEDIUM: Seguridad media.
  2 = STRONG: Alta seguridad.


  Se recomienda elegir 2 (STRONG) para una mayor seguridad, especialmente para la contraseña de    administración.


##  Paso 7: Conclusión

http://localhost/wp-admin/
 Ya puedes gestionarlo y personalizarlo






