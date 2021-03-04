---
keywords: Experience Platform, home, tópicos populares, namespace de identidade, namespace de identidade
solution: Experience Platform
title: Guia de solução de problemas do serviço de identidade
topic: solução de problemas
description: Este documento fornece respostas a perguntas frequentes sobre o Adobe Experience Platform Identity Service, bem como um guia de solução de problemas para erros comuns.
translation-type: tm+mt
source-git-commit: 126b3d1cf6d47da73c6ab045825424cf6f99e5ac
workflow-type: tm+mt
source-wordcount: '2190'
ht-degree: 0%

---


# Guia de solução de problemas do Serviço de identidade

Este documento fornece respostas a perguntas frequentes sobre a Adobe Experience Platform [!DNL Identity Service], bem como um guia de solução de problemas para erros comuns. Em caso de dúvidas e solução de problemas relacionados às APIs [!DNL Platform] em geral, consulte o [Guia de solução de problemas da API da Adobe Experience Platform](../landing/troubleshooting.md).

Os dados que identificam um único cliente geralmente são fragmentados em vários dispositivos e sistemas que eles usam para interagir com sua marca. [!DNL Identity Service] O reúne essas identidades fragmentadas, facilitando uma compreensão completa do comportamento do cliente para que você possa oferecer experiências digitais impactantes em tempo real. Para obter mais informações, consulte a [Visão geral do Serviço de identidade](./home.md).

## Perguntas frequentes

Veja a seguir uma lista de respostas para perguntas frequentes sobre [!DNL Identity Service].

## O que são dados de identidade?

Dados de identidade são quaisquer dados que podem ser usados para identificar uma pessoa. Dependendo do contexto de como os dados são usados em sua organização, os dados de identidade podem incluir nomes de usuário, endereços de email e IDs de sistemas CRM. Os dados de identidade não estão limitados a usuários registrados do seu site ou serviço, pois usuários anônimos também podem ser identificados por seu dispositivo ou ID do cookie.

## Qual é o benefício de rotular campos de dados como identidades?

Rotular determinados campos de dados como identidades em seu registro e dados de séries de tempo permite mapear relações de identidade dentro da estrutura natural de seus dados e reconciliar dados duplicados entre canais. Consulte a [Visão geral do Serviço de identidade](./home.md) para obter mais informações.

## O que são identidades conhecidas e anônimas?

Uma identidade conhecida refere-se a um valor de identidade que pode ser usado isoladamente ou junto a outras informações para identificar, contactar ou localizar uma pessoa individual. Exemplos de identidades conhecidas podem incluir endereços de email, números de telefone e IDs de CRM.

Uma identidade anônima refere-se a um valor de identidade que não pode ser usado isoladamente ou junto a outras informações para identificar, contactar ou localizar uma pessoa individual (como uma ID de cookie).

## O que é um Gráfico de identidade privada?

Um Gráfico de identidade privada é um mapa privado de relações entre identidades vinculadas e unidas, visível somente para a sua organização.

Quando mais de uma identidade é incluída em qualquer dado assimilado de um endpoint de transmissão ou enviado para um conjunto de dados habilitado para [!DNL Identity Service], essas identidades são vinculadas no Gráfico de identidade privada. [!DNL Identity Service] usam esse gráfico para obter identidades de um determinado consumidor ou entidade, permitindo a identificação e a mesclagem de perfis.

## Como faço para criar vários campos de identidade dentro de um esquema XDM?

[Os esquemas do Experience Data Model (XDM)](../xdm/home.md)  suportam vários campos de identidade. Qualquer campo de dados do tipo `string` em um esquema que implemente o Perfil individual XDM ou a classe ExperienceEvent XDM pode ser rotulado como um campo de identidade. Depois de rotulados, os dados contidos nesses campos são adicionados ao mapa de identidade do perfil.

Para obter etapas sobre como rotular um campo XDM como um campo de identidade usando a interface do usuário, consulte a [seção Identidade](../xdm/tutorials/create-schema-ui.md) no tutorial do Editor de esquemas. Se estiver usando a API, consulte a seção [Descritor de identidade](../xdm/tutorials/create-schema-api.md) no tutorial da API do Registro de esquema.

## Há contextos em que alguns campos não devem ser rotulados como identidades?

Os campos de identidade devem ser reservados para valores exclusivos de cada indivíduo. Por exemplo, considere um conjunto de dados para um programa de fidelidade do cliente. O campo de &quot;nível de fidelidade&quot; (ouro, prata, bronze) não seria um campo de identidade útil, enquanto a ID de fidelidade - um valor exclusivo - seria.

Campos como CEPs e endereços IP não devem ser rotulados como identidades de indivíduos, pois esses valores podem se aplicar a mais de uma pessoa individual. Estes tipos de campos só devem ser rotulados como identidades para as estratégias de comercialização ao nível do agregado familiar.

