---
title: GR 2: Redes de Computadores
author: Christian Velasco Pérez
---
# GR 2: Redes de Computadores
*Autor:* Christian Velasco Pérez <img src="https://iili.io/fpTTGnt.md.jpg" alt="Skopez" align="right" style="width:15%; margin-left:4%;margin-bottom:2%">
\
El siguiente contenido corresponde a un **apoyo** educativo para cualquier interesado y por eso puede contener fallos. El documento está orientado al curso de *Redes de computadores* del Grado en Ingeniería Informática de la Universidad de La Rioja y se considera completa responsabilidad del lector lo que haga con la información de este documento.
\
La distribución del documento queda reservada al permiso explícito de su autor. Si necesitase información de contacto puede [enviar un correo](mailto:velskopezz@gmail.com).

---

# Dirección MAC
La **dirección MAC** guarda información relevante en su primer octeto.
- El dígito final del octeto:
    - `0` $\equiv \text{unicast}$
    - `1` $\equiv \text{multicast}$
- El segundo dígito desde la derecha:
    - `0` $\equiv \text{MAC única universal}$
    - `1` $\equiv \text{MAC restringida}$

> Eg: para `0x0A` tendríamos un final de `0b10` que significaría única universal de unicast.

# Información e `ipconfig`
Al hacer `ipconfig` en CMD obtenemos algo del estilo:
```
Adaptador de Ethernet Ethernet 14:
Sufijo DNS específico para la conexión. . : unirioja.loc
Vínculo: dirección IPv6 local. . . : fe80::9077:3f80:1b3a:2bec%20
Dirección IPv4. . . . . . . . . . . . . . : 10.11.63.🃟
Máscara de subred . . . . . . . . . . . . : 255.255.0.0
Puerta de enlace predeterminada . . . . . : 10.11.0.1  
```

Estamos en la red `10.0.0.0` que corresponde a la clase A: privadas por organización.
\
La máscara de subred es `255.255.0.0` por lo que se pueden ponder $2^{16}-2$ dispositivos.
\
Lo que le siga es responsabilidad de la organización por lo que no tiene ningún sentido sintáctico real. Es fundamentalmente semántico.

Si realizamos `ipconfig /all` obtenemos más información. Entre ella encontramos la **IP dinámica**. En realidad, esta corresponde a dispositivos móviles dado que en dispositivos estáticos se vuelve a asignar la misma IP.

## Puerta de enlace
> Ct: Cuando se usa GNS3 es un **error común** olvidarse de imponer la **puerta de enlace**. Esto se dee hacer **siempre que haya un router** de por medio.

Lo normal es poner la **puerta de enlace más baja posible**. Esta es la `255.255.255.0` porque es necesario reservar las redes de octeto final `0` y `255` para la **puerta de enlace** y la dirección de **broadcast**. Por ello, la última dirección asignable es la del octeto `254`.

## Servidor DNS
Corresponde principalmente al temario de la **capa de aplicación**. En los ordenadores de la facultad aparecen dos servidores DNS. Cuando se busca el dominio se suele buscar en el **servidor DNS** y se suele almacenar en caché durante un tiempo.

## Opciones
Si ejecutamos `ipconfig /` permite obtener la información sobre el comando:
```
> ipconfig                       ... Muestra información.
> ipconfig /all                  ... Muestra información detallada.
> ipconfig /renew                ... Renueva todos los adaptadores.
> ipconfig /renew EL*            ... Renueva cualquier conexión cuyo nombre comience con EL.
> ipconfig /release *Con*        ... Libera todas las conexiones coincidentes, por ejemplo:
                                       "Conexión cableada Ethernet 1" o
                                       "Conexión cableada Ethernet 2".
> ipconfig /allcompartments      ... Muestra información sobre todos los compartimientos.
> ipconfig /allcompartments /all ... Muestra información detallada todos los compartimientos
```

> Nota: Dada la configuración de los ordenadores de la facultad no funcionan algunas de estas opciones.

# Paquetes
El **ping** es una herramienta que permite verificar la *conectividad* a nivel IP. Facilita el control de fallos. Para su funcionamiento, utiliza un protocolo llamado ICMP.
> Nota: En el documento de prácticas puede

Al ejecutar `ping` en CMD se realizan, por defecto, 4 peticiones. Se nos indica el **RRT** y el **TTL** (Time to live, tiempo de vida en español). Este último es un campo del último octeto cuya utilidad es **matar paquetes perdidos** para que no colapsen la red por seguir en un tráfico erróneo.
> Eg: los paquetes que envía el CMD de Windows con `ping` tienen un valor por defecto de `TTL=128`, aunque tradicionalmente fueron 32, normalmente es de 64. Esto significa que, en CMD, el paquete puede dar un máximo de 128 saltos para regresar de su destino.

