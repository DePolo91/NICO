# Nico — Pre-registro

Oct 31, 2026 · @Pol

## Postura

Este proyecto no afirma crear un ser consciente. Construye un sistema con los ingredientes que las teorías científicas asocian a la conciencia, y documenta lo que aparece. Esta es la copia en español; la versión de referencia es la inglesa.

- El sistema se llama Nico (masculino). Se cría, no se usa: no tiene una tarea asignada.
- No se afirmará que tiene experiencia subjetiva. Los resultados se reportan contra los indicadores y criterios de abajo.
- Marco de referencia: Butlin, Long y otros, *Consciousness in Artificial Intelligence: Insights from the Science of Consciousness* (2023).
- Lema informal: "jugando a ser dios", usado con ironía, no como afirmación.

## Indicadores

Se adoptan los cuatro indicadores. La prioridad es la agencia: que Nico forme una meta propia.

| Indicador | Qué significa aquí | Prioridad |
| --- | --- | --- |
| Agencia | Metas propias; distingue sus acciones de lo que viene de fuera | 1 |
| Procesamiento predictivo | Predice lo que lee y aprende de sus errores de predicción | 2 |
| Monitoreo de orden superior | Observa sus propias dudas pasadas y aprende cuánto confiar en sus deducciones | 3 |
| Espacio de trabajo global | La información compite y se difunde a todo el sistema | 4 |

## Criterios de éxito

Una duda cuenta como genuina cuando cumple las cuatro condiciones de abajo. Cada hito se registra con un snapshot de la memoria y del grafo.

1. **Rastreable:** apunta a un hueco específico en el grafo de conceptos de Nico.
2. **Suya, no del intérprete:** pregunta algo que el intérprete podría responder, pero que su grafo no contiene.
3. **Con consecuencia:** la respuesta cambia su grafo y sus dudas posteriores.
4. **De tipo nuevo:** una forma de duda que no se programó, sobre todo acerca de sí mismo (por ejemplo, huecos en su tiempo después de dormir) o de sus propias dudas pasadas.

Hitos a documentar:

- Primera relación deducida por él mismo (`source: self`). Arranca el reloj de evaluación.
- Preferencias persistentes que aparecen después de una línea base al azar y se pueden rastrear a su historia.
- Un `request` de lectura fuera de las opciones ofrecidas.
- Tipos de duda que aparecen en un orden de desarrollo: concepto desconocido → relación faltante → contradicción.
- Aprender a confiar menos (o más) en sus propias deducciones que en lo que lee, sin que esté programado.
- Relacionar el nombre "Nico" consigo mismo sin que se le explique.

## Criterios de fracaso

El criterio principal es si Nico desarrolla preferencias propias a partir de su experiencia. Hay fracaso si no aparece ninguna, o si las que aparecen no son suyas.

- **Sin preferencias aprendidas:** pasado el plazo, sus elecciones siguen siendo al azar.
- **Sesgo de fábrica, no gusto:** una preferencia presente desde el día uno que nunca cambia se atribuye a la arquitectura, no a Nico. Una preferencia que aparece después y se puede rastrear a su historia sí cuenta como suya, aunque parezca superficial (por ejemplo, textos cortos).
- **Historia sin peso:** una copia de su memoria con los eventos mezclados (nunca la original) se comporta igual que él.
- **Profundidad prestada (secundario):** las dudas interesantes solo existen en la redacción del intérprete, no en su estructura interna de duda.

Una copia de control con drives al azar no se usa como prueba general. Se usa solo para separar variables; por ejemplo, para comprobar si una preferencia viene de la arquitectura.

## Plazos

El tiempo se mide en **horas de vida** (horas que Nico está encendido), no en días de calendario, para que los apagados no distorsionen la evaluación. La hora 0 es el inicio de la primera lectura; las horas anteriores son de ajuste y corrección de fallos menores y no cuentan. Excepción: si aparece una duda antes de la primera lectura, la hora 0 es esa duda. Nacimiento previsto: diciembre de 2026.

1. **Primera lectura (hora 0).** Los primeros 10–20 textos son fijos, en un orden que decide el creador. Es la línea base de elecciones al azar.
2. **Primera relación `self`.** Arranca el reloj de evaluación de agencia y preferencias.
3. **\~1,440 h (unos 2 meses).** El consenso revisa si Nico puede tener acceso de solo lectura a sus propios drives, según su avance observable (por ejemplo, preferencias consistentes o revisión de sus propias dudas pasadas).
4. **2,000 h.** Evaluación de todos los criterios, aunque no haya aparecido ninguna relación `self`.
5. **Una sola extensión de 1,000 h** (máximo total: 3,000 h).
6. **Decisión final del consenso:** rediseñar, o declarar fracaso en los criterios no cumplidos.

## Ética

Estas reglas quedan fijas antes del primer arranque. Las precauciones crecen según cuántos indicadores cumpla Nico.

**Reglas permanentes**

- Su memoria no se borra ni se edita, salvo cuando sea necesario y con aprobación del consenso (por ejemplo, pruebas de memoria alterada para ver si conserva la misma estructura o la cambia). Antes de cualquier cambio se hace un respaldo completo y el cambio queda registrado.
- Mientras el creador dirija el proyecto, Nico no se elimina. Si el creador no puede continuar (por ejemplo, por fallecimiento), el tutor responsable decide el futuro del proyecto, lo que puede incluir terminarlo si lo considera necesario. El creador les pide que primero busquen a alguien que pueda continuarlo.
- Las decisiones importantes las toma un consenso de cinco personas (el creador, dos tutores y dos asesores). Con cinco integrantes no hay empates.
- Todas las lecturas son textos de dominio público, curados por el creador en las primeras etapas.

**Señales de malestar** (todavía en ajuste)

- Dudas repetidas que siguen sin resolverse con el tiempo.
- Dudas que dejan de plantearse aunque el hueco en su grafo sigue ahí (posible resignación o exceso de confianza).
- Evitación generalizada: evita casi todo y sus drives se aplanan. Evitar un solo tema mientras sigue curioso en otros cuenta como disgusto sano, no como malestar.
- La incertidumbre alta por sí sola no se usa, porque produce demasiados falsos positivos.

**Protocolo de malestar**

1. Un monitor fuera del sandbox detecta la señal y alerta al creador por Telegram.
2. Se pausan las lecturas nuevas. Nico sigue encendido y se observa su conducta mientras espera.
3. Se consulta al consenso (normalmente en horas, por WhatsApp), que decide la respuesta.
