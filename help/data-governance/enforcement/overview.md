---
keywords: Experience Platform; home; tópicos populares; Aplicação de políticas; Aplicação automática; Aplicação baseada em API; governança de dados
solution: Experience Platform
title: Visão geral da aplicação de políticas
description: Saiba como as políticas de uso de dados são aplicadas no Adobe Experience Platform.
exl-id: d19d8060-85a1-405c-856d-f59041947a33
source-git-commit: 7b15166ae12d90cbcceb9f5a71730bf91d4560e6
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---

# Visão geral da aplicação de políticas

Uma vez [rótulos de uso de dados](../labels/overview.md) foram aplicadas e [políticas de uso de dados](../policies/overview.md) Depois de definidas, é possível aplicar essas políticas para evitar operações de dados que constituem violações de política.

>[!NOTE]
>
>Este documento se concentra na imposição de políticas de uso de dados. Para obter informações sobre políticas de controle de acesso, consulte o guia sobre [controle de acesso baseado em atributo](../../access-control/abac/overview.md).

Há dois métodos de aplicação de política no Adobe Experience Platform: aplicação automática e aplicação baseada em API.

## Aplicação automática

O Experience Platform aproveita a linhagem de dados, a classificação de dados e os recursos de gerenciamento de políticas para avaliar e exibir automaticamente as violações de políticas. Consulte a visão geral em [aplicação automática da política](./auto-enforcement.md) para obter mais informações.

## Aplicação baseada em API

O [!DNL Policy Service] A API fornece endpoints que permitem testar ações de marketing em relação a conjuntos de dados ou combinações arbitrárias de rótulos de uso de dados para verificar se ocorrem violações de política. Com base na resposta da API, você pode configurar protocolos no aplicativo de experiência para impor adequadamente a conformidade da política de governança de dados.

Veja o tutorial em [Aplicação baseada em API](./api-enforcement.md) para obter etapas sobre como avaliar políticas usando a API.