> Nota: `ping` permite utilizarse con DNS de tal forma que muestra el nombre canónico del servicio así como su respectiva IP.
> > Eg: si hacemos `ping www.as.com`, a fecha de 25/02/2026, obtenemos:
> > ```
> > Haciendo ping a prisa-us-eu.map.fastly.net [199.232.34.133] con 32 bytes de datos:
> > Respuesta desde 199.232.34.133: bytes=32 tiempo=7ms TTL=57
> > Respuesta desde 199.232.34.133: bytes=32 tiempo=7ms TTL=57
> > Respuesta desde 199.232.34.133: bytes=32 tiempo=7ms TTL=57
> > Respuesta desde 199.232.34.133: bytes=32 tiempo=8ms TTL=57
> > ```
> > Lo que quiere decir es que el servidor tiene un TTL configurado de 57.

Para configurar la **cantidad de peticiones** que hace `ping` se utiliza, en CMD, `ping /t`.

> Eg: al ejecutar `ping [ip] -t 256` haremos 256 peticiones a una red en específico.

> Eg: Si disponemos de una ip con muy mala conexión podríamos tardar mucho tiempo e incluso perder paquetes.

## Tamaño de paquete
Tenemos las opciones `-l` para configurar la longitud del paquete y `-f` para forzar el envío.
> Eg: al ejecutar `ping [ip] -l 1500` habremos elegido una longitud de paquete de 1500. Esto no está permitido en la red de la facultad así que automáticamente habrá sido fragmentado por una flag específica. En cambio, si se ejecuta `ping [ip] -l 1500 -f` notaremos que nos hemos pasado con el tamaño de la cabeceera y, al intentar fragmentarlo, se detiene por un flag en específico:
> ```
> Haciendo ping a 10.11.63.🃟 con 1500 bytes de datos:
> Es necesario fragmentar el paquete pero se especificó DF.
> Es necesario fragmentar el paquete pero se especificó DF.
> Es necesario fragmentar el paquete pero se especificó DF.
> Es necesario fragmentar el paquete pero se especificó DF.
> ```

## Tiempo
Si ejecutamos `ping` en distintas páginas webs notamos que dan tiempos parecidos. Esto se debe a que suele haber **servidores replicados en distinos lugares** que encima corresponden a servicios de *hosting* estpecializados, es decir, que los servidores están en ubicaciones centralizadas aunque el propietario de sus servicios esté a kilómetros de distancia.

> Eg: Hacer `ping` a la página de la [Casa Blanca](www.whitehouse.gov) da el mismo tiempo que el [Ayuntamiento de Madrid](www.madrid.es) porque los servidores están en el mismo sito. En cambio, si se hace a [algún servicio argentino](www.mdp.edu.ar) notaremos un aumento de alrededor de 250ms en el tiempo demostrando que ha saltado por el océano.

Si ejecutamos `ping [ip] -i [TTL]` podremos especificar el TTL del envío del paquete. Si vamos reduciéndolo notaremos en cierto punto que **el paquete no llegará a su destino**.
> Eg:
> ```
> Haciendo ping a proxy.mdp.edu.ar [170.80.24.6] con 32 bytes de datos:
> Respuesta desde 154.54.169.178: TTL expirado en tránsito.
> Respuesta desde 154.54.169.178: TTL expirado en tránsito.
> Respuesta desde 154.54.169.178: TTL expirado en tránsito.
> Respuesta desde 154.54.169.178: TTL expirado en tránsito. 
> ```
> Además, notaremos que la dirección de envío `170.80.24.6` es **distinta** a la dirección de respuesta `154.54.169.178` que nos informa de que el paquete ha agotado el TTL en tránsito.
>
> Si ejecutamos dentro de la facultad un `TTL=4` de salida notaremos que ni siquiera llegamos a salir de la red de la universidad recibiendo una respuesta de una dirección `10.251.0.2`, que corresponde a una red de clase A.
> \
> Si imponemos un `TTL=1` caeremos dentro de la **puerta de enlace** de nuestro router.

