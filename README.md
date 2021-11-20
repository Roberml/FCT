# FCT



11/10/2021:

-Visto vídeo de Presentación, Introducción a Spring e Instalación del entorno de trabajo.

Descargé el IDE Eclipse con el plugin Spring Tool Suite ya que es el que recomiendan en el curso.




18/10/2021

Terminé introducción, contenedor de inversión de control y ámbito y ciclo de vida de un bean.
Sé que es escaso pero tuve bastantes problemas con la instalación de dependencias de maven, al fin creo que conseguí que el proyecto esté bien creado. La semana que viene cubriré más cursos y subiré el proyecto.





1/11/2021

Reinstaleé el IDE porque tuve problemas de nuevo con las dependencias de maven, ahora ya va bien, me surgió un problema con un tipo de fichero xml (new spring bean definition file). Resulta que los cursos de openwebinars están hechos en una versión de spring tool suite anterior a la actual, para solucionar este problema busqué en internet y encontré dos posibles soluciones, la primera es instalar Spring IDE Roo support y a pesar de que era la solución más popular asumo que era en el caso de tener la versión antigua, ya que 
no era posible instalarlo sin que diese fallos teniendo la actual. La otra opción es instalar spring tool 3 add-on for spring tool 4, con esta última ya solucioné el problema así que ahora no debería tener ningún problema más con el IDE. 









#CURSO SPRING CORE#
 
En este primer curso nos hace una introducción a Spring el cual es un framework para el desarrollo de aplicaciones (especialmente empresariales) y un contenedor de inversiones para Java. El IDE utilizado para este curso va a ser Spring Tool Suite, el cual es un plugin de Eclipse que viene incorporado con varias cosas para ayudarnos a crear nuestras aplicaciones. También nos enseña brevemente lo que es un patrón de diseño, pero esto se verá más a fondo más adelante.



La inyección de dependencias es un patrón de diseño orientado a objetos, en la cual los objetos se suministran a una clase en vez de que la clase cree dichos objetos. Estos objetos son llamados Beans los cuales son instanciados por el contenedor de Spring y se usarán cuando sean llamados, serán controlados por nuestro contenedor de inversión de control.

Para configurar y ensamblar estos beans podemos utilizar 3 cosas: un fichero xml, anotaciones o clases Java.

A la hora de definir un bean debemos prorcionarle un ID obligatorio y nombre completo de la clase. Para obtenerlo usamos la función appContext.getBean().

(Nota: esta función tiene distintas sobrecargas: podriamos poner de parámetros solo el id pero en tal caso hay que hacer un casting, otra donde le proporcionamos id y clase y otra donde sólo la clase la cual es la pero de todas, porque si hay dos beans en la misma clase salta excepción).

Si queremos autoinyectar un bean, usamos la anotación Autowired, la cual puede tener diferentes tipos:
no: sin autocableado
byName: en función del nombre de la
propiedad requerida.
byType: en función del tipo de la propiedad
requerida. Si hay más de un bean de este
tipo, se produce excepción.
constructor: análogo a byType, pero para
argumentos del constructor.


Esta opción puede ser un poco confusa, pero siempre podemos poner a false el Autowired en los beans más conflictivos. También podemos poner preferencias a los beans.

Los Beans tienen otros tipos de anotaciones. Como @Required la cual obliga a que una propiedad sea inyectada, sino salta excepción. La anotación @PostConstruct que obliga a que se lance un metodo despues de la inyección. @Predestroy obliga a que se lance un método antes de la destrucción de un bean en el contenedor.


Para todo esto nos ayuda especialmente utilizar la configuración a traves de java ya que aparte de que no suele dar problemas a diferencia de el uso de xml (hay un fallo en el <bean> el cual pone que es un fallo de descarga y resulta que es un fallo que no afecta nada al programa, esto lo encontré en una traducción de un blog chino) es mucho más cómoda. Sólo hay que saber que la clase donde definas los beans tiene que venir anotada con @Configuration (esto a nivel de clase) y los @Beans a nivel de método. Otra cosa importante es saber que para instanciar el contenedor de una clase java se hace diferente que en un fichero xml.
  
