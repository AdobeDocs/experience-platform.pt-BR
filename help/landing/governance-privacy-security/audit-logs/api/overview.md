---
title: Guia da API de consulta de auditoria
description: Consulta de auditoria é uma RESTful API que permite que os desenvolvedores vejam quem fez quais ações no Adobe Experience Platform.
source-git-commit: 5b3459711f41430977f9d7b06f8b35801739207c
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 2%

---

# [!DNL Audit Query] Manual da API

O [!DNL Audit Query] A API fornece endpoints que permitem recuperar e monitorar programaticamente os dados do evento para vários recursos do Adobe Experience Platform. Os endpoints são descritos abaixo. Visite o [guia de introdução](./getting-started.md) para obter informações importantes sobre cabeçalhos necessários, ler chamadas de API de exemplo e muito mais.

Para exibir todos os endpoints e operações CRUD disponíveis, visite a [[!DNL Audit Query] Swagger de API](https://www.adobe.io/experience-platform-apis/references/audit-query/).

## Eventos

Os eventos de auditoria fornecem informações sobre as ações do usuário no Platform, incluindo o tipo de ação, a data e a hora, a ID do email do usuário que executou a ação e atributos adicionais relevantes ao tipo de ação para vários recursos no Adobe Experience Platform. Para saber como recuperar métricas usando a API, consulte o [guia de endpoint de eventos](./events.md).

## Exportar

A exportação de auditoria permite recuperar dados de eventos especificando os eventos que você deseja recuperar no payload. Para saber como recuperar métricas usando a API, consulte o [guia de endpoint de exportação](./export.md).
