+++
title = "¡Un chat con un as bajo la manga!"
date = "2025-03-26T20:00:00Z"

[extra]
author = "negrunch"
img = "/img/chat.jpg"
summary = "Mostro ha implementado un nuevo chat cifrado de extremo a extremo para sus intercambios P2P de Bitcoin, diseñado para resolver disputas sin comprometer la privacidad del usuario. Utilizando criptografía avanzada (DHEC), cada transacción genera una única *llave maestra compartida* conocida solo por el comprador y el vendedor. En caso de disputa, cualquiera de las partes puede voluntariamente entregar esta llave a un mediador, permitiéndole descifrar y revisar únicamente esa conversación específica, la cual es inalterable y no puede ser borrada por estafadores. Esta innovadora característica asegura la disponibilidad de evidencia verificable para una resolución justa, evitando la necesidad de almacenamiento centralizado de mensajes y protegiendo la privacidad general de las comunicaciones en Mostro."
+++

## Introducción: Hablando claro y seguro en el mundo Bitcoin P2P

Intercambiar Bitcoin directamente entre personas (peer-to-peer o P2P) ofrece libertad y control, eliminando intermediarios. En Mostro, estamos comprometidos con hacer esta experiencia lo más fluida y segura posible. Sabemos que la comunicación clara entre comprador y vendedor es fundamental, especialmente cuando las cosas no salen según lo planeado.

Pero, ¿qué pasa si surge una disputa? ¿Cómo podemos asegurarnos de que la verdad salga a la luz sin comprometer la privacidad de nadie? Hoy presentamos una nueva característica en Mostro diseñada exactamente para eso: un **chat integrado, cifrado de extremo a extremo, con un as bajo la manga para resolver disputas de forma justa y transparente.**

## El Dilema de las Disputas: Mensajes Borrados y Privacidad en Riesgo

En nuestros casi cuatro años de experiencia trabajando con [@lnp2pBot](https://lnp2pbot.com/), nos encontramos con un problema recurrente y frustrante: cuando una de las partes intentaba estafar a la otra, a menudo borraba los mensajes de la conversación. ¡Plop! La evidencia desaparecía, dejando al usuario honesto sin poder demostrar lo sucedido y dificultando enormemente la resolución justa de la disputa.

La solución "fácil" sería que nosotros utilizaramos al bot como intermediario de cada mensaje y guardáramos una copia de todas las conversaciones en una base de datos central. Así, un administrador podría simplemente revisar el historial en caso de disputa. Pero seamos sinceros, **eso sería terrible en términos de privacidad**. Iría en contra del espíritu descentralizado y privado de Bitcoin, exponiendo conversaciones que deberían ser confidenciales. Necesitábamos una solución mejor.

## Mostro Chat: Comunicación Privada por Defecto

Por eso, hemos implementado un sistema de chat directamente dentro de los clientes de Mostro. Cuando la operación de compra/venta avanza a un estatus activo, se abre un canal de comunicación directo y privado con la otra parte.

Este chat utiliza el protocolo **Nostr** para la transferencia de mensajes, asegurando que la comunicación viaje de forma descentralizada y resistente a la censura. Más importante aún, la conversación está **cifrada de extremo a extremo**. Esto significa que solo tú y la otra persona involucrada en la transacción pueden leer los mensajes. Ni siquiera nosotros en Mostro podemos saber que están conversando, mucho menos ver lo que se dicen. Hasta aquí, es la privacidad que esperarías.

## La Innovación: La "Llave Maestra Compartida" para Disputas

Aquí es donde las cosas se ponen interesantes y radicalmente diferentes. Para cada operación en Mostro, el sistema utiliza criptografía avanzada (específicamente, un proceso llamado **Diffie-Hellman sobre Curvas Elípticas o DHEC**) para que tú y tu contraparte generen, de forma independiente pero coordinada, una **clave secreta compartida única**.

Piensa en ello como si cada escribieras un mensaje en un papel y lo metieras en una caja fuerte específica para esa orden. Gracias a esta "magia" criptográfica, tanto el comprador como el vendedor obtienen una copia idéntica de la llave para *esa caja fuerte específica*, ¡sin necesidad de enviársela directamente entre partes! **Solo ambas partes conocen esa llave**. Es única para esa conversación y esa operación.

## Resolviendo Disputas sin Romper la Privacidad

Ahora, ¿qué sucede si hay un desacuerdo? Supongamos que el vendedor afirma no haber recibido el pago fiat, o el comprador dice que si lo envió. Aquí entra en juego la "llave maestra compartida":

1.  **Surge una Disputa:** Una de las partes inicia el proceso de disputa en Mostro.
2.  **Decisión Voluntaria:** Cualquiera de las dos partes (comprador o vendedor) tiene la opción de **compartir voluntariamente** su copia de la "llave maestra compartida" con la persona designada para resolver la disputa (el mediador).
3.  **Acceso Controlado:** Con esta llave única, el mediador puede "abrir" la caja fuerte digital y **descifrar únicamente la conversación correspondiente a *esa transacción específica***.
4.  **Evidencia Inmutable:** Los mensajes dentro de este chat están registrados de tal manera que no pueden ser borrados ni alterados sin que sea evidente. El mediador puede ver la conversación tal y como ocurrió, verificando quién dijo qué y cuándo. Esto hace extremadamente difícil para un estafador salirse con la suya si la evidencia está en el chat.

## ¿Por Qué Esto es Revolucionario?

Esta solución logra lo mejor de ambos mundos:

* **Privacidad por Defecto:** Tus conversaciones son privadas y cifradas. Nadie puede espiarlas.
* **Transparencia Bajo Demanda:** Si surge un problema *y* una de las partes lo consiente, la evidencia puede ser revelada de forma segura *solo* al mediador y *solo* para esa disputa.
* **Seguridad Anti-Manipulación:** Los mensajes no pueden ser borrados ni falsificados por un estafador para ocultar sus acciones.
* **Descentralización:** No dependemos de almacenar tus chats privados en nuestros servidores.
* **Claves Únicas por Transacción:** Un detalle crucial es que Mostro genera nuevas claves criptográficas para cada orden. Esto significa que incluso si vuelves a comerciar con la misma persona, la "llave maestra compartida" de esa nueva conversación será completamente diferente. La privacidad y seguridad de cada operación son independientes.

## Conclusión: Un Futuro Más Seguro y Justo para el P2P

Con esta implementación en el chat de Mostro, estamos dando un paso importante para fortalecer la confianza y la seguridad en los intercambios P2P de Bitcoin. Combinamos criptografía robusta con un mecanismo inteligente y respetuoso con la privacidad para asegurar que las disputas puedan resolverse de la manera más justa posible, exponiendo fácilmente a quienes intentan actuar de mala fe.

Queremos que te sientas seguro y respaldado al usar Mostro, sabiendo que cuentas con herramientas innovadoras diseñadas para protegerte sin comprometer tus datos.

## ¿Interesado en los Detalles Técnicos?

Para aquellos con inclinaciones más técnicas que quieran profundizar en la criptografía detrás de la generación de esta llave compartida, pueden consultar nuestro artículo detallado aquí: [https://mostro.network/protocol/chat.html](https://mostro.network/protocol/chat.html)

También puedes probar **mostro-chat** el cual es una prueba-de-concepto y ver por ti mismo el funcionamiento de lo que has leido

[https://github.com/MostroP2P/mostro-chat](https://github.com/MostroP2P/mostro-chat)