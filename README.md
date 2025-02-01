<p align="center"><a href="https://laravel.com" target="_blank"><img src="https://raw.githubusercontent.com/laravel/art/master/logo-lockup/5%20SVG/2%20CMYK/1%20Full%20Color/laravel-logolockup-cmyk-red.svg" width="400" alt="Laravel Logo"></a></p>

# Instalación de Laravel

Pasos a seguir en orden.

## Índice

1. [WSL](#wsl)
2. [PHP y Composer, preparación del entorno](#php-y-composer-preparación-del-entorno)
3. [Node.js](#nodejs)
4. [Creación de proyecto](#creación-de-proyecto)
5. [Laravel Sail](#laravel-sail)
6. [Laravel Breeze](#laravel-breeze)
7. [Configuración del archivo .env](#configuración-del-archivo-env)
8. [Faker](#faker)
9. [Base de datos](#base-de-datos)
10. [Relaciones](#relaciones)
11. [Modelos](#modelos)
12. [Métodos modelos](#métodos-modelos)

## WSL

Antes de nada, si no tenemos instalado WSL, tendremos que instalarlo con:

```sh
wsl --install
```

## PHP y Composer, preparación del entorno

Debemos tener instalado PHP en nuestro sistema:

```sh
# Si queremos comprobar si tenemos instalado PHP antes de nada
php --version
```

```sh
# Si queremos comprobar si tenemos instaladas las extensiones
php -m
```

```sh
# Añadimos el repositorio necesario
sudo add-apt-repository ppa:ondrej/php
```

```sh
# Actualizamos la lista de paquetes
sudo apt update
```

```sh
# Instalamos las extensiones necesarias
sudo apt install php8.1 php8.1-cli php8.1-fpm php8.1-mysql php8.1-mbstring php8.1-xml php8.1-zip
```

```sh
# Instalamos la herramienta PHP-FPM
sudo apt install php8.3-fpm
```

```sh
# Habilitamos la herramienta en el archivo de configuración de Apache
sudo a2enconf php8.3-fpm
```

```sh
# Instalamos Composer
curl -sS https://getcomposer.org/installer | php
```

```sh
# La instrucción anterior descarga el archivo composer.phar al directorio
# de trabajo, así que, para que sea accesible desde cualquier punto del sistema,
# tendremos que moverlo
sudo mv composer.phar /usr/local/bin/composer
```

```sh
# Comprobamos la versión
composer --version
```

## Node.js

```sh
# Instalamos las dependencias de Node.js, deben ser superiores a la versión 16
sudo apt install npm
```

```sh
# Comprobamos su versión
npm --version
```

## Creación de proyecto

```sh
# Instalamos Laravel haciendo uso de Composer
composer global require laravel/installer
```

```sh
# Creamos un nuevo proyecto de Laravel
composer create-project --prefer-dist laravel/laravel nombre-del-proyecto
```

```sh
# (Opcional) En caso de querer tener una versión específica
composer create-project laravel/laravel nombre-del-proyecto "5.8"
```

```sh
# También podemos elegir la subversión más actualizada
composer create-project --prefer-dist laravel/laravel nombre-del-proyecto "9.*"
```

```sh
# Ejecutar npm install
npm install
```

## Laravel Sail

```sh
# IMPORTANTE ESTAR EN LA RUTA CORRECTA DEL PROYECTO

# Instalamos las dependencias de Laravel Sail
composer require laravel/sail --dev
```

```sh
# Accedemos ahora a la carpeta del proyecto e instalamos Laravel Sail utilizando Artisan
php artisan sail:install - posteriormente elegimos el motor de BD que nos interese
```

```sh
# Las dependencias de Laravel Sail se descargan automáticamente cuando creamos un proyecto en Laravel. De no ser así:
composer require laravel/sail --dev
```

```sh
# Tras finalizar el proceso de instalación, y tras asegurarnos de tener abierto Docker, lanzamos nuestra herramienta con el siguiente comando
./vendor/bin/sail up # Comando en Linux
```


```sh
# Comprobamos que nuestro entorno pille Laravel
http://localhost y se tendrá que ver algo así:
```
![laravelHow](https://github.com/user-attachments/assets/4c850321-df2f-47f7-afd9-09b4d45e7dce)

```sh
# En caso de que no se vea así, habrá que parar Apache2 mediante systemctl stop apache2
```

```sh
# Para detener el servicio
./vendor/bin/sail stop
```

```sh
# Puedes crear un alias si no quieres estar poniendo todo el rato ./vendor/bin/sail
alias sail="./vendor/bin/sail"
```

## Laravel Breeze

```sh
# Una vez ya creado nuestro proyecto, procedemos a la instalación de Laravel Breeze
composer require laravel/breeze --dev
```

```sh
# Lo instalamos y lo configuramos
php artisan breeze:install
```

```sh
# Nos aparecerán varias opciones
# Elegimos: Blade with Alpine (FRAMEWORK JS orientado a componentes)
```

```sh
# Nos preguntará si queremos modo oscuro o no (Opcional)
```

```sh
# Seguidamente nos preguntará por la librería que queremos utilizar para el testing
# Elegimos: PHPUnit
```

```sh
# Es posible que tras su instalación se necesite compilar Tailwind CSS y otras dependencias
npm install
npm run dev
```

## Configuración del archivo .env

```sh
# Una vez tengamos todo instalado, nos vamos a la carpeta .env para cambiar varios parámetros tal que así:

APP_LOCALE=es # Este valor viene predefinido en "en"
APP_FALLBACK_LOCALE=en
APP_FAKER_LOCALE=es_ES # Este valor viene predefinido también
```

```sh
# Modificamos también los nombres
DB_CONNECTION=mysql  # Aquí tiene que estar el nombre de nuestro motor
DB_HOST=mysql        # Aquí tiene que estar el nombre de nuestro motor
DB_PORT=3306
DB_DATABASE=laravel  # Ponemos el nombre que queramos a nuestra BD
DB_USERNAME=sail     # Ponemos el nombre que queramos a nuestro usuario
DB_PASSWORD=password # Ponemos la contraseña que queramos a nuestra BD
```

## Faker

```sh
# Documentación oficial de Faker
https://fakerphp.org/   
```

```sh
# Datos personales
fake()->name: Genera un nombre completo aleatorio (nombre y apellido).
fake()->firstName: Genera un nombre aleatorio.
fake()->lastName: Genera un apellido aleatorio.
fake()->email: Genera una dirección de correo electrónico falsa pero con formato válido.
fake()->phoneNumber: Genera un número de teléfono falso.
fake()->address: Genera una dirección postal falsa.
fake()->city: Genera el nombre de una ciudad aleatoria.
fake()->state: Genera el nombre de un estado o provincia aleatoria.
fake()->postcode: Genera un código postal aleatorio.
fake()->dateOfBirth: Genera una fecha de nacimiento aleatoria.
```

```sh
# Texto
fake()->text: Genera un párrafo de texto aleatorio. Puedes especificar la longitud del texto.
fake()->sentence: Genera una oración aleatoria.
fake()->word: Genera una palabra aleatoria.
fake()->paragraph: Genera un párrafo de texto aleatorio.
fake()->title: Genera un título aleatorio.
```

```sh
# Números
fake()->randomNumber: Genera un número entero aleatorio. Puedes especificar un rango.
fake()->randomFloat: Genera un número decimal aleatorio. Puedes especificar precisión y rango.
fake()->numberBetween: Genera un número entero aleatorio entre dos valores específicos.
```

```sh
# Internet
fake()->url: Genera una URL falsa.
fake()->domainName: Genera un nombre de dominio falso.
fake()->userName: Genera un nombre de usuario aleatorio.
fake()->safeEmail: Genera una dirección de correo electrónico segura para pruebas (evita direcciones reales).
```

```sh
# Varios
fake()->boolean: Genera un valor booleano aleatorio (verdadero o falso).
fake()->randomElement: Selecciona un elemento aleatorio de un array que le proporciones.
fake()->randomKey: Selecciona una clave aleatoria de un array asociativo.
fake()->imageUrl: Genera una URL de imagen falsa.
```

## Base de datos

```sh
# Migraciones: Crea la estructura de BD
artisan make:migration create_nombre_table (debe mantener esta nomenclatura)
artisan migrate

# Importante, tienen que ser en orden, si una tabla depende de la otra puede darnos fallos, hay que tener cuidado
```

```sh
# Semilleros: Sirve para poblar la BD con datos prefijados durante el desarrollo
artisan make:seeder nombretablaTableSeeder
artisan db:seed
```

```sh
# Factorias: Sirve para poblar la BD de forma masiva con datos aleatorios utilizando Faker
artisan make:factory nombreTablaFactory
artisan db:seed
```

```sh
# DatabaseSeeder.php: Factorias y semilleros que queremos ejecutar (Tanto semilleros como factorias dependen de esto)
```

## Relaciones

### Relaciones 1:1

- `A` to `B` -> `hasOne`
- `B` to `A` -> `belongsTo`

### Relaciones 1:N

- `A` to `B` -> `hasMany`
- `B` to `A` -> `belongsTo`

### Relaciones N:N

- `A` to `B` -> `belongsToMany`
- `B` to `A` -> `belongsToMany`
- `AB` tabla pivote -> `belongsToMany`
  - El resultado contiene un objeto tipo `pivot`

### Ejemplos

#### Relación 1:1

```php
// En el modelo A
public function b()
{
    return $this->hasOne(B::class);
}

// En el modelo B
public function a()
{
    return $this->belongsTo(A::class);
}
```

#### Relación 1:N

```php
// En el modelo A
public function bs()
{
    return $this->hasMany(B::class);
}

// En el modelo B
public function a()
{
    return $this->belongsTo(A::class);
}
```

#### Relación N:N

```php
// En el modelo A
public function bs()
{
    return $this->belongsToMany(B::class);
}

// En el modelo B
public function as()
{
    return $this->belongsToMany(A::class);
}
```

## Modelos

Importante, si usamos factorias debemos añadir el trait `HasFactory`.

```php
use Illuminate\Database\Eloquent\Factories\HasFactory;
use Illuminate\Database\Eloquent\Model;

class User extends Model
{
    use HasFactory;

    // Nombre de la tabla asociada al modelo
    protected $table = 'users';

    // Clave primaria de la tabla
    protected $primaryKey = 'id';

    // Indica si el modelo debe gestionar las marcas de tiempo (created_at, updated_at)
    public $timestamps = true;

    // Atributos que se pueden asignar masivamente
    protected $fillable = ['name', 'email', 'password'];

    // Atributos que no se pueden asignar masivamente
    protected $guarded = ['id'];

    // Atributos que deben estar ocultos en las representaciones JSON
    protected $hidden = ['password', 'remember_token'];

    // Ejemplo de una relación 1:N
    public function posts()
    {
        return $this->hasMany(Post::class);
    }
}
```

### Atributos

- `protected $table`: Nombre de la tabla asociada al modelo.
  ```php
  protected $table = 'users';
  ```

- `protected $primaryKey`: Clave primaria de la tabla.
  ```php
  protected $primaryKey = 'id';
  ```

- `public $timestamps`: Indica si el modelo debe gestionar las marcas de tiempo (created_at, updated_at).
  ```php
  public $timestamps = true;
  ```

- `protected $fillable`: Atributos que se pueden asignar masivamente.
  ```php
  protected $fillable = ['name', 'email', 'password'];
  ```

- `protected $guarded`: Atributos que no se pueden asignar masivamente.
  ```php
  protected $guarded = ['id'];
  ```

- `protected $hidden`: Atributos que deben estar ocultos en las representaciones JSON.
  ```php
  protected $hidden = ['password', 'remember_token'];
  ```

### Métodos

- `public function posts()`: Ejemplo de una relación 1:N.
  
  ```php
  public function posts()
  {
      return $this->hasMany(Post::class);
  }
  ```

## Métodos modelos

```sh
# create([]): Crea un nuevo registro en la base de datos con los atributos proporcionados.
User::create(['name' => 'John Doe', 'email' => 'john@example.com']);
```

```sh
# getResults(): Obtiene los resultados de una consulta.
$users = User::where('active', 1)->getResults();
```

```sh
# first(): Obtiene el primer registro de una consulta.
$user = User::where('email', 'john@example.com')->first();
```

```sh
# get([]): Obtiene una colección de registros que coinciden con los criterios de la consulta.
$users = User::where('active', 1)->get();
```

```sh
# find(primaryKey): Encuentra un registro por su clave primaria.
$user = User::find(1);
```

```sh
# all(): Obtiene todos los registros de la tabla.
$users = User::all();
```

```sh
# attach(): Asocia un modelo con otro en una relación de muchos a muchos.
$user->roles()->attach($roleId);
```

```sh
# detach(): Desasocia un modelo de otro en una relación de muchos a muchos.
$user->roles()->detach($roleId);
```
