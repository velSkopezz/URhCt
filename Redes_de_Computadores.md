---
title: Redes de Computadores
author: Christian Velasco Pérez
---
# **Redes de Computadores**
*Autor:* Christian Velasco Pérez <img src="https://iili.io/fpTTGnt.md.jpg" alt="Skopez" align="right" style="width:15%; margin-left:4%;margin-bottom:2%">
\
El siguiente contenido corresponde a un **apoyo** educativo para cualquier interesado y por eso puede contener fallos. El documento está orientado al curso de *Redes de computadores* del Grado en Ingeniería Informática de la Universidad de La Rioja y se considera completa responsabilidad del lector lo que haga con la información de este documento.
\
La distribución del documento queda reservada al permiso explícito de su autor. Si necesitase información de contacto puede [enviar un correo](mailto:velskopezz@gmail.com).

# TEMA 0: Introducción
La estructura de Internet está *influida por su historia*. Por ello pueden verse situaciones como el modelo de 5 capas teniendo mayor uso que el [estándar OSI](https://es.wikipedia.org/wiki/Modelo_OSI "Modelo OSI - Wikipedia, la enciclopedia libre").

> Ct: Con respectoa años anteriores, el valor y la estructura del test van a aumentar (probablemente el test será $2\over6$ del examen final). El profesor valora con mayor positividad **aspectos generales sobre particularidades**.
>
> Nota: Este documento data del curso 2025-2026

# TEMA 1: Introducción a las redes de computadores
La información viaja a los **hosts** por *nodos* a la velocidad especificada por el **ancho de banda**.
!['Nuts and bolts' view](https://sbj6364.github.io/images/post6-cn-w1/1.png "'Nuts and bolts' view, by Pearson Fastener")
> Informalmente podemos identificar hosts como *dispositivos diana* y routers y switches (*packet switches*) como *nodos*.
>
> Nota: La descripción de este documento correspondiente a esta parte es escasa y superficial debido a la complejidad del asunto. Para más información se recomienda acudir a transparencias.

> La información sobre los protocolos de red se recoge en **RFC** cuyo mantenimiento es sostenido por grupos como **IETF**.

Los **paquetes** es la unidad en la que se envía la información por la red. Debido al gran tamaño de los archivos, los paquetes suelen corresponder a segmentos del propio archivo. Estos paquetes **pueden recorrer distintas trayectorias** a través de los *nodos* aunque su desplazamiento sea el mismo.

---

## Identificación en la red
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

## Extremo de la red
En el extremo de la red están los **hosts**, normalmente, computadores.

### Servicios orientados a conexión
La conexión sucede **previa a la transferencia de datos**, es decir, primero se *acuerda la conexión* y *posteriormente* se transfieren los datos. El objetivo es garantizar:
- Entrega **ordenada**
- Control del **flujo** y error
- Control de la **congestión**

> Eg: TCP
> 
> Anexo: Los ciberdelincuentes suelen enviarse la información por medio de TCP para garantizar la llegada de datos.

### Servicio sin conexión
Destaca por ser **rápido y simple**. No hay intercomunicación, tan solo transferencia de datos. Su principal característica es el **nulo control de flujo de datos** .
> Eg: UDP
>
> Está enfocado a:
> - Información **multimedia**
> - Compartición a **múltiples hosts**
> - Aplicaciones de **transmisión corta**

---

## Modelos de conexión
### Modelo cliente-servidor
Es un sistema con dos extremos basado en el intercambio de información por medio de **petición al servidor** y **respuesta**.

### Modelo peer-to-peer
Comúnmente llamado P2P, es un sistema similar al cliente-servidor que destaca por su **intercambio de roles** en el que cada host puede recibir y enviar peticiones y respuestas. Está principalmente *orientado a conectar dos hosts*.


## Identificación de procesos
Para **determinar la llegada independiente** de un paquete que llega de la red todos ellos llevan, en su cabecera, designado un **puerto** específico por el que se escucha.
> El que envía información también los debe distinguir según sus procesos. Por ello, así como los paquetes tienen un *puerto de destino* también tiene un **puerto origen**.

---

## Interior de la red
Hay dos formas fundamentales de transmitir información:
- Conmutación **de circuito**: se reserva el camino
- Conmutación **de paquetes**: se trafica el paquete por caminos abiertos

> Concreción: La conmutación de circuito bloquea el uso del circuito para cualquier envío. Se menciona por su uso en otras disciplinas.

## Conmutación de paquetes
Una de sus medidas principales es el **MTU** o tasa máxima limitada que, por defecto, suele corresponder a 1500B y es índice de si el paquete tiene permiso para viajar o debe **fragmentarse**.

Los paquetes son **almacenados y retransmitidos** por el router. La **carga y descarga** toma tiempo y si sucediese un **desbordamiento de la puerta de enlace** se desecharía la información excedente y se enviaría un error para recibir nuevamente la información aumentando el tiempo.
> Nota: Para más información se recomienda revisar transparencias.

---

## Network core
### Enrutamiento
Cada router tiene una **tabla de redirecciones** en la que, al recibir un paquete, decide una **ruta de conmutación**.

![Tabla de redirecciones](https://i.ytimg.com/vi/gFNnab1Gf7M/hq720.jpg?sqp=-oaymwEhCK4FEIIDSFryq4qpAxMIARUAAAAAGAElAADIQj0AgKJD&rs=AOn4CLC1UUHSKbCtKFV5TlJad2NxEOFPUg "Introducción al Enrutamiento, por Hector Munguia, en YouTube")
Para esto es fundamental el *algoritmo de Dijkstra*. Esto lo gestiona un **sistema autónomo**.
> Nota: Se aborda más información sobre el sistema autónomo próximamente.

### Velocidades
> $L \equiv$ "cantidad de bits a transmitir"
> \
> $R \equiv$ "velocidad de carga de bits"
> \
> $D \equiv$ "distancia de viaje de un paquete"
> \
> $v \equiv$ "velocidad de viaje por el medio físico"

La **velocidad de transmisión** es dependiente del tiempo necesario para **cargar** y soltar a la red los paquetes:

$$t_t = { L \over R }$$

La **velocidad de propagación** es dependiente del tiempo necesario para que el paquete **transite** hasta su destino:

$$t_p = { D \over v }$$

### Puntos de intercambio de internet
Los **IXP** e **ISP regionales** son encargados de la **interconexión de dispositivos de distintos ISPs** (proveedores de internet).
> También hay proveedores de internet que *"forman parte de internet"* facilitando la interconexión.

### Round Trip Time
También llamado por sus siglas **RTT**, es el tiempo que pasa entre que se **envía una señal y recibe una respuesta** con respecto a un receptor.

### Comunicación entre niveles
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

# TEMA 2: Nivel físico y de enlace

## Transmisión de datos
Se trata de solventar el problema de enviar información. Para ello se distinguen dos métodos:
- Paralelo (síncrono): requiere reloj
- En serie
    - Síncrona
    - Asíncrona

> Nota: Nuevamente, el paralelo corresponde a interés de otras disciplinas.

El envío de información en paralelo no se utiliza en Ethernet. Consiste en esperar a que la fluctuación de los datos sea la adecuada y enviarlo *"de golpe"*.

## Transmisión en serie
Consiste en enviar los bits de forma secuencial. para ello es necesario conocer cuál es el último bit.

### Asíncrona
Utiliza **bits de inicio** y **bits de parada**.
Se disponen los dos dispositivos a la misma velocidad. Para **mitigar la latencia**, uno de ellos lee un tiempo despues. Es **especialmente sensible a la desincronización** por lo que se utiliza cuando el envío es de pocos bits (alrededor de 8 bits).

### Síncrona
Se incorpora un reloj. Hay varias formas de lograrlo aunque en Ethernet se utiliza un *"doble envío de datos"* en el que se conoce tanto los datos como la _**información del reloj** con la que se generaron_. Consta de múltiples implementaciones

> Nota: La información sobre la Transmisión en serie síncrona de este documento es pobre. Para mayor información revisar las transparencias.

## Tipos de conexión
Se distinguen tres tipos de comunicación fundamentales:
- full duplex
- half duplex
- simplex

![Tipos de conexión](https://www.glsunmall.com/resource/image/guideImage/simplex-half-duplex-full-duplex.png "Simplex vs. Half-Duplex vs.Duplex, by GLSUN")

--- 

## Señales
Se pueden distinguir las señales de distintas formas: **continuas**, **analógicas**, **discretas**, **digitales**, **periódicas**... según distintos criterios. Dado que las señales periódicas son infinitas, para *funciones sinusoidales* se suele representar, en vez de en función del tiempo, su **dominio sobre la frecuencia**. Se da la función de una señal
$$s(t) = Asin(2{\pi}ft + \phi) + C$$
> $A \equiv$ "amplitud"
> \
> $f \equiv$ "frecuencia"
> \
> $\phi \equiv$ "desfase"

![Dominio sobre la frecuencia](https://media.wiki-power.com/img/20221210154759.png "Integridad de la señal: Dominio del tiempo y Dominio de frecuencia en Power's Wiki")

## Ancho de banda
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

## Ancho de banda limitado
Los efectos del **ancho de banda limitado** se identifican en forma de **pérdida de armónicos**.
\
Los medios se comportan como un **filtro a paso bajo**:

![Filtro a paso bajo](https://solectroshop.com/img/cms/Filtros/filtro_paso_bajo.webp "Todo lo que necesitas saber sobre Filtros RC en solectro")

> Anexo:
>
> "En teoría de circuitos, un filtro es una red eléctrica que modifica la amplitud o la fase de las componentes frecuenciales presentes en una señal. Puede modificar, desde el punto de vista frecuencial, tanto amplitud como fase. No añade ni cambia componentes frecuenciales, pero varía la relación entre la amplitud y la fase de las ya existentes. Modifica la forma de la onda que aparece en la entrada de la forma deseada a la salida.", definición de [solectro](https://solectroshop.com/es/blog/todo-lo-que-necesitas-saber-sobre-filtros-rc-n52?).

> Nota: Para información adicional sobre filtros revisar transparencias.

## Atenuación
Es un efecto por el que **la señal pierde su amplitud** ($A$) cuya causa, y agravante por consiguiente, es la **distancia** de la trayectoria.
> La atenuación corresponde al **cambio de escala**.

Se aportan dos soluciones:
- **Aplificadores**: dada la señal atenuada $Asin(2{\pi}ft)$ se limita a tomar un factor $\lambda$ tal que la nueva señal sea $(A{\cdot}\lambda)sin(2{\pi}ft)$.
- **Repetidor**: identifica la señal digital y aplifica esta misma.

> Nota: Se suelen usar los repetidores porque los amplificadores aumentarán otras alteraciones de la señal como el ruido.

## Distorsión
Esta forma de pérdida de información toma forma como **alteración no lineal**, es decir, corresponde a una nueva onda $g( Asin(2{\pi}ft) )$.
> La distorsión corresponde al **cambio de forma**.
> \
> En cierto sentido, es un *término "paragüas"* que recoge tanto alteraciones de **desfase** como **cambios de frecuencia**.

La distorsión ocurre cuando **los armónicos de una señal se desfasan** lo que provoca un cambio total en la función de onda.

![Desfase de armónicos](https://files.soniccdn.com/files/2014/07/24/dib01.png "Distorsión: el mundo real y entrenamiento auditivo, por Pablo Fernández-Cid, en Hispasonic")

## Ruido
Es la peor de las **perturbaciones de señal**. Corresponde a **señales no deseadas** que se *"inyectan"* en la señal.
- Ruido **térmico**: insolventable.

    ![Ruido térmico](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQR5Sgq439WBLy1ZE02tQBFAJGtEINL6lETcA&s "Ruido en Ruido e Interferencia")
- **Diafonía**: dos líneas (señales) en paralelo se interfieren.

    ![Diafonía](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEijWgfCn1F-o9WKgVWg_7NV1CBYHtdJVfzqoo-yjeJF1PkMhGQW07IxOE-gFYMJRr_T-sYMD2YuuidZpODvN_4wwPTnXQK058YeYiN7KwsLdhmiBlz4BnGN1Jl2LdhjYj1X6eLfcawRXJIN/s1600/www-textoscientificos-com.gif "Naturaleza y causas de las interferencias en Ruido e Interferencia")
- Ruido **impulsivo**: corresponde a daños físicos y lleva a **falseamiento**.
    > Las consecuencias del ruido impulsivo es **impredecible**.

> Nota: Para más información revisar transparencias.

### Muestreo
La solución en estos casos es que el **receptor imponga un muestreo** aunque puede llevar a error si los tiempos fueran distintos o la señal estuviera gravemente alterada.

---

## Medios de transmisión
Se trata del **medio** por el que se **transporta la señal**.
- **guiados**: por cable, dependen del **medio**.
- **no guiados** (inalámbrico): por aire, dependen de la **frecuencia**.

Medios guiados | Medios no guiados
:--- | :---
par trenzado | ondas de radio
cable coaxial | microondas
fibra óptica | infrarrojos

> Nota: Evidentemente, hay más.

## Medios de transmisión guiados
Se distinguen dos formas de disponer el cableado:
- **directo**: para conexiones emisor/receptor
- **cruzado**: para conexiones de doble emisor

![Conexión directa y cruzada](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjLqiLslUqesCM5tRuC9o6ktKnzxpGSrQ16e0XDb2yiB66YYLAhMVeQzdvQhlxfZSubJ9NbZq_u85N6WET36yN1v0FT9WJVt-ptF5_OT7l69lTNZNf4bbTD3_0lj9TJQFaMH8aNZoncfKk/s1600/straight-through-vs-crossover-cables.jpg "Cable directo y cruzado, por Jorge, en Redes de datos")

### Par trenzado
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

### Cable coaxial
Consiste en **dos conductores concéntricos** separados por aislante. Para obtener flexibilidad, el conductor exterior se dispone en forma de malla.

Es usado en televisores y, anteriormente, en conexiones LAN entre ordenadores.

![Cable coaxial](https://alfarsl.es/wp-content/uploads/2018/03/caracteristicas-cable-coaxial.jpg "Características del cable coaxial y variantes del dieléctrico en Alfa'r")

### Fibra óptica
Transmite **señales luminosas** por lo que proporciona:
- **inmunidad al daño radioeléctrico**
- **mitigación de atenuación**

Es pequeño, maleable y maneja enormes velocidades.

![Ley de Snell y fibra óptica](https://openstax.org/apps/image-cdn/v1/f=webp/apps/archive/20260105.231123/resources/fb1e4927b295dd1f5c2bd4e56c3c0e4f2bc19b7b "Reflexión interna total: Física universitaria volumen 3 en OpenStax")

## Métodos de transmisión no guiados
Su medio es el **aire** por lo que dispondra de **menor seguridad** en **llegada de paquetes** y **privacidad de contenido**.

Se distingue el tipo de onda según su **frecuencia**.

![Frecuencia de ondas](https://www.adslzone.net/app/uploads-adslzone.net/2017/10/grafico-espectro-electromagnetico1.jpg "¿Cómo lo hace la fibra óptica para no perder intensidad con la distancia?, por Alberto García, en ADSLZone")

En ocasiones es necesario **transformar la señal**. Para ello se utilizará **modulación** y **codificación**.

> Eg: si quieres emitir una canción no puedes hacerlo por voz porque la señal no se emitirá la distancia suficiente.

---

## Modulación
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

> Sobre el documento: Si no se pueden visualizar las imágenes del vector fasor, probablemente, sea culpable la página web. Tal vez se pueda visualizar usando VPNs o proxies.

También se puede aprovechar la **modulación de la amplitud** par codificar más bits.

![Modulación de amplitud PSK](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhcbPSzqAKJZuyewCi3euccyZesRBgFy-9icopE2buljX6jPPVavfL5qc-Z6B_ywzcTzjxjrKpMTsKuIysXKiK6OvoF9PI-8pMFZGpR0NwlDjg6LD80SHQEh2BvuNOsll66hdo0gPfG9gMH/s1600/Captura.PNG "Teleco in a nutshell v8.7: Modulación de Amplitud en Cuadratura, por zerolynx, en Fluproject")

Esto requerirá **mejores receptores** para poder captar con precisión los distintos estados.

> Eg: Wi-Fi es adaptativo y, según la intensidad de la señal, puede variar entre BPSK y 1024-QAM.

Es **fundamental para canalizar las señales** evitando así interferencias entre emisoras. Para ello se utilizan filtros.

> Eg: si solo quisieras escuchar la música de una sola cadena de radio tendrías que modular la señal para captar la frecuencia que le corresponde. De lo contrario, estarías capturando señal de otras radios. Para ello, el modulador aporta valor 1 a las frecuencias escuchadas y 0 al resto de frecuencias creando una caída teóricamente digital aunque realmente analógica.

Por todo esto, el receptor necesita, a su vez, un **demodulador** que permita recibir la señal modulada y extraer su informacón original.

![Proceso de red](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSPcfbvDBJeP4rTh1SVmmnpoJW5Esbd2Bo_Og&s "SISTEMAS ABIERTOS E INTERCONEXIÓN, por M.C Alejandro Gutiérrez Díaz")

## Codificación
Es la forma de tomar señales digitales y **transformarlas en analógicas**. Se distinguen múltiples formas:
- NRZ: no retorno a cero
- RZ: retorno a cero (vuelve a 0 a media fase reduciendo costes)
- NRZI: no retorno a cero invertido (cambia la fase con un 1)
- **Manchester**: se usa en Ethernet de menos de 10b. Comprueba el valor mediante el **cambio de flanco** a mitad de fase.
- **Manchester diferencial**: en este caso la **transición se utiliza para sincronizar**. La falta de sincronización corresponde a un 1.

Velocidades de transmisión y modulación:

$$v_{mod} = v_{tx}/bpe$$

> $v_{tx} \equiv$ "velocidad de transmisión"
> \
> $v_{mod} \equiv$ "velocidad de modulación"
> \
> $bpe \equiv$ "cantidad de bits codificados a la vez"
>
> Por heurística, no se suele enviar información por encima de la décima parte de la banda ancha media.
> \
> Con **velocidad de transmisión** se hace referencia a la cantidad de bits transmitidos en bps.
> \
> Con **velocidad de modulación** se hace referencia a los cambios generados por tiempo en baudios (Bd).

---

# TEMA 2: Enlace y servicios
Un **enlace** es una **trayectoria que conecta dos dispositivos**. Es el encargado de **enrutar por medio de nodods**. La capa de enlace es un intermediario entre lo físico y lo lógico, es decir, **en las próximas capas se ignorarán las trayectorias de la capa de enlace**.

![Capa de enlace](https://laprovittera.com/wp-content/uploads/2022/10/image-116.png "CAPA 2 ENLACE DE DATOS (Acceso a red) Enrutamiento y creación de una LAN, por Laprovittera, en LAPROVITTERA CARLOS")

> En la capa de red se ignorarán los saltos que tome la información. Se tendrá en cuenta únicamente la fuente y el destino.

> Para más aclaración revisar transparencias.

Los **servicios** ofrecen:
- **Delimitación de la trama**
- **Acceso al medio**
- **Detección de errores**
- **Entrega segura**
- **Control de flujo**
- Conmutación duplex

## Datagramas en su encapsulamiento
Cuando llega una cabecera desde el nivel de red para pasar al nivel de enlace se *encapsula* la cabecera alrededor de información de la capa de enlace.

![Encapsulamiento de datos](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEikKBjRvVD1gCNi9mZlTurxXbQPkH4q2JEF2CMw4YPHo-ybw4ExuqgL53ClPamBRenY3vBRpHMbm2-oNRvYuTzFIrsBNG9BhTVYbp7Y4VMam6-PSfSnBEnQ_f8c_zB4s9hMbTPs0Cmta5U/s1600/encapsulamientoEX.png "Proceso de Comunicación de los Datos: Encapsulamiento, por  Marco A. Arenas, en Telecomunicaciones USFX")

### Adaptador de red
También conocido como **NIC** (Network Interface Card) o simplemente **tarjeta de red**, es el encargado de **encapsular** el datagrama en una trama que se transmite implementando los niveles de **enlace y físico**.
\
El adaptador del receptor descarta las partes de la cabecera que no le son necesarias.

Es una unidad semiautónoma y **forma parte del nodo físico** compartiendo alimentación y buses del sistema.
\
El sistema operativo suele **delegar a la tarjeta de red** la tarea de transmisión.

> Nota: Para más usos de la tarjeta de red revisar transparencias.

> Nota: Comúnmente hay que habilitar la tarea de adaptación al sistema operativo para poder registrar lo que sucede, algo que se hará en grupos informáticos.

## Creación de la trama
Existe una **función de enrutamiento** que permite **delimitar** el inicio y el fin y **construir tramas**. Estas contienen:
- **Cabecera** del protocolo.
- **Datos**.
- **Códigos de detección** al inicio y final de la trama.

> Esta forma de construir la trama **presenta un problema**: Hay que designar **marcadores de inicio y final de trama** que pueden **presentarse entre los datos**.

Se utiliza un **marcador de escape** para evitar interpretaciones incorrectas del mensaje. Se distinguirán dos formas de hacerlo:
- **Relleno por byte**
    > Eg: supongamos `0x7E` como valor de `FLAG`:
    > > Nota:  `0x7E` = `0b01111110`.
    > 
    > Si nuestro mensaje fuera el siguiente.
    > ```
    > 0x7E 0x2A 0x3E 0x7E 0x0A 0x7E
    > ```
    > Tendríamos un problema. `0x7E` forma parte del mensaje. Para solucionarlo usaremos el escape al que llamaremos `0x7D`. De esta forma el mensaje quedaría tal que:
    > ```
    > 0x7E 0x2A 0x3E 0x7D 0x7E 0x0A 0x7E
    > ```
    > A la vista queda que lo que antes era `0x7E` a mitad de mensaje ahora es `0x7D 0x7E` donde `0x7D` es el escape y `0x7E` es la información que comparte codificación con el `FLAG`. Como queda escapado, el receptor puede comprender que no es el final del mensaje sino parte de él.
    > > Nota: Si `0x7D` formase parte del mensaje sencillamente se escapa el escape, es decir, se cambia por `0x7D 0x7D`.
- **Relleno por bit**
    > Tras leer 5 unos consecutivos en `0b01111110` (igual a `0x7E`) se cambia el mensaje por `0b01111010` de tal forma que **el antepenúltimo bit no transmite mensaje**, tan solo información sobre si ha acabado el mensaje.
    > > Eg: un byte de relleno por bit transmite una cantidad de información diferente que un byte de relleno por byte.
    >
    > > Nota: Es el utilizado por el protocolo **HDCL**. 

> Nota: Este marcador de escape funciona exactamente igual que el `\` visto en *Regular Expressions* o *strings* en lenguajes de programación como Java.

## Tramas Ethernet
Hay muchas tramas de Ethernet. Las más relevantes son **Ethernet II**, **Ethernet 802.3raw** y **Ethernet IEEE 802.3**.
> Nota: Las transparencias proporcionan un resumen al respecto de IONOS.

- **Ethernet II**

    Es el más utilizado en la actualidad.

    ![Cabecera de Ethernet II](https://www.ionos.com/digitalguide/fileadmin/_processed_/5/b/csm_EN-ethernet-frame-structure_b05e04fde2.webp "Ethernet frame: definition and variants of the frame format en IONOS")

    - El **preámbulo** es una secuencia ordenada de la forma `10101010`... que sirve para que el receptor detecte la conexión. Se repite durante 7 octetos.
    - El **SFD** es el delimitador. Corresponde a la secuencia `10101011` aportando un último `1` para que el receptor delimite el *Bit Secuence*.
    - El **type** proporciona el protocolo que se está utilizando.
        > Nota: `0x800` corresponde a IP y `0x806` corresponde a ARP.
        > > Ct: Típico ejercicio de clase y de examen: Si type es IP o ARP.
    - La **data** contiene la información. Ocupa un mínimo de 46B para que el *Ethernet Frame* ocupe 64B que es el **tamaño mínimo necesario para la detección de colisiones**.
    - El FCS verifica la integridad de los datos.

- **Ethernet 802.3raw**: 

    Fue creado por una empresa poniendo el nombre de Ethernet 802.3 al mismo tiempo que IEEE (*Institute of Electrical and Electronics Engineers*) estandarizaba su IEEE 802.3. Por ello, esta empresa fue obligada a añadirle la etiqueta "*raw*".

    Consiste en cambiar el *type* (4B) por **length** (2B) y añadir un excedente de 2B en forma de `0xFFFF` para rellenar el espacio.

    ![Ethernet 802.3raw](https://www.ionos.com/digitalguide/fileadmin/_processed_/5/7/csm_EN-ethernet-frame-structure2_d194ad28f5.webp "Ethernet frame: definition and variants of the frame format en IONOS")

- **Ethernet IEEE 802.3**:

    Añade **DSAP** y **SSAP** que ocupan 1B cada uno y logran sustituir los bytes de relleno en Ethernet 802.3raw.

    ![Ethernet IEEE 802.3](https://www.ionos.com/digitalguide/fileadmin/_processed_/0/4/csm_EN-ethernet-frame-structure3_51c742720b.webp "Ethernet frame: definition and variants of the frame format en IONOS")

> Para más ejemplos revisar transparencias.
> > Ct: "A mí lo que me importa es la primera".

> Ct: En la actualidad se usan otros. Manchester encoded es para Ethernet a menos de 10 megabits.

---

## Técnicas de detección de errores
Es la forma de lograr **fiabilidad** entre las comunicaciones.

$$ \text{"Tasa de error de bit"} \equiv BER $$

> Nota: *BER* viene de *bit error rate*.

> Ct: Esto aparecerá en las prácticas.

El receptor debe **comprobar y detectar** los errores en la transmisión. Esta detección se realiza mediante **códigos detectores de error** que incorporan **datos adicionales** y aumenta la **complejidad**.
\
Estos codigos detectores de errores, normalmente, cubren **cabecera y datos** y permiten al receptor detectar **ocasionalmente** errores.

### Paridad simple
Puede ser sobre **par o impar**. Consiste en poner **un último bit de paridad**. El receptor debe calcular si la paridad del total de bits es la adecuada.

Esta técnica es **poco consistente** ya que fallará siempre que fallen $2n$ bits.

### CheckSum
Proporciona un **valor como suma de información**. Si el receptor detecta distinto el valor de la suma y la suma de la información significa que se ha habido alguna alteración. Nuevamente, puede fallar.

### CRC
Se calcula electrónicamente mediante **módulos con transistores**.
\
Consiste en una **operación XOR consecutiva** que proporciona un **código resultante** obtenido desde el 0 que debe, en el emisor, ser transmitido y, en el receptor, ser operado hasta obtener dicho 0.

Hay **estándares internacionales definidos** para llevar esto. son los $G_{\text{CRC-}n}$ con $n$ bits.

## Corrección de errores
Se dan dos estrategias de las cuales la más usada es el **ARQ**:
- **FEC** (*Foward Error Correction*) añade **información de recuperación** al mensaje.
- **ARQ** (*Automatic Repeat Request*) pide al emisor la **información nuevamente**.

> Nota: Esto aplica principalmente a la capa de transporte porque en la capa de enlace **se desecha la trama alterada**.

# TEMA 3: Red de Área Local (LAN)
Son redes de **pocos kilómetros** que transmiten información a **pocos dispositivos** a **alta velocidad**.

## Mecanismos de control de acceso al medio (MAC)
Los **controles de acceso al medio** (MAC de *Media Acces Control*) son clasificables:
- con **posibilidad de colisión**
    > Eg: Alohanet, CSMA, CSMA/CD (Ethernet), CSMA/CA (Wi-Fi)...
- **libres de colisión**
    > Eg: Mecanismos de paso de testigo, de reserva, de encuesta...

> Nota: CSMA/CD es una red de área local en el que, en el caso de que hayan colisiones, las trata automáticamente. En cualquier caso, CSMA/CD es una red con posibilidad de colisión por mucho que solvente el problema.

El problema surge cuando varios dispositivos **transmiten información simultáneamente** hacia una misma base provocando así una **colisión**. Para ello se necesita un **control de acceso al medio**.

> Eg:
> \
> En Alohanet el dispositivo **enviaba la información inmediatamente**:
> - Si la información llegaba correctamente se recibe un **mensaje de confirmación**.
> - Si no llega el mensaje de confirmación se **espera un tiempo aleatorio** y se **reenvía** la información.
> 
> El intervalo de espera debía ser considerable puesto que reduce los rendimiento del protocolo.

## Protocolo MAC
Se distinguen en dos tipos según los **enlaces de difusión**:
- **Acceso aleatorio**: el canal no está preasignado por lo que es susceptible a colisiones.
- **Acceso por turnos**: el canal está coordinado para evitar colisiones.

## CSMA/CD
Usado en conexiones Ethernet, viene de *Carrier Sense Multiple Access with Collision Detection* o Detección de Portador de Acceso Múltiple con Detección de Colisiones en español.

Un nodo **usa todo el ancho de banda** cuando transmite.
\
Se **comprueba si está libre el canal**. En tal caso, se transmite de inmediato. De lo contrario, se **espera** a que esté libre.
\
Mientras se transmite **se comprueba que no haya colisiones**.

La **prestación** que se utiliza es **total** entre el emisor y el receptor.

Si se produce una **colisión** se **envía una señal** que, una vez detectada por el emisor, **interrumpe la transmisión de la trama** y, en su lugar, el emisor más cercano a la colisión transmite una **señal de atasco** de 48 bits a todo el sistema.
\
Tras ello, los emisores **esperan un tiempo aleatorio** basado en el **algoritmo de retroceso exponencial binario** y, después, envían la señal.

Un detalle importante es la necesidad de establecer un **tamaño mínimo de la trama** puesto que es posible que **la colisión se detecte después de que el emisor termine de transmitir**. En tal caso, el receptor enviaría una señal de atasco que el emisor ignora creyendo que se envió la trama correctamente.

### Algoritmo de retroceso exponencial binario
Tambien llamado ***Binary Backoff*** en inglés, se asigna el **tiempo de espera**:

$$\text{``tiempo de espera''} \equiv 512 \ k \cdot \frac{1}{R}$$

> $n \equiv$ "número de colisiones"
> \
> $k$ es electo aleatoriamente entre $\{ \ k \in \N \ | \ k < 2^{m}-1 \ \}$
> \
> $m = min(n,10)$
> \
> $R^{-1} \equiv$ "tiempo de bit"

## CSMA/CA
Usado en conexiones Wi-Fi, viene de *Carrier Sense Multiple Access with Collision Avoidance* o Detección de Portador de Acceso Múltiple con Evasión de Colisiones en español.
\
Es **similar CSMA/CD** puesto que sigue siendo CSMA.

- El **emisor** detecta si el **canal está libre por DIFS** segundos. En tal caso **transmite la trama completa**. Si no, espera un tiempo aleatorio según el **algoritmo *BinaryBackoff***.
- El **receptor** comprueba si la **trama recibida es correcta**. En tal caso, devuelve **ACK** (*acknowledge*).

### Evitación de colisión RTC/CTS
Una estación solicita al AP (*Access Point*) **transmitir** una trama de datos con una **trama específica** a la que llamamos **RTS** (*Request To Send*) en la que **se indica el tiempo necesario para transmitir** toda la trama.

El AP contesta por **difusión** enviando otra **trama específica** llamada **CTS** (*Clear To Send*) que da **permiso para transmitir al solicitante** e informa al **resto de dispositivos para que no envíen**.

> Nota: se realiza el intercambio RTS/CTS cuando el tamaño de la trama supera el umbral definido por la estación. Normalmente no se utiliza porque el umbral suele ser mayor que el MTU.

![Evasión de colisión RTS/CTS](https://1.bp.blogspot.com/-PPrAOeC0O3M/YFMYV5KmUVI/AAAAAAAACQE/1aobX4TQ6UcOJ9mVDxtBnPR1oT_brjHYgCLcBGAsYHQ/s740/RTS_CTS_Message_Exchange.JPG "Wi-Fi DoS: CTS Frame Attack, por Mario Valiente, en Blog de ISecAuditors")

## Paso de testigo
Es una forma de acceso al medio **libre de colisión** muy utilizado en **topologías de anillo**.

A lo largo del sistema se transmite el **testigo**. El dispositivo que tiene el testigo tiene **permiso para transmitir**.

Si un nodo quiere transmitir sin testigo debe esperar a tenerlo.
\
En el caso de tenerlo, transmite un **máximo de tramas** y, posteriormente, pasa el testigo. Si no tiene nada que transmitir, sencillamente, **pasa el testigo**.

El motivo de su bajo uso es que **el sistema completo falla con la caída de un solo dispositivo**.

![Topología en anillo](https://redesinalambricasycableadas.wordpress.com/wp-content/uploads/2014/10/descarga-4.jpg "Topologia de anillo: Redes Inalambricas y Cableadas en WordPress")

---

## Estándares de LAN
El estándar que define el comportamiento es el IEEE 802.
> Nota: Para información detallada revisar transparencias. Interesa fundamentalmente la parte física de 802.3, 802.3z, 802.3u y sus subclasificaciones (LAN, MAN...)

La longitud de la trama debe ser de entre 64 a 1518 bytes. Esto  se debe a que 64B es el mínimo para encontrar colisiones.

- Ethernet
- Fast Ethernet
- Gigabit Ethernet
- 10 Gigabit Ethernet

> Nota: Para más información revisar transparencias.

Es interesante apreciar la diferencia entre los **tipos de conexiones** usadas y el uso de **hubs o switches** entre ellos.

> Ct: Se pide entender la notación, más o menos.

# TEMA 4: Protocolo de Internet (IP)
Para pasar los datos al enviar un paquete es necesario apoertar información. Aunque los **switches corresponden a la capa 2** y los **routers a la capa 3**, hoy en día se utiliza lo que se llama **routers de la capa 3**, que reúnen ambas caracterísitcas.

Un router tiene, **al menos, dos adaptadores de red**. El router **asciende hasta el protocolo IP** entre adaptadores para conectar los dispositivos por IP en su interior.

En cuanto se le añade la cabecera IP se habla de **datagramas** IP o paquetes.

## Datagrama IPv4
![Cabecera de datagrama IPv4](https://personales.upv.es/rmartin/tcpip/imagenes/formato-ip.gif "Protocolo de Internet (IP), por R. Martín, en UPV")

Está compuesto por los siguientes elementos:
- **Versión**: Son 4 bits que representan la versión IPv4 o IPv6. Pueden valer 4 (`0x4`) o 6. IPv6 tiene otra cabecera.
- **Longitud**: Indica el tamaño total de la cabecera del datagrama medido en 32 bits por unidad.
    > Eg: si la longitud es `0b0101`, o bien `0x5`, entonces la cabecera ocupa un total de $32 \text{b} \cdot 5 = 160 \text{b}$
- **Tipo de servicio**: Inidica la forma de enviar los datos
    > Ct: No es interesante.
- **Longitud total**: Es un campo de 16 bits que indica la longitud del datagrama en bytes pudiendo valer un máximo teórico de $2^{16} - 1 = 65535$ bytes.
\
Es redundante porque el MTU suele estar limitado a mucho menos.
- **Identificación**: Es un campo, normalmente autoincremental, que identifica el datagrama y cuyo valor está dado por el **host**.
- ***Flags***: Son una serie de 3 bits que indican información sobre fragmentación.
- ***offset* de fragmento**: Identifica el fragmento del datagrama.
- **Tiempo de vida**: El **TTL** se reduce por cada salto evitando que paquetes perdidos circulen eternamente por la red.
- **Protocolo**: Indica qué protocolo se está usando: UDP, TCP, ICMP...
- **Checksum de la cabecera**: Permite encontrar alteraciones en la cabecera.
- **Dirección IP de la fuente**.
- **Dirección IP del destino**.

### Tiempo de servicio (TOS)
Funciona de tal manera que tiene 3 bits de precedencia que indica **códigos de servicio** a los que le siguen otros **4 bits DTAC** y un último bit a 0 que no se usa:
- **D**elay para minimizar el retardo.
- **T**hroughput para maximizar la productividad.
- **R**eliability para maximizar fiabilidad.
- **C**ost para minimizar el coste.

### Time-To-Live (TTL)
Se recomienda un **valor inicial de 64 saltos**, normalmente debe ser **superior a 16** para poder legar al destino y se suele escribir en **potencias de 2**.
\
Es un valor que se **inicializa en el host** y, por cada dispositivo por el que salta, se **reduce en 1** su valor.

### Protocolo
Indica un código que corresponde a algún protocolo de la **misma u otra capa**:
- UDP con 17 o `0x0011`.
- TCP con 6 o `0x0006`.
- ICMP con 1 o `0x0001`.

### Checksum
Es un método para encontrar alteraciones con la información de la cabecera.
> Nota: Para encontrar un ejemplo se recomienda buscar el ejercicio sobre Checksum en las transparencias.

# TEMA 5: Aspectos adicionales sobre el Protocolo de Internet
> Sobre el documento: La entrada del tema 5 en las transparencias es un poco anterior. En cualquier caso es indiferente puesto que el tema 4 y 5 tratan conceptos relativos a las mismas cuestiones.

## Fragmentación de datagramas
Puede ocurrir de diferentes formas, por ejemplo, si un intermediario **reduce el MTU** de la trayectoria este mismo tendrá que fragmentarlo. El MTU máximo teórico de IP es el que corresponde con la longitud de su cabecera, es decir, 65535 bytes o 64kB.

Cuando se fragmenta, la **identificación** y los **flags** siempre se mantienen. En general, se suele copiar gran parte de la cabecera.

Entre los **flags** hay dos bits fundamentales:
- **DF** (do not fragment): indica que **no se debe fragmentar**.
- **MF** (more fragments): indica que **quedan más fragmentos**.

> Eg: en la práctica se vio que al forzar un tamaño mayor al MTU y el flag DF se avisaba de que el paquete no podía llegar porque superaba el MTU.

Es posible que un datagrama fragmentado **también necesite fragmentarse**.

En cualquier caso, los flags y desplazamiento están conformados por:
- **res**
    \
    Es un bit para uso reservado aunque ya se le ha dado algún uso.
- **DF**
- **MF**
- ***offset***
    \
    Es una cuenta para **identificar fragmentos**. El fragmento 0 es el primer fragmento. El dato del *offset* corresponde a la fórmula $\text{``posición de la información''} \over{8}$.
    > Eg: si un datagrama de 1200B pasa por una red con MTU de 600B se dividirá en dos fragmentos con
    > - fragmento 1: $\textit{offest} = 0$
    > - fragmento 2: $\textit{offset} = \frac{600\text{B}}{8} = 75\text{B}$

> Nota: Cuando se fragmenta un datagrama se **recalcula el Checksum**.

## Procesamiento de datagramas
> Nota: Para ver información sobre el procesamiento en host revisar diagrama de flujo en transparencias.

El **router puede actuar como host** pero, en la mayoría de situaciones, se dedica a efectuar el **tráfico de red**.

Tras **verificar el Checksum**, lo primero que hace es **reducir el TTL**.
\
Posteriormente, sigue de la forma esperada. Para información completa revisar el diagrama de las transparencias.

> Ct: Esto cae en los exámenes: el **datagrama *siempre* cambia** entre saltos porque se reduce el TTL.

> Ct: En el examen las longitudes de las partes de los datagramas van a cuadrar con lo esperado.

## Direcciones IPv4
Indican la **dirección lógica** de un host. Son virtuales porque son interpretadas a nivel de software y hay tantas como adaptadores.

Se representan con **4 octetos** y, por tanto, 4 grupos de $2^{32}-1=255$.

### Routers y direccionamiento
Cada router tiene, al menos, dos direcciones IP. Una de ellas es privada y su fin es comunicarse con la red privada. La otra es pública y permite el acceso a Internet.

![Direccionamiento de la red](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEj-TWU0Jgdcli6V5XZQNrlt52C5RDznXLDZRHW6iUetd1qfW5q2CrJfeZSPsqG46gVKb778NdbktzXYk2thIhaUZ2U4YiIxQVYJcCVCRIblzZhn8WxxNwZC_tkaFbXuE8u8nQ-Kr6VPK__d/s1600/puerta-de-enace-o-gateway.jpg "Tecnologías de Información, Comunicaciones y Automatización, por Cibervirtual")

### Direcciones especiales
Hay ciertas direcciones que son especiales por sus condiciones:
- Direcciones de la **red**: `<prefijo de red>, <resto en 0>`
- Direcciones de **loopback**: `127.<dirección>`
- Dirección del **host**: `0.0.0.0`
- Dirección de **difusión dirigida**: `<prefijo de red>, <resto en 1>`
- Dirección de **difusión en red**: `255.255.255.255`
- Direcciones de **redes privadas**

> Nota: "Resto en 1" hace referencia a la escritura bit a bit.

### Tipos de direccionamiento en Internet
Hay dos tipos de direccionamiento según si viene con **máscara de subred** especificada se considera sin clase. De lo contrario, se usa el direccionamiento con clase.
- **Direccionamiento con clase**: pueden ser **A**, **B**, **C**, *D* o *E*.
- **Direccionamiento sin clase**: se proporciona una máscara de subred.

En las redes con clase se identifica la clase por medio del primer bit:
```
* 0<red> - Red de clase A
* 1<red> - Red de clase B 
* 01<red> - Red de clase C
* 001<red> - Red de clase D
* 0001<red> - Red de clase E
```
> Nota: Se debe recordar que `127.<red>` corresponde a una red especial.

Según la clase de la red habrá más espacio para **subredes o  hosts**.

#### Direccionamiento sin clase
También abreviado como CIDR, no hay clases basadas en el prefijo de la red. Esta proporciona una **solución a la falta de direcciones**.

Estas redes son de la forma `<dirección IP>/<máscara de subred>`. La máscara es la **cantidad de bits a 1 desde la izquierda en la IP compartida con notación en binario**.
> Eg: con IP `255.255.240.0` tenemos en bits `11111111.11111111.11110000.00000000` corresponde con una subred `255.255.240.0/20` dado que hay un total de 20 bits a 1 desde la izquierda.

La **dirección de broadcast** corresponde con disponer a 1 todos los bits finales, es decir, **no se debe poner 255 de golpe** dado que induce a error.

Igualmente sucede con la **dirección de la puerta de enlace** que puede provocar error si se realiza con datos incorrectos la operación AND.
> Ct: En los exámenes deben haber problemas con la dirección de broadcast y puerta de enlace cuando hay máscaras de subred.

> Nota: Para más información ver ejemplo en las transparencias.

### Superred
Consiste en disponer redes de forma **contígua**, dentro de un mismo octeto, de tal forma que tienen un **prefijo común** disponiendo así de **múltiples redes a la vez**. Su se da fundamentalmente en entornos empresariales.

### Direcciones privadas
Corresponden a direcciones lógicas **no encaminables** por los routers de Internet. Sus rangos corresponden a:
- `10.0.0.0/8` - 1 red de clase A
- `172.16.0.0/12` - 16 redes de clase B
- `192.168.0.0/16` - 256 redes de clase C

> Nota: La máscara de subred para las redes privadas de la clase B no es divisible entre 8 lo que implica que su notación no corresponde a redes con clase.

#### Obtención de una dirección IP
Manualmente, el administrador de red puede asignar valores a un host. De forma automatizada se utiliza **DHCP**.

Un bloque de direcciones se consigue a través del **ISP** que ha pagado por ellas. A su vez, el IPS proporciona direcciones de forma enumerada y ordenada.

Un IPS obtiene las direcciones IP por medio del **ICANN** que proporciona direcciones IP, direcciones DNS y **resuelve posibles conflictos** entre concesiones. Los países delegan la administración a espacios **geográficos**.
> Eg: España delega la administración a **RIPE NCC**.

Al revisar la reserva de direcciones IP en la [página de IANA](https://www.iana.org/assignments/ipv4-address-space/ipv4-address-space.xhtml) se puede notar que hay redes reservadas por la propia organización. Estas corresponden a distintos motivos como direcciones de *broadcast*, direcciones privadas o reservadas para uso futuro.
> Eg: la red 193 es la utilizada por la Universidad de La Rioja y está reservada por RIPE NCC.

### Encaminamiento IP
Incluye las pautas sistemáticas de lo que hace el router.
\
Los routers y hosts tienen **tablas de encaminamiento** que deben ser **compactas y pequeñas** con información únicamente fundamental:
- Direccion IP de **destino**
- **Máscara de red**
- Adaptador de **salida**
- Dirección IP de **próximo salto**

> Nota: Para ver ejemplos se recomienda revisar las transparencias.

Es importante recordar que el **router tiene una tabla ARP**.

El ISP compra un prefijo de dirección IP que usará para redireccionar a diferentes hosts. Ese prefijo de red va a dividir otros prefijos de forma que **engloba el direccionamiento de redes en packs de 16**.
Dicho de otra forma, los proveedores **suborganizan en 16 redes** por prefijo creando diferentes subredes.
> Nota: Para información aclaratoria revisar transparencias (CIDR reduce el tamaño de las tablas de encaminamiento) notar que `/20` corresponde a 16:

> Eg:
> - ISP compra `200.25.0.0/16`
> - Destina `200.25.16.0/20`
> - A partir de ahí se instalan hosts

## NAT
El *Network Address Translation* es el encargado de gestionar el problema de la **falta de direcciones IPv4 públicas para todos los hosts**. Para ello, se asignan **direcciones IP privadas** a todos los hosts.
\
Hay dos tipos:
- NAT:
    \
    $1 = Card(\text{hosts privados}) \ge Card(\text{hosts públicos})$
- PAT:
    \
    $1 < Card(\text{hosts privados}) \ge Card(\text{hosts públicos})$

Cuando se utiliza **NAT**, el **router intercambia su IP por la de origen** a la salida de la información de tal forma que el destino ignora la existencia del host privado. A la llegada de información, el router **reencamina la información de acuerdo con una tabla NAT**.

Cuando se utiliza **PAT**, el router, aparte de intercambiar la IP de origen así como gestionar la información de llegada de acuerdo con una tabla NAT, se utiliza y el método se **replica con puertos**. Está orientado a múltiples hosts.

### Limitaciones de NAT
Aunque NAT funciona correctamente para las secciones con **control del router**, es decir, capas 2 y 3, el protocolo encuentra **problemas con el resto de capas**.

Es común que se replique la información IP en la cabecera de la capa de aplicación lo que, evidentemente, **escapa al router y a NAT por consiguiente** lo que puede generar problemas.

## DHCP
El *Dynamic Host Configuration Protocol* tiene como objetivo **proporcionar una dirección IP privada**.

Este protocolo permite, además, reutilizar direcciones IP.

El mecanismo tiene 4 fases (DORA):
- **Discover**
    \
    El host envía por difusión `255.255.255.255` que su dirección IP corresponde a `0.0.0.0` con el fin de que le proporcionen alguna.
- **Offer**
    \
    **Múltiples servidores DHCP** ofrecen múltiples direciones para el host por medio de protocolos de **dirección MAC**. Además, se envía el IP del servidor DHCP y un **tiempo de vida** para el servicio.
- **Request**
    \
    El host envía por la **dirección de broadcast** y desde la IP `0.0.0.0` la dirección IP que pretende tomar.
- **Acknowledge**
    \
    Este mensaje se envía con las **direcciones IP definitivas**.
    
## Protocolo ICMP
Es encargado de informar de fundamentalmente **posibles errores** en la entrega de un datagrama.
\
Cumple con el siguiente formato:
- **tipo** (1B): identifica el tipo de mensaje.
- **código** (1B): espeifica el tipo de mensaje.
- **checksum** (2B): con mismo algoritmo que IP.
- **resto de cabecera** (4B): dependiente del tipo y código.

Hay 15 tipos de error siendo fundamentales los de **petición de *echo*** y los de **error**.

Los mensajes de error de ICMP siguen un formato específico:
tipo de dato | tamaño | contenido
---: | :--- | :--
Type | 1B | Identificación del error de ICMP
Code | 1B | Especificación del error de ICMP
Checksum | 2B | Verificación de integridad de la cabecera
Rest of header | 4B | Contenido adicional dependiente del Type y Code
Data | 1472B | Copia de la cabecera IP e ICMP del mensaje perdido

El objetivo es **evitar la aturación de red** por cabecera de errores.

Los dispositivos pueden enviar mensajes de error en distintas situaciones:
- **Routers**
    \
    Pueden enviar un **mensaje ICMP de error** cuando el **TTL=1**.
- **Hosts**
    \
    Pueden provocar un error si envían más datos de los que se pueden cargar.

En el caso de que no se pueda llevar al receptor el datagrama se obtiene **destino inalcanzable**, con múltiples códigos para ese tipo.

![Codes de destino inalcanzable](https://telematika2.wordpress.com/wp-content/uploads/2011/03/tabla2_icmp.jpg "Protocolo de Control de Mensajes en Internet (ICMP) en Telematika2")

## IPv6
Los motivos principales son **el agotamiento de espacio de direcciones**, las **nuevas aplicaciones** y los **grupos de trabajo a nivel internacional**. Proporciona una infromación de identificación con 128 bits. Hay 3 tipos de direcciones:
- **Unicast**: de un solo computador
- **Multicast**: de un grupo de computadores a todos
- **Anycast**: de un grupo de computadores a uno

![Cabecera IPv6](https://certificaciondesistemasoperativos.wordpress.com/wp-content/uploads/2016/04/b2ec6-cabecera.png?w=484&h=254 "IPv4 – IPv6 en Certificacion De Sistemas Operativos")

Se tiene previsto una **fase de transición** donde convivan IPv4 e IPv6.
\
Durante la transición hay **túneles** que permiten encapsular el tráfico IPv6 que pase por las conexiones destinadas a IPv4.
\
Hay formas de mapear direcciones IPv4 en IPv6. Entre las más relevantes se incluye mapear la IPv4 por medio del prefijo `::FFFF:<IPv4>`.

En los túneles es esperable problemas como la **superación del MTU** cuya gestión la realiza automáticamente el router con las técnicas vistas.

# TEMA 6: Enrutamiento a nivel de red
Hay dos tipos de enrutamiento:
- Enrutamiento por **estado de enlace**
    \
    Utilizando el protocolo OSPF con el algoritmo de Dijkstra
- Enrutamiento por **vector de distancia**
    \
    Utilizando el protocolo RIP con el algoritmo de Bellman-Ford

## Algoritmos de encaminamiento
Se pretende determinar el **mejor camino** en el que, representado como un **grafo**, será el camino que pase por la menor cantidad de aristas o **enlaces** de acuerdo un un **valor numérico de coste**. Este valor depende fundamentalmente de la calidad de la red y la distancia.
\
La red de Internet suele estar dividida y enumerada por **sistemas autónomos** que utilizan un **mismo algoritmo de encaminamiento**. Los sistemas autónomos se interconectan en **enrutamiento jerárquico**.

![Sistemas autónomos de red](https://blog.gonzaleztroyano.es/content/images/2022/10/image-1.png "¿Qué es un Sistema Autónomo? Y, ¿qué es Internet?, por Pablo González Troyano, en Pablo González Troyano")

Según las caracterísitcas se pueden distinguir distintos **tipos de encaminamiento**. Lo normal es que sean **escalables y distribuidos**:
- **estático**: con actualización **manual**.
- **dinámico**: sensibles al cambio en el tráfico o **topología de red**.

Hay tipos de protocolos de enrutamiento:
- **Intradominio**
    - **RIP**: *distance vector*
    - **OSPF**: *link state*
- **Interdominio**
    - **BGP**: *path vector*

## Encaminamiento por estado del enlace
Necesita dos condiciones:
1. Cada nodo conoce la **topología completa**
2. Cada nodo conoce la **condición del enlace** (*up or down*)

En tal caso, se puede **obtener la tabla de encaminamiento** por algoritmo de **Dijkstra**.

El router, que conoce los costes del resto de routers, prepara y **difunde un paquete de estado de enlace** a todos los routers de la red. A partir de ahí, cada grafo:
1. **Construye el grafo de la red**
2. **Calcula el camino más corto de Dijkstra**
3. **Construye la tabla de encaminamiento**

Este proceso puede suceder por dos motivos:
- **Periódicamente**, normalmente tras horas.
- Tras **cambios en la topología** de la red.

> Nota: El cambio periódico es modificable por el administrador del sistema.

Cada nodo conoce la **distancia a sus vecinos**. Esta información se **difunde** por toda la red. Con esa información se calcula el **algoritmo de Dijkstra** para cada destino.
\
Cada nodo construye el paquete con:
- Nodo **transmisor**
- Lista de **vecinos y distancia**
- Número de **secuencia**
- Timpo de vida (**TTL**)

Para el envío de un **paquete de estado de enlace** (PEE) se copia, se comprueba que su número de secuencia es mayor al presente en el dispositivo y, posteriormente y en tal caso, lo difunde a sus vecinos.

> Ct: Hacer el agloritmo del router para sacar la tabla de encaminamiento es ejercicio que ha caído en examen.

> Nota: Para ver un ejemplo de las transparencias se recomienda ver las transparencias.

> Ct: Se ha explicado durante 1 hora el algoritmo de Dijkstra y la obtención de la tabla de encaminamiento.

### Open Shortest Path First (IP/OSPF)
Es un algoritmo por **estado de enlace**. Peculiarmente, se envía  **directamente** sobre la cabecera IP pero **no pertenece a la capa de transporte**.

Utiliza el algoritmo de Dijkstra para conocer el camino más cercano y modificar así la tabla de enrutamiento.

El coste del envío se hace por medio de la siguiente operación:

$$C = max(int(\frac{10^{8}}{velocidad}, 1))$$

Hay una serie de características adicionales destacables sobre OSPF que no tiene RIP:
- ***jerarquías de encaminamiento***
- **seguridad**
- **múltiples caminos**
- **diferentes métricas**
- **multicast**


![Relación de zonas fronterizas](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjV6tK7cgczo1aNfsqYgbVeNRcKJAiV5gAUmE-d9Kw4cTj_tdjjPLNyxKiD8wARvkCMlUnOOfD2wIxMIZQdgTSpbiMpyvjmam8XkI925Ds4e4TyHqDStYNb6CSLA-F2khX3dJxMPRpMCLg/s1600/Jerarquia_OSPF.gif "OSPF, por Luis Angel Saldaña Torres, en o0oyandel.blogspot.com")

## Encaminamiento por vector de distancias
Cada nodo mantiene un **vector de distancias** que contiene una estimación de **su distancia al resto de nodo de la red**.
\
A partir de la información conocida y de lelgada se estiman los nodos óptimos.

El algoritmo es **iterativo y asíncrono** porque se repite periódicamente y también responde a cambios de costes. 
\
Es un algoritmo **distribuido** porque no hay ningún nodo central.

El algoritmo funciona de tal forma que **el vecino proporciona su tabla** y, a partir de ella, se estima el coste **sin conocer la topología de la red**. Su funcionamiento es casi recursivo: el nodo origen calcula el coste del nodo destino a partir de su coste al siguiente salto (vecino) y el coste del destino con respecto al vecino.

Se supone que el costo a un **nodo inaccesible** es infinito.

### Problema de la cuenta al infinito
Si un nodo cae es lo **teóricamente esperado** que se produzca una emisión repetida para informar a un nodo inaccesible.
\
La solución fue **dar por perdido el nodo tras 16 intentos** .

### Routing Information Protocol (RIP) IP/UDP
Aunque es parametizable, si un router no da señal tras 180 segundos, se da por muerto. En tal caso, se **elimina el nodo de la tabla de encaminamiento** y se **detiene la propagación del error** tras 16 saltos.

---

## Encamianmiento en Internet
Internet no es una red plana por lo que es necesario que se cumpla:
- **Escalabilidad**
- **Autonomía administrativa**

> Nota: Los algoritmos tendrían problemas de convergencia si no se utilizasen sistemas autónomos y la red se saturaría con paquetes de control.

La solución es el **encaminamiento jerárquico de sistemas autónomos**. Estos sistemas autónomos tienen funciones de encaminamiento **intra-SA** pero, además hay **routers pasarela** con un algoritmo adicional **inter-SA** que rara vez es RIP u OSPF. En cuyo caso, se usa BGP (IPv6/TCP)

![Relación de sistemas autónomos por BGP](https://www.researchgate.net/profile/Shaza-Hanif/publication/265626655/figure/fig1/AS:669443558498308@1536619190306/BGP-protocol-illustration.jpg "BGP - Border Gateway Protocol Bgp Optimale Routen Reflektion Cisco, por Pamela Knowles, en rytomiajygybi")

### Encaminamiento entre sistemas autónomos: Border Gateway Protocol (IPv6/TCP)
Permite a los sistemas autónomos **obtener y propagar información**. Es un protocolo complejo que hace uso de **TCP semi-permanente** que se llaman **sesiones** dentro y fuera del sistema autónomo.
\
Los routers no hacen uso necesariamente de una conexión directa entre routers.

Hace uso de un algoritmo por **vector de caminos** que trabaja con **rutas completas**. Cada sistema autónomo está identificado por un único **ASN**. Cada pasarela informa de la secuencia de sistemas autónomos atravesados hasta el destino.
\
Trabajar con rutas completas impide los bucles por caída.

# TEMA 7: Nivel de transporte: UDP
El **nivel de transporte** roporciona un servicio de **comunicación entre extremos** posicionándose entre la capa de aplicación y de la de red.

## Direccionamiento de transporte
El puerto de dirección de transporte es **distinto al puerto de nivel de red**. El **puerto de red** es un punto de conexión entre computadores mientras que los **puertos a nivel de transporte** es un punto de conexión entre **aplicaciones**.

El puerto proporciona un **identificador de servicio** entre `0`-`65535` valores con sus respectivos **valores reservados**:
- `0`-`1024`: puertos conocidos.
- `1025`-`49151`: puertos registrados.
- `49152`-`65535`: puertos de uso privado/personalizado dinámicos.

> Nota: Para ver detalles de programación relacionados con creación de mensajes UPD y TCP revisar transparencias.

> Nota: Por norma general, los puertos **conocidos y registrados** son utilizados por **servidores** mientras que los puertos **privados** son usados por **clientes**.

## Demultiplexado con conexión
Es un juego de puertos de origen y destino. El servidor **siempre trabaja con el mismo puerto** pero las conexiones tienen **distintos puertos en el lado del cliente** permitiendo múltiples conexiones a un mismo dispositivo.

## Protocolo UDP
Es un protocolo de transferencia **no fiable** porque no comprueba el estado de la conexión.
\
Su ventaja es tener una **sobrecarga mínima de cabecera** con **bloques de hasta 64kB** permitiendo enviarse en difusión. Proporciona una conexión full dúplex.

Si es necesario, el paquete se **segmenta** en paquetes de datagramas. No obstante, cualquier **pérdida de estos paquetes debe ser tratada por la aplicación**.

Dado que el peso de su cabecera es mínimo, permite llevar más información  en un solo mensaje. No se almacena **ningún búfer** por lo que el mejor recurso para asegurar la información es el **número de secuencia** que permitirá a la aplicación comprobar y ordenar paquetes.

La cabecera UDP está conformada por 2 gruposde 32B (64B):
- Puerto **origen**
- Puerto **destino**
- **Longitud** de datagrama
- ***Checksum***

El *Checksum* se calcula sobre una **pseudocabecera** seguido de la cabecera real y datos UDP. El proceso es similar al convencional.

Conviene usar UPD en casos de:
- **pocos datos**
- **multihost** o **broadcast**
- paquetes a **tiempo real**
- reducir necesidades en recursos
- esquema de **verificación proporiconado por aplicación**

# TEMA 8: Nivel de transporte: TCP
TCP se caracteriza por proporcionar medios de **comprobación del mensaje**. Para asegurar la fiabilidad se deben contemplar los **distintos niveles de transferencia en la red**.

A diferencia de un canal ideal, en un canal real pueden darse situaciones de **error de transmisión**, **congestión de red**, **mal encaminamiento**, **permutación**...
> Nota: Deben distinguirse estos problemas, no son sinónimos.

## Automatic Repeat Request
El ARQ proporcioa una serie de emdios para **detectar errores**. Los mecanismos previstos son:
- **Reconocimientos**: Mensajes ACK cuya llegada puede fallar.
- **Retransmisión**: Con un respectivo *timeout*.

Teóricamente, lo que se ve se plantea en la capa de enlace pero funciona mejor en la capa de transporte de cara a la realidad.

### Detección de pérdida de segmento
Se envían una serie de datos. Los datos enviados funcionan de acuerdo con el diagrama de secuencia proporcionado.

![ARQ por reconocimientos](https://w3.ual.es/~vruiz/Docencia/Apuntes/Networking/Protocols/Level-4/04-protocolos_ARQ/ARQ_stop_and_wait_ACK_perdido.png "Protocolos ARQ, por Vicente González Ruiz, en Universidad de Almería")

El problema sucede cuando **se pierde el mensaje de ACK**. En tal caso, se enviará la información duplicada.

#### Stop & Wait
Pretende solventar el problema de los duplicados por medio de un **enumerador de paridad** de 1 bit.
\
El ACK funciona de tal forma que, una vez obtenido el mensaje de paridad 0 se exige el 1, tras obtener el 1 se exige el próximo 0 siguiendo así de forma sucesiva. Si no se llegase a recibir se enviaría de nuevo el paquete perdido.

El mayor problema de este método son **los tiempos en grandes distancias**.

![Stop&Wait](https://media.geeksforgeeks.org/wp-content/uploads/Stop-and-Wait-ARQ-7.png "Stop and Wait ARQ en GeeksforGeeks")

### Ventana deslizante
Es un método de **envío de información a mayores distancias**. Funciona de tal forma que se envían **múltiples segmentos** y, al mismo tiempo, se **exige el siguiente segmento**.

Funciona de una forma más comunicativa que Stop & Wait-
\
Se conforma una **ventana deslizante de una cantidad de segments**. Estos segmentos son enviados, el receptor envía un mensaje **exigiendo el siguiente segmento de la ventana** tras la recepción. La enumeración del segmento de la ventana se reinicia una vez terminada la ventana.

El problema que enfrenta este método es la llegada de **segmentos desordenados**. Hay dos métodos de resolución:
- **go-back**: No se contempla ni se utiliza en la realidad.
- **selectivo**: Para su uso necesita una **ventana de recepción**.

![Ventana deslizante](https://upload.wikimedia.org/wikipedia/commons/thumb/9/9d/Ventana_deslizante_2.JPG/1280px-Ventana_deslizante_2.JPG "Ventana deslizante en Wikipedia, la enciclopedia libre")

#### Go-Back-N ARQ
El **receptor ignora las tramas fuera de orden**. Si el remitente no recibe un ACK después de un tiempo de espera entonces el remitente **vuelve a enviar la totalidad de la ventana**.

El método no es muy efectivo debido a la pérdida de tiempo en **retransmisión**, **propagación** y posterior espera al ***timeout*** puesto que el receptor desecha los paquetes que no corresponden al orden adecuado. El remitente reinicia tras el último paquete correcto.

Se consume mucho ancho de banda en paquetes a desechar. Si la red está congestionada los routers se atascan y asesinan los paquetes que no quepan en el *buffer*. Además, este problema escala por **retroalimentación**.

#### Selective Repeat ARQ
Añade una **ventana de recepción** en la que el receptro **almacena paquetes en desorden** dejando en dicha ventana **huecos** dispoinbles para paquetes perdidos o desordenados.

La ventana de recepción se incrementa con cada **llegada de paquete ordenado**. En el remitente cada paquete tiene su *timeout*. Si el receptor pierde un paquete deja un hueco de la ventana y **espera a que el remitente lo reenvíe por espera de *timeout***.

#### Piggybacking
Es una técnica que consiste en **enviar reconocimientos en paquetes de comunicación** lo que puede reducir el tráfico en la red. No obstante, requuiere **comunicación bilateral**.

## Segmento TCP
El Transmission Control Protocol es un servicio orientado a conexión.
### Maxmum Segment Size
El **MSS** es un dato comunicado al inicio de la conexión. Se obtiene a partir del **MTU**.
\
Por defecto, el MSS es de 536 bytes para TCP por IPv4. El máximo con un MTU de 1500 bytes se calcula restando las cabeceras tal que $1500\text{B}_{MTU} - 20\text{B}_{cabecera\ IP} - 20\text{B}_{cabecera\ TCP} = 1460\text{B}_{MSS}$.

![Encajonamiento de cabeceras TCP](https://www.malwaresa.com/wp-content/uploads/2023/01/intro_42-1.png "3.1.4.2. Estructura de datos de los protocolos de la suit IP/TCP en Malware SA")

### Formato de un segmento TCP
![Formato del segmento TCP](https://cv.uoc.edu/UOC/a/moduls/90/90_329/web/imagenes/f6_18.gif "Formato del segmento TCP en Universitat Oberta de Catalunya")

- **Puerto de origen** (16b).
- **Puerto de destino** (16b).
- **Número de secuencia** (32b): Permite la **ordenación de segmento** por **numeración de bytes** tomando un **valor inicial aleatorio**.
- **Número de reconocimiento** (32b): Similar al número de secuencia a nivel de **recepción**.
    > Nota: Se toma un valor aleatorio inicial (**ISN**) y se va incrementando de tal forma que el cliente pide el siguiente byte a recibir.
    > > Eg: si el número de secuencia absoluto es 532 y se reciben 536 bytes el host pedirá en el número de reconocimiento el byte $532 + 536 = 1068$.
    >
    > Ello con la salvedad de recibir un flag `SYN` o `FIN` puesto que consumen un número de secuencia aunque no lleven datos (**byte fantasma**).
    > > Eg: siguiendo con el ejemplo, supondría un número de reconocimiento de 1069.

- **Longitud de cabecera** (4b).
- **Reserva** (6b): Ya se le ha dado uso a alguno.
- **Código** (6b): *flags*.
- ***Win*** (16b): Indica el **tamaño de ventana** y, posteriormente, se añadió un multiplicador en el campo de opciones debido a los avances en *hardware*.
- ***Checksum*** (16b).
- **puntero a datos urgentes** (16b): Se puede disponer un puntero a datos de lectura urgente.

#### Campo de *flag*
Códgo | Valor | Descripción
---: | :---: | :---
14 | `SYN` | Indica el **inicio de la conexión**. La respuesta es un `SYN + ACK`.
15 | `FIN` | Indica el **final de la conexión**. La respuesta suel ser un `FIN + ACK`.
11 | `ACK` | Indica la **validez del reconocimiento** y pide el **próximo byte**.
12 | `PSH` | Indica una solicitud de **push a la aplicación**.
10 | `URG` | Indica **datos urgentes** obtenibles fuera de orden. (Eg: `CTRL+C`)
13 | `RST` | Indica un **cierre repentino**.

> Ct: Se verán con profundidad luego.

#### Números de secuencia y reconocimiento
Son campos de 32 bits (5 bytes) que identifican el **orden del segmento**. El número de secuencia del emisor es el de recepción del receptor.

Se inicializan con un valor inicial aleatorio llamado ***initial secuence number*** (**ISN**). Este número se **incrementa con bytes reconocidos**. El primero reconocimiento lleva el **ISN**. Todos llevan $ISN+N \cdot MSS$ siendo $n \equiv \text{número de segmento}$ inicializado en 0.

#### Opciones
Pueden indicar diferente información:
- `0`: nada
- `1`: sin operación
- `2`: MSS

En el caso del 2 se indica el tamaño del MSS al receptor. Se **reservan 4 bits** para indicarlo.
\
Entre opreaciones suele haber un 1 (`NOP`: sin operación) para separar opciones.
\
Entre otros casos, el caso 3 proporciona el tamaño de la ventana. Se le proporciona una longitud de 3 y un campo multiplicador debido a los avances en el *hardware*.

Existe una **longitud determinada por opción** orientada a la cantidad de argumentos que requiere y su tamaño.

## Control y flujo del error
El objetivo es **reconocer y transmitir las pérdidas** detectadas por el *Checksum*.
\
La ventana deslizante proporciona una solución a la llegada de **paquetes en desorden** pero **limita la cantidad de paquetes pendientes de reconocimiento** debido a la ventana de transmisión.

### Temporizador RTO
El **RTO** es una variable **no constante** que depende de los retrasos de la red, la cantidad de tráfico y las velocidades de transmisión. Por ello es de carácter **adaptativo**. Para que funcione correctamente es necesario que se cumpla $RTO > RTT$.

Para estimar el RTO se utiliza el **algoritmo de van Jacobson**:
- $RTT_\text{estimado} = (1 - \alpha) \cdot RTT_{\text{estimación}} + \alpha \cdot RTT_\text{muestra}$ tal que $\alpha \in [0, 1)$, normalmente $\alpha = 1/8$
- $RTT_\text{dev} = (1 - \beta) \cdot RTT_\text{dev} + \beta \cdot | RTT_\text{muestra} - RTT_\text{estimado} |$ tal que, normalmente, $\beta = 1/4$
- $RTO = RTT_\text{estimado} + 4 \cdot RTT_\text{dev}$

### Duplicación del intervalo de espera
Proporciona un problema: hay ambigüedad de RTT en retransmisiones. La solución es no tener en cuenta las medidas de RTT de los segmentos retransmitidos Como se dobla el tiempo se habla de ***Exponential Backoff***.

### Reconocimientos acumulativos
Se reconoce el **último segmento recibido correctamente y en seceuncia**: cada recepción tiene la **posibilidad de generar un reconocimiento**.

### Generación de reconocimientos
No es necesario enviar un `ACK` por cada segmento, se pretende **retrasar hasta dado algún caso**:
- recibir varias segmentos
- enviar un segmento de datos en sentido contrario (*piggybacking*)

> Nota: Reduce el tráfico.

### Reconocimientos duplicados
No se retrasan los segmentos, se envían junto a los reconocimientos. Puede generar **segmentos desordenados o perdidos**.

## Gestión de la conexión TCP
Corresponde a lo relativo a las condiciones fáticas.
### Establecimiento de la conexión
Requiere tres segmentos para el establecimiento.
1. **Petición** del cliente.
2. **Aceptación** por el reconocimiento del servidor.
3. **Reconocimiento** del cliente al servidor.

![Sincronización TCP](https://www.ionos.es/digitalguide/fileadmin/_processed_/d/e/csm_EN-tcp_0da4a9188a.webp "TCP (Tra­n­s­mi­s­sion Control Protocol): retrato del protocolo de tra­n­s­po­r­te en IONOS")

### Cierre de conexión
Hay distintas formas de cerrar la conexión. Se proporciona el cierre en **4 fases**.

![Finalización TCP](https://www.ionos.es/digitalguide/fileadmin/_processed_/2/b/csm_EN-tcp-verbindungsabbau_f34500b450.webp "TCP (Tra­n­s­mi­s­sion Control Protocol): retrato del protocolo de tra­n­s­po­r­te en IONOS")

Con respecto al `RST`, puede darse un cierre distinto.

![RST TCP](https://i0.wp.com/lab.wallarm.com/wp-content/uploads/2024/01/297.jpg?w=770&ssl=1 "TCP Resets from Client and Server aka TCP-RST-FROM-Client en Wallarm")

## Control de congestión
Los routers tienen unos ***buffers* de capacidad limitada**. Si se llenan los *buffers* se **descartan los paquetes**. Como los segmentos perdidos se retransmiten, **la pérdida por congestión tiende a retroalimentarse**.

El protocolo TCP **pretende reducir la congestión proporcionando un trato equitativo** de la capacidad. Para ello, se usa la **ventana de congestión**.

### Ventana de congestión
Corresponde a una **estimación de tráfico máximo para la red de la conexión**.
\
La ventana de congestión, dependiente de las capacidades de la red, **limita el tamaño de la ventana de transmisión**:
```
ventanaTransmisiónMAX = min(win, ventanaCongestión)
``` 
Se proporcionan tres algoritmos, que suelen implementarse juntos, cuyo fin es reducir la congestión de red:
- ***Slow Start*** (Arranque lento)
- ***Congestion Avoidance*** (Incremento aditivo)
- ***Multiplicative Decrease*** (Reducción multiplicativa)

En el caso de que se detecte algún problema se seguirá la siguiente tabla:
Detección del problema | Actuación | Arranque | Interpretación 
:--- | ---: | :--- | :---
***timeout*** | Reducir **umbral** a su mitad | *Slow Start* | Hay congestión en la red y algún router no ha podido almacenar el mensaje en su *buffer*.
**3 `ACKs` duplicados** | Reducir el **umbral** y la **ventana de congestión** | *Congestion Avoidance* | Hay congestión en la red, al receptor no le llega el mensaje y es la tercera vez que lo pide.

#### *Slow Start*
No se comienza retransmitiendo todos los segmentos de la ventana. En su lugar, **inicialmente la ventana de congestión es pequeña** y, posteriormente, tiene un **crecimiento exponencial**.
```
ventanaCongestión = 2 // Mensajes
while (comunicación) {
    ventanaCongestión = ventanaCongestión * 2
}
```

#### *Congestion Avoidance*
Se utiliza un **umbral** que puede ser **inicialmente igual a *win***. Prosigue con un **crecimiento lineal** del umbral. El crecimiento se detiene en los siguientes casos:
- El tamaño **alcanza la ventana de recepción**.
- Hay **algún problema** en la comuniación:
    - Si hay **motivo de pérdida** por vencimiento de *timeout* se **reduce el umbral a la mitad**.
    - Si hay **motivo de 3 `ACK`s duplicados** se interpreta que hay congestión y se **reduce el umbral y la ventana de congestión**.

