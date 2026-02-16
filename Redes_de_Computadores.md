---
title: Redes de Computadores
author: Christian Velasco Pérez
---
# Redes de Computadores
*Autor:* Christian Velasco Pérez <img src="https://iili.io/fpTTGnt.md.jpg" alt="Skopez" align="right" style="width:15%; margin-left:4%;margin-bottom:2%">
\
El siguiente contenido corresponde a un **apoyo** educativo para cualquier interesado y por eso puede contener fallos. El documento orientado al curso de *Redes de computadores* del Grado en Ingeniería Informática de la Universidad de La Rioja. Por consiguiente, se considera completa responsabilidad del lector lo que haga con la información de este documento.
\
La distribución del documento queda reservada al permiso explícito de su autor. Si necesitase información de contacto puede [enviar un correo](mailto:velskopezz@gmail.com).

## TEMA 0: Introducción
La estructura de Internet está *influida por su historia*. Por ello pueden verse situaciones como el modelo de 5 capas teniendo mayor uso que el [estándar OSI](https://es.wikipedia.org/wiki/Modelo_OSI "Modelo OSI - Wikipedia, la enciclopedia libre").

> Ct: Con respectoa años anteriores, el valor y la estructura del test van a aumentar (probablemente el test será $2\over6$ del examen final). El profesor valora con mayor positividad **aspectos generales sobre particularidades**.
>
> Nota: Este documento data del curso 2025-2026

## TEMA 1: Introducción a las redes de computadores
La información viaja a los **hosts** por *nodos* a la velocidad especificada por el **ancho de banda**.
!['Nuts and bolts' view](https://sbj6364.github.io/images/post6-cn-w1/1.png "'Nuts and bolts' view, by Pearson Fastener")
> Informalmente podemos identificar hosts como *dispositivos diana* y routers y switches (*packet switches*) como *nodos*.
>
> Nota: La descripción de este documento correspondiente a esta parte es escasa y superficial debido a la complejidad del asunto. Para más información se recomienda acudir a transparencias.

> La información sobre los protocolos de red se recoge en **RFC** cuyo mantenimiento es sostenido por grupos como **IETF**.

Los **paquetes** es la unidad en la que se envía la información por la red. Debido al gran tamaño de los archivos, los paquetes suelen corresponder a segmentos del propio archivo. Estos paquetes **pueden recorrer distintas trayectorias** a través de los *nodos* aunque su desplazamiento sea el mismo.

---

### Identificación en la red
Corresponde a la **dirección única**, que no por ello persistente, encargada de **identificar distintos hosts**.
> En las *cabeceras de los protocolos* siempre **figura la dirección de salida y llegada**.

La dirección única más conocida es la **IPv4**, una serie de dígitos binarios formada por *4 octetos de bits*. No obstante, quedó demostrada su insuficiencia para identificar toda la red y por ello se creó **IPv6**.
- Es una **secuencia de bits**.
- Los mensajes tienen un **tamaño arbitrario**.
- Los routers **almacenan y transmiten** paquetes.
- El tamaño por velocidad se mide en **bits por segundo**.
- Se usa fundamentalmente **TCP y UDP**.
- El *protocolo imprescindible* es **IP**.

> Nota: A diferencia de UDP, TCP ordena los paquetes automáticamente

---

### Extremo de la red
En el extremo de la red están los **hosts**, normalmente, computadores.

#### Servicios orientados a conexión
La conexión sucede **previa a la transferencia de datos**, es decir, primero se *acuerda la conexión* y *posteriormente* se transfieren los datos. El objetivo es garantizar:
- Entrega **ordenada**
- Control del **flujo** y error
- Control de la **congestión**

> Eg: TCP
> 
> Anexo: Los ciberdelincuentes suelen enviarse la información por medio de TCP para garantizar la llegada de datos.

#### Servicio sin conexión
Destaca por ser **rápido y simple**. No hay intercomunicación, tan solo transferencia de datos. Su principal característica es el **nulo control de flujo de datos** .
> Eg: UDP
>
> Está enfocado a:
> - Información **multimedia**
> - Compartición a **múltiples hosts**
> - Aplicaciones de **transmisión corta**

---

### Modelos de conexión
#### Modelo cliente-servidor
Es un sistema con dos extremos basado en el intercambio de información por medio de **petición al servidor** y **respuesta**.

#### Modelo peer-to-peer
Comúnmente llamado P2P, es un sistema similar al cliente-servidor que destaca por su **intercambio de roles** en el que cada host puede recibir y enviar peticiones y respuestas. Está principalmente *orientado a conectar dos hosts*.


### Identificación de procesos
Para **determinar la llegada independiente** de un paquete que llega de la red todos ellos llevan, en su cabecera, designado un **puerto** específico por el que se escucha.
> El que envía información también los debe distinguir según sus procesos. Por ello, así como los paquetes tienen un *puerto de destino* también tiene un **puerto origen**.

---

### Interior de la red
Hay dos formas fundamentales de transmitir información:
- Conmutación **de circuito**: se reserva el camino
- Conmutación **de paquetes**: se trafica el paquete por caminos abiertos

> Concreción: La conmutación de circuito bloquea el uso del circuito para cualquier envío. Se menciona por su uso en otras disciplinas.

### Conmutación de paquetes
Una de sus medidas principales es el **MTU** o tasa máxima limitada que, por defecto, suele corresponder a 1500B y es índice de si el paquete tiene permiso para viajar o debe **fragmentarse**.

Los paquetes son **almacenados y retransmitidos** por el router. La **carga y descarga** toma tiempo y si sucediese un **desbordamiento de la puerta de enlace** se desecharía la información excedente y se enviaría un error para recibir nuevamente la información aumentando el tiempo.
> Nota: Para más información se recomienda revisar transparencias.

---

### Network core
#### Enrutamiento
Cada router tiene una **tabla de redirecciones** en la que, al recibir un paquete, decide una **ruta de conmutación**.

![Tabla de redirecciones](https://i.ytimg.com/vi/gFNnab1Gf7M/hq720.jpg?sqp=-oaymwEhCK4FEIIDSFryq4qpAxMIARUAAAAAGAElAADIQj0AgKJD&rs=AOn4CLC1UUHSKbCtKFV5TlJad2NxEOFPUg "Introducción al Enrutamiento, por Hector Munguia, en YouTube")
Para esto es fundamental el *algoritmo de Dijkstra*. Esto lo gestiona un **sistema autónomo**.
> Nota: Se aborda más información sobre el sistema autónomo próximamente.

#### Velocidades
> $L \equiv$ "cantidad de bits a transmitir"
> \
> $R \equiv$ "tiempo de carga de bits"
> \
> $D \equiv$ "distancia de viaje de un paquete"
> \
> $v \equiv$ "velocidad de viaje por el medio físico"

La **velocidad de transmisión** es dependiente del tiempo necesario para **cargar** y soltar a la red los paquetes:
$$t_t = { L \over R }$$

La **velocidad de propagación** es dependiente del tiempo necesario para que el paquete **transite** hasta su destino:
$$t_p = { D \over v }$$

#### Puntos de intercambio de internet
Los **IXP** e **ISP regionales** son encargados de la **interconexión de dispositivos de distintos ISPs** (proveedores de internet).
> También hay proveedores de internet que *"forman parte de internet"* facilitando la interconexión.

#### Round Trip Time
También llamado por sus siglas **RTT**, es el tiempo que pasa entre que se **envía una señal y recibe una respuesta** con respecto a un receptor.

#### Comunicación entre niveles
Los modelos de referencia dados por distintos proveedores varios, entre ellos, RFC, que presentó problemas, o el modelo **OSI** de 7 niveles proporcionado por **ISO**. Corresponde a una divisón lógica similar a las capas. Por norma general se usa el **modelo TCP/IP** de 5 (o 4) capas.
> Se adjunta una información lexicográfica técnica respecto al nombre del objeto de tráfico
> 
> Capa | Nombre del paquete
> :---: | :---:
> Aplicación | mensaje
> Transporte | segmento/datagrama
> Red | paquete o datagrama
> Enlace | trama
> 
> Nota: En la capa de transporte se llama segmento si es por TCP o datagrama si es por UDP. En la capa de red se usa paquete o datagrama indistintamente. En la capa física solo hay bits.

## TEMA 2: Nivel físico y de enlace

### Transmisión de datos
Se trata de solventar el problema de enviar información. Para ello se distinguen dos métodos:
- Paralelo (síncrono): requiere reloj
- En serie
    - Síncrona
    - Asíncrona

> Nota: Nuevamente, el paralelo corresponde a interés de otras disciplinas.

El envío de información en paralelo no se utiliza en Ethernet. Consiste en esperar a que la fluctuación de los datos sea la adecuada y enviarlo *"de golpe"*.

### Transmisión en serie
Consiste en enviar los bits de forma secuencial. para ello es necesario conocer cuál es el último bit.

#### Asíncrona
Utiliza **bits de inicio** y **bits de parada**.
Se disponen los dos dispositivos a la misma velocidad. Para **mitigar la latencia**, uno de ellos lee un tiempo despues. Es **especialmente sensible a la desincronización** por lo que se utiliza cuando el envío es de pocos bits (alrededor de 8 bits).

#### Síncrona
Se incorpora un reloj. Hay varias formas de lograrlo aunque en Ethernet se utiliza un *"doble envío de datos"* en el que se conoce tanto los datos como la _**información del reloj** con la que se generaron_. Consta de múltiples implementaciones

> Nota: La información sobre la Transmisión en serie síncrona de este documento es pobre. Para mayor información revisar las transparencias.

### Tipos de conexión
Se distinguen tres tipos de comunicación fundamentales:
- full duplex
- half duplex
- simplex

![Tipos de conexión](https://www.glsunmall.com/resource/image/guideImage/simplex-half-duplex-full-duplex.png "Simplex vs. Half-Duplex vs.Duplex, by GLSUN")

--- 

### Señales
Se pueden distinguir las señales de distintas formas: **continuas**, **analógicas**, **discretas**, **digitales**, **periódicas**... según distintos criterios. Dado que las señales periódicas son infinitas, para *funciones sinusoidales* se suele representar, en vez de en función del tiempo, su **dominio sobre la frecuencia**. Se da la función de una señal
$$s(t) = Asin(2{\pi}ft + \phi) + C$$
> $A \equiv$ "amplitud"
> \
> $f \equiv$ "frecuencia"
> \
> $\phi \equiv$ "desfase"

![Dominio sobre la frecuencia](https://media.wiki-power.com/img/20221210154759.png "Integridad de la señal: Dominio del tiempo y Dominio de frecuencia en Power's Wiki")

### Ancho de banda
Es el conjunto de **frecuencias en las que se permite enviar señal**. 
\
Las señales digitales tienen un *ancho de banda infinito*. Las reales, por otra parte, tienen un *ancho de banda propio*. Si el dispositivo no admite la señal por la que se envía la información se limita a ignorarla dada la imposibilidad de captarla.

Para ello, conviene comprender el **desarrollo de Fourier** relativo a las ondas. De forma resumida, se extrae que, dada una función senoidal de la forma $Asin(2{\pi}ft+\phi)$, a la suma infinita de funciones senoidales le corresponde a una gráfica que se identifica con una **señal digital** acercándose más a esta según la cantidad de veces que se sume una función senoidal.

![Convergencia por serie de Fourier](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRde3MDkiX0lkNw_yHSkZtZvrUNRrNtvtuLsQ&s "De las Series de Fourier a la Nanotecnología en Matemáticas y Estadística")
![Convergencia por serie de Fourier](https://upload.wikimedia.org/wikipedia/commons/thumb/2/2c/Fourier_Series.svg/250px-Fourier_Series.svg.png "Serie de Fourier en Wikipedia, la enciclopedia libre")

> Véase la influencia de los armónicos a la función total:
>
> ![Influencia de los armónicos en la función total](https://www.prysmianclub.es/wp-content/uploads/2021/11/Imagen-2.2.jpg "Las series de Fourier cumplen 2 siglos, por Lisardo Recio Maíllo, en Prysmian Club")

---

### Ancho de banda limitado
Los efectos del **ancho de banda limitado** se identifican en forma de **pérdida de armónicos**.
\
Los medios se comportan como un **filtro a paso bajo**:

![Filtro a paso bajo](https://solectroshop.com/img/cms/Filtros/filtro_paso_bajo.webp "Todo lo que necesitas saber sobre Filtros RC en solectro")

> Anexo:
>
> "En teoría de circuitos, un filtro es una red eléctrica que modifica la amplitud o la fase de las componentes frecuenciales presentes en una señal. Puede modificar, desde el punto de vista frecuencial, tanto amplitud como fase. No añade ni cambia componentes frecuenciales, pero varía la relación entre la amplitud y la fase de las ya existentes. Modifica la forma de la onda que aparece en la entrada de la forma deseada a la salida.", definición de [solectro](https://solectroshop.com/es/blog/todo-lo-que-necesitas-saber-sobre-filtros-rc-n52?).

> Nota: Para información adicional sobre filtros revisar transparencias.

### Atenuación
Es un efecto por el que **la señal pierde su amplitud** ($A$) cuya causa, y agravante por consiguiente, es la **distancia** de la trayectoria.
> La atenuación corresponde al **cambio de escala**.

Se aportan dos soluciones:
- **Aplificadores**: dada la señal atenuada $Asin(2{\pi}ft)$ se limita a tomar un factor $\lambda$ tal que la nueva señal sea $(A{\cdot}\lambda)sin(2{\pi}ft)$.
- **Repetidor**: identifica la señal digital y aplifica esta misma.

> Nota: Se suelen usar los repetidores porque los amplificadores aumentarán otras alteraciones de la señal como el ruido.

### Distorsión
Esta forma de pérdida de información toma forma como **alteración no lineal**, es decir, corresponde a una nueva onda $g( Asin(2{\pi}ft) )$.
> La distorsión corresponde al **cambio de forma**.
> \
> En cierto sentido, es un *término "paragüas"* que recoge tanto alteraciones de **desfase** como **cambios de frecuencia**.

La distorsión ocurre cuando **los armónicos de una señal se desfasan** lo que provoca un cambio total en la función de onda.

![Desfase de armónicos](https://files.soniccdn.com/files/2014/07/24/dib01.png "Distorsión: el mundo real y entrenamiento auditivo, por Pablo Fernández-Cid, en Hispasonic")

### Ruido
Es la peor de las **perturbaciones de señal**. Corresponde a **señales no deseadas** que se *"inyectan"* en la señal.
- Ruido **térmico**: insolventable.

    ![Ruido térmico](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQR5Sgq439WBLy1ZE02tQBFAJGtEINL6lETcA&s "Ruido en Ruido e Interferencia")
- **Diafonía**: dos líneas (señales) en paralelo se interfieren.

    ![Diafonía](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEijWgfCn1F-o9WKgVWg_7NV1CBYHtdJVfzqoo-yjeJF1PkMhGQW07IxOE-gFYMJRr_T-sYMD2YuuidZpODvN_4wwPTnXQK058YeYiN7KwsLdhmiBlz4BnGN1Jl2LdhjYj1X6eLfcawRXJIN/s1600/www-textoscientificos-com.gif "Naturaleza y causas de las interferencias en Ruido e Interferencia")
- Ruido **impulsivo**: corresponde a daños físicos y lleva a **falseamiento**.
    > Las consecuencias del ruido impulsivo es **impredecible**.

> Nota: Para más información revisar transparencias.

#### Muestreo
La solución en estos casos es que el **receptor imponga un muestreo** aunque puede llevar a error si los tiempos fueran distintos o la señal estuviera gravemente alterada.

---

### Medios de transmisión
Se trata del **medio** por el que se **transporta la señal**.
- **guiados**: por cable, dependen del **medio**.
- **no guiados** (inalámbrico): por aire, dependen de la **frecuencia**.

Medios guiados | Medios no guiados
:--- | :---
par trenzado | ondas de radio
cable coaxial | microondas
fibra óptica | infrarrojos

> Nota: Evidentemente, hay más.

### Medios de transmisión guiados
Se distinguen dos formas de disponer el cableado:
- **directo**: para conexiones emisor/receptor
- **cruzado**: para conexiones de doble emisor

![Conexión directa y cruzada](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjLqiLslUqesCM5tRuC9o6ktKnzxpGSrQ16e0XDb2yiB66YYLAhMVeQzdvQhlxfZSubJ9NbZq_u85N6WET36yN1v0FT9WJVt-ptF5_OT7l69lTNZNf4bbTD3_0lj9TJQFaMH8aNZoncfKk/s1600/straight-through-vs-crossover-cables.jpg "Cable directo y cruzado, por Jorge, en Redes de datos")

#### Par trenzado
Es el medio guiado más **económico** y consta de dos conductores aislados que se entrelazan. Alcanza una velocidad de alrededor de 100 Mbps.

Se suelen utilizar en:
- telefonía
- redes locales

Además, se distinguen **tipos de pares trenzados** según su apantallado (protección de cables) o **protección de interferencia**:

Nombre | Tipo | Apantallado por par | Apantallado global
:--- | ---: | :---: | :---:
Unshielded Twisted Pair | UTP | ✕ : NO | ✕ : NO
Foiled Twisted Pair | FTP | ✕ : NO |  ✓ : SÍ 
Shielded Twisted Pair | STP | ✓ : SÍ | ✕ : NO
Shielded Foiled Twisted Pair | SFTP | ✓ : SÍ | ✓ : SÍ 

![Tipos de cables trenzados](https://cdn.shopify.com/s/files/1/0642/3091/6354/files/5_e668e12f-9590-44d3-ab93-be2eb80c68c7.jpg?v=1730016624 "La guía completa de los cables de Ethernet: lo que debe saber en Cabletime")

También pueden categorizarse según sus **apliaciones** difiriendo en características como el ancho de banda.
> Nota: El filtro de paso bajo es también **analógico**, es decir, aunque filtre según el ancho de banda, los límites son difusos y pierden amplitud de forma continua atenuándose.

#### Cable coaxial
Consiste en **dos conductores concéntricos** separados por aislante. Para obtener flexibilidad, el conductor exterior se dispone en forma de malla.

Es usado en televisores y, anteriormente, en conexiones LAN entre ordenadores.

![Cable coaxial](https://alfarsl.es/wp-content/uploads/2018/03/caracteristicas-cable-coaxial.jpg "Características del cable coaxial y variantes del dieléctrico en Alfa'r")

#### Fibra óptica
Transmite **señales luminosas** por lo que proporciona:
- **inmunidad al daño radioeléctrico**
- **mitigación de atenuación**

Es pequeño, maleable y maneja enormes velocidades.

![Ley de Snell y fibra óptica](https://openstax.org/apps/image-cdn/v1/f=webp/apps/archive/20260105.231123/resources/fb1e4927b295dd1f5c2bd4e56c3c0e4f2bc19b7b "Reflexión interna total: Física universitaria volumen 3 en OpenStax")

### Métodos de transmisión no guiados
Su medio es el **aire** por lo que dispondra de **menor seguridad** en **llegada de paquetes** y **privacidad de contenido**.

Se distingue el tipo de onda según su **frecuencia**.

![Frecuencia de ondas](https://www.adslzone.net/app/uploads-adslzone.net/2017/10/grafico-espectro-electromagnetico1.jpg "¿Cómo lo hace la fibra óptica para no perder intensidad con la distancia?, por Alberto García, en ADSLZone")

En ocasiones es necesario **transformar la señal**. Para ello se utilizará **modulación** y **codificación**.

> Eg: si quieres emitir una canción no puedes hacerlo por voz porque la señal no se emitirá la distancia suficiente.

---

### Modulación
Es como un proceso en el que se incluye un **modulador** que actúa como **caja negra**.

Para obtener la señal original en el receptor hace falta un proceso de **demodulación**.

![Modulador](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcR4y28zRRq9RHgm3skbztFNZM504iA7wHq82g&s "TEMA 7 Modulación de amplitud en Universidad Nacional de Tucumán")

![](https://onubaelectronica.es/wp-content/uploads/2020/06/am.png.webp "Transmisor de señal de banda AM, por nivel13, en OnubaElectrónica")

Se distinguen tipos de modulación:
- **AM** sobre *amplitud*
- **FM** sobre *frecuencia*
- **Modulación digital** sobre flancos digitales
    - **ASK** sobre *amplitud*
    - **FSK** sobre *frecuencia*
    - **PSK** sobre *fase*
    - **DPSK** sobre fase y diferencial

### Modulación PSK
Consiste en cambiar la fase según la información.

Se ve de forma sencilla usando un vector fasor y un cambio de fase a un bit por 180º.

![Modulación PSK a 180º en vector fasor](https://shopdelta.eu/obrazki_art/dpsk_img2_d.jpg "PSK modulation and its types en Shopdelta")

Sin embargo, esto enfrenta problemas. El desfase **tiene un coste de aumento de frecuencia** pues desfasar esos 180º al instante tiene un coste de alrededor de 1GHz. Para solucionar este problema se **divide** el vector fasor en más ángulos de tal forma que se transmitan **varios bits por ángulo**.

![Modulación PSK a 90º en vector fasor](https://shopdelta.eu/obrazki_art/dpsk_img3_d.jpg "PSK modulation and its types en Shopdelta")