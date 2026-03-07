---
title: GI 2 Redes de Computadores
author: Christian Velasco Pérez
---
# GR 2: Redes de Computadores
*Autor:* Christian Velasco Pérez <img src="https://iili.io/fpTTGnt.md.jpg" alt="Skopez" align="right" style="width:15%; margin-left:4%;margin-bottom:2%">
\
El siguiente contenido corresponde a un **apoyo** educativo para cualquier interesado y por eso puede contener fallos. El documento está orientado al curso de *Redes de computadores* del Grado en Ingeniería Informática de la Universidad de La Rioja y se considera completa responsabilidad del lector lo que haga con la información de este documento.
\
La distribución del documento queda reservada al permiso explícito de su autor. Si necesitase información de contacto puede [enviar un correo](mailto:velskopezz@gmail.com).

---

# Teoría previa
## Direcciones físicas IEEE
Identifican un **adaptador de red** real.
\
Todas estas comparten un **esquema de 48 bit** dado por IEEE. Estas **direcciones físicas** o direcciones MAC se componen de **3 primeros octetos indicando el fabricante** a los que le siguen otros **3 octetos identificando el adaptador**.

Estas direcciones físicas le corresponden al dispositivo y, por lo tanto, cambiar de red no modificará la dirección física del dispositivo.

Todos ellos incluyen una **dirección de difusión** tal que `ff:ff:ff:ff:ff:ff`.

### Asociación entre dirección física y dirección IP
La comunicación entre sistemas de *misma red física* requiere el conocimiento de las **direcciones físicas e IP**. Para conocer las direcciones físicas, necesarias para la **trama**, es necesario usar el protocolo de resolución de direcciones ARP (*Adress Resolution Protocol*)

ARP funciona de tal manera que:

1. Se envía un **menasje por difusión** en la **subred**: "¿Quién (MAC) tiene la dirección IP proporcionada?"
    > Nota: En el caso de la Universidad de La Rioja la subred física corresponde a todos los laboratorios informáticos.
    El mensaje será el siguiente:

    tamaño | nombre | función
    --: | :-- | :--
    6 | Dirección destino | A lo largo de la práctica será `ff:ff:ff:ff:ff:ff` porque se enviará por difusión
    6 | Dirección fuente | La dirección del emisor
    2 | Tipo | Incluye el tipo de protocolo
    46-1500 | Trama | Inlcuye los datos
    4 | CRC |

    > Nota: Tipo 0x806 es ARP

    > Nota: La trama mínima es 46. Como no va a alcanzar habrá relleno de `1`s. Esto no se verá en la práctica porque los procesos lo omiten.

2. El dispositivo al que se le pregunta la dirección **devuelve el mensaje completando la dirección física**.
3. La información se guarda en una tabla de **caché ARP** para evitar saturar el tráfico de red si la conexión es frecuente.

---

# CMD
Abrimos **CMD** como administrador. Al ejecutar el comando `arp -a` veremos la **tabla ARP del dispositivo**.
\
Podemos ejecutar `arp -d *` para borrar la tabla. Para ello debimos ejecutar como administrador.

Notaremos que, *tras borrar la tabla de direcciones*, al enviar alguna otra persona un **ping por broadcast**, aunque sea a otra IP, la recibiremos y podremos **registrarla con Wireshark**.

La práctica concluirá con una petición de resolución de dirección a la **puerta de enlace** que puede encontrarse ejecutando `ipconfig /all` y revisando la conexión de Ethernet adecuada.
\
Para enviar la petición no se usará `ping`. En su lugar, se utilizará la aplicación virtualizada **Packet Builder** en la que habrá que incluir un mensaje en la trama.