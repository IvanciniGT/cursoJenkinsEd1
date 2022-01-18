Proceso 1: Compilar una app JAVA
    Tener instalado JAVA (Tengo que decir a JENKINS donde están¿?)
    Tener instalado MAVEN
    
    
Jenkins sabe hablar con MAVEN? NO
Jenkins sabe hablar con JAVA?  NO

Plugin de cominucación entre JENKINS y MAVEN

# PROYECTOS DE JENKINS

## CONFIGURACIONES GENERALES DEL PROYECTO:
    nombre, parametros
    
## DISPARADORES (triggers)
    Cuando se debe ejecutar el proyecto.
        Un proyecto siempre lo puedo ejecutar manualmente
    Tipos de triggers:
        Despues de otro proyecto
        Cada noche... Cada cierta periodicidad
        Cuando hay un cambio en el código de una aplicación

## FLUJOS DE TAREAS: 
    
    1- Un flujo de tareas "de trabajo" (las que hacen cosas) que se pueden ejecutar en una máquina 
       gobernada por jenkins
        a. Extrae el codigo de un repositorio de git de una app
        b. Compila el codigo
        c. Instala el codigo en una maquina
    
    
    2- Además del flujo de tareas "normal" o "de trabajo", Jenkins permite definir:
        Un flujo de tareas independiente que se ejecuta después del flujo normal
       PENSADO PARA NOTIFICACIONES Y ACCIONES RESULTANTES
        A1. Manda un email si todo ha ido bien
        A2. Manda un email distinto si todo ha ido mal
        B. Cuando hayas acabado, guarda el resultado de haber compilado
        

TRABAJO: Revisar la calidad del trabajo que están haciendo unos desarrolladores
    PROYECTO 1: Revisar la calidad del ...
    PROYECTO 2: Ejecutar la Revision de la calidad diariamente
        -> Disparador del PROYECTO 1
        
JENKINS -> Cuando ejecuta un proyecto:
    TAREA "N" -> Plugin que prepare un comando que se ejecuta a nivel del SO.
    
Cada ejecución de un proyecto en JENKINS se denomina BUILD
Un BUILD se ejecuta por un EJECUTOR
Un EJECUTOR es un proceso en un MAQUINA GESTIONADA POR JENKINS


PROYECTOS

Proyecto A      >>>> A1.  >>> A2
Proyecto B      >>>> B1 
Proyecto C      >>>> C1.  >>> C2 >>>> C3

Solicitudes de ejecucaciones: COLA (Va por orden)
    
                        Primera que se solicitó
                         V
C3 > A2 > C2 > C1 > B1 > A1.     <<<< Ejecutores
                                        Ejecutor 1    A1....C2..A2......
                                        Ejecutor 2    B1..C1..........C3
                                
                                Esos ejecutores no son sino PROCESOS a nivel de SO
                                Los ejecutores (procesos) se abren en UNA MAQUINA DONDE TENGAMOS UN JENKINS MONTADO
                                
############################################################################################################                                
Ejemplo:
    
    MAESTRO JENKINS                                                         SERVIDOR DE BBDD
    (maquina 1)                                                             (maquina 3)
        AQUI ESTA EL PROYECTO DEFINIDO
        ESTA MAQUINA PUEDE EJECUTAR EL PROYECTO (Esto no lo haría)
        
    WORKER 1 JENKINS
        (maquina 2)
        ESTA MAQUINA PUEDE EJECUTAR EL PROYECTO
            Al ejecutarlo: Abre un cliente de BBDD, que conecte con el servidor de BBDD
                            y ejecute un script de BBDD
    
Proyecto: Crear unas tablas en una BBDD

# QUE ES UN SCM o Sistema de Control de Versión?

Cuando escribimos un programa... ese programa acaba teniendo muchos ficheros, lineas de codigo...
Eso hay que controlarlo:
    - Me interesa controlar las modificaciones. Por qué?
        Para ver que ha cambiado por si hay un problema.
    - Un historial almacenado de todas las versiones por las que que han ido evolucionando mis archivos.
        Dar marcha atrás
    - Que pasa si trabajamos varias personas juntas en el proyecto?
        Algun mecanismo para que o bien, se bloqueen archivos mientras están siendo editados...
        O obien, algo más inteligente: que se fusionen los cambios que hayan hecho personas independientes sobre mis archivos.
    - Los archivos suelen ( y lo hacen con muchisisisma frecuencia ) evolucionar de diferentes formas SIMULTANEAMENTE
    
"Programa" Instalador
                                    Recibo un email... QUE HAN FALLADO TODAS LAS INSTALACIONES
                                     |                  Hay un bug en el programa 
                                     V                  Hay una version nueva de Linux... y el comando ha cambiado
    instalador.sh ............v1............v2......................> TIEMPO
                              V
                            Empiezo a usar esta version 1 para instalar mis maquinas
    Enero     Febrero   Marzo                  
    1       > 2           > 3 **
                            4 **
                            5 **
                            
En los sistemas de control de versión tenemos el concepto de RAMA: Linea temporal paralela 
    en la que mi proyecto evoluciona.
                            
Programa: aplicacion WEB 
          aplicacion Telefono movil
          script que automatice la configuración de un servidor
          script que instale un software
          script que haga unas pruebas automatizadas
          

PROYECTO DE SOFTWARE

RAMA: MAESTRA o "MAIN" < "MASTER", "TRUNK": Sagrada linea temporal:
    En esa rama no se modifica NADA. PROHIBIDO
    Algo que está en main, se presupone que está listo para ejecutarse en producción
    
HOTFIX      ------------------------X-XX-------------------------------------> Tiempo    
                                   /    \
MAIN        ----------------------X------X----------X------------------------> Tiempo    
                                 /                 /
WINDOWS     --------------------X--X--------------/--------------------------> Tiempo
                               /    \            /
DESARROLLO  --X---X-----X-----X--X---X------X---X------------------------------> Tiempo



# MAVEN: Empaquetador, compilador de JAVA
    Requiere un fichero de configuración a nivel de proyecto, llamado pom.xml
 Permite ejecutar tareas:
    clean - borra la carpeta target
    ------
    compile - El programa principal
     V
    test-compile - Compila las pruebas
     V
    test - Ejecuta las pruebas. <<<<<<<<<< Maven genera un fichero .xml con un informe de las pruebas realizadas
            target/surefire-reports
     V
    package - Empaqueta el proyecto
        fichero dentro de la carpeta target con extensión: 
            jar - Si lo que tenemos entre manos es una libreria que podamos usar en otros proyectos
            war - Si lo que tenemos es una aplicación WEB
            ear /