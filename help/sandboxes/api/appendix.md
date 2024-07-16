---
keywords: Experience Platform;página inicial;tópicos populares;api;API;sandbox;Sandbox;sandboxes;Sandboxes
solution: Experience Platform
title: Apêndice do guia de API de sandbox
description: Este documento fornece informações adicionais relacionadas ao trabalho com a API de sandbox.
role: Developer
exl-id: 48ffea01-f1b4-48c6-a6f5-c321074023d3
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 1%

---

# Apêndice do guia de API de sandbox

Este documento fornece informações adicionais relacionadas ao trabalho com a API [!DNL Sandbox].

## Uso de parâmetros de consulta {#query}

A [[!DNL Sandbox] API](https://www.adobe.io/experience-platform-apis/references/sandbox) oferece suporte ao uso de parâmetros de consulta para página e filtrar resultados ao listar sandboxes.

>[!NOTE]
>
>Os parâmetros de consulta `limit` e `offset` devem ser especificados juntos. Se você especificar apenas um, a API retornará um erro. Se você especificar nenhum, o limite padrão é 50 e o deslocamento é 0.

| Parâmetro | Descrição |
| --- | --- |
| `limit` | O número máximo de registros a serem retornados na resposta. |
| `offset` | O número de entidades do primeiro registro do qual iniciar (deslocamento) a lista de respostas. |
