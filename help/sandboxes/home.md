---
keywords: Experience Platform, home, tópicos populares, sandbox, sandbox, teste, teste
solution: Experience Platform
title: Visão geral das sandboxes
topic: visão geral
description: As sandboxes são partições virtuais em uma única instância do Experience Platform, o que permite uma integração perfeita com o processo de desenvolvimento de seus aplicativos de experiência digital.
translation-type: tm+mt
source-git-commit: 62ce5ac92d03a6e85589fc92e8d953f7fc1d8f31
workflow-type: tm+mt
source-wordcount: '755'
ht-degree: 0%

---


# Visão geral das sandboxes

O Adobe Experience Platform foi criado para enriquecer os aplicativos de experiência digital em escala global. Geralmente, as empresas executam vários aplicativos de experiência digital em paralelo e precisam atender ao desenvolvimento, teste e implantação desses aplicativos, além de garantir a conformidade operacional.

Para atender a essa necessidade, o Experience Platform fornece sandboxes que particionam uma única instância da Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

Este documento fornece uma visão geral de alto nível das sandboxes no Experience Platform.

## Noções básicas sobre sandboxes

As sandboxes são partições virtuais em uma única instância do Experience Platform, o que permite uma integração perfeita com o processo de desenvolvimento de seus aplicativos de experiência digital. Uma instância do Experience Platform suporta uma sandbox de produção e várias sandboxes de não produção, com cada sandbox mantendo sua própria biblioteca independente de recursos da plataforma (incluindo esquemas, conjuntos de dados, perfis e assim por diante).  Todo o conteúdo e as ações realizadas em uma sandbox são restritas apenas a essa sandbox e não afetam nenhuma outra sandbox.

As sandboxes de não produção permitem testar recursos, executar experimentos e fazer configurações personalizadas sem afetar a sandbox de produção. Além disso, as sandboxes de não produção têm um recurso de redefinição que remove todos os recursos criados pelo cliente da sandbox. As sandboxes de não produção não podem ser convertidas em sandboxes de produção. Uma licença padrão do Experience Platform concede cinco sandboxes (uma produção e quatro não produção). É possível adicionar pacotes de dez sandboxes de não produção até um máximo de 75 sandboxes no total. Entre em contato com o administrador de organização IMS ou o representante de vendas de Adobe para obter mais detalhes.

>[!NOTE]
>
>Quando uma sandbox é criada pela primeira vez, ela não contém dados. Como cada sandbox mantém seu próprio armazenamento de dados isolado, ele também deve assimilar seus dados de maneira independente.

Em resumo, as sandboxes oferecem os seguintes benefícios:

* **Gerenciamento** do ciclo de vida do aplicativo: Crie ambientes virtuais separados para desenvolver e desenvolver aplicativos de experiência digital.
* **Gerenciamento** de projetos e marcas: Permitir que vários projetos sejam executados em paralelo na mesma Organização IMS, fornecendo controle de isolamento e acesso. As versões futuras fornecerão suporte para implantação em várias regiões.
* **ecosistema** de desenvolvimento flexível: Fornecer sandboxes de uma maneira contínua, escalável e econômica para fins de exploração, ativação e demonstração.

## Controle de acesso para sandboxes

Por padrão, todos os usuários de uma organização têm acesso a uma sandbox de produção. O acesso a sandboxes de não produção deve ser concedido por um administrador de sistema, administrador de produto ou administrador de perfil de produto por meio do [Adobe Admin Console](https://adminconsole.adobe.com).

Para visualizar, criar, atualizar ou excluir sandboxes de não produção, os usuários também devem receber permissões de Administração de sandbox.

Para obter mais informações sobre o gerenciamento de funções e permissões para sandboxes, consulte a [visão geral do controle de acesso](../access-control/home.md).

## Sandboxes na interface do usuário do Experience Platform

Na [interface do usuário do Experience Platform](https://platform.adobe.com), os usuários podem alternar entre as sandboxes às quais têm acesso usando o controle **sandbox switcher** no canto superior esquerdo da tela.  Os usuários com privilégios de Administração de sandbox também têm acesso à guia **[!UICONTROL Sandboxes]** na navegação à esquerda, onde podem visualizar e gerenciar sandboxes para sua organização. Para obter mais informações sobre como trabalhar com sandboxes na interface do usuário, consulte o [guia do usuário da sandbox](ui/overview.md).

## Sandboxes em APIs do Experience Platform

Ao fazer chamadas para APIs do Experience Platform, um nome de sandbox deve ser fornecido no cabeçalho `x-sandbox-name`. Por exemplo, ao chamar o [[!DNL Catalog Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) para exibir todos os conjuntos de dados na sandbox de produção, o nome da sandbox (&quot;prod&quot;) é fornecido como um cabeçalho na solicitação da API:

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: prod'
```

Se `x-sandbox-name` não estiver incluído em uma chamada de API, o sistema usará uma sandbox padrão. No entanto, a prática recomendada é sempre incluir esse cabeçalho em todas as chamadas de API, mesmo ao usar a sandbox padrão. Por esse motivo, a documentação da API para Experience Platform trata `x-sandbox-name` como um cabeçalho necessário.

### API de sandbox

A API de sandbox permite gerenciar sandboxes usando operações de RESTful API. Consulte o [guia do desenvolvedor do sandbox](api/getting-started.md) para obter informações detalhadas sobre como usar a API, incluindo solicitações formatadas corretamente e respostas de exemplo.

## Próximas etapas

Ao ler este documento, você foi apresentado aos conceitos essenciais sobre sandboxes no Experience Platform. Para obter etapas detalhadas sobre como gerenciar sandboxes, consulte o [guia do usuário](ui/overview.md) para a interface do usuário ou o [guia do desenvolvedor](./api/getting-started.md) para a API.

Embora as sandboxes sirvam como uma ferramenta valiosa para isolar ambientes da plataforma para sua equipe de desenvolvimento, você também pode gerenciar um controle de acesso mais granular usando a Adobe Admin Console. Consulte a [visão geral do controle de acesso](../access-control/home.md) para obter mais informações.