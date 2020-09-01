---
keywords: Experience Platform;home;popular topics;data governance;data usage label api;policy service api;data usage labels overview
solution: Experience Platform
title: Visão geral dos rótulos de uso de dados
topic: labels
description: O Adobe Experience Platform Data Governance permite que você aplique rótulos de uso de dados a conjuntos de dados e campos, categorizando cada um de acordo com as políticas de uso de dados relacionadas. Este documento fornece uma visão geral das etiquetas de uso de dados no Experience Platform.
translation-type: tm+mt
source-git-commit: 0f3a4ba6ad96d2226ae5094fa8b5073152df90f7
workflow-type: tm+mt
source-wordcount: '614'
ht-degree: 0%

---


# Visão geral dos rótulos de uso de dados

A Adobe Experience Platform [!DNL Data Governance] permite que você aplique rótulos de uso de dados a conjuntos de dados e campos, categorizando cada um de acordo com as políticas de uso de dados relacionadas.

Este documento fornece uma visão geral dos rótulos de uso de dados em [!DNL Experience Platform]. Antes de ler este guia, consulte a visão geral [do](../home.md) Data Governance para obter uma introdução mais robusta à estrutura do Data Governance.

## Noções básicas sobre rótulos de uso de dados

Rótulos de uso de dados permitem categorizar conjuntos de dados e campos de acordo com as políticas de uso que se aplicam a esses dados. As etiquetas podem ser aplicadas a qualquer momento, proporcionando flexibilidade na forma como você escolhe administrar os dados. As práticas recomendadas incentivam a rotulação de dados assim que eles são ingeridos [!DNL Experience Platform], ou assim que os dados estiverem disponíveis para uso em [!DNL Platform].

Os rótulos de uso de dados aplicados no nível do conjunto de dados são propagados para todos os campos no conjunto de dados. Os rótulos também podem ser aplicados diretamente a campos individuais (cabeçalhos de coluna) em um conjunto de dados, sem propagação.

[!DNL Platform] fornece várias etiquetas &quot;principais&quot; de uso de dados prontas para uso, que abrangem uma grande variedade de restrições comuns aplicáveis ao controle de dados. Para obter mais informações sobre esses rótulos e as políticas de uso que eles representam, consulte o guia sobre os rótulos [](reference.md)de uso de dados principais.

Além das etiquetas fornecidas pelo Adobe, você também pode definir suas próprias etiquetas personalizadas para sua organização. Consulte a seção sobre como [gerenciar rótulos](#manage-labels) para obter mais informações.

## Herança de etiqueta para segmentos de audiência

Todos os segmentos de audiência criados pelo Serviço [de segmentação da](../../segmentation/home.md) Adobe Experience Platform herdam os rótulos de uso de seus conjuntos de dados correspondentes. Isso permite que os aplicativos criados sobre [!DNL Experience Platform] (como [!DNL Real-time Customer Data Platform]) forneçam a aplicação automática da política de uso de dados ao ativar segmentos para destinos.

Além de herdar rótulos de nível de conjunto de dados, os segmentos herdam todos os rótulos de nível de campo de seus conjuntos de dados associados por padrão. Dependendo de como seu aplicativo [!DNL Platform]baseado consome segmentos, você pode especificar potencialmente quais campos são usados, impedindo assim o segmento de herdar rótulos de campos excluídos.

Para obter mais informações sobre como a aplicação automática funciona na CDP em tempo real, consulte a visão geral sobre o controle de [dados na CDP](../../rtcdp/privacy/data-governance-overview.md#enforce-data-usage-compliance)em tempo real.

### Herança dos controles de exportação de dados da Adobe Audience Manager

[!DNL Experience Platform] tem a capacidade de compartilhar segmentos com a Adobe Audience Manager. Todos os Controles de exportação de dados que foram aplicados a segmentos Audience Manager são traduzidos para rótulos equivalentes e ações de marketing reconhecidas por [!DNL Experience Platform][!DNL Data Governance].

Para obter uma referência sobre como os controles de exportação de dados específicos mapeiam para rótulos de uso de dados em [!DNL Platform], consulte a documentação [do](https://docs.adobe.com/content/help/en/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aam-data-export-control-in-aep)Audience Manager.

## Gerenciamento de rótulos de uso de dados em [!DNL Experience Platform] {#manage-labels}

Você pode gerenciar rótulos de uso de dados usando [!DNL Experience Platform] APIs ou a interface do usuário. Consulte as subseções abaixo para obter detalhes sobre cada uma.

### Uso da interface

A área de trabalho **[!UICONTROL Políticas]** na [!DNL Experience Platform] interface do usuário permite que você visualização e gerencie rótulos principais e personalizados para sua organização. A **[!DNL Datasets]** área de trabalho permite aplicar rótulos a conjuntos de dados e campos. For more information, refer to the [labels user guide](user-guide.md).

### Uso de APIs

O `/labels` endpoint na API [do Serviço de](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) Política permite gerenciar programaticamente os rótulos de uso de dados, incluindo a criação de rótulos personalizados. Consulte o guia [de pontos de extremidade de](../api/labels.md) etiquetas para obter mais informações.

A API [do Serviço de](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dataset-service.yaml) Conjunto de Dados é usada para gerenciar rótulos para conjuntos de dados e campos. Consulte o guia sobre como [gerenciar rótulos](./dataset-api.md) de conjuntos de dados para obter mais informações.

## Próximas etapas

Este documento forneceu uma introdução aos rótulos de uso de dados e sua função dentro da estrutura de controle de dados. Consulte a documentação vinculada em todo este guia para saber mais sobre como gerenciar as etiquetas no [!DNL Experience Platform].