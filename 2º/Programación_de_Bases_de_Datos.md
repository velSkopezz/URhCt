---
title: Programación de Bases de Datos
author: Christian Velasco Pérez
---
# **Programación de Bases de Datos**
*Autor:* Christian Velasco Pérez <img src="https://iili.io/fpTTGnt.md.jpg" alt="Skopez" align="right" style="width:15%; margin-left:4%;margin-bottom:2%">
\
El siguiente contenido corresponde a un **apoyo** educativo para cualquier interesado y por eso puede contener fallos. El documento está orientado al curso de *Programación de bases de datos* del Grado en Ingeniería Informática de la Universidad de La Rioja y se considera completa responsabilidad del lector lo que haga con la información de este documento.
\
La distribución del documento queda reservada al permiso explícito de su autor. Si necesitase información de contacto puede [enviar un correo](mailto:velskopezz@gmail.com).

# TEMA 1: Arquitectura de aplicaciones de Bases de Datos
Se habla de separación **topológica** cuando se trata de una *separación física*. La separación **lógica** se basa en capas:
1. Capa de **presentación**
    - generación
    - representación
2. Capa de **lógica de negocio**
3. Capa de **persistencia**

> Eg: corresponde a la *representación* un HTML, la *lógica de negocio* implementa las reglas de negocio y corresponden a la *persistencia* los programas almacenados o sistemas de gestión de bases de datos.

---

## Topología de un nivel
Consiste en **un solo servidor** con su base de datos y un **emulador de terminal** para representar la información. Es el sistema más simple.

## Arquitectura cliente-servidor
También se conoce como como *topología de dos niveles*.

Se distinguen **dos roles**: uno de ellos hace *peticiones al servidor* y el otro *gestiona los recursos* para dar una respuesta. La **persistencia** puede estar dividida entre el cliente y el servidor así como estar completamente en alguna de ellas.
\
Se habla de ***Thin-Client*** o ***Fat-Client*** según la *cantidad de persistencia en el cliente*.
> Eg: se considera *Fat-Client* si el grueso de la aplicación reside en el cliente.

