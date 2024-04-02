#INFO SOBRE EL DOCKER

nginx: Este servicio utiliza la imagen oficial de Nginx y se encarga de servir los archivos estáticos y actuar como proxy inverso para dirigir el tráfico a otros servicios. Está configurado para escuchar en el puerto 8181 de la máquina host y se mapea al puerto 80 del contenedor Nginx. Además, monta un archivo de configuración personalizado default.conf desde el directorio local ./docker/nginx/ en el contenedor para personalizar la configuración de Nginx. Este servicio también utiliza el volumen del servicio php.

frontend: Este servicio utiliza un Dockerfile personalizado ubicado en ./docker/node/ para construir una imagen del contenedor. Este servicio se utiliza para servir el frontend de la aplicación. Está configurado para escuchar en el puerto 8182 de la máquina host y se mapea al puerto 8080 del contenedor. Además, monta el directorio ./frontend en el directorio /app del contenedor para proporcionar los archivos de la aplicación frontend.

php: Este servicio utiliza un Dockerfile personalizado ubicado en ./docker/php/ para construir una imagen del contenedor. Está configurado para ejecutar un servidor PHP para servir la aplicación backend. Monta el directorio ./backend en el directorio /var/www/html del contenedor para proporcionar los archivos de la aplicación backend. También monta un archivo de configuración personalizado custom.ini desde ./docker/php/ en el contenedor para personalizar la configuración de PHP. Este servicio también establece variables de entorno para la base de datos, como el puerto y el host del servicio database. Además, utiliza el enlace al servicio database.

database: Este servicio utiliza la imagen oficial de MySQL 5.7 para ejecutar una base de datos MySQL. Está configurado con una contraseña de root y una base de datos predeterminada. Además, monta un volumen en el directorio /var/lib/mysql del contenedor para persistir los datos de la base de datos. Está configurado para escuchar en el puerto 33065 de la máquina host y se mapea al puerto 3306 del contenedor.