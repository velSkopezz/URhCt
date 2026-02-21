---
title: Ingeniería del Software
author: Christian Velasco Pérez
---
# Ingeniería del Software
*Autor:* Christian Velasco Pérez <img src="https://iili.io/fpTTGnt.md.jpg" alt="Skopez" align="right" style="width:15%; margin-left:4%;margin-bottom:2%">
\
El siguiente contenido corresponde a un **apoyo** educativo para cualquier interesado y por eso puede contener fallos. El documento orientado al curso de *Ingeniería del Software* del Grado en Ingeniería Informática de la Universidad de La Rioja. Por consiguiente, se considera completa responsabilidad del lector lo que haga con la información de este documento.
\
La distribución del documento queda reservada al permiso explícito de su autor. Si necesitase información de contacto puede [enviar un correo](mailto:velskopezz@gmail.com).


## TEMA 1: Producto
> Ct: No pretende que nos aprendamos las definiciones de memoria

Un **software** es una colección de **programas y documentación**.

Tipos de Software:
- **genérico**: orientado a un público amplio
- **personalizado**: orientado a un cliente que especifica los requisitos

> Eg: un software de uso generalizado es genérico y uno encargado es personalizado.

### Características del software
- elemento lógico
- mayoritariamente cerrado
- desarrollo a medida
- degradación por cambio de infraestructura

> Nota: El software se *degrada*, no se deteriora

---

### Factores de calidad del software
- **Factores externos**: son percibidos por el usuario
- **Factores internos**: son percibidos por el desarrollador

> Eg: un bug corresponde a algo externo y una funcion indocumentada corresponde a un factor interno

### Problemas del desarrollo del software
Sus causas son, fundamentalmente, su **naturaleza lógica**, la **intervención de grupos**, la falta de **comunicación**, un escaso **análisis y diseño**, deficiente **gestión de proyectos**, la resistencia a la **actualización** o ciertos _mitos_.
> Por parte de los encargados
> - creencia en *metodología fija*
> - suposición de *conocimiento de herramientas*
> - creencia en que la *falta de planificación es subsanable* con más recursos

> Por parte del cliente
> - confianza en el desarrollo para *iniciar vagamente*
> - confianza en la *plasticidad* del software

> Por parte del desarrollador:
> - omisión del *mantenimiento* del software
> - omisión de la *documentación*

---

### Ingeniería de requisitos
Se refiere a la *detección* de los **requisitos funcionales** y **no funcionales**. Es común el uso de herramientas estandarizadas como UML (Unified Modeling Language).

### Análisis
Una vez capturados los requisitos, se trata de **identificar las ideas principales** y darles forma.

### Diseño
En esta fase se *visualiza* la **arquitectura del sistema de diseño** y conviene **distinguir en subsistemas**. Es una etapa que incluye el diseño de *interfaces* y, si fuera pertinente, el **diseño de objetos**.

### Implementación
Es el momento de **codificar**. También es el último momento al que se puede aplazar la **elección del lenguaje** y es *fundamental* crear **documentación**.

### Pruebas
El objetivo de esta fase es **detectar la mayor cantidad de errores**, en específico, los intolerables.
1. Pruebas de **unidad**: Se pretende que cada módulo funcione de forma independiente.
2. Pruebas de **integración**: Se pretende que los módulos funcionen entre ellos.
3. Pruebas de **sistema**: Se pretende que todo el *sistema* funcione.

> Eg: un módulo podría ser una subrutina dentro del código del software.

### Mantenimiento
Se orienta al **cambio** en forma de *reparación y adaptación*. Es la fase más larga y costosa.
- Mantenimiento **correctivo**: arreglar errores.
- Mantenimiento **perfectivo**: mejorar el producto.
- Mantenimiento **adaptativo**: adoptar cambios.
- Mantenimiento **preventivo**: adaptación temprana; **reingeniería del software**.

> Eg: un mantenimiento adaptativo puede deberse a cambios legislativos, de tecnología, de hardware, de software...

---

### Estructuras y tipos de metodologías de trabajo

#### Cascade
Data de 1970. Consiste en múltiples *etapas formalizadas* en forma de **cascada**. Su mayor crítica es la **escasa mutabilidad** y **baja tolerancia al cambio**.
\
Para el funcionamiento de *cascade* es **imprescindible una ejecución perfecta de cada parte**, algo particularmente difícil y, *a veces, imposible*.

#### Evolutivo
Consiste en múltiples **iteraciones** de muestra *cada vez mas completa* al consumidor de tal forma que este **sigue especificando** sus necesidades. Se distinguen prototipados:
- **evolutivo**
- **incremental**
- **iterativo**
- **iterativo e incremental**

> El desarrollo *incremental* avanza por **secciones del sistema con funcionalidad completa** mientras que el desarrollo *iterativo* avanza por **sistema completo con funcionalidad incompleta**.

>>>>> AQUÍ FALTAN 40 MINUTOS DE CLASE

## TEMA 3: Estudio de viabilidad del sistema e ingeniería de requisitos

>>>>> AQUÍ SIGUEN FALTANDO LOS MISMOS 40 MINUTOS DE CLASE

### Diagrama de casos de uso
>>>>> AQUÍ FALTA CLASE

#### Relaciones
Constituyen las conexiones de los elementos:
- **Asociación**: Une un **actor** con un **caso de uso** de tal forma que el actor **puede participar** en el sistema.
- **Inclusión**: Relaciona **casos de uso** y representa **obligatoriedad de participación** entre ellos.
- **Extensión**: Une **casos de uso** representando **opcional**idad de tal forma que crea una subrama.
- **Generalización** o herencia: Representa la herencia convencional y aplica tanto a **actores con actores** como a **casos de uso con casos de uso** aunque no se recomienda el uso de este último.
    > Eg: es especialmente útil para crear múltiples usuarios.

> Ct: La notación es imprescindible: "Tiene pocas reglas sintácticas y, por tanto, hay que seguirlas al pie de la letra".

#### Actores múltiples
Se pueden dar las siguientes situaciones:
- **Distinto rol**: se conectan los actores de forma convencional-
- **Mismo rol**: se crea un superactor mediante herencia y este reúne el caso de uso de ambos.

#### Descripción de CdU
Las descripciones deben ser **legibles** y deben estar indicadas:
- **inicio y final**
- **actores**
- **objetos**
- **flujos principales y excepcionales**

Hay diferentes formas de **estructurar un CdU**. Se pueden usar **plantillas** entre las cuales se encuentra **Larman**.
> Nota: Para más información revisar transparencias.

> Eg: Larman es de máximos y peca de incorporar documentación excesiva llegando a indicar intereses de los actores cuando debería incorporar únicamente la del sistema.
> \
> Apuntes:
> - No conviene dar pistas de implementación en la descripción de CdU. Es un estado muy temprano.
> - Aunque contextualice, no conviene poner información en la que el sistema no esté explícitamente involucrado.
> - Una variante del sistema Larman es separa el texto en 2 columnas: por un lado lo que hace el actor y por el otro lo que hace el sistema.
> - Cualquier caso de uso en un diagrama CdU debe ser de uso, es decir, debe hacer algo.
> - No se debe hacer descomposición funcional, es decir, crear múltiples unidades de CdU que solo componen un único CdU.