# Práctica: Instalación de WordPress en Ubuntu 24.04 (LAMP en marcha)

**Nombre:** Javier Montesa  
**Curso:** Sistemas Microinformáticos y Redes (SMR) - Aplicaciones Web  
**Fecha:** 28/10/2026  

---

## 1. Conexión por SSH y comprobación del servidor

Para administrar el servidor sin entorno gráfico, nos conectamos remotamente desde el terminal del ordenador anfitrión y comprobamos que los servicios web y de base de datos están activos.

```bash
hostname -I
ssh alumno@192.168.56.10
systemctl is-active apache2 mariadb
php -v
```

📸 **[ARRASTRA AQUÍ TU CAPTURA 1: Conexión SSH y comprobación]**

**¿Qué dos "puertas" (programas y puertos) usas para trabajar con el servidor en esta práctica y para qué sirve cada una?**
*   **SSH (puerto 22):** Se usa con el programa de Terminal para administrar el servidor de forma interna mediante comandos de texto (instalar, copiar, configurar).
*   **HTTP (puerto 80):** Se usa con el Navegador web para utilizar WordPress de forma gráfica (ver la web y usar el panel de control).

---

## 2. Dejar Apache con un único sitio

Desactivamos los sitios virtuales de prácticas anteriores y reactivamos el sitio por defecto de Apache para que todo el tráfico vaya directamente a la carpeta `/var/www/html`.

```bash
sudo a2dissite sitio1.conf sitio2.conf
sudo a2ensite 000-default.conf
sudo apache2ctl configtest
sudo systemctl reload apache2
ls /etc/apache2/sites-enabled/
grep DocumentRoot /etc/apache2/sites-enabled/000-default.conf
```

📸 **[ARRASTRA AQUÍ TU CAPTURA 2: Comandos y página por defecto de Apache]**

**¿Qué diferencia hay entre desactivar un sitio con `a2dissite` y borrar sus ficheros?**
*   Desactivar un sitio simplemente elimina el enlace de acceso directo en la carpeta `sites-enabled`, por lo que Apache deja de publicarlo, pero los ficheros de configuración y la web siguen guardados en el disco duro por si se quieren volver a usar en el futuro.
**¿Por qué ahora ves la página por defecto de Apache y antes veías sitio1?**
*   Porque hemos desactivado la configuración que le decía a Apache que mostrara `sitio1.local` y hemos vuelto a habilitar el archivo `000-default.conf`, cuyo `DocumentRoot` apunta directamente a `/var/www/html`.

---

## 3. Crear la base de datos de WordPress

WordPress requiere una base de datos propia para almacenar su información. Entramos al gestor MariaDB y creamos la base, el usuario y le asignamos los permisos necesarios.

```bash
sudo mariadb
CREATE DATABASE wordpress;
CREATE USER 'wp_user'@'localhost' IDENTIFIED BY '********';
GRANT ALL ON wordpress.* TO 'wp_user'@'localhost';
exit
mariadb -u wp_user -p wordpress
```

**Explicación de los comandos:**
*   `CREATE DATABASE wordpress;`: Crea el "armario" o base de datos vacía donde WordPress guardará todos sus datos.
*   `CREATE USER 'wp_user'...`: Crea la "llave" o usuario de conexión y le asigna su propia contraseña.
*   `GRANT ALL ON wordpress.*...`: Concede permisos totales a esa llave exclusivamente para usar el armario `wordpress` y ningún otro.

📸 **[ARRASTRA AQUÍ TU CAPTURA 3: Creación de BD y entrada con usuario]** *(Asegúrate de que la contraseña esté tapada)*

**¿Por qué crees que WordPress usa su propio usuario wp_user con permiso solo sobre su base y no el usuario root de MariaDB?**
*   Por seguridad. Si la web sufriera un ataque y descubrieran la contraseña de `wp_user`, el atacante solo tendría acceso a la base de datos de WordPress. Si usara el usuario root, tendría el control total de todas las bases de datos de todo el servidor.

---

## 4. Descargar e instalar los ficheros de WordPress

Descargamos el paquete oficial de WordPress, lo descomprimimos, lo movemos a la carpeta pública de Apache y le asignamos el propietario correcto para que funcione sin problemas de permisos.

```bash
sudo apt install wget -y
cd /tmp
wget https://wordpress.org/latest.tar.gz
tar -xzf latest.tar.gz
sudo rm /var/www/html/index.html
sudo cp -a /tmp/wordpress/. /var/www/html/
rm -r /tmp/wordpress /tmp/latest.tar.gz
sudo chown -R www-data:www-data /var/www/html
sudo find /var/www/html -type d -exec chmod 755 {} \;
sudo find /var/www/html -type f -exec chmod 644 {} \;
ls -ld /var/www/html
```

📸 **[ARRASTRA AQUÍ TU CAPTURA 4: Carpeta de WordPress y permisos]**

**Explica qué hace cada uno de los comandos que acabas de ejecutar:**
*   `wget` y `tar -xzf`: Descargan el archivo comprimido oficial de internet y lo extraen en la carpeta temporal.
*   `rm` y `cp -a`: Borran la página de bienvenida de Apache para evitar conflictos y copian todo el contenido extraído de WordPress a la carpeta web pública.
*   `chown -R www-data:www-data`: Cambia el propietario de todos los archivos y carpetas al usuario propio de Apache.
*   `find ... chmod`: Asigna permisos seguros: 755 a las carpetas (para poder entrar y leer) y 644 a los archivos (para poder leer).