## Por que meus campos de identidade não estão vinculando da maneira esperada?

Usando o ponto de extremidade [`/cluster/members`](./api/list-cluster-identites.md) na API do Serviço de identidade, é possível exibir as identidades associadas para um ou mais campos de identidade. Se a resposta não retornar as identidades vinculadas esperadas, forneça as informações de identidade apropriadas nos dados XDM. Consulte a seção [fornecendo dados XDM ao Serviço de identidade](./home.md) na visão geral do Serviço de identidade para obter mais informações.

## O que é um namespace de identidade?

Um namespace de identidade fornece contexto para como os campos de identidade estão relacionados à identidade de um cliente. Por exemplo, os campos de identidade no namespace &quot;Email&quot; devem estar em conformidade com um formato de email padrão (name<span>@emailprovider.com), enquanto os campos que usam o namespace &quot;Telefone&quot; devem estar em conformidade com um número de telefone padrão (como 987-555-1234 na América do Norte).

Os namespaces distinguem valores de identidade semelhantes entre diferentes sistemas CRM. Por exemplo, considere um perfil que contém uma ID de fidelidade numérica associada ao programa de recompensas da empresa. Um namespace de &quot;Fidelidade&quot; separaria esse valor de uma ID numérica semelhante para seu sistema de eCommerce, que também aparece no mesmo perfil.

Consulte a [visão geral do namespace de identidade](./home.md) para obter mais informações.

## Como associo uma identidade a um namespace de identidade?

Os campos de identidade devem ser associados a um namespace de identidade existente ao serem criados. Qualquer novo namespace deve ser [criado usando a API](#how-do-i-create-a-custom-namespace-for-my-organization) antes de associá-lo aos campos de identidade.

Para obter instruções passo a passo para definir um namespace ao criar um descritor de identidade usando a API, consulte a seção sobre [criar um descritor](../xdm/tutorials/create-schema-ui.md) no guia do desenvolvedor do Registro de Schema. Para marcar um campo de esquema como uma identidade na interface do usuário, siga as etapas no [Tutorial do Editor de esquemas](../xdm/tutorials/create-schema-api.md).

## Quais são os namespaces de identidade padrão fornecidos pela Experience Platform? {#standard-namespaces}

Os namespaces de identidade padrão são namespaces disponíveis para todas as organizações. Consulte a [Visão geral dos namespaces de identidade](./namespaces.md) para obter uma lista completa dos namespaces padrão disponíveis.

## Onde posso encontrar a lista de namespaces de identidade disponíveis para minha organização?

Usando a [API do Serviço de identidade](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/id-service-api.yaml), você pode listar todos os namespaces de identidade disponíveis para sua organização, fazendo uma solicitação GET para o endpoint `/idnamespace/identities`. Consulte a seção [listando namespaces disponíveis](./api/list-namespaces.md) na visão geral da API do Serviço de identidade para obter mais informações.

## Como criar um namespace personalizado para minha organização?

Usando a [API do Serviço de identidade](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/id-service-api.yaml), você pode criar um namespace de identidade personalizado para sua organização, fazendo uma solicitação POST para o endpoint `/idnamespace/identities`. Consulte a seção [criar um namespace personalizado](./api/create-custom-namespace.md) na visão geral da API do Serviço de identidade para obter mais informações.

## O que são identidades compostas e XIDs?

As identidades são referenciadas em chamadas de API por sua identidade composta ou XID. Uma identidade composta é uma representação de uma identidade que contém um valor de ID e um namespace. Um XID é um identificador de valor único que representa a mesma construção de uma identidade composta (uma ID e um namespace) e é automaticamente atribuído a novas identidades quando persistido pelo Serviço de identidade. Consulte a [Visão geral da API do serviço de identidade](./home.md) para obter mais informações.

## Como o Serviço de identidade lida com informações de identificação pessoal (PII)?

O Serviço de identidade cria um hash criptográfico de PII forte e unidirecional antes dos valores persistentes. Os dados de identidade nos namespaces &quot;Telefone&quot; e &quot;Email&quot; são automaticamente atribuídos a hash usando SHA-256, com valores de &quot;Email&quot; convertidos automaticamente em minúsculas antes do hash.

## Devo criptografar todas as PII antes de enviar para a Plataforma?

Não é necessário criptografar manualmente os dados de PII antes de assimilá-los na plataforma. Ao aplicar o rótulo de uso de dados `I1` a todos os campos de dados aplicáveis, a Platform converte automaticamente esses campos em valores de ID com hash após a assimilação.

Para obter etapas sobre como aplicar e gerenciar rótulos de uso de dados, consulte o [tutorial de rótulos de uso de dados](../data-governance/labels/user-guide.md).

## Existem considerações ao fazer o hash de identidades baseadas em PII?

Se você estiver enviando valores PII com hash para o Serviço de identidade, deverá usar o mesmo método de criptografia em seus conjuntos de dados. Isso garante que o mesmo valor de identidade entre conjuntos de dados gere os mesmos valores com hash e possa ser correspondido e vinculado corretamente no gráfico de identidade.

<!-- Documentation does not show any methods of editing the identityMap directly, and this table never overtly recommends using identityMap anyway. This should probably be removed unless PM thinks otherwise. -->
<!-- ## When should I use the Identity map rather than labeling individual XDM schema fields?

The following table describes when the recommended approach for including identity data in your XDM would be identity map and when an identity field is the better method.

>[!NOTE]
>
>An advantage `identityMap` has is the ability to include multiple identity values for a single namespace.

Write|XDM identity field|`identityMap`
---|---|---
UI|Supported|Supported
Developer|Recommended|Supported
ETL|Recommended|Avoid - While this is supported, data should be formatted naturally when using an ETL, favoring identity fields over `identityMap`.
Internal solutions|Preferred|Common

--- -->

## Solução de problemas

A seção a seguir fornece sugestões de solução de problemas para códigos de erro específicos e comportamento inesperado que você pode encontrar ao trabalhar com a API [!DNL Identity Service].

## [!DNL Identity Service] mensagens de erro

Veja a seguir uma lista de mensagens de erro que podem ser encontradas ao usar a API [!DNL Identity Service].

### Parâmetro de consulta necessário ausente

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Missing required query parameter - namespace"
}
```

Este erro é exibido quando um parâmetro de consulta obrigatório não foi incluído no caminho da solicitação. O `detail` da mensagem de erro fornece o nome do parâmetro ausente. As variações dessa mensagem de erro incluem:

- Parâmetro de consulta necessário ausente - nsId
- Parâmetro de consulta necessário ausente - id
- Parâmetro de consulta necessário ausente - xid ou (nsid,id)
- Parâmetro de consulta necessário ausente - targetNs
- Parâmetro de consulta necessário ausente - xids ou compostoXids

Verifique se você está incluindo corretamente o parâmetro indicado no caminho da solicitação antes de tentar novamente.

### O carimbo de data e hora deve estar nos últimos 180 dias

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Timestamp should be within last 180 days"
}
```

