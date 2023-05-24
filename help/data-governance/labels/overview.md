---
keywords: Experience Platform;página inicial;tópicos populares;governança de dados;uso de dados rótulo api;política serviço api;uso de dados rótulos visão geral
solution: Experience Platform
title: Visão geral dos rótulos de uso de dados
description: Saiba como os rótulos de uso de dados são usados para ajudar a impor a conformidade da governança de dados no Adobe Experience Platform.
exl-id: 4f113000-b9a1-4dfb-9502-6a5d08f0b26f
source-git-commit: a1628df7d0eefc795d1eaeefce842a65c7133322
workflow-type: tm+mt
source-wordcount: '794'
ht-degree: 15%

---

# Visão geral dos rótulos de uso de dados {#overview}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_dataUsageLabels_description"
>title="Controle o acesso a dados confidenciais e protegidos"
>abstract="<h2>Descrição</h2><p>Controle o acesso a atributos de dados e/ou segmentos específicos, permitindo projetar fluxos de trabalho flexíveis para as várias personas e equipes que operam em casos de uso da Experience Platform.</p>"

O Adobe Experience Platform permite aplicar rótulos de uso de dados a conjuntos de dados e campos, categorizando cada um de acordo com as configurações relacionadas [políticas de governança de dados](../policies/overview.md) e [políticas de controle de acesso](../../access-control/abac/ui/policies.md).

Este documento fornece uma visão geral dos rótulos de uso de dados no [!DNL Experience Platform].

## Noções básicas sobre o uso de rótulos de dados

Os rótulos de uso de dados permitem categorizar conjuntos de dados e campos de acordo com as políticas de governança que se aplicam a esses dados. Os rótulos podem ser aplicados a qualquer momento, proporcionando flexibilidade na maneira como você escolhe controlar os dados. As práticas recomendadas incentivam a rotulagem de dados assim que eles são assimilados na [!DNL Experience Platform]ou assim que os dados estiverem disponíveis para uso no [!DNL Platform].

Os rótulos de uso de dados aplicados no nível do conjunto de dados são propagados para todos os campos no conjunto de dados. Os rótulos também podem ser aplicados diretamente a campos individuais (cabeçalhos de coluna) em um conjunto de dados, sem propagação.

[!DNL Platform] O fornece vários rótulos de uso de dados &quot;principais&quot; prontos para uso, que abrangem uma grande variedade de restrições comuns aplicáveis ao controle de dados. Para obter mais informações sobre esses rótulos e as políticas de governança que eles representam, consulte o guia em [rótulos de uso de dados principais](reference.md).

Além dos rótulos fornecidos pelo Adobe, você também pode definir seus próprios rótulos personalizados para sua organização. Consulte a seção sobre [gerenciamento de rótulos](#manage-labels) para obter mais informações.

## Herança de rótulos para segmentos de público

Todos os segmentos de público-alvo criados por [Serviço de segmentação do Adobe Experience Platform](../../segmentation/home.md) herdar os rótulos de uso de seus conjuntos de dados correspondentes. Isso permite que o Experience Platform forneça aplicação automática de políticas ao ativar segmentos para destinos.

Além de herdar rótulos de nível de conjunto de dados, os segmentos herdam todos os rótulos de nível de campo de seus conjuntos de dados associados por padrão. Portanto, você pode identificar mais facilmente quais atributos devem ser excluídos de seus segmentos e impedir que eles herdem rótulos de campos excluídos.

Para obter mais informações sobre como a imposição automática funciona na Platform, consulte a visão geral em [aplicação automática de política](../enforcement/auto-enforcement.md).

### Herança dos controles de exportação de dados do Adobe Audience Manager

[!DNL Experience Platform] O tem a capacidade de compartilhar segmentos com a Adobe Audience Manager. Quaisquer controles de exportação de dados aplicados aos segmentos do Audience Manager são traduzidos em rótulos equivalentes e ações de marketing reconhecidas pelo [!DNL Experience Platform] Governança de dados.

Para obter uma referência sobre como os Controles de exportação de dados específicos são mapeados para rótulos de uso de dados no [!DNL Platform], consulte o [Documentação do Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aam-data-export-control-in-aep).

## Gerenciamento de rótulos de uso de dados no [!DNL Experience Platform] {#manage-labels}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_dataUsageLabels_instructions"
>title="Instruções"
>abstract="<ul><li>Rotule campos e segmentos XDM para classificar os campos e ou segmentos aos quais você deseja restringir o acesso.</li><li>Funções de rótulo: adicionar rótulos a uma função permite que você defina os rótulos nos quais os membros dessa função devem ter restrições.</li><li>Criar políticas: uma política cria uma relação entre os rótulos em objetos rotulados, como campos e segmentos XDM e os rótulos em funções. Se os rótulos corresponderem, uma permissão ou um acesso restrito poderão ser definidos.</li></ul>"

É possível gerenciar rótulos de uso de dados usando o [!DNL Experience Platform] APIs ou a interface do usuário. Consulte as subseções abaixo para obter detalhes sobre cada uma.

### Uso da interface

A variável **[!UICONTROL Políticas]** espaço de trabalho no [!DNL Experience Platform] A interface do usuário permite visualizar e gerenciar rótulos principais e personalizados para sua organização. Você pode usar o **[!UICONTROL Esquemas]** espaço de trabalho [aplicar rótulos aos esquemas do Experience Data Model (XDM)](../../xdm/tutorials/labels.md)ou você pode usar o **[!DNL Datasets]** espaço de trabalho [aplicar rótulos a conjuntos de dados](./user-guide.md) em vez disso.

>[!NOTE]
>
>A aplicação de rótulos no nível do conjunto de dados só é compatível com casos de uso de governança de dados. Se você estiver tentando criar políticas de acesso para os dados, será necessário aplicar rótulos ao esquema no qual o conjunto de dados se baseia. Consulte a visão geral em [controle de acesso baseado em atributos](../../access-control/abac/overview.md) para obter mais informações.

### Uso de APIs

A variável `/labels` endpoint na variável [API de serviço de política](https://www.adobe.io/experience-platform-apis/references/policy-service/) O permite gerenciar de forma programática os rótulos de uso de dados, incluindo a criação de rótulos personalizados. Consulte a [guia de endpoint de rótulos](../api/labels.md) para obter mais informações.

A variável [API do serviço de conjunto de dados](https://www.adobe.io/experience-platform-apis/references/dataset-service/) é usado para gerenciar rótulos para conjuntos de dados e campos. Consulte o guia sobre [gerenciamento de rótulos de conjunto de dados](./dataset-api.md) para obter mais informações.

>[!NOTE]
>
>A aplicação de rótulos no nível do conjunto de dados só é compatível com casos de uso de governança de dados. Se estiver tentando criar políticas de acesso para os dados, você deverá [aplicar rótulos ao esquema](../../xdm/tutorials/labels.md) em que o conjunto de dados se baseia. Consulte a visão geral em [controle de acesso baseado em atributos](../../access-control/abac/overview.md) para obter mais informações.

## Próximas etapas

Este documento forneceu uma introdução aos rótulos de uso de dados e sua função na estrutura de governança de dados. Consulte a documentação vinculada a este guia para saber mais sobre como gerenciar rótulos no [!DNL Experience Platform].
