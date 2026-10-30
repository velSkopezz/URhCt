---
title: Threads & Streams
author: Christian Velasco Pérez
---

# **Threads & Streams**

*Autor:* Christian Velasco Pérez <img src="../assets/skpz.jpg" alt="Skopez" align="right" style="width:15%; margin-left:4%;margin-bottom:2%">
\
El siguiente contenido cumple con el propósito de proporcionar información que, si bien pueden encontrarse entre los distintos documentos, aquí se reúnen en retrospectiva y pretendiendo maximizar la comprensión de los contenidos.
\
La distribución del documento queda reservada al permiso explícito de su autor. Si necesitase información de contacto puede [enviar un correo](mailto:velskopezz@gmail.com).

# **Streams**

Un *stream* es una secuencia de datos disponibles a lo largo del tiempo. Estos datos serán, en todos los casos, ***byte**s* ya sea en mayor o menor nivel.

# Streams en C++

Normalmente, se incluyen por medio de [`<iostream>`](https://es.cppreference.com/cpp/io), que incluyen distintas clases del `namespace` `std` utilizados con frecuencia.
\
Es por ello que, en los textos que los IDEs suelen proporcionar un texto por defecto para ficheros de C++, se suele comenzar incluyendo dicha librería.

> e.g.:
>
> ```cpp
> #include <iostream>
>
> using namespace std
> int main() {
>     cout << "Hello World!" << endl;
>     return 0;
> }
> ```
>
> En este caso, `cout` es un objeto de clase `ostream`.

> Para información con mayor accesibilidad véase [`<iostream>` en Wikipedia](https://es.wikipedia.org/wiki/Iostream)

Todos los *streams* se conectan a un **recurso virtual** (e.g.: descriptor de archivo, en Unix para archivos). De esa forma, funcionan de forma opaca al programador.

La mayoría de clases de *streams* en C++ corresponden a una abstracción de otra clase. Para ello se utiliza el `typedef`:

```cpp
typedef basic_istream<char> istream;
typedef basic_ostream<char> ostream;
typedef basic_ifstream<char> ifstream;
typedef basic_ofstream<char> ofstream;
```

## `std::ostream`

Es la clase por defecto de salida de caracteres. Se trata de una abstracción, en específico `std::basic_ostream<char>` utilizando [*templates*](https://en.cppreference.com/cpp/language/templates).

Las clases de tipo *stream* de salida tienen un método `ostream& flush()` (devuelve el propio objeto) que fuerza el envío de datos.

> El objeto `cout` es de tipo `ostream`.

## `std::istream`

Es la clase por defecto de entrada de caracteres. Se trata de una abstracción, en específico `std::basic_istream<char>` utilizando [*templates*](https://en.cppreference.com/cpp/language/templates).

> El objeto `cin` es de tipo `istream`.

### `std::ofstream` y `std::ifstream`

Son las clases por defecto que proporciona [`<fstream>`](https://es.cppreference.com/cpp/header/fstream). Funcionan de forma similar a las de entradas por defecto de datos, incluyendo el hecho de ser abstracciones de `std::basic_ofstream<char>` y de `std::basic_ifstream<char>` respectivamente.

# Streams en Java

Se importarán por medio de distintas clases y paquetes puesto que se utilizan clases que heredan de las más básicas y que proporcionan funcionalidad específica. Muchas de ellas funcionarán por medio de filtros. Además, suma tener en cuenta que Java se especializa por correr dentro de una máquina virtual ([JVM](https://es.wikipedia.org/wiki/M%C3%A1quina_virtual_Java)) por lo que, a diferencia de otros lenguajes como C++, no hace falta valorar distintas formas de utilizar un *stream* en condición del sistema operativo para el que se destine el programa.

### InputStream y OutputStream

Pertenecen al paquete `java.io` que proporciona funcionalidad de entrada y salida. Son clases básicas y muy presentes en otras clases como [`java.net.Socket`](https://docs.oracle.com/javase/8/docs/api/java/net/Socket.html).

Ambas clases deben **cerrarse tras su uso** por el método `close(): void`. Esto lleva a que todas las clases hijas o que funcionen como filtro deban cerrarse también con el mismo método o similar.

## [`java.io.InputStream`](https://docs.oracle.com/javase/8/docs/api/java/io/InputStream.html)

Es la más básica de las clases para la entrada de datos. Soporta flujo de *bytes* en los siguientes tres métodos principales.

- [**`public abstract int read() throws IOException`**](https://docs.oracle.com/javase/8/docs/api/java/io/InputStream.html#read--)
  - `returns int`: Devuelve el siguiente *byte* o `-1` si no se lee nada.

- [**`public int read(byte[] b) throws IOException`**](https://docs.oracle.com/javase/8/docs/api/java/io/InputStream.html#read-byte:A-)
  \
  Toma los datos y los introduce en el *array* de *bytes*.
  - `byte[] b`: Los datos.
  - `returns int`: Devuelve la cantidad de *bytes* leídos.
  
- [**`public int read(byte[] b, int off, int len) throws IOException`**](https://docs.oracle.com/javase/8/docs/api/java/io/InputStream.html#read-byte:A-int-int-)
  \
  Toma los datos y los introduce en el *array* de *bytes*.
  - `byte[] b`: Los datos.
  - `int off`: De *offset*, indica el inicio donde se escribe en el *array*.
  - `int len`: De *length*, indica la cantidad de *bytes* que se leen. Por consiguiente, se lee desde `off` hasta `off + len`.
  - `returns int`: Devuelve la cantidad de *bytes* leídos. Nótese que podría leer menos que `len` *bytes*.

## [`java.io.OutputStream`](https://docs.oracle.com/javase/8/docs/api/java/io/OutputStream.html)

Es la más básica de las clases para la salida de datos. Soporta flujo de *bytes* en los siguientes tres métodos principales.

- [**`public abstract void write(int b) throws IOException`**](https://docs.oracle.com/javase/8/docs/api/java/io/OutputStream.html#write-int-)
  - `int b`: Escribe el *byte*.

- [**`public void write(byte[] b) throws IOException`**](https://docs.oracle.com/javase/8/docs/api/java/io/OutputStream.html#write-byte:A-)
  \
  Envía los datos.
  - `byte[]`: Los datos.
 
- [**`public void write(byte[] b, int off, int len) throws IOException`**](https://docs.oracle.com/javase/8/docs/api/java/io/OutputStream.html#write-byte:A-int-int-)
  \
  Envía los datos.
  - `byte[] b`: Los datos.
  - `int off`: De *offset*, indica el inicio donde se escribe en el *array*.
  - `int len`: De *length*, indica la cantidad de *bytes* que se escriben. Por consiguiente, se escribe desde `off` hasta `off + len`.

- [**`public void flush()`**](https://docs.oracle.com/javase/8/docs/api/java/io/OutputStream.html#flush--)
  \
  Los *streams* pueden esperar antes de enviar los datos. Este método fuerza el envío de datos.

## [`java.io.FileInputStream`](https://docs.oracle.com/javase/8/docs/api/java/io/FileInputStream.html) y [`java.io.FileOutputStream`](https://docs.oracle.com/javase/8/docs/api/java/io/FileOutputStream.html)

Su funcionamiento es análogo a `java.io.InputStream` y `java.io.OutputStream`. Su mayor diferencia es que, en su constructor, se indica el fichero del flujo por medio de clase `java.lang.String` con la ruta del archivo o por clase `java.io.File`, entre opciones.

## [`java.io.DataInputStream`](https://docs.oracle.com/javase/8/docs/api/java/io/DataInputStream.html)

Funciona por medio de filtro y es clase hija de `java.io.InputStream`. Proporciona varios métodos que aportan funcionalidad para enviar datos abstractos por *streams*.

El método [`readLine(): String`](https://docs.oracle.com/javase/8/docs/api/java/io/DataInputStream.html#readLine--) lee cadenas de texto. No obstante, es un método obsoleto puesto que no trabaja correctamente con codificaciones de texto.

> e.g.: Obtener texto de un `DataInputStream`
> Sea `is` una variable de tipo `java.io.InputStream`.
> 
> ```java
> String text;
> try (DataInputStream dis = new DataInputStream(is)) {
>     while ((text = is.readLine()) != null) {
>         text += "\r\n";
>     }
> } catch (IOException ioe) {
>     ioe.printStackTrace();
> }
> ```
>
> > Se ha aprovechado que `InputStream` implementa [`AutoCloseable`](https://docs.oracle.com/javase/8/docs/api/java/lang/AutoCloseable.html) para utilizar un [*try-with-resources*](https://docs.oracle.com/javase/tutorial/essential/exceptions/tryResourceClose.html).
> 
> > Nótese que el método **`readLine(): String` excluye el carácter de fin de línea**.

## [`java.io.DataOutputStream`](https://docs.oracle.com/javase/8/docs/api/java/io/DataOutputStream.html)

Funciona por medio de filtro y es clase hija de `java.io.OutputStream`. Proporciona varios métodos que aportan funcionalidad para enviar datos abstractos por *streams*.

El método [`writeBytes(String s): void`](https://docs.oracle.com/javase/8/docs/api/java/io/DataOutputStream.html#writeBytes-java.lang.String-), lejos de lo que pudiera parecer, envía `String`s, no `byte`s.

> - El método [`writeChars(String s): void`](https://docs.oracle.com/javase/8/docs/api/java/io/DataOutputStream.html#writeChars-java.lang.String-) envía caracteres línea a línea.
> - El método [`writeUTF(String str): void`](https://docs.oracle.com/javase/8/docs/api/java/io/DataOutputStream.html#writeUTF-java.lang.String-) utiliza una **modificación de UTF-8** propia de Java.

> e.g.: Enviar un texto con un `DataOutputStream`
> Sea `os` una variable de tipo `java.io.OutputStream`.
> 
> ```java
> String text = "Hello World!";
> try (DataOutputStream dos = new DataOutputStream(os)) {
>     dos.writeBytes(text);
>     dos.flush();
> } catch (IOException ioe) {
>     ioe.printStackTrace();
> }
> ```
>
> > Se ha aprovechado que `OutputStream` implementa [`AutoCloseable`](https://docs.oracle.com/javase/8/docs/api/java/lang/AutoCloseable.html) para utilizar un [*try-with-resources*](https://docs.oracle.com/javase/tutorial/essential/exceptions/tryResourceClose.html).
> 
> > Nótese que se ha utilizado **`flush(): void` para garantizar el envío** de la información. Esto será importante para evitar bloqueos.

## [`java.io.PrintStream`](https://docs.oracle.com/javase/8/docs/api/java/io/PrintStream.html)

Funciona a modo de filtro de un `java.io.OutputStream` aunque también se le puede proporcionar un `java.io.File` o una `java.lang.String` para abrir un *stream*.

> `System.out` es un objeto de tipo `java.io.PrintStream`

## [`java.util.Scanner`](https://docs.oracle.com/javase/8/docs/api/java/util/Scanner.html)

Funciona a modo de filtro de un `java.io.InputStream` aunque también se le puede proporcionar un `java.io.File` o una `java.lang.String` para abrir un *stream*.

> e.g.: Leer texto de la entrada del sistema.
>
> ```java
> Scanner sc = new Scanner(System.in);
> String text = sc.nextLine();
> ```
>
> > Nótese que no se ha utilizado el método `close(): void` porque el recurso `System.in` se cerrará junto con el proceso.
> > \
> > Si fuera otro recurso requeriría de un cierre.

## [`java.io.BufferedReader`](https://docs.oracle.com/javase/8/docs/api/java/io/BufferedReader.html)

Es una clase **especializada en datos de texto** que funciona a modo de filtro de `java.io.Reader`s. A estos últimos, se les puede añadir, en su constructor, un *encoding* como parámetro.

Esta clase toma del *stream* los datos de lectura y un **margen adicional en un *buffer***. Esto la hace **mucho más veloz que `java.io.DataInputStream`** aunque también impide la lectura de datos que no sean texto así como **impide su uso en *sockets***.

> e.g.: Mostrar un archivo desde un `BufferedReader`.
>
> ```java
> try (BufferedReader br = new BufferedReader(new InputStreamReader(new FileInputStream("archivo.txt"), StandardCharsets.UTF_8))) {
>     String linea;
>     while ((linea = br.readLine()) != null) {
>         System.out.println(linea);
>     }
> } catch (Exception e) {
>     e.printStackTrace();
> }
> ```

## [`java.io.BufferedWriter`](https://docs.oracle.com/javase/8/docs/api/java/io/BufferedWriter.html)

Es una clase **especializada en datos de texto** que funciona a modo de filtro de `java.io.Writer`s. A estos últimos, se les puede añadir, en su constructor, un *encoding* como parámetro.

> e.g.: Enviar un texto desde un `BufferedWriter`.
>
> ```java
> try (BufferedWriter writer = new BufferedWriter(new FileWriter("archivo.txt"))) {
>     writer.write("Hola, mundo!");
>     writer.newLine();
>     writer.flush();
> } catch (IOException e) {
>     e.printStackTrace();
> }
> ```
> 
> > Nótese que existe el método `newLine(): void`. Este método se asegura de **añadir una línea compatible con el sistema operativo** (e.g.: Unix utiliza `\n`, Windows utiliza `\r\n`, los Mac clásicos utilizan `\r`...).

# **Threads**

Un *thread* es una secuencia de instrucciones que pueden ser ejecutadas por un computador. A diferencia de los procesos, los *threads* comparten la imagen del proceso.

Si bien los *threads* son una gran ventaja, puesto que permiten la **ejecución paralela**, provocan graves problemas de concurrencia: el programador no puede controlar el orden de ejecución de un *thread* ni si termina su ejecución antes que otro.

### *Daemon*

Un *daemon* es un *thread* que continúa su ejecución, y la del programa con él, a pesar de que el hilo principal ya ha terminado su ejecución. Se excluye de la definición a aquellos *threads* que deban ejecutarse tras el hilo principal por propósitos del programa.

# Threads en C++

Se utiliza la clase [`std::thread`](https://es.cppreference.com/cpp/header/thread) para la que se debe incluir [`<thread>`](https://en.cppreference.com/cpp/thread/thread/join). Se puede utilizar el método [`join(): void`](https://en.cppreference.com/cpp/thread/thread/join) para esperar al *thread*.

> e.g.: *Thread*s en C++.
>
> ```cpp
> #include <thread>
>
> void function(int arg) { /* . . . */ }
>
> int main() {
>     std::thread th1(function, 42);
>     return 0;
> }
> ```

# Threads en Java

Se van a proporcionar múltiples clases e interfaces para proporcionar *threads* de forma sencilla, o bien, solventar problemas para aprovechar las funcionalidades de Java.

## [`java.lang.Thread`](https://docs.oracle.com/javase/8/docs/api/java/lang/Thread.html)

Requiere que se sobreescriba e implemente el método [`run(): void`](https://docs.oracle.com/javase/8/docs/api/java/lang/Runnable.html#run--) de la interfaz `Runnable`. Se ejecuta con el método [`start(): void`](https://docs.oracle.com/javase/8/docs/api/java/lang/Thread.html#start--).

> e.g.: Uso de `Thread`.
>
> ```java
> Thread th = new Thread() {
>     @Override
>     public void run() { /* . . . */ }
> }
> th.start();
> ```

### Paso de parámetros con `Thread`

Pasar parámetros de retorno con `Thread` requiere añadir métodos adicionales. Aunque se recomienda utilizar `Callable<V>`y `Future<V>`, es posible lograr la misma funcionalidad con un `Thread`.

> e.g.: Paso de parámetros con un `Thread`
>
> ```java
> public class Hilo extends Thread {
>    private Object in_Parameter;
>    private Object outParameter;
>    private Exception throwable;
>
>    public Hilo(Object input) {
>        super();
>        this.in_Parameter = input;
>    }
>    public void run() {
>        try {
>            /* . . . */
>        } catch (Exception e) {
>            this.throwable = e;
>        }
>    }
>    public Object getResult() throws Exception {
>        if (this.throwable != null) { throw this.throwable; }
>        return this.outParameter;
>    }
> }
>
> public class Main {
>    public static void main(String[] args) {
>        Object in = new Object();
>        Object result = null;
>        Hilo th = new Hilo(in);
>        th.start();
>        try {
>            th.join();
>            result = th.getResult();
>        } catch (Exception e) {
>            e.printStackTrace();
>        }
>        /* . . . */
>    }
> }
> ```
>
> > Nótese que una excepción es un objeto [`java.lang.Exception`](https://docs.oracle.com/javase/8/docs/api/java/lang/Exception.html) que funciona como cualquier otra clase.

## [`java.lang.Runnable`](https://docs.oracle.com/javase/8/docs/api/java/lang/Runnable.html)

El objetivo es poder crear clases de *threads* que permitan heredar de otras clases. El funcionamiento requiere instanciar un `java.lang.Thread`.

> e.g.: Uso de `Runnable`.
>
> ```java
> public class Hilo implements Runnable {
>     @Override
>     public void run() { /* . . . */ }
> }
>
> public class Main {
>     public static void main(String[] args) {
>         Hilo hilo = new Hilo();
>         Thread th = new Thread(Hilo);
>         th.start();
>     }
> }
> ```
