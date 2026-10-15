# Paginación y segmentación

Cómo se traduce una dirección **paso a paso**: la dirección partida en campos de
bits, la tabla que se consulta y la memoria física adonde llega. Paginación,
segmentación con sus controles de límite y permisos, la fragmentación interna y
externa, la segmentación paginada, la memoria virtual con el bit de presencia,
la atención completa de un fallo de página, y las tablas grandes: plana,
jerárquica e invertida.

Está armado sobre la **guía de ejercicios de Memoria (2016)**: los ejercicios 1,
2, 3, 4, 5, 6, 7 y 11 están adentro, con sus números, y el recurso los resuelve
mostrando cada cuenta. Los ejercicios 8, 9 y 10 —sustitución de páginas y TLB—
están en el recurso hermano, `page-replacement`.

Se abre haciendo doble clic en `index.html`. No necesita internet ni instalar
nada.

Es de la misma familia que los otros recursos y da por sabido lo de **Procesos e
hilos** y **Planificación de procesos**: los estados de proceso y sus colores, el
bloqueo por E/S y el planificador. El ejemplo 12 los usa.

Este archivo es la documentación del recurso: qué enseña, cómo editarlo y qué no
se puede tocar. Si vas a modificar `index.html`, leelo antes.

**Todavía no está enlazado desde la portada**: figura como «próximamente».

---

## Los quince ejemplos

Son **135 pasos** en total, contando las cuatro variantes del 12. La escalera va
agrupada en cinco tramos.

| # | Tramo | Ejemplo | Qué enseña | De la guía | Pasos |
|---|---|---|---|---|---|
| 1 | Paginación | La dirección partida en dos | Página y desplazamiento, y cuántos bits lleva cada parte | Ej. 1 | 7 |
| 2 | Paginación | De página a marco | Traducir con la tabla de páginas | — | 8 |
| 3 | Paginación | Lo que entra y lo que sobra | El programa más grande, fragmentación interna y externa | Ej. 2 | 7 |
| 4 | Segmentación | Base y límite | Traducir con la tabla de segmentos, y el control del límite | Ej. 3 | 7 |
| 5 | Segmentación | Permisos | Dos controles por acceso: límite y permiso | Ej. 4 | 10 |
| 6 | Segmentación | Los huecos | Fragmentación externa y compactación | Ej. 11 c | 9 |
| 7 | Segmentación | La tabla al revés | Reconstruir la tabla desde traducciones conocidas | Ej. 11 | 9 |
| 8 | Combinada | Segmentación paginada | Una tabla de páginas por segmento | — | 8 |
| 9 | Memoria virtual | Más grande que la memoria | La lógica ya no depende de la física | Ej. 5 y 6 a | 5 |
| 10 | Memoria virtual | Una tabla por proceso | Formato de la fila, tabla de marcos libres, tablas desde el mapa | Ej. 6 b, 6 c y 8 b | 7 |
| 11 | Memoria virtual | La página que no está | Bit de presencia y fallo de página | Ej. 7 | 9 |
| 12 | Memoria virtual | Atender un fallo de página | Todo lo que pasa desde el fallo hasta repetir la instrucción | — | 9 + 8 + 7 + 4 |
| 13 | Tablas grandes | La tabla que no entra | Cuánto ocupa una tabla plana y cuánto está vacío | — | 4 |
| 14 | Tablas grandes | Paginación jerárquica | Lo que ahorra y lo que cuesta | — | 8 |
| 15 | Tablas grandes | Tabla invertida | Una fila por marco, buscar con un hash | — | 9 |

El 12 tiene cuatro variantes, que se eligen en el renglón de abajo de la escalera:
**hay un marco libre**, **víctima sin modificar**, **víctima modificada** (dos E/S)
y **dirección inválida** (no es un fallo de página: el proceso termina).

Cada ejemplo termina con una **placa de cierre** (`closing`), y cada título de
panel tiene su globito (`PANEL_TIPS`). Los controles y las teclas son los de toda
la familia: **Primero · Anterior · Siguiente · Último · Reproducir**, las flechas,
`Inicio` y `Fin`.

### Las preguntas

Veinticuatro pasos traen una pregunta antes de mostrar la respuesta: el paso
pregunta, y el siguiente resuelve. Aparece a la derecha de la narración, con tres
o cuatro opciones. Al elegir una, la pregunta muestra **por qué esa opción está
bien o mal** y, si está mal, cuál era y por qué. Cada opción incorrecta es un error
típico con su explicación, no un número al azar: «sumarle el marco a la
dirección», «quedarse con el comienzo del marco», «confundir los bits de la física
con los de la lógica».