[!DNL Identity Service] limpa os dados com mais de 180 dias. Essa mensagem de erro é exibida quando você tenta acessar dados mais antigos que este.

### Existe um limite de 1000 XIDs em uma única chamada

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "There is a limit of 1000 XIDs in a single call"
}
```

Esta mensagem de erro é exibida ao tentar recuperar informações de identidade para mais do que o número máximo de [XIDs](#what-are-composite-identities-and-xids) permitido em uma única chamada de API. Reduza o número de XIDs em sua solicitação para abaixo do limite exibido para resolver esse problema.


### Existe um limite para 1000 compostoXids em uma única chamada

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "There is a limit for 1000 compositeXids in a single call"
}
```

Essa mensagem de erro é exibida ao tentar recuperar informações de identidade para mais do que o número máximo de [identidades compostas](#what-are-composite-identities-and-xids) permitidas em uma única chamada de API. Reduza o número de identidades compostas na solicitação para abaixo do limite exibido para resolver esse problema.

### O tipo de gráfico especificado é inválido

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "The graph-type abc specified is invalid. Please provide a valid graph-type"
}
```

Esta mensagem de erro é exibida quando um parâmetro de consulta `graph-type` recebe um valor inválido no caminho da solicitação. Consulte a seção sobre [gráficos de identidade](./home.md) na visão geral [!DNL Identity Service] para saber quais tipos de gráficos são suportados.

### O token de serviço não tem um escopo válido

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Service token does not have valid scope. Either acp.core.identity or acp.foundation is required"
}
```

Essa mensagem de erro é exibida quando a Organização IMS não foi provisionada com as permissões apropriadas para [!DNL Identity Service]. Entre em contato com o administrador do sistema para resolver esse problema.

### O token de serviço de gateway não é válido

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Gateway service token is not valid"
}
```

No caso deste erro, o token de acesso é inválido. Os tokens de acesso expiram a cada 24 horas e devem ser regenerados para continuar usando [!DNL Platform] APIs. Consulte o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en) para obter instruções sobre como gerar novos tokens de acesso.

### O token de serviço de autorização não é válido

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Authorization service token is not valid"
}
```

No caso deste erro, o token de acesso é inválido. Os tokens de acesso expiram a cada 24 horas e devem ser regenerados para continuar usando [!DNL Platform] APIs. Consulte o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en) para obter instruções sobre como gerar novos tokens de acesso.

