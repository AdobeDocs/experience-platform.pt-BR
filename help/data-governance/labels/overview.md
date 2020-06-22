---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Visão geral dos rótulos de uso de dados
topic: labels
translation-type: tm+mt
source-git-commit: e3c69589e0d4f8224b74a663b23f67e6731ddec4
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 0%

---


# Visão geral dos rótulos de uso de dados

O DULE (Data Usage Labeling and Implacation, Rotulação e Aplicação de Uso de Dados) é o mecanismo principal do Adobe Experience Platform Data Governance. Os recursos DULE permitem aplicar rótulos de uso de dados a conjuntos de dados e campos, categorizando cada um de acordo com as políticas de uso de dados relacionadas.

Este documento fornece uma visão geral das etiquetas de uso de dados (também conhecidas como etiquetas DULE) no Experience Platform. Antes de ler este guia, consulte a visão geral [do](../home.md) Data Governance para obter uma introdução mais robusta à estrutura DULE.

## Noções básicas sobre rótulos de uso de dados

Rótulos de uso de dados permitem categorizar conjuntos de dados e campos de acordo com as políticas de uso que se aplicam a esses dados. As etiquetas podem ser aplicadas a qualquer momento, proporcionando flexibilidade na forma como você escolhe administrar os dados. As práticas recomendadas incentivam a rotulação de dados assim que eles forem ingeridos no Experience Platform ou assim que os dados estiverem disponíveis para uso no Platform.

Os rótulos de uso de dados aplicados no nível do conjunto de dados são propagados para todos os campos no conjunto de dados. Os rótulos também podem ser aplicados diretamente a campos individuais (cabeçalhos de coluna) em um conjunto de dados, sem propagação.

Para obter mais informações sobre os rótulos de uso de dados disponíveis no Experience Platform e as políticas de uso que eles representam, consulte o guia sobre os rótulos [de uso de dados](reference.md)suportados.

## Herança de etiqueta para segmentos de audiência

Todos os segmentos de audiência criados pelo Serviço [de segmentação de](../../segmentation/home.md) Adobe Experience Platform herdam os rótulos de uso de seus conjuntos de dados correspondentes. Isso permite que os aplicativos criados sobre o Experience Platform (como a Real-time Customer Data Platform) forneçam a aplicação automática da política de uso de dados ao ativar segmentos para destinos.

Além de herdar rótulos de nível de conjunto de dados, os segmentos herdam todos os rótulos de nível de campo de seus conjuntos de dados associados por padrão. Dependendo de como seu aplicativo baseado no Platform consome segmentos, você pode especificar potencialmente quais campos são usados, impedindo assim o segmento de herdar rótulos de campos excluídos.

Para obter mais informações sobre como a aplicação automática funciona na CDP em tempo real, consulte a visão geral [da CDP Data Governance em tempo](../../rtcdp/privacy/data-governance-overview.md#enforce-data-usage-compliance)real.

<!-- (Add after DEC mapping reference is added to AAM docs to link out to)
### Inheritance from Adobe Audience Manager Data Export Controls

Experience Platform has the ability to share segments with Adobe Audience Manager. Any Data Export Controls that have been applied to Audience Manager segments are translated to equivalent labels and marketing actions recognized by Experience Platform Data Governance.

For a reference on how specific Data Export Controls map to data usage labels in Platform, please refer to the [Audience Manager documentation](https://docs.adobe.com/content/help/en/audience-manager/user-guide/features/data-export-controls.html).
-->

## Próximas etapas

Agora que você foi introduzido nos rótulos de uso de dados, pode continuar a ler o guia [do](user-guide.md) usuário para saber como gerenciar os rótulos na interface do usuário do Experience Platform. Para obter etapas sobre como gerenciar rótulos usando APIs, consulte a seção apropriada no guia [do desenvolvedor do serviço de](../../catalog/api/labels.md)catálogo.