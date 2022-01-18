# Qué es JENKINS?

Un orquestador de tareas < Servidor de automatización.

# DEVOPS
    Integración continua: Continuous integration. CI
        Haber conseguido automatizar: EMPAQUETADO/Compilación/Pruebas de una app
            Disponer automatizadamente SIEMPRE de la última versión de una app en el entorno de INTEGRACION
                sometida a pruebas automatizadas
    Entrega continua:     Continuous Delivery.    CD
        Haber conseguido automatizar la generación y distribución del entregable de una app
    Despliegue continuo.  Contoinuous Deployment. CD
        Instalo en producción automativcamente la app

Otro significado de la palabra DEVOPS es un perfil de trabajador IT:
    - Administradores de sistemas
    - Administradores de BBDD
    - Desarrolladores
    - Analistas
    - Testeres Q&A
    - Devops: Alguien que se encarga de configurar herramientas tipo Jenkins

Cultura, filosofía: DE LA AUTOMATIZACION:
    Estandarización < IMPORTANTISIMO
    Programas... que hagan cosas: Tareas que antes se hacían a mano

Tareas Ciclo de vida de una aplicaición:
    Desarrollo... picando código
        Compilarlo/Empaquetarlo/Distribuirlo -> BUILD (Compilación)
            JAVA -> maven/gradle
            JS (NodeJS)  -> npm
            C# -> msbuild
    Pruebas
        Frameworks de pruebas unitarias:
            JUNIT
            TestNG
            TESTUNIT
        SELENIUM: Automatizar pruebas de una app web
        APPIUM: Automatizar pruebas de una app mobile
        JMETER: Pruebas de rendimiento y carga
        SONARQUBE: Pruebas de calidad de código
    Instalación
        Herramientas:
            Ansible/Puppet/Chef: Provisionadores de software/Configuraciones
            Terraform: Adquirir infraestructura de un cloud automaticamente
        Entornos:
            Desarrollo
            Pruebas
            Producción
            Preproducción
    Operarla
    Administrarla

###. Escalabilidad: Capacidad de ajustar la infra(hw/sw) a las necesidades de cada momento

Aplicación Nueva APP 1
    Dia 1:      100 usuarios al dia
    Dia 100:    1000 usuarios al dia
    Dia 500:    10000 usuarios al dia
    Dia 1000:   100000 usuarios al dia

Aplicación Nueva APP 2
    Dia n:      100 usuarios al dia
    Dia n+1:    100000 usuarios al dia.     Black Friday
    Dia n+2:    1000 usuarios al dia
    Dia n+3:    1000000 usuarios al dia.    Ciber Monday

Hoy en día lo que hacemos es alquilar hw por horas... por minutos - Clouds

# CLOUD
    
    Conjunto de servicios (mundo IT) que una empresa ofrece a través de internet.
        Amazon: aws.com
        Microsoft: azure.com
        Google cloud
        IBM cloud

# METODOLOGIAS AGILES: SCRUM, KANBAN, XtremeProgramming
    Antes: Metodogías en cascada (waterfall): V, espiral
        Toma de requisitos <<<< Dia 
            Analisis 
                Desarrollo
                    Pruebas 200 pruebas
                        Documentación  
                            Instalación
            Hito:
                N Tareas ** 
                Fecha > Se movia
    Hoy en día:
        Se basan en el concepto de iteración: Scrum (Sprint)
        Se hace una entrega al cliente (producción) cada 15 dias - 2 meses
            Dia 0  - Comienza trabajo
            Dia 15 - Instalación en producción  5% de la funcionalidad... 100% funcional
            Dia 30 - Instalación en producción 15% de la funcionalidad... 100% funcional
            Dia 45 - Instalación en producción 25% de la funcionalidad... 100% funcional
        Iteraciones:
            N Tareas >> Se cambian de iteración
            Fecha **
        Consecuencias:
            Tengo que instalar cada 2, 3, 4 semanas... en Producción
                Pruebas incrementales:
                    entrega 1: 15 requisitos/pruebas
                    entrega 2: + 10 requisitos... 25 pruebas
                    .... 1000 pruebas
            De donde saco la pasta para esto? 
            Cómo lo resolvemos? -> Automatización
                Revolución / Evolución de perfiles de IT:
                    Testers -> Q&A                  -> Programadores
                    Administradores de sistemas     -> Programadores
                    

# CONTENEDORES. Docker , Kubernetes (Openshift)
    Forma de distribuir e instalar/operar software
    Todos los entornos de producción d todas las emrpesas se están llevando a Kubernetes.
    
    Kubernetes: orquestador de contenedores en cluster
    Una aplicación la vamos a instalar decenas de veces al menos. (METODOLOGIAS AGILES)
    **
    Instalaciones en producción:
        - Escalabilidad
        - Alta disponibilidad: Garantizar un determinado tiempo de disponibilidad de la app:
            90%             10 dias 1 out                       |    €
            99%             100 dias 1 out: 3.5 dias al año     |    €€
            99,9%           1000 dias 1 out: 8 horas al año     |    €€€€
            99,99%          Minutos al año                      V    €€€€€€€
        
    Esto se implementa eprincipalmente mediante el uso de CLUSTERs: 
        Grupo de maquinas/procesos que operan como uno solo

## Herramientas tipo Jenkins:
    TravisCI
    Bamboo
    Teamcity
    AzureDevops
    
