# Redes de Computadores: Otros aspectos relacionados con la red

De lo que aquí se comprende sólo importa ICMP y tablas de enrutamiento.

## Tabla de enrutamiento

Véase un ejemplo específico del comando `route print` en Windows:

```cmd
IPv4 Tabla de enrutamiento
===========================================================================
Rutas activas:
Destino de red        Máscara de red   Puerta de enlace   Interfaz  Métrica
          0.0.0.0          0.0.0.0      192.168.0.1     192.168.0.16     35
        127.0.0.0        255.0.0.0      En vínculo         127.0.0.1    331
        127.0.0.1  255.255.255.255      En vínculo         127.0.0.1    331
  127.255.255.255  255.255.255.255      En vínculo         127.0.0.1    331
     172.25.224.0    255.255.240.0      En vínculo      172.25.224.1   5256
     172.25.224.1  255.255.255.255      En vínculo      172.25.224.1   5256
   172.25.239.255  255.255.255.255      En vínculo      172.25.224.1   5256
      192.168.0.0    255.255.255.0      En vínculo      192.168.0.16    291
     192.168.0.16  255.255.255.255      En vínculo      192.168.0.16    291
    192.168.0.255  255.255.255.255      En vínculo      192.168.0.16    291
     192.168.56.0    255.255.255.0      En vínculo      192.168.56.1    281
     192.168.56.1  255.255.255.255      En vínculo      192.168.56.1    281
   192.168.56.255  255.255.255.255      En vínculo      192.168.56.1    281
        224.0.0.0        240.0.0.0      En vínculo         127.0.0.1    331
        224.0.0.0        240.0.0.0      En vínculo      192.168.56.1    281
        224.0.0.0        240.0.0.0      En vínculo      172.25.224.1   5256
        224.0.0.0        240.0.0.0      En vínculo      192.168.0.16    291
  255.255.255.255  255.255.255.255      En vínculo         127.0.0.1    331
  255.255.255.255  255.255.255.255      En vínculo      192.168.56.1    281
  255.255.255.255  255.255.255.255      En vínculo      172.25.224.1   5256
  255.255.255.255  255.255.255.255      En vínculo      192.168.0.16    291
===========================================================================
```

De aquí se puede extraer información.
\
Se supone que el *host* al que pertenece dicha tabla de enrutamiento, al tener un datagrama con destino `Destino de red` podrá conocer la dirección de red por una operación AND con la `Máscara de red` y enviará el datagrama desde la interfaz de red `Interfaz` por medio de la `Puerta de enlace` asociada en la tabla.

> `En vínculo` significa que el destino está directamente conectado con el *host* y no requiere utilizar ningún intermediario. Esto sucede porque todos ellos pertenecen a adaptadores privados o propios como el rango de direcciones de *loopback* `127.0.0.0/8`.

Dicho de otra forma, `Interfaz` es lo que pone el remitente original en la dirección IP de origen en el datagrama, `Destino de red` debe coincidir con el resultado de [(dirección IP de destino) *AND bit a bit* (`Máscara de red`)] y, según la congruencia, se envía por la `Puerta de enlace`.
\
Ante la duda, los *routers* también hacen uso de puertas de enlace para transportar la información por Internet. En efecto, una puerta de enlace es un intermediario que permite la conexión del nodo actual con el de destino.

## NAT

Es un protocolo necesario para permitir el funcionamiento del rango de direcciones privadas.

El protocolo NAT consiste en que, en el cambio del router de utilizar su adaptador privado al público, modifica el datagrama para disponer su dirección IP pública donde el *host* dispuso su dirección IP privada.

