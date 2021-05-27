---
keywords: Experience Platform, inicial, tópicos populares, api, API, sandbox, sandbox, sandboxes, sandboxes
solution: Experience Platform
title: Apêndice do Guia da API do Sandbox
description: Este documento fornece informações adicionais relacionadas ao trabalho com a API do Sandbox.
topic-legacy: developer guide
source-git-commit: e4067f79e9da106fe2d2a86fa0024c2e5fe5d0ba
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 1%

---

# Apêndice do guia da API de sandbox

Este documento fornece informações complementares relacionadas ao trabalho com a API [!DNL Sandbox].

## Uso de parâmetros de consulta {#query}

A [[!DNL Sandbox] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sandbox-api.yaml) suporta o uso de parâmetros de consulta para página e filtrar resultados ao listar sandboxes.

>[!NOTE]
>
>Os parâmetros de consulta `limit` e `offset` devem ser especificados juntos. Se você especificar apenas um, a API retornará um erro. Se você especificar nenhum, o limite padrão é 50 e o deslocamento é 0.

| Parâmetro | Descrição |
| --- | --- |
| `limit` | O número máximo de registros a serem retornados na resposta. |
| `offset` | O número de entidades do primeiro registro para iniciar (deslocar) a lista de resposta. |
