## Day 5 : Dandole estilo al enlace de navegación actualmente activo

Hoy nos enfocaremos en estos enlaces de navegación! Necesitamos descubrir como aplicar estilos personalizados basados en cual es la ruta o url seleccionada.

Visualmente noten como el estilo de navegacion activa esta "quemada" en el 'Home' page, aún cuando hagamos clic en otro enlace. Lo vamos a arreglar.

Empecemos en nuestro archivo 'layout.blade.php'. Noten como Tailwind nos da la sugerencia de que debemos configurar la altura a 100% tanto en "<html>" como en "<body>", Así que lo haremos ahora.

    <!--
    This example requires updating your template:

    ```
    <html class="h-full bg-gray-100">
    <body class="h-full">
    ```
    -->

Así que ahora podras ver en tu pagina web, como el fondo es de color gris y cubre el 100% de contenido de la pantalla.

Muy bien ahora iremos adonde estan los enlaces de navegación: 

	<div class="hidden md:block">
                            <div class="ml-10 flex items-baseline space-x-4">
                                <!-- Current: "bg-gray-900 text-white", Default: "text-gray-300 hover:bg-gray-700 hover:text-white" -->
                                <a href="/" class="rounded-md bg-gray-900 px-3 py-2 text-sm font-medium text-white" aria-current="page">Home</a>
                                <a href="/about" class="rounded-md px-3 py-2 text-sm font-medium text-gray-300 hover:bg-gray-700 hover:text-white">About</a>
                                <a href="/contact" class="rounded-md px-3 py-2 text-sm font-medium text-gray-300 hover:bg-gray-700 hover:text-white">Contacts</a>
                            </div>
                        </div>

Y noten como el primero tiene el estilo activo "bg-gray-900". En general, en Tailwind, el nivel 100 es la version mas liviana o transparente y el nivel 900 el mas oscuro. Así que si esta activo, lucira con texto en color blanco y fondo oscuro; de lo contrario, lucira con un fondo un poco mas claro y un texto blanco cuando situemos el punto sobre el.

Así que esto es lo que haremos: correremos una condicion que determinara si la página actual esta o no en la pagina principal "Home", y luego removeremos el resto:

	
	- <a href="/" class="rounded-md bg-gray-900 px-3 py-2 text-sm font-medium text-white" aria-current="page">Home</a>
	+ <a href="/" class="{{ false ? 'rounded-md bg-gray-900 px-3 py-2 text-sm font-medium text-white' : 'rounded-md px-3 py-2 text-sm font-medium text-gray-300 hover:bg-gray-700 hover:text-white'}}" aria-current="page">Home</a>


Ahora, no va a pasar nada hasta que cambienmos el condicional de 'True' a 'False'.

    <a href="/" class="{{ false ? 'rounded-md bg-gray-900 px-3 py-2 text-sm font-medium text-white' : 'rounded-md px-3 py-2 text-sm font-medium text-gray-300 hover:bg-gray-700 hover:text-white'}}" aria-current="page">Home</a>

Muy bien! Ahora lo que nos falta es sustituir la condición 'false' con un método real de llamada para que cambie. Laravel incluye fuera de la caja una función 'request Helper'. Usted puede llamarla para tomar información acerca del pedido actual.

Ahora, uno de los metodos en el objeto se llama 'is' y nos permite pasar una expresion RegEx, un patrón que determinara si la pagina actual es igual al patrón.

	<a href="/" class="{{ request()->is('/') ? 'rounded-md bg-gray-900 px-3 py-2 text-sm font-medium text-white' : 'rounded-md px-3 py-2 text-sm font-medium text-gray-300 hover:bg-gray-700 hover:text-white'}}" aria-current="page">Home</a>
                                <a href="/about" class="rounded-md px-3 py-2 text-sm font-medium text-gray-300 hover:bg-gray-700 hover:text-white">About</a>
                                <a href="/contact" class="rounded-md px-3 py-2 text-sm font-medium text-gray-300 hover:bg-gray-700 hover:text-white">Contacts</a>

