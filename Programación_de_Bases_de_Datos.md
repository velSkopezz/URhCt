---
title: Programación de Bases de Datos
author: Christian Velasco Pérez
---
# Programación de Bases de Datos
*Autor:* Christian Velasco Pérez <img src="https://iili.io/fpTTGnt.md.jpg" alt="Skopez" align="right" style="width:15%; margin-left:4%;margin-bottom:2%">
\
El siguiente contenido corresponde a un **apoyo** educativo para cualquier interesado y por eso puede contener fallos. El documento orientado al curso de *Programación de bases de datos* del Grado en Ingeniería Informática de la Universidad de La Rioja. Por consiguiente, se considera completa responsabilidad del lector lo que haga con la información de este documento.
\
La distribución del documento queda reservada al permiso explícito de su autor. Si necesitase información de contacto puede [enviar un correo](mailto:velskopezz@gmail.com).

## TEMA 1: Arquitectura de aplicaciones de Bases de Datos
Se habla de separación **topológica** cuando se trata de una *separación física*. La separación **lógica** se basa en capas:
1. Capa de **presentación**
    - generación
    - representación
2. Capa de **lógica de negocio**
3. Capa de **persistencia**

> Eg: corresponde a la *representación* un HTML, la *lógica de negocio* implementa las reglas de negocio y corresponden a la *persistencia* los programas almacenados o sistemas de gestión de bases de datos.

---

### Topología de un nivel
Consiste en **un solo servidor** con su base de datos y un **emulador de terminal** para representar la información. Es el sistema más simple.

### Arquitectura cliente-servidor
También se conoce como como *topología de dos niveles*.

Se distinguen **dos roles**: uno de ellos hace *peticiones al servidor* y el otro *gestiona los recursos* para dar una respuesta. La **persistencia** puede estar dividida entre el cliente y el servidor así como estar completamente en alguna de ellas.
\
Se habla de ***Thin-Client*** o ***Fat-Client*** según la *cantidad de persistencia en el cliente*.
> Eg: se considera *Fat-Client* si el grueso de la aplicación reside en el cliente.

