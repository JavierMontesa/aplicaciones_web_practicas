Se comprueba la version del sistema.

<img width="369" height="134" alt="imagen" src="https://github.com/user-attachments/assets/e07b6fc4-cffc-48fe-b7c2-e3f69eff0439" />

Se instala apache.

<img width="493" height="56" alt="imagen" src="https://github.com/user-attachments/assets/2a4ac96b-863b-4363-a187-179148763e9f" />
<img width="403" height="58" alt="imagen" src="https://github.com/user-attachments/assets/7a39701d-364a-43ef-a01d-4bd9f90f2425" />

❓¿Qué paquetes adicionales se han instalado como dependencias?

<img width="739" height="42" alt="imagen" src="https://github.com/user-attachments/assets/c394b0b7-0937-43e7-a4e8-10fb822f69bf" />

Se comprueba el estado del servicio.

<img width="814" height="345" alt="imagen" src="https://github.com/user-attachments/assets/444a3e45-f197-40e8-aea3-2fd20b8789f8" />

Puertos de escucha.

<img width="786" height="80" alt="imagen" src="https://github.com/user-attachments/assets/54f1c1b0-b318-4cc2-b910-8b4930aec8e1" />

Prueba terminal y navegador.

<img width="535" height="203" alt="imagen" src="https://github.com/user-attachments/assets/c029d52b-90ec-4b19-a2d1-3c66d4151d4c" />
<img width="851" height="710" alt="imagen" src="https://github.com/user-attachments/assets/7a66daa7-ec95-424e-a441-c184d80921c9" />

Firewall.

<img width="423" height="120" alt="imagen" src="https://github.com/user-attachments/assets/4f69206c-33e8-4cd5-8042-4e5ec4ff36c8" />

❓Qué diferencia hay entre los perfiles Apache, Apache Full y Apache Secure?

Apache-> instalacion basica..
Apache-> se instala apache con mas modulos.
Apache secure -> configuración orientada en https y seguridad.

Inicio de servicio

<img width="466" height="19" alt="imagen" src="https://github.com/user-attachments/assets/a703427f-fe6a-4d78-91bf-a37c850e785a" />

Detiene el servicio.

<img width="453" height="18" alt="imagen" src="https://github.com/user-attachments/assets/5eaacf85-67f5-41eb-8227-b135aa9955e5" />

Reinicia.

<img width="488" height="22" alt="imagen" src="https://github.com/user-attachments/assets/05c0feca-bba0-40db-921c-4a9c88f34dd2" />

Recarga la configuración sin cortar conexiones.

<img width="474" height="25" alt="imagen" src="https://github.com/user-attachments/assets/431c66f1-6014-4686-a51f-c6df1b36fcc9" />

Arranque automático al iniciar el sistema.

<img width="938" height="91" alt="imagen" src="https://github.com/user-attachments/assets/19cd7bc4-8889-4d1e-8060-382d2d4b4df6" />

Desactiva el arranque automático.

<img width="943" height="115" alt="imagen" src="https://github.com/user-attachments/assets/862d1e15-4ae4-474b-b1a8-804d4a75319a" />

Comprueba la sintaxis de la configuración.

<img width="947" height="84" alt="imagen" src="https://github.com/user-attachments/assets/c851b992-10a9-44b4-8906-07fb5511b763" />

Muestra los sitios (virtual hosts) cargados.

<img width="952" height="308" alt="imagen" src="https://github.com/user-attachments/assets/9b2d1f8c-ccb5-4ca1-b515-47f98e751013" />

Lista los módulos cargados.

<img width="890" height="253" alt="imagen" src="https://github.com/user-attachments/assets/d26121fe-4bbd-4681-8c28-e31407911dc8" />

Activa / desactiva módulos.

<img width="943" height="416" alt="imagen" src="https://github.com/user-attachments/assets/c628c185-3d9a-472f-9910-7f3e4b60f9e0" />

Activa / desactiva sitios.

<img width="551" height="176" alt="imagen" src="https://github.com/user-attachments/assets/152f1665-607e-4832-9e72-cdf4461cc0af" />

Activa / desactiva fragmentos de configuración.

<img width="948" height="173" alt="imagen" src="https://github.com/user-attachments/assets/6b367137-c1dd-4944-a172-95c315d20f58" />

❓Cuándo conviene usar reload en lugar de restart?

Conviene usarlo cundo se realizan cambios menores de configuracion.

Explorar la esructura de una configuracion.

<img width="657" height="251" alt="imagen" src="https://github.com/user-attachments/assets/15fa4f3e-db17-4ca5-93e3-71f0e5edae33" />


| Ruta | Descripción |
| :--- | :--- |
| `/etc/apache2/apache2.conf` | Fichero de configuración principal |
| `/etc/apache2/ports.conf` | Puertos en los que escucha Apache |
| `/etc/apache2/sites-available/` | Sitios disponibles (definidos, no necesariamente activos) |

Se comprueba que los ficheros de sites-enabled son enlaces simbólicos:

<img width="948" height="81" alt="imagen" src="https://github.com/user-attachments/assets/ecaa8ba9-3674-4187-928f-9258d5184e8b" />

❓Por qué Apache usa enlaces simbólicos entre los directorios *-available y *-enabled?

Para separar la creación de una configuración de su activación.

Haz siempre una copia de seguridad antes de modificar un fichero.

<img width="863" height="62" alt="imagen" src="https://github.com/user-attachments/assets/6b2c9078-9971-4cbc-a8ec-38be0e8f3c6a" />

Cambiar la pagina de inicio.

<img width="889" height="70" alt="imagen" src="https://github.com/user-attachments/assets/a04f7892-7140-4031-8af6-456c927bb0e0" />

Cambiar el puerto de escucha.

<img width="523" height="355" alt="imagen" src="https://github.com/user-attachments/assets/7c8a51c7-90c1-4405-9d30-3ee86b3e4ea3" />
<img width="943" height="339" alt="imagen" src="https://github.com/user-attachments/assets/bb14af14-01e7-4e6e-8805-9b9a986802b1" />

Definir el nombre del servidor.

<img width="945" height="289" alt="imagen" src="https://github.com/user-attachments/assets/67a7ce20-a356-4e75-b251-2ea8239e56c1" />

Cambiar el correo del administrador.

<img width="893" height="494" alt="imagen" src="https://github.com/user-attachments/assets/035cc31c-14f9-4be1-94d0-6cd817377549" />

