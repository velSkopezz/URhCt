# Redes de Computadores: Servicio DNS

El contenido del examen sobre DNS comprende únicamente cuestiones teóricas para las cuales la memorización prima sobre la compresión profunda. Se incluyen preguntas teóricas superficiales y, en el peor de los casos, podría formar parte de un ejercicio en el que se involucrase en el interior de una trama completa.

## Domain Name System (DNS)

Es un protocolo de aplicación que accede a una base de datos distribuida (motivos obvios) y que utiliza su **sintaxis propia**.

```
dominios_de_segundo_nivel.dominio_top_level.
```

- **Dominio Root**: Más alto expresado con `.`
- **Dominios Top-Level**: com, org, edu, es...
- **Dominios de segundo nivel**: continenen hosts y subdominios

> Ejemplo:
>
> ```
> unirioja.blackboard.com
> ```
>
> `unirioja` es de segundo nivel.
> \
> `blackboard` es de segundo nivel, de una jerarquía mayor que el anterior.
> \
> `com` es de top-level.
> \
> Existe un `.` implícito al final del URL.
> 
> URL real, ignorando nombres canónicos:
> ```
> unirioja.blackboard.com.
> ```

## Servidores DNS

Se organizan en 3 tipos:
- **Servidores locales**
  \
  Pertenecen al ISP y sirven para no saturar la red.

- **Servidores raíz**
  \
  Hay 13 servidores distribuidos por el planeta. Es común que un servidor raíz no conozca el nombre de un host, en cuyo caso, le preguntará a un encargado DNS (autorizado) del dominio al que pertenezca el host.

- **Servidores autorizados**
  \
  Un servidor es autorizado si en su base de datos existe la correspondencia nombre-dirección, es decir, si no ha tenido que preguntar a otro.

## Consultas DNS

Hay dos formas de evaluar una consulta. Normalmente son recursivas a excepción de la primera, que es iterativa.

### Consulta DNS recursiva

Consiste en un proceso de peticiones y respuestas bilaterales.

```
HOST - ISP - ROOT - intermediario - AUTORIZADO
```

1. `HOST` le pregunta al servidor `ISP` por un dominio.
2. Servidor `ISP` desconoce el dominio: le pregunta a un servidor `ROOT`.
3. Servidor `ROOT` desconoce el dominio: le pregunta al servidor `intermediario` del dominio.
4. Servidor `intermediaro` desconoce el dominio: le pregunta al servidor `AUTORIZADO`.

El servidor `AUTORIZADO` conoce la dirección del dominio así que se lo comunicará al `intermediario`, este al `ROOT`, este al `ISP`, y este al `HOST`.