![Arquitectura cliente-servidor](https://edgarbc.wordpress.com/wp-content/uploads/2014/02/501f9-cliente-servidor.png "ARQUITECTURA CLIENTE/SERVIDOR (DOS CAPAS) en WordPress")

### Topología de tres niveles
Utiliza **múltiples roles de servidor**. Está reforzado en el mundo empresarial por J2EE. Uno de ellos sirve la **lógica de negocios**  y el otro los **datos**, aunque pueden mezclarse en diferentes casuísticas.

![Topología de tres niveles](https://bbdd.abrilcode.com/lib/exe/fetch.php?media=bloque1:3_capas.png "Fundamentos de Bases de Datos en abrilCode")

#### Ventajas sobre el **cliente grueso**
- simplificación del **tráfico de red**
- mayor **seguridad**
- facilidad de **mantenimiento**
- compartición de **lógica de negocio**
- fácilmente **escalable**

### División en capas
Proporciona una solución más **flexible y dinámica** en la que cada **capa asume funciones aisladas**. Su arquitectura se forma en torno a tres capas:
1. **Generación de presentación**
2. **Lógica de negocio**
3. **Control de persistencia** 

> La tecnología principal para lograrlo suele ser la **orientación a objetos**.
>
> Nota: Para intercambiar la información entre distintos sistemas se suelen usar objetos de misma clase para garantizar la compatibilidad de los datos.

![Divisón en capas](https://reactiveprogramming.io/_next/image?url=%2Ffigures%2Fcapas-flow.png&w=1920&q=75 "APLICACIONES DE 2, 3 Y N CAPAS en WordPress")

> La mayor diferenciación que ofrece esta arquitectura incluye las siguientes ventajas
> - facilidad de **mantenimiento**
> - **especialización** en la respectiva capa
> - separación física que facilita la **escalabilidad**
> - permite disponer de **variantes de una misma capa**
> - clara **diferenciación** de funciones en capas
> - **estabilidad** al recodificar una capa

---

### Capa de presentación
Se encarga de la **interacción** con entidades externas y pueden existir en una sola aplicación **múltiples capas de presentación** para distintas entidades. Puede tener *cualquier medio* y *no debe incluir reglas de negocio*.

> Eg: en una página web al cliente le corresponde la **representación** y al servidor le corresponde la **generación**.
> 
> Nota: El ejemplo logra ilustrar que la capa de presentación no le corresponde exclusivamente al cliente.

### Capa de lógica de negocio
Es el "corazón de la aplicación". Se encarga de **efectuar las normas de negocio**. Suele trabajar con **técnicas de orientación a objetos** y dos elementos:
- ***Domain model***: objetos de negocio
- ***Business model***: servicios que atienden a las reglas

> Eg: al *Domain model* le corresponderá el objeto `Cliente` y al *Business model* le corresponderá comprobar en `ProcesarPago()` si se puede efectuar.

### Capa de persistencia
Se encarga del almacenamiento y tratamiento de **datos**. Interface las operaciones **CRUD** (create, retrieve, update, delete) y el **intercambio de colecciones de objetos** para la **comunicación con las bases de datos**.

## TEMA 2: Panorámica general de la programación de bases de datos
Este tema refiere a las alternativas (herramientas y metodologías) para implementar la **capa de persistencia**.

Se agrupan en dos estrategias fundamentales: **CLI** y **SLI**.
\
En Java se dispone de las herramientas SQLJ y **JDBC**. Estas APIs son de carácter general y facilitan la migración de código a otras herramientas fácilmente.
> Tienen compatibilidad con distintas tecnologías.

Se utiliza **SQL** en sistemas informáticos sobre la ejecución directa por un doble motivo:
- **ocultación** de complejidad de consulta SQL
- **seguridad** en forma de funcionalidad definida

---

Se distinguen dos formas de embeber: **Statement-Level Interface** (SLI) y **Call-Level Interface** (CLI).
\
Una llama a consultas y la otra incorpora *funciones que llaman a consultas* en su interior, respectivamente.
> Eg: SLI
> ```java
> #sql {SELECT nombre INTO :nPersona FROM Persona WHERE DNI=:dnis[i]}
> /* Nótese que se llama con un '#' */
> ```
>
> Eg: CLI
> ```java
> ResultSet rs = stmt.executeQuery("SELECT nombre FROM Persona WHERE DNI=" + dnis[i]);
> /* Nótese que la consulta es un string del lenguaje huésped */
> ```
>
> Nota: Tanto SLI como CLI se considera que tienen SQL embebido.

### Statement-Level Interface (SLI)
Existen llamadas de **precompilado de transacciones** en las que se **insertan** de forma binaria. No basta con el compilador del lenguaje porque **no lo incorpora dentro del lenguaje**.

Como SLI necesita de precompilado de transacciones no es posible utilizar **SQL dinámico**.
> La longitud de las SLI suele ser menor en texto de código fuente.
> 
> Se dice que **SQL está embebido** en el *lenguaje huésped*.

### Call-Level Interface (CLI)
El lenguaje es **intrínsecamente huésped** y las consultas son **strings**, que son editables de forma dinámica durante la ejecución. No se considera que SQL esté embebido.

### Diferencias y ventajas de las interfaces
concepto | SLI | CLI
:--- | :---: | :---:
legibilidad de código fuente según longitud | (+) mayor | menor
momentos de compilación | (+) precompilado de SQL | compilado único sin SQL
velocidad de compilación | suele traducir a CLI | (+) veloz: no compila SQL
introducción de herramientas de desarrollo | muy pesada | (+) sencilla: un binario
compatibilidad con SQL dinámico | difícilmente | (+) nativa

---
---

### Elementos de una API de acceso a base de datos
Las APIs proveen una **interfaz** para un sistema de bases de datos. Proporciona:
- Conexiones
- Instrucciones
- Cursores

#### Conexiones
Permite obtener **información meta** y debe cerrarse tras su uso.

#### Instrucciones
Se distinguen dos planes de ejecución:
- **a demanda**: se recalcula el *plan de ejecución*.
- **preparada**: se reutiliza un *plan de ejecución* para varias transacciones.

> Involucrará a las clases de JDBC `Statement` y `PreparedStatement` para las instrucciones *a demanda* y *preparadas* respectivamente.

#### Cursores
Se utilizan fundamentalmente para **consultas**. Son zonas de memoria del servidor que sirven a modo de **almacén personal**. Hay diferentes tipos:
- unidireccionales
- multidireccionales
- actualizables

> Los actualizables referencian a la base de datos para poder alterar valores.

### Microsoft ODBC
Es un API de Microsoft orientado a múltiples aplicaciones y **marcas**. Para usar ODBC se necesita un *driver ODBC específico* para la respectiva base de datos.

ODBC es un **generalizador**: abstrae conexiones, interacciones, representaciones... En definitva, permite **separar la base de datos** de las capas de persistencia y lógica de negocios.
\
Tiene un **controlador de drivers**.

Se distinguen dos tipos de drivers ODBC:
- **una capa**: transfiere la instrucción
- **dos capas**: *traduce* la instruccion al lenguaje nativo y la transfiere

> Eg: un driver de una capa necesita que utilices el lenguaje SQL específico de la base de datos. Con dos capas se generaliza el SQL independientemente de la base de datos.
>
> Nota: La implementación del driver ODBC depende del encargado del sistema de la base de datos.

### JDBC
Es un API de pocas clases y fundamentalmente **interfaces**. 
\
Los propios encargados que conocen el sistema de bases de datos son los que deben proporcionar un **driver** (en forma de archivo jar) que incluya clases que implementen dichas interfaces.

![Proceso de conexión a una base de datos](https://lh5.googleusercontent.com/proxy/R1fvs-rCO2LXBgJmnXH7SpHlDcMQRO3GjmN7KA3CotxIe0tcsBtkZS0ASVu22NbJBpX9d9QatF821yTE1slxuTngM1C9U5GEqehefnbRl8mogJF3LIG8-g "JDBC en UNAM")

> Nota: Para la **portabilidad** hay que crear objetos de *clases interfaces* para el entendimiento del compilador.

Se distinguen hasta cuatro tipos de formas de conectarse con la base de datos utilizando JDBC.

![Tipos de controlador](https://otroblogsobretics.wordpress.com/wp-content/uploads/2011/08/19-1-conectividad-java-base-de-datos-alternativo.png "Java y Base de Datos: JDBC en WordPress")

> Nota: El método del puente está dejando de ser utilizado.

#### Interfaz `Driver` y clase `DriverManager`
La interfaz `Driver` se utiliza para obtener generalización.
\
Es fundamentalmente necesario para la **estandarización del API**.

El **`DriverManager`** es un **gestor de drivers**. Almacena una **lista de drivers** y decide cuál es el driver que debe ser utilizado.

> Nota: Añadir un driver al listado se hacía de forma manual hasta la versión 4.0 de JDBC. Para información adicional sobre añadir drivers de forma manual revisar transparencias.

> Nota: Para ver **información sobre el método `getConnection()`** revisar transparencias,

#### Interfaz `Connection`
Un objeto de una clase que implementa **`Connection`** representa una **sesión abierta**. Se dispone de tres clases fundamentales de las cuales la segunda y tercera mencionadas heredan de la primera:

- **`Statement`** para operaciones *a demanda*
- **`PreparedStatement`** para operaciones *preparadas*
- **`CallableStatement`** para **programas almacenados**

#### URL de conexión
Se adjunta un ejemplo:

```java
jdbc:orcale:thin@IP:1521/ServiceName
```

Pada cada sistema gestor se tuene una URL con ligeras variaciones.

> Eg: para una base de datos de Oracle se pondrá `oracle:thin@` aunque para una base de datos de MySQL se pondrá `mysql://`.

A cada conexión le debería corresponder un bloque de control de errores con un `finally` que la cierre.

> Nota: Es recomendable que una base de datos tenga un máximo de usuarios activos.

#### Interfaz `Statement`
Su función fundamental es **ejecutar transacciones**:
- `executeQuery(String): ResultSet` se utiliza para ejecutar transacciones de tipo consulta.
- `executeUpdate(String): int` se utiliza para transacciones DDL y DML sin consultas.
- `execute(String): boolean` para uso generalizado. Devuelve `true` si la cadena corresponde a un select o false si corresponde a otra operación.

> Nota: La función de `execute(String): boolean` es fundamentalmente tratar con transacciones cuyo contenido no conoces. Es más claro y aporta mayor control usar las funciones específicas.

Tanto **`Statement`** como **`ResultSet`** tienen un método **`close()`** para cerrar la comunicación. Oracle recomienda **cerrarlo explícitamente**.