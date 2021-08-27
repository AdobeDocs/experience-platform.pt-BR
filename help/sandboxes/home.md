---
keywords: Experience Platform, home, tópicos populares, sandbox, sandbox, teste, teste
solution: Experience Platform
title: Visão geral das sandboxes
topic-legacy: overview
description: As sandboxes são partições virtuais em uma única instância do Experience Platform, o que permite uma integração perfeita com o processo de desenvolvimento de seus aplicativos de experiência digital.
exl-id: b760a979-8134-4a44-8433-ec6fb49bc508
source-git-commit: 5160bc8057a7f71e6b0f7f2d594ba414bae9d8f6
workflow-type: tm+mt
source-wordcount: '1005'
ht-degree: 0%

---

# Visão geral das sandboxes

O Adobe Experience Platform foi criado para enriquecer os aplicativos de experiência digital em escala global. Geralmente, as empresas executam vários aplicativos de experiência digital em paralelo e precisam atender ao desenvolvimento, teste e implantação desses aplicativos, além de garantir a conformidade operacional.

Para atender a essa necessidade, o Experience Platform fornece sandboxes que particionam uma única instância da Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

Este documento fornece uma visão geral de alto nível das sandboxes no Experience Platform.

## Noções básicas sobre sandboxes

As sandboxes são partições virtuais em uma única instância do Experience Platform, o que permite uma integração perfeita com o processo de desenvolvimento de seus aplicativos de experiência digital. Todo o conteúdo e as ações realizadas em uma sandbox são restritas apenas a essa sandbox e não afetam nenhuma outra sandbox. Há dois tipos de sandboxes compatíveis com o Experience Platform:

* **Caixa de proteção** de produção: Uma sandbox de produção deve ser usada com perfis no ambiente de produção. A Platform permite criar várias sandboxes de produção para fornecer a funcionalidade correta para os dados, mantendo o isolamento operacional. Esse recurso permite dedicar sandboxes de produção específicas a linhas distintas de negócios, marcas, projetos ou regiões. As sandboxes de produção oferecem suporte a um volume de perfis de produção até o compromisso [!DNL Profile] licenciado (medido cumulativamente em todas as sandboxes de produção autorizadas). Você tem direito a usar o perfil médio licenciado por [!DNL Profile] autorizado (medido cumulativamente em todas as sandboxes de produção autorizadas).
* **Sandbox** de desenvolvimento: Uma sandbox de desenvolvimento é uma sandbox que pode ser usada exclusivamente para desenvolvimento e testes com perfis não relacionados à produção. As sandboxes de desenvolvimento oferecem suporte a um volume de perfis de não produção de até 10% do compromisso [!DNL Profile] licenciado (medido cumulativamente em todas as sandboxes de desenvolvimento autorizadas). Você tem direito a até:
   * Uma riqueza média de perfis de não produção de 75 quilobytes por perfil de não produção autorizado (medida cumulativamente em todas as sandboxes de desenvolvimento autorizadas);
   * Um trabalho de segmentação em lote por dia, por sandbox de desenvolvimento;
   * Uma média de 120 [!DNL Profile] chamadas de API, por [!DNL Profile], por ano (medidas cumulativamente em todas as sandboxes de desenvolvimento autorizadas.

Uma instância do Experience Platform suporta várias sandboxes de produção e desenvolvimento, com cada sandbox mantendo sua própria biblioteca independente de recursos da plataforma (incluindo esquemas, conjuntos de dados, perfis e assim por diante). Além disso, as sandboxes de produção e desenvolvimento têm um recurso de redefinição que remove todos os recursos criados pelo cliente da sandbox. As sandboxes de desenvolvimento não podem ser convertidas em sandboxes de produção.

Uma licença Experience Platform padrão concede um total de cinco sandboxes, que podem ser classificadas como produção ou desenvolvimento. Você pode licenciar pacotes adicionais de 10 sandboxes até um máximo de 75 sandboxes no total. Essas sandboxes adicionais podem ser usadas para criar sandboxes de produção e desenvolvimento. Entre em contato com o administrador de organização IMS ou o representante de vendas de Adobe para obter mais detalhes.

Finalmente, a sandbox de produção padrão é a primeira sandbox de produção criada quando uma Org de IMS é criada pela primeira vez. A sandbox de produção padrão permite assimilar ou consumir dados da Platform, bem como aceitar solicitações que não incluem valores para um nome de sandbox ou ID de sandbox.

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

Ao fazer chamadas para APIs do Experience Platform, um nome de sandbox deve ser fornecido no cabeçalho `x-sandbox-name`. Por exemplo, ao chamar o [[!DNL Catalog Service API]](https://www.adobe.io/experience-platform-apis/references/catalog/) para exibir todos os conjuntos de dados na sandbox de produção, o nome da sandbox (&quot;prod&quot;) é fornecido como um cabeçalho na solicitação da API:

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

A API de sandbox permite gerenciar sandboxes usando operações de RESTful API. Consulte o [guia do desenvolvedor do sandbox](api/overview.md) para obter informações detalhadas sobre como usar a API, incluindo solicitações formatadas corretamente e respostas de exemplo.

## Próximas etapas

Ao ler este documento, você foi apresentado aos conceitos essenciais sobre sandboxes no Experience Platform. Para obter etapas detalhadas sobre como gerenciar sandboxes, consulte o [guia do usuário](ui/overview.md) para a interface do usuário ou o [guia do desenvolvedor](./api/getting-started.md) para a API.

Embora as sandboxes sirvam como uma ferramenta valiosa para isolar ambientes da plataforma para sua equipe de desenvolvimento, você também pode gerenciar um controle de acesso mais granular usando a Adobe Admin Console. Consulte a [visão geral do controle de acesso](../access-control/home.md) para obter mais informações.
