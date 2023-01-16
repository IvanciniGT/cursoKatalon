

# Katalon Studio

Herramienta para automatizar pruebas "funcionales".

Tipos de pruebas?


# Tipos de Pruebas de software

- Caja negra / caja blanca


TAXONOMIA 1:

- Estáticas: Las que no requieren poner el código en marcha (no requieren ejecución)
    - Calidad de código < SONARQUBE ... Las pruebas que antes hacía un desarrollador SENIOR >>>> MANTENIMIENTO
        Fallos en la nomenclatura
        Fallos en las convenciones de uso
        Código repetido
    - Definición / Revisión de requisitos !
    - Revisión de un modelo de datos

- Dinámicas: Las que requieren poner el código en marcha (ejecutar)
    - Funcionales       Se centran en la funcionalidad / funcionamiento
    - No funcionales    Se centran en otros aspectos:
      - Rendimiento
      - Estres
      - Carga
      - Usabilidad
      - ...

TAXONOMIA 2: Nivel de la prueba

- Unitarias             Revisar un componente de forma AISLADA... En ocasiones necesitamos de MOCKS
                        Mock??? Es un componente que intercepta comunicaciones con otros componentes y 
                                devuelve una respuesta preestablecida > Nos ayuda a aislar el componente.
                        Cuántas queremos? MONTONONES ! Al menos una prueba por componente!
                            Sonarqube nos da una pista guay: Complejidad ciclomática.
                                Complejidad ciclomática? Es el número de caminos que puede tomar un código.
                                Al menos tantas como la complejidad ciclomática del código.
                            COMPONENTE A √
                            COMPONENTE B √
- Integración           Revisan la COMUNICACION entre componentes
                            COMPONENTE A -> COMPONENTE B x -> La comunicación
- End2End (Sistema)     Revisan el COMPORTAMIENTO del sistema en su conjunto. Se comporta el sistema como debe.
- Aceptación            Las que me toca hacer si o si!

                                                    PODRIA 
                                                        OPCION 1: No hacer nada !
si condicion1 entonces:                                 
    tarea1                                              OPCION 2 = tarea1 + tarea2
    si condicion2 entonces:
        tarea2
    sino condicion2 entonces:                           OPCION 3 = tarea1 + tarea3
        tarea3
sino, si condicion3 entonces:
    tarea4                                              OPCION 4 = tarea4 + tarea5
    si condicion4 entonces:
        tarea5                                          OPCION 5 = tarea4 + tarea6
    sino condicion4 entonces:
        tarea6
                                                    COMPLEJIDAD CICLOMATICA DE 5 >>>> Cuántas pruebas al menos debo hacer !

# Pruebas de regresión: 

Cualquier prueba que vuelvo a hacer al tiempo para asegurarme que sigue OK !

Hoy en día "TODAS" las pruebas se convierten en pruebas de regresión !

Por qué? (Lo de arriba no siempre ha sido así... hace 20 años no ocurría)
- Metodologías de desarrollo de software.
  - Hace 20 años se usaban: CASCADA WATERFALL
    Me meto a hacer TODO el desarrollo (8 meses... 2 años)... Y al acabar hago las pruebas ! 1 única vez... o 2(5) si falla la primera.
  - Hoy en día usamos: AGILES (Scrum, Xtreme programming)
    Voy dando a mi cliente el producto de forma incremental! 
    En un plazo de entre 2 semanas y 2 meses le hago un entregable en producción ! > PRUEBAS POR UN TUBO !
                                                                                        Y de las gordas !!!!!!
    Entrega 1 (Sprint 1) Doy el 10% de la funcionalidad: Pantalla de login de la app.
        Que pruebo aquí (1)? El 10% de la funcionalidad

    Entrega 2 (Sprint 1) Doy un 5% adicional de la funcionalidad: Pantalla de login de la app + menu principal
        Que pruebo aquí (2)? El 5% de la funcionalidad nueva
                             + El 10% de la funcionalidad ya entregada (pruebas de regresión)
    En un proyecto voy a acabar entregando 40 veces.... MONTONONES DE VECES TENGO QUE EJECUTAR LAS PRUEBAS !
        Me suele traer cuentas AUTOMATIZARLAS !