y Funciona! Asi que ahora vamos a replicarlo en los demas enlaces:

	
	<a href="/" class="{{ request()->is('/') ? 'rounded-md bg-gray-900 px-3 py-2 text-sm font-medium text-white' : 'rounded-md px-3 py-2 text-sm font-medium text-gray-300 hover:bg-gray-700 hover:text-white'}}">Home</a>
                                <a href="/about" class="{{ request()->is('about') ? 'rounded-md bg-gray-900 px-3 py-2 text-sm font-medium text-white' : 'rounded-md px-3 py-2 text-sm font-medium text-gray-300 hover:bg-gray-700 hover:text-white'}} rounded-md px3 py-2 text-sm font-medium">About</a>
                                <a href="/contact" class="{{ request()->is('contact') ? 'rounded-md bg-gray-900 px-3 py-2 text-sm font-medium text-white' : 'rounded-md px-3 py-2 text-sm font-medium text-gray-300 hover:bg-gray-700 hover:text-white'}} rounded-md px3 py-2 text-sm font-medium">Contacts</a>

Parece que a este punto, todo esta funcionando bien. Recuerden que un par de días atrás les dije que los enlaces, en la vida real, se podían poner un poco complicados a medida que vamos modificandolo y poniendo estas condicionales.


Por que no, entonces, reintroducimos un componente de navegacion y vemos como luce. Vayamos a componentes y creemos un nuevo componente llamado 'nav-link.blade.php'.

Agregamos esta línea de código:

	<a href="/" class="{{ request()->is('/') ? 'rounded-md bg-gray-900 px-3 py-2 text-sm font-medium text-white' : 'rounded-md px-3 py-2 text-sm font-medium text-gray-300 hover:bg-gray-700 hover:text-white'}}">Home</a>

Como discutimos la vez pasada, no queremos que este con elementos 'quemados'

Nuestros enlaces en el 'layout' luciran de esta manera:

	<x-nav-link href="/">Home</x-nav-link>
                                <x-nav-link href="/about">About</x-nav-link>
                                <x-nav-link href="/contact">Contacts</x-nav-link>


Ahora bien editemos nuestro componente de navegacion y modifiquemos esta parte del 'aria-current'. Si estas contruyento una app en produccion y deseas ser accesible como sea posible esto es para escritores de pantalla y es una forma de indicar si el actual enlace representa la pagina actual en una lista de paginas. Si en lugar de esto lo cambiamos a 'false', eso significa que no es la pagina actual.

    - <a class="{{ request()->is('/') ? 'rounded-md bg-gray-900 px-3 py-2 text-sm font-medium text-white' : 'rounded-md px-3 py-2 text-sm font-medium text-gray-300 hover:bg-gray-700 hover:text-white'}}" aria-current="page">Home</a>
    + <a class="{{ request()->is('/') ? 'rounded-md bg-gray-900 px-3 py-2 text-sm font-medium text-white' : 'rounded-md px-3 py-2 text-sm font-medium text-gray-300 hover:bg-gray-700 hover:text-white'}}" aria-current="false ">Home</a>



Pero, también podemos configurarlo de la siguiente manera: 

	<a class="{{ request()->is('/') ? 'rounded-md bg-gray-900 px-3 py-2 text-sm font-medium text-white' : 'rounded-md px-3 py-2 text-sm font-medium text-gray-300 hover:bg-gray-700 hover:text-white'}}" aria-current="{{ request()->is('/') ? 'page' : 'false'}}">Home</a>

Ahora vamos a dinamizar lo que va en medio de la etiqueta de ancla '<a>' utilizando nuestra variable '$slot':

	<a class="{{ request()->is('/') ? 'rounded-md bg-gray-900 px-3 py-2 text-sm font-medium text-white' : 'rounded-md px-3 py-2 text-sm font-medium text-gray-300 hover:bg-gray-700 hover:text-white'}}" aria-current="{{ request()->is('/') ? 'page' : 'false'}}">{{ $slot }}</a>

Muy bien, ahora podemos utilizar un 'prop' que indica si este enlace de navegación debería ser marcado como el enlace activo.

