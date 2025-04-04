---
title: Referência do teste de consistência de tag
description: Saiba como o recurso do auditor testa a consistência de tags na Adobe Experience Platform Debugger.
exl-id: 642b0c49-a7c7-4142-8189-67f00ed50015
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 38%

---

# Referência do teste de consistência da tag

Esta referência fornece mais informações sobre como o recurso de auditor no Adobe Experience Platform Debugger testa a consistência de tags.

>[!NOTE]
>
>Para obter mais informações sobre testes do auditor no Experience Platform Debugger, consulte a [visão geral do recurso do auditor](./overview.md).

Os testes de consistência de tags procuram inconsistências em todas as páginas digitalizadas. Esses são valores ou configurações que devem ser os mesmos em todas as páginas do site para garantir uma coleta de dados precisa.

| Teste | Peso | Critérios | Recomendação |
| --- | --- | --- | --- |
| Adobe Analytics - Versão de código consistente | 5 | Mais de uma versão do código do Analytics foi encontrada. | Substitua todas as instâncias do Analytics pela versão atual.<br><br>[Informações adicionais](https://experienceleague.adobe.com/docs/analytics/implementation/home.html) |

{style="table-layout:auto"}