# DEV -> OPS

Filosofía / Cultura / conjunto de prácticas en pro de la automatización.

                AUTOMATIZABLES?         HERRAMIENTAS                                                    QUIEN LAS USA
Plan                    x
Code                    x
Build                   √
        JAVA                            maven, gradle, sbt
        JS                              npm, yarn, webpack                                              desarrolladores
        C# .net                         dotnet, msbuild
Test
        Definición      x
        Ejecución       √
            Funcionales                 
                De un código pelao      Frameworks de pruebas unitarias: JUnit, UnitTest, MSTest        desarrollador

                De una interfaz web     Selenium \  Katalon Studio es una interfaz gráfica que usa SELENIUM
                De una app smatphone    Appium    |
                Basadas en el Comportamiento        Cucumber ^
                 BDD                                                                                    testers de automatización
                Rendimiento             JMeter, Loadrunner
                App de escritorio       UFT
                API Web (REST)          Postman, Karate
                API Web (SOAP)          SoapUI
        Donde las hago? 
            En la máquina del desarrollador? Ni de coña !!!!! Están bien maleadas esas máquinas !
            En la máquina del tester       ? Ni de coña !!!!! Están bien maleadas esas máquinas !
            En un entorno de pruebas precreado? Ni de coña! (antes lo haciamos así) Están bien maleadas esas máquinas !
            Hoy en día los entornos de pruebas, que siguen existiendo claramente y es donde hacemos las pruebas
            SON DE USAR Y TIRAR (esa es la tendencia)  ---> Palizón de trabajo.. 
                a no ser que este proceso (de creación y desmantelamiento de entornos) esté AUTOMATIZADO.

                Terraform                                                                               administradores de sistemas
                Vagrant
                Ansible
                Puppet
                Chef
                Salt
                Docker
                Kubernetes
<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<< INTEGRACION CONTINUA ! CI
Release
        Imágenes de contenedores (Docker)
<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<< ENTREGA CONTINUA ! C Delivery 
Deployment
<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<< DESPLIEGUE CONTINUO ! C Deployment
Operation
Monitor

Nos falta por automatizar la llamada ORQUESTADA a todas esas automatizaciones que hemos hecho.
Una automatización que podríamos llamar de SEGUNDO NIVEL: Servidores de AUTOMATIZACIÓN: Servidores de CI/CD

* Jenkins
- Bamboo
- Azure Devops
- Travis CI
- Gitlab CI/CD
- Github actions

La configuración de estas herramientas, que es una tarea que antes no hacíamos (hace 20 años), la hace el perfil DEVOPS !

# Son automatizables las pruebas?

Depende...  Definición de la prueba                 x
            Hacer un programa que realice la prueba x
            Ejecución de la prueba (ese programa)   √

# Qué significa AUTOMATIZAR una prueba? 

Hacer un programa (script secuencia de tareas) que haga la prueba por nosotros.   >>>     Testers > Programadores

# Por qué queremos automatizar las pruebas ? 

Para no hacerlas manualmente. Ahorrar tiempo...y pasta ... realmente ahorramos tiempo frente a ejecutarlas manualmente? 
Depende. De qué? Del número de veces que vaya a necesitar esa prueba!

> Si el tiempo de desarrollo < Tiempo empleado en ejecutar manualmente la prueba TODAS LAS VECES QUE SEA NECESARIO 

Conseguimos una mejora en la calidad del producto, al poder ejecutar "de gratis" las pruebas 
tantas veces como quiera (que suele ser todos los días)

A día de hoy, dentro de los flujos de CI, que los puedo ejecutar cada noche, 
me permito el ejecutar cada noche TODAS LAS PRUEBAS.

