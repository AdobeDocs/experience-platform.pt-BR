---
keywords: Experience Platform, home, tópicos populares, governança de dados, api de etiqueta de uso de dados, api de serviço de política, visão geral dos rótulos de uso de dados
solution: Experience Platform
title: Visão geral dos rótulos de uso de dados
topic-legacy: labels
description: Saiba como os rótulos de uso de dados são usados para ajudar a reforçar a conformidade com o controle de dados no Adobe Experience Platform.
exl-id: 4f113000-b9a1-4dfb-9502-6a5d08f0b26f
source-git-commit: 7e4c2ef8089276829604c9d8a8dd20a122b18c7a
workflow-type: tm+mt
source-wordcount: '680'
ht-degree: 0%

---

# Visão geral dos rótulos de uso de dados

O Adobe Experience Platform permite aplicar rótulos de uso de dados a conjuntos de dados e campos, categorizando cada um de acordo com os campos relacionados [políticas de governança de dados](../policies/overview.md) e [políticas de controle de acesso](../../access-control/abac/ui/policies.md).

Este documento fornece uma visão geral dos rótulos de uso de dados em [!DNL Experience Platform].

## Noções básicas sobre rótulos de uso de dados

Os rótulos de uso de dados permitem categorizar os conjuntos de dados e campos de acordo com as políticas de governança que se aplicam a esses dados. Rótulos podem ser aplicados a qualquer momento, fornecendo flexibilidade na maneira como você decide controlar os dados. As práticas recomendadas incentivam a rotulagem de dados assim que eles forem assimilados em [!DNL Experience Platform]ou assim que os dados estiverem disponíveis para uso em [!DNL Platform].

Os rótulos de uso de dados que são aplicados no nível do conjunto de dados são propagados para todos os campos no conjunto de dados. Os rótulos também podem ser aplicados diretamente a campos individuais (cabeçalhos de coluna) em um conjunto de dados, sem propagação.

[!DNL Platform] O fornece vários rótulos &quot;principais&quot; de uso de dados prontos para uso, que abrangem uma grande variedade de restrições comuns aplicáveis ao controle de dados. Para obter mais informações sobre esses rótulos e as políticas de governança que eles representam, consulte o guia em [rótulos principais de uso de dados](reference.md).

Além dos rótulos fornecidos pelo Adobe, você também pode definir seus próprios rótulos personalizados para sua organização. Consulte a seção sobre [gerenciamento de rótulos](#manage-labels) para obter mais informações.

## Herança de rótulo para segmentos de público-alvo

Todos os segmentos de público-alvo criados por [Serviço de segmentação do Adobe Experience Platform](../../segmentation/home.md) herdar os rótulos de uso de seus conjuntos de dados correspondentes. Isso permite que o Experience Platform forneça a aplicação automática da política ao ativar segmentos para destinos.

Além de herdar rótulos de nível de conjunto de dados, os segmentos herdam todos os rótulos de nível de campo de seus conjuntos de dados associados por padrão. Portanto, é possível identificar mais facilmente quais atributos devem ser excluídos de seus segmentos e impedir que eles herdem rótulos de campos excluídos.

Para obter mais informações sobre como a imposição automática funciona no Platform, consulte a visão geral em [aplicação automática da política](../enforcement/auto-enforcement.md).

### Herança dos controles de exportação de dados do Adobe Audience Manager

[!DNL Experience Platform] O tem a capacidade de compartilhar segmentos com a Adobe Audience Manager. Quaisquer Controles da exportação de dados que foram aplicados a segmentos de Audience Manager são traduzidos para rótulos e ações de marketing equivalentes reconhecidos por [!DNL Experience Platform] Governança de dados.

Para obter uma referência sobre como os Controles da exportação de dados específicos são mapeados para rótulos de uso de dados em [!DNL Platform]consulte o [Documentação do Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aam-data-export-control-in-aep).

## Gerenciamento de rótulos de uso de dados em [!DNL Experience Platform] {#manage-labels}

Você pode gerenciar rótulos de uso de dados usando [!DNL Experience Platform] APIs ou a interface do usuário. Consulte as subseções abaixo para obter detalhes sobre cada uma.

### Uso da interface do usuário

O **[!UICONTROL Políticas]** na área de trabalho do [!DNL Experience Platform] A interface do usuário permite visualizar e gerenciar rótulos principais e personalizados para sua organização. Você pode usar o **[!UICONTROL Esquemas]** espaço de trabalho para [aplicar rótulos aos seus esquemas do Experience Data Model (XDM)](../../xdm/tutorials/labels.md)ou você pode usar o **[!DNL Datasets]** espaço de trabalho para [aplicar rótulos a conjuntos de dados](./user-guide.md) em vez disso.

>[!NOTE]
>
>A aplicação de rótulos no nível do conjunto de dados só é compatível com casos de uso de governança de dados. Se estiver tentando criar políticas de acesso para os dados, você deve aplicar rótulos ao esquema em que o conjunto de dados se baseia. Consulte a visão geral em [controle de acesso baseado em atributo](../../access-control/abac/overview.md) para obter mais informações.

### Uso de APIs

O `/labels` endpoint no [API do serviço de política](https://www.adobe.io/experience-platform-apis/references/policy-service/) O permite gerenciar programaticamente rótulos de uso de dados, incluindo a criação de rótulos personalizados. Consulte a [guia de endpoint de etiquetas](../api/labels.md) para obter mais informações.

O [API do serviço do conjunto de dados](https://www.adobe.io/experience-platform-apis/references/dataset-service/) é usada para gerenciar rótulos para campos e conjuntos de dados. Consulte o guia sobre [gerenciamento de rótulos do conjunto de dados](./dataset-api.md) para obter mais informações.

>[!NOTE]
>
>A aplicação de rótulos no nível do conjunto de dados só é compatível com casos de uso de governança de dados. Se você estiver tentando criar políticas de acesso para os dados, será necessário [aplicar rótulos ao esquema](../../xdm/tutorials/labels.md) em que o conjunto de dados se baseia. Consulte a visão geral em [controle de acesso baseado em atributo](../../access-control/abac/overview.md) para obter mais informações.

## Próximas etapas

Este documento forneceu uma introdução aos rótulos de uso de dados e sua função na estrutura de Governança de dados. Consulte a documentação vinculada a este guia para saber mais sobre como gerenciar rótulos em [!DNL Experience Platform].