**Nunca bloquea**: se puede seguir con «Siguiente» sin contestar, y el paso que
viene muestra la respuesta igual.

**Las respuestas se guardan en el navegador** (`localStorage`, clave
`ssoo-recursos:memory-translation:v1`), así que cambiar de ejemplo o recargar no
las borra. Es una comodidad y nada más: si el navegador no deja guardar —pasa al
abrirlo desde el disco en algunos navegadores—, todo funciona igual y sólo se
olvidan al recargar. «Probar otra» borra la respuesta de esa pregunta.

---

## Lo que el recurso hace y lo que no

**Las traducciones no están escritas a mano: las hace el recurso.** Los ejemplos
2, 4, 5, 8, 11 y 15 declaran su máquina —el tamaño de página y la tabla, o la
tabla de segmentos, o la tabla invertida— y cada paso declara sólo **qué
dirección** y **hasta dónde** se tradujo (`phase`). Los bits de cada campo, la
fila que se resalta, el marco, la física, los controles y el veredicto salen de
una cuenta. Por eso **el panel no puede decir algo distinto de la narración**: la
narración usa esos mismos valores (`{pagina}`, `{marco}`, `{fisica}`).

Cada paso que cierra una traducción trae el resultado esperado en `expect`, y el
recurso **verifica al abrir** que la cuenta dé eso. Cuando se armó, esa
verificación encontró un error en los datos: en el ejercicio 7 la dirección 0 va a
la física **3072** (la página 0 está en el marco 3), no a la 0.

Los otros ejemplos (1, 3, 6, 7, 9, 10, 12, 13 y 14) declaran lo que muestra cada
panel, porque lo que se ve son cuentas, un mapa de memoria que cambia o una
secuencia de acciones, y no una traducción. Los campos de bits que declaran se
comprueban igual: si una línea dice que la dirección vale 4077h, los campos
pegados tienen que dar 4077h.

---

## El chasis se comparte; el canvas se deriva

Está en `CLAUDE.md` porque vale para todo el repositorio; acá está la derivación
de cada ejemplo.

**No hay interruptor de granularidad.** Las unidades no anidan: una cuenta no se
descompone en partes de una traducción, ni una acción del sistema operativo en
pasos de una búsqueda. Cada ejemplo declara su `stepUnit`, que se ve siempre, y el
que la cambia trae `stepUnitNote` y lo dice una vez.

| # | Unidad del paso | Lo que muta y hay que mirar | Canvas |
|---|---|---|---|
| 1 | una cuenta | cuántos bits tiene cada campo | Dirección + Cuentas |
| 2 | una parte de la traducción | los campos, la fila de la tabla, el marco | Dirección + Tabla de páginas + Memoria física |
| 3 | una cuenta | los marcos ocupados y lo que sobra en el último | Cuentas + Memoria física |
| 4 | una parte de la traducción | el control del límite y adónde cae la física | Dirección + Tabla de segmentos + Memoria física |
| 5 | una parte de la traducción | los dos controles y el veredicto | Dirección + Tabla de segmentos |
| 6 | un cambio en la memoria | los huecos, y las bases al compactar | Memoria física + Segmentos en memoria |
| 7 | una pista | la tabla que se completa | Pistas + Dirección + Tabla de segmentos + Memoria física |
| 8 | una parte de la traducción | las dos tablas que se consultan | Dirección + Tabla de segmentos + Tablas de páginas + Memoria física |
| 9 | una cuenta | los bits de la lógica y de la física | Dirección + Cuentas |
| 10 | una cuenta o una tabla | las tres tablas que se llenan | Fila de la tabla + Cuentas + Tablas de páginas + Memoria física |
| 11 | una parte de la traducción | la presencia de cada fila | Dirección + Tabla de páginas + Memoria física |
| 12 | una acción del hardware o del SO | el estado del proceso, la CPU, el disco, la tabla | Quién hace qué + Memoria física + Tabla de páginas + La atención, en orden |
| 13 | una cuenta | cuánto de la tabla está vacío | Dirección + Cuentas + La tabla entera |
| 14 | una cuenta o un acceso a memoria | las internas que existen, y el recorrido | Dirección + Cuentas + Tabla externa + Tabla interna |
| 15 | una parte de la búsqueda | el hash y la cadena que se recorre | Dirección + Tabla de hash + Tabla invertida |

