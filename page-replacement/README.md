# Sustitución de páginas

El estudiante **arma la tabla de marcos** como en el ejercicio en papel: una
columna por referencia, una fila por marco, y abajo si hubo fallo, qué página
salió y —cuando importa— qué se escribió en disco. En cada referencia toca el
marco donde queda la página, y el recurso le dice si acertó y, cuando no, le
muestra la respuesta correcta y por qué es esa. También se puede mirar todo ya
resuelto, paso a paso.

Se abre haciendo doble clic en `index.html`. No necesita internet ni instalar
nada.

Sale de la guía de ejercicios de memoria de la cátedra (2016): los ejercicios
**8, 9 y 10**, más un ejemplo de la anomalía de Belady. Da por sabido qué es una
página, un marco y la tabla de páginas; lo que agrega es qué pasa cuando la página
no está y no hay lugar.

Este archivo es la documentación del recurso: qué enseña, cómo editarlo y qué no
se puede tocar. Si vas a modificar `index.html`, leelo antes.

**No está enlazado desde la portada.**

---

## Los ocho ejemplos

Son **126 pasos** en modo Ver, contando las variantes, y **116 referencias** para
contestar en modo Resolver. La escalera va agrupada en cuatro tramos.

| # | Tramo | Ejemplo | Qué enseña | Sale de | Pasos |
|---|---|---|---|---|---|
| 1 | Los cuatro algoritmos | FIFO | Cómo se llena la tabla, y sacar la que entró primero | Ej. 8 | 15 |
| 2 | Los cuatro algoritmos | Óptimo | El mínimo posible, y por qué no se puede implementar | Ej. 8 | 15 |
| 3 | Los cuatro algoritmos | LRU | Mirar el pasado para adivinar el futuro, y que a veces falla | Ej. 8 | 15 |
| 4 | Los cuatro algoritmos | Clock | El bit de uso y el puntero; la tabla comparativa de los cuatro | Ej. 8 | 15 |
| 5 | Más marcos | Más marcos, más fallos | La anomalía de Belady con FIFO | — | 13 + 13 |
| 6 | Con escrituras | LRU con páginas modificadas | Direcciones en vez de páginas, el bit de modificado, la escritura a disco | Ej. 9 | 8 |
| 7 | Con escrituras | Clock modificado | Preferir sacar páginas limpias; la comparación con LRU (9b) | Ej. 9 | 8 |
| 8 | TLB | Cuándo sirve la TLB | Contar accesos a TLB, memoria y disco, y la localidad (10b) | Ej. 10 | 14 + 10 |

Los cuatro primeros **comparten enunciado** —la misma secuencia y los mismos
cuatro marcos—, y lo mismo el 6 y el 7: la diferencia entre las dos tablas es la
lección. Los resultados son los de la guía: **FIFO 7, Óptimo 6, LRU 8 y Clock 7
fallos**; en el ejercicio 9, **LRU 5 fallos y 2 escrituras contra Clock modificado
4 y 1**; en el 10, **P1 13 accesos a la TLB, 18 a memoria y 5 a disco, y P2 9, 18
y 9**.

Cada ejemplo termina con una **placa de cierre** («Para llevarse») en el campo
`closing`, y los ejemplos 4, 5, 7 y 8 además muestran una tabla comparativa en el
último paso (`compare`). Cada título de panel tiene su globito, en `PANEL_TIPS`.

Los controles son **Primero · Anterior · Siguiente · Último · Reproducir**, con
las flechas del teclado y `Inicio` / `Fin`, como en el resto de la familia.
Reproducir sólo existe en modo Ver.

---

## Dos modos sobre los mismos datos

Arriba a la derecha, **Modo · Resolver / Ver**, en el mismo lugar que en
`cpu-scheduling`. Arranca en Resolver.

