# GIT

git app desarrollada por Linus Torvalds
    
    Linux < Kernel de SO (basado en la especificación de UNIX)
    GNU
        GNU/Linux < SO completo > Ubuntu, Debian, Redhat...

git es como si fuera un kernel de Sistema de Control de Versión.
A la hora de usar git, necesitamos un servidor remoto que aloje repositorios.
    Github    < Servicio Internet
    Gitlab    < Servicio en Internet pero ademas se puede instalar on premises
    Bitbucket < Servicio en Internet pero ademas se puede instalar on premises

En git, como en todos los sistemas de control de versión, trabajamos con RAMAS (BRANCHES)
Qué branches típicos nos vamos a encontrar?
    - Principal: MAIN, master, trunk.
        El código que hay en esa rama, es el código que PASA A PRODUCCIÓN
    - Desarrollo: develop, development
        El codigo que se está desarrollando en un momento dado
    

# MAVEN

Herramienta para compilar y empaquetar apps "JAVA"
La configuracion de maven se da en un fichero llamado pom.xml > MAVEN
    ¿Cómo se que versión de java es necesaria para una determinada app? En el pom.xml
    ¿Cómo se el tipo de archivo empaquetado que se generará?            En el pom.xml

Cuando use usa maven en un proyecto java:
    - Donde está el código de la app?                En qué carpeta? src/main/
    - Donde está el código de las pruebas de la app? En qué carpeta? src/test/      
            ¿Qué frameworks se utilizan habitualmente para hacer pruebas?
                JUnit < Fue el primero. Sentó un estandar en los informes que se generan.
                TestNG
                UnitTest        ... Todos ellos generan los informes con el formato de JUnit
    - Donde se compila el codigo de la app?                          target/classes
    - Donde se compila el codigo de las pruebas de la app?           target/test-classes
    - Donde se aloja el resultante de empaquetar la app?             target/
        Se podría generar al empaquetar un fichero con una de las siguientes extensiones:
            - jar >  Librerias + Apps para telefonos moviles
            - war \ 
            - ear -  Aplicaciones WEB
    - Al ejecutar las pruebas de la app, se generan una serie de informes.
        Que extension tienen esos informes?                         xml
        Donde se guardan?                                           target/surefire-reports/

A maven le podía pedir distintas tareas: GOALS 
    compile
      ^
    test-compile
      ^
    test
      ^
    package
    clean                                                           Borra la carpeta target




## ejercicio 1. Proyecto JAVA basado en MAVEN

√ Crear un directorio
√ De donde sacamos el proyecto? De un repositorio de git (clonado)
√ Compilar el proyecto > mvn compile
√ Compilar las pruebas del proyecto > mvn test-compile
√ Ejecutar las pruebas del proyecto > mvn test > Informes
√ Empaquetar el proyecto > mvn package         > Fichero JAR (de empaquetado) Este es el que se distribuye / Instala
Poner todo el código en automatico en la rama main
√ Borrado al final
    Por qué quiero borrar?
        Limpiar y que no queden cosas que más adelante me puedan dar problemas
        Liberar espacio
    
    Borrar todo el workspace? 
        INTERESA? Dependerá.
            Ocupa mucho mi proyecto?    No... da igual todo 
                                        Si... sopesar: 
                                                Si descargo mucho y quiero velocidad
                                                O si quiero ahorrar espacio en el servidor de jenkins
            Se compila con mucha frecuencia? Puede no interesarnos clonar todo el rato el repo (cada vez)
                                             Puede interesarme descargar solo los cambios (ocupará mucho menos)
    Borrar no todo el Workspace, pero si la carpeta TARGET < 
        Con la tarea CleanWorkspace, pero eligiendo solo la carpeta target
        mvn clean
        
        Interesa esto?
            Bueno... me aseguro que cada vez tengo una compilación limpia desde 0
            Pero a cambio... cada vez debo compilar todo... y puede tardar mucho.
            Si tengo ya una carpeta target de antemano, maven compila solo lo que ha cambiado
    



Podríamos querer:
    Montar un circuito de Integración Continua:     Que la última versión del codigo que hacen los desarrolladores
                                                    esté continuamente en el entorno de integración 
                                                    sometiendose a pruebas automatizadas.
                                                    
                                                    Cada cuanto se hace este trabajo?   Continuamente
                                                                                        Todas las noches
                                                                                        2 veces al día
        Trabajamos contra la rama desarrollo
        
    Montando un circuito de Entrega continua:       El objetivo es CUANDO ALGO ESTE ACABADO (cada 2,3,5 semanas)
                                                    Coger el codigo que funciona y empaquetarlo para su distribución
        
        Trabajamos contra la rama desarrollo > Pruebas > si todo OK > Main > empaqueto y guardo el resultante
                                                                             Pongo en disposición de quien lo necesite
                                                                             ese resultante
                                                                             Lo guardo en Jenkins / Nexus / Artifactory
        
    Monto un circuito de Despliegue continuo: Instalar en producción lo ultimo que haya en la rama MAIN
                                                o lo ultimo que tenga en un repositorio de artefactos
        
        