Decisiones de canvas que conviene entender antes de cambiarlas:

- **El 5 no tiene memoria física.** Lo que enseña son los controles, y tres de las
  cuatro escrituras no llegan a la memoria. Un mapa ahí sería peso muerto.
- **El 6 no tiene panel de dirección.** No se traduce nada: lo que muta es el mapa.
  La tabla de «Segmentos en memoria» sale del mapa, no está escrita aparte, y
  marca las filas cuya base cambió.
- **En el 12 la memoria va abajo de «Quién hace qué» y la secuencia ocupa su
  propia columna.** La secuencia llega a ocho renglones en la variante de la
  víctima modificada, y es lo que el estudiante se lleva: es la respuesta a
  «¿qué pasa en un fallo de página?».
- **En el 13 y el 14 la tabla se dibuja como una grilla de 32 × 32.** Cada
  cuadradito es una página de tabla (en el 13) o una fila de la externa (en el
  14): es la misma imagen, y por eso los tres cuadraditos rellenos están en el
  mismo lugar en los dos ejemplos.
- **En el 15 no hay memoria física.** La tabla invertida *es* el mapa de la
  memoria: la fila 5 dice qué hay en el marco 5. Dibujar los marcos aparte sería
  dibujar lo mismo dos veces.

---

## Los paneles

| Panel | Muestra | Lo usan |
|---|---|---|
| Dirección | la lógica y la física, partidas en campos de bits, con los controles y el veredicto | 1, 2, 4, 5, 7, 8, 9, 11, 13, 14, 15 |
| Fila de la tabla | el formato de una fila: marco y bits de control | 10 |
| Cuentas | las cuentas en orden, la del paso marcada | 1, 3, 9, 10, 13, 14 |
| Tabla de páginas | una fila por página, con presencia y modificado cuando hacen falta | 2, 11, 12 |
| Tablas de páginas | varias tablas lado a lado | 8, 10 |
| Tabla de segmentos | base, largo y permisos | 4, 5, 7, 8 |
| Segmentos en memoria | lo que está cargado, sacado del mapa | 6 |
| Memoria física | marcos en grilla, o una tira proporcional de direcciones | 2, 3, 4, 6, 7, 8, 10, 11, 12 |
| Pistas | las pistas del enunciado, marcadas al usarse | 7 |
| Quién hace qué | el estado del proceso, quién tiene la CPU, qué hace el disco | 12 |
| La atención, en orden | lo que hizo el sistema operativo, un renglón por paso | 12 |
| La tabla entera / Tabla externa | la grilla de 1024 cuadraditos | 13, 14 |
| Tabla interna | la interna que se está recorriendo | 14 |
| Tabla invertida / Tabla de hash | las filas por marco y el comienzo de cada cadena | 15 |

### Cómo se lee una dirección

Cada campo es una fila de casilleros, uno por bit, con su color arriba y debajo
el nombre, la cantidad de bits y el valor. A la derecha, la dirección entera.
Cuando un campo todavía no se calculó, los casilleros están vacíos: así la
pregunta no se contesta sola. En las direcciones hexadecimales los bits van
agrupados de a cuatro desde la derecha, para que cada grupo sea una cifra.

En la segmentación de los ejemplos 4 y 15 la dirección se da como par —(2, 500),
(A, 1, 300)— y no como bits: los campos muestran el número y no casilleros.

### Los controles

Los controles de límite y de permiso se escriben como renglones con `✓` o `✗`. El
del límite va siempre primero. Si falla, el de permiso no aparece: el acceso ya
se frenó.

---

## Cambiar un texto

Todos los textos que ve un estudiante están en el bloque `<script id="data">`,
arriba de todo del archivo. **No hay ni un texto visible escrito en el motor ni en
el dibujo.**

1. Abrí `index.html` en cualquier editor.
2. Buscá el texto tal como aparece en pantalla.
3. Cambialo, guardá y recargá.

Dentro de los textos hay tres marcas:

- `[[fallo:fallo de página]]` — sale con un globito. Antes de los dos puntos, cuál
  de las explicaciones de `TOOLTIPS` usa; después, lo que se lee.
