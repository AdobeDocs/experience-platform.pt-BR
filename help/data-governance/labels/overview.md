---
keywords: Experience Platform;página inicial;tópicos populares;governança de dados;uso de dados rótulo api;política serviço api;uso de dados rótulos visão geral
solution: Experience Platform
title: Visão geral dos rótulos de uso de dados
description: Saiba como os rótulos de uso de dados são usados para ajudar a impor a conformidade da governança de dados no Adobe Experience Platform.
exl-id: 4f113000-b9a1-4dfb-9502-6a5d08f0b26f
source-git-commit: 916eb01ea7878366620b859c1d6a667a88b850c9
workflow-type: tm+mt
source-wordcount: '786'
ht-degree: 16%

---

# Visão geral dos rótulos de uso de dados {#overview}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_dataUsageLabels_description"
>title="Controle o acesso a dados confidenciais e protegidos"
>abstract="<h2>Descrição</h2><p>Controle o acesso a atributos de dados e/ou segmentos específicos, permitindo projetar fluxos de trabalho flexíveis para as várias personas e equipes que operam em casos de uso da Experience Platform.</p>"

O Adobe Experience Platform permite aplicar rótulos de uso de dados a conjuntos de dados e campos, categorizando cada um de acordo com as [políticas de governança de dados](../policies/overview.md) e [políticas de controle de acesso](../../access-control/abac/ui/policies.md) relacionadas.

Este documento fornece uma visão geral dos rótulos de uso de dados em [!DNL Experience Platform].

## Noções básicas sobre rótulos de uso de dados

Os rótulos de uso de dados permitem categorizar conjuntos de dados e campos de acordo com as políticas de governança que se aplicam a esses dados. Os rótulos podem ser aplicados a qualquer momento, proporcionando flexibilidade na maneira como você escolhe controlar os dados. As práticas recomendadas incentivam a rotulagem de dados assim que eles forem assimilados no [!DNL Experience Platform] ou assim que os dados estiverem disponíveis para uso no [!DNL Experience Platform].

Os rótulos de uso de dados aplicados no nível do conjunto de dados são propagados para todos os campos no conjunto de dados. Os rótulos também podem ser aplicados diretamente a campos individuais (cabeçalhos de coluna) em um conjunto de dados, sem propagação.

O [!DNL Experience Platform] fornece vários rótulos de uso de dados &quot;principais&quot; prontos para uso, que abrangem uma grande variedade de restrições comuns aplicáveis à governança de dados. Para obter mais informações sobre esses rótulos e as políticas de governança que eles representam, consulte o manual em [rótulos de uso de dados principais](reference.md).

Além dos rótulos fornecidos pelo Adobe, você também pode definir seus próprios rótulos personalizados para sua organização. Consulte a seção sobre [gerenciamento de rótulos](#manage-labels) para obter mais informações.

## Herança de rótulos para segmentos de público

Todos os segmentos de público-alvo criados pelo [Serviço de segmentação do Adobe Experience Platform](../../segmentation/home.md) herdam os rótulos de uso de seus conjuntos de dados correspondentes. Isso permite que o Experience Platform forneça aplicação automática de políticas ao ativar segmentos para destinos.

Além de herdar rótulos de nível de conjunto de dados, os segmentos herdam todos os rótulos de nível de campo de seus conjuntos de dados associados por padrão. Portanto, você pode identificar mais facilmente quais atributos devem ser excluídos de seus segmentos e impedir que eles herdem rótulos de campos excluídos.

Para obter mais informações sobre como a imposição automática funciona no Experience Platform, consulte a visão geral em [imposição de política automática](../enforcement/auto-enforcement.md).

### Herança dos controles de exportação de dados do Adobe Audience Manager

[!DNL Experience Platform] pode compartilhar segmentos com a Adobe Audience Manager. Quaisquer Controles de Exportação de Dados que tenham sido aplicados a segmentos do Audience Manager são traduzidos em rótulos equivalentes e ações de marketing reconhecidas pela Governança de Dados do [!DNL Experience Platform].

Para obter uma referência sobre como os Controles de Exportação de Dados específicos são mapeados para rótulos de uso de dados no [!DNL Experience Platform], consulte a [documentação do Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=pt-BR#aam-data-export-control-in-aep).

## Gerenciamento dos rótulos de uso de dados na [!DNL Experience Platform] {#manage-labels}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_dataUsageLabels_instructions"
>title="Instruções"
>abstract="<ul><li>Rotule campos e segmentos XDM para classificar os campos e ou segmentos aos quais você deseja restringir o acesso.</li><li>Funções de rótulo: adicionar rótulos a uma função permite que você defina os rótulos nos quais os membros dessa função devem ter restrições.</li><li>Criar políticas: uma política cria uma relação entre os rótulos em objetos rotulados, como campos e segmentos XDM e os rótulos em funções. Se os rótulos corresponderem, uma permissão ou um acesso restrito poderão ser definidos.</li></ul>"

Você pode gerenciar rótulos de uso de dados usando as APIs do [!DNL Experience Platform] ou a interface do usuário. Consulte as subseções abaixo para obter detalhes sobre cada uma.

### Uso da interface

O espaço de trabalho **[!UICONTROL Policies]** na interface do usuário do [!DNL Experience Platform] permite exibir e gerenciar rótulos principais e personalizados para sua organização. Você pode usar o espaço de trabalho **[!UICONTROL Schemas]** para [aplicar rótulos aos seus esquemas do Experience Data Model (XDM)](../../xdm/tutorials/labels.md) ou aprender a [criar e gerenciar rótulos personalizados na **[!UICONTROL Policies]** interface](./user-guide.md) lendo o guia do usuário de rótulos de uso de dados.

>[!IMPORTANT]
>
>Os rótulos não podem mais ser aplicados a campos no nível do conjunto de dados. Esse workflow foi substituído em favor da aplicação de rótulos no nível do schema. Quaisquer rótulos aplicados anteriormente no nível do objeto do conjunto de dados ainda serão compatíveis por meio da interface do usuário do Experience Platform até 31 de maio de 2024. Para garantir que seus rótulos sejam consistentes em todos os esquemas, todos os rótulos anteriormente anexados a campos no nível do conjunto de dados devem ser migrados para o nível do esquema por você no ano seguinte. Consulte a seção sobre [migrando rótulos aplicados anteriormente](../e2e.md#migrate-labels) para obter instruções sobre como fazer isso.

### Uso de APIs

O ponto de extremidade `/labels` na [API de Serviço de Política](https://www.adobe.io/experience-platform-apis/references/policy-service/) permite gerenciar de forma programática rótulos de uso de dados, incluindo a criação de rótulos personalizados. Consulte o [manual de ponto de extremidade de rótulos](../api/labels.md) para obter mais informações.

A [API de Serviço do Conjunto de Dados](https://www.adobe.io/experience-platform-apis/references/dataset-service/) é usada para gerenciar rótulos para conjunto de dados e campos. Consulte o manual sobre [gerenciamento de rótulos de conjunto de dados](./dataset-api.md) para obter mais informações.

## Próximas etapas

Este documento forneceu uma introdução aos rótulos de uso de dados e sua função na estrutura de governança de dados. Consulte a documentação vinculada a este manual para saber mais sobre como gerenciar rótulos no [!DNL Experience Platform].
