## Instalación Laravel 11

<p>Hay diferentes opciones que puedes utilizar para la instalación de Laravel 11</p>
<article>Entre ellas podemos mencionar:
+ Xampp
+ Wampp
+ Lampp
+ Laragon
+ Composer
+ Node.js
+ En este tutorial utilizaremos <a href="https://herd.laravel.com/windows">Laravel Herd </a>
</article>

## Creando tu primer Route y View

Lo primero que vamos a ver es las rutas! ¿Cómo funciona esta pieza de información que encontramos bajo el folder routes/web.php?

    Route::get('/', function () {
    return view('welcome');
    });

Route, get, '/' [eso es tipicamente el homepage]...cuando 'obtienes' o 'visitas' el homepage, entonces 'corre', 'ejecuta esta función. Y parece que esta función retorna una vista llamada "welcome".

Así que básicamente estamos declarando una Ruta que esta escuchando un pedido GET, lo cual es visitar un URL en el navegador; en este caso, escuchar una petición a la 'homepage'. Si una persona esta escuchando un petición a la pógina 'about' lo escribiríamos así:

    Route::get('/about', function () {
    return view('about');
    });

Entonces, si el usuario visita esa página desencadena la función, y la función retorna una vista llamada 'welcome'.

Luego, nuestro siguiente pensamiento es: ¿Dónde esta la vista 'welcome'?

Para ello, debemos ir a la carpeta 'resources' y abrir otra carpeta que esta adentro llamada 'views' y ¡voilá!Encontraremos un archivo llamado 'welcome.blade.php'.

Blade es un motor de plantillas de Laravel. Es una capa encima de php que ofrece algunas comodidades que encontraras muy útiles. 

Al revisar 'welcome.blade.php' veremos que contiene el 'markup' para el 'homepage'. Hagámos lo siguiente, borremos todo lo que está en medio de la etiqueta 'body' y escribamos un título 'h1' que diga "Hello, World!

Refresquemos nuestra página y funciona! Muy bien, acabamos de aprender entonces que puedes visitar un archivo 'route' y puedes declarar una ruta, y esa 'ruta' puede retornar a lo que llamamos una 'vista'. Mantenlo simple.

Ahora, Declaremos una nueva ruta. hay un par de formas de hacerlo:

una: retornemos una simple cadena,

    Route::get('/about', function () {
    return 'about page';
    });

Así que volvamos a nuestro navegador y escribamos 'example.test/about'...Allí lo tienes: funciona!

También podemos retornar un arreglo [array]

    Route::get('/about', function () {
    return ['foo' => 'bar'];
    }); 

Y nuestro navegador lo convierte en un formato JSON.

dos: retornemos una vista...

    Route::get('/about', function () {
    return view('about');
    });

En este caso, tendremos que ir una vez más a la carpeta 'resources/views' y crear una nueva vista llamada simplemente 'about.php'.

Bien, ahora tenemos un nuevo proyecto en Laravel, donde hemos declarado dos rutas. Una de ellas es el 'homepage', y la otra carga la página 'About'.

Muy bien! Ahora una tarea: trata de crear una ruta que retorne una vista llamada "Contacts".


