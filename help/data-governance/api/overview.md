---
keywords: Experience Platform, home, tópicos populares
solution: Experience Platform
title: Guia da API do Serviço de Política
topic-legacy: developer guide
description: A API do Serviço de política permite aos desenvolvedores gerenciar rótulos e políticas de uso de dados no Experience Platform. Siga este manual para saber como executar operações importantes usando a API.
exl-id: 23c05670-7107-4b96-bc24-0a51b5d267b2
source-git-commit: 03e7863f38b882a2fbf6ba0de1755e1924e8e228
workflow-type: tm+mt
source-wordcount: '504'
ht-degree: 4%

---

# [!DNL Policy Service] Manual da API

A Governança de dados do Adobe Experience Platform permite gerenciar os dados do cliente e garantir a conformidade com regulamentos, restrições e políticas aplicáveis ao uso de dados. Ele desempenha um papel fundamental no [!DNL Experience Platform] em vários níveis, incluindo catalogação, linhagem de dados, rotulagem de uso de dados, políticas de uso de dados e controle do uso de dados para ações de marketing.

O [!DNL Policy Service] A API fornece vários endpoints que permitem gerenciar programaticamente rótulos e políticas de uso de dados, bem como avaliar ações de marketing para violações de política. Esses endpoints são descritos abaixo. Visite os guias de ponto de extremidade individuais para obter detalhes e consulte [guia de introdução](./getting-started.md) para obter informações importantes sobre cabeçalhos necessários, ler chamadas de API de exemplo e muito mais.

Para exibir todos os endpoints e operações CRUD disponíveis, visite a [[!DNL Policy Service] Swagger de API](https://www.adobe.io/experience-platform-apis/references/policy-service/).

## Rótulos

Os rótulos de uso de dados permitem categorizar os conjuntos de dados e campos de acordo com as políticas de uso que se aplicam a esses dados. Rótulos podem ser aplicados a qualquer momento, fornecendo flexibilidade na maneira como você decide controlar os dados. As práticas recomendadas incentivam a rotulagem de dados assim que eles forem assimilados em [!DNL Experience Platform]ou assim que os dados estiverem disponíveis para uso em [!DNL Platform]. Você pode criar, exibir, editar e excluir rótulos usando o `/labels` endpoint . Para saber como usar esse terminal, visite o [guia de endpoint de etiquetas](./labels.md).

## Ações de marketing

As ações de marketing (também chamadas de casos de uso de marketing), no contexto da estrutura de Governança de dados, são ações que [!DNL Experience Platform] o consumidor de dados pode assumir, para o qual sua organização deseja restringir o uso de dados. Para obter informações detalhadas sobre como trabalhar com ações de marketing, consulte o [guia do endpoint de ações de marketing](./marketing-actions.md).

## Políticas

As políticas de uso de dados são regras que descrevem os tipos de ações de marketing das quais você tem permissão para ou tem restrição para executar em dados dentro de [!DNL Experience Platform]. Uma política é definida pelo seguinte:

1. Uma ação de marketing específica
1. Os rótulos de uso de dados com os quais a ação está restrita não são executados

Para saber como gerenciar políticas na API, consulte o [guia do endpoint de políticas](./policies.md)

## Avaliação

Depois que os rótulos de uso de dados forem aplicados a [!DNL Platform] os conjuntos de dados e as políticas de uso de dados foram definidos para ações de marketing em relação a esses rótulos, os recursos de Governança de dados permitem que você imponha essas políticas e evite operações de dados que constituem violações de política.

O [!DNL Policy Service] A API fornece endpoints que permitem testar ações de marketing em relação a conjuntos de dados ou combinações arbitrárias de rótulos de uso de dados para verificar se ocorrem violações de política. Com base na resposta da API, você pode configurar protocolos no aplicativo de experiência para impor adequadamente a conformidade da política de uso de dados. Consulte a [guia de endpoints de avaliação](./evaluation.md) para obter mais informações.

## Próximas etapas

Para começar a fazer chamadas usando a variável [!DNL Policy Service] Leia a API do [guia de introdução](./getting-started.md) em seguida, selecione um dos guias de endpoint para saber como usar endpoints específicos. Para trabalhar com rótulos e políticas usando o [!DNL Experience Platform] Por favor, consulte a [guia do usuário de rótulos](../labels/user-guide.md) e [guia do usuário de políticas](../policies/user-guide.md), respectivamente.
