---
title: Apêndice do guia da API de ferramentas de sandbox
description: Este documento fornece informações adicionais relacionadas ao trabalho com a API de ferramentas de sandbox.
exl-id: fdfa019d-ce0e-456b-b591-7d96d1115e02
source-git-commit: 955c6946786e9425bdb99d623595420a6d13747e
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 1%

---

# Apêndice do guia de API de sandbox

Este documento fornece informações adicionais relacionadas ao trabalho com a API [!DNL Sandbox].

## Uso de parâmetros de consulta {#query}

A API de ferramentas de sandbox suporta o uso de parâmetros de consulta para paginar e filtrar resultados ao listar pacotes.

>[!NOTE]
>
>O `limit` pode ser passado e iniciado individualmente.

| Parâmetro | Descrição |
| --- | --- |
| `limit` | O número máximo de registros a serem retornados na resposta. O limite padrão é 20. |
| `start` | O início de onde uma lista subdefinida de itens deve começar. |
| `targetSandbox` | Representa o nome da sandbox onde você deseja importar seus artefatos. |
| `jobType` | O tipo de trabalho. Este valor pode ser `NEW`, `RESUME` ou `ROLLBACK`. |
| `jobStatus` | O status do trabalho. Este valor pode ser `PENDING`, `IN_PROGRESS`, `SUCCESS`, `FAILED` ou `CANCELLED`. |
| `requestType` | O tipo de solicitação. Este valor pode ser `EXPORT`, `IMPORT` ou `COPY`. |
| `expiryPeriod` | Esse período especificado pelo usuário define a data de expiração do pacote (em dias) a partir da hora em que o pacote foi publicado. Esse valor não deve ser negativo. O valor padrão é 90 dias a partir do momento em que a API de atualização ou publicação é chamada. |
| `packageType` | O tipo de pacote. Este valor pode ser `PARTIAL` ou `FULL`. |
| `status` | O status do pacote. Este valor pode ser `DRAFT`, `PUBLISHED`, `PUBLISH_IN_PROGRESS` ou `PUBLISH_FAILED`. |
