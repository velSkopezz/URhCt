---
title: Métodos Formales en Programación
author: Christian Velasco Pérez
---
# Métodos Formales en Programación
*Autor:* Christian Velasco Pérez <img src="https://iili.io/fpTTGnt.md.jpg" alt="Skopez" align="right" style="width:15%; margin-left:4%;margin-bottom:2%">
\
El siguiente contenido corresponde a un **apoyo** educativo para cualquier interesado y por eso puede contener fallos. El documento está orientado al curso de *Métodos formales en programación* del Grado en Ingeniería Informática de la Universidad de La Rioja y se considera completa responsabilidad del lector lo que haga con la información de este documento.
\
La distribución del documento queda reservada al permiso explícito de su autor. Si necesitase información de contacto puede [enviar un correo](mailto:velskopezz@gmail.com).

# TEMA 1: Introducción, abstracción y formalismo en programación
Al principio, la programación era procedural y en lenguaje máquina lo que conllevaba una **difícil depuración**. Tras la crisis de los 60' y 70' se crearon los **métodos formales** en forma de formalismos matemáticos.
> Nota: Para ver los formalismos concretos revisar las transparencias.

Se distinguen dos tipos de abstracciones:
- Abstracción a **nivel de datos** (Eg: TADs)
- Abstracción a **nivel de acciones** (Eg: verificación de corrección de algoritmos)

Los métodos formales son fundamentales para la **verificación formal** que, debido a su **alto coste**, es comúnmente omitida. Por norma general, se suele verificar con totalidad en ocasiones en las que **no se toleren fallos** (Eg: software médico).

A nivel de datos se espera la existencia de tipos con **propiedades específicas** que se pueden utilizar con total **desconocimiento de la implementación**.
\
De un TAD se esperan **propiedades** *documentadas*, **especificaciones**, *semántica* e **implementación**
\
Los TADs tienen una **función de abstracción** que determina qué dato interno representa a cada dato externo.

# TEMA 2: Especificación e implementación de tipos abstractos
> Sobre el documento: Tal vez falten datos o encuentre una estructura inconsistente en el siguiente tema. Esto se debe a una reestructuración del orden de los contenidos distinta a la presentada en las transparencias para favorecer una mejor comprensión.

## Función de abstracción
La **función de abstracción** cumple con las siguientes características.
> Con $f:A \to B$ siendo $A$ y $B$ conjuntos de partida y llegada respectivamente

- Puede ser **parcial**
    > $\exists a \in A \ | \quad f(a) \notin B$
- Puede ser **inyectiva**
    > $f(x) = f(y) \implies x = y$
- Puede ser **sobreyectiva**
    > $\forall a \in A \quad \exists f(a) \in B$
- Debe **conmutar los operadores**
    > Sea un operador $T$;
    > \
    > $f(T(x)) = T(f(x))$

## Especificación
La manipulación de un TAD debe únicamente **depender de la especificación** de tal forma que se mantenga su utilidad incluso si su desarrollador quisiera *cambiar su implementación*.
> Ejemplo de especificación:
> ```
> TAD Baraja
> - usa Carta
> - género baraja
> - operaciones
>   acción iniciarBaraja(salida baraja b)
>       { Pre: }
>       { Pos: inicia b como una baraja de cartas ordenadas }
>   acción barajear(entrada/salida baraja b)
>       { Pre: b está inicializada y tiene cartas }
>       { Pos: mueve aleatoriamente la posición de las cartas en b }
>   función cima(entrada baraja b) devuelve Carta
>       { Pre: b está inicializada y tiene cartas }
>       { Pos: devuelve la carta de la cima de b }
>  [ . . . ]
> ```
    
## Implementación
La implementación de un TAD cuenta con:
- **Representación**
- **Operadores**

> Eg: en orientación a objetos, por ejemplo, la representación del TAD puede corresponder a sus atributos y los operadores a sus métodos.

---

## Árboles
Es una estructura en fomra de grafo con **naturaleza jerárquica** y caracterizado por tener nodos con un antecesor (salvo la raíz).
\
Es la estructura adecuada para **relaciones de orden parcial**.

> Con respecto a la **definición**.
> \
> Distinguiremos una base:
> - Un árbol de 0 nodos es un árbol vacío o **nulo**
> - Un **nodo** es un árbol
> 
> Y una recurrencia:
> - Se conoce como **enraizar** a la construcción de un árbol a > partir de la asignación de un nodo como raíz
>
> > Nota: En las transparencias la información es distinta e innecesariamente más compleja.

> Con respecto a la **terminología**.
> - Un nodo es **padre** de otro si es su *primer ascendente*.
> - Un **camino** es la sucesión de nodos para llegar a un destino.
> - Un **nivel** es el número de avances hasta el nodo destino desde la raíz (0).
> - Un nodo **antecesor** es ascendente del nodo especificado.
> - Un nodo **descendiente** es el opuesto lógico al ascendente.
> - Un nodo **hoja** o **terminal** es aquel que no tiene descendencia
> - Un nodo **interior** es el antónimo lógico del nodo hoja.
> - La **profundidad** es el máximo nivel de un árbol.
> - El **grado** de un árbol corresponde al mayor grado de sus nodos.

## Árbol binario
Corresponde a un caso específico de árbol con restricciones adicionales:
\
Cada nodo tiene **grado 2** y descendencia distinguida en **rama derecha e izquierda**.
\
Por consiguiente, un árbol nulo es un árbol binario.
> Nota: Un árbol binario debe distinguir claramente si una de sus descendencias corresponde a la rama derecha o a la rama izquierda independientemente de si cuenta únicamente con una rama.

## Montículo
Un **montículo de máximos**, *max heap* en inglés, es un tipo de árbol binario. Es **casicompleto**, es decir, obtenido a partir de un árbol completo al que se le han **eliminado 0 o más hojas del último nivel comenzando por la derecha**.

> Eg: en la siguiente imagen, el nodo 7 no es un árbol casicompleto porque, aunque solo se hayan eliminado hojas del último nivel, no se han eliminado de la derecha. En cambio, los nodos 6 y 9 sí son árboles casicompletos porque, o bien se ha eliminado el nodo hoja desde la derecha como en el 9, o bien se han eliminado 0 nodos hoja.
>
> !["Imagen de árbol binario"](https://upload.wikimedia.org/wikipedia/commons/thumb/3/36/Binary_tree_%28oriented_digraph%29.png/250px-Binary_tree_%28oriented_digraph%29.png "Árbol binario en Wikipedia, la enciclopedia libre")

Cabe destacar que, en esta ocasión, si tiene sentido crear métodos para **insertar en un montículo** o **eliminar la raíz**.
> Nota: Para revisar la implementación específica revisar transparencias.

Como el montículo es casicompleto, es más rentable la **implementación estática** sobre la dinámica. 
\
De esta forma dada la implementación con un *array* $v$ de tamaño $n$, utilizando un índice $i$ se tiene que:
- Los hijos de un nodo están en $v$[$2i \pm 1$]
- El padre de un nodo está en $v$[$\lfloor \frac{i-1}{2} \rfloor$]

La complejidad de sus operaciones es fundamentalmente **logarítmica** ($O \log_{2}(n)$).
\
La implementación dinámica lo empeora por la complejidad de las operaciones para volver al padre del nodo.