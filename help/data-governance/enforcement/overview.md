---
keywords: Experience Platform;página inicial;tópicos populares;Imposição de política;Imposição automática;Imposição baseada em API;governança de dados
solution: Experience Platform
title: Visão Geral da Aplicação de Política
description: Saiba como as políticas de uso de dados são aplicadas no Adobe Experience Platform.
exl-id: d19d8060-85a1-405c-856d-f59041947a33
source-git-commit: 7b15166ae12d90cbcceb9f5a71730bf91d4560e6
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---

# Visão geral da aplicação de políticas

Depois que [rótulos de uso de dados](../labels/overview.md) forem aplicados e [políticas de uso de dados](../policies/overview.md) forem definidas, você poderá aplicar essas políticas para impedir operações de dados que constituam violações de política.

>[!NOTE]
>
>Este documento se concentra na aplicação de políticas de uso de dados. Para obter informações sobre políticas de controle de acesso, consulte o manual sobre [controle de acesso baseado em atributos](../../access-control/abac/overview.md).

Há dois métodos de aplicação de políticas no Adobe Experience Platform: aplicação automática e aplicação baseada em API.

## Aplicação automática

O Experience Platform aproveita a linhagem de dados, a classificação de dados e os recursos de gerenciamento de políticas para avaliar e detectar automaticamente violações de políticas. Consulte a visão geral sobre [aplicação automática de política](./auto-enforcement.md) para obter mais informações.

## Imposição com base em API

A API [!DNL Policy Service] fornece endpoints que permitem testar ações de marketing em relação a conjuntos de dados ou combinações arbitrárias de rótulos de uso de dados para verificar se ocorrem violações de política. Com base na resposta da API, você pode configurar protocolos no aplicativo de experiência para aplicar adequadamente a conformidade com a política de governança de dados.

Consulte o tutorial em [Imposição baseada em API](./api-enforcement.md) para obter etapas sobre como avaliar políticas usando a API.