![NAT](https://i.blogs.es/69a1f0/nat_concept-en.svg/650_1200.png "NAT")

> Ejemplo:
>
> Un *host* envía un datagrama por la red privada que tiene por `Source IP` la dirección `192.168.0.2`.
>
> El datagrama, tras hacer una operación `Destination IP && Subnet Mask`, debe enviar el datagrama a una red desconocida.
>
> Una red desconocida no figura en la tabla de enrutamiento. En tal caso, se utiliza la dirección `0.0.0.0`: una meta-dirección IP utilizada para destinar lo que no se sabe dónde enviar.
>
> La puerta de enlace de la dirección `0.0.0.0` es la dirección privada `192.168.0.1`. Esta dirección no es casualidad: se trata de la interfaz de red privada del *router*.
>
> El router lee el datagrama y cambia la `Source IP` con dirección `192.168.0.2` por la dirección de su adaptador público `77.230.188.123`.
>
> > Este movimiento es estrictamente necesario y conforma el protocolo NAT. Si el *router* hubiese dejado la dirección perteneciente a la red `192.168.0.0/16` no se podría identificar al emisor o se identificaría erroneamente puesto que la red `192.168.0.0/16` está reservada para uso privado y se repite en todas las redes privadas de todos los hogares.
> 
> El datagrama viaja por Internet con `Source IP` de dirección `77.230.188.123`.
>
> Cuando se destine un datagrama en el que, en su lugar, el `Destination IP` sea el *host* mencionado, viajará por Internet con `Destination IP` de valor `77.230.188.123` pero, al llegar al *router* desde el adaptador público, será intercambiado por `192.168.0.2` de tal forma que ni el *host* ni el receptor noten en ningún momento que hablan con un intermediario.

### PAT

Se trata de una adición a NAT. Hace el mismo proceso pero, además, el *router* también intercambia los puertos de la capa de transporte por los suyos.

## DHCP

Es el protocolo que proporciona una dirección IP privada a un *host* recién conectado a la red.

Implica la comunicación del *host* con un servidor DHCP. Sigue las siguientes fases:

1. DISCOVER
   \
   El *host* envía por difusión (`255.255.255.255`) un mensaje de descubrimiento desde la dirección `0.0.0.0`.

2. OFFER
   \
   Varios servidores DHCP responden desde su propia dirección ofreciendo una dirección de red `IP`.

3. REQUEST
   \
   El *host* responde al servidor DHCP desde la dirección `0.0.0.0` hacia la dirección IP específica del servidor indicando que pretende tomar la dirección `IP` anteriormente ofrecida.

4. ACK
   \
   El servidor DHCP envía un mensaje de reconocimiento con los datos definitivos indicando al *host* la dirección IP que ha adoptado.

##  *Internet Control Message Protocol* (ICMP)

Pertenece a la capa de Internet aunque se encapsule dentro de IP. Es un protocolo dedicado a la obtención de información e informe de errores, no obstante, no corrige errores.
\
Le corresponde el Protocolo `1` en el datagrama.

```
    0                   1                   2                   3
    0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
   +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
   |     Type      |     Code      |          Checksum             |
   +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
   |                    Type and Code dependent                    |
   +-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+-+
```

- Tipo
  \
  Es el identificador principal de la motivación del datagrama ICMP.
  
- Código
  \
  Es un parámetro identificativo que especifica el propósito del Tipo.
  
- Checksum

- Extensión de cabecera
  \
  Algunas combinaciones de Tipo y Código pueden incluir información adicional.

Todos los mensajes ICMP de error copian la cabecera del datagrama IP que lo causó y sus primeros 8 bytes de datos.

> Estos 8 bytes son porque en las dos primeras líneas (de 4 bytes: 32 bits) se disponen los datos más importantes de los encapsulados en IP. Por ejemplo, en TCP corresponden a los puertos y el número de secuencia, y en UDP capturan la totalidad de la cabecera.

## IPv6

Pretende solucionar problemas de IPv4, en especial, la escasez de direcciones.

# Observaciones del autor

Nos encontramos una vez más. Es excelente porque puedo escribir «una vez más» pero jamás sabrás si hice los documentos en desorden y este es el primer encuentro en realidad.
\
¿Qué te voy a contar? Nada que no sepas ya de antemano. Especialmente porque sabes qué entra desde el inicio del documento. Además, ponerle nombre al documento ya ha sido suficiente desafío, el encargado de nombar los temas le ha puesto distinto nombre a lo largo de los documentos, índices y diapositivas así que me he puesto creativo y le he puesto el que he querido, ni sentido sintáctico le he dejado. ¿Será sintáctico? Ni idea, mi problema es enredar con las redes, no con la lengua. El caso es que ese título es -0.2 en selectividad.

Las tablas de enrutamiento entran al examen prehechas por lo que tienes que aprenderte su estructura ya que tu forma de estructurar la información es inútil. Ten en que el examen es una prueba de cómputo y no una prueba de evaluación. Eso sí, que van a aparecer en el examen es conocimiento seguro, común y popular.

El tema NAT no recuerdo que entrase, pero si realmente necesitas estudiar un protocolo que tan solo intercambia números tal vez y sólo tal vez deberías replantearte el lugar en el que estás.

De DHCP no voy a decir nada. No entra y ya. Memorízate "DORA" por si acaso.

ICMP entra con total seguridad. Es más, incluso puede ponerte un ejercicio trampa con ICMP: por experiencia hablo. El examen va a tener, al menos, 2 trampas entre sus ejercicios principales. Destaco lo de "principales" porque el examen solito y sin ayuda, como un niño grande, ya es una trampa por sí solo para que pagues una matrícula más.
\
Si en la protectora de diablillos que tienen por departamento sigue siendo tan cariñoso como acostumbra no tienes que aprenderte información específica de combinaciones Tipo-Código: vienen en el anexo que proporcionan. Esto es más un llamado a la calma porque, evidentemente, la memoria no te va a dar para memorizar tanto dato inútil. Por cierto, lo de los 8 bytes de datos del datagrama de error en ICMP sonaría inteligente si no fuera porque desde hace 15 años la red funciona lo suficientemente bien como para enviar más de 8 bytes o la totalidad los datos.

Respecto a IPv6, es una pena. No se explica nada importante y en el examen no aparece absolutamente nada. No obstante, a nivel personal, es extremadamente curioso porque supone un cambio radical en el funcionamiento de Internet para depurarlo de todos los problemas derivados de IPv4 y devolverle a Internet la intención real que pensaron los ingenieros hace décadas. En cambio, como seguimos en ese eterno proceso de migración a IPv6 o infinto incluso si se aprueba la propuesta del retrocompatible IPv8.
\
En realidad, pareciera la clase de problemas reales a las que debe enfrentarse un ingeniero y no a descifrar capturas de Wireshark que, curiosamente, en la aplicación vienen descifradas y sin obligarte a contar bits. Quizás algún día se enteren de que el avance en la tecnología desde los últimos 20 años no es únicamente para que creen sus exámenes más fácilmente.

Por cierto, he omitido todo el contenido de IPv6. Si se encuentra en el tema probablemente sea por alguna obligación burocrática.
