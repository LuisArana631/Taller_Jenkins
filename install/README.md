# **Taller de Jenkins**

![Jenkins](https://img.shields.io/badge/Jenkins-gray?style=flat-square&logo=jenkins)
![Docker](https://img.shields.io/badge/Docker-gray?style=flat-square&logo=docker)
![Angular](https://img.shields.io/badge/Angular-gray?style=flat-square&logo=angular)

## Descripción 

Bienvenidos a este taller de Jenkins, donde encontrarás una guía básica sobre la herramienta de CI/CD Jenkins, información sobre la instalación utilizando Docker y como implementar un pipeline.

## Contenido

- [Instalación de Jenkins](#Instalación-de-Jenkins)


## Instalación de Jenkins

Para instalar Jenkins en un contenedor de Docker necesitaremos ejecutar los comandos en consola:

```
$ docker run -p 8080:8080 -p 50000:50000 -v jenkins_home:/var/jenkins_home jenkins/jenkins:lts-jdk11
```

Lo recomendable es utilizar el dockerfile y construir la imágen para posteriormente crear el contenedor, ya que para las pruebas de angular necesitaremos una instalación de Chrome y con el dockerfile solucionamos el problema, los comandos son:

```
$ docker build -t jenkins-chrome .

# Debes agregar el usuario a grupo de docker con el siguiente comando: sudo usermod -aG docker {user}
# Generalmente se agrega el usuario root como en el ejemplo, pero puedes utilizar otro usuario.

$ docker run -u root -p 8080:8080 -p 50000:50000 -v jenkins_home:/var/jenkins_home -v /var/run/docker.sock:/var/run/docker.sock -d --restart unless-stopped jenkins-chrome:latest
```

Al ejecutar este comando estarás dentro del contenedor y en la consola nos interesará una cosa de toda la salida que se presentó:

```
Jenkins initial setup is required. An admin user has been created and a password generated.
Please use the following password to proceed to installation:

7bbc9c2d83df4548bdc7ad12d8e0c2ef

This may also be found at: /var/jenkins_home/secrets/initialAdminPassword
```

Debemos almacenar la password para poder continuar con la configuración de Jenkins. 

Ahora debemos ingresar a Jenkins desde un navegador colocando ```http://localhost:8080/```. Y nos aparecerá una ventana similar a la siguiente, acá debemos colocar la password que guardamos anteriormente:

![PasswordJenkins](https://www.jenkins.io/doc/book/resources/tutorials/setup-jenkins-02-unlock-jenkins-page.png)

Al ingresar Jenkins nos aparecerán dos botones para seleccionar la instalación de plugins, puede ser por defecto o personalizada, en este caso instalaremos los plugins por defecto.

![CustomizePlugins](https://www.prado.lt/wp-content/uploads/2019/12/Customize_Jenkins.png)

Después de la instalación de los plugins es hora de crear nuestro primer Usuario Admin, para los datos puedes colocar los que desees:

![FirstAccountJenkins](https://www.linuxcloudvps.com/blog/wp-content/uploads/2021/06/jenkins-installation-on-ubuntu-20.04.png)

Para finalizar con la configuración nos aparecerá la pestaña de configuración de la instancia, acá solo seleccionaremos el botón ```Save and Finish```.

![FirstAccountJenkins](https://i.ibb.co/xXwm7Rj/p4.png)

Y listo ya tienes instalado Jenkins en un contenedor de Docker, ahora ya puedes empezar a trabajar con tus pipelines y automatizar varios procesos. 😉