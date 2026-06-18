+++
title = "Nueva versión del protocolo Mostro"
date = "2026-06-18T12:00:00Z"

[extra]
author = "negrunch"
img = "/img/vesion2.jpg"
summary = "La versión 2 del protocolo Mostro deja atrás los gift wraps (NIP-59) para el envío de mensajes entre Mostro y los clientes, adoptando en su lugar eventos kind 14 con contenido encriptado mediante NIP-44. Este cambio cierra la ventana de ataque que bautizamos como \"Gift Wrap Apocalypse\", un vector de spam que, cualquiera podría usar para inutilizar un nodo Mostro, sin sacrificar la privacidad, ya que mantenemos la rotación de llaves por cada orden. La mejora llega en la versión 0.18.0 del nodo Mostro y, junto al anti-abuse bond, deja a Mostro listo para producción."
+++

## Cómo empezamos

Cuando comenzamos a trabajar en Mostro, teníamos que decidir de qué manera los clientes y el nodo Mostro se iban a comunicar. Los primeros experimentos los hicimos utilizando NIP-04, con el que encriptábamos la data en Nostr; en ese momento NIP-04 era el estándar.

NIP-04 tenía un problema: filtraba información de los usuarios, y esa información podía servir para que terceros los deanonimizaran. Como en los inicios de Mostro el usuario podía publicar órdenes utilizando cualquier llave privada, empezamos a notar que algunos usuarios usaban la misma llave privada con la que posteaban en clientes como Amethyst, Damus, etc., lo cual era todavía mucho más terrible para su privacidad.

Inmediatamente comenzamos a trabajar en una solución que le permitiera al usuario estar protegido sin afectar la UX de los clientes. Por eso pensamos, implementamos, repensamos y reimplementamos la primera versión del protocolo.

## La primera versión: gift wraps y rotación de llaves

Decidimos utilizar gift wraps (NIP-59), que nos venían como anillo al dedo, ya que ocultaban datos como el origen del mensaje: cada mensaje se envía con una llave efímera. Aun así, seguíamos teniendo un problema. Los mensajes que Mostro enviaba al cliente iban dirigidos a una pubkey única del usuario, y si los usuarios estaban usando la misma pubkey con la que posteaban en Damus, iba a ser muy sencillo vincularlos con Mostro.

Así que decidimos crear un sistema de rotación de llaves. En lugar de permitir al usuario ingresar una llave privada, hicimos que los clientes generaran una seed (BIP-39) y, a partir de ahí, el cliente generara una llave para cada orden que el usuario creara o tomara, al más puro estilo de una wallet de Bitcoin (BIP-32).

La implementación no era sencilla, pero el resultado era que el usuario obtenía un alto grado de privacidad.

## El "Gift Wrap Apocalypse"

En la teoría esto funciona muy bien, pero la utilización de gift wraps en Nostr abre una ventana de ataque a los relays y a los nodos Mostro. A este ataque yo lo llamo "Gift Wrap Apocalypse".

Como los gift wraps se envían con llaves efímeras y el timestamp modificado, un atacante puede enviar cualquier cantidad de estos eventos con basura dentro, espameando, y hasta que Mostro no los desencripte no sabrá si son eventos legítimos o no. Esto hace muy costoso resistir estos ataques, ya que desencriptar requiere recursos de Mostro. En teoría es muy fácil inutilizar un nodo Mostro enviando una gran cantidad de estos eventos; ahora, con IA, cualquier script kiddie sin ningún conocimiento técnico puede atacar a un nodo Mostro hasta dejarlo sin capacidad de respuesta.

Hasta ahora no hemos recibido este temido ataque, pero antes de que ocurra nos hemos adelantado y hemos decidido prescindir de los gift wraps para el envío de mensajes entre Mostro y los clientes. Sí, eliminamos una capa de privacidad, pero, siendo sinceros, al rotar llaves por cada orden seguimos manteniendo un alto grado de privacidad al operar en Mostro.

## La solución: kind 14 + NIP-44

En su lugar utilizamos eventos kind 14 con el contenido encriptado (NIP-44). Así, sin más, tan sencillo como eso. Hemos pasado de tener un contenido encriptado como este:

```json
// external wrap layer
{
  "id": "<id>",
  "kind": 1059,
  "pubkey": "<Buyer's ephemeral pubkey>",
  "content": {
    // seal
    "id": "<seal's id>",
    "pubkey": "<index 0 pubkey (identity key)>",
    "content": {
      // rumor
      "id": "<rumor's id>",
      "pubkey": "<Index 1 pubkey (trade key)>",
      "kind": 1,
      "content": [
        {
          "order": {
            "version": 1,
            "id": "<Order Id>",
            "trade_index": 1,
            "action": "take-sell",
            "payload": null
          }
        },
        "<index 1 signature of the sha256 hash of the serialized first element of content>"
      ],
      "created_at": 1691518405,
      "tags": []
    },
    "kind": 13,
    "created_at": 1686840217,
    "tags": [],
    "sig": "<index 0 pubkey (identity key) signature>"
  },
  "tags": [["p", "<Mostro's pubkey>"]],
  "created_at": 1234567890,
  "sig": "<Buyer's ephemeral pubkey signature>"
}
```

A este:

```json
[
  {
    "order": {
      "version": 2,
      "id": "<Order Id>",
      "trade_index": 1,
      "action": "take-sell",
      "payload": null
    }
  },
  "<index 1 signature of the sha256 hash of the serialized first element>",
  ["<index 0 pubkey (identity key)>", "<index 0 identity proof signature>"]
]
```

No ahondaré en detalles técnicos, ya que esto puedes verlo en la [documentación del protocolo](https://mostro.network/protocol/key_management.html).

## Versionado y disponibilidad

Esta mejora sale en la versión 0.18.0 de Mostro node. A partir de ahí, la versión 1 del protocolo queda deprecada, pero todavía se puede utilizar. En la versión 0.19.0, la opción de protocolo por defecto de Mostro será la "2", y todo rastro de la versión "1" será eliminado: es tiempo suficiente para que todos los clientes Mostro se actualicen.

Con esta mejora, junto al [anti-abuse bond](https://mostro.network/blog/es/anti-abuse-bond/), consideramos que Mostro está listo para ser utilizado en producción. Siempre teniendo en cuenta que es software experimental y seguramente con bugs por arreglar, pero confiamos en que tenemos un producto estable que brinde soluciones a quienes requieran poder comprar y vender Bitcoin libremente, sin miedo a la censura, represalias o vigilancia.
