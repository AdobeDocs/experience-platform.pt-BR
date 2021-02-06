---
keywords: Experience Platform;home;populares tópicos
solution: Experience Platform
title: Guia da API do Serviço de Política
topic: developer guide
description: A API de serviço de política permite que os desenvolvedores gerenciem as etiquetas e políticas de uso de dados no Experience Platform. Siga este guia para saber como executar operações principais usando a API.
translation-type: tm+mt
source-git-commit: e649ab3da077cdd8e98562199b8bdece6108a572
workflow-type: tm+mt
source-wordcount: '504'
ht-degree: 0%

---


# [!DNL Policy Service] Guia de API

A Adobe Experience Platform [!DNL Data Governance] permite gerenciar dados do cliente e garantir a conformidade com regulamentos, restrições e políticas aplicáveis ao uso de dados. Ele desempenha um papel fundamental em [!DNL Experience Platform] em vários níveis, incluindo a catalogação, a linhagem de dados, a rotulagem de uso de dados, as políticas de uso de dados e o controle do uso de dados para ações de marketing.

A API [!DNL Policy Service] fornece vários endpoints que permitem gerenciar programaticamente rótulos e políticas de uso de dados, bem como avaliar ações de marketing para violações de políticas. Esses pontos finais são descritos abaixo. Visite os guias de ponto de extremidade individuais para obter detalhes e consulte o [guia de introdução](./getting-started.md) para obter informações importantes sobre cabeçalhos necessários, como ler amostras de chamadas de API e muito mais.

Para visualização de todos os pontos de extremidade e operações CRUD disponíveis, visite o [[!DNL Policy Service] swagger de API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml).

## Rótulos

Rótulos de uso de dados permitem categorizar conjuntos de dados e campos de acordo com as políticas de uso que se aplicam a esses dados. As etiquetas podem ser aplicadas a qualquer momento, proporcionando flexibilidade na forma como você escolhe administrar os dados. As práticas recomendadas incentivam a rotulação de dados assim que eles são ingeridos em [!DNL Experience Platform], ou assim que os dados estiverem disponíveis para uso em [!DNL Platform]. Você pode criar, visualização, editar e excluir rótulos usando o terminal `/labels`. Para saber como usar esse terminal, visite o [guia de endpoint de etiquetas](./labels.md).

## Ações de marketing

As ações de marketing (também chamadas de casos de uso de marketing), no contexto da estrutura [!DNL Data Governance], são ações que um [!DNL Experience Platform] consumidor de dados pode realizar, para as quais sua organização deseja restringir o uso de dados. Para obter informações detalhadas sobre como trabalhar com ações de marketing, consulte o [guia de ponto de extremidade de ações de marketing](./marketing-actions.md).

## Políticas

As políticas de uso de dados são regras que descrevem os tipos de ações de marketing às quais você tem permissão ou é restrito para executar em dados em [!DNL Experience Platform]. Uma política é definida pelo seguinte:

1. Uma ação de marketing específica
1. Os rótulos de uso de dados com os quais a ação está restrita não são executados

Para saber como gerenciar políticas na API, consulte o [guia do ponto de extremidade de políticas](./policies.md)

## Avaliação

Depois que os rótulos de uso de dados forem aplicados a [!DNL Platform] conjuntos de dados, e as políticas de uso de dados tiverem sido definidas para ações de marketing contra esses rótulos, os recursos do Data Governance permitirão que você aplique essas políticas e previna operações de dados que constituam violações de política.

A API [!DNL Policy Service] fornece pontos de extremidade que permitem testar ações de marketing em relação a conjuntos de dados ou combinações arbitrárias de rótulos de uso de dados para verificar se ocorrem violações de política. Com base na resposta da API, você pode configurar protocolos dentro do aplicativo de experiência para aplicar adequadamente a conformidade da política de uso de dados. Consulte o [guia de pontos de extremidade de avaliação](./evaluation.md) para obter mais informações.

## Próximas etapas

Para começar a fazer chamadas usando a API [!DNL Policy Service], leia o [guia de introdução](./getting-started.md) e selecione um dos guias de ponto de extremidade para saber como usar pontos de extremidade específicos. Para trabalhar com etiquetas e políticas usando a interface do usuário [!DNL Experience Platform], consulte [guia do usuário de etiquetas](../labels/user-guide.md) e [guia do usuário de políticas](../policies/user-guide.md), respectivamente.