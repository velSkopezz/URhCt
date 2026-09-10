# **ARyS: Práctica 1**

# Placa base
Sirve para disponer los componentes. Se distinguen de acuerdo a su **factor de forma**:
- Factor **pequeño**
- Factor de **torre**
- Factor de **rack**
      > Nota: Las de clase son 19''.
      
      > Nota: Existen los llamados ***Blade Servers***. Son más pequeños y se insertan de forma vertical en un **mismo bastidor**

> Nota: El factor de forma también decide la disposición de los componentes en la placa.

> Nota: Las fuentes de alimentación van aparte y su ventilación es independiente y propia del fabricante.

# Bastidor
Es un componente **condicionante** de:
- Tipos de **placa base**
- **Unidades** disponibles
- **Conectividad** a periféricos
- **Expansión**

Se distinguen chasis de **tipo**:
- **Torre**
- **Rack**
- Otros (ATX, BTX...)

Algunas características que nos pueden hacer decidir un bastidor pueden ser los **factores de forma permitidos**, **módulos de conversión torre/rack** y, sobretodo, la **eficiencia de ventilación**.

## Chasis tipo rack
### Factores de forma normalizados U
Hay desde 1U hasta 5U.1U = 1.75''. Los racks de 1U suelen soportar 1 slot de expansión. Algunos racks no tienen conexiones normalizadas.

Hay que tener en cuenta que los ventiladores pequeño consumen más, hacen más ruido y vibran debido a las altas revoluciones. No obstante, en estos racks, debido a su reducido tamaño, son los únicos que entran.

# Ventilación

## Radiadores
Las piezas críticas requieren **radiadores**. Estos tienen **aletas** que se disponen de forma longitudinal con estas piezas de tal forma que, por **convección**, el calor se disipa con tan solo el radiador.
\
Cuando el radiador es insuficiente, disponemos ventiladores para forzar el movimiento del calor al radiador.

> Nota: Un radiador se distingue en:
> - **Pasivo** si se basta con el radiador.
> - **Activo** si tiene ventiladores para forzar el correcto flujo de aire.
> 
> Hoy en día, los ventiladores están dispuestos estratégicamente para aprovechar los radiadores. Además, existen **deflectores** que reparten el calor equitativamente. 

> Nota: Los ventiladores suelen ser de 120mm, 92mm u 80mm.

Es común que algunos ventiladores no puedan tomar el aire correctamente. Para solucionar dicho problema, se suelen disponer radiadores en los ventiladores.

## Ventilación en SCSI
La tecnología SCSI permite a los ventiladores a girar a altas revoluciones, lo que genera calor. Por ello, en servidores, con el uso de la tecnología SCSI, se utilizan ventiladores para los discos.

## Flujo de aire
Es un estándar de la industria: los computadores se ventilan **desde delante hacia detrás**.

# Seguridad
Existe un conflicto con los servidores. Se necesita un **sistema sencillo de apertura** para poder cambiar piezas fácilmente. Sin embargo, también se necesita **seguridad** puesto que los servidores suelen tener datos sensibles.
\
Es por ello que estos servidores vienen con **llaves y candados de bloqueo** y una **señal** en la placa para que desde el software se informe al equipo Administrador de sistemas cuando el dispositivo sea abierto.

# Memoria RAM o principal
Es memoria volátil, un componente crítico del sistema, está encapsulado por memorias **DIMM** (d de *double*). Antiguamente eran **SIMM** y por sólo una cara (de ahí la S de *single*).
\
Funcionan de tal manera que por encima de cierto voltaje se considera un `1` lógico. Este voltaje va cayendo por lo que es **realimentado** para no perder la memoria. De ahí que se llame memoria volátil.

A veces se habla de ***Dual Channel***. Es un sistema en el que existen **2 BUSes de acceso a memoria** de forma que cada *channel* se puede utilizar a la vez. En un computador de 64 bits se pueden utilizar un total de 128 bytes.
\
Como el *Dual Channel* no presentaba toda la capacidad que se sospechaba debido al **SDR**, se optó por el **DDR**. El cambio reside en que la transferencia de un *channel* se hace en el flanco de subida y el otro en el flanco de bajada.

> Nota: Hará falta conocer la forma de identificar los tipos de RAM de acuerdo con las indicaciones del fabricante para la asignatura.

Nótese que:

$ 2 \cdot f_{\aplha \tao} = BUS_{vel} = \frac{BW}{\text{bytes}} $

## Memorias para servidores
Utilizan tecnologías impropias para ordenadores personales.

> Nota: Las memorias ECC no son necesariamente *Registered*, aunque casi todas las memorias de tipo *Registered* suelen ser ECC.

### ECC (*error correction code*)
En busca de **seguridad**, utiliza un código de corrección de 7 bits por cada 64 bits de datos. Es común que tenga un pequeño módulo más. Se genera un código de verificación en la escritura y este se comprueba en el momento de la lectura.
\
Por contraparte, son **más caras** puesto que se necesita un chip adicional y son **más lentas** puesto que la verificación toma tiempo. Se siguen utilizando por el notable componente de **fiabilidad**.

### RDIMM (*Registered/buffered Memory*)
Son memorias especiales con un **chip de refuerzo eléctrico**. El objetivo es **reducir la carga** que debe suministrar el controlador de memoria a cada módulo.