Por último realizamos el proyecto de MovieAdvisor, la cual es una aplicación de escritorio que te recomienda películas sacadas de un fichero con una gran lista de estas. Está subido.
  
  
  
 
  
  
#CURSO DE SPRING BOOT Y SPRING MVC#
  
  En este curso aprenderemos sobre el patrón de diseño modelo-vista-controlador, acceder a datos utilizando Spring Data JPA, saber las ventajas del uso de Spring boot y darle una seguridad a nuestra API.
  
  
  
  El Spring Boot nos facilita (mucho) la creación de un proyecto, viene con un servidor embebido tomcat, ya viene con dependencias iniciales el proyecto, configuración automática de librerías...
  
  
  Creamos este tipo de proyectos a través de Spring Initializr.
  
  
  Como esto nos autoconfigura muchas cosas podemos utilizar la anotación  @EnableAutoConfiguration(exclude ...clas)
  
  
  
  
  Antes sólo estábamos haciendo aplicaciones de escritorio, ahora empezamos a hacer aplicaciones web aplicando el patrón de diseñó MODELO-VISTA-CONTROLADOR, donde el modelo es el encargado de gestionar los datos ( a través de una base de datos) los cuales actualizan las vistas que verá el usuario y este intarctuará con estas mandándole información al controlador sobre qué hacer, el cual le dará instrucciones al modelo para hacer cambios si es necesario.
  
  
  Las clases Controladores tienen que ir anotadas con @Controller, las vistas van a ser archivos .html y las entidades (el modelo) van a ir anotadas con  @Entity
  
  
  En la clase Controller utilizaremos las anotaciones @GetMapping, @PostMapping, @PutMapping que vienen con la ruta donde se llamará  la petición.
  
  
  También saber la utilización de @RequestParam y @PathVariable los cuales nos pueden pillar información de la URI de diferente manera. @RequestParam pilla información de la query (?name=roberto por ejemplo) y @PathVariable nos la pilla directamente de la ruta
  
  
  Podemos implementar formularios con nuestros ficheros html para que la IU sea mejor, a partir de esto tambien tenemos la posibilidad de subir ficheros (como curiosidad se puede poner en el properties del proyecto el tamaño máximo del fichero).
  
  
  También empezamos a implementar Spring Security el cual nos permite hacer un sistema simple de autentificación y autorización.
  
  
  Spring Data JPA lo usamos para utilizar una base de datos relacional (en nuestro caso H2 que viene en una dependencia) para esto como comenté usamos la anotación @Entity en la clase la cual sea la "tabla" en las propiedades de la entity podemos usar @Id para saber que es clave primaria y @GeneratedValue para que el valor se genere automáticamente. (Como curiosidad hay una anotación @Table la cual nos permite cambiarle el nombre a la tabla si se da el caso de que el nombre de la clase no es permitido)
  
  
  También utilizarermos interfaces llamadas repositorios que extienden de CRUDREPOSITORY y se le pasa el tipo de entidad y el tipo de id <Entity, Long>
  
  esto nos permite guardar en una lista todas las entidades y utilizar metodos CRUD muy utiles save(), saveAll(), findAll(), findById()... todos estos métodos te los genera automáticamente al extender de crudrepository.
  
  
  Otra cosa interesante que podemos hacer es manejar apropiadamente errores, supongamos que tenemos un metodo en el controlador de encontrar por id a un usuario. Si ese usuario no existe podemos crear una excepción noUserFoundException el cual tendrá que extender de RunTimeException
  
  
  Podemos ponerle la anotación @ResponseStatus con el tipo de error que queremos que se active el método (por ejemplo el error 404)
  
  
  Hasta ahora hemos estado haciendo peticiones en Postman el cual es un software gratuito pero esto no nos va a funcionar si lo utilizamos desde una aplicacion angular, vue, jQUery por ejemplo.
  
  Para esto tenemos que implementar CORS la cual no es más que una política de seguridad que nos permite saber quien puede acceder a u
  
  
  Por último hicimos un proyecto que engloba todo de una API que maneja productos de segunda mano.
  
  
  
  Otra cosa importante es saber utiliar clases DTO (data transfer object) que no son más que una clase pojo que contiene información de las entidades en la capa de negocio. (puede tener solo datos de una entidad). Utilizar estas clases aligera transacciones.

  
  
  
  
  
  
  
  
  
  
  
 #CURSO DE DESARROLLO DE UNA API REST CON SPRING BOOT#
  
  
  en este curso aprenderemos sobre arquitectura rest, usar la librera lombok y saber la estructura de un controlador Rest.
  
  
  
  Rest está basado en el protocolo HTTP, no tiene estados, tiene una interfaz uniforme y un sistema de capas. Está orientado a ofrecer recursos (a través de URIs).
  
  El servidor puede ofrecer diferentes representaciones del recurso (xml, json).
  
  Sus ventajas son la separacion entre cliente y servidor. visibilidad, fiabilidad y escalabilidad, heterogeniedad, variedad de formatos, rapido y usa menos ancho de banda.
  
  
  Para proyectos rest, nuestros controladores ahora tendrán la anotación  @RestController
  
  También utilizaremos la dependencia lombok la cual nos facilita el uso de clases ya que nos ahorra crear todos los setters y getters, constructores y metodos que hay que sobreescribir.
  
  Tambien vamos a utilizar la clas HttpMessageConverter para elegir cómo queremos que se nos devuelva la información (por ejemplo en json).
 
