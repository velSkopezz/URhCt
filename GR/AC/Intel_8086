---
title: Intel 8086 Arquitectura de Computadores
author: Christian Velasco Pérez
---
# **Intel 8086: Arquitectura de Computadores**
*Autor:* Christian Velasco Pérez <img src="https://iili.io/fpTTGnt.md.jpg" alt="Skopez" align="right" style="width:15%; margin-left:4%;margin-bottom:2%">
\
El siguiente contenido corresponde a un **apoyo** educativo para cualquier interesado y por eso puede contener fallos. El documento está orientado al curso de *Arquitectura de computadores* del Grado en Ingeniería Informática de la Universidad de La Rioja y se considera completa responsabilidad del lector lo que haga con la información de este documento.
\
La distribución del documento queda reservada al permiso explícito de su autor. Si necesitase información de contacto puede [enviar un correo](mailto:velskopezz@gmail.com).

---

Durante las prácticas de la asignatura de [Arquitectura de Computadores](../../3º/Arquitectura_de_Computadores.md) se va a utilizar [lenguaje ensamblador](https://es.wikipedia.org/wiki/Lenguaje_ensamblador). Ello implica que es necesario conocer un procesador específico, en esta asignatura ese procesador será el [Intel 8086](https://es.wikipedia.org/wiki/Intel_8086_y_8088), conocido por ser el inicio de la [arquitectura x86](https://es.wikipedia.org/wiki/X86).

> El procesador 8086 es de 16 bits y divide el trabajo de procesamiento y transferencia para que funcione de forma paralelizada.

# Buses del sistema

Que el procesador sea de 16 bits no solo implica la cantidad de bits que almacenan los registros sino, también, la cantidad de **líneas de anchura** de datos de los buses.

-  **Bus de datos**

    Transporta los valores.

    En el Intel 8086 es de 16 bits.

- **Bus de direcciones**

    Transporta las direcciones. Con un procesador de $n$ bits se permiten $2^n$ direcciones.
    
    En específico, el Intel 8086 tiene 20 bits para las direcciones. En total, debería ser $2^{20}b = 2^{10} \cdot 2^{10}b = 1MB$ de valores direccionables. Desde la `0x 00 0000` hasta la `0x ff ffff`.

- **Bus de control**

    Se verá próximamente, transporta información de control de ciertas situaciones.
        
    > A pesar de lo dicho, no se verá próximamente.

Para llegar a registros de 20 bits se van a tener que **utilizar dos registros**, lo que dejará un aholgura de $20b - 2 \cdot 16b = 12b$.

## Segmentación de la memoria

La memoria está dividida en **segmentos**. Estos segmentos contarán con un **desplazamiento** para formar una **dirección de memoria**.
\
Se calcula de la siguiente forma con el fin de que sólo se puedan direccionar direcciones disponibles:

$$\text{``direccion física"} = 16 \cdot \text{``segmento"} + \text{``desplazamiento"}$$

> Las direcciones físicas suelen escribirse en hexadecimal. Es por ello que la fórmula puede reescribirse en `dir_física = 10 * dir_segmento + desplazamiento`, lo que facilitará los cálculos.

> e.g.: Dirección `0000:1050`.
>
> segmento := `0x 0000`
> \
> desplazamiento := `0x 1050`
>
> dirección = `(0x 0000) * (0x 10) + (0x 1050) = (0x 00 1050)`
>
> > Si se hacen los cálculos, puede notarse que `0010:0f50`, `0100:0050` o `0105:0000`, por ejemplo, también direccionan la misma ubicación en memoria.

Es importante notar que las **direcciones de memoria están solapadas entre los segmentos**. A pesar de que deberían haber $64^2kB$ de espacio direccionable puesto que hay 64kB de segmento y 64kB de desplazamiento, en realidad sólo hay $1MB$ de espacio real de direcciones.

> Nótese que todas las direcciones de segmento acaban por `0x 0` yq ue todas las direcciones que acaben por `0x 0` indican el inicio de un nuevo segmento puesto que cada dirección de segmento se ve multiplicada por `0x 10`.

# Registros

Se identifica el tipo de acuerdo con un sufijo alfabético. Además existen una serie de **registros de estado**.

## Generador de direcciones

A partir de los registros se calcula la **dirección de memoria principal** que se corresponde.

## Identificación de registros

Los registros se identifican de acuerdo con el siguiente sufijo:

- **`X`**: generales
- **`I`**: índices
- **`P`**: punteros
- **`S`**: segmentos

Además de registros de **estado** que están en los *flags*.

> Los *flags* indican el resultado de la última operación de la ALU. Ello implica que, salvo operaciones de modificación directa de los *flags* (e.g.: `CLD`, `STC`...), los registros de estado se veran inalterados si una instrucción no requiere pasar por la ALU.
>
> > e.g.: **`MOV AX, 0` no levantará el *flag* `ZF`** porque `MOV` no es una instrucción aritmética ni lógica: no pasa por la ALU.

### Registros generales

Hay cuatro registros generales que pueden usarse de **forma generalizada** aunque **almacenan resultados normativos**.

> La notación `AH << 4 + AL` será equivalente a `AH:AL` siendo `AH` y `AL` registros de 1 byte.

Todos los registros generales ocupan 2 bytes y podrán dividirse en 2 partes de 1 byte cuyos sufijos serán `H` si son la mayor o `L` si son el menor.

> e.g.: `AX = AH:AL`, `BX = BH:BL`, etc

- **Acumulador** (`AX`)
        \
        Almacena los resultados de la ALU.

- **Base** (`BX`)
        \
        Almacena la dirección base de un array, sin su desplazamiento.

- **Contador** (`CX`)
        \
        Almacena la cantidad de veces que debe repetirse un bloque funcional.
    
- **Datos** (`DX`)
        \
        Apoya al acumulador en caso de overflow formando `DX:AX`. También almacena información en ciertas instrucciones de entrada y salida, inlcuyendo los puertos.

Por tanto, se pueden almacenar 32 bits, y con ello [números en coma flotante](https://es.wikipedia.org/wiki/IEEE_754), por medio de `DX:AX` ($2 \cdot 8b + 2 \cdot 8b = 32b$).

