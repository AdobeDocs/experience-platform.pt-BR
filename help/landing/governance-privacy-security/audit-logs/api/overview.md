---
title: Guia da API de consulta de auditoria
description: A Consulta de auditoria é uma API RESTful que permite aos desenvolvedores ver quem realizou quais ações no Adobe Experience Platform.
role: Developer
feature: Audits, API
exl-id: 9ed291c6-ff8b-4d9b-9fed-d1e3fa8f92fb
source-git-commit: c0eb5b5c3a1968cae2bc19b7669f70a97379239b
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 2%

---

# [!DNL Audit Query] Manual da API

A API [!DNL Audit Query] fornece pontos de extremidade que permitem recuperar e monitorar programaticamente os dados do evento para vários recursos do Adobe Experience Platform. Os endpoints são descritos abaixo. Visite o [guia de introdução](./getting-started.md) para obter informações importantes sobre os cabeçalhos necessários, como ler exemplos de chamadas de API e muito mais.

Para exibir todos os pontos de extremidade e operações CRUD disponíveis, visite o [[!DNL Audit Query] API swagger](https://www.adobe.io/experience-platform-apis/references/audit-query/).

## Eventos

Os eventos de auditoria fornecem insights sobre as ações do usuário na Platform, incluindo o tipo de ação, a data e a hora, a ID de email do usuário que executou a ação e atributos adicionais relevantes para o tipo de ação para vários recursos no Adobe Experience Platform. Para saber como recuperar métricas usando a API, consulte o [manual de endpoint de eventos](./events.md).

## Exportar

A exportação de auditoria permite recuperar dados de eventos especificando os eventos que você deseja recuperar na carga. Para saber como recuperar métricas usando a API, consulte o [manual do endpoint de exportação](./export.md).
