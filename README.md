## Day 3: Create a Layout file using Laravel Components

Aquí es donde nos quedamos al final del día 2:

    Route::get('/contact', function () {
    return view('contact');
    });

Creamos en nuestra tarea una ruta para la página 'Contact'

Aún estamos utilizando la página 'welcome' que viene por defecto. ¿qué tal si cambiamos su nombre a 'home'? Ok, entonces si cambio ese nombre tendré que actualizar el nombre de la vista:

    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>Home Page</title>
    </head>
    <body>
        <h1>Hello from the Home Page.</h1>
    </body>
    </html>

Creamos la vista de 'contact tambien utilizando la misma plantilla, y luego probamos en el navegador si funciona.

Obviamente no deseamos estar cambiando de URL cada vez que tengamos que cambiar de página, así que agregaremos nuestra simple área de navegación:

    <nav>
        <a href="/">Home</a>
        <a href="/about">About</a>
        <a href="/contact">Contact</a>
    </nav>

la cual colocaremos arriba de nuestro 'Hello from..."

No se verá lindo pero si vamos a la 'home' page veremos el menú. Ahora, por lo menos desde 'home', podremos accesar la página 'about' o la de 'contact.

Ahora bien, desde el momento que cargamos esas páginas perderemos esa área de navegación.

Si somos principitantes esto lo resolveremos fácilmente copiando y pegando el área de navegación en cada vista. Y funcionará, pero no es 'escalable', no es la mejor idea.

Es en este caso que utilizaremos una plantilla o 'layout'. Primero volvamos a cambiar los nombres de nuestras vistas agregando la palabra 'blade' a su nombre: home.blade.php.

Recuerda, Blade es el motor de plantillas de Laravel. Es una pequeña capa sobre PHP que una vez cargada por el navegador es compilado por este.

Es una pequeña capa que te brinda algunos "goodies" tales como 'Helpers', 'shortcuts', 'directives' de las cuales aprenderemos pronto; así como 'layouts' o archivos maestros. 

## Componentes

Vamos a crear una nueva carpeta llamada "Components" bajo 'views'. Este nombre de directorio es importante a propósito. 

Si no estas familiarizado con este término, piensa que es un bloque reutilizable, que será utilizado en varios lugares de tu aplicación: una tarea, un menú, un 'dropdown', un elemento, un archivo de plantilla [layout], una tarjeta, un mensaje, un avatar, etc.

Crearemos un archivo llamado 'layout' en este directorio y eso le indicará a Laravel que lo trate como un componente: layout.blade.php. 

¡No olvides agregar la palabra 'blade' en el nombre del archivo. Muchas personas lo olvidan.

Vamos a copiar todo este código en el archivo 'layout.blade.php':

    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>About Page</title>
    </head>
    <body>
        <nav>
            <a href="/">Home</a>
            <a href="/about">About</a>
            <a href="/contact">Contact</a>
        </nav>
        <h1>Hello from the Home Page.</h1>
    </body>
    </html>

Bien ahora, en nuestro archivo 'home.blade.php' vamos a referenciar el archivo 'layout' que acabamos de editar. Lo haremos como si fuera una etiqueta HTML personalizada:

    <x-layout>
    
    </x-layout>

Así le daremos el nombre del archivo a esa etiqueta, anteponiendo 'x-' para asegurarnos que es único y que no interfiera con existentes etiquetas HTML.

Esto es cool! Si vamos a nuestro navegador y refrescamos, veremos cargarse ese archivo 'layout', lo cuál es grandioso.

Ok, ahora bien tenemos un pequeño problema por aquí en relación a la siguiente línea:

    <h1>Hello from the Home Page.</h1>

Esto no debería estar en una archivo 'layout' ya que se vería reflejado en cualquiera de las vistas donde hagamos referencia a nuestro archivo 'layout'.

Para resolver este inconveniente podríamos copiar esta línea de codigo a nuestra página 'home' así:

    <x-layout>
        <h1>Hello from the Home Page.</h1>
    </x-layout>

Pero al refrescar nuestro navegador no veríamos 'Hello from the Home Page'; y no es porque lo hayamos hecho inapropiadamente, sino que en el archivo 'layout' tenemos que declarar explicitamente en que ranura esta etiqueta '<h1>' debera aparecer.

Para dicho efecto, podemos utilizar la variable '$slot' que siempre va a estar disponible en Laravel para tí. Podemos utilizar esta 'forma larga':

    <body>
        <nav>
            <a href="/">Home</a>
            <a href="/about">About</a>
            <a href="/contact">Contact</a>
        </nav>
        
        <?php echo $slot ?>
    </body>

Al refrescar nuestro navegador, ahora sí veremos 'Hello from the Home page' debajo de nuestro pequeño menú.

Ahora, hemos creado nuestro primer componente para nuestro archivo Layout, o como le llaman algunas nuestro 'master file'. El archivo 'layout' es casi como la 'estructura' de tu aplicación. Es todas las marcas circundantes incluidas en él como el head, el nav, los scripts que deben ser importados, es la estructura general, y después tipicamente tienes una seccion principal que siempre sera unica para cada página.

Así que diseñaremos toda la estructura y después insertaremos las marcas especificas de la pagina en la ranura (slot).

Ahora podremos reutilizar este 'layout' en todas nuestra otras páginas, reemplanzando la palabra home por la de cada una de ellas.

    <x-layout>
        <h1>Hello from the About Page.</h1>
    </x-layout>

    <x-layout>
        <h1>Hello from the Contact Page.</h1>
    </x-layout>

## Your first Blade Helper

Podemos utilizar la siguiente sintaxis en nuestro layout:

    <?php echo $slot ?>

Pero, ya que estamos utilizando Blade podemos utilizar el siguiente helper:

    {{ $slot }}

Al reemplazarlo en nuestro archivo 'layout' y refrescar nuestro navegador functionar, simple y sencillamente porque {{ }} es igual a <?php echo  ?>.

## Resumen

+ Para el día 3 hemos aprendido a crear nuestro primer simple layout de tres páginas. Es básico, pero deberías estar orgulloso de haber aprendido algo nuevo el dia de hoy.
+ También tuviste tu primer introducción a componentes en tu archivo layout, lo cual es super poderoso y muy prominente en la comunidad Laravel.

## Homework

Create a <nav-link> Laravel component.
