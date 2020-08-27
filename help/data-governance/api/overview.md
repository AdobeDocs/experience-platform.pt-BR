---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guia do desenvolvedor da API do Serviço de Política
topic: developer guide
translation-type: tm+mt
source-git-commit: 71678b10c9e137016ea404305b272508b9c8cabe
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 1%

---


# [!DNL Policy Service] Guia do desenvolvedor da API

A Adobe Experience Platform [!DNL Data Governance] permite gerenciar dados do cliente e garantir a conformidade com regulamentos, restrições e políticas aplicáveis ao uso de dados. Ele desempenha um papel fundamental em vários [!DNL Experience Platform] níveis, incluindo a catalogação, a linhagem de dados, a rotulagem de uso de dados, as políticas de uso de dados e o controle do uso de dados para ações de marketing.

A [!DNL Policy Service] API fornece vários endpoints que permitem gerenciar programaticamente rótulos e políticas de uso de dados, bem como avaliar ações de marketing para violações de políticas. Esses pontos finais são descritos abaixo. Visite os guias de ponto de extremidade individuais para obter detalhes e consulte o guia [de](./getting-started.md) introdução para obter informações importantes sobre cabeçalhos necessários, como ler chamadas de API de amostra e muito mais.

Para visualização de todos os pontos de extremidade e operações CRUD disponíveis, visite o swagger [[!DNL Policy Service] da](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml)API.

## Rótulos

Rótulos de uso de dados permitem categorizar conjuntos de dados e campos de acordo com as políticas de uso que se aplicam a esses dados. As etiquetas podem ser aplicadas a qualquer momento, proporcionando flexibilidade na forma como você escolhe administrar os dados. As práticas recomendadas incentivam a rotulação de dados assim que eles são ingeridos [!DNL Experience Platform], ou assim que os dados estiverem disponíveis para uso em [!DNL Platform]. Você pode criar, visualização, editar e excluir rótulos usando o `/labels` ponto de extremidade. Para saber como usar esse terminal, visite o guia [de ponto de extremidade de](./labels.md)etiquetas.

## Ações de marketing

As ações de marketing (também chamadas de casos de uso de marketing), no contexto da [!DNL Data Governance] estrutura, são ações que um consumidor de [!DNL Experience Platform] dados pode realizar, para as quais sua organização deseja restringir o uso de dados. Para obter informações detalhadas sobre como trabalhar com ações de marketing, consulte o guia [de pontos de extremidade de ações de](./marketing-actions.md)marketing.

## Políticas

As políticas de uso de dados são regras que descrevem os tipos de ações de marketing às quais você tem permissão ou é restrito para executar em dados dentro de [!DNL Experience Platform]. Uma política é definida pelo seguinte:

1. Uma ação de marketing específica
1. Os rótulos de uso de dados com os quais a ação está restrita não são executados

Para saber como gerenciar políticas na API, consulte o guia de ponto de extremidade de [políticas](./policies.md)

## Avaliação

Depois que os rótulos de uso de dados forem aplicados a [!DNL Platform] conjuntos de dados e as políticas de uso de dados tiverem sido definidas para ações de marketing contra esses rótulos, os recursos de controle de dados permitirão que você aplique essas políticas e evite operações de dados que constituam violações de política.

A [!DNL Policy Service] API fornece pontos de extremidade que permitem testar ações de marketing em relação a conjuntos de dados ou combinações arbitrárias de rótulos de uso de dados para verificar se ocorrem violações de política. Com base na resposta da API, você pode configurar protocolos dentro do aplicativo de experiência para aplicar adequadamente a conformidade da política de uso de dados. Consulte o guia [de pontos de extremidade de](./evaluation.md) avaliação para obter mais informações.

## Próximas etapas

Para começar a fazer chamadas usando a [!DNL Policy Service] API, leia o guia [de](./getting-started.md) introdução e selecione um dos guias de ponto de extremidade para saber como usar pontos de extremidade específicos. Para trabalhar com etiquetas e políticas usando a [!DNL Experience Platform] interface do usuário, consulte o guia [do usuário de](../labels/user-guide.md) etiquetas e o guia [de usuário de](../policies/user-guide.md)políticas, respectivamente.