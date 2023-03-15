# CVDS_LAB05
## MVC PRIMEFACES INTRODUCTION
## ***Integrantes:***
- Erika Juliana Castro Romero
- Mariana Pulido Moreno
## **PARTE I. - JUGANDO A SER UN CLIENTE HTTP**
1. Abra una terminal Linux o consola de comandos Windows.
2. Realice una conexión síncrona TCP/IP a través de Telnet al siguiente servidor:
* Host: www.escuelaing.edu.co
* Puerto: 80
Teniendo en cuenta los parámetros del comando telnet:
```
  telnet HOST PORT 
```
3. Antes de que el servidor cierre la conexión por falta de comunicación:
* Revise la página 36 del RFC del protocolo HTTP, sobre cómo realizar una petición GET. Con esto, solicite al servidor el recurso ‘sssss/abc.html’,
usando la versión 1.0 de HTTP.
* Asegúrese de presionar ENTER dos veces después de ingresar el comando.
* Revise el resultado obtenido. ¿Qué codigo de error sale?, revise el significado del mismo en la lista de códigos de estado HTTP.
¿Qué otros códigos de error existen?, ¿En qué caso se manejarán?
4. Realice una nueva conexión con telnet, esta vez a:
* Host: www.httpbin.org
* Puerto: 80
* Versión HTTP: 1.1
Ahora, solicite (GET) el recurso /html. ¿Qué se obtiene como resultado? 

¡Muy bien!, ¡Acaba de usar del protocolo HTTP sin un navegador Web!. Cada vez que se usa un navegador, éste se conecta a un servidor HTTP, envía peticiones
(del protocolo HTTP), espera el resultado de las mismas, y -si se trata de contenido HTML- lo interpreta y dibuja.

5. Seleccione el contenido HTML de la respuesta y copielo al cortapapeles CTRL-SHIFT-C. Ejecute el comando wc (word count) para contar palabras con la
opción -c para contar el número de caracteres:
```
  wc -c
```
Pegue el contenido del portapapeles con CTRL-SHIFT-V y presione CTRL-D (fin de archivo de Linux). Si no termina el comando wc presione CTRL-D de nuevo. No presione mas de dos veces CTRL-D indica que se termino la entrada y puede cerrarle la terminal. Debe salir el resultado de la cantidad decaracteres que tiene el contenido HTML que respondió el servidor.

Claro está, las peticiones GET son insuficientes en muchos casos. Investigue: ¿Cuál es la diferencia entre los verbos GET y POST? ¿Qué otros tipos de
peticiones existen?

6. En la practica no se utiliza telnet para hacer peticiones a sitios web sino el comando curl con ayuda de la linea de comandos:
```
  curl www.httpbin.org
```
Utilice ahora el parámetro -v y con el parámetro -i:
```
  curl -v www.httpbin.org
  curl -i www.httpbin.org
```
¿Cuáles son las diferencias con los diferentes parámetros?

## **PARTE II. - HACIENDO UNA APLICACIÓN WEB DINÁMICA A BAJO NIVEL.**
En este ejercicio, va a implementar una aplicación Web muy básica, haciendo uso de los elementos de más bajo nivel de Java-EE (Enterprise Edition), con el fin de revisar los conceptos del protocolo HTTP. En este caso, se trata de un módulo de consulta de clientes Web que hace uso de una librería de acceso a datos disponible en un repositorio Maven local.

I. Para esto, cree un proyecto maven nuevo usando el arquetipo de aplicación Web estándar maven-archetype-webapp
```
  mvn archetype:generate -DarchetypeGroupId=org.apache.maven.archetypes -DarchetypeArtifactId=maven-archetype-webapp -      DarchetypeVersion=1.4
```
1. Revise la clase SampleServlet incluida a continuacion, e identifique qué hace:

**SERVLET** --> Estos pueden dar soporte al contenido dinámico de paginas web o lo que podria ser acceder a una base de datos , dando asi servicio a varios clientes al mismi tiempo y filtrar datos.

Referencia de : https://www.ibm.com/docs/es/was-nd/9.0.5?topic=applications-servlets

2. Revise qué valor tiene el parámetro ‘urlPatterns’ de la anotación @WebServlet, pues este indica qué URLs atiende las peticiones el servlet.
```
 "/helloServlet"
```

3. Revise en el pom.xml para qué puerto TCP/IP está configurado el servidor embebido de Tomcat (ver sección de plugins).

El servidor se encuentra configurado para el puerto 8080

4. Compile y ejecute la aplicación en el servidor embebido Tomcat, a través de Maven con:
```
  mvn package
  mvn tomcat7:run
```
![1](https://github.com/MPulidoM/CVDS_LAB05/tree/main/Imagenes/PARTE2.1.PNG)