- **Resolver.** Sólo se contesta la columna de la referencia actual, la que tiene
  la raya debajo del número. En sus casilleros se ve, en gris, cómo estaban los
  marcos al llegar la referencia; al pasar el mouse sobre un marco aparece la
  página que entraría ahí. **Se contesta tocando el marco donde queda la página**:
  el que ya la tiene si es un acierto, o el que la recibe si es un fallo. Un solo
  toque dice las dos cosas —si hubo fallo y a quién se sacó—, igual que en papel.
  También sirven las teclas `1` a `4`, una por fila de marco.

  - En el 6 y el 7 aparece arriba del tablero el botón **«Dirección inválida»**,
    **en todas las columnas**, para que su presencia no delate en cuál hace falta.
  - En el 8 no se toca un marco: se elige entre **«Acierto en la TLB»**, **«Fallo de
    TLB, la página está en memoria»** y **«Fallo de página»** (teclas `1` a `3`).

  Al contestar, la columna se revela con la respuesta correcta —se haya acertado o
  no— y se abre la siguiente. La narración dice **«Bien.»** o qué estuvo mal, y
  después siempre el razonamiento completo de esa referencia. La fila **Tu
  respuesta** deja un ✓ o un ✗ en cada columna, y abajo a la derecha se lleva la
  cuenta de aciertos. Con las flechas se puede volver a mirar columnas ya
  contestadas; para adelante no se pasa de la que falta contestar.

  **No se adelanta nada.** Los contadores, la fila de fallos, la de «Sale», los bits
  y el panel de estado muestran siempre lo que había **antes** de la referencia
  abierta, que es el dato con el que se decide —como la cola de listos de
  `cpu-scheduling`—.

- **Ver.** Un paso es una referencia, con el tablero revelado hasta ahí y la
  narración explicando la decisión con sus números («LRU saca la que se usó hace
  más tiempo: la 2, usada por última vez en la referencia 6»).

**Las respuestas se guardan** en el navegador (`localStorage`, clave
`ssoo-recursos:page-replacement:v1`), por ejemplo y por variante, para que cambiar
de ejemplo o recargar no las pierda. Es una comodidad y nada más: si el navegador
no deja guardar —pasa con algunos al abrir el archivo con doble clic—, el recurso
anda igual y sólo se olvida al recargar. Cuando un ejemplo está resuelto entero
(todas sus variantes), su botón de la escalera muestra un ✓. **«Empezar de
nuevo»** borra las respuestas del ejemplo y la variante que estás mirando.

### La escalera no se mueve

Como en `deadlock`, los botones muestran sólo el número y el título completo va en
la narración. El ✓ de resuelto **tiene su lugar reservado siempre**, invisible
mientras el ejemplo no está resuelto: si apareciera de la nada, el botón crecería y
correría a todos los que vienen después. Medido: en todos los ejemplos, en los dos
modos y antes y después de resolverlos, la escalera tiene **una sola disposición**.

### Pistas

En los ejemplos donde el algoritmo decide con un dato que en papel se lleva
aparte —el orden de llegada en FIFO, el próximo uso en Óptimo, el último uso en
LRU, el orden de la TLB—, el panel de estado tiene un interruptor **«Pistas ·
Mostrar / Ocultar»**, sólo en Resolver. Ocultarlo deja los contadores y las
páginas, y saca ese dato: hay que llevarlo de memoria. En Clock y Clock
modificado no hay interruptor, porque los bits y el puntero **se escriben en la
tabla** como en papel: no son una pista, son parte del tablero.

---

## El chasis se comparte; el canvas se deriva

**No hay interruptor de granularidad.** La unidad es la misma en los ocho
ejemplos —**una referencia a memoria**— y no se descompone en nada más chico que
el estudiante tenga que ver. Por eso tampoco hay `stepUnitNote`.

| # | Lo que muta y hay que mirar | Canvas |
|---|---|---|
| 1 a 3 | qué página hay en cada marco, y el orden de llegada / el próximo uso / el último uso | Marcos + Estado |
| 4 | lo mismo, más el bit de uso y el puntero, que van en la tabla | Marcos + Estado |
| 5 | lo mismo que en 1, con 3 o 4 filas según la variante | Marcos + Estado |
| 6 | los marcos, el bit de modificado y qué se escribe en disco | Marcos (con fila «A disco») + Estado |
| 7 | lo mismo, más el bit de uso y el puntero | Marcos (con fila «A disco») + Estado |
| 8 | los marcos, las entradas de la TLB y los tres contadores de accesos | Marcos y TLB + Estado |

