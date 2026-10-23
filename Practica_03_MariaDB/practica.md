# Práctica: Instalación de MariaDB y PHP en Ubuntu 24.04 (LAMP)

**Nombre:** Javier Montesa  
**Curso:** Sistemas Microinformáticos y Redes (SMR) - Aplicaciones Web  
**Fecha:** 23/10/2026  

---

## Preparación del sistema
En primer lugar, deshabilitamos los sitios virtuales de la práctica anterior para dejar solo el sitio por defecto activo, y actualizamos los repositorios y paquetes del sistema.

```
sudo a2ensite 000-default.conf
sudo systemctl reload apache2
sudo apt update
sudo apt upgrade -y
systemctl is-active apache2
```
<img width="962" height="280" alt="Captura de 2026-10-23 09-37-11" src="https://github.com/user-attachments/assets/0da1b558-7218-4c11-bf1c-b3ea7326c34f" />

## Procedemos a instalar el sistema gestor de bases de datos MariaDB.

<img width="819" height="237" alt="Captura de 2026-10-23 09-40-09" src="https://github.com/user-attachments/assets/aaef06ee-7d06-40d4-861f-b0fac6872de9" />

## Comprobamos que el servicio está activo y configurado para arrancar con el sistema.

<img width="755" height="336" alt="Captura de 2026-10-23 09-42-38" src="https://github.com/user-attachments/assets/2c661b3f-2fc0-44b7-a41d-632f9c5b71a6" />

## Vamos a simular un fallo apagando la base de datos a propósito para comprobar qué error nos devolvería al intentar acceder

<img width="908" height="302" alt="Captura de 2026-10-23 09-44-45" src="https://github.com/user-attachments/assets/70d7b34e-3f89-4b26-8683-8a089d6acb0e" />

## Instalación de PHP.

```
sudo apt install php libapache2-mod-php php-mysql php-curl php-gd php-mbstring php-xml php-zip php-intl -y
php -v
sudo systemctl restart apache2
sudo apache2ctl -M | grep -E "mpm|php"
php -m | grep -i mysql
echo '<?php phpinfo();' | sudo tee /var/www/html/info.php
sudo rm /var/www/html/info.php
```

<img width="960" height="335" alt="Captura de 2026-10-23 09-54-48" src="https://github.com/user-attachments/assets/172f1f89-59d2-415b-ac97-5c331e11d7a9" />

<img width="952" height="1031" alt="Captura de 2026-10-23 10-00-48" src="https://github.com/user-attachments/assets/f1740073-6ebe-43be-b3d0-1300ad97afb3" />
