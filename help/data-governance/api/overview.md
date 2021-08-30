---
keywords: Experience Platform, home, tópicos populares
solution: Experience Platform
title: Guia da API do Serviço de Política
topic-legacy: developer guide
description: A API do Serviço de política permite aos desenvolvedores gerenciar rótulos e políticas de uso de dados no Experience Platform. Siga este manual para saber como executar operações importantes usando a API.
exl-id: 23c05670-7107-4b96-bc24-0a51b5d267b2
source-git-commit: 8133804076b1c0adf2eae5b748e86a35f3186d14
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 5%

---

# [!DNL Policy Service] Manual da API

O Adobe Experience Platform [!DNL Data Governance] permite gerenciar os dados do cliente e garantir a conformidade com regulamentos, restrições e políticas aplicáveis ao uso de dados. Ele desempenha uma função essencial em [!DNL Experience Platform] em vários níveis, incluindo catálogos, linhagem de dados, rotulagem de uso de dados, políticas de uso de dados e controle o uso de dados para ações de marketing.

A API [!DNL Policy Service] fornece vários endpoints que permitem gerenciar programaticamente rótulos e políticas de uso de dados, bem como avaliar ações de marketing para violações de política. Esses endpoints são descritos abaixo. Visite os guias de ponto de extremidade individuais para obter detalhes e consulte o [guia de introdução](./getting-started.md) para obter informações importantes sobre cabeçalhos necessários, como ler chamadas de API de exemplo e muito mais.

Para exibir todos os pontos de extremidade disponíveis e operações CRUD, visite o [[!DNL Policy Service] API swagger](https://www.adobe.io/experience-platform-apis/references/policy-service/).

## Rótulos

Os rótulos de uso de dados permitem categorizar os conjuntos de dados e campos de acordo com as políticas de uso que se aplicam a esses dados. Rótulos podem ser aplicados a qualquer momento, fornecendo flexibilidade na maneira como você decide controlar os dados. As práticas recomendadas incentivam a rotulagem de dados assim que eles são assimilados em [!DNL Experience Platform], ou assim que os dados forem disponibilizados para uso em [!DNL Platform]. Você pode criar, exibir, editar e excluir rótulos usando o ponto de extremidade `/labels`. Para saber como usar esse endpoint, visite o [guia de endpoint de rótulos](./labels.md).

## Ações de marketing

As ações de marketing (também chamadas de casos de uso de marketing), no contexto da estrutura [!DNL Data Governance], são ações que um consumidor de dados [!DNL Experience Platform] pode realizar, para as quais sua organização deseja restringir o uso de dados. Para obter informações detalhadas sobre como trabalhar com ações de marketing, consulte o [guia de ponto de extremidade de ações de marketing](./marketing-actions.md).

## Políticas

As políticas de uso de dados são regras que descrevem os tipos de ações de marketing às quais você tem permissão ou é restrito, executando em dados dentro de [!DNL Experience Platform]. Uma política é definida pelo seguinte:

1. Uma ação de marketing específica
1. Os rótulos de uso de dados com os quais a ação está restrita não são executados

Para saber como gerenciar políticas na API, consulte o [guia do ponto de extremidade de políticas](./policies.md)

## Avaliação

Depois que os rótulos de uso de dados tiverem sido aplicados a [!DNL Platform] conjuntos de dados e as políticas de uso de dados tiverem sido definidas para ações de marketing em relação a esses rótulos, os recursos de Governança de dados permitirão aplicar essas políticas e evitar operações de dados que constituem violações de política.

A API [!DNL Policy Service] fornece endpoints que permitem testar ações de marketing em relação a conjuntos de dados ou combinações arbitrárias de rótulos de uso de dados para verificar se ocorrem violações de política. Com base na resposta da API, você pode configurar protocolos no aplicativo de experiência para impor adequadamente a conformidade da política de uso de dados. Consulte o [guia de endpoints de avaliação](./evaluation.md) para obter mais informações.

## Próximas etapas

Para começar a fazer chamadas usando a API [!DNL Policy Service], leia o [guia de introdução](./getting-started.md) e selecione um dos guias de ponto de extremidade para saber como usar endpoints específicos. Para trabalhar com rótulos e políticas usando a interface [!DNL Experience Platform], consulte o [guia do usuário de rótulos](../labels/user-guide.md) e [guia do usuário de políticas](../policies/user-guide.md), respectivamente.
