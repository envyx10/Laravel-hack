# Instalación de Laravel

Pasos a seguir en orden.

# WSL

Antes de nada, si no tenemos instalado WSL, tendremos que instalarlo con: wsl --install

# PHP y Composer, preparación del entorno

Debemos tener instalado PHP en nuestro sistema:

```
# Si queremos comprobar si tenemos instalado PHP antes de nada
php --version

# Si queremos comprobar si tenemos instaladas las extensiones
php -m

# Añadimos el repositorio necesario
sudo add-apt-repository ppa:ondrej/php

# Actualizamos la lista de paquetes
sudo apt update

# Instalamos las extensiones necesarias
sudo apt install php8.1 php8.1-cli php8.1-fpm
php8.1-mysql php8.1-mbstring php8.1-xml php8.1-zip

# Instalamos la herramienta PHP-FPM
sudo apt install php8.3-fpm

# Habilitamos la herramienta en el archivo de configuración de Apache
sudo a2enconf php8.3-fpm

# Instalamos Composer
curl -sS https://getcomposer.org/installer | php

# La instrucción anterior descarga el archivo composer.phar al directorio
# de trabajo, así que, para que sea accesible desde cualquier punto del sistema,
# tendremos que moverlo
sudo mv composer.phar /usr/local/bin/composer

# Comprobamos la versión
composer --version
```

# Node.js

```
# Instalamos las dependencias de Node.js, deben ser superiores a la versión 16
sudo apt install npm

# Comprobamos su versión
npm --version
```

# Creación de proyecto

```
# Instalamos Laravel haciendo uso de Composer
composer global require laravel/installer

# Creamos un nuevo proyecto de Laravel
composer create-project --prefer-dist laravel/laravel nombre-del-proyecto

# (Opcional) En caso de querer tener una versión específica
composer create-project laravel/laravel nombre-del-proyecto "5.8"
    # También podemos elegir la subversión más actualizada
    composer create-project --prefer-dist laravel/laravel nombre-del-proyecto "9.*"
        
# Ejecutar npm install
npm install
```

# Laravel Sail

```
# IMPORTANTE ESTAR EN LA RUTA CORRECTA DEL PROYECTO

# Instalamos las dependencias de Laravel Sail
composer require laravel/sail --dev

# Accedemos ahora a la carpeta del proyecto e instalamos Laravel Sail utilizando Artisan
php artisan sail:install - posteriormente elegimos el motor de BD que nos interese

# Las dependencias de Laravel Sail se descargan automáticamente cuando creamos un proyecto en Laravel. De no ser así:
composer require laravel/sail --dev

# Tras finalizar el proceso de instalación, y tras asegurarnos de tener abierto Docker, lanzamos nuestra herramienta con el siguiente comando
./vendor/bin/sail up # Comando en Linux

![alt text](image-1.png)

# Comprobamos que nuestro entorno pille Laravel
http://localhost y se tendrá que ver algo así:
![alt text](image.png)

# En caso de que no se vea así, habrá que parar Apache2 mediante systemctl stop apache2

# Para detener el servicio
./vendor/bin/sail stop

# Puedes crear un alias si no quieres estar poniendo todo el rato ./vendor/bin/sail
alias sail="./vendor/bin/sail"
```

# Laravel Breeze

```
# Una vez ya creado nuestro proyecto, procedemos a la instalación de Laravel Breeze
composer require laravel/breeze --dev

# Lo instalamos y lo configuramos
php artisan breeze:install

# Nos aparecerán varias opciones
Elegimos: Blade with Alpine (FRAMEWORK JS orientado a componentes)

# Nos preguntará si queremos modo oscuro o no (Opcional)

# Seguidamente nos preguntará por la librería que queremos utilizar para el testing
Elegimos: PHPUnit

# Es posible que tras su instalación se necesite compilar Tailwind CSS y otras dependencias
npm install
npm run dev
```

# .env

```
# Una vez tengamos todo instalado, nos vamos a la carpeta .env para cambiar varios parámetros tal que así:

APP_LOCALE=es # Este valor viene predefinido en "en"
APP_FALLBACK_LOCALE=en
APP_FAKER_LOCALE=es_ES # Este valor viene predefinido también

# Modificamos también los nombres
DB_CONNECTION=mysql  # Aquí tiene que estar el nombre de nuestro motor
DB_HOST=mysql        # Aquí tiene que estar el nombre de nuestro motor
DB_PORT=3306
DB_DATABASE=laravel  # Ponemos el nombre que queramos a nuestra BD
DB_USERNAME=sail     # Ponemos el nombre que queramos a nuestro usuario
DB_PASSWORD=password # Ponemos la contraseña que queramos a nuestra BD
```

# Faker

```
# Documentación oficial de Faker
https://fakerphp.org/   

# Datos personales
name: Genera un nombre completo aleatorio (nombre y apellido).
firstName: Genera un nombre aleatorio.
lastName: Genera un apellido aleatorio.
email: Genera una dirección de correo electrónico falsa pero con formato válido.
phoneNumber: Genera un número de teléfono falso.
address: Genera una dirección postal falsa.
city: Genera el nombre de una ciudad aleatoria.
state: Genera el nombre de un estado o provincia aleatoria.
postcode: Genera un código postal aleatorio.
dateOfBirth: Genera una fecha de nacimiento aleatoria.

# Texto
text: Genera un párrafo de texto aleatorio. Puedes especificar la longitud del texto.
sentence: Genera una oración aleatoria.
word: Genera una palabra aleatoria.
paragraph: Genera un párrafo de texto aleatorio.
title: Genera un título aleatorio.

# Números
randomNumber: Genera un número entero aleatorio. Puedes especificar un rango.
randomFloat: Genera un número decimal aleatorio. Puedes especificar precisión y rango.
numberBetween: Genera un número entero aleatorio entre dos valores específicos.

# Internet
url: Genera una URL falsa.
domainName: Genera un nombre de dominio falso.
userName: Genera un nombre de usuario aleatorio.
safeEmail: Genera una dirección de correo electrónico segura para pruebas (evita direcciones reales).

# Varios
boolean: Genera un valor booleano aleatorio (verdadero o falso).
randomElement: Selecciona un elemento aleatorio de un array que le proporciones.
randomKey: Selecciona una clave aleatoria de un array asociativo.
imageUrl: Genera una URL de imagen falsa.
```

