---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Visão geral dos rótulos de uso de dados
topic: labels
translation-type: tm+mt
source-git-commit: f4b3148db3b4a17d071c1c8ad2aff8dd64ddd0b7
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 0%

---


# Visão geral dos rótulos de uso de dados

O DULE (Data Usage Labeling and Implacation, Rotulação e Aplicação de Uso de Dados) é o mecanismo principal do Adobe Experience Platform Data Governance. Os recursos DULE permitem aplicar rótulos de uso de dados a conjuntos de dados e campos, categorizando cada um de acordo com as políticas de uso de dados relacionadas.

Este documento fornece uma visão geral dos rótulos de uso de dados (também conhecidos como rótulos DULE) no [!DNL Experience Platform]. Antes de ler este guia, consulte a visão geral [do](../home.md) Data Governance para obter uma introdução mais robusta à estrutura DULE.

## Noções básicas sobre rótulos de uso de dados

Rótulos de uso de dados permitem categorizar conjuntos de dados e campos de acordo com as políticas de uso que se aplicam a esses dados. As etiquetas podem ser aplicadas a qualquer momento, proporcionando flexibilidade na forma como você escolhe administrar os dados. As práticas recomendadas incentivam a rotulação de dados assim que eles são ingeridos [!DNL Experience Platform], ou assim que os dados estiverem disponíveis para uso em [!DNL Platform].

Os rótulos de uso de dados aplicados no nível do conjunto de dados são propagados para todos os campos no conjunto de dados. Os rótulos também podem ser aplicados diretamente a campos individuais (cabeçalhos de coluna) em um conjunto de dados, sem propagação.

[!DNL Platform] fornece várias etiquetas &quot;principais&quot; de uso de dados prontas para uso, que abrangem uma grande variedade de restrições comuns aplicáveis ao controle de dados. Para obter mais informações sobre esses rótulos e as políticas de uso que eles representam, consulte o guia sobre os rótulos [](reference.md)de uso de dados principais.

Além das etiquetas fornecidas pela Adobe, você também pode definir suas próprias etiquetas personalizadas. Para obter etapas sobre como fazer isso na interface do usuário, consulte o guia [do usuário de etiquetas de uso de](./user-guide.md)dados. Para obter etapas sobre como executar isso usando chamadas de API, consulte o guia [da API de rótulos de uso de](./api.md)dados.

## Herança de etiqueta para segmentos de audiência

Todos os segmentos de audiência criados pelo Serviço [de segmentação de](../../segmentation/home.md) Adobe Experience Platform herdam os rótulos de uso de seus conjuntos de dados correspondentes. Isso permite que os aplicativos criados sobre [!DNL Experience Platform] (como [!DNL Real-time Customer Data Platform]) forneçam a aplicação automática da política de uso de dados ao ativar segmentos para destinos.

Além de herdar rótulos de nível de conjunto de dados, os segmentos herdam todos os rótulos de nível de campo de seus conjuntos de dados associados por padrão. Dependendo de como seu aplicativo [!DNL Platform]baseado consome segmentos, você pode especificar potencialmente quais campos são usados, impedindo assim o segmento de herdar rótulos de campos excluídos.

Para obter mais informações sobre como a aplicação automática funciona na CDP em tempo real, consulte a visão geral [da CDP em tempo real da](../../rtcdp/privacy/data-governance-overview.md#enforce-data-usage-compliance)Adobe.

### Herança dos controles de exportação de dados do Adobe Audience Manager

O Experience Platform tem a capacidade de compartilhar segmentos com o Adobe Audience Manager. Todos os Controles de exportação de dados que foram aplicados a segmentos de Audience Manager são traduzidos para rótulos e ações de marketing equivalentes reconhecidos pelo Controle de dados de Experience Platform.

Para obter uma referência sobre como os controles de exportação de dados específicos mapeiam para rótulos de uso de dados no Platform, consulte a documentação [do](https://docs.adobe.com/content/help/en/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aam-data-export-control-in-aep)Audience Manager.


## Próximas etapas

Agora que você foi introduzido nos rótulos de uso de dados, pode continuar a ler o guia [do](user-guide.md) usuário para saber como gerenciar os rótulos na [!DNL Experience Platform] interface do usuário. Para obter etapas sobre como gerenciar rótulos usando APIs, consulte o guia [da API de etiquetas de](./api.md)uso.