---
keywords: Experience Platform, inicial, tópicos populares, api, API, sandbox, sandbox, sandboxes, sandboxes
solution: Experience Platform
title: Apêndice do Guia da API do Sandbox
description: Este documento fornece informações adicionais relacionadas ao trabalho com a API do Sandbox.
exl-id: 48ffea01-f1b4-48c6-a6f5-c321074023d3
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 1%

---

# Apêndice do guia da API de sandbox

Este documento fornece informações complementares relacionadas ao trabalho com a [!DNL Sandbox] API.

## Uso de parâmetros de consulta {#query}

O [[!DNL Sandbox] API](https://www.adobe.io/experience-platform-apis/references/sandbox) O suporta o uso de parâmetros de consulta para página e filtrar resultados ao listar sandboxes.

>[!NOTE]
>
>O `limit` e `offset` os parâmetros de consulta devem ser especificados juntos. Se você especificar apenas um, a API retornará um erro. Se você especificar nenhum, o limite padrão é 50 e o deslocamento é 0.

| Parâmetro | Descrição |
| --- | --- |
| `limit` | O número máximo de registros a serem retornados na resposta. |
| `offset` | O número de entidades do primeiro registro para iniciar (deslocar) a lista de resposta. |
