---
title: Sistemas Distribuidos
author: Christian Velasco Pérez
---
# **Sistemas Distribuidos**
*Autor:* Christian Velasco Pérez <img src="../assets/skpz.jpg" alt="Skopez" align="right" style="width:15%; margin-left:4%;margin-bottom:2%">
\
El siguiente contenido corresponde a un **apoyo** educativo para cualquier interesado y por eso puede contener fallos. El documento está orientado al curso de *Sistemas Distribuidos* del Grado en Ingeniería Informática de la Universidad de La Rioja y se considera completa responsabilidad del lector lo que haga con la información de este documento.
\
La distribución del documento queda reservada al permiso explícito de su autor. Si necesitase información de contacto puede [enviar un correo](mailto:velskopezz@gmail.com).

De acuerdo con los temas 1 y 3, es posible enocntrar información mejor organizada en el documento [*Threads&Streams*](../adicional/Threads&Streams.md), en los documentos adicionales.

# TEMA 1: Entrada/Salida en Java

## Streams

El **stream** es una conexión por la que viaja un flujo de **bytes**. Los streams existen por igual en todos los lenguajes y deben **cerrarse** tras su uso.

> Cita: Es pregunta de examen qué viaja por un stream (Respuesta: bytes).

## [`OutputStream`](https://docs.oracle.com/javase/8/docs/api/java/io/OutputStream.html)

- `close(): void`; cierra el stream
- `flush(): void`; envía los datos y los libera de la queue
- `write(int): void`; envía el valor numérico del byte a la queue
- `write(byte[]): void`; envía los bytes a la queue
- `write(byte[], int, int)`; envía los bytes desde el byte indicado hasta la cantidad que se indique respectivamente

## [`FileOutputStream`](https://docs.oracle.com/javase/8/docs/api/java/io/FileOutputStream.html)

Es una subclase similar a `OutputStream` enfocado en **escribir ficheros**. Es por ello que su método `write(int[]): void` funciona de forma similar.

## [`DataOutputStream`](https://docs.oracle.com/javase/8/docs/api/java/io/DataOutputStream.html)

Es un filtro que proporciona métodos para tratar con datos de forma lógica en vez de usar bytes.

> Entre sus métodos, `writeBytes(String): void` trata con Strings.

> El método para caracteres y UTF es desaconsejado por el profesor:
> - El primero envía los caracteres línea a línea.
> - El segundo, lejos de utilizar UTF-8, utiliza un UTF específico de Java.

Se usa de acuerdo con el siguiente ejemplo:
```java
DataOutputStream dos = new DataOutputStream(new OutputStream());
```

## [`PrintStream`](https://docs.oracle.com/javase/8/docs/api/java/io/PrintStream.html)

`System.out` es de tipo `PrintStream`, por ejemplo.

## [`InputStream`](https://docs.oracle.com/javase/8/docs/api/java/io/InputStream.html)

Los métodos funcionan de forma análoga a los de `OutputStream`, reemplazando las palabras `write` por **`read`**. En lugar de `void`, devuelven un **`int` con la cantidad de bytes** recibidos. Salvo, por supuesto, `read(byte[]): int`, que devuelve `-1` en caso de error.

> Si no queda lo suficientemente claro me lo hacéis saber.

## [`FileInputStream`](https://docs.oracle.com/javase/8/docs/api/java/io/FileInputStream.html)
Análogo. Es más lento que `BufferedReaded`.

## [`SequenceInputStream`](https://docs.oracle.com/javase/8/docs/api/java/io/SequenceInputStream.html)

## [`DataInputStream`](https://docs.oracle.com/javase/8/docs/api/java/io/DataInputStream.html)

Análogo. Utiliza `readLine(): String` para leer una línea.

## [Reader](https://docs.oracle.com/javase/8/docs/api/java/io/Reader.html)s y [Writer](https://docs.oracle.com/javase/8/docs/api/java/io/Writer.html)s