- `*así*` — sale en negrita.
- `{fisica}`, `{marco}`, `{desp}` — valores que el recurso completa con la cuenta.
  **No los reemplaces por el número escrito a mano**: son lo que garantiza que la
  narración diga lo que muestra el panel. Si escribís uno que el recurso no sabe
  completar, la consola lo avisa al abrir.

Las claves disponibles dependen de la máquina del ejemplo:

| Máquina | Ejemplos | Claves |
|---|---|---|
| Paginación | 2, 11 | `{direccion}`, `{pagina}`, `{desp}`, `{marco}`, `{fisica}` |
| Segmentación | 4, 5 | `{direccion}`, `{segmento}`, `{desp}`, `{base}`, `{limite}`, `{fisica}`, `{acceso}`, `{permiso}` |
| Segmentación paginada | 8 | `{direccion}`, `{segmento}`, `{pagina}`, `{desp}`, `{contenido}`, `{paginas}`, `{marco}`, `{fisica}` |
| Invertida | 15 | `{proceso}`, `{numero}`, `{pagina}`, `{desp}`, `{hash}`, `{primero}`, `{sonda}`, `{siguiente}`, `{marco}`, `{fisica}` |

## Agregar o cambiar una pregunta

Una pregunta es un campo `ask` en un paso:

```js
ask: {
  question: "¿A qué dirección física va la 5000?",
  correct: "right",
  options: [
    { id: "right", text: "8072", why: "Por qué es ésta." },
    { id: "noOffset", text: "7168", why: "Qué error lleva a este número, y por qué está mal." }
  ]
}
```

El paso que pregunta **no tiene que dar la respuesta** ni en la narración ni en los
paneles: en las máquinas, la fase `ask` muestra la dirección pero no la parte. El
paso siguiente la resuelve. Cada opción necesita su `why`; el recurso lo verifica.
Ojo con el alto: la explicación de una opción incorrecta más la de la correcta
tienen que entrar en el alto de la narración a 1280×720, así que cada `why` va en
una o dos líneas.

## Agregar una traducción a un ejemplo con máquina

Un paso con `address` (la dirección) y `phase` (hasta dónde se tradujo):

| Máquina | Fases, en orden |
|---|---|
| Paginación | `table`, `ask`, `split`, `lookup`, `compose` |
| Segmentación | `table`, `ask`, `split`, `limit`, `perm`, `compose` |
| Segmentación paginada | `table`, `ask`, `split`, `segment`, `page`, `compose` |
| Invertida | `table`, `ask`, `search`, `hash`, `probe` (con `probe: n`), `compose` |

Si un paso no trae `address`, sigue con la del paso anterior. `address: null`
saca la dirección de la pantalla. Agregá `expect` con el resultado —un número, o
`"fault"`, `"segfault"`, `"protection"`— en el paso que lo muestra.

---

## Lo que el recurso verifica solo al abrirse

**No son comentarios: son campos que el código chequea**, y si algo no da lo dice
la consola del navegador.

- que cada `expect` sea lo que da la traducción;
- que los campos de bits de una dirección, pegados, den la dirección, y que ningún
  valor se salga de sus bits;
- que la dirección 00402A10h del 14 caiga en la fila 1 de la externa, en la fila 2
  de la interna, y vaya a la física 002F1A10h;
- que cada pregunta tenga su opción correcta entre las opciones, sin repetir, y
  con un `why` en cada una, y que el último paso no tenga pregunta;
- que todas las pistas del 7 se usen, y una sola vez;
- que cada ejemplo tenga `closing` y `stepUnit`, que todo panel tenga nombre y
  globito y algo que mostrar en cada paso, que los tramos estén contiguos y los
  números en orden;
- que no quede ningún `{dato}` sin completar ni ninguna marca sin cerrar, que todo
  globito invocado exista y que todo globito escrito se use.

---

## Hasta dónde llega

Explica al nivel de la materia y no más.

No aparece en ningún lado: algoritmos de sustitución (están en `page-replacement`;
el 12 dice sólo que «el algoritmo elige una víctima»), la TLB más allá de un
globito, tablas de más de dos niveles, particiones fijas y dinámicas, buddy
system, asignación de marcos y thrashing, y ninguna arquitectura real.

Tampoco se dice nunca qué entra o qué no entra en el parcial.

---

## Decisiones que conviene confirmar con la cátedra

1. **Ejercicio 4, la dirección 0BEEFh.** El desplazamiento se sale del límite *y*
   el segmento es de sólo lectura. El recurso responde **segmentation fault**,
   porque controla el límite primero, y lo dice en la nota del paso. Si la cátedra
   espera «error de protección», o las dos cosas, hay que cambiar el orden de los
   controles.
