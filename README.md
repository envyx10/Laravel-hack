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
13. [Enrutamiento en Laravel 11](#enrutamiento-en-laravel-11)

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

![laravelHow](https://github.com/user-attachments/assets/2e8dd0fe-d081-4c7d-84d8-d80055450936)

En caso de que no se vea como arriba y se vea asi:

![image](https://github.com/user-attachments/assets/d9d08e6e-5277-4c4b-a289-0a9534a69713)

Se arregla modificando los valores de .env que se especifican algo mas abajo de los apuntes. 


```sh
# En caso de que no se vea así de ninguna de las maneras de las de arriba y se vea apache2, habrá que parar Apache2 mediante:
systemctl stop apache2
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

```sh
# Modificamos nombre especificado
SESSION_DRIVER=database # Por defecto viene database, cambiar a file para que no de problemas
SESSION_LIFETIME=120
SESSION_ENCRYPT=false
SESSION_PATH=/
SESSION_DOMAIN=null

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

### Migraciones

Las migraciones son una herramienta en Laravel que permite crear y modificar la estructura de la base de datos de manera controlada y versionada. Son especialmente útiles para mantener la consistencia de la base de datos a lo largo del desarrollo y las actualizaciones.

#### Crear una migración

```sh
# Crear una nueva migración
artisan make:migration create_nombre_table (debe mantener esta nomenclatura)
```

#### Ejecutar migraciones

```sh
# Ejecutar todas las migraciones pendientes
artisan migrate
```

#### Ejemplo de migración

En la función up(), definimos la estructura de la tabla users. 
Especificamos el nombre de la tabla y las columnas que contendrá, indicando su tipo de dato y propiedades.

Cada columna se declara dentro del método table(), donde el primer argumento es el nombre de la columna y el segundo define su tipo. 
También podemos agregar restricciones como claves primarias, valores predeterminados o marcas de tiempo.

```php
use Illuminate\Database\Migrations\Migration;
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Support\Facades\Schema;

class CreateUsersTable extends Migration
{
    public function up()
    {
        Schema::create('users', function (Blueprint $table) {
            $table->id();
            $table->string('name');
            $table->string('email')->unique();
            $table->timestamp('email_verified_at')->nullable();
            $table->string('password');
            $table->rememberToken();
            $table->timestamps();
        });
    }

    public function down()
    {
        Schema::dropIfExists('users');
    }
}
```

### Semilleros

Los seeders (semilleros) son una herramienta en Laravel que permite poblar la base de datos con datos de prueba. 
Son especialmente útiles durante el desarrollo y las pruebas, ya que permiten llenar la base de datos con datos consistentes y predecibles.

#### Crear un seeder

```sh
# Crear un nuevo seeder
artisan make:seeder nombretablaTableSeeder
```

#### Ejecutar seeders

```sh
# Ejecutar todos los seeders
artisan db:seed
```

#### Ejemplo de Seeder

```php
use Illuminate\Database\Seeder;
use Illuminate\Support\Facades\Hash;

class UsersTableSeeder extends Seeder
{
    public function run()
    {
        DB::table('users')->insert([
            'name' => 'John Doe',
            'email' => 'john@example.com',
            'password' => Hash::make('password'),
        ]);
    }
}
```

### Factorías

Las factorías son una herramienta en Laravel que permite crear modelos de manera masiva con datos aleatorios utilizando Faker. 
Son especialmente útiles para poblar la base de datos con datos de prueba durante el desarrollo y las pruebas.

#### Crear una factoría

```sh
# Crear una nueva factoría
artisan make:factory nombreTablaFactory
```

#### Ejecutar factorías

```sh
# Ejecutar las factorías
artisan db:seed
```

#### Ejemplo de Factoría

```php
use Illuminate\Database\Eloquent\Factories\Factory;
use Illuminate\Support\Str;

class UserFactory extends Factory
{
    protected $model = User::class;

    public function definition()
    {
        return [
            'name' => $this->faker->name,
            'email' => $this->faker->unique()->safeEmail,
            'email_verified_at' => now(),
            'password' => Hash::make('password'), // password
            'remember_token' => Str::random(10),
        ];
    }
}
```

### DatabaseSeeder.php

El archivo `DatabaseSeeder.php` es el punto de entrada para ejecutar todos los seeders y factorías que queremos ejecutar. 
Tanto los seeders como las factorías dependen de este archivo para ser ejecutados.

Ejecutamos la inserción de datos utilizando factory(), donde el primer argumento es el modelo asociado a la tabla y el segundo define la cantidad de registros a generar.
    Ejemplo: Usuario::factory(10)->create()
    
#### Ejemplo de DatabaseSeeder.php

```php
use Illuminate\Database\Seeder;

class DatabaseSeeder extends Seeder
{
    public function run()
    {

        # Llamamos al seeder de Usuario
        $this->call(UsuarioSeeder::class); 

        # Creamos 10 usuarios con el factory
        Usuario::factory(10)->create();

        # Creamos 30 series con el factory
        Serie::factory(30)->create(); 

        # Creamos 30 valoraciones con el factory
        Valoracion::factory(30)->create(); 
   
    }
    }
}
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

Importante, si usamos factorías debemos añadir el trait `HasFactory`.

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

## Enrutamiento en Laravel 11

En este documento se explica cómo funcionan las rutas en Laravel 11, enfocándose en los métodos HTTP más comunes: GET, POST, PUT, DELETE y PATCH.

### Concepto Básico del Routing en Laravel

En Laravel, el enrutamiento se utiliza para definir qué acción debe tomar la aplicación cuando un usuario accede a una URL específica. Los enrutamientos se definen generalmente en los archivos ubicados dentro del directorio `routes/`. Para aplicaciones web, el archivo principal es `routes/web.php`.

Cada ruta está asociada con un controlador o una función closure que maneja la lógica correspondiente.

### Métodos HTTP en Laravel

Laravel proporciona métodos específicos para cada verbo HTTP. A continuación, se explican cada uno:

#### Ruta GET

El método GET se utiliza para recuperar información de un recurso. Es el tipo de solicitud más común cuando visitas una página web.

```php
Route::get('/ruta', function () {
    return 'Respuesta al hacer una solicitud GET';
});
```

Ejemplo Práctico:

```php
Route::get('/saludo', function () {
    return 'Hola, bienvenido a mi sitio';
});
```

Si visitas la URL `/saludo` en tu navegador, verás el mensaje "Hola, bienvenido a mi sitio".

#### Ruta POST

El método POST se utiliza para enviar datos al servidor, típicamente desde formularios. Este método no debe ser accesible directamente desde la barra de direcciones del navegador.

```php
Route::post('/ruta', function () {
    return 'Respuesta al hacer una solicitud POST';
});
```

Ejemplo Práctico:

```php
Route::post('/enviar-formulario', function (Request $request) {
    // Acceder a los datos enviados por el formulario
    $nombre = $request->input('nombre');
    return 'Formulario enviado correctamente. Nombre: ' . $nombre;
});
```

Para probar esto, necesitarías un formulario HTML que envíe datos a esta ruta usando el método POST.

#### Ruta PUT

El método PUT se utiliza para actualizar un recurso existente. En general, se emplea en APIs RESTful.

```php
Route::put('/ruta/{id}', function ($id) {
    return 'Actualizando el recurso con ID: ' . $id;
});
```

Ejemplo Práctico:

```php
Route::put('/actualizar-usuario/{id}', function ($id) {
    return 'Usuario con ID ' . $id . ' ha sido actualizado';
});
```

Este tipo de ruta suele usarse en combinación con JavaScript o herramientas como Postman para realizar solicitudes.

#### Ruta DELETE

El método DELETE se utiliza para eliminar un recurso específico.

```php
Route::delete('/ruta/{id}', function ($id) {
    return 'Recurso con ID: ' . $id . ' eliminado';
});
```

Ejemplo Práctico:

```php
Route::delete('/eliminar-usuario/{id}', function ($id) {
    return 'Usuario con ID ' . $id . ' ha sido eliminado';
});
```

Al igual que con PUT, este método suele requerir una solicitud desde JavaScript o herramientas externas.

#### Ruta PATCH

El método PATCH también se usa para actualizar recursos, pero a diferencia de PUT, solo actualiza partes específicas del recurso en lugar de reemplazarlo completamente.

```php
Route::patch('/ruta/{id}', function ($id) {
    return 'Recurso con ID: ' . $id . ' parcialmente actualizado';
});
```

Ejemplo Práctico:

```php
Route::patch('/actualizar-perfil/{id}', function ($id, Request $request) {
    $campo = $request->input('campo');
    return 'Campo ' . $campo . ' del perfil con ID ' . $id . ' actualizado';
});
```

### Parámetros en las Rutas

Las rutas pueden incluir parámetros dinámicos que permiten trabajar con identificadores únicos o valores variables.

#### Parámetros Obligatorios

```php
Route::get('/usuario/{id}', function ($id) {
    return 'Mostrando usuario con ID: ' . $id;
});
```

Aquí, `{id}` es un parámetro obligatorio.

#### Parámetros Opcionales

```php
Route::get('/buscar/{termino?}', function ($termino = null) {
    if ($termino) {
        return 'Buscando: ' . $termino;
    } else {
        return 'No se proporcionó ningún término de búsqueda';
    }
});
```

El signo `?` indica que el parámetro es opcional.

### Redirección de Rutas

Puedes redirigir una ruta a otra usando el método `redirect()`.

Ejemplo:

```php
Route::get('/antigua-ruta', function () {
    return redirect('/nueva-ruta');
});
```

### Rutas con Controladores

En lugar de usar closures, puedes asignar rutas a métodos de un controlador.

```php
Route::get('/ruta', [Controlador::class, 'metodo']);
```

Ejemplo Práctico:

```php
use App\Http\Controllers\UsuarioController;

Route::get('/usuarios', [UsuarioController::class, 'index']);
Route::post('/usuarios', [UsuarioController::class, 'store']);
Route::put('/usuarios/{id}', [UsuarioController::class, 'update']);
Route::delete('/usuarios/{id}', [UsuarioController::class, 'destroy']);
```

### Grupos de Rutas

Los grupos de rutas permiten agrupar varias rutas bajo un prefijo o middleware común.

#### Ejemplo con Prefijo

```php
Route::prefix('admin')->group(function () {
    Route::get('/usuarios', function () {
        return 'Lista de usuarios administrativos';
    });

    Route::get('/configuracion', function () {
        return 'Configuración del panel de administración';
    });
});
```

#### Ejemplo con Middleware

```php
Route::middleware('auth')->group(function () {
    Route::get('/dashboard', function () {
        return 'Panel de control (requiere autenticación)';
    });
});
```

### Resumen de Métodos HTTP

| Método  | Acción                      | Ejemplo Práctico                |
|---------|-----------------------------|---------------------------------|
| GET     | Recuperar datos             | Mostrar lista de usuarios       |
| POST    | Crear un nuevo recurso      | Guardar datos de un formulario  |
| PUT     | Actualizar un recurso completo | Actualizar perfil de usuario |
| PATCH   | Actualizar partes de un recurso | Cambiar correo electrónico  |
| DELETE  | Eliminar un recurso         | Eliminar usuario                |
