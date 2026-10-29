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

# Streams

Un *stream* es una secuencia de datos disponibles a lo largo del tiempo. Estos datos serán, en todos los casos, ***byte**s* ya sea en mayor o menor nivel.

## Streams en C++

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

### `std::ostream`

Es la clase por defecto de salida de caracteres. Se trata de una abstracción, en específico `std::basic_ostream<char>` utilizando [*templates*](https://en.cppreference.com/cpp/language/templates).

> El objeto `cout` es de tipo `ostream`.

### `std::istream`

Es la clase por defecto de entrada de caracteres. Se trata de una abstracción, en específico `std::basic_istream<char>` utilizando [*templates*](https://en.cppreference.com/cpp/language/templates).

> El objeto `cin` es de tipo `istream`.

### `std::ofstream` y `std::ifstream`

Son las clases por defecto que proporciona [`<fstream>`](https://es.cppreference.com/cpp/header/fstream). Funcionan de forma similar a las de entradas por defecto de datos, incluyendo el hecho de ser abstracciones de `std::basic_ofstream<char>` y de `std::basic_ifstream<char>` respectivamente.




