# Redes de Computadores: Servicio Mail

El examen incluye 3 protocolos principales: SMTP, ESMTP e IMAP. POP3 es mencionado aunque su relevancia es mínima. La puntuación relativa a este tema se encuentra en el tipo test y, por consiguiente, el objetivo de estudio de este tema es la memorización de datos teóricos ignorando por completo el funcionamiento de las aplicaciones y cualquier cosa que exceda la complejidad máxima para que responder la pregunta de un test valga siquiera la pena.

En concreto, se incide con máxima frecuencia en los comandos existentes de cada aplicación. Por ello, es fundamental comprender cuál es el funcionamiento de cada uno y memorizar los comandos que proporciona.

## Simple Mail Transfer Protocol (SMTP)

> Enviar correos

Viene implementado en los servidores de correos puesto que sirve para **enviar correos entre servidores de correos** y para enviar correos desde los clientes a los servidores.
\
Utiliza **TCP**.

Sigue la siguiente estructura:
- Cabecera
- Línea en blanco
- Datos

Conjunto de órdenes (cliente) | Función
:-- | :--
`HELO nombre de dominio <CR><LF>` | Identifica el origen de la conexión
`MAIL FROM: <dirección origen> <CR><LF>` | Remitente
`RCPT TO: <dirección destino> <CR><LF>` | Destinatario
`DATA <CR><LF>` | Introducción de datos
`RSET <CR><LF>` | Aborta la conexión con servidor SMTP
`QUIT <CR><LF>` | Cierra la conexión con servidor SMTP
`HELP <CR><LF>` | Muestra ayuda sobre órdenes
`EXPN <dirección de correo> <CR><LF>` | Expande una lista de correo
`VRFY <dirección de correo> <CR><LF>` | Verifica la existencia de una dirección

> Todos los servidores de correos deben implementar `EHLO` cuyo fin es utilizar ESMTP. No obstante, si no implementasen ESMTP, están obligados a responder a EHLO con un código de error del tipo `5XX` (error permanente).

> Ejemplo de diálogo SMTP:
> ```http
> S: 220 mail.example.com ESMTP Service Ready
> C: HELO mail.eevidence.com
> S: 250 mail.example.com Hello mail.eevidence.com
> C: MAIL FROM:info@eevidence.com
> S: 250 OK
> C: RCPT TO:johndoe@example.com
> S: 250 OK
> C: DATA
> S: 354 End data with <CR><LF>.<CR><LF>
> C: Subject: Test SMTP message
> C: From: info@eevidence.com
> C: To: johndoe@example.com
> C:
> C: Hola John, este es un mensaje de prueba enviado mediante SMTP.
> C: .
> S: 250 OK Message accepted for delivery
> C: QUIT
> S: 221 Bye
> ```

### Extended SMTP (ESMTP)

Se trata de extensiones para SMTP que pueden estar implementadas en servidores.

Extensiones mencionadas en el PDF del temario:
- `8BITMIME`: Permite usar datos de 8 bits en vez de los 7 bits de ASCII NVT (con el primer bit a 0).
- `SIZE <cantidad>`: Indica el tamaño máximo del mensaje salvo el fin del mensaje.
- `DSN` (Delivery Status Notification): Proporciona al emisor información DSN si el correo no se logra enviar correctamente.

### Multipurpose Internet Mail Extension (MIME)

Proporciona soluciones a los problemas de SMTP relativos a:
- Distintos alfabetos
- Contenido multimedia

Indicación complementaria | Uso | Ejemplos
:-- | :-- | --:
`Content-Type` | Indicador de tipo/subtipo | text/plain, image/gif, audio/x-mpeg, application/pdf
`Content-Transfer-Encoding` | Indicador de codificación | 7bit, base64
`Charset` | Indicador de juego de caracteres | \

> Ejemplo de uso desde cliente:
> ```http
> From: maria@disca.upv.es
> To: paco@upvnet.upv.es
> Subject: ENVIANDO VIDEO
> MIME-Version: 1.0
> Content-Type: video/mpeg
> Content-Transfer-Encoding: base64
> Datoscodificados en base64.....
> ................................
> .....Datoscodificados en base64
> ```

#### Codificación de Base64

Consiste en usar una tabla que codifica menos caracteres pero **solo necesita 6 bits** ($2^{6} = 64$) para codificar un caracter.

A nivel computacional es inútil el cambio a un solo byte pero la conversión gana utilidad con números divisibles tanto entre 6 como entre 8:
- 3 bytes (24 bits) de 8 bits por grupo (byte convencional) codifican 3 caracteres
- 3 bytes (24 bits) de 6 bits por grupo (Base64) codifican 4 caracteres

