+++
title = "Estado actual en Mostro"
date = 2024-12-20

[extra]
author = "negrunch"
img = "/img/first-post.webp"
summary = "Durante el último año, Mostro ha logrado avances significativos en la gestión de llaves (rotando llaves para cada operación y mejorando la privacidad), estandarizando las órdenes en Nostr a través del nuevo NIP-69 y consolidando su ecosistema gracias a la participación en la residencia b4os, la creación de la Mostro Foundation y el desarrollo de librerías (mostro-tools) y nuevos clientes (una aplicación móvil y la interfaz de terminal Mostrui). Todo esto tiene como objetivo proporcionar una plataforma de intercambio peer-to-peer centrada en la privacidad y fácil de usar, respaldada por HRF, Opensats y otros colaboradores."
+++

Desde hace más de un año hemos estado trabajando incansablemente en Mostro, y aquí tienes un breve resumen.

## Gestión de llaves

Hemos realizado muchas mejoras y probablemente una de las más importantes sea el diseño final de la gestión de llaves. Empezamos a discutir esta idea el trimestre pasado y la comentamos en el último informe. La gestión de llaves es una forma en que los clientes rotan las llaves para cada operación, añadiendo otra capa de privacidad a la implementación previa de gift wrap. Puedes encontrar información más detallada [aquí](https://github.com/MostroP2P/mostro/pull/398). Hoy hemos fusionado nuestro [PR](https://github.com/MostroP2P/mostro/pull/398) principal para implementarlo en mostrod, y también lo implementamos en [mostro-core](https://github.com/MostroP2P/mostro-core/pull/67/files) y [mostro-cli](https://github.com/MostroP2P/mostro-cli/pull/89).

## Nuevo Nostr NIP fusionado

También tuvimos nuestro primer NIP oficial fusionado, [NIP-69](https://github.com/nostr-protocol/nips/blob/master/69.md). Con esto buscamos estandarizar todas las órdenes de la plataforma peer-to-peer en Nostr para tener un gran pool de liquidez fácilmente filtrable.

## B4OS

Mostro fue uno de los proyectos que participó en la [residencia b4os](https://www.libreriadesatoshi.com/b4os), la cual se llevó a cabo en Buenos Aires justo después de la [LABITCONF](https://www.labitconf.com/) de este año.

Yo participé como mentor, yendo allí diariamente durante todo el programa, ayudando a los desarrolladores a comenzar con Mostro. Mostro recibió mucha atención y contó con el mayor número de colaboradores trabajando en él (8 en total). Tuvimos dos semanas muy productivas en las que refinamos cómo Mostro manejará la privacidad y la reputación al mismo tiempo. Esto requerirá algunos cambios en mostrod y mejoras en la [documentación del protocolo](https://mostro.network/protocol/), para la cual (cruzando los dedos) ahora tenemos una versión final.

Durante la residencia b4os, recibimos [contribuciones](https://github.com/MostroP2P/mostro-regtest/pull/2) que mejoraron nuestros contenedores Docker de Mostro — un trabajo increíble que puedes ver [aquí](https://github.com/MostroP2P/mostro-regtest).

## Fundación Mostro

También avanzamos en el establecimiento de la Fundación Mostro, que servirá como entidad legal para gestionar donaciones y dirigirlas a los desarrolladores que deseen contribuir. Otro [colaborador](https://github.com/MostroP2P/mostro-foundation-website) creó el [sitio web de la Fundación Mostro](https://mostro.foundation/).

## Mostro-tools

Ya contamos con colaboradores trabajando en [mostro-tools](https://github.com/MostroP2P/mostro-tools), una biblioteca en TypeScript que implementa el [protocolo Mostro](https://mostro.network/protocol/).

## Aplicación móvil

Nuestro intento anterior de crear la aplicación móvil fracasó, el desarrollador se fue, así que encontramos a otro desarrollador; la tercera es la vencida. Ahora estamos avanzando con la aplicación móvil, que está siendo desarrollada por un desarrollador llamado Biz. Trabajar en Mostro es algo complejo porque nos centramos en la privacidad y la resistencia a la censura, y nuestro objetivo principal es entregar estas funciones de privacidad en una aplicación fácil de usar. Quiero que esta aplicación sea muy intuitiva, adecuada incluso para usuarios no técnicos. Biz entregó una primera aplicación móvil funcional; podemos ver todo el trabajo [aquí](https://github.com/MostroP2P/mobile/pull/31) y [aquí](https://github.com/MostroP2P/mobile/pull/33). La probamos y funciona :D

## Mostrui

Finalmente, iniciamos otro cliente, una Interfaz de Usuario de Terminal (TUI) que nos está ayudando a implementar y comprender los problemas que los desarrolladores de clientes pueden encontrar en el proceso de construir un cliente. Este cliente se llama [Mostrui](https://github.com/MostroP2P/mostrui).

Todo esto no hubiera sido posible sin el apoyo de [HRF](https://hrf.org/), [Opensats](https://opensats.org/) y todos los colaboradores <3
