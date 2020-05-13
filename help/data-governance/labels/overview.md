---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Visão geral dos rótulos de uso de dados
topic: labels
translation-type: tm+mt
source-git-commit: 4b6b9ca5ae7861f8e8b974550be14fbce6efdcf1
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 0%

---


# Visão geral dos rótulos de uso de dados

A DULE (Data Usage Labeling and Implementation) é o mecanismo principal do Adobe Experience Platform Data Governance. Os recursos DULE permitem aplicar rótulos de uso de dados a conjuntos de dados e campos, categorizando cada um de acordo com as políticas de uso de dados relacionadas.

Este documento fornece uma visão geral das etiquetas de uso de dados (também conhecidas como etiquetas DULE) na plataforma Experience. Antes de ler este guia, consulte a visão geral [do](../home.md) Data Governance para obter uma introdução mais robusta à estrutura DULE.

## Noções básicas sobre rótulos de uso de dados

Rótulos de uso de dados permitem categorizar conjuntos de dados e campos de acordo com as políticas de uso que se aplicam a esses dados. As etiquetas podem ser aplicadas a qualquer momento, proporcionando flexibilidade na forma como você escolhe administrar os dados. As práticas recomendadas incentivam a rotulação de dados assim que eles são ingeridos na plataforma da experiência, ou assim que os dados se tornarem disponíveis para uso na plataforma.

Os rótulos de uso de dados aplicados no nível do conjunto de dados são propagados para todos os campos no conjunto de dados. Os rótulos também podem ser aplicados diretamente a campos individuais (cabeçalhos de coluna) em um conjunto de dados, sem propagação.

Para obter mais informações sobre os rótulos de uso de dados disponíveis na Experience Platform e as políticas de uso que eles representam, consulte o guia sobre os rótulos [de uso de dados](reference.md)suportados.

## Herança de etiqueta para segmentos de audiência

Todos os segmentos de audiência criados pelo [Adobe Experience Platform Segmentation Service](../../segmentation/home.md) herdam os rótulos de uso de seus conjuntos de dados correspondentes. Isso permite que os aplicativos criados sobre a Plataforma de experiência (como a Plataforma de dados do cliente em tempo real) forneçam a aplicação automática da política de uso de dados ao ativar segmentos para destinos.

Além de herdar rótulos de nível de conjunto de dados, os segmentos herdam todos os rótulos de nível de campo de seus conjuntos de dados associados por padrão. Dependendo de como seu aplicativo baseado em plataforma consome segmentos, você pode especificar potencialmente quais campos são usados, impedindo assim o segmento de herdar rótulos de campos excluídos.

Para obter mais informações sobre como a aplicação automática funciona na CDP em tempo real, consulte a visão geral [da CDP Data Governance em tempo](../../rtcdp/privacy/data-governance-overview.md#enforce-data-usage-compliance)real.

## Próximas etapas

Agora que você foi introduzido nos rótulos de uso de dados, pode continuar a ler o guia [do](user-guide.md) usuário para saber como gerenciar os rótulos na interface do usuário da plataforma de experiência. Para obter etapas sobre como gerenciar rótulos usando APIs, consulte a seção apropriada no guia [do desenvolvedor do serviço de](../../catalog/api/labels.md)catálogo.