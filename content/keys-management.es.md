+++
title = "Manejo de llaves en Mostro"
date = "2025-02-01T12:00:00Z"

[extra]
author = "negrunch"
img = "/img/gift.jpg"
summary = "La gestión de llaves en Mostro se basa en un sistema de seguridad tan sencillo como intercambiar regalos envueltos y cambiar combinaciones de caja fuerte: cada mensaje entre el usuario y la plataforma utiliza llaves efímeras que funcionan como “candados desechables”, mientras que cada orden de compra o venta se vincula a una llave distinta derivada de una semilla única, lo que garantiza que la información y las transacciones estén siempre protegidas."
+++

La gestión de llaves en Mostro puede sonar complicada si nunca has manejado conceptos técnicos relacionados con la seguridad y la criptografía. Sin embargo, te lo explicaremos con ejemplos que podrías encontrar en tu vida diaria. ¡Es más fácil de lo que parece!

## Imagina que envías un regalo envuelto

Pensemos en la gestión de llaves como el proceso de intercambiar [regalos envueltos](https://github.com/nostr-protocol/nips/blob/master/59.md). Cuando envías un regalo a alguien, quieres asegurarte de que solo esa persona pueda abrirlo. En el mundo de Mostro, estos regalos son los datos que envías, y el envoltorio es la capa de seguridad que los protege.

En este caso, las llaves son como las combinaciones secretas necesarias para abrir ese envoltorio. Mostro utiliza una llave efímera para cada mensaje que se envía entre el cliente y la plataforma. Estas llaves efímeras, una característica esencial de los **gift wraps**, garantizan que cada mensaje esté protegido de manera individual y única.

## Rotación de llaves: Cambiar de cerradura para cada operación

Supongamos que en el mundo físico necesitas intercambiar un paquete con Bob. Para ello, Bob y tú deben enviarse varias cartas confidenciales para ponerse de acuerdo en cómo hacer el intercambio. Para esta operación, utilizarás una identidad diferente a la que usarás en tus siguientes operaciones con otros usuarios. Incluso si volvieras a operar con Bob, ambos estarían utilizando identidades distintas. ¡Eso es lo que hace Mostro con la rotación de llaves!

Cada vez que un usuario crea o toma una orden de compra o venta, se genera una nueva llave específica para esa operación. Estas llaves se derivan de una semilla (_seed_) que el cliente genera aleatoriamente para el usuario. De esta semilla se pueden derivar muchas llaves: la llave pública con índice `0` (ruta de derivación `m/44'/1237'/38383'/0/0`) actúa como identificador principal ante Mostro, mientras que las llaves con índices a partir de `1` (por ejemplo, `m/44'/1237'/38383'/0/n`) son las que se rotan para cada nueva orden. De este modo, aunque la llave para una operación permanezca constante mientras dura la operación, al finalizar esta se usa una nueva llave para la siguiente orden, lo que garantiza seguridad adicional.

## Llaves efímeras: Cerraduras desechables para mensajes únicos

Ahora imagina que necesitas enviar una carta importante por correo, pero no quieres usar tu cerradura habitual para protegerla. En su lugar, utilizas un candado desechable que solo sirve para ese envío en particular. Una vez que la carta llega a su destino, el candado ya no tiene utilidad.

En Mostro, las llaves efímeras funcionan de manera similar. Son llaves que se crean para proteger datos durante un corto período de tiempo o para un propósito específico, como un mensaje individual entre el cliente y Mostro. Una vez que el mensaje se procesa, esa llave se destruye y no se puede volver a usar. Esto minimiza el riesgo de que alguien pueda aprovechar una llave comprometida.

## Reputación vs. Modo privado completo

Mostro permite a los usuarios elegir entre dos modos de operación: **reputación** y **modo privado completo**.

- **Modo reputación**: Tal como indicamos anteriormente, los usuarios se identifican ante Mostro con la llave pública de índice `0` (`m/44'/1237'/38383'/0/0`). Esto permite mantener la reputación vinculada a esta llave. Solo Mostro y el usuario conocen dicha llave pública, garantizando la privacidad del usuario. Mostro se encarga del cálculo de la reputación a partir de la calificación de la contraparte.

- **Modo privado completo**: Permite a los usuarios operar sin necesidad de enviar una llave identificadora. De esta forma, Mostro no puede vincular las órdenes de un mismo usuario, lo que garantiza un nivel máximo de privacidad y seguridad. Debido a la naturaleza privada de este modo, no es posible mantener una reputación para el usuario.

## ¿Por qué es importante esto?

Piensa en cuánto te esfuerzas para proteger algo valioso, como un documento confidencial o un regalo especial. La gestión de llaves en Mostro asegura que toda la información y las operaciones realizadas estén protegidas al máximo nivel. Combinando el uso de llaves efímeras para proteger cada mensaje y la rotación de llaves para cada operación, Mostro garantiza que tus datos estén siempre seguros.

## Conclusión

En resumen, la gestión de llaves en Mostro puede entenderse como el arte de usar combinaciones de seguridad únicas, temporales y específicas para mantener tus datos protegidos. Ya sea utilizando llaves efímeras para mensajes individuales o rotando llaves derivadas de una semilla para cada orden, el sistema está diseñado para ofrecer tranquilidad y seguridad en cada interacción.

¡Ahora ya sabes que Mostro no solo protege tus datos, sino que lo hace de forma eficiente y cuidadosa, como si cada dato fuera un regalo envuelto solo para ti!

## Más información

**Keys Management en el protocolo de Mostro**: [https://mostro.network/protocol/keys-management](https://mostro.network/protocol/keys-management)
