---
keywords: Experience Platform;página inicial;tópicos populares;sandbox;Sandbox;teste;Teste
solution: Experience Platform
title: Visão geral de sandboxes
description: As sandboxes são partições virtuais dentro de uma única instância do Experience Platform, o que permite uma integração perfeita com o processo de desenvolvimento de seus aplicativos de experiência digital.
exl-id: b760a979-8134-4a44-8433-ec6fb49bc508
source-git-commit: 7ee472294e8f255d9de3c15982a6f5d2d3654755
workflow-type: tm+mt
source-wordcount: '971'
ht-degree: 0%

---

# Visão geral de sandboxes

O Adobe Experience Platform foi criado para enriquecer aplicativos de experiência digital em escala global. As empresas geralmente executam vários aplicativos de experiência digital em paralelo e precisam atender ao desenvolvimento, ao teste e à implantação desses aplicativos enquanto garantem a conformidade operacional.

Para atender a essa necessidade, o Experience Platform fornece sandboxes que particionam uma única instância da Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

Este documento fornece uma visão geral de alto nível das sandboxes no Experience Platform.

## Noções básicas sobre sandboxes

As sandboxes são partições virtuais dentro de uma única instância do Experience Platform, o que permite uma integração perfeita com o processo de desenvolvimento de seus aplicativos de experiência digital. Todo o conteúdo e as ações realizadas em uma sandbox estão confinados somente a essa sandbox e não afetam outras sandboxes. Há dois tipos de sandboxes compatíveis com o Experience Platform:

* **Sandbox de produção**: uma sandbox de produção deve ser usada com perfis em seu ambiente de produção. A Platform permite criar várias sandboxes de produção para fornecer a funcionalidade certa para os dados e, ao mesmo tempo, manter o isolamento operacional. Esse recurso permite dedicar sandboxes de produção específicas a linhas de negócios, marcas, projetos ou regiões distintas. As sandboxes de produção oferecem suporte a um volume de perfis de produção até o compromisso licenciado do [!DNL Profile] (medido cumulativamente em todas as sandboxes de produção autorizadas). Você está autorizado a usar todo o volume total de dados licenciado (medido cumulativamente em todas as sandboxes de produção autorizadas).

* **Sandbox de desenvolvimento**: uma sandbox de desenvolvimento é uma sandbox que pode ser usada exclusivamente para desenvolvimento e teste com perfis de não produção. As sandboxes de desenvolvimento são compatíveis com um volume de perfis de não produção até 10% do comprometimento do [!DNL Profile] licenciado (medido cumulativamente em todas as sandboxes de desenvolvimento autorizadas). Você tem direito a até:
   * Um trabalho de segmentação em lote por dia, por sandbox de desenvolvimento;
   * Uma média de 120 chamadas de API do [!DNL Profile], por [!DNL Profile], por ano (medidas cumulativamente em todas as sandboxes de desenvolvimento autorizadas).

Uma instância do Experience Platform é compatível com várias sandboxes de produção e desenvolvimento, com cada sandbox mantendo sua própria biblioteca independente de recursos da plataforma (incluindo esquemas, conjuntos de dados, perfis e assim por diante). Além disso, as sandboxes de produção e desenvolvimento têm um recurso de redefinição que remove da sandbox todos os recursos criados pelo cliente. Sandboxes de desenvolvimento não podem ser convertidas em sandboxes de produção.

Uma licença de Experience Platform padrão concede um total de cinco sandboxes, que você pode classificar como produção ou desenvolvimento. Você pode licenciar pacotes adicionais de 10 sandboxes até um máximo de 75 sandboxes no total. Essas sandboxes adicionais podem ser usadas para criar sandboxes de produção e desenvolvimento. Entre em contato com o administrador da organização ou com o representante de vendas da Adobe para obter mais detalhes.

