---
title: Classe da Lista de Marketing Comercial XDM
description: Este documento fornece uma visão geral da classe de Lista de Marketing de Negócios XDM no Experience Data Model (XDM).
source-git-commit: 19bb39b66f3a3eb93fd0138ac021568021d77b0f
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 3%

---

# [!UICONTROL Classe da ] Lista de Marketing de Negócios XDM

>[!NOTE]
>
>Essa classe só está disponível para organizações que têm acesso à edição B2B da Plataforma de dados do cliente em tempo real.

[!UICONTROL O XDM Business Marketing ] lista uma classe padrão do Experience Data Model (XDM) que captura as propriedades mínimas necessárias de uma lista de marketing. As listas de marketing permitem priorizar clientes potenciais com maior probabilidade de comprar seu produto.

![](../../images/classes/b2b/business-marketing-list.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `extSourceSystemAudit` | [[!UICONTROL Atributos de Auditoria do Sistema de Origem Externa]](../../data-types/external-source-system-audit-attributes.md) | Se a lista de marketing for proveniente de um sistema de origem externo, esse objeto capturará atributos de auditoria para esse sistema. |
| `marketingListKey` | [[!UICONTROL Origem B2B]](../../data-types/b2b-source.md) | Um identificador composto para a entidade da lista de marketing. |
| `_id` | String | Um identificador exclusivo para o registro. Este é um valor gerado pelo sistema separado do `marketingListID`. |
| `marketingListDescription` | String | Uma descrição para a lista de marketing. |
| `marketingListID` | String | Uma ID exclusiva para a entidade da lista de marketing. |
| `marketingListName` | String | O nome da lista de marketing. |