Se revisó que el canvas no estuviera heredado: en los ocho, lo que muta es lo que
hay en cada marco (el tablero) y el dato con el que decide el algoritmo (el estado),
así que los dos paneles se ganan su lugar en todos. **Lo que se deriva por ejemplo
son las filas del tablero**: la fila «A disco» existe sólo donde hay bit de
modificado; la fila de direcciones y la columna «Inicio», sólo donde el enunciado
las trae; las filas de la TLB y «Resultado», sólo en el 8. Y el panel de estado del
8 no lista los marcos uno por uno, como los otros: muestra **dos órdenes** —los
marcos del uso más viejo al más nuevo, y la TLB de la entrada más vieja a la más
nueva—, porque eso es exactamente lo que miran LRU y FIFO, y con ocho filas de
lista no entraba a 1280×720.

---

## Los paneles

| Panel | Muestra | Lo usan |
|---|---|---|
| Marcos | la tabla: referencia, página (y dirección), una fila por marco, Fallo, Sale, A disco, Tu respuesta | 1 a 7 |
| Marcos y TLB | la misma tabla con cuatro filas más para la TLB y una fila Resultado | 8 |
| Estado | contadores y, por marco, el dato con el que decide el algoritmo, después de la última columna resuelta | todos |
| Narración | qué pasó en la referencia y por qué, o la presentación del ejemplo | todos |

La referencia de colores y símbolos va **al costado de la tabla** cuando hay lugar,
y abajo cuando no. Se arma con lo que hay en ese ejemplo: el puntero sólo aparece
en Clock, «A disco» sólo con bit de modificado, y en el 8 la referencia **dice
cuánto cuesta cada caso** con los números de `costs`.

---

## Cambiar un texto

Todos los textos que ve un estudiante están en el bloque `<script id="data">`,
arriba de todo del archivo. **No hay ni un texto visible escrito en el motor ni en
el dibujo.**

1. Abrí `index.html` en cualquier editor.
2. Buscá el texto tal como aparece en pantalla. Va a estar entre comillas.
3. Cambialo, guardá y recargá la página.

Hay dos clases de texto:

- **Los de cada ejemplo**, adentro de `EXAMPLES`: `title`, `subtitle`, `intro` (la
  presentación, que es el primer paso), `notes` (una aclaración extra para una
  referencia, por número), `closing` y `compare`.
- **La narración de cada referencia no está escrita a mano**: se arma con las
  plantillas de `UI_TEXT.narr`, con los números que da la simulación. Por eso
  cambiar «LRU saca la que se usó hace más tiempo» se hace **una vez** y cambia en
  todas las referencias de todos los ejemplos LRU. Las devoluciones de Resolver
  están en `UI_TEXT.feedback`.

Dentro de los textos hay tres marcas:

- `[[fallo:fallo de página]]` — la palabra sale con un globito. Antes de los dos
  puntos va cuál de las explicaciones de `TOOLTIPS` usa.
- `*así*` — sale en negrita.
- `{fallos_3}`, `{page}`, `{victim}` — valores que el recurso completa solo. En
  las frases de cierre y en las tablas comparativas sirven `{fallos_N}`,
  `{escrituras_N}`, `{tlb_N_V}`, `{memoria_N_V}` y `{disco_N_V}` (N es el número
  del ejemplo y V la variante, desde 1). **No conviene reemplazarlos por el número
  escrito a mano**: son lo que garantiza que la tabla diga lo que dio la
  simulación.

---

## Agregar o cambiar un ejemplo

Un ejemplo es un objeto en `EXAMPLES`. Lo mínimo:

```js
{
  number: 9,
  group: "cuatro",
  algorithm: "lru",
  title: "…", short: "…", adds: "Agrega: …", subtitle: "…",
  stepUnit: "Un paso = una referencia a memoria",
  canvas: { columns: "minmax(0, 1fr) minmax(290px, 0.4fr)", panels: ["board", "state"] },
  hints: true,
  frames: ["0", "1", "2"],
  references: [7, 0, 1, 2, 0, 3],
  expect: { faults: 6, victims: [7, 0, 1] },
  intro: "…",
  closing: "…"
}
```

- `algorithm` es `fifo`, `optimal`, `lru`, `clock`, `clockModified` o `tlb`.
- `frames` son los nombres de los marcos, en el orden de las filas (y en el orden
  en que los recorre el puntero).