Con el comando `tracert [ip]` en CMD podemos obtener la **traza** o los saltos que realiza el paquete en su viaje hasta el destino por la red.
> Eg:
> ```
> Traza a la dirección proxy.mdp.edu.ar [170.80.24.6]
> sobre un máximo de 30 saltos:
> 1    <1 ms    <1 ms    <1 ms  toy_alum.unirioja.es [10.11.0.1]
> 2    <1 ms    <1 ms    <1 ms  10.250.3.1
> 3    <1 ms    <1 ms    <1 ms  10.250.1.2
> 4    <1 ms    <1 ms    <1 ms  10.251.0.2
> 5     3 ms     3 ms     3 ms  unirioja-ppal.ethtrunk0-55.unizar.rt2.ara.red.rediris.es [130.206.195.49]
> 6     8 ms     8 ms     8 ms  unizar-rt2.ethtrunk4.ehu.rt2.pav.red.rediris.es [130.206.245.21]
> 7    16 ms    17 ms    17 ms  ehu-rt2.ethtrunk2.telmad.rt1.mad.red.rediris.es [130.206.245.17]
> 8    18 ms    23 ms    18 ms  hu0-2-0-15.rcr81.b015537-1.mad05.atlas.cogentco.com [149.14.241.17]
> 9    13 ms    12 ms    13 ms  be5120.ccr31.mad05.atlas.cogentco.com [154.54.36.81]
> 10    17 ms    17 ms    17 ms  be2324.ccr31.bio02.atlas.cogentco.com [154.54.61.129]
> 11    92 ms    92 ms    92 ms  port-channel2252.ccr91.dca04.atlas.cogentco.com [154.54.47.137]
> 12   109 ms   109 ms   109 ms  be3482.ccr41.atl01.atlas.cogentco.com [154.54.169.178]
> 13   135 ms   123 ms     *     be5576.ccr81.mia03.atlas.cogentco.com [154.54.47.50]
> 14   252 ms   249 ms   249 ms  38.88.56.133
> 15     *        *        *     Tiempo de espera agotado para esta solicitud.
> 16     *        *        *     Tiempo de espera agotado para esta solicitud.
> 17   255 ms   255 ms   255 ms  tunnel.mdp.edu.ar [200.0.182.7]
> 18   258 ms   257 ms   257 ms  170.80.24.6

---
title: GR 2: Redes de Computadores
author: Christian Velasco Pérez
---
# GR 2: Redes de Computadores
*Autor:* Christian Velasco Pérez <img src="https://iili.io/fpTTGnt.md.jpg" alt="Skopez" align="right" style="width:15%; margin-left:4%;margin-bottom:2%">
\
El siguiente contenido...
\
La distribución del documento queda reservada al permiso explícito de su autor. Si necesitase información de contacto puede [enviar un correo](mailto:velskopezz@gmail.com).

---

# Dirección MAC
La **dirección MAC** guarda información relevante en su primer octeto.
- El dígito final del octeto:
    - `0` $\equiv$ unicast
    - `1` $\equiv$ multicast
- El segundo dígito desde la derecha:
    - `0` $\equiv$ MAC única universal
    - `1` $\equiv$ MAC restringida

> Eg: para `0x0A` tendríamos un final de `0b10` que significaría única universal de unicast.

# Información e `ipconfig`
Al hacer `ipconfig` en CMD obtenemos algo del estilo:
```
Adaptador de Ethernet Ethernet 14:
Sufijo DNS específico para la conexión. . : unirioja.loc
Vínculo: dirección IPv6 local. . . : fe80::9077:3f80:1b3a:2bec%20
Dirección IPv4. . . . . . . . . . . . . . : 10.11.63.🃟
Máscara de subred . . . . . . . . . . . . : 255.255.0.0
Puerta de enlace predeterminada . . . . . : 10.11.0.1  
```

Estamos en la red `10.0.0.0` que corresponde a la clase A: privadas por organización.
\
La máscara de subred es `255.255.0.0` por lo que se pueden ponder $2^{16}-2$ dispositivos.
\
Lo que le siga es responsabilidad de la organización por lo que no tiene ningún sentido sintáctico real. Es fundamentalmente semántico.

Si realizamos `ipconfig /all` obtenemos más información. Entre ella encontramos la **IP dinámica**. En realidad, esta corresponde a dispositivos móviles dado que en dispositivos estáticos se vuelve a asignar la misma IP.

## Puerta de enlace
> Ct: Cuando se usa GNS3 es un **error común** olvidarse de imponer la **puerta de enlace**. Esto se dee hacer **siempre que haya un router** de por medio.

Lo normal es poner la **puerta de enlace más baja posible**. Esta es la `255.255.255.0` porque es necesario reservar las redes de octeto final `0` y `255` para la **puerta de enlace** y la dirección de **broadcast**. Por ello, la última dirección asignable es la del octeto `254`.

## Servidor DNS
Corresponde principalmente al temario de la **capa de aplicación**. En los ordenadores de la facultad aparecen dos servidores DNS. Cuando se busca el dominio se suele buscar en el **servidor DNS** y se suele almacenar en caché durante un tiempo.

## Opciones
Si ejecutamos `ipconfig /` permite obtener la información sobre el comando:
```
> ipconfig                       ... Muestra información.
> ipconfig /all                  ... Muestra información detallada.
> ipconfig /renew                ... Renueva todos los adaptadores.
> ipconfig /renew EL*            ... Renueva cualquier conexión cuyo nombre comience con EL.
> ipconfig /release *Con*        ... Libera todas las conexiones coincidentes, por ejemplo:
                                       "Conexión cableada Ethernet 1" o
                                       "Conexión cableada Ethernet 2".
