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
![1](https://github.com/MPulidoM/CVDS_LAB05/blob/main/Imagenes/PARTE2.1.PNG)
![2](https://github.com/MPulidoM/CVDS_LAB05/blob/main/Imagenes/PARTE2.2.PNG)

5. Abra un navegador, y en la barra de direcciones ponga la URL con la cual se le enviarán peticiones al ‘SampleServlet’. Tenga en cuenta que la URL tendrá
como host ‘localhost’, como puerto, el configurado en el pom.xml y el path debe ser el del Servlet. Debería obtener un mensaje de saludo.

![3](https://github.com/MPulidoM/CVDS_LAB05/blob/main/Imagenes/PARTE2.3.PNG)

6. Observe que el Servlet ‘SampleServlet’ acepta peticiones GET, y opcionalmente, lee el parámetro ‘name’. Ingrese la misma URL, pero ahora agregandoun parámetro GET (si no sabe como hacerlo, revise la documentación en http://www.w3schools.com/tags/ref_httpmethods.asp).

![4](https://github.com/MPulidoM/CVDS_LAB05/blob/main/Imagenes/PARTE2.4.PNG)

7. Busque el artefacto gson en el repositorio de maven y agregue la dependencia.

```
  <!-- https://mvnrepository.com/artifact/com.google.code.gson/gson -->
<dependency>
 <groupId>com.google.code.gson</groupId>
 <artifactId>gson</artifactId>
 <version>2.3.1</version>
</dependency>
```
8. En el navegador revise la dirección https://jsonplaceholder.typicode.com/todos/1. Intente cambiando diferentes números al final del path de la url.

* numero = 1
![5](https://github.com/MPulidoM/CVDS_LAB05/blob/main/Imagenes/PARTE2.5.PNG)
* numero = 2
![6](https://github.com/MPulidoM/CVDS_LAB05/blob/main/Imagenes/PARTE2.6.PNG)
* numero = 23
![7](https://github.com/MPulidoM/CVDS_LAB05/blob/main/Imagenes/PARTE2.7.PNG)

9. Basado en la respuesta que le da el servicio del punto anterior, cree la clase edu.eci.cvds.servlet.model.Todo con un constructor vacío y los métodos getter y setter para las propiedades de los "To Dos" que se encuentran en la url indicada.

```
 Se encuentra en  edu.eci.servlet.model.Todo
```
 10. Cree una clase que herede de la clase HttpServlet (similar a SampleServlet), y para la misma sobrescriba el método heredado doGet. Incluya la anotación @Override para verificar –en tiempo de compilación- que efectivamente se esté sobreescribiendo un método de las superclases.
 
```
 Se encuentra en  edu.eci.servlet.NuevoServlet
```
11. Teniendo en cuenta las siguientes métodos disponibles en los objetos ServletRequest y ServletResponse recibidos por el método doGet:

* response.setStatus(N); <- Indica con qué código de error N se generará la respuesta. Usar la clase HttpServletResponse para indicar el código de respuesta.
* request.getParameter(param); <- Consulta el parámetro recibido, asociado al nombre ‘param’.
* response.getWriter() <- Retorna un objeto PrintWriter a través del cual se le puede enviar la respuesta a quien hizo la petición.
* response.setContentType(T) <- Asigna el tipo de contenido (MIME type) que se entregará en la respuesta.

Implemente dicho método de manera que:

* Asuma que la petición HTTP recibe como parámetro el número de id de una lista de cosas por hacer (todo), y que dicha identificación es un
número entero.
* Con el identificador recibido, consulte el item por hacer de la lista de cosas por hacer, usando la clase "Service" creada en el punto 10.

**Si el item existe:**
- Responder con el código HTTP que equivale a ‘OK’ (ver referencia anterior), y como contenido de dicha respuesta, el código html correspondiente a una página con una tabla que tenga los detalles del item, usando la clase "Service" creada en el punto 10 par crear la tabla.

**Si el item no existe:**
- Responder con el código correspondiente a ‘no encontrado’, y con el código de una página html que indique que no existe un item con el identificador dado.
- Si no se paso parámetro opcional, o si el parámetro no contiene un número entero, devolver el código equivalente a requerimiento inválido.
- Si se genera la excepcion MalformedURLException devolver el código de error interno en el servidor
Para cualquier otra excepcion, devolver el código equivalente a requerimiento inválido.
```
 Se encuentra en  edu.eci.servlet.model.Todo
```
12. Intente hacer diferentes consultas desde un navegador Web para probar las diferentes funcionalidades
* Salida Valida
![8](https://github.com/MPulidoM/CVDS_LAB05/blob/main/Imagenes/PARTE2.8.PNG)

* Excepcion numberFormatException
![9](https://github.com/MPulidoM/CVDS_LAB05/blob/main/Imagenes/PARTE2.9.PNG)

* Excepcion fileNotFoundException
![10](https://github.com/MPulidoM/CVDS_LAB05/blob/main/Imagenes/PARTE2.10.PNG)

## **PARTE III. - HACIENDO UNA APLICACIÓN WEB DINÁMICA A BAJO NIVEL.**
1. En su servlet, sobreescriba el método doPost, y haga la misma implementación del doGet.
2. Cree el archivo index.html en el directorio src/main/webapp/index.html de la siguiente manera:
```
<!DOCTYPE html>
<html>
  <head>
    <title>Start Page</title>
     <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
  </head>
  <body>
    <h1>Hello World!</h1>
  </body>
</html>
```

![11](https://github.com/MPulidoM/CVDS_LAB05/blob/main/Imagenes/PARTE3.1.PNG)

3. En la página anterior, cree un formulario que tenga un campo para ingresar un número (si no ha manejado html antes, revise http://www.w3schools.com/html/ ) y un botón. El formulario debe usar como método ‘POST’, y como acción, la ruta relativa del último servlet creado (es decir la URL pero excluyendo ‘http://localhost:8080/’).

![12](https://github.com/MPulidoM/CVDS_LAB05/blob/main/Imagenes/PARTE3.2.PNG)
![13](https://github.com/MPulidoM/CVDS_LAB05/blob/main/Imagenes/PARTE3.3.PNG)



