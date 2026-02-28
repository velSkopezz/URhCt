---
title: Ingeniería del Software
author: Christian Velasco Pérez
---
# Ingeniería del Software
*Autor:* Christian Velasco Pérez <img src="https://iili.io/fpTTGnt.md.jpg" alt="Skopez" align="right" style="width:15%; margin-left:4%;margin-bottom:2%">
\
El siguiente contenido corresponde a un **apoyo** educativo para cualquier interesado y por eso puede contener fallos. El documento está orientado al curso de *Ingeniería del Software* del Grado en Ingeniería Informática de la Universidad de La Rioja y se considera completa responsabilidad del lector lo que haga con la información de este documento.
\
La distribución del documento queda reservada al permiso explícito de su autor. Si necesitase información de contacto puede [enviar un correo](mailto:velskopezz@gmail.com).


# TEMA 1: Producto
> Ct: No pretende que nos aprendamos las definiciones de memoria

Un **software** es una colección de **programas y documentación**.

Tipos de Software:
- **genérico**: orientado a un público amplio
- **personalizado**: orientado a un cliente que especifica los requisitos

> Eg: un software de uso generalizado es genérico y uno encargado es personalizado.

## Características del software
- elemento lógico
- mayoritariamente cerrado
- desarrollo a medida
- degradación por cambio de infraestructura

> Nota: El software se *degrada*, no se deteriora

---

## Factores de calidad del software
- **Factores externos**: son percibidos por el usuario
- **Factores internos**: son percibidos por el desarrollador

> Eg: un bug corresponde a algo externo y una funcion indocumentada corresponde a un factor interno

## Problemas del desarrollo del software
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

## Ingeniería de requisitos
Se refiere a la *detección* de los **requisitos funcionales** y **no funcionales**. Es común el uso de herramientas estandarizadas como UML (Unified Modeling Language).

## Análisis
Una vez capturados los requisitos, se trata de **identificar las ideas principales** y darles forma.

## Diseño
En esta fase se *visualiza* la **arquitectura del sistema de diseño** y conviene **distinguir en subsistemas**. Es una etapa que incluye el diseño de *interfaces* y, si fuera pertinente, el **diseño de objetos**.

## Implementación
Es el momento de **codificar**. También es el último momento al que se puede aplazar la **elección del lenguaje** y es *fundamental* crear **documentación**.

## Pruebas
El objetivo de esta fase es **detectar la mayor cantidad de errores**, en específico, los intolerables.
1. Pruebas de **unidad**: Se pretende que cada módulo funcione de forma independiente.
2. Pruebas de **integración**: Se pretende que los módulos funcionen entre ellos.
3. Pruebas de **sistema**: Se pretende que todo el *sistema* funcione.

> Eg: un módulo podría ser una subrutina dentro del código del software.

## Mantenimiento
Se orienta al **cambio** en forma de *reparación y adaptación*. Es la fase más larga y costosa.
- Mantenimiento **correctivo**: arreglar errores.
- Mantenimiento **perfectivo**: mejorar el producto.
- Mantenimiento **adaptativo**: adoptar cambios.
- Mantenimiento **preventivo**: adaptación temprana; **reingeniería del software**.

> Eg: un mantenimiento adaptativo puede deberse a cambios legislativos, de tecnología, de hardware, de software...

---

## Estructuras y tipos de metodologías de trabajo

### Cascade
Data de 1970. Consiste en múltiples *etapas formalizadas* en forma de **cascada**. Su mayor crítica es la **escasa mutabilidad** y **baja tolerancia al cambio**.
\
Para el funcionamiento de *cascade* es **imprescindible una ejecución perfecta de cada parte**, algo particularmente difícil y, *a veces, imposible*.

### Evolutivo
Consiste en múltiples **iteraciones** de muestra *cada vez mas completa* al consumidor de tal forma que este **sigue especificando** sus necesidades. Se distinguen prototipados:
- **evolutivo**
- **incremental**
- **iterativo**
- **iterativo e incremental**

> El desarrollo *incremental* avanza por **secciones del sistema con funcionalidad completa** mientras que el desarrollo *iterativo* avanza por **sistema completo con funcionalidad incompleta**.

