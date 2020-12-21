---
keywords: Experience Platform;home;popular topics;data governance;data usage label api;policy service api;data usage labels overview
solution: Experience Platform
title: Visão geral dos rótulos de uso de dados
topic: labels
description: O Adobe Experience Platform Data Governance permite que você aplique rótulos de uso de dados a conjuntos de dados e campos, categorizando cada um de acordo com as políticas de uso de dados relacionadas. Este documento fornece uma visão geral das etiquetas de uso de dados no Experience Platform.
translation-type: tm+mt
source-git-commit: e680191d495e4c33baa8242d40a15b9124eec8cd
workflow-type: tm+mt
source-wordcount: '603'
ht-degree: 0%

---


# Visão geral dos rótulos de uso de dados

A Adobe Experience Platform [!DNL Data Governance] permite que você aplique rótulos de uso de dados a conjuntos de dados e campos, categorizando cada um de acordo com as políticas de uso de dados relacionadas.

Este documento fornece uma visão geral dos rótulos de uso de dados em [!DNL Experience Platform]. Antes de ler este guia, consulte a [visão geral do Data Governance](../home.md) para obter uma introdução mais robusta à estrutura do Data Governance.

## Noções básicas sobre rótulos de uso de dados

Rótulos de uso de dados permitem categorizar conjuntos de dados e campos de acordo com as políticas de uso que se aplicam a esses dados. As etiquetas podem ser aplicadas a qualquer momento, proporcionando flexibilidade na forma como você escolhe administrar os dados. As práticas recomendadas incentivam a rotulação de dados assim que eles são ingeridos em [!DNL Experience Platform], ou assim que os dados estiverem disponíveis para uso em [!DNL Platform].

Os rótulos de uso de dados aplicados no nível do conjunto de dados são propagados para todos os campos no conjunto de dados. Os rótulos também podem ser aplicados diretamente a campos individuais (cabeçalhos de coluna) em um conjunto de dados, sem propagação.

[!DNL Platform] fornece várias etiquetas &quot;principais&quot; de uso de dados prontas para uso, que abrangem uma grande variedade de restrições comuns aplicáveis ao controle de dados. Para obter mais informações sobre esses rótulos e as políticas de uso que eles representam, consulte o guia em [principais rótulos de uso de dados](reference.md).

Além das etiquetas fornecidas pelo Adobe, você também pode definir suas próprias etiquetas personalizadas para sua organização. Consulte a seção [gerenciar rótulos](#manage-labels) para obter mais informações.

## Herança de etiqueta para segmentos de audiência

Todos os segmentos de audiência criados pelo [Adobe Experience Platform Segmentation Service](../../segmentation/home.md) herdam os rótulos de uso dos conjuntos de dados correspondentes. Isso permite que o Experience Platform forneça a aplicação automática da política de uso de dados ao ativar segmentos para destinos.

Além de herdar rótulos de nível de conjunto de dados, os segmentos herdam todos os rótulos de nível de campo de seus conjuntos de dados associados por padrão. Portanto, você pode identificar mais facilmente quais atributos devem ser excluídos de seus segmentos e impedir que eles herdem rótulos de campos excluídos.

Para obter mais informações sobre como a imposição automática funciona na Plataforma, consulte a visão geral sobre [imposição automática de política](../enforcement/auto-enforcement.md).

### Herança dos controles de exportação de dados da Adobe Audience Manager

[!DNL Experience Platform] tem a capacidade de compartilhar segmentos com a Adobe Audience Manager. Todos os Controles de exportação de dados que foram aplicados a segmentos Audience Manager são traduzidos para rótulos e ações de marketing equivalentes reconhecidos por [!DNL Experience Platform] [!DNL Data Governance].

Para obter uma referência sobre como os controles de exportação de dados específicos mapeiam para rótulos de uso de dados em [!DNL Platform], consulte a [documentação do Audience Manager](https://docs.adobe.com/content/help/en/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aam-data-export-control-in-aep).

## Gerenciando rótulos de uso de dados em [!DNL Experience Platform] {#manage-labels}

Você pode gerenciar rótulos de uso de dados usando [!DNL Experience Platform] APIs ou a interface do usuário. Consulte as subseções abaixo para obter detalhes sobre cada uma.

### Uso da interface

A área de trabalho **[!UICONTROL Policies]** na interface do usuário [!DNL Experience Platform] permite que você visualização e gerencie rótulos principais e personalizados para sua organização. A área de trabalho **[!DNL Datasets]** permite que você aplique rótulos a conjuntos de dados e campos. Para obter mais informações, consulte o [guia do usuário de etiquetas](user-guide.md).

### Uso de APIs

O endpoint `/labels` na API [Policy Service](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) permite gerenciar programaticamente os rótulos de uso de dados, incluindo a criação de rótulos personalizados. Consulte [guia de ponto final de etiquetas](../api/labels.md) para obter mais informações.

A [API do Serviço de Conjunto de Dados](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dataset-service.yaml) é utilizada para gerir etiquetas para o conjunto de dados e campos. Consulte o guia em [gerenciar rótulos de conjuntos de dados](./dataset-api.md) para obter mais informações.

## Próximas etapas

Este documento forneceu uma introdução aos rótulos de uso de dados e sua função dentro da estrutura de controle de dados. Consulte a documentação vinculada em todo este guia para saber mais sobre como gerenciar rótulos em [!DNL Experience Platform].