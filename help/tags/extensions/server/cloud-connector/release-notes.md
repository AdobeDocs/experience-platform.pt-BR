---
title: Notas de versão da extensão do Adobe Experience Platform Cloud Connector
description: As notas de versão mais recentes para a extensão Cloud Connector no Adobe Experience Platform.
source-git-commit: e232ad7a9b581e65f7f4240bbc06155aec409eb7
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 22%

---

# Notas de versão da extensão do Adobe Experience Platform Cloud Connector

>[!NOTE]
>
>A Adobe Experience Platform Launch foi reformulada como um conjunto de tecnologias de coleta de dados no Adobe Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](../../../term-updates.md) para obter uma referência consolidada das alterações de terminologia.

## 17 de janeiro de 2023

v1.0.1

* Correção de um problema em que um JSON válido colado na área de texto Corpo bruto era salvo como uma sequência de caracteres em vez de um JSON.
* Não permita que Body seja definido em solicitações GET ou HEAD.
* Correção de um erro em que salvar uma resposta maior que 5kb resultaria em falha na execução da regra.