![Recursion DNS](https://w3.ual.es/~vruiz/Docencia/Apuntes/Networking/Protocols/Level-5/01-DNS/c02f21.png "Recursion DNS")

### Consulta DNS iterativa

La idea sigue siendo comunicación bilateral con la salvedad de que un servidor responde con la dirección que puede ayudarle.

```
      ROOT
        |
HOST - ISP - intermediario
        |
    AUTORIZAOD
```

1. `HOST` le pregunta al servidor `ISP` por un dominio.
2. Servidor `ISP` desconoce el dominio: le pregunta a un servidor `ROOT`.
3. Servidor `ROOT` desconoce el dominio: le indica a `ISP` que `intermediario` conoce la respuesta.
4. Servidor `intermediaro` desconoce el dominio: le indica a `ISP` que `AUTORIZADO` conoce la respuesta.

El servidor `AUTORIZADO` se comunica directamente con `ISP` y este le indica la respuesta a `HOST`.

![Consulta DNS iterativa](https://www.administracionderedes.com/wp-content/uploads/2017/01/consulta-iterativa.jpg "Consulta DNS iterativa")

## Caché y registros DNS

Cuando un dispositivo recibe una correspondencia DNS hace una **copia en caché** en favor del Principio de Localidad de Referencia. Se indica como nodo *no autoritativo*.

Los servidores almacenan información en forma de ***registro de recursos** (RR):
- nombre
- valor
- tipo
- TTL

### Tipo de registros DNS

- Tipo `A`
  \
  Dirección IPv4 de un host.

- Tipo `NS`
  \
  Nombre de un servidor autorizado para un dominio.

- Tipo `CNAME`
  \
  Alias de un nombre canónico.
  
- Tipo `MX`
  \
  Alias d eun servidor de correos.

- Tipo `PTR`
  \
  Dirección IP codificada como nombre de dominio.

## Mensajes DNS

Siguen el siguiente formato

```
                                    1  1  1  1  1  1
      0  1  2  3  4  5  6  7  8  9  0  1  2  3  4  5
    +--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+
    |                      ID                       |
    +--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+
    |QR|   Opcode  |AA|TC|RD|RA|   Z    |   RCODE   |
    +--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+
    |                    QDCOUNT                    |
    +--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+
    |                    ANCOUNT                    |
    +--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+
    |                    NSCOUNT                    |
    +--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+
    |                    ARCOUNT                    |
    +--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+
```

Cabecera:
- ID: 2 btyes de identificador.
- Flags: el PDF no los explica de forma detatllada, revisar el [RFC 1035](https://www.ietf.org/rfc/rfc1035.txt) en cuyo caso.
- Cantidad de consultas.
- Cantidad de RR respuesta.
- Cantidad de RR de autorización.
- Cantidad de RR adicionales.

Contenido, de tamaño variable:
- Consultas.
  \
  Con el siguiente formato
  ```
                                      1  1  1  1  1  1
      0  1  2  3  4  5  6  7  8  9  0  1  2  3  4  5
    +--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+
    |                                               |
    /                     QNAME                     /
    /                                               /
    +--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+
    |                     QTYPE                     |
    +--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+
    |                     QCLASS                    |
    +--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+
  ```
- RR de respuestas.
- RR de autorización.
- RR sobre información adicional.

Los RR siguien el siguiente formato:
```
                                    1  1  1  1  1  1
      0  1  2  3  4  5  6  7  8  9  0  1  2  3  4  5
    +--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+
    |                                               |
    /                     NAME                      /
    /                                               /
    +--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+
    |                     TYPE                      |
    +--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+
    |                     CLASS                     |
    +--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+
    |                     TTL                       |
    +--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+
    |                     RDLENGTH                  |
    +--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+
    |                                               |
    /                     RDATA                     /
    /                                               /
    +--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+--+
```

### Comprensión de mensajes DNS

Para escribir URLs se utiliza una notación especial. Puesto que los nombres no pueden contener números, la cantidad de caracteres del nombre se indica como punto. Véase un ejemplo.
```
unirioja.blackboard.com.
```
\
Aparecería en una trama de la siguiente forma:
```
8unirioja10blackboard3com0
```

Además, si ya se hubiera visitado otra página de blackboard y, por consiguiente, se tuviera `blackboard.com.` en el mensaje, se haría uso de punteros de tal forma que un puntero \*P hacia `10blackboard3com0` se dispondría para ahorrar espacio con:
```
8unirioja*P
```

Para identificar un puntero se toma cualquier byte igual o superior a `0x C0`. Esto se debe a que no se permite que un dominio tenga 192 caracteres por lo que, al encontrar dicho byte, se decarta que se trate del tamaño del dominio y se presupone que es un puntero. Es común encontrar `0x C0 0C` (`0x 0C` = 12), esto se debe a que la cabecera de DNS son 12 bytes.

# Observaciones del autor

La capa de aplicación para sorpresa de nadie no tiene ningún interés formativo. La ventaja es que, si te interesa DNS, probablemente cualquier cosa sea lo suficientemente divertida para tí porque no creo que ni el profesor disfrute de la información de este tema.

El contenido de este tema, como se indica al principio, o pertenece al test cuya calificación es absurdamente injusta o, además de pertenecer al test, forma parte del ejercicio con mayor maldad que pueda añadir jamás. Si sucede este último mejor hacerse bola y llorar que intentar sacarlo porque a un tema por semana no vale la pena aprender tanto DNS.

Tal vez lo único que valga la pena aprender sean los tipos de servidores, de consultas y de dominios pero todos sabemos que en una ingeniería no se puede preguntar por contenido útil a nivel profesional si eso implica que más de un 50% del alumnado se libre de pagar una segunda matrícula: si querían pagar una vez que paguen la privada. O algo así deben pensar del estudiante.
\
Las preguntas probablemente tengan relación únicamente con los formatos que alguna vez un ser del averno decidió escribir antes de publicarlos en el RFC 1035. No pasa nada, DNS no es lo suficientemente importante como para que te dé tiempo a aprenderte esto y el resto del tema, aunque el profesor lo vaya a preguntar igualmente por el valor de 0.5 puntos del examen. No te preocupes, lo importante no es acertar, sino tener una excusa válida para fallar. Y, con sinceridad, que ese examen sólo lo complete a tiempo una supercomputadora de un centro de datos a un océano de distancia debería ser excusa suficiente para todos pero, por lo visto, según la Constitución, que el 60% de los presentados suspenda significa que el 60% de los presentados no ha estudiado y no que el profesor no ha logrado transmitir el conocimiento ni al 40% de la clase o que directamente la evaluación sea pésima. En cualquier caso, asegúrate de saber qué es el RR porque el muy agradable sujeto que te ha dado clase durante 6 meses se va a dedicar a escribir RR en el examen para asegurarse de que sobreentiendas que habla del DNS en la capa de aplicación y no de absolutamente cualquier concepto que ha salido en los otros tantos protocolos de literalmente todas las capas del modelo.

En cualquier caso, este tema carece de importancia salvo que aparezca en un ejercicio. En el test no valdrá lo suficiente como para que te sea más rentable invertir tu tiempo en aprenderte esto que en el formato de TCP porque de alguna forma se la ha ingeniado para que ningún ejercicio del examen valga la pena.