> ipconfig /allcompartments      ... Muestra información sobre todos los compartimientos.
> ipconfig /allcompartments /all ... Muestra información detallada todos los compartimientos
```

> Nota: Dada la configuración de los ordenadores de la facultad no funcionan algunas de estas opciones.

# Paquetes
El **ping** es una herramienta que permite verificar la *conectividad* a nivel IP. Facilita el control de fallos. Para su funcionamiento, utiliza un protocolo llamado ICMP.
> Nota: En el documento de prácticas puede

Al ejecutar `ping` en CMD se realizan, por defecto, 4 peticiones. Se nos indica el **RRT** y el **TTL** (Time to live, tiempo de vida en español). Este último es un campo del último octeto cuya utilidad es **matar paquetes perdidos** para que no colapsen la red por seguir en un tráfico erróneo.
> Eg: los paquetes que envía el CMD de Windows con `ping` tienen un valor por defecto de `TTL=128`, aunque tradicionalmente fueron 32, normalmente es de 64. Esto significa que, en CMD, el paquete puede dar un máximo de 128 saltos para regresar de su destino.

> Nota: `ping` permite utilizarse con DNS de tal forma que muestra el nombre canónico del servicio así como su respectiva IP.
> > Eg: si hacemos `ping www.as.com`, a fecha de 25/02/2026, obtenemos:
> > ```
> > Haciendo ping a prisa-us-eu.map.fastly.net [199.232.34.133] con 32 bytes de datos:
> > Respuesta desde 199.232.34.133: bytes=32 tiempo=7ms TTL=57
> > Respuesta desde 199.232.34.133: bytes=32 tiempo=7ms TTL=57
> > Respuesta desde 199.232.34.133: bytes=32 tiempo=7ms TTL=57
> > Respuesta desde 199.232.34.133: bytes=32 tiempo=8ms TTL=57
> > ```
> > Lo que quiere decir es que el servidor tiene un TTL configurado de 57.

Para configurar la **cantidad de peticiones** que hace `ping` se utiliza, en CMD, `ping -n`.

> Eg: al ejecutar `ping [ip] -n 256` haremos 256 peticiones a una red en específico.

> Eg: Si disponemos de una ip con muy mala conexión podríamos tardar mucho tiempo e incluso perder paquetes.

## Tamaño de paquete
Tenemos las opciones `-l` para configurar la longitud del paquete y `-f` para forzar el envío.
> Eg: al ejecutar `ping [ip] -l 1500` habremos elegido una longitud de paquete de 1500. Esto no está permitido en la red de la facultad así que automáticamente habrá sido fragmentado por una flag específica. En cambio, si se ejecuta `ping [ip] -l 1500 -f` notaremos que nos hemos pasado con el tamaño de la cabeceera y, al intentar fragmentarlo, se detiene por un flag en específico:
> ```
> Haciendo ping a 10.11.63.🃟 con 1500 bytes de datos:
> Es necesario fragmentar el paquete pero se especificó DF.
> Es necesario fragmentar el paquete pero se especificó DF.
> Es necesario fragmentar el paquete pero se especificó DF.
> Es necesario fragmentar el paquete pero se especificó DF.
> ```

## Tiempo
Si ejecutamos `ping` en distintas páginas webs notamos que dan tiempos parecidos. Esto se debe a que suele haber **servidores replicados en distinos lugares** que encima corresponden a servicios de *hosting* estpecializados, es decir, que los servidores están en ubicaciones centralizadas aunque el propietario de sus servicios esté a kilómetros de distancia.

> Eg: Hacer `ping` a la página de la [Casa Blanca](www.whitehouse.gov) da el mismo tiempo que el [Ayuntamiento de Madrid](www.madrid.es) porque los servidores están en el mismo sito. En cambio, si se hace a [algún servicio argentino](www.mdp.edu.ar) notaremos un aumento de alrededor de 250ms en el tiempo demostrando que ha saltado por el océano.

Si ejecutamos `ping [ip] -i [TTL]` podremos especificar el TTL del envío del paquete. Si vamos reduciéndolo notaremos en cierto punto que **el paquete no llegará a su destino**.
> Eg:
> ```
> Haciendo ping a proxy.mdp.edu.ar [170.80.24.6] con 32 bytes de datos:
> Respuesta desde 154.54.169.178: TTL expirado en tránsito.
> Respuesta desde 154.54.169.178: TTL expirado en tránsito.
> Respuesta desde 154.54.169.178: TTL expirado en tránsito.
> Respuesta desde 154.54.169.178: TTL expirado en tránsito. 
> ```
> Además, notaremos que la dirección de envío `170.80.24.6` es **distinta** a la dirección de respuesta `154.54.169.178` que nos informa de que el paquete ha agotado el TTL en tránsito.
>
> Si ejecutamos dentro de la facultad un `TTL=4` de salida notaremos que ni siquiera llegamos a salir de la red de la universidad recibiendo una respuesta de una dirección `10.251.0.2`, que corresponde a una red de clase A.
> \
> Si imponemos un `TTL=1` caeremos dentro de la **puerta de enlace** de nuestro router.

Con el comando `tracert [ip]` en CMD podemos obtener la **traza** o los saltos que realiza el paquete en su viaje hasta el destino por la red.
> Eg:
> ```
> Traza a la dirección proxy.mdp.edu.ar [170.80.24.6]
> sobre un máximo de 30 saltos:
> 1    <1 ms    <1 ms    <1 ms  toy_alum.unirioja.es [10.11.0.1]
> 2    <1 ms    <1 ms    <1 ms  10.250.3.1
> 3    <1 ms    <1 ms    <1 ms  10.250.1.2
> 4    <1 ms    <1 ms    <1 ms  10.251.0.2
> 5     3 ms     3 ms     3 ms  unirioja-ppal.ethtrunk0-55.unizar.rt2.ara.red.rediris.es [130.206.195.49]
> 6     8 ms     8 ms     8 ms  unizar-rt2.ethtrunk4.ehu.rt2.pav.red.rediris.es [130.206.245.21]
> 7    16 ms    17 ms    17 ms  ehu-rt2.ethtrunk2.telmad.rt1.mad.red.rediris.es [130.206.245.17]
> 8    18 ms    23 ms    18 ms  hu0-2-0-15.rcr81.b015537-1.mad05.atlas.cogentco.com [149.14.241.17]
> 9    13 ms    12 ms    13 ms  be5120.ccr31.mad05.atlas.cogentco.com [154.54.36.81]
> 10    17 ms    17 ms    17 ms  be2324.ccr31.bio02.atlas.cogentco.com [154.54.61.129]
> 11    92 ms    92 ms    92 ms  port-channel2252.ccr91.dca04.atlas.cogentco.com [154.54.47.137]
> 12   109 ms   109 ms   109 ms  be3482.ccr41.atl01.atlas.cogentco.com [154.54.169.178]
> 13   135 ms   123 ms     *     be5576.ccr81.mia03.atlas.cogentco.com [154.54.47.50]
> 14   252 ms   249 ms   249 ms  38.88.56.133
> 15     *        *        *     Tiempo de espera agotado para esta solicitud.
> 16     *        *        *     Tiempo de espera agotado para esta solicitud.
> 17   255 ms   255 ms   255 ms  tunnel.mdp.edu.ar [200.0.182.7]
> 18   258 ms   257 ms   257 ms  170.80.24.6
> 
> Traza completa.
> ```

# Resumen
Con todo esto, se puede resumir el carácter práctico de esta práctica en:
- **`ipconfig /all`**: para obtener toda la información del comando `ipconfig`.
- **`ping [ip]`**: para realizar peticiones a un host con la dirección IP proporcionada. Además, cuenta con las siguientes opciones:
    - **`-i [TTL]`**: para especificar el TTL (número máximo de saltos).
    - **`-l [length]`**: para especificar el tamaño del paquete.
        > Nota: Hay que tener en cuenta que el tamaño de la trama será mayor.
    - **`-n [number]`**: para especificar la cantidad de peticiones que se hacen.
- **`tracert [ip]`**: muestra la trama de los paquetes con destino a la IP proporcionada.