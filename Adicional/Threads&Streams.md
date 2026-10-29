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

##
