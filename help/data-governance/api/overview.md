---
keywords: Experience Platform;página inicial;tópicos populares
solution: Experience Platform
title: Guia da API do Serviço de política
description: A API de serviço de política permite que os desenvolvedores gerenciem rótulos e políticas de uso de dados no Experience Platform. Siga este manual para saber como executar operações importantes usando a API.
role: Developer
exl-id: 23c05670-7107-4b96-bc24-0a51b5d267b2
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '543'
ht-degree: 4%

---

# [!DNL Policy Service] Manual da API

O Adobe Experience Platform Data Governance permite gerenciar dados de clientes e garantir conformidade com regulamentos, restrições e políticas aplicáveis ao uso de dados. Ele desempenha uma função importante no [!DNL Experience Platform] em vários níveis, incluindo catalogação, linhagem de dados, rotulagem de uso de dados, políticas de uso de dados e controle do uso de dados para ações de marketing.

A API [!DNL Policy Service] fornece vários endpoints que permitem gerenciar de forma programática rótulos e políticas de uso de dados, bem como avaliar ações de marketing para violações de política. Esses endpoints são descritos abaixo. Visite os manuais de endpoint individuais para obter detalhes e consulte o [guia de introdução](./getting-started.md) para obter informações importantes sobre cabeçalhos necessários, como ler chamadas de API de exemplo e muito mais.

Para exibir todos os pontos de extremidade e operações CRUD disponíveis, visite o [[!DNL Policy Service] API swagger](https://www.adobe.io/experience-platform-apis/references/policy-service/).

## Rótulos

Aplicar rótulos de uso de dados a esquemas para categorizar conjuntos de dados e campos de acordo com as políticas de uso que se aplicam a esses dados. Os rótulos podem ser aplicados a qualquer momento, proporcionando flexibilidade na maneira como você escolhe controlar os dados. As práticas recomendadas incentivam a rotulagem de dados assim que eles forem assimilados no [!DNL Experience Platform] ou assim que os dados estiverem disponíveis para uso no [!DNL Platform]. Você pode criar, exibir, editar e excluir rótulos usando o ponto de extremidade `/labels`. Para saber como usar este ponto de extremidade, visite o [manual de ponto de extremidade de rótulos](./labels.md).

## Ações de marketing

As ações de marketing (também chamadas de casos de uso de marketing), no contexto da estrutura de Governança de dados, são ações que um consumidor de dados do [!DNL Experience Platform] pode realizar, para as quais sua organização deseja restringir o uso de dados. Para obter informações detalhadas sobre como trabalhar com ações de marketing, consulte o [manual de endpoint de ações de marketing](./marketing-actions.md).

## Políticas

As políticas de governança de dados são regras que descrevem os tipos de ações de marketing que você tem permissão ou restrição para executar em dados no [!DNL Experience Platform].

>[!NOTE]
>
>As políticas de governança de dados não devem ser confundidas com as políticas de controle de acesso, que determinam os atributos de dados específicos que podem ser acessados por determinados usuários da Platform em sua organização. Consulte o manual sobre [controle de acesso baseado em atributos](../../access-control/abac/overview.md) para obter mais informações.

Uma política de governança de dados é definida pelo seguinte:

1. Uma ação de marketing específica
1. Os rótulos de uso de dados nos quais a ação está restrita de ser executada

Para saber como gerenciar políticas na API, consulte o [manual de ponto de extremidade de políticas](./policies.md)

## Avaliação

Depois que os rótulos de uso de dados tiverem sido aplicados aos esquemas da plataforma e as políticas de uso de dados tiverem sido definidas para ações de marketing com relação a esses rótulos, os recursos de Governança de dados permitirão aplicar essas políticas e impedir operações de dados que constituem violações de política.

A API [!DNL Policy Service] fornece endpoints que permitem testar ações de marketing em relação a conjuntos de dados ou combinações arbitrárias de rótulos de uso de dados para verificar se ocorrem violações de política. Com base na resposta da API, é possível configurar protocolos no aplicativo de experiência para aplicar adequadamente a conformidade com a política de uso de dados. Consulte o [manual de endpoints de avaliação](./evaluation.md) para obter mais informações.

## Próximas etapas

Para começar a fazer chamadas usando a API [!DNL Policy Service], leia o [guia de introdução](./getting-started.md) e selecione um dos manuais de endpoint para saber como usar endpoints específicos. Para trabalhar com rótulos e políticas usando a interface do usuário do [!DNL Experience Platform], consulte o [guia do usuário de rótulos](../labels/user-guide.md) e o [guia do usuário de políticas](../policies/user-guide.md), respectivamente.
