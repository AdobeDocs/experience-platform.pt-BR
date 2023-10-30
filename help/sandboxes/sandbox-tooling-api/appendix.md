---
title: Apêndice do guia da API de ferramentas de sandbox
description: Este documento fornece informações adicionais relacionadas ao trabalho com a API de ferramentas de sandbox.
exl-id: fdfa019d-ce0e-456b-b591-7d96d1115e02
source-git-commit: 308d07cf0c3b4096ca934a9008a13bf425dc30b6
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 1%

---

# Apêndice do guia de API de sandbox

Este documento fornece informações adicionais relacionadas ao trabalho com o [!DNL Sandbox] API.

## Uso de parâmetros de consulta {#query}

A API de ferramentas de sandbox suporta o uso de parâmetros de consulta para paginar e filtrar resultados ao listar pacotes.

>[!NOTE]
>
>A variável `limit` podem ser transmitidos e iniciados individualmente.

| Parâmetro | Descrição |
| --- | --- |
| `limit` | O número máximo de registros a serem retornados na resposta. O limite padrão é 20. |
| `start` | O início de onde uma lista subdefinida de itens deve começar. |
| `targetSandbox` | Representa o nome da sandbox onde você deseja importar seus artefatos. |
| `jobType` | O tipo de trabalho. Esse valor pode ser NEW, RESUME e ROLLBACK. |
| `jobStatus` | O status do trabalho. Esse valor pode ser PENDING, IN_PROGRESS, SUCCESS, FAILED e CANCELED. |
| `requestType` | O tipo de solicitação. Esse valor pode ser EXPORTAR, IMPORTAR e COPIAR. |
| `expiryPeriod ` | Esse período especificado pelo usuário define a data de expiração do pacote (em dias) a partir da hora em que o pacote foi publicado. Esse valor não deve ser negativo. O valor padrão é 90 dias a partir do momento em que a API de atualização ou publicação é chamada. |
