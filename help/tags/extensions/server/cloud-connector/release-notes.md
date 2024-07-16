---
title: Notas de versão da extensão do Adobe Experience Platform Cloud Connector
description: As notas de versão mais recentes da extensão do Cloud Connector no Adobe Experience Platform.
exl-id: 5ee85d9f-71f4-46ee-9064-4ceee1cf90e7
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 21%

---

# Notas de versão da extensão do Adobe Experience Platform Cloud Connector

>[!NOTE]
>
>O Adobe Experience Platform Launch foi reformulado como um conjunto de tecnologias de coleção de dados na Adobe Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](../../../term-updates.md) para obter uma referência consolidada das alterações de terminologia.

## 17 de janeiro de 2023

v1.0.1

* Correção de um problema em que um JSON válido colado na área de texto Corpo bruto era salvo como uma sequência em vez de um JSON.
* Não permitir que o corpo seja definido em solicitações GET ou HEAD.
* Correção de um erro em que salvar uma resposta com mais de 5kb resultaria em falha na execução da regra.
