# Redes de Computadores: Protocolo UDP

Este es uno de los temas más importantes de toda la asignatura. Cuenta con un detalle adicional pues este protocolo es más sencillo que TCP en todos los sentidos por lo que es de interés del profesor para ejercicios más fáciles.

En cuanto al examen, prácticamente puede entrar todo el temario salvo la teoría. No hace falta que te preocupes por la teoría porque prácticamente no tiene y, en cuyo caso, lo único que hay es una tabla de puertos. En cambio, el protocolo, que comprende en realidad la única parte práctica, consta de 4 campos muy sencillos de 2 bytes cada uno.

Para hacer este tema importan fundamentalmente dos aspectos:
1. Que reconozcas con facilidad la información de cabecera UDP desde la captura de Wireshark.
2. Que en vez de hacer el punto 1 con UDP lo hagas con TCP puesto que probablemente UDP sea, tan solo, parte del test.
3. Que reconozcas aún mejor toda la información de la cabecera IP, puesto que ahí siempre es donde te va a querer esconder algo.

## Puertos

Se trata de un identificador para la capa de transporte que funciona en conjunto con la dirección de la capa de Internet para ofrecer transportes diferenciados.
\
Un socket se identifica por medio de, al menos, la dirección de red y el puerto de transporte.

> Ejemplo: Múltiples conexiones activas desde los mismos dispositivos.

Son números entre ciertos valores que se clasifican en tres tipos:

Rango | Nombre | Significado
:--: | :-- | :--
0 - 1023 | Well Known | Son puertos con una funcionalidad prefijada por el estándar de IANA.
1024 - 49151 | Registrados | Son puertos reservados para terceros respecto a IANA.
49152 - 65535 | Dinámicos o privados | Son puertos para el usuario, normalmente utilizados por el sistema operativo para abrir sesiones como cliente.

Puertos frecuentemente utilizados:

Números de puerto (DEC) | Puerto Servicio
--: | :--
7 | ECO
13 | HORA
17 | QOTD
21 | FTP
23 | Telnet
25 | SMTP
53 | DNS
80 | HTTP
110 | POP3
143 | IMAP

## Protocolo UDP

Es un protocolo destacado por penalizar la seguridad en favor de una mayor velocidad y proporcionar compatibilidad con *broadcast*.

```
                  0      7 8     15 16    23 24    31
                 +--------+--------+--------+--------+
                 |     Source      |   Destination   |
                 |      Port       |      Port       |
                 +--------+--------+--------+--------+
                 |                 |                 |
                 |     Length      |    Checksum     |
                 +--------+--------+--------+--------+
                 |
                 |          data octets ...
                 +---------------- ...
```

- Puerto de origen
  \
  Indica el puerto del *host* emisor.

- Puerto de destino
  \
  Indica el puerto del *host* receptor.

- Longitud
  \
  Indica la longitud total del datagrama incluyendo cabecera y datos.

- Checksum
  \
  Hace uso de una pseudocabecera, exactamente igual que en TCP, de la siguiente forma:
  
  ```
                    0      7 8     15 16    23 24    31
                 +--------+--------+--------+--------+
                 |          source address           |
                 +--------+--------+--------+--------+
                 |        destination address        |
                 +--------+--------+--------+--------+
                 |  zero  |protocol|   UDP length    |
                 +--------+--------+--------+--------+
  ```

  En conjunto, se hace: $Checksum = pseudocabecera + cabecera + datos$.

  > Recordatorio de que se hacen en palabras de 16 bits, si faltase un byte se rellena con un *padding* de `0x 00`.

# Observaciones del autor

Vamos a hacer un repaso porque no hay mucho con lo que perderse aquí.

Para empezar, no vale mucho la pena mirar este tema. Quisiera decir que, siendo el departamento tan agradable como para hacer un examen que evalúa tu capacidad de computar cual ordenador en vez de evaluar tu conocimiento, poner UDP en vez de TCP por ser más liviano es una posibilidad real. En cambio, esto es falso. Como mucho, podrás ver el mayor acto de misericordia en forma de 6 preguntas del test sobre un protocolo que debería preguntarte en el ejercicio de las 20 tramas. Pero no, cuando se dijo «Verás cosas aun peores que estas» muy probablemente se referían a este examen.

Si te interesan los tipos de puertos, no te entusiasmes. Al examen no.

Si te interesan los puertos comúnmente utilizados, insolente: se te va a olvidar. Y, además, no te entusiasmes. Al examen no más que un mísero ejercicio de los ochenta del test que vale la mitad o menos del ordinario.

Sólo tienes que hacer una cosa, leer bytes y computar. No importa que lo entiendas: lee bytes y computa.
