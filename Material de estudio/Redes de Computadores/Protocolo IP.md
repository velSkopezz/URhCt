# Redes de Computadores: Protocolo de Internet

Este tema es el grueso del examen. Importa todo salvo las clases de las redes.

## Cabecera de un datagrama

```
    0                   1                   2                   3
    0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
   +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
   |Version|  IHL  |Type of Service|          Total Length         |
   +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
   |         Identification        |Flags|      Fragment Offset    |
   +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
   |  Time to Live |    Protocol   |         Header Checksum       |
   +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
   |                       Source Address                          |
   +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
   |                    Destination Address                        |
   +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
   |                    Options                    |    Padding    |
   +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
```

- Versión
  \
  Indica la versión de IP. En la asignatura siempre será `4` puesto que se trata con IPv4.

- Longitud de cabecera de Internet
  \
  Indica la cantidad de líneas (4 bytes) que ocupa la cabecera. Lo común será el caso en el que no haya opciones. Entonces serán `5` líneas ($5 \ línea \cdot 4 \frac{byte}{línea} = 20 {byte}$).

- Tipo de servicio
  \
  Son bits a modo de `flag` que aportan indicaciones especiales sobre como debe tratarse el datagrama.

- Longitud total
  \
  Adivina. Viene dado por un campo de 16 bits, por consiguiente, tiene un valor máximo de $2^{16} = 65535$ bytes. Nótese que se mide en bytes.

  Adicionalmente, existe un parámetro de los canales llamado *Maximum Transmission Unit* (MTU) que indica el valor máximo que debe tener un datagrama por dicho canal. Este parámetro tiene un valor por defecto de 1500 B y rara vez resulta alterado.

- Identificación
  \
  Un campo identificador del datagrama.

- *Flags*
  \
  Son bits dedicados a proporcionar información sobre fragmentación:
  - Bit 0 (reservado): Debe estar a 0.
  - Bit 1 (DF: *Do not Fragment*): Indica que el datagrama no se puede fragmentar.
  - Bit 2 (MF: *More Fragments*): Indica que hay más fragmentos del datagrama con misma identificación.
 
- *Offset*
  \
  Es un campo de tantos bits como lo que ocupan los *flags* y lo que sobre hasta completar la línea. Indica qué posición ocupa entre los fragmentos del datagrama, en unidades de 8 bytes en específico. Si fuese el primero de ellos su *offset* sería 0.

- TTL
  \
  Indica la cantidad de saltos restantes en la red antes de dar por perdido el datagrama. Si llega a 0 se descarta el datagrama por lo que, cuando queda 1 salto, se evita directamente el envío.

  No se debe olvidar este campo puesto que es responsable de que un datagrama siempre cambie con cada salto.

- Protocolo
  \
  Indica a qué protocolo se ajustan los datos encapsulados en el datagrama según su identificación proporcionada por IANA.

  > Ejemplo:
  >
  > - ` 1`: ICMP
  > - `17`: UDP
  > - ` 6`: TCP

- Checksum de cabecera
  \
  Se trata de la suma de todos los datos de la cabecera del datagrama en palabras de 2 bytes contiguos desde el primer byte. Para la suma se presupone que este mismo campo vale 0. Además, por el TTL, este campo siempre cambia con cada salto.

  El campo suele escribirse en hexadecimal. Si hubiese un quinto dígito en hexadecimal se suma dicho dígito como unidad al resto de dígitos repitiéndose hasta ocupar correctamente la cantidad de bits adecuada.

  > Ejemplo del acarreo:
  >
  > Si se obtuviese `0x2f6e4` y nótese que ocupa 5 dígitos hexadecimales, se toma el quinto dígito (`0x2`) y se le suma a los últimos 4 (`0xf6e4`) de tal forma que el *checksum* es el resultado de la suma `0xf6e4 + 0x2 = 0xf6e6`.

- Dirección de origen
  \
  Dirección lógica de Internet del emisor.

- Dirección de destino
  \
  Dirección lógica de Internet del receptor.

## Direcciones IP

Son un conjunto de 4 octetos normalmente descritos en decimal. Estos pueden describir redes o *hosts* pertenecientes a una red. La dirección de la red se incluye en la dirección del *host* y puede conocerse mediante la máscara de subred.

Pueden usarse direcciones CIDR en las que se indica una máscara de subred, es decir, los bits con los que al hacer una operación AND bit a bit con la dirección IP de un *host* se obtiene la dirección.

> Ejemplo:
>
> El *host* con dirección `192.168.1.45/26` indica tener una máscara de subred `255.255.255.192` (se obtiene poniendo `/26` bits a `1` desde la izquierda y rellenando con `0` por la derecha hasta completar 32 bits).
>
> Si se hace una operacion `192.168.1.45 && 255.255.255.192` se obtiene que la dirección de red es `192.168.1.0`. No obstante, no se debe caer en la confusión, pues la dirección más alta (*broadcast*) que permite la red, al contar los bits, es `192.168.1.63`.

