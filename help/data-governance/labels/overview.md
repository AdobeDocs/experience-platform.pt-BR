---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Visão geral dos rótulos de uso de dados
topic: labels
translation-type: tm+mt
source-git-commit: d4964231ee957349f666eaf6b0f5729d19c408de
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 0%

---


# Visão geral dos rótulos de uso de dados

O DULE (Data Usage Labeling and Implacation, Rotulação e Aplicação de Uso de Dados) é o mecanismo principal do Adobe Experience Platform Data Governance. Os recursos DULE permitem aplicar rótulos de uso de dados a conjuntos de dados e campos, categorizando cada um de acordo com as políticas de uso de dados relacionadas.

Este documento fornece uma visão geral dos rótulos de uso de dados (também conhecidos como rótulos DULE) no [!DNL Experience Platform]. Antes de ler este guia, consulte a visão geral [do](../home.md) Data Governance para obter uma introdução mais robusta à estrutura DULE.

## Noções básicas sobre rótulos de uso de dados

Rótulos de uso de dados permitem categorizar conjuntos de dados e campos de acordo com as políticas de uso que se aplicam a esses dados. As etiquetas podem ser aplicadas a qualquer momento, proporcionando flexibilidade na forma como você escolhe administrar os dados. As práticas recomendadas incentivam a rotulação de dados assim que eles são ingeridos [!DNL Experience Platform], ou assim que os dados estiverem disponíveis para uso em [!DNL Platform].

Os rótulos de uso de dados aplicados no nível do conjunto de dados são propagados para todos os campos no conjunto de dados. Os rótulos também podem ser aplicados diretamente a campos individuais (cabeçalhos de coluna) em um conjunto de dados, sem propagação.

Para obter mais informações sobre rótulos de uso de dados disponíveis em [!DNL Experience Platform] e as políticas de uso que eles representam, consulte o guia sobre rótulos [de uso de dados](reference.md)suportados.

## Herança de etiqueta para segmentos de audiência

Todos os segmentos de audiência criados pelo Serviço [de segmentação de](../../segmentation/home.md) Adobe Experience Platform herdam os rótulos de uso de seus conjuntos de dados correspondentes. Isso permite que os aplicativos criados sobre [!DNL Experience Platform] (como [!DNL Real-time Customer Data Platform]) forneçam a aplicação automática da política de uso de dados ao ativar segmentos para destinos.

Além de herdar rótulos de nível de conjunto de dados, os segmentos herdam todos os rótulos de nível de campo de seus conjuntos de dados associados por padrão. Dependendo de como seu aplicativo [!DNL Platform]baseado consome segmentos, você pode especificar potencialmente quais campos são usados, impedindo assim o segmento de herdar rótulos de campos excluídos.

Para obter mais informações sobre como a aplicação automática funciona na CDP em tempo real, consulte a visão geral [da CDP em tempo real da](../../rtcdp/privacy/data-governance-overview.md#enforce-data-usage-compliance)Adobe.

<!-- (Add after DEC mapping reference is added to AAM docs to link out to)
### Inheritance from Adobe Audience Manager Data Export Controls

Experience Platform has the ability to share segments with Adobe Audience Manager. Any Data Export Controls that have been applied to Audience Manager segments are translated to equivalent labels and marketing actions recognized by Experience Platform Data Governance.

For a reference on how specific Data Export Controls map to data usage labels in Platform, please refer to the [Audience Manager documentation](https://docs.adobe.com/content/help/en/audience-manager/user-guide/features/data-export-controls.html).
-->

## Próximas etapas

Agora que você foi introduzido nos rótulos de uso de dados, pode continuar a ler o guia [do](user-guide.md) usuário para saber como gerenciar os rótulos na [!DNL Experience Platform] interface do usuário. Para obter etapas sobre como gerenciar rótulos usando APIs, consulte a seção apropriada no guia [do desenvolvedor do serviço de](../../catalog/api/labels.md)catálogo.