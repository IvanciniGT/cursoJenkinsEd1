UNIX 
    SO Tiempo compartido de uso de CPU
    
    2 CPU 
        El SO puede ejecutar 10 procesos en paralelo
        
        
# Pruebas

## Dinamicas: Poner el software en ejecución para la prueba
    Funcionales
        Unitarias       JUNIT
        Integracion
        Sistema         SELENIUM
        Aceptación
    No funcionales
        Carga       JMETER, LOADRUNNER
        Estres
        HA
        UI          SELENIUM, UFT, APPIUM
        UX

## Estaticas: No requieren poner el software en ejecución para la prueba
    Calidad de código   < SonarQube : leer el codigo escrito por otras personas
    
Instalar SonarQube  mediante un contenedor  

docker run -d -p 8081:9000 --name misonarqube sonarqube:8.9.6-community

mvn sonar:sonar \
    -Dsonar.projectKey=curso1 \
    -Dsonar.host.url=http://172.31.6.161:8081 \
    -Dsonar.login=b59496805c9cd3ceda689ca2ef264ebf30fddf82
    

Jenkins > Plugin mvn       > mvn                     > sonarqube (servidor)

Jenkins > Plugin sonarqube > escaneador de sonarqube > sonarqube (servidor)



Kubernetes es una herramienta que permite gestionar un cluster de maquinas fisicas
Y en esas máquinas montar dinámicamente PODS: Conjunto de contenedores

Jenkins, al configurarle un cloud de kubernetes para trabajar:
    Creara un POD dinamicamente para cada ejecución de cada proyecto.