Desarrollador (codigo) -> YA ESTA LISTO !
    SCM (git) -> 
        Empaquetar la app ->  maven
            Disponer de un entorno de pruebas -> terraform
                Configurar el entorno de pruebas -> ansible
                    Instalar la app -> ansible
                        Hacerle Pruebas -> selenium + sonarqube....
                            Almacenar el entregable -> nexus, artifactory
                                Disponer del entorno de producción -> terraform
                                    Configurar el entorno de producción -> ansible
                                        Instalar en un entorno de producción -> ansible
                                            SmokeTest -> Pruebas
                                                Revertir la instalación en caso de problemas
        
        JENKINS? Orquestar todas esas tareas / programas
        

Procedimientos de instalación de software:

TRADICIONAL:
    
    App1 | App2 | App3                  Inconvenientes: 
    ------------------                          - Dependencias/Librerias
            SO                                  - Configuraciones
    ------------------                          - Qué pasa si la App1... se vuelve loca (BUG)... 100% CPU
          HIERRO                                        APP1 cruje... no responde...
                                                        APP2 muere... y APP3 tampoco

MAQUINAS VIRTUALES: VIRTUALIZACION
    
     App1  |  App2 + App3
    -------------------                 INCONVENIENTES:
      SO 1 |    SO 2                            - GASTO DE RECURSOS
    -------------------                         - Complica la gestión/mnto/operación
      MV 1 |    MV 2     
    -------------------
        hipervisor          VMWare, Citrix, HyperV, kvm, virtualBOX
    -------------------
            SO
    -------------------
           HIERRO                   
                                    
CONTENEDORES
    
     App1  |  App2 + App3
    -------------------                         - Complica la gestión/mnto/operación
      C 1  |    C 2                     Limitación de acceso al hardware
    -------------------
    ejecutor de contenedores          Docker + Podman + ContainerD + CRIO
    -------------------
          SO Linux 
    -------------------
           HIERRO                   
         
        Un contenedor es un entorno aislado donde se ejecutan procesos (apps) dentro de un SO Linux.
        Los contenedores responden a un estandar:
            Todos los contenedores se distribuyen, operan y configuran de la misma forma**
                y son ejecutables por cualquier ejecutor de contenedores.
            
            ** Da igual si quiero instalar/operar/configurar:
                Oracle DB
                Servidor de Web APACHE
                Aplicación custom de mi empresa
             Todo se hace de la misma manera
             

# JENKINS:

App web desarrollada en JAVA + Servidor WEB (que sepa comunicarse con JAVA)
Java es un lenguaje de programación pero un poquito peculiar.

## Clasificar los lenguajes de programación:

### Lenguajes compilados / interpretados

#### Compilación. Depende del kernel de SO destino
    .cobol -> Binario ejecutable
    .c     -> Binario ejecutable
#### Interpretación
    .sh    -> Interpretados (sh)
    .py    -> Interpretados (python, python3)

JAVA: Compilado + Interpretado
    .java   -> javac -> Compilan: .class (Byte-code) -> java (JVM) = Interpreta

Servidores WEB que sepan de JAVA: Servidores de aplciaciones JAVA
    JBoss
    Weblogic
    Websphere
    Tomcat
    
Entorno distribuido
    Varias instalaciones de un aherramienta, 
        donde cada una de las instalaciones hace una tarea independiente y diferente del resto
    Maestro de Jenkins - Mayordomo
        Workers - Curritos - Agente de jenkins (ssh > UNIX)
Cluster
    Varias instalaciones haciendo lo mismo - Replicias
    

Linus Torwalds -> Linus' Unix ->  Necesitaba un SCM Bueno para montar Linux
    Empezó usando CVS -> git 
        (Cuando no tengamos claro como hacer algo en git, 
        solo hay que mirar a como se hace en CVS y hacer lo contrario)
    
    Github < Microsoft (solo como servicio web)
    GitLab (Tener on premisses)
    BitBucket (Attlasian, JIRA)
    
    
    MySQL > MariaDB
    OpenOffice (sun) -> LibreOffice
    Hudson -> Jenkins ... Opensource (Que puedo ver el código) + Freeware
                CloudBees

ARQUITECTURA DISTRIBUIDA TRADICIONAL DE JENKINS
    
    Maquina donde tenemos instalado JENKINS:
        Definimos tareas:
            - Tarea 1 - Compilar y probar una app JAVA
            - Tarea 2 - Compilar y probar una app C#
            - Tarea 3 - Compilar y probar una app PYTHON
    
    Maquina preparada para hacer compilaciones y pruebas en JAVA (Instalado un agente de jenkins)
        Ejecutar la tarea 1: Compilar y probar una app JAVA
            Que voy a necesitar alá donde vaya a ejecutar la tarea? JAVA + maven + librerias adicionales
        
    Maquina independiente preparada para hacer compilaciones y pruebas en PYTHON  (Instalado un agente de jenkins)
        Ejecutar la tarea 3: Compilar y probar una app PYTHON
            Que voy a necesitar alá donde vaya a ejecutar la tarea? PYTHON v2 v3 + librerias adicionales
        
ARQUITECTURA DISTRIBUIDA NUEVA Y MAS UTILIZADA DE JENKINS
    
    Maquina donde tenemos instalado JENKINS:
        Definimos tareas:
            - Tarea 1 - Compilar y probar una app JAVA
            - Tarea 2 - Compilar y probar una app C#
            - Tarea 3 - Compilar y probar una app PYTHON   
            
    Clouds:
        Cluster de Kubernetes: Donde El maestro de Jenkins irá solicitando que se generen contenedores
            para ejecutar tareas... que luego son eliminados
        Clous AWS: Donde Jenkins solicitará a Amazon que cree MVs o Contenedores donde ejecutar tareas...
            que luego son eliminados
        Aqui también existe el concepto de AGENTE... pero son CADUCOS... se elimina después de su utilización.
        SON DE UN SOLO USO