# **ARyS: Práctica 2**

# Interfaz de comunicación para sistemas de almacenamiento

La interfaz estándar **IDE** (*Integrated Drive Electronics*), posteriormente denominado **ATA** (*Advanced Technology Attachment*) se creó para conectar los dispositivos de almacenamiento, basado en ISA.
\
ATA se dividió en dos tecnologías:

- **PATA**: *Parallel* ATA
      \
      Se transmite en paralelo por buses de 16 bits.

- **SATA**: *Serial* ATA
      \
      Se transmite en serie por una única línea.
      
> Nota: *A priori* puede parecer que PATA deba ser más veloz. Sin embargo, la inducción de los hilos paralelos provoca **diafonías** a altas velocidades. Por ello, existe una limitación entre la velocidad y la cantidad de buses.

> Nota: También existe *ATA over Ethernet*, una implementación sobre Ethernet de comandos ATA para montar una SAN (red de área de almacenamiento) presentada como alternativa a iSCSI.

## Interfaz PATA
Incluye 40 pines de los cuales 8 envían datos. El resto son de control. A veces, los cables de las interfaces PATA permiten conectar múltiples discos a un único cable que se conecte a un único adaptador en la placa base.

Quedaron relegados por el estándar SATA y sistema SCSI. 

## Interfaz SATA
Tiene un único conector que ocupa poco. La placa madre suele tener múltiples adaptadores llegando a ser incluso 10 en placas madres antiguas.

La alimentación de SATA tiene múltiples pines para proporcionar más potencia eléctrica.

La transmisión de información en SATA utiliza 7 hilos de los cuales 2 pares transmiten información. Se utilizan en pares puesto que utilizan codificación diferencial.

## Interfaz SCSI
No se estandarizó debido a darle soporte a demasiados adaptadores de forma que usarlo casi siempre requería un adaptador y porque requería un coste adicional en forma de controlador SCSI para la placa base.

Es un sistema **ideado para servidores** de tal forma que soporta de 7 a 15 dispositivos por canal en sus primeras salidas. Además, este bus era veloz: hablamos de alrededor de 150 MB/s que se mantenía a pesar de añadir más discos. Si bien SATA III alcanza 600 MB/s, SCSI lograba 150 MB/s con más de 10 discos a la vez.

## Interfaz SAS
Cuando se habla de *Serial Attached SCSI* se refiere a una interfaz que adopta la transferencia de datos de SCSI utilizando la velocidad que proporcionaba ATA. Sigue utilizando comandos SCSI.

SAS proporciona mayor velocidad de transferencia cuanto mayor es el número de dispositivos conectados. Permite utilizar discos duros SATA y sus adaptadores son también heredados de SATA.

# Sistemas de alimentación en servidores
Hoy en día se utilizan **fuentes de alimentación conmutadas**, de tamaño más reducido, compacto y eficiente que las antiguas estaciones que llegaban a pesar kilogramos. Funcionan de tal manera que *choppean* la señal constantemente, a veces incluso a una frecuencia audible.

Los servidores suelen estar equipados con **múltiples fuentes de alimentaciones** y sistemas **SAI**, es decir, baterías de emergencia en caso de corte de luz. El objetivo de tener múltiples fuentes es el respaldo, es decir, tener 2 fuentes de alimentación de 1000 V no implica tener disponibles 2000 V: sólo se dispone de 1000 V.

> Nota: Todos los servidores del aula de servidores del Complejo Científico Tecnológico tienen 2 fuentes de alimentación de hasta 1000 V.

Las consideraciones para elegir una fuente son:
- Carga del servidor
- Consumo del servidor
- Ubicación geográfica del servidor

## MOLEX 20+4 pines
Es utilizado para la placa base. Muy reconocible.

## MOLEX 4 pines
Utilizado para ciertas placas de vídeo, unidades de almacenamiento, refrigeración y *modding*.

## Estándares
Entre los aspectos más importantes de las normativas se encuentran los límites de ruido y oscilación en sus salidas de voltaje: 120 mV de rizado para +12 V y 50 mV para +5 V, +3.3 V respectivamente.