# TEMA 2: Metodologías de desarrollo de software
> Sobre el documento: El siguiente tema puede tener deficiencias en su contenido porque el tema se explicó rápidamente por lo que la siguiente información corresponde a un intento de síntesis de transparencias.

Cumple con una serie de características generales. Suele ser:
- Iterativo e incremental
- Dirigido por casos de uso
- Orientado a objetos
- Modelado mediante UML

Aunque es especialmente apreciado por su **flexibilidad**.

## Producto, artefactos y modelos
El **producto** es el **sistema de software** obtenido como **resultado final** del trabajo.
\
Por contraparte, un **artefacto** es un **término general** para cualquier producto, ya sea de ingeniería o gestión.
> Eg: el artefacto más importante del Proceso Unificado es el **modelo**: conjunto de diagramas UML, por ejemplo.

Se tienen diferentes **modelos**:
- Modelos de casos de uso.
    > Eg: Diagramas de CdU
- Modelos de análisis y diseño
    > Eg: Diagramas de clases
- Modelos de despliegue
    > Eg: Diagramas de despliegue
- Modelos de implementación
    > Eg: Diagramas de componentes
- Modelo de pruebas

Por norma general, los modelos tienen dependencias entre ellos.
> Eg: Un diagrama de clases suele representar un único caso de uso de un diagrama de CdU.

## Proceso
Hace referencia a un contexto que sirve para **ajustar disciplinas y flujos de trabajo**.

## Elementos
Se distinguen tres elementos:
- **Fases**
    - Inicio: se define el aclance del proyecto y los casos del negocio.
    - Elaboración: se planifica el proyecto y se detallan especificaciones sobre el uso y arquitectura.
    - Construcción: se construye el producto.
    - Transición: se corrigen los problemas del producto que ahora se considera en *beta*.
- **Puntos de control** o hitos
- **Flujos de trabajo** o disciplinas
    Un **punto de control** marca el final de una **fase**. Además de ello, una fase suele cosntar de varias **iteraciones**.
    \
    Una **iteración** es una secuencia con actividades y criterios de evaluación definidos.

---

## Scrum
Está principalmente orientado a **proyectos largos** con **requisitos cambiantes**.

Es un proceso **ágil** con **entregas parciales y regulares** cuya prioridad es **el beneficio del receptor** al proyecto.

EL proceso parte de una ***product backlog*** de objetivos priorizados
\
El proyecto se ejecuta en iteraciones o bloques cortos y fijos llamados **sprints**. El resultado de cada sprint es un incremento **susceptible de ser entregado**.
> Nota: Durante el sprint no hay cambios.

