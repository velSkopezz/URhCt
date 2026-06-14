# Redes de Computadores: Enrutamiento

En este tema sólo importa el algoritmo de Dijkstra, la tabla de distancias y la tabla de encaminamiento.

## Intradominio: Estado de enlace

Se necesitan dos condiciones, pues se va a utilizar el algoritmo de Dijkstra:
- Cada nodo conoce la topología completa.
- Cada nodo conoce el estado de los enlaces.

Un nodo creador envía un paquete de estado de enlace (LSP de *Link State Packet*). El receptor comprueba si la nueva copia es más nueva que la que ya tuviera y, en tal caso, la mantiene y reenvía a todas sus interfaces excepto de la que procedía dicha copia.

Este envío responde a tiempos periódicos o a cambios en la topología de red.

En OSPF se realiza el cálculo del coste de acuerdo con la fórmula $\text{coste} = max(\ int(\frac{10^{8}}{\text{velocidad}}), 1\ )$.

## Intradominio: Encaminamiento por vector de distancias

Cada nodo guarda información sobre su distancia estimada respecto a otros nodos. Esta información la difunde a sus nodos adyacentes de forma periódica.

Si no se tiene enlace desde un nodo ni ninguno de los nodos conocidos se supone infinito su coste hasta tener acceso.

Un protocolo utilizado es RIP.

## Interdominio: *Border Gateway Protocol*

El protocolo BGP pretende conectar diferentes sistemas autónomos y difundir la información dentro del mismo sistema autónomo.

Hace uso de un número identificador de sistemas autónomos llamado ASN.

# Observaciones del autor

Con todo el descaro lo digo, no he puesto casi nada de este tema, pero si las transparencias son 20 diapositivas menos que la media es por algo. Este tema es fundamentalmente práctico y, en realidad, tu única responsabilidad es ponerte videos de YouTube para entenderlo y ser autodidacta una vez más en la universidad. Los profesores de universidad disfrutan mucho de culpar a los institutos de traer a los alumnos sin base y probablemente nunca descubran que con lo mal que explican y estructuran las clases es imposible que nadie entienda lo explicado en 50 minutos. Ellos sabrán, son ellos a los que les falta un máster sobre enseñar y los que suspenden al 50% del alumnado por año.

Aquí la teoría no importa absolutamente nada. No se va a preguntar ni en el test. El algoritmo de Dijkstra, la tabla de distancias y la de encaminamiento es lo único que importa, lo demás es totalmente omisible. Es más, en el pasado, el ejercicio más rentable era hacer el algoritmo de Dijkstra de un grafo endemoniado pues era relativamente rápido y tenía un valor propio de un ejercicio del tiempo que toma. No obstante, desde que el test vale mucho más, ha decidido ponerlo en al menos una ocasión como una pregunta práctica -si, de test: es una pregunta que cuenta como si fuera un test pero cuesta como si fuera un ejercicio-.
\
No te preocupes, solo bromeaba. No lo ha puesto como una pregunta de test: lo ha puesto como tres preguntas de test diferenciadas (recordatorio de que no es test, tienes que rellenar tablas vacías) en las que debes sacar las anteriores correctamente para poder aspirar a puntuar en las siguientes por muy bien que estén. Pero no te preocupes, que su santísima magnanimidad y, por encima, todobondadoso espíritu tiene el descaro de avisarte durante el tiempo de examen del terrible diseño que ha elegido.

Otro detalle: utiliza las tablas de los ejercicios hechos en clase. En el examen te va a poner sus tablas con huecos por lo que, si tenías tu forma cómoda de disponer la información ya no la tienes. Una vez más el examen demuestra ser un ejercicio de cómputo humano a contrarreloj y no un examen de evaluación.
