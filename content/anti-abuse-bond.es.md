+++
title = "El depósito anti-abuso: poner la honestidad en garantía"
date = "2026-06-17T12:00:00Z"

[extra]
author = "catrya"
img = "/img/anti-abuse-bond.jpg"
summary = "Uno de los grandes retos de un sistema P2P descentralizado, resistente a la censura y privado como Mostro es mitigar el abuso: el spam en el libro de órdenes y los intentos de estafa de quienes pueden crear una identidad nueva en segundos. Por eso sumamos un mecanismo opcional: el depósito anti-abuso. Al entrar en una operación, el usuario bloquea una pequeña cantidad de sats como garantía que recupera íntegra si actúa de buena fe, pero que pierde si intenta estafar, hacer spam o abandonar la operación. Es un segundo hold invoice independiente del escrow, y cada nodo decide si lo activa y bajo qué condiciones, según las características de su comunidad."
+++

Construir un sistema de intercambio P2P descentralizado, resistente a la censura y privado sobre Nostr, como es Mostro, trae consigo un reto difícil: ¿cómo mitigar el abuso?

Un usuario malintencionado puede intentar llenar el libro de órdenes de un Mostro con ofertas spam, solo para molestar y dejar las ofertas reales perdidas entre tanto ruido. O al revés: vaciar el libro tomando todas las ofertas únicamente para que desaparezcan. Y como Mostro es anónimo —y crear una identidad nueva es tan fácil como generar un par de llaves—, también está quien intenta estafar directamente a su contraparte. ¿Cómo se frena a quien quiere sabotear el libro de órdenes o estafar a otros usuarios?

