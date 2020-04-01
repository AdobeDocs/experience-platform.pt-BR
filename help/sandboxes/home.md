---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Visão geral das caixas de proteção
topic: overview
translation-type: tm+mt
source-git-commit: 564940f37b66159c84ca7402bd3648010232182b

---


# Visão geral das caixas de proteção

A plataforma Adobe Experience foi criada para enriquecer aplicativos de experiência digital em escala global. O Empresa geralmente executa vários aplicativos de experiência digital em paralelo e precisa atender ao desenvolvimento, teste e implantação desses aplicativos, garantindo a conformidade operacional.

Para atender a essa necessidade, a plataforma Experience fornece **caixas de proteção** que dividem uma única instância da plataforma em ambientes virtuais separados para ajudar a desenvolver e desenvolver aplicativos de experiência digital.

Este documento fornece uma visão geral de alto nível das caixas de proteção na Experience Platform.

## Como entender as caixas de proteção

As caixas de proteção são partições virtuais em uma única instância da Experience Platform, que permite uma integração perfeita com o processo de desenvolvimento de seus aplicativos de experiência digital. Uma instância da plataforma Experience suporta uma caixa de proteção de produção e várias caixas de proteção que não sejam de produção, com cada caixa de proteção mantendo sua própria biblioteca independente de recursos da plataforma (incluindo schemas, conjuntos de dados, perfis e assim por diante).  Todo o conteúdo e as ações realizadas em uma caixa de proteção estão confinados apenas a essa caixa de proteção e não afetam nenhuma outra caixa de proteção.

As caixas de proteção de não-produção permitem testar recursos, executar experimentos e fazer configurações personalizadas sem afetar sua caixa de proteção de produção. Além disso, as caixas de proteção de não produção têm um recurso de redefinição que remove todos os recursos criados pelo cliente da caixa de proteção. As caixas de proteção de não produção não podem ser convertidas em caixas de proteção de produção.

>[!NOTE] Quando uma caixa de proteção é criada pela primeira vez, ela não contém dados. Como cada caixa de proteção mantém seu próprio armazenamento de dados isolado, eles também devem ingerir seus dados de forma independente.

Em resumo, as caixas de proteção oferecem os seguintes benefícios:

* **Gerenciamento** do ciclo de vida do aplicativo: Crie ambientes virtuais separados para desenvolver e desenvolver aplicativos de experiência digital.
* **Gerenciamento** de projetos e marcas: Permita que vários projetos sejam executados em paralelo na mesma Organização IMS, além de fornecer isolamento e controle de acesso. As versões futuras oferecerão suporte para implantação em várias regiões.
* **Ecossistema** de desenvolvimento flexível: Forneça caixas de proteção de uma forma contínua, escalável e econômica para fins de exploração, ativação e demonstração.

## Controle de acesso para caixas de proteção

Por padrão, todos os usuários de uma organização têm acesso a uma caixa de proteção de produção. O acesso a caixas de proteção que não sejam de produção deve ser concedido por um administrador do sistema, administrador do produto ou administrador do perfil do produto por meio do [Adobe Admin Console](https://adminconsole.adobe.com).

Para visualização, criar, atualizar ou excluir caixas de proteção que não sejam de produção, os usuários também devem receber permissões de Administração de caixa de proteção.

Para obter mais informações sobre como gerenciar funções e permissões para caixas de proteção, consulte a visão geral [do](../access-control/home.md)controle de acesso.

## Caixas de proteção na interface do usuário da plataforma de experiência

Na interface [do usuário da plataforma](https://platform.adobe.com)Experience, os usuários podem alternar entre as caixas de proteção às quais têm acesso usando o controle do alternador **de** caixa de proteção na parte superior esquerda da tela.  Os usuários com privilégios de Administração de Sandbox também têm acesso à guia **Sandboxes** na navegação à esquerda, onde podem visualização e gerenciar caixas de proteção para sua organização. Para obter mais informações sobre como trabalhar com caixas de proteção na interface do usuário, consulte o guia [do usuário da](ui/overview.md)caixa de proteção.

## Caixas de proteção nas APIs da plataforma Experience

Ao fazer chamadas para APIs da plataforma Experience, um nome de caixa de proteção deve ser fornecido no cabeçalho `x-sandbox-name`. Por exemplo, ao fazer uma chamada para a API [do serviço de](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) catálogo para visualização de todos os conjuntos de dados na caixa de proteção Produção, o nome da caixa de proteção (&quot;prod&quot;) é fornecido como um cabeçalho na solicitação da API:

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: prod'
```

Se não `x-sandbox-name` estiver incluído em uma chamada de API, o sistema usará uma caixa de proteção padrão. No entanto, a prática recomendada é sempre incluir esse cabeçalho em todas as chamadas de API, mesmo quando usar a caixa de proteção padrão. Por esse motivo, a documentação da API para a Experience Platform trata `x-sandbox-name` como um cabeçalho obrigatório.

### API do Sandbox

A API Sandbox permite gerenciar caixas de proteção usando operações RESTful API. Consulte o guia [do desenvolvedor da](api/getting-started.md) caixa de proteção para obter informações detalhadas sobre como usar a API, incluindo solicitações formatadas corretamente e respostas de exemplo.

## Próximas etapas

Ao ler este documento, você foi apresentado aos conceitos essenciais sobre caixas de proteção na Experience Platform. Para obter etapas detalhadas sobre como gerenciar caixas de proteção, consulte o guia [do](ui/overview.md) usuário para a interface do usuário ou o guia [do](./api/getting-started.md) desenvolvedor para a API.

Embora as caixas de proteção sirvam como uma ferramenta valiosa para isolar ambientes da plataforma para sua equipe de desenvolvimento, você também pode gerenciar controles de acesso mais detalhados usando o Adobe Admin Console. Consulte a visão geral [do](../access-control/home.md) controle de acesso para obter mais informações.