### O token de usuário não tem contexto de produto válido

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "User token does not have valid product context"
}
```

Esta mensagem de erro é exibida quando o token de acesso não foi gerado a partir de uma integração [!DNL Experience Platform]. Consulte o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en) para obter instruções sobre como gerar novos tokens de acesso para uma integração [!DNL Experience Platform].

### Erro interno ao obter o XID nativo do código de identidade e namespace

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Invalid IMS Token/IMS Org | Internal error - when tried to get native XID from identity and namespace code"
}
```

Quando [!DNL Identity Service] mantém uma identidade, a ID da identidade e a ID de namespace associada são atribuídas a um identificador exclusivo chamado XID. Essa mensagem é exibida quando ocorre um erro durante o processo de localização do XID para um determinado valor de ID e namespace.

### A Organização IMS não está provisionada para uso [!DNL Identity Service]

```json
{
    "title": "AccountNotProvisioned",
    "status": 403,
    "detail": "The IMS Org. {IMS_ORG_NAME} is not provisioned for Identity Service usage"
}
```

Essa mensagem de erro é exibida quando a Organização IMS não foi provisionada com as permissões apropriadas para [!DNL Identity Service]. Entre em contato com o administrador do sistema para resolver esse problema.

### Erro interno do servidor

```json
{
    "title": "InternalError",
    "status": 500,
    "detail": "Internal Server Error. There was a problem processing your request"
}
```

Este erro é exibido quando uma exceção inesperada ocorre na execução de uma chamada de serviço [!DNL Platform]. A prática recomendada é programar suas chamadas automatizadas para repetir as solicitações algumas vezes em um intervalo de tempo ao receber esse erro. Se o problema persistir, entre em contato com o administrador do sistema.

## Códigos de erro de assimilação em lote

[!DNL Identity Service] assimila dados de identidade de dados de registro e de séries de tempo que são carregados para  [!DNL Platform] usar a Assimilação em lote. Como a assimilação em lote é um processo assíncrono, é necessário visualizar os detalhes de um lote para exibir erros. Os erros acumular-se-ão à medida que o lote avança até à conclusão do mesmo.

Esta é uma lista de mensagens de erro relacionadas a [!DNL Identity Service] que podem ser encontradas ao usar a [API de assimilação de dados](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml).

### Esquema XDM desconhecido

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Unknown XDM schema"
}
```

[!DNL Identity Service] O consome somente identidades para dados de registro ou de série de tempo que estejam em conformidade com as classes  [!DNL Profile] ou  [!DNL ExperienceEvent] , respectivamente. Tentar assimilar dados para [!DNL Identity Service] que não adere a nenhuma das classes acionará esse erro.

### Havia 0 identidades válidas nas primeiras 100 linhas do lote processado

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "There were 0 valid identities in the first 100 rows of the processed batch"
}
```

Esse erro é exibido quando as primeiras 100 linhas de um lote não apresentaram identidades. Contudo, este erro não indica de forma conclusiva que não foram detectadas identidades em registros subsequentes.

### Registros ignorados, pois tinham apenas 1 identidade por registro XDM

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Skipped {NUMBER_OF_RECORDS} records as they had only 1 identity per XDM record"
}
```

[!DNL Identity Service] somente vincula identidades quando registros únicos apresentam dois ou mais valores de identidade. Essa mensagem de erro ocorre uma vez para cada lote assimilado e exibe o número de registros nos quais apenas uma identidade pôde ser encontrada e não resultou em nenhuma alteração no gráfico de identidade.

### O Código de Namespace não está registrado para esta Organização IMS

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Namespace Code {ERRONEOUS_CODE} is not registered for this IMS Org"
}
```

Esse erro é exibido quando um registro assimilado apresenta uma identidade cujo namespace associado não existe ou está inacessível pela Organização IMS.

### Ignorar a assimilação em lote, pois a Organização IMS não está provisionada para o Gráfico de identidade privada

```json
{
    "title": "AccountNotProvisioned",
    "status": 403,
    "detail": "Skipping batch ingestion as IMS Org is not provisioned for Private Identity Graph"
}
```

Ao assimilar dados em lote, essa mensagem de erro é exibida quando a Organização IMS não foi provisionada com as permissões apropriadas para [!DNL Identity Service]. Entre em contato com o administrador do sistema para resolver esse problema.

### Erro interno

```json
{
    "title": "InternalError",
    "status": 500,
    "detail": "Internal Error. There was a problem during the ingestion"
}
```

Esse erro é exibido quando ocorre uma exceção inesperada durante uma assimilação em lote. A prática recomendada é programar suas chamadas automatizadas para repetir as solicitações algumas vezes em um intervalo de tempo ao receber esse erro. Se o problema persistir, entre em contato com o administrador do sistema.