![Esquema de Scrum](https://scrumorg-website-prod.s3.amazonaws.com/drupal/inline-images/ScrumPoster.png "Qué es Scrum?, por Joel Francia Huambachano, en Scrum.org")

### Roles
Scrum cuenta con diferentes roles.
- ***Product Owner***
    \
    Representa la **voz del cliente** y aporta la visión del negocio. Escribe y prioriza las necesidades del usuario.
- ***Scrum Master***
    \
    Facilita el trabajo para que el equipo consiga el objetivo del sprint.
- ***Equipo***
    \
    Tiene la **responsabilidad de entregar** el producto. Suele tener entre 5 y 9 miembros de **diferentes disciplinas**.
    \
    Los equipos suelen ser auto-organizativos y no cambian durante un sprint.
- **Usuarios**
- **Clientes y vendedores**
- **Gestores y directivos**

### Reuniones
Se identifican diferentes reuiniones.
- ***Sprint planning***
    \
    Consiste en dos partes. En la **selección de requitos** el cliente presenta al equipo los requisitos priorizados. En la **planificación de la iteración** los equipos elaboran una lista de tareas (***sprint backlog***) y estiman el esfuerzo.
- ***Daily scrum meeting***
    \
    Los miembros del equipo inspeccionan el trabajo del resto del equipo para tomar adaptaciones necesarias.
- ***Sprint review***
    \
    El equipo presenta lo realizado durante el **sprint**. Es de carácter **informal** y todo el equipo participa.
- ***Sprint retrospective***
    \
    Periódicamente, normalmente tras un sprint, se revisa que el **proceso** sigue el rumbo adecuado. Son de **muy corta duración**, participa todo el equipo y analiza su forma de trabajar.

### Artefactos
- ***Product backlog***
    \
    Es una **lista priorizada** de todos los **trabajos** deseados para el proyecto.
- ***Sprint backlog***
    \
    Contiene **planes de ejecución** relativos al *product backlog*.
- ***Burndown charts***
    \
    Esquematiza el **desarrollo del proyecto** en función de la fecha.
    
    ![Gráfico de burndown chart](https://cdn.nulab.com/learn-wp/app/uploads/2020/01/14210753/burndown402x.png "Get started using a burndown chart to track your project, por Georgina Guthrie, en Nulab")

## *Extreme Programming* (XP)
Se basa en **resistir a los cambios** que suceden durante el desarrollo.

Es una metodología **ágil** que asume que se pueden mitigar los daños de los cambios si se **planifica adecuadamente**.

### Valores
Los siguientes que inspiran el funcionamiento de XP:
- **Simplicidad**
    \
    Consiste en desarrolar únicamente las **necesidades actuales** del sistema facilitando así la **identificación de necesidades reales**.
- ***Feedback***
    \
    Consiste en aportar **entregas continuas** del trabajo realizado permitiendo **encontrar fallos** de forma temprana. 
- **Coraje**
    \
    Implica tomar **decisiones difíciles** sin indecisiones.
- **Comunicación**
    \
    No solo entre los desarrolladores sino también con los clientes.

> También cuenta con fases y roles. Para más información revisar transparencias.

# TEMA 3: Estudio de viabilidad del sistema e ingeniería de requisitos
> Sobre el documento: El siguiente tema puede tener deficiencias en su estructura y el contenido del inicio puede ser deficiente también

Consiste en cuatro cuestiones fundamentales:
- **comprender el proyecto**
- **recabar información**
- **formalizar funcionalidades**
- **Estudio de viabilidad**

Hay **numerosas alternativas** que deben ser **evaluadas desde distintos puntos de vista**.
> CT: Importante para TFGs. Es probable que, tras *Prácticas Externas*, la propia empresa proponga un TFG. Si el tribunal pregunta para quién está orientado el producto hay que recordar defender que está orientado a una empresa. Corresponde al **estudio de viabilidad**..

También hay distintas **técnicas de recogida de información**.
> Nota: Para ver un listado de estas técnicas revisar transparencias.

## Reuniones
El objetivo de las reuniones es **obtener información** sobre requisitos, funcionamientos, estructuras, etc. El mayor peligro que pueden tener es concluir sin resultados.

### Preparación
Pretende **fijar los objetivos**, **documentarse** al respecto y elaborar una **lista de personal**.
\
Concluye enviando un **huión**.

### Desarrollo
Lo primero es **romper el hielo**. A ello le sigue **explicar y aclarar**.

Tras la **apertura**, hablar **adecuando el vocabulario y reiterando los puntos** y respuestas tratadas.

### Consolidación o análisis
Trata de documentar los resultados, enviar el acta a los participantes y, finalmente, **contrastar los resutlados** con las respuestas anteriores.

---

## Ingeniería de requisitos
Es el proceso necesario en el que se **estudia para indagar y encontrar las necesidades** de un producto. Se distinguen:
- Requisitos **funcionales**: qué servicios se ofrecen.
- Requisitos **no funcionales**: qué tan bien se ofrece el servicio.

> Eg: un inicio de sesión corresponde a un requisito funcional. Las condiciones de seguridad necesarias como *hashear* la contraseña corresponde a un requisito no funcional.

Existe un **proceso de ingeniería de requisitos** para facilitar la tarea:
1. **Identificación de requisitos**
    \
    Contiene tres fases en su proceso:
    1. Recopilar la información
    2. Investigar el ajuste del sistema a las necesidades
    3. Predecir el funcionamiento diario del sistema

2. **Análisis y negociación de requisitos**
    \
    Consiste en negociar el esfuerzo y resultados del desarrollo con el cliente.

3. **Validación de requisitos**
    \
    Asegurar la correctitud y precisión de los requisitos.
    > Eg: no puede ser información ambigua, imposible o incompleta.
    
    También debe incluir pruebas que verifiquen la correctitud de los requisitos.

4. **Especificación de requisitos de software**
    \
    Es un proceso en el que se registran los requisitos quedando dispuestos para avanzar a la siguiente fase.

> Nota: Para información detallada revisar transparencias.

---

## Diagrama de casos de uso
Es una técnica gráfica para modelar el sistema desde el **punto de visa del usuario**.
\
Por ello, se incluyen únicamente **requisitos funcionales**. Para ello se utiliza la dualidad **actor** y **caso de uso**.

### Actores
Representa un **rol** que puede ser un humano, una organización o un sistema.

### Casos de uso
Es una secuencia que describe una tarea o **actividad** que realiza un actor. Debe ser:
- **legible** para el usuario inexperto
- deben indicarse inicio, final, elementos y flujos
- ocasionalmente algún tipo de **descripción** del CdU

### Relaciones
Constituyen las conexiones de los elementos:
- **Asociación**: Une un **actor** con un **caso de uso** de tal forma que el actor **puede participar** en el sistema.
- **Inclusión**: Relaciona **casos de uso** y representa **obligatoriedad de participación** entre ellos.
- **Extensión**: Une **casos de uso** representando **opcionalidad** de tal forma que crea una subrama.
- **Generalización** o herencia: Representa la herencia convencional y aplica tanto a **actores con actores** como a **casos de uso con casos de uso** aunque no se recomienda el uso de este último.
    > Eg: es especialmente útil para crear múltiples usuarios.

> Ct: La notación es imprescindible: "Tiene pocas reglas sintácticas y, por tanto, hay que seguirlas al pie de la letra".

### Actores múltiples
Se pueden dar las siguientes situaciones:
- **Distinto rol**: se conectan los actores de forma convencional-
- **Mismo rol**: se crea un superactor mediante herencia y este reúne el caso de uso de ambos.

### Descripción de CdU
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

## Diagrama de Secuencia del Sistema
Es un caso específico del **diagrama de secuencia** especializado en la **fase de análisis**, a diferencia del convencional que está orientado a la etapa de diseño.

Utiliza la notación del diagrama de secuencia para representar la **interacción entre el actor, su petición y la respuesta del sistema**. El diagrama representa **un único caso de uso**.

Se muestra al actor y al objeto del sistema con sus respectivas **líneas de vida**. Se proporcionan peticiones y respuestas en forma de **flechas dirigidas** y estas, a su vez, pueden estar encajonadas representando **iteraciones**.

### Eventos
Guardan el nombre de la pteición y la **información que se envía**. Para mensajes **condicionales** se pone la condicion encerrada en corchetes antes de la petición. En el caso contrario se hace sacando otra línea.

Los bucles son distintos según la cantidad de afectados. Si son varios se engloban en un marco y se especifica la condición tal que \*\[condición\], destacando el asterisco (*).

> Nota: Se recomienda encarecidamente revisar las transparencias donde se pueden encontrar ejemplos claros de lo anteriormente comentado.

## Diagrama de Actividad
Representa en un grafo el análisis. Es el más **descriptivamente potente** y bastante similar a un diagrama de flujo.

![Diagrama de Actividad](https://www.liderdeproyecto.com/uml/imagenes/012.gif "Del Negocio al Sistema: El Diagrama de Actividad, por Sergio Orozco, en LiderDeProyecto.com")

- El diagrama tiene un **punto de inicio** y un **punto final**.
- Las **actividades** están unidas por una **arista dirigida** o flecha.
- Los **condicionales** se representan con un **rombo** y muestra por **corchetes** adjuntos a la arista **la condición**.
- Los **bucles** se representan dirigiendo la arista de una actividad a otra actividad anterior.
- Existe una notación opcional de **fusión** que se representa uniendo las flechas a un mismo rombo aunque también es válido, sencillamente, unir las flechas a la misma actividad.
    > Ct: Al profesor no le gustan los rombos de fusión porque dificultan la identificación *a primera vista*.

- Los caminos pueden **dividirse** y **unirse** mediante el uso de segmentos de rectas que sean apuntados por una serie de flechas. Es una operación distinta a la fusión. La unión y división requieren que **todos ellos sucedan**.
- Opcionalmente, puede dividirse el diagrama en **calles** que engloben un área en el que, si una actividad se encuentra dentro, se espera que dicha actividad le corresponda a esa parte del sistema.