## VRM
Los *Voltage Regulator Module* son dispositivos que facilitan la regulación de rizados. Funcionan a modo de filtros.

## Sistemas de alimentación en servidores
La potencia necesaria para un sistema de alimentación ininterrumpida puede ser calculada sumando la potencia consumida por cada dispositivo.

Ciertos servidores pueden requerir SAIs más caros o más baratos. Por ejemplo, un sistema médico debería cubrir múltiples horas.

- SAI *standby* (*off-line*)
      \
      Ordenadores personales.
      \
      Funciona de tal forma que existe un conmutador que, al caer la luz, permite el paso de una corriente alterna recién transformada de una batería. El problema es que el conmutador **tarda hasta 6 ms en conmutar** pudiendo caer el servidor.
      
- SAI *Line-interactive*
      \
      Servidores tipo torre y rack.
      \
      Utiliza un sistema en el que existe un **inversor AC/DC** que controla si debe invertir su funcionamiento de acuerdo a si lleva energía o, por el contrario, llega de ella.
      
- SAI *double-conversion* (*on-line*)
      \
      Utilizados en salas con muchos servidores, normalmente *data-centers*. Se denominan verdaderos SAIs.
      \
      Utiliza dos conversores de energía. Primero pasa de AC a DC, luego se carga la batería, sigue a un conversor a AC y luego lo toma el servidor. Tiene un **elevado coste por la doble conversión** de energía, pero el sistema permite que la batería responda de forma inmediata.
      
La función del SAI incluye:
- Cortes de energía
- Sobretensión
- Caida de tensión
- Picos de tensión
- Ruido eléctrico
- Inestabilidad de frecuencia
- Distorsión armónica

Además, también proporcionan protección contra rayos. Cuando caen crean cierto daño al circuito eléctrico. Estos componentes de protección estallan protegiendo al resto de componentes.

La potencia aparente ($S$) se mide mediante voltiamperios (VA) mientras que la potencia activa ($P$) se mide en Wats (W). Se puede aproximar de acuerdo a la siguiente identidad.

$$0.6 \cdot VA = W$$

### Problema de dimensionamiento de SAI/UPS
Requiere la siguiente información:
1. **Potencia activa** necesaria para la actividad.
2. Añadirle un **factor de seguridad** (+20%).
3. Convertir a **potencia aparente**.
4. Determinar el **tiempo de autonomía** requerido.
5. Calcular la **energía requerida**.
6. Seleccionar la **topología de SAI**: *off-line*, *inline*, *on-line*

> Ejemplo 1: Dos servidores Dell con fuentes redundantes de 600 W (80% de eficiencia) se necesitan proteger en caso de falla eléctrica durante 45 minutos. Determinar el SAI necesario a colocar.
>
> Paso 1: Determinar la potencia.
> 
> $$600 W / 80% = 750 W$$
>
> > Nota: El SAI se posiciona entre la alimentación y la fuente. Esto significa que el SAI debe proporcionar la misma energía que la corriente a la fuente.
>
> $$750\frac{W}{\text{servidor}} \cdot 2\text{servidores} = 1500 W$$
>
> Paso 2: Añadir el factor de seguridad.
>
> $$1500 W \cdot (1+20%) = 1800 W$$
>
> Paso 3: Convertir a potencia aparente.
>
> $$1800W / 0.6\frac{W}{VA} = 3000 VA$$
>
> Paso 4: Determinar el tiempo de autonomía.
>
> $$45 min * \frac{1 h}{60 min} = 0.75 h$$
>
> Paso 5: Calcular la energía requerida.
>
> $$E = S \cdot t = 3000 VA \cdot 0.75 h = 2250 VAh$$
>
> Paso 6: Seleccionar la topología del SAI.
>
> Búsquese en la tabla.

> Ejemplo 2: Un SAI existente de tipo *double-conversion* de 3500 VAh tiene conectado una carga de servidores total de 1800 W. ¿Durante cuánto tiempo aguantarán sin caer en caso de falla eléctrica?
>
> $$t = \frac{E}{P} = \frac{3500VAh}{1800W \cdot \frac{1VA}{0.6W}} = 1.18h$$