# Para qué sirven las pruebas?

x Para verificar que la app es estable y no tiene errores
- Para verificar que un software cumple con unos requerimientos
- Para identificar la mayor cantidad posible de defectos.
- Para si algo no funciona, IDENTIFICAR RAPIDAMENTE QUE ES LO QUE NO FUNCIONA ! Facilitar el debugging

# MUNDO DEL TESTING: ISTQB

Falacia de La ausencia de errores : Es imposible garantizar esto.

# En el mundo del testing hablamos de:

- Errores:      Comportamiento cometido por un ser humano
- Defectos:     Damos lugar a defectos en el código
- Fallos:       Algunos de los defectos pueden dar la cara (manifestarse) en forma de error


# Entornos de trabajo

- Entorno de desarrollo
- Entorno de pruebas / Q&A / testing / pre-producción / Entorno de INTEGRACIÓN !
- Entorno de producción

---

# Pruebas funcionales sobre una interfaz gráfica WEB

## Por qué automatizar las pruebas de interfaz WEB?

Por todo lo anterior...
Y:
- La misma prueba la quiero hacer en varios navegadores.
    Cada vez tengo más garantizado que lo que funciona en un navegador va 
    a funcionar en el resto (o en los más importantes al menos):
    - Casi todos los navegadores se basan en el mismo código CHROMIUM
    - Estándares más rígidos y mejor definidos en el mundo WEB (HTML, CSS, Javascript ES7, EC2019, EC2022)
    - Casi todas las web las acabamos montando con los mismos frameworks, que están bastante probados:
      - ReactJS
      - AngularJS
      - VueJS
      - Bootstrap

    App para una empresa privada interna: Está muy limitado la cantidad de navegadores desde donde la app se ejecuta.
    App web para un ministerio, banco, wallapop, amazon
- Los navegadores , en todas sus versiones se comportan de la misma forma? 
    A lo mejor me interesa hacer la prueba en las últimas n(5) versiones del navegador
- En todos los Sistemas operativos: Android (Kernel linux), Windows, iOS, MacOS, GNU/Linux (Ubuntu, Debian, Fedora)
  - En la última versión de esos SO?
- En distintos dispositivos? tablets, telefonos -> Resoluciones muy especificas y diferentes a las computadoras 

5 x 5 x 5 x 3 x 3 = 125 x 9 ... + de 1000 pruebas XD !!!!!!

Al final esto NO SE HACIA ! Hoy en día si gracias a la AUTOMATIZACION ... y en concreto gracias a SELENIUM !

# Selenium ?

Selenium NO PERMITE HACER PRUEBAS !

Selenium AUTOMATIZA operaciones sobre un navegador de internet!

Tiene 3 herramientas:
- Selenium IDE = RUINA GRANDE !!! NO SE USA PA' NA'
- Selenium Webdriver = GUAY !!!!!!
- Selenium GRID = También es guay, pero para otra cosa.

# Selenium IDE: 

Permite grabar/escribir operaciones que hacemos en un navegador web y ejecutarlas en automático a posteriori.
NO SE USA PARA NADA !

# Selenium Webdriver

Framework para controlar desde programa escritos en :
- Java
- Python
- JS
- C#
- ...
Navegadores de internet, como:
- Edge
- Chrome
- Firefox
- Opera
- ...


Programa Python > Librería Selenium Webdriver   Python  > driver de control de un navegador > navegador
         JAVA                                   JAVA            chrome (para cada versión)      chrome
         C#                                     C#              opera                           opera
         ...                                    ....            edge                            edge