2. **Ejercicio 6 b, «64Kb».** Se leyó como 64 KiB: 128 marcos de 0,5 KiB, 7 bits
   de marco y 16 bytes de tabla de marcos libres. Si eran kilobits, cambian las tres
   cuentas.
3. **Ejercicio 6 b, el formato de la fila.** La guía dice «proponga». El recurso
   propone presencia + marco, 8 bits. Para el 8 b propone R, W, X, uso,
   modificado, presencia y 5 bits de marco: 11 bits.
4. **Ejercicio 11 b.** El recurso dice que el código es «posiblemente» el segmento
   1, como la guía, y no distingue cuál de los otros dos es la pila y cuál los
   datos: las pistas no alcanzan.
5. **El ejemplo 12 no viene de la guía**, ni el 2, el 8, el 13, el 14 ni el 15: los
   números se armaron para el recurso. En el 12 la víctima la elige «el algoritmo
   de sustitución» sin decir cuál, a propósito.
6. **El hash del 15**, (número de proceso + página) mod 8, es el más simple
   posible, para que se pueda hacer de cabeza. No es el de ningún sistema real.

### Colores

El recurso no estrena tipografía: usa la pila del sistema, como los demás.

Los colores de los estados de proceso son los de la cátedra y aparecen sólo en el
12: `RUNNING` azul, `READY` verde, `BLOCKED` rojo, `TERMINATED` gris. Lo demás lo
eligió este recurso, porque la cátedra no tiene colores para la memoria:

| Rol | Tono |
|---|---|
| Número de página | violeta `#6d28d9` |
| Desplazamiento | verde azulado `#0b6a62` |
| Número de marco | ocre `#9a4507` |
| Número de segmento | magenta `#be185d` |
| Fila de la tabla externa (14) | índigo `#4338ca` |
| Proceso (15) y bits de control | grises |
| Fallos y errores | **tinta**, con `✗` y borde punteado |
| «Cambió en este paso» | grafito, como en toda la familia |

**Los fallos y los errores no son rojos.** El rojo es `BLOCKED`, y en el 12 las
dos cosas aparecen en la misma pantalla: un fallo de página *causa* que el proceso
quede en `BLOCKED`, y pintarlos del mismo color diría que son lo mismo. Lo dicen
el `✗`, el borde punteado y el texto. En `page-replacement` el fallo sí es rojo,
porque ahí no aparece ningún estado de proceso; **si la cátedra prefiere que los
dos recursos marquen el fallo igual, hay que elegir uno de los dos criterios.**

---

## Verificación antes de publicar un cambio

1. Abrirlo con doble clic, sin servidor y sin internet.
2. La consola limpia, en los quince ejemplos y en las cuatro variantes del 12.
3. Recorrer cada ejemplo para adelante y para atrás: cada paso igual en los dos
   sentidos.
4. A 1280×720, nada scrollea: ni la página ni ningún panel, tampoco con una
   pregunta contestada mal.
5. A 390 px, una columna y nada se va para el costado.
6. Teclado: flechas, `Inicio`, `Fin`, `Tab` con el foco visible, y las preguntas
   contestables sin mouse.
7. Con el almacenamiento bloqueado, las preguntas funcionan igual.

Lo medido al construirlo: **135 pasos** y **270 tableros** (1280×720 y 390 px) sin
un desborde, sin scroll de página, con la consola limpia y sin un solo pedido de
red; **135 vueltas** ida contra vuelta, todas idénticas; **48 respuestas** (una
mal y una bien en cada una de las 24 preguntas) sin desborde; las respuestas
sobreviven a la recarga y el recurso anda con el almacenamiento bloqueado; **22
paradas de `Tab`**, todas con contorno visible; todos los textos de color arriba de
4,5:1 contra el fondo que de verdad les toca (el más justo, 4,58:1).

---

## Lo que falta

**Toda la narración la escribió un agente y no la revisó nadie de la cátedra**:
las 135 narraciones y sus notas, las 24 preguntas con sus 78 explicaciones, las
dieciocho frases de cierre (una por variante en el 12), los dieciséis globitos de
panel y los veinticinco de término. Lo único que viene dado son los enunciados y
los números de la guía. Es lo primero que hay que leer antes de mandarles el link
a los estudiantes.
