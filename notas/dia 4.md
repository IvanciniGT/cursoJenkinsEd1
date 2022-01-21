En los proyectos Pipeline, lo que hacemos es crear scripts programaticamente.

Tenemos a disposición 2 lenguajes de programación independientes (comparten muchas cosas... otras no)
    - Declarativo       *** Más sencilla y menos potente
    - Scripted          *** Menos sencilla y mucho más potente
    

# SISTEMAS DE CONTROL DE VERSION:
    SVN, CVS: SCM Centralizados
        Servidor central (Donde está el repositorio) > Extraigo ficheros para su edición en máquinas locales
    
    GIT : SCM Distribuido
        En cada máquina, cada persona que trabaja con un proyecto tiene SU PROPIO REPOSITORIO
        
            PERSONA 1                          REPO REMOTO                      PERSONA 2
                repo local         >>           repo                 <<           repo local    
                                   ramas        accesible desde red http(s)
                                                    BITBUCKET
                                                    GITHUB
                                                    GITLAB
                                                    
                                                    
# Creación Proyecto de tipo Pipeline

1º Disponer de un repositorio git o en otro tipo de SCM
    - Opción 1:
        Crear un repo de git local (en nuestro pc):
            git init
        Hemos vinculado nuestro repo local con un remoto que hemos creado en una herramienta tipo gihub, bitbucket, gitlab sin inicializar el repo remoto.
            git remote add <NOMRE-REMOTO> <URL-REPO>
    - Opción 2: <<< Esta es la que usaremos cuando alguien ya haya creado el repo previamente.
        Crear un repo remoto en una herramienta tipo gihub, bitbucket, gitlab. 
            Inicializar este repo remoto: Por ejemplo mediante la creación de un fichero README.md
        Clonar ese repo en nuestro pc
            git clone <URL-REPO>

2º Crear el fichero Jenkinsfile

3º Mandar ese fichero al repo REMOTO
    git add Jenkinsfile
    git commit -m 'envío del Jenkinsfile'
    git push
        ^ Nota: Si el repo lo hemos creado con opción 1, la primera vez me da error y me da un comando alternativo:
            git push -u NOMBRE-REMOTO RAMA

4º Creo un proyecto de tipo PIPELINE en Jenkins
   Le configuro que el archivo Jenkinsfile, lo saque del repo (URL) que hemos creado y donde hemos dejado el fichero Jenkinsfile
  
5º Disfrutar

# Tecnologias importantes que conocer a la hora de usar Jenkins:
    # GIT
    # Programación de la BASH (SH)
    # Docker / Contenedores
    
    
    
Para subir los cambios del fichero alñ repo remoto:
    git add *
    git commit -m 'MENSAJE de confirmación'
    git push
    
    
    git commit -am 'MENSAJE de confirmación' # SOLO SI YA SE HA HECHO UN GIT ADD PREVIO
    git push
    
    
    
# CONTENEDORES - DOCKER

Qué es un contenedor?
Un entorno (lógico) aislado dentro de un SO Linux donde poder ejecutar procesos, procesos que son ejecutados por el SO 
Linux que tengo instalado.

Aislado... en cuanto a qué?
    - Limitación de acceso a hardware
    - Configuración de red propia
    - Sistema de archivos independiente
    - Variables de entorno propias

Un contenedor se crea desde una IMAGEN DE CONTENEDOR.

IMAGEN DE CONTENEDOR > CONTENEDOR 1
                     > CONTENEDOR 2

Las images de contenedor las descargo de un repo de imagenes de contenedor (docker hub)

Qué es una imagen de contenedor?
Un triste fichero ZIP que incluye un programa (o varios) YA INSTALADOS Y PRECONFIGURADOS


Instalar office:
1º Descargar los programas de INSTALACION DE OFFICE
2º Ejecuto ese programa
    Creará carpetas, configuraciones, entradas en el registro de windows...
    
    c:\archivos de programa\office
                                V
                                Fichero ZIP >> Os lo mando por email



docker container create --name mimariadb \
                        -e MARIADB_ROOT_PASSWORD=password \
                        -e MARIADB_DATABASE=prueba \
                        -e MARIADB_USER=usuario \
                        -e MARIADB_PASSWORD=password \
                        mariadb

docker start mimariadb


docker container create --name mipostgres \
                        -e POSTGRES_PASSWORD=password \
                        -e POSTGRES_DB=prueba \
                        -e POSTGRES_USER=usuario \
                        postgres

docker start mipostgres

docker hub



Docker 
    Un contenedor con NGINX: IP 172.17.0.2

Cuantas interfaces de red tiene normalmente un pc?
    loopback: (localhost) 127.0.0.1
    ethernet:             172.31.6.161
    docker                172.17.0.1
        nginx               172.17.0.2
        httpd               172.17.0.3
        sonarqube           172.17.0.4
    
    
    
    