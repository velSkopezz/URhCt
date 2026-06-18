# Redes de Computadores: Redes de área local (LAN)

No entra nada.

## Mecanismos MAC con colisión: CSMA/CD (acceso aleatorio)

El *Carrier Sense Multiple Access with Collision Detection* (CSMA/CD) es usado en conexiones Ethernet.

Consiste en 2 principios:
- Si el canal está ocupado se espera.
- Si el canal está libre se transmite de inmediato.

Además, mientras se transmite se comprueba constantemente que no se produzca una colisión.

Si se diese el caso de una colisión entonces se espera un tiempo aleatorio de acuerdo con el algoritmo *binary backoff*.

Se requieren tramas de, al menos, 64 bytes para poder asegurar que la detección de colisiones regrese mientras el emisor sigue transmitiendo.

## Mecanismos MAC con colision: CSMA/CA (acceso aleatorio)

El *Carrier Sense Multiple Access with Collision Avoidance* (CSMA/CA) es usado en conexiones Wi-Fi.

El emisor:
- Si el canal está libre por `DIFS` segundos. En tal caso envía la trama completa.
- Si el canal está ocupado se espera de acuerdo con el algoritmo *binary backoff*.

El receptor:
- Devuelve `ACK` tras `SIFS` segundos si la trama se recibe correctamente.

### Evitación de colisión RTS/CTS

1. Una estación solicita al AP transmitir por difusión una trama RTS (*Request To Send*).
2. El AP contesta por difusión con una trama CTS (*Clear To Send*).
3. Se envían los datos y se devuelve un `ACK`.

Este proceso se hace únicamente cuando la trama supera cierto umbral definido por la estación.

## Mecanismos MAC libres de colisión: Paso de testigo (acceso controlado)

Un nodo tiene el testigo. Si tiene algo que transmitir lo transmite, si no tiene nada que transmitir pasa el testigo al siguiente nodo y no vuelve a transmitir hasta volver a tener el testigo.

## Direcciones físicas

Son una secuencia de 6 bytes normalmente escritos en hexadecimal. La dirección `ff:ff:ff:ff:ff:ff` está reservada para difusión.

Esta dirección viene configurada por el *firmware* e identifica un adaptador.

Para asociar una dirección física (MAC) con una lógica (IP) se hace uso del *Address Resolution Protocol* (ARP).

## ARP

Se identifica con el código `0x 08 06` así como IP se identifica con `0x 08 00`. Forma parte de la capa de enlace aunque se encapsule en una trama.

El protoclo se dedica a averiguar la dirección MAC de una IP. Para ello, se hace una consulta por difusión que se responde con discriminación.

![ARP](https://media.geeksforgeeks.org/wp-content/uploads/20240117160730/long1-(1).png "ARP")

La tabla ARP contiene la asociación entre direcciones IP y direcciones MAC. Esta asociación se almacena por tiempo limitado en una base de datos (caché) y luego se elimina.

## *Hubs*, *switches* y *routers*

Los *hubs* se limitan a la capa física, es decir, ignora el formato de la trama y repiten el contenido por todos sus puertos.

Los *switches* abarcan el nivel de enlace y, por ello, pueden distinguir entre direcciones físicas (MAC) enviando la trama únicamente a su receptor.

Los *routers* pueden abarcar incluso el nivel de red, lo que permite que se haga NAT, la comunicación por direcciones IP, etc.

## Formato de trama

- Dirección física de origen (6 bytes)
- Dirección física de destino (6 bytes)
- Protocolo (2 bytes)
- Datos de trama (46 - 1500 bytes)
- CRC (4 bytes)

# Observaciones del autor

El formato de la trama para que no te pierdas como un tonto y poco más. Y que ARP es `0x 08 06` y que IP es `0x 08 00` además tal vez.

Es que no va a entrar nada de este tema, ¿qué quieres que te diga? Por entrar no va a entrar ni el CRC de la captura copypasta que te va a traer de Wireshark. Ni de las otras 19 capturas tampoco.

Es más, dijo explícitamente en clase que de las implementaciones físicas de Ethernet entender más o menos qué significa el nombre. O quizás lo dijo con los cables del tema 1.
\
Mira, no tengo ni idea, pero no preguntó ni uno ni otro. Simplemente pasa al tema siguiente y ya.

También faltan algunos mecanismos MAC, entre ellos Alohanet, pero no creo que los pregunte porque no vas a usar Alohanet en tu vida. No ha preguntado CSMA/CD en el examen y va a pregunta Alohanet, nanay.