![Arquitectura cliente-servidor](https://edgarbc.wordpress.com/wp-content/uploads/2014/02/501f9-cliente-servidor.png "ARQUITECTURA CLIENTE/SERVIDOR (DOS CAPAS) en WordPress")

## Topología de tres niveles
Utiliza **múltiples roles de servidor**. Está reforzado en el mundo empresarial por J2EE. Uno de ellos sirve la **lógica de negocios**  y el otro los **datos**, aunque pueden mezclarse en diferentes casuísticas.

![Topología de tres niveles](https://bbdd.abrilcode.com/lib/exe/fetch.php?media=bloque1:3_capas.png "Fundamentos de Bases de Datos en abrilCode")

### Ventajas sobre el **cliente grueso**
- simplificación del **tráfico de red**
- mayor **seguridad**
- facilidad de **mantenimiento**
- compartición de **lógica de negocio**
- fácilmente **escalable**

## División en capas
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

## Capa de presentación
Se encarga de la **interacción** con entidades externas y pueden existir en una sola aplicación **múltiples capas de presentación** para distintas entidades. Puede tener *cualquier medio* y *no debe incluir reglas de negocio*.

> Eg: en una página web al cliente le corresponde la **representación** y al servidor le corresponde la **generación**.
> 
> Nota: El ejemplo logra ilustrar que la capa de presentación no le corresponde exclusivamente al cliente.

## Capa de lógica de negocio
Es el "corazón de la aplicación". Se encarga de **efectuar las normas de negocio**. Suele trabajar con **técnicas de orientación a objetos** y dos elementos:
- ***Domain model***: objetos de negocio
- ***Business model***: servicios que atienden a las reglas

> Eg: al *Domain model* le corresponderá el objeto `Cliente` y al *Business model* le corresponderá comprobar en `ProcesarPago()` si se puede efectuar.

## Capa de persistencia
Se encarga del almacenamiento y tratamiento de **datos**. Interface las operaciones **CRUD** (create, retrieve, update, delete) y el **intercambio de colecciones de objetos** para la **comunicación con las bases de datos**.

# TEMA 2: Panorámica general de la programación de bases de datos
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

## Statement-Level Interface (SLI)
Existen llamadas de **precompilado de transacciones** en las que se **insertan** de forma binaria. No basta con el compilador del lenguaje porque **no lo incorpora dentro del lenguaje**.

Como SLI necesita de precompilado de transacciones no es posible utilizar **SQL dinámico**.
> La longitud de las SLI suele ser menor en texto de código fuente.
> 
> Se dice que **SQL está embebido** en el *lenguaje huésped*.

## Call-Level Interface (CLI)
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

## Elementos de una API de acceso a base de datos
Las APIs proveen una **interfaz** para un sistema de bases de datos. Proporciona:
- Conexiones
- Instrucciones
- Cursores

### Conexiones
Permite obtener **información meta** y debe cerrarse tras su uso.

#### Instrucciones
Se distinguen dos planes de ejecución:
- **a demanda**: se recalcula el *plan de ejecución*.
- **preparada**: se reutiliza un *plan de ejecución* para varias transacciones.

> Involucrará a las clases de JDBC `Statement` y `PreparedStatement` para las instrucciones *a demanda* y *preparadas* respectivamente.

### Cursores
Se utilizan fundamentalmente para **consultas**. Son zonas de memoria del servidor que sirven a modo de **almacén personal**. Hay diferentes tipos:
- unidireccionales
- multidireccionales
- actualizables

> Los actualizables referencian a la base de datos para poder alterar valores.

## Microsoft ODBC
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

# TEMA 3: JDBC
Es un API de pocas clases y fundamentalmente **interfaces**. 
\
Los propios encargados que conocen el sistema de bases de datos son los que deben proporcionar un **driver** (en forma de archivo jar) que incluya clases que implementen dichas interfaces.

![Proceso de conexión a una base de datos](https://lh5.googleusercontent.com/proxy/R1fvs-rCO2LXBgJmnXH7SpHlDcMQRO3GjmN7KA3CotxIe0tcsBtkZS0ASVu22NbJBpX9d9QatF821yTE1slxuTngM1C9U5GEqehefnbRl8mogJF3LIG8-g "JDBC en UNAM")

> Nota: Para la **portabilidad** hay que crear objetos de *clases interfaces* para el entendimiento del compilador.

Se distinguen hasta cuatro tipos de formas de conectarse con la base de datos utilizando JDBC.

![Tipos de controlador](https://otroblogsobretics.wordpress.com/wp-content/uploads/2011/08/19-1-conectividad-java-base-de-datos-alternativo.png "Java y Base de Datos: JDBC en WordPress")

> Nota: El método del puente está dejando de ser utilizado.

## Interfaz `Driver` y clase `DriverManager`
La interfaz `Driver` se utiliza para obtener generalización.
\
Es fundamentalmente necesario para la **estandarización del API**.

El **`DriverManager`** es un **gestor de drivers**. Almacena una **lista de drivers** y decide cuál es el driver que debe ser utilizado.

> Nota: Añadir un driver al listado se hacía de forma manual hasta la versión 4.0 de JDBC. Para información adicional sobre añadir drivers de forma manual revisar transparencias.

> Nota: Para ver **información sobre el método `getConnection()`** revisar transparencias,

## Interfaz **`Connection`**
Un objeto de una clase que implementa **`Connection`** representa una **sesión abierta**. Se dispone de tres clases fundamentales de las cuales la segunda y tercera mencionadas heredan de la primera:

- **`Statement`** para operaciones *a demanda*
- **`PreparedStatement`** para operaciones *preparadas*
- **`CallableStatement`** para **programas almacenados**

### URL de conexión
Se adjunta un ejemplo:

```java
jdbc:orcale:thin@IP:1521/ServiceName
```

Pada cada sistema gestor se tuene una URL con ligeras variaciones.

> Eg: para una base de datos de Oracle se pondrá `oracle:thin@` aunque para una base de datos de MySQL se pondrá `mysql://`.

A cada conexión le debería corresponder un bloque de control de errores con un `finally` que la cierre.

> Nota: Es recomendable que una base de datos tenga un máximo de usuarios activos.

## Interfaz **`Statement`**
Su función fundamental es **ejecutar transacciones**:
- `executeQuery(String): ResultSet` se utiliza para ejecutar transacciones de tipo consulta.
- `executeUpdate(String): int` se utiliza para transacciones DDL y DML sin consultas.
- `execute(String): boolean` para uso generalizado. Devuelve `true` si la cadena corresponde a un select o false si corresponde a otra operación.

> Nota: La función de `execute(String): boolean` es fundamentalmente tratar con transacciones cuyo contenido no conoces. Es más claro y aporta mayor control usar las funciones específicas.

Tanto **`Statement`** como **`ResultSet`** tienen un método **`close()`** para cerrar la comunicación. Oracle recomienda **cerrarlo explícitamente**.

## Interfaz **`ResultSet`**
Ofrece métodos para **recorrer los resultados** de las **consutlas**:
- `next(): boolean` devuelve `true` si hay más tuplas o `false` si no las hay.
- `getObject(int): Object` devuelve el dato i-ésimo de la tupla como `Object`
    > Nota: También hay `getDouble`, `getInt`, `getString` etc.

### Tratamiento de `null`s
Para los **tipos primitivos** los valores `null` son transforamdos a su equivalente más lógico.
> Eg: `int` pasa a ser valer 0, `String` pasa a valer la cadena vacía, etc. Esto se debe a que en Java los tipos primitivos y los objetos van aparte. Los objectos a efectos prácticos son una referencia por lo que se les puede asignar `null`. Los tipos primitivos no cuentan con esta ventaja.

Para controlarlo se pueden seguir dos métodos:
1. Usar el método `wasNull(): boolean` que devuelve si es `null`.
2. Transformarlo a un **objeto** ya que estos pueden valer `null`:
    - `getObject(int): Object`
    - `getObject(int, Class<T>): T`

## Interfaz **`PreparedStatement`**
Sirve para realizar **transacciones parametrizadas** utilizando un caracter `?` como almohadilla que permite introducir **parámetros** en **transacciones preparadas**.
+ `setObject(int, Object): void` donde se introduce el índice del parámetro y el dato a ingresar.
    > Nota: Al igual que en `ResultSet`, también hay métodos para otros tipos de datos. 

Es especialmente útil porque **almacena la ruta de la transacción** aumentando la eficiencia y, al mismo tiempo, es **fundamental para la seguridad** ya que impide la **inyección de código**.
> Eg: véase por inyección de código.
>
> Si el código tiene la siguiente forma y, por tanto, usa `Statement`:
> ```java
> String query;
> query = "SELECT * FROM users WHERE usr='" + user + "' AND pwd='" + password + "'";
> ```
> El usuario puede ingresar en su entrada:
> ```
> user?
> > admin
> password?
> > any' OR '1'='1
> ```
> Esto inmediatamente transformaría la `String` `query` en:
> ```sql
> SELECT *
> FROM users
> WHERE usr='admin'
>   AND pwd='any'
>   OR '1'='1'
> ```
> Como se puede apreciar, la condición de dicha consulta *siempre se cumple* por lo que se puede ingresar a cualquier usuario sin tener la contraseña.
>
> En `PreparedStatement` el código se dispondría tal que:
> ```java
> PreparedStatement statement = connection.preparedStatement(
>       """
>       SELECT * 
>       FROM user 
>       WHERE usr=?
>          AND pwd=?"
>       """
> );
> statement.setString(1, user);
> statement.setString(2, password);
> ```
> El dato se introduce directamente a la consulta evitando dicho problema.

> Nota: Los problemas y las soluciones con los `null`s persisten. 

## Interfaz **`CallableStatement`**
Sirven para **llamar programas almacenados** y extiende `PreparedStatement. Se pueden llamar ***procedure**s* o ***function**s*.

Al usar `[? = ]call <procedure_name>[(?, ?...)]` como el argumento del método `prepareCall(String): String` del objeto `Connection` se prepara la llamada de acuerdo con los parámetros {`in`, `out`, `inout`} que se disponen en el final de la expresión

Para obtener los datos usamos `registerOutParameter(int, Types.[tipo]): void` y posteriormente el comando *getter* adecuado.

---

## Transacción JDBC
Cuando se necesita que **las transacciones SQL se hagan como bloques** hace falta formarlos como un bloque o **transacción JDBC**.

En JDBC el `autocommit` está habilitado por defecto. Para deshabilitarlo se usa el método `setAutoCommit(boolean): void` de la interfaz `Connection`.

> Nota: Llamamos **contexto transaccional** a aquello que nos indica cómo se realiza la transacción.
> > Eg: queda compuesto tras hacer:
> > 1. `connection.setAutoCommit(false)`
> > 2. `try { . . . ; connection.commit(); }`
> > 3. `catch (SQLException e) { . . . ; connection.rollback(); }`

Hay **situaciones en las que *no* hace falta arreglar el bloque**. 
> Eg: una **instrucción única** provoca que, por su propia arquitectura, cualquier error provoque un ***rollback* a nivel de instrucción**. Un sistema gestor de base de datos que corrompiese la base de datos por, por ejemplo, un corte de luz, sería un mal sistema gestor.

> Ct: se exige saber cuándo se debe o no hacerlo y penaliza muchísimo porque se entiende que no comprendes nada de los contenidos.

Existen **save points** para que el *rollback* vuelva al punto determinado.

> Nota: Siempre y cuando el driver cumpla con JDBC 4.1 se puede usar ***try-with-resources*** para cerrar el `Connection`.

### Control de concurencia
Se trata con mayor profundidad en el tema 4.
\
Se logra mediante el **aislamiento** del que se distinguen 4 formas proporcionadas por JDBC.

### **`SQLException`**
Proporciona métodos:
- `getMessage(): String` devuelve el mensaje de error.
- `getErrorCode(): int` devuelve el código de **error SQL**. Sirve para la redirección del usuario en caso de errores.
- `getNextException(): SQLException` proporciona el siguiente error.

### **`DatabaseMetaData`**
Permite obtener **metainformación** relativa a la base de datos como su esquema e **información sobre el sistema gestor de base de datos**.
\
Sus métodos devuelven un `ResultSetMetaData`.

### Pool de conexiones
Existe una **piscina de conexiones** en la que, en vez de cerrar una `Connection`, se almacena en una *pool* y se recoge cuando vuelva a hacer falta.
\
Suele **combinarse con `PreparedStatement`** aprovechando el plan de ejecución ya que, de lo contrario, se pierde junto con el cierre de la `Connection`.

### Actualizaciones por lotes
Disponible desde JDBC 4, consiste en añadir operaciones con `addBatch(String): void` y, finalmente, **ejecutar todo de golpe** lo que mejora el rendimiento. Está orientada a **modificaciones** y no debería usarse en consultas. Devuelve un array con los resultados de las operaciones al usar `executeBatch(): int[]`.
> Nota: Las operaciones de modificación devuelven la cantidad de filas modificadas.

> Nota: Para el método `clearParameters` revisar transparencias.

> Nota: En MySQL es necesario añadir una cláusula adicional para usar lotes en la conexión.

Es inviable hacer lotes muy grandes por lo que normalmente toca hacer **múltiples lotes**. En todos ellos se debe hacer el **contexto transaccional** dado que cada uno de ellos se ejecuta como un único `Statement`.

> Nota: Oracle recomienda lotes de entre 50 y 100 operaciones.

> ¿Anexo?: Existe `ResultSet` actualizable-

# TEMA 4: Procesamiento de transacciones y acceso concurrente
El objetivo es **garantizar la consistencia y calidad de los metadatos**. La pérdida de esta calidad puede darse **al modificar** la información.

Esto puede afectar a las consultas en múltiples casos, especialmente, en caso de **concurrencia**. La solución suele ser usar lotes.

El sistema gestor de bases de datos debe garantizar la **coherencia** representativa con el mundo y, al mismo tiempo, **firmeza** en sus operaciones.
> Nota: Hay problemas tipo y estos serán los estudiados a lo largo del temario.

## Análisis de un problema y recuperación
Todo se basa en la consistencia de la base de datos.
\
Cuando se realiza una operación DDL o DML la base de datos entra en una fase de peligro en la que cualquier concurrencia puede ser motivo de un error.

Cualquier tipo de **interrupción** o **concurrencia** puede provocar situaciones en las que se deba recuperar la base de datos. Para garantizar la seguridad es fundamental usar lotes o **batches**.

La recuperacion puede concluir de dos formas:
- Con la **terminación** mantenieno los efectos.
- Con la **anulación** de tal forma que se revierta el estado al anterior.

Además, la recuperación puede tener dos alcances:
- Sobre toda la **base de datos**
- Sobre una **transacción**

Una recuperación puede hacerla el **sistema gestor de bases de datos** o el **usuario** según la casuística.

## Concurrencia
Son la fuente de muchos peligros. Algunos de ellos tienen nombre propio.

Para trabajar con concurrencias se suele utilizar **recursos compartidos**, es decir, se evita el paralelismo en la base de datos.

### Problema de la actualización perdida
Se da cuando un usuario $T_{1}$ y un segundo usuario $T_{2}$ siguen el siguiente esquema de tal forma que en el quinto tiempo la modificación de $T_{2}$ pisa la realizada por $T_{1}$.

tiempo | 1 | 2 | 3 | 4 | 5
:--- | :---: | :---: | :---: | :---: | :---:
$T_{1}$ | transferirBloque(X) | modificarBloque(X) |  | modificar(X) |  |
$T_{2}$ |  |  | transferirBloque(X) |  | modificar(X)

### Problema de la lectura sucia
Ocurre cuando un usuario $T_{2}$ lee unos datos modificados por una operación finalmente alterada.

tiempo | 1 | 2 | 3 | 4
:--- | :---: | :---: | :---: | :---:
$T_{1}$ | transferirBloque(Y) | modificar(Y) |  | rollback(Y)
$T_{2}$ |  |  | leer(Y) | 

> Nota: El dato que lee $T_{2}$ está alterado por $T_{1}$ por lo que, luego del *rollback*, se está leyendo un dato falso. Esto no sucede en Oracle pero sí en MySQL y SQLServer-.

### Problema del resumen incorrecto
Es un problema que sucede cuando $T_2$ realiza una función de agregación (`SUM`, `AVG`...) mientras se alteran los datos de la base de datos de tal forma que los datos leídos alteran su valor **durante la función** de agregación.

tiempo | 1 | 2 | 3 | 4 | 5 
:--- | :---: | :---: | :---: | :---: | :---: 
$T_{1}$ | transferirBloque(X) |  | modificar(X) |  |  
$T_{2}$ |  | funcion(X[0::n/2]) |  | funcion(X[n/2::n]) | resultadoFuncion()

> Nota: $T_{2}$ lee un dato inconsistente de un bloque y consistente del otro.

> Nota: El problema encuentra su solución con el aislamiento de, al menos, `REPETEABLE_READ`.

### Otros problemas
Entre otros problemas comunes se encuentran la lectura no repetible y la lectura fantasma cuya principal diferencia es la adición o modificación:
- **Lectura no repetible**
    \
    Una consulta que no es repetible porque, concurrentemente, se ha **modificado o eliminado** algún registro.
- **Lectura fantasma**
    \
    Una consulta que proporciona datos erróneos porque se ha **añadido** una *tupla fantasma* de forma concurrente.

## Herramientas de control de concurrencia
Aparte de las ya vistas **transacciones por lotes**, se dispone de las siguientes operaciones:
- commit
- rollback
- abort

## Estados de una transacción
Se distinguen distintos estados de una transacción:
- **Activa**
    \
    Una transacción es activa cuando realiza operaciones de lectura o escritura.
- **Parcialmente confirmada**
    \
    Una transacción está parcialmente confirmada cuando se acepta la operación pero no se realiza un *commit*. Suele relacionarse con restricciones diferidas.
- **Confirmada**
    \
    Una transacción está confirmada cuando se ha efectuado un *commit*.
- **Fallida**
    \
    Una transacción ha fallado si en algún momento se ha abortado.
- **Terminada**
    \
    Una transacción está terminada cuando se ha abortado o completado exitosamente.

![Estados de una transacción](https://miro.medium.com/0*FYOwlEL8-6yMBMoP. "Diagrama de estados de una transacción, por Toni Mas, en Medium")

Se espera que una transacción tenga las **propiedades ACID**:
- Atomicidad
- Consistencia
- Aislamiento
- Durabilidad

### Restricciones de integridad
Hay dos formas de **restricción de integridad**:
- inmediata
- diferida

Las restricciones inmediatas son aquellas que suceden durante la operación. En cambio, las **operaciones diferidas** se destacan porque **posponen la revisión al commit**. Esta distinción es la que provoca la diferencia prinicpal entre la fase de parcialmente confirmada y confirmada.
> Eg: el caso más claro es el de las restricciones de referencia cíclicas

Un error de restricción diferida **deshace toda la transacción** en vez de únicamente la tupla afectada.

Para definir una restricción de integridad:
1. Declarar la **restricción diferible**
    \
    Para declarar una variable diferible se utilizan las siguientes opciones:
    - `DEFERABLE`
    - `NOT DEFERABLE`

    > Nota: Las transacciones son `NOT DEFERABLE` por defecto.

2. Diferirla
    \
    Se hace mediante la adición de un `CONSTRAINT`. Para ello se distinguen dos tipos:
    - `INITIALLY INMEDIATE`
    - `INITIALLY DEFERRED`
    
    Ello indica la forma en la que **se trata por defecto**, por ello, lo común es dejarlo en `INITIALLY INMEDIATE`.

    > Nota: Por defecto se encuentra en `INITIALLY INMEDIATE`.

    > Eg: `CONSTRAINT <nombre> <características> INITIALLY INMEDIATE` y, posteriormente, `SET CONSTRAINT <nombre> DEFERRED`.

## Recuperación de base de datos
Se pueden hablar de recuperacion a dos **niveles**:
- **Base de datos**: recuperar suele incluir restaurar el estado.
- **Transacción**: recuperar suele incluir el aborto de la transacción.

Estas recuperaciones pueden hacerse mediante diarios o **logs**.

### Actualizacion diferida
Consiste en trabajar con 3 elementos:
- caché
- log
- base de datos

De la hoja de transacción pasa al caché, del caché al hacer *commit*, al log y, después, se formaliza el cambio del caché a la base de datos. Todos los cambios de la base de datos deben pasar primero por el log.
\
El objetivo es que **el log registre todos los cambios** y que, en el peor de los casos, **recupere una transacción**.

Recibe el nombre de **diferida** porque se trabaja sobre una caché que se **limpia tras la transacción** o al hacer un ***rollback***. Además, si el resultado de una consulta está presente en la caché, el sistema gestor evita acceder a la base de datos en su búsqueda.

![Actualización diferida](https://static.packt-cdn.com/products/9781788291804/graphics/0d085f8b-9535-4fec-b3f1-fcc57643fdc5.png "İnternetin kara kutusu Log, por Arenklorden, TurkHackTeam")

### Actualización inmediata
No utiliza caché por lo que es necesario **deshacer o rehacer** cambios. Algunas operaciones pueden registrarse antes en la base de datos que en el log.

> Nota: Oracle usa actualización inmediata con 2 logs.

### Puntos de recuperación y *rollback* de instrucción
Los puntos de recuperación (*savepoint*) hacen referencia a instrucciones específicas entre *commit* y *commit* a los que se puede regresar en vez de realizar un *rollback* y perder todo el progreso de la transacción.

La base de datos suele utilizar un *rollback* a nivel de **instrucción** por lo que **escribir contexto transaccional en operaciones únicas** resulta innecesario.

> Ct: Los puntos de recuperación son poco usados en el entorno profesional.

### Diario del sistema (log)
Se guardan en disco dado que, de lo contrario, podría perderse la información por algún imprevisto en **memoria no persistente**. Hay 5 tipos de registros en el log:
- `start_transaction, T`
- `write_item, T, X, <valor_anterior>, <valor_actual>`
- `read_item, T, X`
- `commit, T`
- `abort, T`

Para deshacer una transacción se lee el diario y se retorna al estado anterior. El proceso consiste en **leer hacia atrás el documento** y realizar las operaciones **actualizando en cascada**.

Para deshacer instrucciones, el sistema debe buscar transacciones efectuadas con **`start_transaction`** sin ***commit***.
\
Para rehacer instrucciones, el sistema debe buscar transacciones no efectuadas con **`start_transacion`** con ***commit***.

#### Puntos de control
No debe confundirse con el punto de recuperación.
\
Los puntos de control se disponene en el **guión** y se incluyen de forma **arbitraria por el sistema gestor de bases de datos**.

Los puntos de control son **globales al diario** y sirven para **confirmar la permanencia** de las últiams operaciones de tal forma que no se desvíen recursos de la base de datos al guión durante la operación.

#### Recuperación en Oracle
Oracle utiliza **actualización inmediata** con dos logs:
- ***redo-records*** guarda en ***redo-logs***. Adicionalmente, almacena valores anteriores por el remanente de transacciones de actualización.
- ***undo-records*** guarda en ***rollback segments*** y RBS. Se almacenan en **memoria primaria** y **encadena datos de misma transacción**.

Los *undo-records* se almacenan en memoria volátil y encadenados por transacción por cuestiones de eficiencia. Por remanente, los *rollback segments* son **reconstruibles** por los *redo-records*.

Nuevamente, en la base de datos no se formalizan cambios hasta que pasen por los *redo-records*.

Los ***redo-records* permitirán rehacer** cambios interrumpidos y los ***undo-records* permitirán deshacer** los cambios que no debieron completarse.

## Aislamiento de transacciones
Pretende controlar en qué medida los datos de una transacción pueden ser modificados o accedidos por otra transacción.
\
Se consideran **niveles de aislamiento** definidos por SQL2:

Nivel de aislamiento | Lectura sucia | Lectura no repetible | Lectura fantasma
:--- | :---: | :---: | :---:
**Lectura no confirmada** | ⚠️ | ⚠️ | ⚠️ |
**Lectura confirmada** | 🛡️ | ⚠️ | ⚠️ |
**Lectura repetible** | 🛡️ | 🛡️ | ⚠️ |
**Serializable** | 🛡️ | 🛡️ | 🛡️ |

- ***read uncommited***
    \
    Se pueden leer los datos no confirmados o sin confirmar, es decir, sin que haya pasado un *commit*.

- ***read commited***
    \
    Solo se pueden leer los datos con *commit* protegiendo la transacción de la **lectura sucia**.

- ***repeteable read***
    \
    Solo se pueden leer datos confirmados y, además, todos los datos de consultas **deben dar el mismo resultado**.

- ***serializable***
    \
    Solo se pueden leer datos confirmados, las consultas deben dar mismos resultados y **trabaja sobre una *"foto"*** de tal forma que la transacción no trabaja sobre la base de datos hasta aportar los resultados.

### Configuración de transacciones
Se especifican con **`SET TRANSACTION <config>`**. Se pueden indicar:
- **modo de acceso**
    - `READ ONLY`
    - `READ WRITE`

    > Nota: *Read only* trabaja sobre una copia serializable.

- **nivel de aislamiento** con `SET TRANSACTION ISOLATION LEVEL`
    - `READ UNCOMMITED`
    - `READ COMMITED`
    - `REPETEABLE READ`
    - `SERIALIZABLE`

    > Nota: En JDBC se omite el "`LEVEL`".

    > Nota: Oracle solo implementa `READ COMMITED` (por defecto) y `SERIALIZABLE`.

### Niveles de aislamiento en Oracle
Solamente proporciona **`READ COMMITED`** Y **`SERIALIZABLE`** por lo que Oracle no tiene riesgo de lectura sucia. EL nivel por defecto es `READ COMMITED`.

Por consecuencia, se debería suponer que `SERIALIZABLE` sea **bloqueante**. No obstante, en Oracle esto no es así. Si un **dato es cambiado durante otra transacción serializable** se le avisa para que lo gestione por medio de un error con el fin de que lo gestione. La transacción serializable sigue trabajando sobre una copia.

Oracle recomienda el uso de **`READ COMMITED`** cuando no pueda suceder el problema, recomienda **`SERIALIZABLE`** cuando la probabilidad de colisión sea baja y recomienda medidas **bloqueantes** cuando la probabilidad de colisión sea alta.

> Nota: Si se da el caso de que una opración seralizable no pueda serializar un cambio porque otra consulta entra en conflicto **se imponen los cambios de toda la transacción salvo que sean conflictivas**. Ello provocaría un error de serialización.

> Nota: Los bloqueos a nivel de instrucción afectan a todo el registro. Esto es necesario para protegerse de la actualización perdida.

### JDCB
Para aplicar el nivel de seguridad se usa **`setTransactionIsolation(...)`**. No obstante, también puede usarse `execute(String)` para lograrlo.
- `setTransactionIsolation` proporciona un nivel de aislamiento para la **conexión**.
- `execute` **pierde el nivel de aislamiento** tras el `commit` o el `rollback`.

### Bloqueos
Los ***locks*** son recursos que permiten reservar recursos a usuarios impidiendo nuevos accesos. Es un medio que **reduce la concurrencia** y muy particuñar según el sistema gestor de bases de datos.
\
Se distinguen, a nivel teórico, tres niveles de bloqueos:

- **Lectura/escritura**

    Una transacción con **bloqueo de lectura** impone una reserva que impide modificar datos. El objetivo es mantener la integridad de la repetición de lectura.
    
    Particularmente, **Oracle no bloquea** la modificación ni lectura propia.
    
    **Ninguna otra transacción podrá leer los registros sin bloquearlo también**, por ello se habla de **bloqueo compartido**. Para evitar otras lecturas se debe usar una **promoción de bloqueo de lectura**.

    Una transacción con **bloqueo de lectura** solo permite una transacción bloqueante y no permite que **nadie lea o escriba** los registros afectados.

- **Granularidad**

    La granularidad permite bloquear entre **tablas**, **tuplas** y **atributos** aunque, a nivel práctico, ningún sistema de gestión proporciona bloqueo a nivel de atributo.
    \
    Es interesante a nivel de eficiencia **bloqueos de mayor grano**. Por ello, si el número de filas es muy grande, algunos sistemas gestores hacen ***lock escalation*** y bloquean toda la tabla.

- **Implícito/explícito**

    Los **bloqueos implícitos** son realizados por el sistema gestor de bases de datos y sirven para la integridad de los datos. Por contraparte, los **bloqueos explícitos** están dados por instrucciones proporcionadas por el usuario.

Los niveles de aislamiento se relacionan con el uso de *locks*:
- `READ UNCOMMITED`:
    - *locks* liberados **tras la operación**
- `READ COMMITED`:
    - *locks* de **escritura** liberados **tras la transacción**
    - *locks* de **lectura** liberados **tras la operación**
- `REPETEABLE READ`:
    - *locks* se liberan **tras la transacción**
- `SERIALIZABLE`:
    - algunos sistemas gestores **bloquean toda la tabla** o **bloquean los índices**
 
En resumen:

criterio | tipo | descripción
:-- | :--  | :--:
lectura/escritura | lectura | Impide la escritura y es compartido.
lectura/escritura | escritura | Impide la lectura y es exclusivo.
granularidad | campo | No se suele implementar.
granularidad | fila | Puede escalar a granularidad de tabla en un proceso de *lock escalation*.
granularidad | tabla | Se pierde menos espacio en almacenamiento de sobre el *lock*.
implícito/explícito | implícito | Lo realiza el sistema gestor en sus operaciones.
implícito/explícito | explícito | Se indica de forma explícita por el usuario.

#### Bloqueos en Oracle
Sigue dos principios:
- **lectores no bloquean a escritores**
- **escritores no bloquean a lectores**

Esto se logra por medio de la **consistencia de lectura** para casos de lectura y escritura simultánea. Para esto se utilizan los **rollback segments**.
\
Los rollback segments almacenan un ***system change number*** (SCN) asociado al valor del atributo. Si la transacción tiene un SNC inferior al último valor almacenado entonces dicho valor se ignora y se **recupera el último valor previo al SNC** de la transacción. Hay **consistencia de lectura a nivel de operación y de transacción**. Este proceso es fundamental para las *"fotos"* del `SERIALIZABLE`.

En resumen, en Oracle:

tipo | descripción
:--  | :--:
`ROW SHARE` | Intención de modificación. Impide bloqueos `EXCLUSIVE`.
`ROW EXCLUSIVE` | Se adquiere con órdenes de modificación. Impide bloqueos de otros tipos.
`SHARE` | Únicamente impide modificación.
`SHARE ROW EXCLUSIVE` | Similar a `ROW EXCLUSIVE` pero es un *lock* exclusivo.
`EXCLUSIVE` | Sólamente permite consultas. Impide el resto de operaciones, incluidos bloqueos.

#### Bloqueo implícito en Oracle DML
Es un bloqueo exclusivo (para lectura) hasta confirmada o deshecha la transacción.

Se ilustra mejor con un ejemplo:

tiempo | 1 | 2 | 3
---: | :---: | :---: | :---:
$T_1$ |  | update |  
$T_2$ | update |  | finalizar 

Veamos los casos quese pueden dar:
- Si se **deshace** $\bold{T_2}$ entonces $T_1$ se ejecutará en el tercer tiempo cuando $T_2$ termine.
- Si se **efectúan los cambios** el resultado dependerá del nivel de aislamiento:
    - Si es `READ_COMMITED` se efectuará tras el tiempo 3.
    - Si es `SERIALIZABLE` obtendremos un error de serialización.

> Nota: En las transparencias se pueden encontrar ejemplos muy reveladores

#### Bloqueo implícito en Oracle DDL
Los bloques DDL utilizan también bloqueos por lo que **no pueden haber dos usuarios concurrentes editando la estructura** de una tabla.
\
Se distinguen tipos:
- ***Shared***: se pueden modificar **datos** pero no estructuras. Se utiliza en la creación de vistas.
- ***Exclusive***: no se permite ningún tipo de modificación. Es la más común en DDL.

#### Bloqueos explícitos en Oracle
Hay 5 tipos de bloqueos. Para llamarlos se utiliza:
`LOCK TABLE <tablas> IN <lockmode> MODE [NOWAIT/WAIT]`
> Nota: La cláusula `WAIT` funciona de tal manera que establece un tiempo de espera en el caso de que el recurso ya estuviera bloqueado por otra transacción. Utilizar `NOWAIT` intentará hacer uso del recurso aunque esté bloqueado dando un error instantáneamente en el caso de que lo esté lo que permite evitar *deadlocks* o largos tiempos de espera ya que, por defecto, se suspende la transacción hasta poder realizarse.

Oracle **nunca impide la lectura**.
De los modos de bloqueos solamente interesan 2 de cara al curso:
- *Shared*
- *Exclusive*

Para realizar un **bloqueo explícito por registro** se utiliza un `SELECT` con una cláusula adicional `FOR UPDATE [NOWAIT/WAIT]`. Es un bloqueo exclusivo que afecta a los registros que se obtienen tras ejecutar la consulta.

Esto significa que se puede **simular `REPETEABLE_READ`** utilizando un `SELECT` con un **bloqueo de sólo lectura** o con un **bloqueo explícito por registro**, aunque lo recomendable es **evitar el uso de bloqueos** en favor del aislamiento `SERIALIZABLE`.
> Puede ser rentable usar el bloqueo cuando la probabilidad de que se produzca un error de serialización sea alta y ello evite recibir muchos errores.

### *Deadlock*
Un ***deadlock*** ocurre cuando **dos transacciones se bloquean entre ellas**. Por ejemplo, dos transacciones cruzadas cambiando un atributo de dos registros.

En tal caso, el sistema gestor, Oracle al menos, **envía un error a alguna de las transacciones** indicando la detección de un *deadlock*. Esta transacción no se ejecuta y, en cambio, se ejecuta la otra.

Para evitar *deadlocks* se utilizael **Two Phase Locking**:
1. Fase 1: **Expansión**
    \
    Se bloquean todos los recursos que se van a utilizar.
2. Fase 2: **Contracción**
    \
    Se liberan los recursos gradualmente tras su uso.

### Transacciones autónomas
A veces, una transacción debe iniciar otra **subtransacción** que debe ejecutarse de forma autónoma.

### Concurrencia optimista
Consiste en intentar **evitar bloqueos** proporcionando **soluciones que detecten** el error susceptible.

En ciertos casos, lo comun es usar un **campo timeStamp** que proporcione el **momento de último cambio**. Para ello, se **requiere que la tabla tenga un campo timeStamp**. Al momento del `UPDATE`, por ejemplo, se puede revisar si el timeStamp corresponde al adecuado evitando así situaciones de actualización perdida.

# TEMA 5: Técnicas de Mapeo Objeto-Relacional
Un ORM es una herramienta, framework o técnica de programación encargado de mapear entidades relacionales de bases de datos a objetos de orientación a objetos. No obstante, en la práctica, también proporcionan técnicas para objetos NoSQL.

Entre los ORM de Java se encuentra **JPA**.

## Impedance Mismatch
Hace referencia a las diferencias de mundos que impiden la correspondencia directa entre el mundo de los objetos de Orientación a Objetos y las tablas SQL:
- **Granularidad**
    > eg: algo que sea un atributo en SQL y un objeto en Orientación a Objetos
- **Herencia**
    > eg: relativo a implementación de herencia de nivel conceptual a físico 
- **Identidad**
    > eg: si no se reescribe equals(Object):boolean de Java
- **Asociación**
- **Navegación**
    > Nota: Se puede hablar de las $n+1$ transacciones de OML

## ORM
ORM pretende aportar persistencia de forma **automáticay transparente**. Para ello se utiliza metainformación de mapeo logrando que solo se tenga que realizar el ejercicio **una única vez**.

Se componen de:
- **API** para operaciones CRUD.
- **API** para consultas sobre clases.
- Medio para especificar **metadatos de mapeo**.
- Tácnicas de **optimización**.

El mayor problema de OMR es que suele hacer falta analizar si es rentable su uso para la casuística determinada.

## JPA
En esta asignatura se utiliza JPA por su **capacidad de abstracción** que proporciona múltiples implementaciones para distintos sitemas gestores de bases de datos.

En su creación se aprovechó de los ORMs existentes para integrar ventajas de otros OMRs.

Utiliza la **persistencia basada en POJOs** (objetos planos con su constructor, getters y setters). No se espera que las clases tengan ninguna caracterísitca particular.

JPA trabaja sobte **clases y sus propiedades** por lo que la cláusula JPA `SELECT atributo FROM Clase` está buscando un **atributo `atributo`** de la **clase `Clase`** siendo el lenguaje sensible a mayúsculas y minúsculas.
\
Es importante tener en cuenta que **las consultas no se realizan sobre la base de datos**.

Para mapear clases con tablas se puede usar **XML** o **anotaciones** sobre el código. Cada una proporciona sus ventajas e inconvenientes.
> eg: en el siguiente ejemplo el `@Override` corresponde a una anotación
> ```java
> @Override
> public String toString() { . . . }
> ```