> Ejemplo de conversión:
> ```http
> DNI10:        1       2       3       4       5       6       7       8       P
> DNI16:       31      32      33      34      35      36      37      38      50
> DNI02: 001100010011001000110011001101000011010100110110001101110011100001010000
> DNI02: 001100010011001000110011001101000011010100110110001101110011100001010000
> Dni64:     12    19    08    51    13    03    20    54    13    51    33    16
>             M     T     I     z     N     D     U     2     N     z     h     Q
> ```
> ![Tabla de conversión Base64](https://upload.wikimedia.org/wikipedia/commons/0/01/Base_64_table_index.png "Tabla de conversión Base64")
>
> > Nota del autor:
> > Con total honestidad, no tengo ni idea de cómo funciona esto. Es como si tomase el valor en ASCII, luego lo transformase en binario (tamaño 8), luego los agrupase en 6 bits y, finalmente, los transformase según la tabla de codificación de Base64.
> >
> > En cualquier caso, si sale, esto es un ejercicio del *"tipo test"* -entre comillas dado que cuenta y penaliza como un test pero cuesta como un ejercicio convencional- y es lo suficientemente costoso como para que no valga la pena hacerlo en el descaradamente insuficiente tiempo que el examen requiere para completarse.

#### Mensajes multiparte

Mediante el ejemplo:

```http
Content-Type: multipart/mixed; boundary=Secuencia_reconocible
```

Cada vez que aparezca en el mensaje la secuencia de texto `--Secuencia_reconocible` se identificará como un indicador de cambio de parte del correo. Normalmente esta secuencia reconocible será un conglomerado de caracteres ilegibles.

Subtipos de multipart:
- mixed: múltiples partes independientes con procesamiento secuencial
- parallel: las partes deben verse simultáneamente
- digest: cada parte es un mensaje RFC 822
- alternative: mismo mensaje pero en diversos formatos

## POP3

> Leer correos

Utiliza el puerto 110 de TCP.

El servidor responde con un `+OK` o con `-ERR`. Deja un espacio en blanco y proporciona información adicional en la línea siguiente.

Órdenes del cliente | Uso
:-- | :--
`USER usuario <CR><LF>` | Identificación de usuario
`PASS password <CR><LF>` | Contraseña
`STAT <CR><LF>` | Devuelve número de mensajes y tamaño en bytes
**`LIST <CR><LF>`** | Lista mensajes en el buzón y sus tamaños
**`RETR n<CR><LF>`** | Lee un mensaje
**`DELE n<CR><LF>`** | Marca un mensaje para borrar (al salir)
`TOP mens líneas <CR><LF>` | Lista las cabeceras de los mensajes más las líneas del cuerpo que se indican
`UIDL <CR><LF>` | Lista los mensajes con su "unique id listing"
`RSET <CR><LF>` | Abandona. No se borran los mensajes marcados
`QUIT <CR><LF>` | Termina. Borrar todos los mensajes marcados

> Ejemplo de sesión POP3
> ```http
> S: +OK POP3 server ready
> C: user paco
> S: +OK
> C: pass paco_pass
> S: +OK user successfully logged on
> C: list
> S: 1 123
> S: 2 456
> S: 3 789
> S: .
> C: retr 1
> S: <contenidomensaje1>
> S: .
> C: dele 1
> C: retr 2
> S: <contenidomensaje2>
> S: .
> C: dele 2
> C: retr 3
> S: <contenidomensaje3>
> S: .
> C: dele 3
> C: quit
> S: +OK POP3 server signing off
> `` 

## Internet Message Access Protocol (IMAP)

> Gestión general

Utiliza el puerto 143 de TCP.

Es más completo que los protocolos anteriores.

Órdenes de IMAP contempladas por el PDF:
- `LOGIN`: Ingreso de un usuario a su cuenta. Forma no segura porque el password es visible (texto plano)
- `AUTHENTICATE`: autentifica al usuario de forma segura
- `LOGOUT`: desconexión
- `CREATE`: crea una carpeta
- `DELETE`: borra una carpeta
- `RENAME`: Cambia el nombre de una carpeta
- `SELECT`: selecciona una carpeta en el servidor para acceder/modificar
- `CLOSE`: cierra la carpeta y borra los mensajes marcados para borrar
- `EXPUNGE`: borra todos los mensajes marcados para borrar
- `SEARCH`: busca mensajes según algún criterio de búsqueda
- `FETCH`: lee un mensaje (o una parte del mismo)
- `STORE`: cambia el valor de los flags de un mensaje
- `COPY`: copia los mensajes de una carpeta a otra

Respuesta del servidor | Significado
:-- | :--
`OK` | Ejecución correcta
`NO` | No se ha podido realizar
`BAD` | Comando desconocido

# Observaciones del autor

Resulta obvio que este tema no tiene ningún interés a nivel formativo puesto que todo su contenido son tablas que en tu vida laboral vas a acabar buscando en internet.

El test está lleno de contenido de servicio de correos. El motivo tampoco lo oculta el Pentágono: a los profesores les pica una barbaridad que no asistas a clase. Así, además, lo ha hecho notar en los grupos reducidos y actividades de evaluación contínua cuyo coste es el 40% de la nota aunque luego resulte totalmente irrelevante porque necesitas un 3.5/10 del examen ordinario (60%) para aprobar.

Este tema no se pregunta porque tenga cualquier tipo de interés académico sino porque es la herramienta estrella del profesor para averiguar quién ha asistido a clase los días en los que menos vale la pena asistencia, es decir, las preguntas ni siquiera pretenden ser difíciles (e.g.: Qué significa DSN.) ni desafiantes. Son únicamente un escape moral del profesor para excusarse por suspender al 60% de la clase.

Los puertos de la capa de aplicación tampoco tienen interés académico pero todos sabemos que poner sobresaliente en la universidad, y más en una ingeniería, se considera pecado capital. Mi recomendación es no estudiarlo porque se te va a olvidar igualmente.

En el exámen se preguntan explícitamente comandos. Tampoco puede preguntar mucho más de IMAP y POP3 porque su atracción probablemente homoerótica al protocolo SMTP le impide dar temario de algo que no se te vaya a olvidar en media semana y que incluso el propio profesor se haya tenido que estudiar minutos antes de dar la clase en la que revise reiteradas veces la diapositiva a modo de chuleta porque la memoria no está hecha para guardar información que proporciona un comando *help* -o al menos eso creo que piensan los pedagogos, aunque su opinión tampoco le importa mucho a los docentes-. Mi recomendación es que aprendas qué tipo de servicio proporciona cada protocolo (SMTP, POP3, IMAP) para poder deducir si el comando sirve para proporcionar su servicio o, en su defecto, no encaja: como si estuvieras haciendo la EBAU en Andalucía y triángulo no encajase en el hueco de la circunferencia.
