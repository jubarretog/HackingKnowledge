---
hidden: true
layout:
  width: default
  title:
    visible: true
  description:
    visible: false
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
  metadata:
    visible: true
---

# Pendientes

## Plantear Remediación Vulns Web

### Solve SSRF

Para solucionar una vulnerabilidad de SSRF tenemos que asegurarnos que el input recibido cumpla con el formato esperado según el caso de uso, ya sea letras, números, o ambos. Siempre debemos chequear formatos por lista blanca (ej: me aseguro que solo tenga letras y `-`) y no por lista negra. Cuando recibimos un request, todo lo que venga en el path, en la querystring, en el body o en la mayoría de headers es input controlado por el usuario, y por lo tanto debe ser chequeado antes de usar. Si esperamos un formato más complejo y ninguna de las opciones anteriores se adapta a nuestro caso, podemos usar expresiones regulares.

* Nunca concatenes parámetros para armar una URL sin codificarlos, usa funciones estándar de las librerías de tu lenguaje para codificar los parámetros (urlencode, encodeURIComponent, etc.).



## Writeup CDNio

## Revision seccion Pentesting

Agregar Pentesting vs Bug Bounty

##

## Continuación sección Crypto

## Nueva sección - AI - ML Hacking

AI, Machine Learning, Deep Learning, GenAI, LLMs, SLM, transformers, tokens, pretraining and finetuning, Prompt, Prompt Injection

Un promp bien formulado define rol, obejtivo, alcance de tarea y condiciones específicas, few shot y zero ahot prompting, ejemplificación, identificación y verificacion

RAG, Retrieval Augmented Generation, retriever Kb y generator

## Continuación sección Pwn

