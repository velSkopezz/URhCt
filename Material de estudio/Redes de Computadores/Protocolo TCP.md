# Redes de Computadores: Protocolo TCP

Este es uno de los temas más importantes de toda la asignatura. Se trata del protocolo de transferencia segura de información.

En cuanto al examen, prácticamente puede entrar todo el temario salvo la teoría. No hace falta que te preocupes por la teoría porque el examen ya es lo suficientemente largo y no le cabe más espacio en el test para preguntar por la teoría del protocolo: ventana de congestión, Stop&Wait, etc.

Para hacer este tema importan fundamentalmente dos aspectos:
1. Que reconozcas con facilidad la información de cabecera TCP desde la captura de Wireshark.
2. Que reconozcas aún mejor toda la información de la cabecera IP, puesto que ahí siempre es donde te va a querer esconder algo.

## Automatic Repeat Request (ARQ)
Pretende detectar y solventar un problema de pérdida de paquetes.

Consiste en enviar el mensaje, y esperar a que se agote antes un *retransmission timeout* (RTO) o llegue antes un *acknowledge* (ACK).
1. Si llega primero el ACK se envía el siguiente mensaje.
2. Si se agota primero el RTO se presupone perdido el mensaje inicial y se reenvía.

### Stop & Wait

Pretende evitar problemas si el mensaje que se pierde es un ACK puesto que, en tal caso, el emisor enviaría duplicados.

Para ello, incluye **paridad** en el mensaje ACK.
1. Si se envía el mensaje de paridad 0, se espera el ACK con petición de mensaje de paridad 1.
2. Si se envía el mensaje de paridad 0, se espera el ACK con petición de mensaje de paridad 0.

