# Redes de Computadores: Nivel físico

Aquí puedes ser preguntado, principalmente, por aspectos de flancos.

## Transmisión de datos

### Transmisión paralela

Se usan tantos cables como bits y se envían simultaneamente.

### Transmisión en serie: asíncrona

Utiliza bits de inicio y de parada.

![Transmisión en serie asíncrona](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQ3UUbDbRZ0rwgnZeUYmODWUp5nPXhuu4gtFXsL-utsv09wfBNfuf_bC8w&s=10 "Transmisión en serie asíncrona")

### Transmisión en serie: síncrona

Se envían los datos y el reloj con el que se han creado.

![Transmisión en serie síncrona](https://picmania.garcia-cuervo.net/images/trans_sincrona_02.gif "Transmisión en serie síncrona")

## Señales

Dado que las ondas senoiales son periódicas, es común la representación por amplitud sobre frecuencia (dominio de la frecuencia).

![Graficar ondas](https://media.wiki-power.com/img/20221210154759.png "Graficar ondas")

En la representación pude incluirse armóncos de la misma onda.

### Perturbaciones de la señal

- Ancho de banda limitado: el ancho de banda provocará un efecto de filtro de paso bajo.
- Atenuación: se contrarresta con amplificadores o repetidores.
- Distorsión
  - Por atenuación
  - Por retardo
- Ruido
  - Térmico
  - Diafonía
  - Impulsivo
 
## Medios de transmisión

Se clasifican.
- Guiados
  - Par trenzado
    
    Clasificados de acuerdo al esquema de cableado:
    - Cable directo
    - Cable cruzado
    
    Clasificados de acuerdo con la protección y apantallamiento:
    - UTP (Sin apantallado)
    - FTP (Con Pantalla Global)
    - STP (Con Apantallado)
    - SFTP (Apantallado con Pantalla Global)
  - Cable coaxial
  - Fibra óptica
- Inalámbricos
  - Radio
  - Infrarrojos

## Modulación y Codificación

- Modulación
  \
  Genera una señal analógica a partir de una digital.
  
- Codificación
  \
  Genera una señal digital a partir de otra digital.

### Mdulación digital

- En amplitud (ASK).
- En frecuencia (FSK).
- En fase (PSK).
- En fase diferencial (DPSK): sólo si el siguiente equivale a `1` altera la fase.

![Tipos de modulación digital](https://thumbs.static-thomann.de/thumb//thumb1000x/pics/cms/image/guide/es/microfonos_inalambricos/03_03_pskusw_esp.jpg "Tipos de modulación digital")

Además, también se pueden combinar entre ellas para obtener múltiples codificaciones a la vez.

![PSK a múltiple nivel](https://ars.els-cdn.com/content/image/1-s2.0-S0030401819302500-gr1.jpg "PSK a múltiple nivel")

La modulación permite crear canales por medio de filtros de paso bajo.

## Codificación

- No retorno a cero (NRZ): Los `0` se leen como flanco bajo y los `1` como flanco alto. Se mantiene el flanco.
- Retorno a cero (RZ): Igual a NRZ con la salvedad de que entre bit y bit se baja el flanco a 0.
- No retorno a cero invertido (NRZI): El cambio en el flanco indica `1`. Se mantiene el flanco.
- Manchester: En la totalidad de los bits hay un cambio de flanco a la mitad de la duración del interbalo del bit. Facilita la sincronicación y es usado en Ethernet.
- Manchester diferencial: Similar a Manchester pero se codifica `1` con la lectura de un cambio del patrón.

![Tipos de codificación](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEga8qP7M1KdfH0W4W5HNOkLTcA79LYbMq78E3pzLDw4IfdAi48SIjb5vzbXjVPr4LOAHurrKvM8iVE0249zzzXjghDVoxcuX2uvFLEQN5TfsNgpQe0KyVl6C-MsLiwVeItf9BWucy5N0-b6/s400/sistemas_de_codificacion.PNG "Tipos de codificación")

# Observaciones del autor

Un tema que es lo que parece, relleno puro y duro. Lo que se supone que es base para tu conocimiento pero en realidad es contenido para que el temario que sí te van a preguntar haya que darlo a última hora y corriendo las últimas 7 semanas con todos los trabajos y parciales de por medio. Y ni se te ocurra faltar a una clase por querer aprobar un trabajo de la misma asignatura, eh. Ni que valiese más el trabajo que la representación del mismo en el examen final con la salvedad de qu e si sacas un 0 en el trabajo no apruebas porque vale mucho porcentaje pero si sacas un 0 en el examen tampoco apruebas porque han puesto un criterio crítico para que pagues otra matrícula.

Me voy por las ramas. Estúdiate codificación, modulación y los apantallados de los cables. Lo demás no creo que lo pregunte, los tipos de transmisión tienen poca gracia y la parte de señales sería deshonesto sin haber dado desarrollo de Fourier y vagamente armónicos.

Parte de test, por supuesto. Aunque no descartes un ejercicio práctico en el test por ningún motivo.
