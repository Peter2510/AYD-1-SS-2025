
# CI/CD con Jenkins y GitHub

Guía breve para entender qué es **CI/CD**, por qué utilizar **Jenkins**, y cómo integrarlo con **GitHub** para automatizar compilaciones, pruebas y despliegues.

## ¿Qué es CI/CD?

**Integración Continua (CI)** y **Entrega/Despliegue Continuo (CD)** son prácticas que automatizan el ciclo de vida del software:

-   **CI:** cada cambio de código se integra frecuentemente, se valida con pruebas y análisis de calidad de forma automática.
    
-   **CD:** los cambios validados se empaquetan y se entregan a entornos (Desarrollo, Staging, Producción) de manera confiable y repetible, con o sin aprobación manual.
    

**Idea clave:** entregar valor más rápido y con menos riesgo mediante automatización, retroalimentación temprana y procesos reproducibles.

## Beneficios

-   **Velocidad:** ciclos de entrega más cortos.
    
-   **Calidad:** reducción de errores gracias a pruebas y análisis automatizados.
    
-   **Trazabilidad:** claridad sobre qué versión llegó a qué entorno.
    
-   **Repetibilidad:** procesos definidos como configuración, no como tareas manuales.
    
-   **Confianza:** despliegues previsibles y reversibles.
    

----------

## Jenkins

**Jenkins** es un servidor de automatización **open source** para CI/CD:

-   Define procesos de construcción, pruebas, empaquetado y despliegue.
    
-   Arquitectura **Controller + Agents** (máquinas o contenedores que ejecutan trabajos).
    
-   Gran ecosistema de **plugins** para SCM, artefactos, análisis, seguridad y despliegue.
    
-   Soporta **multibranch/organization** para descubrir repos, ramas y Pull Requests automáticamente.
    
-   Se integra con herramientas de notificación, calidad, contenedores y orquestadores.


## Patrones de integración con GitHub

-   **Webhook clásico:** GitHub notifica a Jenkins ante eventos (push, pull request). Sencillo y directo.
    
-   **GitHub Branch Source (Multibranch/Org Folder):** Jenkins descubre repos, ramas y PRs; crea trabajos automáticamente y reporta estados en GitHub.
    
-   **Autenticación con GitHub App o Token Personal (PAT):** acceso seguro para clonar repos, crear webhooks y publicar estados de build.
    

> Para la mayoría de equipos, **Multibranch + Webhook** cubre la integración de forma robusta y escalable.

## Glosario

-   **Pipeline:** flujo automatizado de construcción, pruebas y despliegue.
    
-   **Agent:** recurso (máquina/contenedor) que ejecuta trabajos de CI/CD.
    
-   **Multibranch:** configuración que crea trabajos por cada rama y PR de un repo.
    
-   **Webhook:** notificación HTTP que GitHub envía ante eventos del repositorio.   

# Ejemplo práctico

# Configuracion Swap

sudo fallocate -l 3G /swapfile

sudo chmod 600 /swapfile

sudo mkswap /swapfile

sudo swapon /swapfile

swapon --show


# Instalaciones necesarias

    https://docs.docker.com/engine/install/ubuntu/

## Configuración EC2

    sudo nano /etc/apt/sources.list

deb [http://archive.ubuntu.com/ubuntu/](http://archive.ubuntu.com/ubuntu/) noble main restricted universe multiverse deb [http://archive.ubuntu.com/ubuntu/](http://archive.ubuntu.com/ubuntu/) noble-updates main restricted universe multiverse deb [http://archive.ubuntu.com/ubuntu/](http://archive.ubuntu.com/ubuntu/) noble-backports main restricted universe multiverse

    sudo apt update

## Configuración de Jenkins
Dockerfile

    #alpine
    FROM jenkins/jenkins:lts-alpine
    
    #usuario root 
    USER root
    
    #OpenJDK 21, Maven y Docker CLI
    RUN apk update && \
        apk add --no-cache openjdk21 maven docker-cli docker-compose
    
    RUN apk add --no-cache sudo
    
    RUN echo "jenkins ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers
    
    #entorno para OpenJDK 21
    ENV JAVA_HOME=/usr/lib/jvm/java-21-openjdk
    ENV MAVEN_HOME=/usr/share/maven
    ENV PATH="$JAVA_HOME/bin:$MAVEN_HOME/bin:$PATH"
    
    #usuario Jenkins
    USER jenkins
    
    #puerto 8080 de Jenkins
    EXPOSE 8080
    
    #comando de entrada por defecto para Jenkins
    ENTRYPOINT ["/sbin/tini", "--", "/usr/local/bin/jenkins.sh"]

docker-compose.yml

    services:
      jenkins:
        build:
          context: .
          dockerfile: Dockerfile
        ports:
          - "8080:8080"
        volumes:
          - jenkins_home:/var/jenkins_home
          - /var/run/docker.sock:/var/run/docker.sock  #montando el socket de Docker
    
    volumes:
      jenkins_home:
  

