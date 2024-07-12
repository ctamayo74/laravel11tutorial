s## Day 4 : Make a pretty layout using Tailwind CSS

Para empezar vamos a completar la tarea del día 3. Recuerda que te pedimos extraer uno de estos enlaces de navegación a su propio componente dedicado:

    <nav>
        <a href="/">Home</a>
        <a href="/about">About</a>
        <a href="/contact">Contact</a>
    </nav>

Hagamos eso juntos. En nuestro directorio 'Components', creamos el archivo 'nav-link.blade.php. Tomemos esta línea de código y lo pegamos en nuestro nuevo archivo:

    <a href="/">Home</a>

y esa linea la reemplazamos por:

    <x-nav-link></x-nav-link>

en nuestro archivo 'layout.blade.php'.

Ahora bien, esto funcionará; pero necesitamos que sea más dinámico, para que pueda ser utilizado por cualquier elemento del enlace de navegación.

Entonces, utilizaremos nuestra técnica del '$slot' aquí:

    <a href="/"> {{ $slot }}</a>

Sin embargo, al refrescar notarás que el cualquiera de los enlaces nos llevan al mismo directorio raíz.

    <nav>
        <x-nav-link>Home</x-nav-link>
        <x-nav-link>About</x-nav-link>
        <x-nav-link>Contact</x-nav-link>
    </nav>

 Entonces que tendremos que modificar nuestro layout una vez mas. Parece que tendremos que pasar un "href=" como normalmente hacemos. 

    <nav>
        <x-nav-link href="/">Home</x-nav-link>
        <x-nav-link href="/about">About</x-nav-link>
        <x-nav-link href="/contact">Contact</x-nav-link>
    </nav>

Pero entonces en nuestro 'nav-link', cómo lo accesaremos?

Bueno, todos los componentes blade de Laravel tienen acceso al objeto "atributes", y este objeto contendrá los detalles de todos los atributos que le pases tales como "href", "id", "class", cualquiera de estos.

Así que si volvemos a nuestro componente, podemos 'php echo' dicho objeto:

    <a {{ $attributes }}> {{ $slot }}</a>

y eso encadenará apropiadamente. Pero, recuerda que '$attributes' es un objeto así que hay mas "bombos y platillos" de los que ves inicialmente aquí. Pero mantegamoslo simple por hoy.

Bien, ahora si refrescamos nuestro navegador veremos que los enlaces si nos llevan a la página 'contact' o 'about' o 'home.

Muy bien, solo recuerda que si agregas otros atributos tales como 'style' eso tambien se desplegará:

    <nav>
        <x-nav-link href="/">Home</x-nav-link>
        <x-nav-link href="/about" style="color: green">About</x-nav-link>
        <x-nav-link href="/contact">Contact</x-nav-link>
    </nav>

Excelente! Estos nos ayudara en el futuro a aislar algunas caracteristicas que podrian complicar un poco el menu de navegacion, así guárdalo en tu bolsa.

## Tailwind CSS

Este no es un pre-requisito de este curso. Pero Tailwind nos ayudará a hacer las cosas un poco mas fáciles en términos de CSS. ¿Qué es Tailwind CSS? Tailwind es una marco de trabajo utilitario de CSS.

Y por utilitario, entendemos que podemos declarar clases que nos refieren a propiedades especificas de CSS efectivamente. Por ejemplo, podría haber una clase llamada 'text-red-500' y eso literalmente se refiere a configurar el color a ese tipo de rojo. 

Podría haber otra nombre de clase 'mr-2'y eso se traduce "a configurar el margen derecho al nivel 2".

Así que es fácil de aprender pero no es un pre-requisito.

Ahora bien, una cosa que realmente me gusta de Tailwind es 'companion Tailwind ui.com'. Esta es una herramienta de paga pero ellos ofrecen componentes de ejemplo gratis y esos serán justamente los que utilizaremos para esta seria.

Si navegamos a https://tailwindui.com/ y hacemos clic en "Browse components", y nos desplazamos a "Application UI", notarás que ellos tienen ejemplos de 'sidebars' y 'multicolumn layouts' y 'headings'; componentes que nos permitirán formar el andamiaje de cualquier aplicación nueva en la que estes trabajando.

Ok, hagamos clic en 'Stacked layouts' y copiemos el primer ejemplo, el cual es gratuito haciendo clic en el botón de 'copiar'. Y en nuestro archivo 'layout.blade.php' en medio de la etiqueta 'body' pegaremos el código que copiamos.

Es una gran pieza de HTML, que no copiare aquí! Iremos a lo que es importante y borraremos mucho de lo que esta ahí y no necesitamos.

Al refrescar el navegador, nos daremos cuenta que hemos incorporado todas esas clases de Tailwind; pero aún no hemos incorporado el framework de Tailwind CSS. Así que, puedes adjuntar esto a la herramienta de construcción que mejor te parezca, si sabes lo que eso es; pero, mientras estemos en la 'fase de juego' lo vamos a referenciar en un CDN:

    <script src="https://cdn.tailwindcss.com"></script>

Y voila! Al refrescar el navegador lo verás funcionando. Cool!

Ahora tomaremos un par de minutos para borrar todo lo que no vamos a necesitar: 

    + dropdown menu
    + mobile styling
    + en el menu solo necesitamos 3 enlaces (links): "Home, About y Contact" y reemplazaremos los href
    + php echo $slot
    + change dynamically the heading 

Ahora bien, esa variable $heading no ha sido declarada por lo tanto recibiremos un mensaje de error, lo cual es un comportamiento esperado. ¿Cómo la declaramos?

La podemos declarar como un 'prop' en nuestro archivo 'home.blade.php'. Un prop es como un atributo personalizado:

    <x-layout heading="">
        <h1>Hello from the Home Page.</h1>
    </x-layout>

o, podemos declarar un slot nombrado. Recuerda que los slots son áreas donde pegamos contenido; así que podemos tener slots en diferentes áreas de nuestra página. Por eso, necesitamos nombrarlos, para poder distinguirlos: Dashboard slot, main slot, footer slot, etc.

    <x-layout>
        <x-slot:heading>
            Home Page
        </x-slot:heading>
        <h1>Hello from the Home Page.</h1>
    </x-layout>

Y replicamos ese slot named en About and Contact page. Ahora bien podriamos modificar las imágenes del usuario y de la empresa, para lo cual buscariamos las etiquetas de imágenes para editarlas.

## Homework

Ahora bien, habrás notado que cada vez que haces clic ya sea en 'About' o 'Contact' menu, 'Home' se queda seleccionado. Tendremos que encontrar la manera condicional de crear layouts o aplicar Styling basado en cuál es la URL actual, o cuál es la ruta actual. Aprenderemos a hacer eso en el día 5. Así que no tendremos tarea el día de hoy. Nos vemos luego! Bye!