**¿Por qué hay que cambiar el propietario de la carpeta de WordPress a www-data? ¿Qué podría fallar si siguiera siendo tu usuario?**
*   Porque `www-data` es el usuario invisible con el que se ejecuta el servidor Apache en segundo plano. Si el propietario siguiera siendo nuestro usuario personal, WordPress no tendría permisos de escritura, lo que impediría subir imágenes, instalar plugins o modificar la configuración desde la web.

---

## 5. Terminar la instalación desde el navegador (la parte gráfica)

Accedemos a la IP del servidor desde el navegador para completar la instalación gráfica, conectando WordPress a la base de datos MariaDB y creando nuestro usuario administrador.

📸 **[ARRASTRA AQUÍ TU CAPTURA 5: Pantallas 3 y 5 de instalación y escritorio]**

**¿Qué partes de la instalación has hecho en la terminal y cuáles en el navegador?**
*   **En la terminal:** Preparamos Apache, creamos la base de datos, descargamos los archivos, los movimos y asignamos los permisos (toda la configuración técnica interna).
*   **En el navegador:** Ejecutamos el asistente gráfico para elegir el título de la web, enlazar la base de datos y crear el usuario administrador (toda la configuración visual e interactiva).

**¿Por qué el servidor no necesita tener interfaz gráfica?**
*   Porque el servidor simplemente almacena y envía el código y texto de las páginas web; es el navegador de nuestro ordenador (el anfitrión) el que se encarga de procesar e interpretar ese código para dibujar la interfaz gráfica.

---

## 6. Comprobamos que WordPress funciona

Creamos una entrada de prueba desde el panel de administración y verificamos en la terminal cómo la base de datos ha generado las tablas internas para guardar esa información.

```bash
sudo mariadb wordpress -e "SHOW TABLES;"
```

📸 **[ARRASTRA AQUÍ TU CAPTURA 6: Entrada publicada y SHOW TABLES]**

**¿Dónde guarda WordPress las entradas que escribes: en ficheros del servidor o en la base de datos? ¿Cómo lo has comprobado?**
*   Las guarda en la base de datos, concretamente en la tabla `wp_posts` de MariaDB. Lo he comprobado ejecutando el comando `SHOW TABLES;` desde la terminal, lo que demuestra que el contenido (entradas, páginas, configuraciones) se almacena en tablas y no en archivos sueltos en el disco.

---

## 7. Para que no se rompa si cambia la IP

Modificamos el archivo de configuración principal de WordPress para que utilice variables dinámicas en lugar de una IP estática, evitando que la web se rompa si la máquina virtual cambia de dirección.

```bash
sudo nano /var/www/html/wp-config.php
# (Se añaden WP_HOME y WP_SITEURL con \$_SERVER['HTTP_HOST'])
php -l /var/www/html/wp-config.php
```

📸 **[ARRASTRA AQUÍ TU CAPTURA 7: Líneas en wp-config.php y comprobación]**

---

## 8. Dos ajustes para trabajar cómodamente

Habilitamos la lectura del archivo `.htaccess` para poder usar enlaces permanentes "bonitos" y modificamos la configuración de PHP para permitir la subida de archivos pesados (hasta 64 MB).

```bash
sudo nano /etc/apache2/conf-available/wordpress.conf
# (Se añade AllowOverride All al directorio)
sudo a2enmod rewrite
sudo a2enconf wordpress
sudo apache2ctl configtest
sudo systemctl restart apache2

printf 'upload_max_filesize = 64M\npost_max_size = 64M\n' | sudo tee /etc/php/8.3/apache2/conf.d/99-wordpress.ini
sudo systemctl restart apache2

ls -la /var/www/html/.htaccess
```

📸 **[ARRASTRA AQUÍ TU CAPTURA 8: Ajustes Apache, enlace bonito y subida 64MB]**

**¿Por qué las direcciones "bonitas" dan error 404 si Apache no tiene permitido leer el fichero .htaccess?**
*   Porque WordPress utiliza el archivo oculto `.htaccess` para guardar las reglas que traducen las rutas "bonitas" en consultas reales. Si Apache tiene bloqueada la directiva `AllowOverride`, ignora este archivo y, por tanto, no sabe interpretar la ruta solicitada, devolviendo un error 404 de página no encontrada.

---

## 9. ¿Qué pasa si MariaDB se para?

Simulamos una caída de la base de datos para identificar el error característico que devuelve WordPress y practicamos cómo solucionarlo restaurando el servicio.

```bash
sudo systemctl stop mariadb
# (Se recarga la web y muestra error)
sudo systemctl start mariadb
systemctl is-active mariadb
```

📸 **[ARRASTRA AQUÍ TU CAPTURA 9: Error en el navegador y web recuperada]**

**Cuando WordPress muestra "Error al establecer una conexión con la base de datos", ¿qué dos cosas comprobarías y en qué orden?**
*   **Primero:** Comprobaría si el servicio MariaDB está encendido y funcionando ejecutando `systemctl is-active mariadb`.
*   **Segundo:** Si el servicio está activo, comprobaría si el usuario y la contraseña siguen siendo correctos intentando entrar a mano a la base de datos ejecutando `mariadb -u wp_user -p wordpress`.

---

## 10. Comprobación final

Realizamos una última verificación de los servicios principales para asegurar que el entorno está estable y listo para trabajar.

```bash
systemctl is-active apache2 mariadb
php -v
ls /etc/apache2/sites-enabled/
sudo mariadb wordpress -e "SHOW TABLES;"
```