!["Stop & Wait"](https://media.geeksforgeeks.org/wp-content/uploads/Stop-and-Wait-ARQ-7.png "Stop & Wait")

### Ventana deslizante

Pretende mejorar Stop & Wait para que se puedan enviar mensajes mientras se espera al ACK del anterior logrando perder menos tiempo.

De momento, se indica cómo se envían mensajes en ventana deslizante, posteriormente cómo solventar errores.

Se ajusta una ventana de $n$ mensajes en el emisor. El emisor envía $n$ mensajes sin esperar y *desliza* la ventana hacia nuevos mensajes tras recibir su ACK.
> Ejemplo:
> 
> Con una ventana de tamaño `n` identificada por un *buffer*, se comienza por el conjunto de índices desde `[0..n]`. Tras recibir el `ACK 1`, que pide el mensaje 1 porque el mensaje 0 ha llegado bien, la ventana se reconfigura a los índices `[1..n+1]`

![Ventana deslizante](https://upload.wikimedia.org/wikipedia/commons/thumb/9/9d/Ventana_deslizante_2.JPG/1280px-Ventana_deslizante_2.JPG "Ventana deslizante")

#### Ventana deslizante: Go-Back-N ARQ

Si faltase o llegase en desorden un mensaje, el receptor se limita a no aceptar ningún mensaje en desorden y esperar a que venza el RTO del emisor para que reenvíe toda la ventana.

Go-Back no se utiliza porque hacer al emisor reenviar toda la ventana provoca una congestión evitable en la red.

> Ejemplo:
> 
> Supóngase una ventana de `[21..26]`.
>
> Ahora supóngase que llegan el mensaje `21`, luego se envía el `ACK 22`: entonces el emisor desliza la ventana hasta `[22..27]`.
>
> No obstante, el mensaje `22` se pierde por el camino: no lo recibe.
>
> El receptor recibe los mensajes `23`, `24`, `25`, `26` y `27` pero no los acepta pues, a su vista, llegan en desorden: todos llegan antes del `22`.
>
> El receptor desecha los mensajes y espera a que el emisor reenvíe la ventana.
>
> El emisor reenvía el primer mensaje dentro de la ventana, el `22`.
>
> Ahora no sucede el error y el receptor vuelve a aceptar el mensaje `22`, envía el consiguiente `ACK 23`, el emisor desliza la ventana y el proceso sigue con normalidad.

#### Ventana deslizante: Selective repeat ARQ

Requiere una ventana de recepción. Pretende solventar el problema de la carga de red de Go-Back.

El receptor utiliza una ventana de recepción donde almacena los mensajes en desorden en forma de *buffer*, enviando los ACKs adecuados y, por consiguiente, permitiendo al emisor discriminar para reenviar únicamente mensajes individuales cuyo RTO haya agotado.

![Selective repeat ARQ](https://media.geeksforgeeks.org/wp-content/uploads/20250924172002124275/Selective-Repeat-Sliding-Window-Protocol.jpg "Selective Repeat ARQ")

## Transmission Control Protocol (TCP)

Existe una medida llamada *Maximum Segment Size* (MSS) cuyo valor por defecto es de 536 bytes. Puede ser incrementado puesto que el MTU de IP es 1500 bytes. Indica el tamaño máximo de un mensaje TCP, excluyendo cabecera de transporte.

```
    0                   1                   2                   3
    0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
   +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
   |          Source Port          |       Destination Port        |
   +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
   |                        Sequence Number                        |
   +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
   |                    Acknowledgment Number                      |
   +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
   |  Data |           |U|A|P|R|S|F|                               |
   | Offset| Reserved  |R|C|S|S|Y|I|            Window             |
   |       |           |G|K|H|T|N|N|                               |
   +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
   |           Checksum            |         Urgent Pointer        |
   +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
   |                    Options                    |    Padding    |
   +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
   |                                                               |
   /                             data                              /
   /                                                               /
   +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
```

- Puerto origen.
  \
  Normalmente elegido y alto por el sistema operativo en clientes, elegido de los *Well Known Ports* en servidores.
  
- Puerto destino
  \
  Si se encuentra entre los *Well Known Ports* por un cliente se espera un servicio en específico.

- Número de secuencia
  \
  Sirve a modo de identificador de segmento enviado.

  Se dispone inicialmente mediante un número aleatorio con nombre de *Initial Sequence Number* (ISN). Posteriormente, se incrementa mediante la suma de los bytes enviados.
  \
  A modo de excepción, un segmento aumenta en 1 el número de secuencia si tiene activo el *flag* `SYN` o si tiene activo el *flag* `FIN`.

  > En concreto, la fórmula es $\Delta \text{NumSec} = payload + \text{SYN} + \text{FIN}$

- Número de reconocimiento
  \
  Sirve a modo de identificador de segmento recibido con funcionamiento similar al número de reconocimiento. Se intercambia con el de reconocimiento en el intercambio emisor con receptor.

- Longitud de cabecera
  \
  Descrito en el [RFC 793](https://www.rfc-es.org/rfc/rfc0793-es.txt) como "*Data Offset*" o "Posición de cabecera", indica la cantidad de líneas de bytes que ocupa la cabecera.

- *Flags*
  \
  Incluye bits reservados y una serie de *flags* que aportan información esencial

  *flag* | uso
  :--: | :--
  URG | Se superpone incluso si llega en desorden.
  ACK | Pide el siguiente segmento.
  PSH | Indica que los segmentos ya componen una información procesable completa.
  RST | Cierra bruscamente la conexión, normalmente por motivo de error.
  SYN | Indica petición de apertura de conexión.
  FIN | Indica petición de cierre de conexión.
  
- *win*
  \
  Indica el tamaño de la ventana.
  
- Checksum
  \
  Utiliza una pseudocabecera para su cálculo.

  ```
                     +--------+--------+--------+--------+
                     |           Source Address          |
                     +--------+--------+--------+--------+
                     |         Destination Address       |
                     +--------+--------+--------+--------+
                     |  zero  |  PTCL  |    TCP Length   |
                     +--------+--------+--------+--------+
  ```

  En conjunto, se hace: $Checksum = pseudocabecera + cabecera + datos$.

  > Recordatorio de que se hacen en palabras de 16 bits, si faltase un byte se rellena con un *padding* de `0x 00`.

- Puntero urgente
  \
  Apunta a un byte del segmento que debe ser leído con urgencia.

- Opciones
  \
  Hay muchas opciones pero interesa leer la combinación `0x 02 04 XX XX` donde `XX XX` indica el valor del MSS.

Adicionalmente, si se trata de una comunicación bidireccional se puede hacer *piggybacking*, es decir, unir en un sólo segmento un reconocimiento (ACK) con datos de la comunicación.

## Temporizador RTO

Se utiliza una aproximación a partir del RTT. En específico, el algoritmo de van Jacobson.

## Sincronización TCP

Consta de 3 fases.

1. SYN
2. SYN + ACK
3. ACK

El objetivo es realizarlo lo antes posible.

![TCP SYN](https://www.ionos.es/digitalguide/fileadmin/DigitalGuide/Schaubilder/EN-tcp.png "TCP SYN")

## Finalización TCP

El caso de estudio consta de 4 fases.

1. FIN
2. ACK
3. FIN
4. ACK

El objetivo es garantizar que se ha cerrado la conexión.

![TCP FIN](https://www.ionos.es/digitalguide/fileadmin/DigitalGuide/Schaubilder/EN-tcp.png "TCP FIN")

## Ventana de congestión

La ventana de congestión (cwnd) es un valor limitante en la red de la ventana de transmisión. La ventana de transmisión es, a su vez, el tamaño de la ventana real con la que se está transmitiendo.

$$\text{VentanaTrans} = min(win, cwnd)$$

Se suceden algoritmos de ajuste de ventana: *Slow Start* (arranque lento), *Congestion Avoidance* (incremento aditivo) y *Multiplicative Decrease* (reducción multiplicativa).

### *Slow Start*

Consiste en una sencilla fórmula exponencial de la forma:

$$\text{cwnd} = (2 \cdot MSS)^{n_{\text{ACK}}}$$

Escrito en pseudocodigo:

```lua
cwnd = 2*MSS
while (ACK != false) then
  cwnd = cwnd * 2*MSS
end
```

### *Congestion Avoidance*

Utiliza un límite adicional: el umbral (ssthresh). Inicialmente puede ser igual a *win*.

Una vez superado el umbral, se abandona *Slow Start* y el crecimiento de la ventana de congestión es lineal. Continúa hasta dado alguno de los siguientes casos:
- cwin alcanza el valor de win.
- Vence un temporizador (implica *Multiplicative Decrease*).
- Se reciben 3 ACKs duplicados (implica *Multiplicative Decrease*).

### *Multiplicative Decrease*

Si se vence un temporizador o se reciben 3 ACKs duplicados se sobreentiende que hay congestión.

```lua
ssthresh = max(VentanaTransmision/2, 2)
if (temporizador_perdido) then
  cwin = 1
elseif (ack_duplicados >= 3) then
  cwin = ssthresh
end
```

# Observaciones del autor

Un tema larguísimo, sin duda alguna, pero prácticamente todo es irrelevante porque no se pregunta en el examen. Vamos a hacer un repaso. Aunque adelanto que la conclusión es que lo único útil es lo que te permita identificar información desde tramas de Wireshark porque el examen es interpretar más de 4000 bits en 20 minutos y seguir haciendo lo anterior en el tiempo restante porque, en cualquier mente sana, 20 minutos son insuficientes.

Respecto a ARQ, puedes olvidar *Stop & Wait* y *Go-Back* puesto que no van a salir para nada. *Selective Repeat* podría preguntarse porque se utiliza con frecuencia pero, con total seguridad, tampoco va a aparecer.

Si hay algo que importa en este tema es la cabecera TCP y nada más. De verdad, absolutamente nada más. Aprendérselo de memoria porque en el test no hay chuleta y saber qué es cada cosa. Por lo demás ni te preocupes porque no va a preguntar. Es más, si preguntase más cosas sobre IP/UDP/TCP en el examen que no fuera eso se quedaría sin examen para preguntar el resto de temas.

El algoritmo de van Jacobson no se lo sabe ni el profesor, no creo ni que se acuerde de que exista cuando hace el examen.

Vale la pena aprenderse la situación de SYN y FIN porque van a aparecer en el ejercicio del infierno de las tramas. Tampoco te lo va a preguntar porque va a suponer que es conocimiento mínimo, pero vas a tener que distinguir cuando comienza o acaba una conversación.

La ventana de congestión la puedes ignorar. Sencillamente, no puede preguntarlo sin sacrificar preguntar por otros 2 temas de la asignatura. Tampoco es que sea algo especialmente importante porque pretende solucionar problemas del año de la pera: cuando 250 kB de memoria persistente valía casi tanto como 8 GB de DDR5 en la actualidad. Hace unos años serían 32 GB, pero los centros de datos me van a obligar a editar el símil. Además, las empresas utilzan otros algoritmos de congestión que logran mayores velocidades percibidas.

Lo de que no va a aparecer ni el algoritmo de van Jacobson o como se llame ni la ventana de congestión es tan seguro que hasta, y doy aviso, se ha omitido información en el documento o, al menos, no incluido imágenes.

Importantísimo saberse lo del `02 04 XX XX` de las opciones para saber MSS. Da igual que el profesor lo haya dado corriendo y mal. Da igual que no esté en el anexo. Da igual cualquiera de las excusas válidas por las que no deberías aprenderte eso. Cae y ya está. Autodidactismo como siempre en la universidad porque aquí es más fácil hacer exámenes y culpar al alumnado que aprender a enseñar y tener honestidad.

Adicionalmente, se supone que hay 12 temas pero el 9 son sockets cuyo interés es nulo hasta para el profesor y el PDF del tema 9 (Sockets) incluye el tema 10 (Clientes y servidores).