En los componentes blade escucharas acerca de los atributos y los 'props', asi que permite aclararte un poco acerca de ello.

Los 'attributes' representan atributos HTML: tales como href, id, class, etc. 

 
Un 'prop' sería cualquier cosa que no sea un atributo. Basicamente los distinguiremos, porque debes saber bien si ese 'prop' sera incluido como uno de los atributos que haremos 'echo' como parte de la etiqueta ancla 'a' o no. Así que si tienes un 'prop' llamado activo y haces 'echo' como parte de los atributos, ahora tienes una etiqueta ancla 'a' con un nombre de atributo 'active' y eso no tiene sentido. Por eso tenemos que distinquir entre estos dos y aquí tenemos como lo haremos:

En la parte superior de mi componente blade usaré una directiva Blade. Reconoceras una directiva blade porque ellas empiezan con un símbolo '@' y note como nuestro edito autocompleta todas las opciones disponibles aquí y hay infinidad de ellas.

En nuestro caso, utilizaremos una llamada '@props()', así que podemos declarar nuestros 'props' como un arreglo. y hemos decidido que usaremos uno llamado 'active'. Ok! Dejame mostrarte como funciona!

	@props(['active'])

    <a class="{{ request()->is('/') ? 'rounded-md bg-gray-900 px-3 py-2 text-sm font-medium text-white' : 'rounded-md px-3 py-2 text-sm font-medium text-gray-300 hover:bg-gray-700 hover:text-white'}}" aria-current="{{ request()->is('/') ? 'page' : 'false'}}"
    {{ $attributes }}
    >{{ $slot }}</a>

Ahora bien, como lo hemos definido como un 'prop' no se podra ver el contenido de ese atritubo con la variable '$attributes'. Por lo tanto, debemos configurar o definir nuestra variable 'active':

	@props(['active' => false])

    <a class="{{ $active ? 'rounded-md bg-gray-900 px-3 py-2 text-sm font-medium text-white' : 'rounded-md px-3 py-2 text-sm font-medium text-gray-300 hover:bg-gray-700 hover:text-white'}}" aria-current="{{ request()->is('/') ? 'active' : 'false'}}"
{{ $attributes }}
>{{ $slot }}</a>

Ahora bien, asi como esta, cualquier valor que este en el prop 'active' sera tomado como falso porque se leera como un string.

	<x-nav-link href="/">Home</x-nav-link>
                                <x-nav-link href="/about" active="foobar">About</x-nav-link>
                                <x-nav-link href="/contact">Contacts</x-nav-link>


Para evitarlo y hacerle saber al compilador que debe leer el contenido como una expresión en lugar de una cadena, debemos anteponer dos puntos antes del nombre del 'prop'


	 <x-nav-link href="/">Home</x-nav-link>
                                <x-nav-link href="/about" :active="false">About</x-nav-link>
                                <x-nav-link href="/contact">Contacts</x-nav-link>

Bien ahora que ya podemos proveer una expresion, podemos regresar a lo que originalmente tenia. 

    <x-nav-link href="/" :active="request()->is('/')">Home</x-nav-link>
                                <x-nav-link href="/about" :active="request()->is('about')">About</x-nav-link>
                                <x-nav-link href="/contact" :active="request()->is('contact')">Contacts</x-nav-link>


Excelente! ahora tenemos un componente dedicado blade. Hemos aprendido acerca de los atributos, hemos aprendido acerca de los 'props'. Recuerda que tu puedes hacer cosas como estas, donde puedes declarar una directiva PHP ('@php') y podrias hacer un '@endphp' para crear nuestro bloque efectivamente y entonces adentro de esto podrias tener algun tipo de codigo. podria ser una condicion, inspeccionar el valor de un activo, etc.

## HOMEWORK

Continuemos con este idea del componente. Me gustaria que introdujeras un nuevo 'prop'. Llamaremos a este prop 'type' y  este indicara si el enlace de navegacion deberia ser presentado como una etiqueta ancla 'a' o una etiqueta 'button'