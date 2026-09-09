---
title: Diseño Tecnológico de Sistemas de Información
author: Christian Velasco Pérez
---
# **Diseño Tecnológico de Sistemas de Información**
*Autor:* Christian Velasco Pérez <img src="../assets/skpz.jpg" alt="Skopez" align="right" style="width:15%; margin-left:4%;margin-bottom:2%">
\
El siguiente contenido corresponde a un **apoyo** educativo para cualquier interesado y por eso puede contener fallos. El documento está orientado al curso de *Diseño Tecnológico de Sistemas de Información* del Grado en Ingeniería Informática de la Universidad de La Rioja y se considera completa responsabilidad del lector lo que haga con la información de este documento.
\
La distribución del documento queda reservada al permiso explícito de su autor. Si necesitase información de contacto puede [enviar un correo](mailto:velskopezz@gmail.com).

# TEMA 1: Programación orientada a Aspectos
El objetivo es **secularizar el manejo de errores** del módulo donde surgen para reunirlos en un único apartado.

## Elementos
El siguiente apartado trata el conjunto de componentes que se deben considerar en un sistema POA:

- **Componentes**
    \
    Son la parte de un módulo que interesa a nivel funcional.
- **Aspectos**
    \
    Refiere a aquello relativo a aspectos no funcionales como el control de errores o de acceso.

> Nota: Las transparencias hablan de
> - *Core concern*: Unidad encapsulable limpiamente.
> - *Cross-cutting concern*: Atraviesa diferentes módulos.

## Pasos a seguir
1. Se programan las **componentes** con normalidad. Seguido, se hacen los **aspectos** del código de forma **independiente entre ellos**.
2. Se utiliza el **weaver** para combinar la componente y el aspecto antes de la ejecución del programa.

## Conceptos básicos
> Sobre el documento: Probablemente falten por añadir. Avisar en Issues.

- **`joinpoint`**
    \
    Es un punto identificable del programa en el que se puede **añadir un comportamiento adicional**, por ejemplo, una llamada.
- **`advice`**
    \
    Delata el salto de un **punto de enlace**. Hay tres tipos:
    - `before`, antes.
    - `after`, después.
    - `around`, en su lugar.
- **`pointcut`** es el conjunto de todos los **puntos de enlace** que se utilizan para definir el momento de ejecutarse un **advise**.

## AspectJ
Fue inicialmente desarrollado por Xerox en 1998. Aunque también tiene crosscutting dinámico, en la asignatura se utilizará el estático.

Se pueden utilizar **anotaciones** (`@`) **o keywords**. Se distinguen:
- **`pointcut`s**: para puntos de corte.
- **`Logger`**: para el registro de los eventos.

Lo interesante de la cuestión es la **definición de puntos de corte**. Véanse ejemplos en las transparencias.