Es importante saber tambien utilizar objetos dto (data transfer object) los cuales son clases POJO que tienen propiedades de las entidades en la capa negocio (puede tener solo proiedades de una entidad tambien) esto nos permite aligerar transacciones.
 
 
 
 Tambien saber utilizar excepciones personalizadas, pongamos el ejemplo que en cierta ruta podemos encontrar a un producto por su id, si ese producto no existe podemos crear la excepcion noProductoFoundException() la cual tiene que extender de RunTimeException.
 
 
 
 Podemos tambien ponerle la anotacion @ResponseStatus a un metodo para que responda a un error en concreto (como error 404).
 
 
 Hasta ahora hemos estado utilizando postman para hacer peticiones a nuestra api, pero esto en otros casos nos daria fallo ya que no estamos implementando el CORS que no es más que una politica de seguridad que nos permite indicar quien puede acceder a nuestros recursos.
 
 
 La configuracion de CORS en Spring viene dada por las anotaciones @CrossOrigin (que hay que ponersela a un metodo en un controlador) la cual nos permite a traves de metodos saber la lista de origenes, lista de metodos http soportados y duracion máxima en segundos en caché entre otras.
 
 Si queremos documentar nuestra APIRest utilizaremos swagger.
 
 
 
 
 #CURSO DE ELEMENTOS AVANZADOS EN APIREST#
 
 
 aprenderemos a manejar el patron dto en peticiones y respuestas conocer HATEOAS que es un patrón, implementar una api con spring data rest entre otras cosas
 
 
 
 
 
 
 
 
 Hasta ahora no hemos controlado el numero de elementos que nos aparecen en consulta. Pero en proyectos muy grandes donde haya que cargar mucha informacion es recomendable el uso de paginación, la  cual no es más que limitar el numero de elementos que aparecen por busqueda.(Pone un ejemplo muy bueno que es la TimeLine de twitter, no tiene sentido que te cargue todos los twits desde que te creaste una cuenta).
 
 
 Para utilizar los ya mencionados DTO crearemos una clase con la anotación @Builder gracias a lombok, esto nos permite construir nuestro objeto paso a paso setteando cada uno de los atributos que necesite.
 
 
 
 
 HEATEOAS Y HAL 
 
 
 HATEOAS basicamente nos permite que la información devuelta por el servidor incluya hipervinculos.
 
 
 El HAL es el standar para definir hipermedia como enlaces a recursos externos dentro del codigo json o xml.
 
 
 
 Hasta ahora hemos estado utilizando una base de datos en memoria la cual nos es util para testear nuestra aplicación, pero nuestra aplicacion Rest necesita implementar un sistema gestor base de datos real como postgreSQL para ello necesitaremos de un docker.
 
 
 
 
 
 
 
 #CURSO DE SEGURIDAD EN APIREST#
 
 En este curso aprenderemos a como implementar seguridad de diferentes maneras adecuadamente a través de Spring security
 
 
 
 
 Spring security es una dependencia la cual implementa la seguridad en nuestra API, basicamente nos permite responde a estas dos cuestiones: ¿Quien eres? y ¿Para qué tienes permisos?
 
 
 
 
 Esto nos permite hacer una gestión de usuarios básica en nuestro programa, pero hay diferentes formas de Seguridad, nosotros veremos la básica, con JWT, y con OAUTh2
 
 
 La seguridad básica consiste en que el usuario solicita un recurso protegido al servidor, este le pide que se logee, nosotros nos logeamos con la contraseña encriptada y el servidor nos devuelve el recurso protegido.
 
 
 
 
 
 La seguridad JWT consiste en una seguridad a partir de tokens, el usuario se logea, el servidor le proporciona un token el cual el usuario firma, el servidor comprueba la firma del token y se obtiene el recurso.
 
 Spring de forma nativa nos permite usar JWT
 
 
 
 
 La seguridad Oauth2 es un estandar abierto para la autorizacion de APis. Implementa diferentes flujos de autentificacion, y es el usado por grandes empresas como facebook twitter y GitHub, una característica de esta seguridad es que nos permite logearnos en programas que también tengan esta seguridad (podemos logearnos a facebook usando nuestra cuenta de Twitter).
 
 
 
 
 
 
 
 
 #FIN#
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
  
  
  
  
  
  
  


