---
keywords: Experience Platform, home, tópicos populares, governança de dados, api de etiqueta de uso de dados, api de serviço de política, visão geral dos rótulos de uso de dados
solution: Experience Platform
title: Visão geral dos rótulos de uso de dados
topic-legacy: labels
description: A Governança de dados do Adobe Experience Platform permite aplicar rótulos de uso de dados a conjuntos de dados e campos, categorizando cada um de acordo com as políticas de uso de dados relacionadas. Este documento fornece uma visão geral de rótulos de uso de dados no Experience Platform.
exl-id: 4f113000-b9a1-4dfb-9502-6a5d08f0b26f
source-git-commit: 937225ff08e2e02c5840f86d6ed50644e05bdfe5
workflow-type: tm+mt
source-wordcount: '611'
ht-degree: 0%

---

# Visão geral dos rótulos de uso de dados

O Adobe Experience Platform [!DNL Data Governance] permite aplicar rótulos de uso de dados a conjuntos de dados e campos, categorizando cada um de acordo com as políticas de uso de dados relacionadas.

Este documento fornece uma visão geral dos rótulos de uso de dados em [!DNL Experience Platform]. Antes de ler este guia, consulte a [Visão geral da governança de dados](../home.md) para obter uma introdução mais robusta à estrutura de governança de dados.

## Noções básicas sobre rótulos de uso de dados

Os rótulos de uso de dados permitem categorizar os conjuntos de dados e campos de acordo com as políticas de uso que se aplicam a esses dados. Rótulos podem ser aplicados a qualquer momento, fornecendo flexibilidade na maneira como você decide controlar os dados. As práticas recomendadas incentivam a rotulagem de dados assim que eles são assimilados em [!DNL Experience Platform], ou assim que os dados forem disponibilizados para uso em [!DNL Platform].

Os rótulos de uso de dados que são aplicados no nível do conjunto de dados são propagados para todos os campos no conjunto de dados. Os rótulos também podem ser aplicados diretamente a campos individuais (cabeçalhos de coluna) em um conjunto de dados, sem propagação.

[!DNL Platform] O fornece vários rótulos &quot;principais&quot; de uso de dados prontos para uso, que abrangem uma grande variedade de restrições comuns aplicáveis ao controle de dados. Para obter mais informações sobre esses rótulos e as políticas de uso que eles representam, consulte o guia em [principais rótulos de uso de dados](reference.md).

Além dos rótulos fornecidos pelo Adobe, você também pode definir seus próprios rótulos personalizados para sua organização. Consulte a seção sobre [gerenciamento de rótulos](#manage-labels) para obter mais informações.

## Herança de rótulo para segmentos de público-alvo

Todos os segmentos de público-alvo criados pelo [Adobe Experience Platform Segmentation Service](../../segmentation/home.md) herdam os rótulos de uso de seus conjuntos de dados correspondentes. Isso permite que o Experience Platform forneça a aplicação automática da política de uso de dados ao ativar segmentos para destinos.

Além de herdar rótulos de nível de conjunto de dados, os segmentos herdam todos os rótulos de nível de campo de seus conjuntos de dados associados por padrão. Portanto, é possível identificar mais facilmente quais atributos devem ser excluídos de seus segmentos e impedir que eles herdem rótulos de campos excluídos.

Para obter mais informações sobre como a imposição automática funciona na plataforma, consulte a visão geral em [imposição automática de política](../enforcement/auto-enforcement.md).

### Herança dos controles de exportação de dados do Adobe Audience Manager

[!DNL Experience Platform] O tem a capacidade de compartilhar segmentos com a Adobe Audience Manager. Quaisquer Controles da exportação de dados que foram aplicados a segmentos de Audience Manager são traduzidos para rótulos e ações de marketing equivalentes reconhecidos por [!DNL Experience Platform] [!DNL Data Governance].

Para obter uma referência sobre como os Controles de exportação de dados específicos mapeiam para rótulos de uso de dados em [!DNL Platform], consulte a [documentação do Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aam-data-export-control-in-aep).

## Gerenciamento de rótulos de uso de dados em [!DNL Experience Platform] {#manage-labels}

Você pode gerenciar rótulos de uso de dados usando [!DNL Experience Platform] APIs ou a interface do usuário. Consulte as subseções abaixo para obter detalhes sobre cada uma.

### Uso da interface do usuário

O espaço de trabalho **[!UICONTROL Policies]** na interface do usuário [!DNL Experience Platform] permite visualizar e gerenciar rótulos principais e personalizados para sua organização. O espaço de trabalho **[!DNL Datasets]** permite aplicar rótulos a conjuntos de dados e campos. Para obter mais informações, consulte o [guia do usuário de rótulos](user-guide.md).

### Uso de APIs

O endpoint `/labels` na [API do Serviço de Política](https://www.adobe.io/experience-platform-apis/references/policy-service/) permite gerenciar programaticamente os rótulos de uso de dados, incluindo a criação de rótulos personalizados. Consulte o [guia de ponto de extremidade de rótulos](../api/labels.md) para obter mais informações.

A [API do Serviço de Conjunto de Dados](https://www.adobe.io/experience-platform-apis/references/dataset-service/) é usada para gerenciar rótulos para campos e conjuntos de dados. Consulte o guia em [gerenciar rótulos do conjunto de dados](./dataset-api.md) para obter mais informações.

## Próximas etapas

Este documento forneceu uma introdução aos rótulos de uso de dados e sua função na estrutura de Governança de dados. Consulte a documentação vinculada a este guia para saber mais sobre como gerenciar rótulos em [!DNL Experience Platform].