- `references` son números de página, o —como en el 6 y el 7— objetos
  `{ address, mode, page, offset }` con `pageSize`; el recurso **recalcula la página
  y el desplazamiento** de cada dirección y avisa si no coinciden con lo escrito.
- `initial` (opcional) declara las páginas ya cargadas, con sus bits y el instante
  de su última referencia, y adónde apunta el puntero.
- `bits` (opcional) dice qué bits se escriben en la tabla: `["u"]`, `["m"]` o
  `["u", "m"]`.
- `processPages` e `invalidOption` hacen que una página fuera del proceso sea un
  error y ofrecen el botón «Dirección inválida».
- `expect` es **lo que el ejemplo tiene que dar**: fallos, y opcionalmente
  escrituras, víctimas en orden y accesos. El recurso simula el algoritmo y avisa
  por consola si no da eso.
- `variants` reemplaza cualquiera de los campos por variante, como en el 5 y el 8.

---

## Lo que el recurso verifica solo al abrirse

El motor **simula** los algoritmos —son deterministas— y compara contra lo que
declaran los datos. Avisa por la consola del navegador:

- si la cantidad de fallos, de escrituras a disco o de accesos (TLB, memoria,
  disco) no es la declarada en `expect`;
- si las páginas que salen, en orden, no son las declaradas;
- si una dirección no da la página o el desplazamiento que dice el dato;
- en Clock, si una página entra a un marco libre que no es el del puntero;
- si un estado inicial usa un marco que no existe;
- si un ejemplo no tiene `closing`, `stepUnit`, `intro` o marcos, o usa un panel
  sin nombre o sin globito;
- si queda un `{dato}` sin completar, una marca sin cerrar, un globito que no
  existe, o un globito escrito que nadie usa;
- si los grupos de la escalera quedan cortados.

Si se agrega una regla nueva, conviene romper los datos a propósito una vez para
confirmar que la consola la reporta y que la página no se cae.

---

## Decisiones que hay que confirmar con la cátedra

1. **La dirección 172100 del ejercicio 9.** Cae en la página 21 y el proceso
   (159 KiB en páginas de 8 KiB) tiene 20 páginas, de la 0 a la 19. El recurso lo
   trata como **dirección inválida: no es un fallo de página, el sistema operativo
   finaliza el proceso y la última referencia (100, lectura) nunca se ejecuta**.
   Su columna se ve tachada y gris. Si la cátedra resuelve el ejercicio de otra
   forma —por ejemplo, ignorando la referencia y siguiendo—, es un cambio de datos
   (`processPages`) y de la plantilla `narr.invalid`.
2. **Cómo se cuentan los accesos en el ejercicio 10.** Acierto en la TLB: 1 acceso
   a la TLB y 1 a memoria. Fallo de TLB con la página en memoria: 1 a la TLB y 2 a
   memoria (la tabla y el dato). Fallo de página: 1 a la TLB, 2 a memoria y 1 a
   disco. Con eso, P1 da 13 / 18 / 5 y P2 da 9 / 18 / 9. Está en `costs` y la
   referencia del tablero lo dice; si la cátedra cuenta distinto —por ejemplo, un
   segundo acceso a la TLB al reintentar después del fallo—, se cambia ahí y en
   `expect`. Cuando una página sale de memoria, su entrada en la TLB se borra; con
   estos datos no cambia ningún número, porque la que sale de la TLB siempre es
   la misma que sale de memoria.
3. **Convenciones de Clock.** El bit de uso se pone en 1 al cargar y al
   referenciar; en un acierto el puntero no se mueve; en un fallo avanza desde
   donde está, pasando a 0 los unos, y queda en el marco siguiente al reemplazado;
   cargar en un marco libre también lo avanza. En el ejercicio 8 arranca en el
   marco 0.
4. **Clock modificado** se hace en vueltas: primero (U = 0, M = 0) sin tocar nada;
   después (U = 0, M = 1) pasando a 0 el bit de uso de cada marco que deja atrás;
   y si tampoco, se repite. En el ejercicio 9 la referencia 2 necesita **tres
   vueltas**.
5. **Con marcos libres, la página va al primero libre** (al del puntero, en Clock).
   En Resolver, tocar otro marco libre se cuenta como error y la explicación lo
   dice.
