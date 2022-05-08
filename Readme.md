Estructura del proyecto
1. DOMINIO:

   DTO y objetos del dominio (Contexto de la aplicación)
   Servicios: Puente entre los controladores y la capa de persistencia.
   Especificación de repositorios: Interfaces que determinan las reglas que debe cumplir la persistencia para actuar entre los objetos de dominio y la DB.

2. WEB:

   Controladores de API Rest.

3. PERSISTENCIA:

   Repositorios: Implementan las especificaciones que tiene la capa de DOMINIO.
   Entities: Mapean y actúan como tablas de la DB.

¿Qué es JPA?

Jpa es una especificación de Java, standar, para un framework ORM. Quiere decir que son uan serie de reglas que Java define para que cualquier framework que quierea interactura con la BD de Java, tenga que seguir.

Los frameworks mas populares de Java para este fin son:

    Hibernate
    TopLink
    EclipseLink
    ObjectDB

<h3>Anotaciones JPA</h3>

JPA utiliza anotaciones para conectar clases a tablas de la BD y asi evitar hacerlo de manera nativa con SQL.

    @Entity. Indica a una clase de java que esta representando una tabla de nuestra BD.
    @Table. Recibe el nombre de la tabla a la cual esta mapeando la clase.
    @column. Se le pone a los atributos de la clase, no es obligatoria, se indica sólo cuando el nombre de la columna es diferente al nombre del atributo de la tabla.
    @id amd @EmbededID. Es el atributo como clave primaria de la tabla dentro de la clase. @id se utiliza cuando es clave primaria sencilla y @EmbededID cuando es una clave primaria compuesta.
    @GeneratedValue. Permite generar automáticamente generar valores para las clases primarias en nuestras clases
    @OneToMany and @MatyToOne. Representar relaciones

Conocer qué es Spring Data

Spring Data NO es una implementacion de JPA, sino mas bien es un proyecto que usa JPA para ofrecer funcionalidaes extra en la gestion de tareas desde JAVA a las base de datos.

Spring Data internamente tiene varios subproyectos, entre ellos: Spring Data JPA y Spring Data JDBC, para conectarnos a BD relacionales (SQL). Spring Data MongoDB y Spring Data Cassandra, son proyectos para conectarnos a BD no relacionales.

La tarea principal de Spring Data es optimizar tareas repitivas.

Spring data nos provee de respositorios sin codigo, nos permiten hacer todo tipo de operaciones en BD (CRUD) sin utilizar una linea de código.

También nos provee de auditorías transparentes, por ello, posee un motor de auditorias que nos permite saber cuadno se insertó un registro, cuando se borró, cuando se actualizo en la BD, etc.
<h3>Implementación en el proyecto Market.</h3>

Se busca en MAVEN el repositorio Spring Boot Starter Data JPA, se copia el group y el name en las dependencias del archivo build.gradle de nuestro proyecto quedando de la siguiente manera.

dependencies {
//Dependencia agregada
implementation 'org.springframework.boot:spring-boot-starter-data-jpa'

    implementation 'org.springframework.boot:spring-boot-starter-web'
	testImplementation('org.springframework.boot:spring-boot-starter-test') {
		exclude group: 'org.junit.vintage', module: 'junit-vintage-engine'
	}
}

<h3>Los query method son muy potentes. Además de los explicado, permiten realizar múltiples operaciones de comparación con:</h3>

    Números: mayores, menores, iguales…
    Textos: contiene cierta porción de texto, empieza o termina con una porción de texto, ignora case sensitive…
    Fechas: Antes de cierta fecha, después de cierta fecha, entre cierta fecha…
    Joins entre entidades: Si tenemos una entidad que se relaciona con otra, es posible realizar “joins” con esa relación para tener queries más específicas según nuestra necesidad. Por ejemplo, si tengo una relación de Producto y Categoría y quiero tener todos los productos de cierta categoría podría hacer: findAllByCategoriasId(Integer categoriaId) y así poder llegar a esta relación. Esto puede mezclarse con múltiples relaciones en simultáneo
    Comparación entre un conjunto de datos: Si por ejemplo quiero traerme los productos con varias categorías, podría escribir findAllByCategoriasIdIn(List<Integer> categoriaIds); y así trabajar bajo un conjunto de Id de categorías

Existen más funcionalidades ✌🏼. Pueden ver más detalle acá: https://docs.spring.io/spring-data/jpa/docs/current/reference/html/#jpa.query-methods.query-creation