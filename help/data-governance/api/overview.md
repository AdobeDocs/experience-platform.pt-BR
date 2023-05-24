---
keywords: Experience Platform;página inicial;tópicos populares
solution: Experience Platform
title: Guia da API do Serviço de política
description: A API de serviço de política permite que os desenvolvedores gerenciem rótulos e políticas de uso de dados no Experience Platform. Siga este manual para saber como executar operações importantes usando a API.
exl-id: 23c05670-7107-4b96-bc24-0a51b5d267b2
source-git-commit: 0c09db51d97bc0cf321c5d2fd57c42d194b25d5f
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 4%

---

# [!DNL Policy Service] Manual da API

O Adobe Experience Platform Data Governance permite gerenciar dados de clientes e garantir conformidade com regulamentos, restrições e políticas aplicáveis ao uso de dados. Desempenha um papel fundamental na [!DNL Experience Platform] em vários níveis, incluindo catalogação, linhagem de dados, rotulagem de uso de dados, políticas de uso de dados e controle do uso de dados para ações de marketing.

A variável [!DNL Policy Service] A API fornece vários endpoints que permitem gerenciar programaticamente rótulos e políticas de uso de dados, bem como avaliar ações de marketing para violações de política. Esses endpoints são descritos abaixo. Acesse os manuais de endpoint individuais para obter detalhes e consulte a [guia de introdução](./getting-started.md) para obter informações importantes sobre cabeçalhos necessários, ler chamadas de API de exemplo e muito mais.

Para exibir todos os endpoints e operações CRUD disponíveis, visite o [[!DNL Policy Service] API swagger](https://www.adobe.io/experience-platform-apis/references/policy-service/).

## Rótulos

Aplicar rótulos de uso de dados a esquemas para categorizar conjuntos de dados e campos de acordo com as políticas de uso que se aplicam a esses dados. Os rótulos podem ser aplicados a qualquer momento, proporcionando flexibilidade na maneira como você escolhe controlar os dados. As práticas recomendadas incentivam a rotulagem de dados assim que eles são assimilados na [!DNL Experience Platform]ou assim que os dados estiverem disponíveis para uso no [!DNL Platform]. É possível criar, exibir, editar e excluir rótulos usando a `/labels` terminal. Para saber como usar este endpoint, visite o [guia de endpoint de rótulos](./labels.md).

## Ações de marketing

As ações de marketing (também chamadas de casos de uso de marketing), no contexto da estrutura de governança de dados, são ações que [!DNL Experience Platform] o consumidor de dados pode aceitar, para o qual sua organização deseja restringir o uso de dados. Para obter informações detalhadas sobre como trabalhar com ações de marketing, consulte [manual de endpoint de ações de marketing](./marketing-actions.md).

## Políticas

As políticas de governança de dados são regras que descrevem os tipos de ações de marketing que você tem permissão ou restrição para realizar em dados dentro do [!DNL Experience Platform].

>[!NOTE]
>
>As políticas de governança de dados não devem ser confundidas com as políticas de controle de acesso, que determinam os atributos de dados específicos que podem ser acessados por determinados usuários da Platform em sua organização. Consulte o guia sobre [controle de acesso baseado em atributos](../../access-control/abac/overview.md) para obter mais informações.

Uma política de governança de dados é definida pelo seguinte:

1. Uma ação de marketing específica
1. Os rótulos de uso de dados nos quais a ação está restrita de ser executada

Para saber como gerenciar políticas na API, consulte a [manual de endpoint de políticas](./policies.md)

## Avaliação

Depois que os rótulos de uso de dados tiverem sido aplicados aos esquemas da plataforma e as políticas de uso de dados tiverem sido definidas para ações de marketing com relação a esses rótulos, os recursos de Governança de dados permitirão aplicar essas políticas e impedir operações de dados que constituem violações de política.

A variável [!DNL Policy Service] A API fornece endpoints que permitem testar ações de marketing em relação a conjuntos de dados ou combinações arbitrárias de rótulos de uso de dados para verificar se ocorrem violações de política. Com base na resposta da API, é possível configurar protocolos no aplicativo de experiência para aplicar adequadamente a conformidade com a política de uso de dados. Consulte a [guia de endpoints de avaliação](./evaluation.md) para obter mais informações.

## Próximas etapas

Para começar a fazer chamadas usando o [!DNL Policy Service] API, leia as [guia de introdução](./getting-started.md) em seguida, selecione um dos manuais de endpoint para saber como usar endpoints específicos. Para trabalhar com rótulos e políticas usando o [!DNL Experience Platform] Interface do usuário do, consulte a [guia do usuário de rótulos](../labels/user-guide.md) e [guia do usuário de políticas](../policies/user-guide.md), respectivamente.