O Se pueden usar redes con clase en su defecto:
- Clase A: `/8`, para las que empiecen con el bit a `0` desde la izquierda. Orientadas a grandes organizaciones.
- Clase B: `/16`, para las que empiecen con el bit a `1` desde la izquierda. Orientadas a medianas organizaciones.
- Clase C: `/24`, para las que empiecen con los bits a `01` desde la izquierda. De uso generalizado.

> Se puede seguir una secuencia similar respecto a los bits para las clases D y E.

Existen direcciones IP especiales:
- `127.0.0.0/8`: *Loopback*, para el propio ordenador.
- `0.0.0.0`: Direccion especial. Se usa en DHCP para indicar que no se tiene dirección IP. También se usa en tablas de enrutamiento para indicar direcciones IP no registradas en la tabla del nodo.
- Dirección más alta de la red: Dirección de difusión (*broadcast*) de la red.
- `255.255.255.255`: Dirección de difusión (*broadcast*) a la red IP conectada. Se usa en DHCP cuando no se conoce la dirección del servidor DHCP.
- Direcciones privadas.

### Rango de direcciones privadas

Si la dirección IP con la que se trate estuviera dentro de los siguientes rangos de direcciones entonces se estaría tratando con direcciones especiales reservadas por IANA. Estas direcciones especiales no pueden usarse como direcciones públicas puesto que se repiten entre distintas redes privadas. Esto existe con el fin de solventar la falta de direcciones IP.
- `10.0.0.0/8` - De clase A.
- `172.16.0.0/12` - De clase B. Nótese que la máscara no es múltiplo de 8.
- `192.168.0.0/16` - De clase C.

# Observaciones del autor

Bienvenido a la capa de Red, el Protocolo de Internet, IP o, también bien llamado, el campo de exterminio.
\
Primeramente, este tema es el examen. Realmente nada importa tanto en todo el examen como este tema. Es más, este tema es más de medio examen. Como bien se menciona al principio, las redes con clase no hace falta aprendérselo y es porque están en desuso. Eso sí, el direccionamiento CIDR te lo estudias por tu cuenta. He intentado explicarlo de la forma más sencilla posible sin empezar a poner ejemplo tras ejemplo de operaciones AND bit a bit pero no hay manera. Para complicártelo yo mejor complícate por tu cuenta y me quito de culpas.

La cabecera del datagrama es importantísima. Conocer a fondo casi cada parte. Empezando por lo fácil, si no entiendes los campos Versión y Longitud te recomiendo llamar al 112 y barajar la posibilidad de que te esté dando un ictus.

La longitud de cabecera está hecha un lío y sabiendo que no podían poner menos de 5 podrían haberse ahorrado unos bits. En cualquier caso, junto a la Versión y el Tipo de Servicio que siempre serán 4 y 0 respectivamente porque nunca va a entrar IPv6 ni nada posterior a 2003 y porque ni su creador quiere saberse los tipos de servicio respectivamente, encontrar la combinación `45 00` en la misma ubicación en las 20 tramas que te va a poner en el examen va a ser tu pase para intuir que ahí empieza IP. Reitero, digo "*intuir*" porque ese mismo `45 00` se usó en el ordinario de 2026 como ejercicio trampa para pillar resultando ser únicamente datos que debías saber por mirar el *offset*.

Los *flags* tienen la ventaja de que no se pueden combinar de cualquier forma. La desventaja es la distracción que llega cada vez que ves como alguien que no insultaba lo suficiente escribió y llamo "MF" a un bit en un RFC de los protocolos más utilizados de la historia.

El tema identificador y *offset* te lo ponen aparte pero en realidad es un truco de las altas esferas para que no te percates de que el identificador real del datagrama es la tupla identificador y *offset*. Habría sido una gozada que los *flags* estuvieran al final para poder leer el MF con la paridad del número, pero me temo que el ciclo de CPU del operador `<<` para calcualr el *offset* que supondría era lo suficientemente costoso en los 70' como para que 50 años después tengas que sufrirlo: en clase, por supuesto, en la vida real y laboral Wireshark o cualquer *software* te lo da masticadito. No te preocupes, tal vez en el cementerio encuentres a los creadores que te resuelvan tus dudas.

El resto de los parámetros ni merecen que hable de ellos.

Lo que definitivamente merece algo es la forma en la que funcionan las direcciones IP, y ese algo es, en específico, una medalla a la osadía en el ejército de Lucifer. Esta cosa le mete miedo al diablo.

Te tengo una noticia terrible, tienes que saber perfectamente cómo funciona esto de las direcciones porque es un ejercico recurrente y con recurrente me refiero a que debe llevar siendo el ejercicio 1 del examen desde, por lo menos, 2017. La otra opción es intentar aprobar con el ejercicio de las tramas. Escoge lo que quieras, no te va a dar tiempo a terminar el examen de ninguna manera.
\
Y tampoco puedo decir mucho. Que la IANA debería elegir mejores números porque esto de elegir números aleatorios para las direcciones privadas y de *loopback* o directamente poner TCP al 6 y UDP al 17 tiene tanto sentido como barrer playas con escoba para sacar la arenilla.