Programa que vamos a montar: SCRIPT
 Paso 1 : Abrir conexión con el driver para controlar un navegador
 Paso 2 : Realizar operaciones en el navegador
                Vete a la página https://miapp.miempresa.com    (1)
                En el formulario de login mete:                 
                    Usuario: fererico                           (2) **
                    Contraseña: Federi02022$
                Pulsa en el menú en el enlace: Buscar
                En el formulario rellena en un campo el valor "MANZANAS"
                Mira el resultado.
                Si salen manzanas, es que la web está funcionando!!!  ***** ESTA OPERACION NO ES DE SELENIUM: LA PRUEBA !
                        Se escribe con un framework de pruebas unitarias. ESTO NO ES SELENIUM 
                    Y saca FOTO !!! 
 Paso 3 : Cerrar conexión con el navegador

El tema es: quién escribe este script?
- Lo puedo escribir yo, si se de (python | java | c# y demás de selenium)
- O lo puede escribir en """automático""" herramientas como KATALON STUDIO o KATALON RECORDER (similar a selenium IDE = kk)
                                                                                Hace poco... PERO LO QUE HACE ES GUAY !!!
KATALON STUDIO lleva dentro una herramienta parecida a SELENIUM IDE, que me permite 
generar """" automaticamente """" estos scripts

Por cierto.... estamos generando un script: PROGRAMA ... Donde lo voy a guardar? En una carpeta en mi disco duro? 
NI DE COÑA !!!!
En un repositorio de un sistema de control de código fuente tipo GIT !!!!


# Y cómo escribo esas instrucciones??? ESTO ES CRITICO 

Lo primero necesito un lenguaje de programación... 
Si uso algo como Katalon, Katalon va a ser quién use el lenguaje de programación y escriba el código.

En resumen, Katalon traduce mis palabras (actos) en código python, JAVA, ... 

PERO DESGRACIADAMENTE NO BASTA CON ESO !
2** Cómo sabe Katalon cuál es la casilla donde debe poner "federico"? 

Identificando el elemento HTML sobre el que quiero hacer una operación determinada !

Y cómo lo identifico? 
- Por sus atributos = RUINA GRANDE !
- Por sus estilos   = IGUAL DE RUINA !
- Por su posición   = RUINOTE !!!!
- Por un identificador que tenga asociado = SUPERGUAY, INMEJORABLE (si es que lo tiene)

Esto nos obliga a tener cierto entendimiento de HTML

# HTML

Lenguaje de marcado de hipertextos, basado en etiquetas. 
Lo define un estándar publicado por la organización: W3C World Wide Web Consortium (Tim Berners Lee)

<html>
    <head>
        <!-- Titulo -->
        <!-- Referenciar las hojas de estilo utilizadas : CSS -->
        <!-- Referenciar los JAVASCRIPT utilizadas : JS -->
    </head>
    <body>
        <!--Contenido que queremos visualizar en la web-->
        <p>Un parrafo</p>
        <img src="ruta"/>
        <ol>
            <li id="item1">Item 1</li>
            <li>Item 2</li>
            <li>Item 3</li>
        </ol>
        <button id="boton_login">
        <table>
        <a>
        <!-- La información acerca de COMO representar estos elementos se detalla en los ficheros: CSS -->
    </body>
</html>

Si los desarrolladores lo han tenido a bien (si son buena gente... y usualmente NO LO SON... quieren putearnos!)
habrán identificado cada elemento mediante un atributo "id".
El estándar HTML obliga a que ciertos elementos lleven un ID... pero solo algunos.
Y cuando el estándar no obliga que hacen los desarrolladores, tiriri !!!!

SI QUEREMOS USAR SELENIUM, DEBEMOS LLEGAR A UN ACUERDO CON EL EQUIPO DE DESARROLLO, 
y tratar de que TODO elemento con el que se pueda interactuar lleve un ID.


Cuando no tengo un ID, lo que tengo es un PROBLEMON ! GORDO !

Si dejo a Katalon intentar buscar una forma creativa de identificar un elemento 
con el que estoy interactuando, la va a encontrar!

Esa forma que Katalon calcula para identificar el elemento en el 90% de los casos NO VALE !
Si dejo eso, a los 3 días ( si me apurais en 2) deja de funcionar el script !


Echad un ojo a W3School > XPATH
