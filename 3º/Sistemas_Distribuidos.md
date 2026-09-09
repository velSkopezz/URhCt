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

# TEMA 1: Entrada/Salida en Java
## Streams
El **stream** es una conexión por la que viaja un flujo de **bytes**. Los streams existen por igual en todos los lenguajes y deben **cerrarse** tras su uso.

> Ct: Es pregunta de examen qué viaja por un stream (Respuesta: bytes).

## `OutputStream`
- `close(): void` ; cierra el stream.
- `flush(): void` ; envía los datos y los libera de la queue.
- `write(int): void`; envía el valor numérico del byte a la queue.
- `write(byte[]): void`; envía los bytes a la queue.
- `write(byte[], int, int)`; envía los bytes desde el byte indicado hasta la cantidad que se indique respectivamente.

## `FileOutputStream`
Es una subclase similar a `OutputStream` enfocado en **escribir ficheros**. Es por ello que su método `write(int[]): void` funciona de forma similar.

## `DataOutputStream`
Es un filtro que proporciona métodos para tratar con datos de forma lógica en vez de usar bytes.

> Nota: Entre sus métodos, `writeBytes(String): void` trata con Strings.

> Nota: El método para caracteres y UTF es desaconsejado por el profesor:
> - El primero envía los caracteres línea a línea.
> - El segundo, lejos de utilizar UTF-8, utiliza un UTF específico de Java.

Se usa de acuerdo con el siguiente ejemplo:
```java
DataOutputStream dos = new DataOutputStream(new OutputStream());
```
## `PrintStream`
`System.out` es de tipo `PrintStream`, por ejemplo.

## `InputStream`
Los métodos funcionan de forma análoga a los de `OutputStream`, reemplazando las palabras `write` por **`read`**. En lugar de `void`, devuelven un **`int` con la cantidad de bytes** recibidos. Salvo, por supuesto, `read(byte[]): int`, que devuelve `-1` en caso de error.

> Nota: Si no queda lo suficientemente claro me lo hacéis saber.

## `FileInputStream`
Análogo. Es más lento que `BufferedReaded`.

## `SequenceInputStream`

## `DataInputStream`
Análogo. Utiliza `readLine(): String` para leer una línea.

## Readers y Writers
Debido al encoding, se utilizan para que el paso de los caracteres sea correcto. Aunque los caracteres de ASCII no suelen dar problemas, vale la pena tener esto en cuenta.
\
Para ello, se utilizan clases como **`BufferedReader`**, por ejemplo, como **filtros de clase**.

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

## `File`
Representa los archivos a un nivel exterior. Su objetivo es proporcionar los **metadatos** del archivo.