Es cierto que ya tenemos defensas. Contra la estafa, existe un sistema de disputas, y la hold invoice del escrow no se libera hasta que el vendedor confirma que recibió el fiat, así que un estafador difícilmente logra su objetivo; y contra el spam, Mostro aplica una [prueba de trabajo](https://mostro.network/protocol/chat.html#other-considerations) (*proof of work*) que encarece inundar la red de eventos. Pero ninguna era suficiente: al estafador, intentarlo no le costaba nada, y la prueba de trabajo no detiene a un atacante decidido. El que lo intentaba y fallaba simplemente lo volvía a intentar.

## Una decisión que nos tomó tiempo

Llevábamos tiempo pensando en un depósito anti-abuso, pero nos frenaba que, si alguien completamente nuevo quiere comprar sats, ¿cómo va a pagar un depósito si todavía no tiene sats?

La respuesta fue no imponerlo. Decidimos que esta funcionalidad sería **opcional**: cada administrador de un nodo Mostro puede activarla o no, y fijar las condiciones que considere según las características propias de su comunidad. Un nodo orientado a recién llegados puede prescindir de ella; otro, más expuesto al abuso, puede activarla. La red decide, no nosotros.

## ¿Qué es el depósito anti-abuso?

La idea es la misma que la de un depósito de alquiler. Cuando alquilas un apartamento te piden una garantía: si devuelves todo en orden, la recuperas íntegra; solo la pierdes si rompes algo. Funciona porque alinea los incentivos —cuidas más lo que sabes que te puede costar.

En Mostro, al entrar en una operación pones en garantía una pequeña cantidad de sats que recuperas **por completo** si actúas de buena fe, pero que pierdes si intentas estafar a tu contraparte, vaciar el libro de órdenes o hacer spam, o si incumples tu parte del trato. La consecuencia es directa: tanto el estafador como el spammer dejan de jugar gratis. Ahora ponen **su propio dinero en riesgo**, y eso desalienta el abuso antes de que ocurra.

## Cada nodo pone sus reglas

Recuerda que Mostro no es un único servidor, sino muchos nodos compitiendo entre sí. Cada nodo que activa el depósito define sus propias reglas: a quién se lo pide (a quien crea la orden, a quien la toma, o a ambos) y de cuánto es. El monto suele ser un porcentaje pequeño del valor de la orden —por ejemplo, un **1%** con un mínimo en sats—, pero ese porcentaje lo decide cada nodo.

> **Consejo:** Puedes consultar si el nodo que estás usando exige un depósito anti-abuso —y de cuánto sería— desde tu propio cliente de Mostro, en la sección *Acerca de*, antes de operar.

## ¿No es lo mismo que el escrow?

No. El depósito es completamente independiente del escrow de la operación. Es un segundo hold invoice: tus sats quedan únicamente bloqueados en tu billetera, no se gastan. Si todo va bien, se desbloquean y vuelven a ti sin haber salido nunca de tu billetera. No se mezcla ni se descuenta del monto del intercambio.

Así que, en condiciones normales, el depósito no es un costo: vuelve íntegro a tu billetera, igual que los sats bloqueados en cualquier hold invoice.

## ¿Cuándo recupero mi depósito?

Recuperas el **100%** siempre que cumplas tu parte:

- Completas el intercambio correctamente.
- Cancelas la orden de forma cooperativa.
- Surge una disputa y el administrador no determina que hayas actuado de mala fe.

## ¿Y cuándo puedo perderlo?

Solo pierdes tu depósito por intentar abusar del sistema. Hay dos situaciones:

1. **Por decisión en una disputa.** Un administrador (*solver*), tras revisar las pruebas, determina que actuaste de mala fe e instruye a Mostro a cobrar tu depósito.
2. **Por incumplir y dejar correr el tiempo.** Si tomas o creas una orden y luego no pagas la hold invoice de la orden o no entregas tu factura a tiempo, dejas vencer el plazo que te correspondía. Esto solo aplica si el nodo activó esa política.

## ¿A dónde van los sats de un depósito cobrado?

Cuando un depósito se cobra por decisión en una disputa, los sats se reparten entre el nodo —que así financia el trabajo de resolver disputas y mantener el servicio— y la contraparte honesta, como compensación por el perjuicio. La proporción de ese reparto la define cada nodo y es pública, así que puedes conocerla antes de operar.

Si en cambio se cobra por dejar vencer el plazo, los sats van al nodo.

## Veámoslo con un ejemplo

**Un vendedor que quiere quedarse con todo.** Carlos crea una orden de venta (es el **vendedor**) y Diana la toma para comprar sats (es la **compradora**), en un nodo que exige depósito anti-abuso. Diana hace la transferencia fiat correctamente y guarda el comprobante. Pero Carlos, de mala fe, se niega a liberar los sats y alega que nunca recibió el pago, con la esperanza de quedarse a la vez con el fiat y con los sats.

Diana abre una disputa y le presenta al administrador el comprobante de la transferencia. El *solver* confirma que Diana pagó: Mostro libera los sats del escrow a su favor y **cobra el depósito de Carlos**. Como compensación por el mal rato, Diana recibe una parte de ese depósito; el resto queda para el nodo. Carlos no solo no logró su estafa, sino que perdió su propio dinero por intentarla.

**Alguien que toma una orden y desaparece.** Eduardo toma una orden para comprar sats y Mostro le pide el siguiente paso para continuar. Pero Eduardo simplemente deja de responder: no paga, no avanza, no cancela. Su contraparte queda en el aire esperando a alguien que ya no va a aparecer.

En un nodo que activó la política de plazos, no hace falta abrir ninguna disputa: cuando vence el tiempo que le correspondía a Eduardo, **pierde el depósito de esa operación** automáticamente. Así, abandonar una orden a medias deja de ser gratis, y quien actúa en serio no queda atrapado esperando indefinidamente.

## Si te corresponde el depósito de tu contraparte

Si tu contraparte pierde su depósito y a ti te toca una parte, tu cliente te pedirá una factura para enviarte esos sats. Dispones de un plazo definido por el nodo (por ejemplo, **15 días**) para reclamarla; si lo dejas pasar, pierdes el derecho a cobrar esa parte. Por eso conviene atender la solicitud de tu cliente en cuanto aparezca.

## Conclusión

El depósito anti-abuso persigue un objetivo claro: que en Mostro actuar de buena fe sea lo natural y que abusar salga caro, sin sacrificar privacidad ni descentralización. Quien cumple no paga nada; quien abusa, paga. Y como cada nodo decide sus reglas y las hace públicas, tú eliges siempre con la información por delante.

## Más información

- **Documentación de usuario:** [Depósito anti-abuso](https://mostro.network/docs-spanish/anti-abuse-bond.html)
- **Especificación técnica:** [ANTI_ABUSE_BOND.md](https://github.com/MostroP2P/mostro/blob/main/docs/ANTI_ABUSE_BOND.md)
- **Documentación del protocolo:** [Add Bond Invoice](https://mostro.network/protocol/add_bond_invoice.html)

¡Opera tranquilo: en Mostro, la honestidad siempre se recupera íntegra! 🧌🫶