Por fim, a sandbox de produção padrão é a primeira sandbox de produção criada quando uma organização é criada pela primeira vez. A sandbox de produção padrão permite assimilar ou consumir dados da Platform, bem como aceitar solicitações que não incluem valores para um nome de sandbox ou uma ID de sandbox.

>[!NOTE]
>
>Quando uma sandbox é criada pela primeira vez, ela não contém dados. Como cada sandbox mantém seu próprio armazenamento de dados isolado, elas também devem assimilar seus dados independentemente.

Em resumo, as sandboxes oferecem os seguintes benefícios:

* **Gerenciamento do ciclo de vida do aplicativo**: crie ambientes virtuais separados para desenvolver aplicativos de experiência digital.
* **Gerenciamento de projetos e marcas**: permite que vários projetos sejam executados em paralelo na mesma organização, fornecendo isolamento e controle de acesso.
* **Ecossistema de desenvolvimento flexível**: forneça sandboxes de forma contínua, escalável e econômica para fins de exploração, capacitação e demonstração.

## Controle de acesso para sandboxes

Por padrão, todos os usuários de uma organização têm acesso a uma sandbox de produção. O acesso às sandboxes de não produção deve ser concedido por um administrador do sistema, administrador do produto ou administrador do perfil do produto por meio do [Adobe Admin Console](https://adminconsole.adobe.com).

Para exibir, criar, atualizar ou excluir sandboxes de não produção, os usuários também devem receber permissões de Administração de sandbox.

Para obter mais informações sobre como gerenciar funções e permissões para sandboxes, consulte a [visão geral do controle de acesso](../access-control/home.md).

## Sandboxes na interface do Experience Platform

Na [interface de usuário Experience Platform](https://platform.adobe.com), os usuários podem alternar entre as sandboxes às quais têm acesso usando o controle **alternador de sandbox** no canto superior esquerdo da tela.  Os usuários com privilégios de Administração de sandbox também têm acesso à guia **[!UICONTROL Sandboxes]** na navegação à esquerda, onde podem exibir e gerenciar sandboxes para sua organização. Para obter mais informações sobre como trabalhar com sandboxes na interface do usuário, consulte o [guia do usuário da sandbox](ui/overview.md).

## Sandboxes em APIs Experience Platform

Ao fazer chamadas para APIs Experience Platform, um nome de sandbox deve ser fornecido sob o cabeçalho `x-sandbox-name`. Por exemplo, ao chamar o [[!DNL Catalog Service API]](https://www.adobe.io/experience-platform-apis/references/catalog/) para exibir todos os conjuntos de dados na sandbox de Produção, o nome da sandbox (&quot;prod&quot;) é fornecido como um cabeçalho na solicitação da API:

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: prod'
```

Se `x-sandbox-name` não estiver incluído em uma chamada de API, o sistema usará uma sandbox padrão. No entanto, a prática recomendada é sempre incluir esse cabeçalho em todas as chamadas de API, mesmo ao usar a sandbox padrão. Por isso, a documentação da API do Experience Platform trata `x-sandbox-name` como um cabeçalho obrigatório.

### API de sandbox

A API de sandbox permite gerenciar sandboxes usando operações da API RESTful. Consulte o [guia do desenvolvedor da sandbox](api/overview.md) para obter informações detalhadas sobre como usar a API, incluindo solicitações formatadas corretamente e respostas de exemplo.

## Próximas etapas

Ao ler este documento, você foi apresentado aos conceitos essenciais sobre sandboxes no Experience Platform. Para obter etapas detalhadas sobre como gerenciar sandboxes, consulte o [guia do usuário](ui/overview.md) para a interface ou o [guia do desenvolvedor](./api/getting-started.md) para a API.

Embora as sandboxes sirvam como uma ferramenta valiosa para isolar ambientes da Platform para a sua equipe de desenvolvimento, você também pode gerenciar um controle de acesso mais granular usando o Adobe Admin Console. Consulte a [visão geral do controle de acesso](../access-control/home.md) para obter mais informações.