6. **Empates en Óptimo** (dos páginas que no vuelven a usarse): sale la del marco
   de más arriba. Con los datos de la guía no hay empates.
7. **El ejemplo 5 no está en la guía.** Es la secuencia clásica de la anomalía de
   Belady (1 2 3 4 1 2 5 1 2 3 4 5), con FIFO: 9 fallos con 3 marcos y 10 con 4.
8. **En el ejercicio 9, LRU decide con los instantes del enunciado** (28, 3 y 15)
   y toda referencia nueva cuenta como posterior a todos ellos. La guía dice que
   no hace falta calcular los instantes; el recurso no los inventa: las nuevas se
   nombran por su número de referencia.

### Decisiones de color y tipografía

**El recurso no estrena tipografía**: usa la pila del sistema, como el resto de la
familia. La paleta de la cátedra no nombra ningún rol de este tema —no hay estados
de proceso ni diagrama de Gantt en pantalla—, así que lo que sigue lo eligió este
recurso:

| Rol | Tono | Por qué |
|---|---|---|
| Marcos, páginas, bits, puntero | neutros (tinta y grises) | no nombran nada que necesite un color |
| Fallo de página y errores | rojo `#c0392f`, siempre con texto («F», «inválida», ✗) | el fallo bloquea al proceso, y es el rojo de `BLOCKED`, que acá no aparece en ningún otro lado |
| «Cambió en esta referencia» | anillo grafito, por dentro del casillero | regla del repositorio: el color nombra una cosa, la tinta dice que cambió |
| Escritura a disco | sin color: la fila «A disco» lo dice | un tono más no agregaba nada que la fila no diga |
| Algoritmos | ninguno | no se gastan tonos en distinguir algoritmos |

**El anillo va por dentro del casillero** (`inset`), no por fuera como en
`deadlock`: la tabla es densa y con el anillo de afuera hacía falta separar más las
filas de lo que entra a 1280×720. Por dentro, dos casilleros marcados nunca se
tocan, con cualquier separación.

---

## Verificación antes de publicar un cambio

1. Abrirlo con doble clic, sin servidor y sin internet. Funciona igual.
2. La consola del navegador limpia, en los ocho ejemplos, las cuatro variantes y
   los dos modos.
3. Resolver cada ejemplo entero, una vez acertando todo y otra equivocándose: la
   columna se revela con la respuesta correcta y la cuenta de aciertos da.
4. Recargar: las respuestas siguen ahí. Y con el almacenamiento bloqueado, anda
   igual.
5. En Ver, recorrer cada ejemplo entero para adelante y para atrás: cada paso se
   ve igual en los dos sentidos.
6. A 1280×720 entra todo, sin scroll de página y sin que ningún panel scrollee,
   en los dos modos. Los más justos son el 5 con 4 marcos y el 8 con P2, en su
   último paso.
7. A 390 px de ancho se lee en una columna; la tabla scrollea adentro de su panel
   y la página no se va para el costado.
8. Teclado: flechas, `Inicio`, `Fin`, `1` a `4` para contestar, `Tab` con el foco
   siempre visible.
9. Contraste de todo el texto contra su fondo real, calculado, con piso de 4,5:1.

Lo medido en la construcción: **126 pasos** de Ver recorridos a 1280×720 sin un
desborde y con la consola limpia; las **116 referencias** contestadas en Resolver,
con aciertos y con errores, sin desbordes; **126 comparaciones** de ida y vuelta,
todas idénticas; **136 tableros** a 390 px sin scroll horizontal de página;
**16 combinaciones** de texto y fondo, la peor en 4,58:1; **59 paradas de `Tab`**
con contorno visible; la escalera con una sola disposición en todos los estados;
y ningún pedido de red, con la red cortada y con «reducir movimiento».

---

## Lo que falta

**Toda la narración la escribió un agente y no la revisó nadie de la cátedra.** Son
las ocho presentaciones, las notas, las ocho frases de cierre, las plantillas de
narración y de devolución (`UI_TEXT.narr` y `UI_TEXT.feedback`), nueve globitos de
término y tres de panel. Lo que sí sale palabra por palabra de la guía son los
enunciados: las secuencias, los tamaños, el estado inicial del ejercicio 9 y las
direcciones. Es lo primero que hay que leer antes de mandarles el link a los
estudiantes.