Debido al encoding, se utilizan para que el paso de los caracteres sea correcto. Aunque los caracteres de ASCII no suelen dar problemas, vale la pena tener esto en cuenta.
\
Para ello, se utilizan clases como [**`BufferedReader`**](https://docs.oracle.com/javase/8/docs/api/java/io/BufferedReader.html), por ejemplo, como **filtros de clase**.

## Try with Resources

Se cierran en orden inverso a la declaración. Se usa de la siguiente forma, como ilustra el ejemplo.
```java
try (FileInputStream ifile = new FileInputStream(ipath);
    FileOutputStream ofile = new FileOutputStream(opath);
    /* . . . */) {
    // bloque de código
} catch (FileNotFoundException fnfe) {
    fnfe.printStackTrace();
} catch (IOException ioe) {
    ioe.printStacktrace();
}
// no hace falta un bloque finally
```

## [`File`](https://docs.oracle.com/javase/8/docs/api/java/io/File.html)

Representa los archivos a un nivel exterior. Su objetivo es proporcionar los **metadatos** del archivo.

## Serialización

Para ello se facilita el método `readOject(): Object` que permite obtener objetos de flujos que implementan la interfaz `Serializable`.

Al fichero se envía el **estado del objeto**, no sus métodos puesto que son generalizados. Se puede añadir las *keywords* **`transient`** o **`static`** para **evitar que se envíe el atributo en la serialización**.

Los **Object** tienen un atributo lamado **serialVersionUID**. Esta se ve alterada con el cambio de la clase. Se puede forzar de forma arbitraria con una sentencia **`static final long serialVersionUID = [ . . . ]`**. Esto se suele hacer para realizar cambios. Los **métodos** no se guardan a la serialización por lo que no da mucho problema. Los **atributos** se asocian con las que tienen el **mismo nombre** y, si no existiera, se trabaja con su forma de **preinicialización**

> e.g.: la preinicialización de un objeto de clase es `null`, la de los `int` es `0`, la de los `boolean` es `false`... 

# TEMA 2: Programación en red en Java

## [`java.net.InetAddress`](https://docs.oracle.com/javase/8/docs/api/java/net/InetAddress.html)

Es una clase que permite **obtener información de la red**. Se instancia por medio de una factoria: sigue un patrón **Factory**.

- `getHostName(): String`
- `getCanonicalHostName(): String`
- `getHostAddress(): String`
- `getAddress(): byte[]`

## [`Socket`](https://docs.oracle.com/javase/8/docs/api/java/net/Socket.html)

Desde la perspectiva del cliente se puede conectar a un socket (combinación de dirección IP y puerto) usando esta API.

| | **Origen** | **Destino**
--: | :-- | :--
Puerto | `getLocalPort()` | `getPort()`
Dirección | `getLocalInetAddress` | `getInetAddress()`

La información a partir del `Socket` se envía por ***streams***. Esto implica que pueden aplicarse los **mismos filtros que con ficheros** (`DataInputStream`, `BufferedReader`...), lo que también implica que **cerrar el filtro también cierra el *socket*** y, por consiguiente, la conexión.

Respecto a la WorldWideWeb, implica el uso de **HTTP** y **servidores**.

## HTTP

Utiliza URLs, se suele usar para páginas web aunque es un protocolo de transferencia de información para cualquier uso de la **capa de aplicación**.

Funciona de tal manera que **cada respuesta está asociada a una petición** y viceversa, es decir, **varias respuestas requieren varias peticiones**.

> Los comandos más utilizados incluyen:
>
> - `GET`
> - `POST`
> - `PUT`
> - `DELETE`
> - `HEAD`
>
> > `DELETE` es comúnmente rechazado por servidores públicos puesto que el usuario no suele tener la autoridad necesaria para utilizarlo.

No guarda estados aunque permite *jugar* con la información por medio de ***cookies***. De forma coasional, en la URL también puede haber una ***StringQuery*** visible tras un caracter `?` en forma de clave-valor y separados por un '&'.

> e.g.: Google lo utiliza para registrar telemetría.

### Estructura HTTP

![Estructura HTTP](../assets/tutorialspoint_http-message-request.jpg "Estructura HTTP en tutorialspoint.com")

> Hay que evitar leer el tráfico de red con `BufferedReader` puesto que **lee de más** al almacenar parte del mensaje en un *buffer*. `BufferedReader` está específicamente diseñado para leer ficheros y de texto.

### `GET`

La línea de petición se visualiza con el ejemplo: `GET /index.html HTTP/1.1`.

> Es poco común ver cuerpo en `GET` puesto que este comando sirve para obtener información.

Una respuesta puede comenzar con la línea `HTTP/1.1 200 OK`. De ahí, nuevamente puede haber, o no, cuerpo con mensaje.

### Cabeceras destacables

- **`Content-Length`**: longitud del cuerpo del mensaje
- **`Content-Type`**: utiliza **MIME** para indicar el tipo de archivo
- `Date`
- `Referer`
- `User-Agent`
- ...

> Para información adicional sobre `Content-Type` véase la capa de aplicación en [Redes de Computadores](../2º/Redes_de_Computadores.md)

## Herramientas de servidor

### [`ServerSocket`](https://docs.oracle.com/javase/8/docs/api/java/net/ServerSocket.html)

Es una clase que proporciona la posibilidad de abrir un servidor:

- `ServerSocket(int)`; constructor, abre la conexión en el puerto indicado
- `accept(): Socket`; devuelve un `Socket` con el cliente conectado

> El método `accept(): Socket` de `ServerSocket` es un método **bloqueante**, es decir, detendrá el código en ese punto hasta que se conecte un usuario. Para ello existen métodos de *timeout*, aunque lo lógico es utilizar *multithread*.

```java
// Estructura estándar de un servidor en java
try (ServerSocket server = new ServerSocket(INTERNAL_PORT)) {
    while (true) {
        try (Socket client = server.accept()) {
            // ...
        }
    }
}
```

### *Multithread*

Se ve con detenimiento en el próximo tema. Permite el **paralelismo** aumentando rápidamente la velocidad por medio del uso de múltiples núcleso. Se crea un *thread* por cliente y se utiliza un ***pool* de *threads*** para optimizar su creación.

# TEMA 3: Programación concurrente

Es fundamental en **servidores** puesto que es obligatorio para poder tratar con **múltiples clientes** eficientemente. A veces es necesaria también la **comunicación entre hilos**.

> En principio, con $n$ núcleos puedes ejecutar $n$ hilos de forma paralela. No obstante, la tecnología ***hyperthreading*** permite ejecutar $2n$ hilos.

El objetivo es **dividir** las tareas en tanto que sea posible. No obstante, el programador **no tiene control sobre el core al que se delega ni el momento en el que se ejecuta**. Esto se debe a que la tarea de elegir el core forma parte del **planificador del sistema operativo**.

> Tomar un hilo tiene cierto coste que se traduce en pérdida de tiempo. Por ello, hay que evitar hacer *threads* de más.

## Estados de un *thread*

Se identifican cuatro esrados entre los que se desplaza un *thread* deacuerdo con sus subrutinas:

- **nuevo**
- **ejecutable**
- **no ejecutable**
- **muerto**

> La documentación de Java desaconseja forzar la detención de hilos. Esto se hace mediante métodos como `wait()`, `stop()`...

## *Daemons*

Un ***daemon*** es un *thread* que continúa su **ejecución sin que sea necesario** para el programa después de que el *thread* principal termine.

Para cerrar su ejecución tras el final del *thread* principal se puede usar el método **`setDaemon(boolean): void`** que debe uitilizarse **antes de ejecutar `start(): void`** puesto que en ejecución no se revisa el *flag* que activa.

## [`Thread`](https://docs.oracle.com/javase/8/docs/api/java/lang/Thread.html) y [`Runnable`](https://docs.oracle.com/javase/8/docs/api/java/lang/Runnable.html)

Para usar *threads* en Java se requiere **crear una clase que extienda de `Thread`** e implementar su método **run**. Luego, hay que ejecutar el método **`start(): void`**.

```java
public class Hilo extends Thread {
    public void run() {
        /* . . . */
    }
}

public class Main {
    public void main(String[] args) {
        Hilo th = new Hilo();
        th.start()
    }
}
```

Existe otra forma de hacerlo en el caso de que la clase requiriese tener herencia. Para ello, se necesita que **implemente la interfaz `Runnable`**. Esto es así para poder usar clases que ya hereden de ortas. Funciona de forma similar a `Thread` pero se debe instanciar con un filtro `Thread`.

```java
public class Hilo implements Runnable {
    public void run() {
        /* . . . */
    }
}

public class Main {
    public void main(String[] args) {
        Hilo th = new Thread(new Hilo());
        th.start();
    }
}
```

> También se pueden usar **clases anónimas**:
> 
> ```java
> public class Main {
>     public void main(String[] args) {
>         Thread th = new Thread(new Runnable() {
>             public void run() { /* . . . */ }
>         });
>     }
> }
> ```

### Parámetros `Thread` de Java

Para ejecutar un Thread en Java se utiliza **`start(): void`** que ejecuta un **`run(): void`**. Para pasar parámetros es necesario **crear parámetros de clase** y **devolverlos en un *getter*** específico del `Thread` creado. De forma similar se hace cuando es necesario **lanzar excepciones** puesto que el método `run(): void` no tiene `throws` en su cabecera.

```java
public class Hilo extends Thread {
    private Object in_Parameter;
    private Object outParameter;
    private Exception throwable;

    public Hilo(Object input) {
        super();
        this.in_Parameter = input;
    }
    public void run() {
        try {
            /* . . . */
        } catch (Exception e) {
            this.throwable = e;
        }
    }
    public Object getResult() throws Exception {
        if (this.throwable != null) { throw this.throwable; }
        return this.outParameter;
    }
}

public class Main {
    public static void main(String[] args) {
        Object in = new Object();
        Object result = null;
        Hilo th = new Hilo(in);
        th.start();
        try {
            th.join();
            result = th.getResult();
        } catch (Exception e) {
            e.printStackTrace();
        }
        /* . . . */
    }
}
```

### Parada de un `Thread`

Se utilizan distintos métodos para **enviar una señal de interrupción** de tal fomra que el *thread* se **detiene de forma segura**.

> Cita: "Cómo se interrumpe un hilo en Java es pregunta de examen"

Para establecer el control, los *threads* tienen un método **`isInterrupted(): boolean`** que muestra un *flag* que se puede activar con el método **`interrupt(): void`**.

El método `interrupt(): void` no fuerza la interrupción, en su lugar, indica al *thread* que debe cerrarse.
\
El *thread* debe **saber cómo interrumpirse**, de lo contrario, no se interrumpirá ya que el poder de interrupción lo tiene el propio *thread* y no su padre.

> El método `interrupt(): void` puede lanzar **`InterruptedException`** al interrumpir.

### Protección contra concurrencia

El objetivo es evitar problemas de concurrencia como la actualización perdida.

> Para más información sobre problemas de concurrencia véase el temario de [Progrmación de Bases de Datos](../2º/Programación_de_Bases_de_Datos.md).

- **`volatile`**
    \
    Es un modificador poco utilizado. Entre *threads*, siempre lee el último valor modificado de la variable.

- **`synchronized`**
    \
    En un **método**, proporciona **exclusión mútua sobre su instancia**.

    > Hay que destacar que es sobre la instancia. Sobre la siguente clase,
    >
    > ```java
    >   public class Clase {
    >       public Clase() { }
    >       public synchronized void metodo() { /* . . . */ }
    >   }
    > ```
    >
    > y con las siguientes instancias,
    > 
    > ```java
    > Clase instancia1 = new Clase();
    > Clase instancia2 = new Clase();
    > Clase instancia1_2 = instancia1;
    > ```
    > 
    > - Se pueden ejecutar concurrentemente `instancia1.metodo()` e `instancia2.metodo()` puesto que son distintas instancias.
    > - No así como con `instancia1.metodo()` e `instancia1_2.metodo()` porque son la misma instancia.

    > El modificador `synchronized` es **necesario** para crear un **patrón Singleton** (véase [Ingeniería del Software](../2º/Ingeniería_del_Software.md) para más información sobre patrones de diseño).

    También existen **bloques `synchronized`** de forma que todo **un bloque de código tiene asociado un *lock***.

    > E.g.:
    >
    > ```java
    > /* . . . */
    > synchronized (<objeto>) {
    >     /* . . . */
    > }
    > /* . . . */
    > ```

> Estas herramientas deben utilizarse con cuidado pues, por ejemplo, `synchronized` puede llevar a **interbloqueos** (véase Sistemas Operativos para más información sobre *deadlocks*), para más información, véase el ejemplo en las transparencias.

### [`Timer`](https://docs.oracle.com/javase/8/docs/api/java/util/Timer.html) y [`TimerTask`](https://docs.oracle.com/javase/8/docs/api/java/util/TimerTask.html)

Para ejecutar tareeas de forma periódica se puede extender de la clase **`TimerTask`**, que funciona de forma similar a `Thread`.
\
`TimerTask` hereda de `Timer` los métodos imprescindibles para su funcionalidad, son, principalmente, sobrecargas de **`schedule(<args>)`**.

### Colecciones concurrentes

Su objetivo es ser *thread safe*.
- `ArrayList` tiene su forma *thread safe* en `Vector`
- `HashMap` tiene su forma *thread safe*  en `Hashtable`

Hacer una clase *thread safe* tiene su coste en eficiencia.

La librería `java.util.concurrent` proporciona ciertos métodos con colecciones comunes con métodos estándar (e.g.: `List<T> synchronized List<T>(List<T>)`).

Por ejemplo, existen:
- `java.util.HashMap`
- `java.util.concurent.SynchronizedMap`: impide el acceso concurrente
- `java.util.concurrent.ConcurrentHashMap`: permite alternar distintos accesos a la vez

> Cita: La diferencia entre aquellos 3 **es** pregunta de examen.

## *Pool* de *threads*

Crear y destruir hilos es una tarea costosa. Para reducir tiempo, vale la pena abrir unos hilos y dejarles corriendo hasta asignarle una tarea adecuada. para ello, se utiliza un ***pool* de *threads***.

El medio en Java es **`ExecutorService`** y la factoría **`Executors`**.
- **`newFixedThreadPool(int): ExecutorService <<static>>`**
- **`newCachedThreadPool(): ExecutorService <<static>>`**

> Los otros 3 métodos tienen una funcionalidad que se ve mejor proporcionada por las clases `Timer`.

> 1. Crear el *pool* (`ExecutorService`).
> 2. *Try-with-resources* con el `ServerSocket`.
> 3. `while (true)`
> 4. `try`
> 5. `ServerSocket.accept()`
> 6. `ExecutorService.submit( . . . )`

## [`java.util.concurrent.Callable<V>`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/Callable.html) y [`java.util.concurrent.Future<V>`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/Future.html)

Existen para solucionar el **paso de parámetros de `Thread`**. La interfaz utiliza **genéricos** para devolver un tipo de dato. En su lugar, se reescribe el **método `call(): <T>`.

Por otro lado, `Future<V>` proporciona el método **`get(): <T>`** que proporciona el resutlado. Este es un **método bloqueante** pues utiliza **`join(): void`** de Thread de forma interna.

> `ExecutorService` tiene un método para ejecutar múltiples hilos a la vez y de forma bloqueante. Es el método **`invokeAll(Collection<Callable<V>>): List<Future<V>>`.

> Los métodos que llaman a *threads* pueden producir **`InterruptedException`**.

## Sincronizadores

Son herramientas para sincronizar la ejecución de hilos. Se aprovechan de compartir el espacio de memoria.

> Normalmente, son clases conceptuales que funcionan internamente con contador.

### [`Semaphore`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/Semaphore.html)

Guarda una cantidad de *locks* que permiten ejecutar un hilo. Un hilo debe adquirir mediante `acquire(): void` y, al final de su ejecución, debe liberarlo mediante `release(): void`.

Si la cantidad de *locks* se ve agotada se obliga a esperar al *thread* hasta que algún otro ejecute `release(): void`, dejando libre un *lock.*

### [`CountDownLatch`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/CountDownLatch.html)

Su constructor toma como parámetro la cantidad de inicial de la cuenta atrás.

Un *thread* debe ejecutar `countDown(): void` y se esperará por el método bloqueante `await(): void` en otro *thread* hasta que la cuenta atrás sea 0.

### [`CyclicBarrier`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/CyclicBarrier.html)

Permite que múltiples los *threads* esperen al resto por meido del método `await(): void`.

En su constructor se indica la cantidad de *threads* a los que se debe esperar. Una vez alcanzada dicha cantidad de hilos bloqueados en `await(): void`, se liberan.

### Colas bloqueantes

Funcionan de tal forma que se **envía un objeto a una cola**. Si la cola se llena, cualquier *thread* que intente enviar información por la cola se bloquea.

# TEMA 4: Programación avanzada en red

El objetivo es comprender el uso de **clases de alto nivel** para realizar funciones que en temas anteriores se han enseñado con herramientas más rudimentarias.

Para ello, se presentan clases como [**`java.net.URL`**](https://docs.oracle.com/javase/8/docs/api/java/net/URL.html). Esta clase permite el **tratamiento de `Strings`** y proporciona funcionalidad para **conexiones por ULR** por medio de **HTTP** y FTP entre otros.

> Cita: En el examen se puede pedir explícitamente que no se use.

A veces **`java.net.URL`** no permite obtener información que el usuario pudiera necesitar. En cuyo caso, hay clases disponibles como [**`java.net.URLConnection`**](https://docs.oracle.com/javase/8/docs/api/java/net/URLConnection.html).

> Nótese que:
>
> - `java.net.URL` tiene el método `openStream(): InputStream` que proporciona únicamente el *payload* de aplicación.
> - `java.net.URLConnection` tiene el método `openConnection(): URLConnection` que proporciona **todo el contenido** de la capa de aplicación.

## `java.net.URLConnection`

debe tenerse en cuenta el protocolo que se utiliza. Por ejemplo, en HTTP, hay que obtener el **`InputStream`** después del mensaje PUT.

Algunos métodos interesantes pueden ser **`getContentLength(): int`**, **`getContentType(): String`**, **`addRequestProperty(String key, String value): void`** y **`setRequestProperty(String key, String value): void`**.

### CGI

Cierta información tiene cabecera propia (*véase trasparencias*). En `PUT`s se puede requerir, por ejemplo, `Content Length`.

## [`java.net.URLEncoder`](https://docs.oracle.com/javase/8/docs/api/java/net/URLEncoder.html)

Permiten cambiar caracteres indisponibles para URLs (e.g.: espacios, tildes...) por su forma codificada en URLs (e.g.: `%20`).

> Se incluye *proxies*, StringQueries, etc que se pueden usar en el trabajo.

### Cerrar un [`java.net.HttpURLConnection`](https://docs.oracle.com/javase/8/docs/api/java/net/HttpURLConnection.html)

Utilizan el método **`disconnect(): void`** para cerrarlo todo. El método `close: void` no cierra todo aunque, con certeza, el sistema operativo acabará liberando dicho recurso tras pasado el *timeout*.

## Protocolo UDP

Utiliza dos clases principales [**`java.net.DatagramPacket`**](https://docs.oracle.com/javase/8/docs/api/java/net/DatagramPacket.html) y [**`java.netDatagramSocket`**](https://docs.oracle.com/javase/8/docs/api/java/net/DatagramSocket.html). La primera se utiliza para **enviar la información** mientras que la segunda puede **enviar y recibir** por igual.

> El protocolo UDP se proporciona principalmente para el trabajo de la asignatura.

> El protocolo UDP no está orientado a conexión e ignora el orden y y la llegada de los paquetes.

### `java.net.DatagramPacket`

Se construye con un ***buffer* de *bytes*** junto a un **puerto**. Requiere la **dirección** (`InetAddress`) y un **puerto** para enviar la información. Los datos se obtienen con **`getData(): byte[]`**.

### `java.net.DatagramSocket`

Se construye con un **puerto**. Sus métodos son del tipo **`recieve(DatagramPacket): void`** para obtener datos y **`send(DatagramPacket): void`** para enviar.

# TEMA 5: *Extensible Markup Language*

El estándar **XML** es uno entre el subconjunto SBML junto con HTML, entre otros. Permite proporcionar un **contexto a la información**.

Sigue una **estructura jerarquizada** en la que existe una **raíz única** y cada etiqueta tiene una **etiqueta de cierre**.

> Se habla de **documentos estructurados**.

Los documentos XML pueden tener **fijado un estilo**. Para eso se pueden utilizar **DTD**s o **XML Schema**s.

## Documentos XML

La primera línea suele indicar la versión

```xml
<?xml version="1.0" encoding="UTF-8"?>
<root>
    . . .
</root>
```

### Elementos

Son las etiquetas más comunes de XML. No es obligatorio que tengan **contenido** ni tampoco **elementos hijos**.

### Atributos

Se disponen tras un espacio en la etiqueta de la forma `nombre="valor"`. El valor **debe estar rodeado por comillas simples o dobles**.

También puede haber atributos en la etiqueta de cierre.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<root>
    <element key="value">sample</element>
</root>
```

### Referencias a entidades

Es una forma de escribir caracteres reservados (e.g.: `<`, `>`, `&`). Para ello, se escribe un **'&'** y se sigue con un nombre único (e.g.: `&gt`, `&lt`, `&amp` respecto al ejemplo anterior).

### Secciones CDATA

Obliga al *parser* a tomar la sección com texto, ignorando caracteres reservados.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<root>
    <title>sample</title>
    <content>
        <![CDATA[
            SELECT *
            FROM sample
            WHERE condition=true
        ]]>
    </content>
</root>
```

### Documento bien formado

Un documento XML está **bien formado** cuando cumple con las **reglas sintácticas de XML**.