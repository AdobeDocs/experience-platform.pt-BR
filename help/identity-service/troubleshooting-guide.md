---
keywords: Experience Platform;home;popular topics;identity namespace;Identity namespace
solution: Experience Platform
title: Guia de solução de problemas do Adobe Experience Platform Identity Service
topic: troubleshooting
description: Este documento fornece respostas para perguntas frequentes sobre o Adobe Experience Platform Identity Service, bem como um guia de solução de problemas para erros comuns.
translation-type: tm+mt
source-git-commit: 04efbf63741ef39bbf0b22795be74087f1f7c595
workflow-type: tm+mt
source-wordcount: '2248'
ht-degree: 1%

---


# Guia de solução de problemas do Serviço de identidade

Este documento fornece respostas para perguntas frequentes sobre o Adobe Experience Platform [!DNL Identity Service], bem como um guia de solução de problemas para erros comuns. Em caso de dúvidas e solução de problemas relacionados às [!DNL Platform] APIs em geral, consulte o guia [de solução de problemas da API](../landing/troubleshooting.md)Adobe Experience Platform.

Os dados que identificam um único cliente são frequentemente fragmentados em vários dispositivos e sistemas que ele usa para se relacionar com sua marca. [!DNL Identity Service] reúne essas identidades fragmentadas, facilitando uma compreensão completa do comportamento do cliente para que você possa oferecer experiências digitais de impacto em tempo real. Para obter mais informações, consulte a visão geral [do Serviço de](./home.md)identidade.

## Perguntas frequentes

A seguir, uma lista de respostas a perguntas frequentes sobre [!DNL Identity Service].

## O que são dados de identidade?

Dados de identidade são todos os dados que podem ser usados para identificar uma pessoa. Dependendo do contexto de como os dados são usados em sua organização, os dados de identidade podem incluir nomes de usuário, endereços de email e IDs de sistemas CRM. Os dados de identidade não estão limitados a usuários registrados de seu site ou serviço, pois os usuários anônimos também podem ser identificados por seu dispositivo ou ID de cookie.

## Qual é o benefício de rotular os campos de dados como identidades?

Rotular determinados campos de dados como identidades nos dados de registro e série de tempo permite mapear relações de identidade dentro da estrutura natural dos dados e reconciliar canais cruzados de dados do duplicado. Consulte a visão geral [do Serviço de](./home.md) identidade para obter mais informações.

## O que são identidades conhecidas e anônimas?

Uma identidade conhecida refere-se a um valor de identidade que pode ser usado sozinho ou com outras informações para identificar, entrar em contato ou localizar uma pessoa individual. Exemplos de identidades conhecidas podem incluir endereços de email, números de telefone e IDs de CRM.

Uma identidade anônima refere-se a um valor de identidade que não pode ser usado sozinho ou com outras informações para identificar, contatar ou localizar uma pessoa individual (como uma ID de cookie).

## O que é um Gráfico de identidade particular?

Um Gráfico de identidade privada é um mapa privado de relações entre identidades pontilhadas e ligadas, visível apenas para a sua organização.

Quando mais de uma identidade é incluída em qualquer dado assimilado de um ponto de extremidade de transmissão ou enviado para um conjunto de dados ativado para [!DNL Identity Service], essas identidades são vinculadas no Gráfico de identidade privada. [!DNL Identity Service] aproveita esse gráfico para obter identidades de um determinado consumidor ou entidade, permitindo a identificação e a união de perfis.

## Como faço para criar vários campos de identidade em um schema XDM?

[Os schemas do Modelo de Dados de Experiência (XDM)](../xdm/home.md) suportam vários campos de identidade. Qualquer campo de dados do tipo `string` em um schema que implemente o Perfil individual XDM ou a classe ExperienceEvent XDM pode ser rotulado como um campo de identidade. Depois de rotulados, todos os dados contidos nesses campos são adicionados ao mapa de identidade do perfil.

Para obter etapas sobre como rotular um campo XDM como um campo de identidade usando a interface do usuário, consulte a seção [](../xdm/tutorials/create-schema-ui.md) Identidade no tutorial do Editor de Schemas. Se você estiver usando a API, consulte a seção [Descritor de](../xdm/tutorials/create-schema-api.md) identidade no tutorial da API do Registro do Schema.

## Há contextos em que alguns campos não devem ser rotulados como identidades?

Os campos de identidade devem ser reservados para valores exclusivos para cada indivíduo. Por exemplo, considere um conjunto de dados para um programa de fidelidade do cliente. O campo de &quot;nível de fidelidade&quot; (ouro, prata, bronze) não seria um campo de identidade útil, ao passo que a ID de fidelidade — um valor único — seria.

Campos como CEP e endereços IP não devem ser rotulados como identidades para indivíduos, pois esses valores podem se aplicar a mais de uma pessoa individual. Estes tipos de campos só devem ser rotulados como identidades para as estratégias de comercialização a nível do agregado familiar.

## Por que meus campos de identidade não estão vinculando da maneira que eu espero?

Usando o [`/cluster/members` endpoint](./api/list-cluster-identites.md) na API do Serviço de identidade, é possível visualização das identidades associadas para um ou mais campos de identidade. Se a resposta não retornar as identidades vinculadas esperadas, verifique se você está fornecendo as informações de identidade apropriadas nos dados XDM. Consulte a seção sobre como [fornecer dados XDM ao serviço](./home.md) de identidade na visão geral do serviço de identidade para obter mais informações.

## O que é uma namespace de identidade?

Uma namespace de identidade fornece contexto sobre como os campos de identidade se relacionam à identidade de um cliente. Por exemplo, os campos de identidade na namespace &quot;Email&quot; devem estar em conformidade com um formato do email padrão (nome<span>@emailprovider.com), enquanto os campos que usam a namespace &quot;Telefone&quot; devem estar em conformidade com um número de telefone padrão (como 987-555-1234 na América do Norte).

As namespaces distinguem valores de identidade similares entre sistemas CRM diferentes. Por exemplo, considere um perfil que contenha uma ID de Fidelidade numérica associada ao programa redirecionado do empresa. Uma namespace de &quot;Fidelidade&quot; separaria esse valor de uma ID numérica semelhante para seu sistema de comércio eletrônico que também aparece no mesmo perfil.

Consulte a visão geral [da namespace de](./home.md) identidade para obter mais informações.

## Como associar uma identidade a uma namespace de identidade?

Os campos de identidade devem ser associados a uma namespace de identidade existente quando são criados. Qualquer nova namespace deve ser [criada usando a API](#how-do-i-create-a-custom-namespace-for-my-organization) antes de associá-la aos campos de identidade.

Para obter instruções passo a passo sobre como definir uma namespace ao criar um descritor de identidade usando a API, consulte a seção sobre como [criar um descritor](../xdm/tutorials/create-schema-ui.md) no guia do desenvolvedor do Registro de Schemas. Para marcar um campo de schema como uma identidade na interface do usuário, siga as etapas no tutorial [do Editor de](../xdm/tutorials/create-schema-api.md)Schemas.

## Quais são as namespaces de identidade padrão fornecidas pela Experience Platform? {#standard-namespaces}

As seguintes namespaces padrão são fornecidas para uso por todas as organizações dentro do Experience Platform:

| Nome de exibição | ID | Código | Descrição |
| ------------ | --- | --- | ----------- |
| CORE | 0 | CORE | nome do legado: &quot;Adobe AudienceManager&quot; |
| ECID | 4 | ECID | alias: &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot; |
| Email | 6 | Email |  |
| Email (SHA256, em minúsculas) | 11 | Emails | Namespace padrão para email pré-hash. Os valores fornecidos nesta namespace são convertidos em minúsculas antes de hash com SHA-256. |
| Telefone | 7 | Telefone |  |
| Windows AID | 8 | WAID |  |
| AdCloud | 411 | AdCloud | alias: Ad Cloud |
| Adobe Target | 9 | TNTID | ID do público alvo |
| ID do Google Ad | 20914 | GAID | GAID |
| Apple IDFA | 20915 | IDFA | ID para anunciantes |

## Onde posso encontrar a lista de namespaces de identidade disponível para minha organização?

Usando a API [do Serviço de](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/id-service-api.yaml)identidade, você pode lista todas as namespaces de identidade disponíveis para sua organização, fazendo uma solicitação de GET para o `/idnamespace/identities` endpoint. Consulte a seção sobre como [listar namespaces](./api/list-namespaces.md) disponíveis na visão geral da API do Serviço de identidade para obter mais informações.

## Como faço para criar uma namespace personalizada para minha organização?

Usando a API [do Serviço de](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/id-service-api.yaml)identidade, você pode criar uma namespace de identidade personalizada para sua organização, solicitando um POST para o `/idnamespace/identities` endpoint. Consulte a seção sobre como [criar uma namespace](./api/create-custom-namespace.md) personalizada na visão geral da API do Serviço de identidade para obter mais informações.

## O que são identidades compostas e XIDs?

As identidades são referenciadas em chamadas de API pela identidade composta ou por XID. Uma identidade **** composta é uma representação de uma identidade que contém um valor de ID e uma namespace. Um **XID** é um identificador de valor único que representa a mesma construção que uma identidade composta (uma ID e uma namespace) e é automaticamente atribuído a novas identidades quando persistido pelo Serviço de identidade. Consulte a visão geral [da API do Serviço de](./home.md) identidade para obter mais informações.

## Como o Serviço de Identidade lida com informações de identificação pessoal (PII)?

O Serviço de identidade cria um hash criptográfico de PII forte e unidirecional antes dos valores persistentes. Os dados de identidade nas namespaces &quot;Telefone&quot; e &quot;Email&quot; são automaticamente hash usando SHA-256, com valores de &quot;Email&quot; automaticamente convertidos em minúsculas antes de hash.

## Devo criptografar todas as PII antes de enviar para a Plataforma?

Não é necessário criptografar manualmente os dados de PII antes de assimilá-los na Plataforma. Ao aplicar o rótulo de uso de `I1` dados a todos os campos de dados aplicáveis, a Plataforma converte esses campos automaticamente em valores de ID com hash após a ingestão.

Para obter etapas sobre como aplicar e gerenciar rótulos de uso de dados, consulte o tutorial [de rótulos de uso de](../data-governance/labels/user-guide.md)dados.

## Há alguma consideração ao hash identidades baseadas em PII?

Se você estiver enviando valores de PII com hash para o Serviço de identidade, deverá usar o mesmo método de criptografia nos conjuntos de dados. Isso garante que o mesmo valor de identidade nos conjuntos de dados gere os mesmos valores com hash e seja capaz de ser corretamente correspondido e vinculado no gráfico de identidade.

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

A seção a seguir fornece sugestões de solução de problemas para códigos de erro específicos e comportamento inesperado que você pode encontrar ao trabalhar com a [!DNL Identity Service] API.

## [!DNL Identity Service] mensagens de erro

Veja a seguir uma lista de mensagens de erro que podem ser encontradas ao usar a [!DNL Identity Service] API.

### Parâmetro de query obrigatório ausente

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Missing required query parameter - namespace"
}
```

Esse erro é exibido quando um parâmetro de query obrigatório não foi incluído no caminho da solicitação. O nome `detail` da mensagem de erro fornece o nome do parâmetro ausente. As variações dessa mensagem de erro incluem:

- Parâmetro de query obrigatório ausente - nsId
- Parâmetro de query obrigatório ausente - id
- Parâmetro de query obrigatório ausente - xid ou (nsid,id)
- Parâmetro de query obrigatório ausente - targetNs
- Parâmetro de query obrigatório ausente - xids ou compostoXids

Verifique se você está incluindo corretamente o parâmetro indicado no caminho da solicitação antes de tentar novamente.

### O carimbo de data e hora deve estar nos últimos 180 dias

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Timestamp should be within last 180 days"
}
```

[!DNL Identity Service] elimina dados com mais de 180 dias. Esta mensagem de erro é exibida quando você tenta acessar dados mais antigos do que isso.

### Existe um limite de 1000 XIDs em uma única chamada

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "There is a limit of 1000 XIDs in a single call"
}
```

Esta mensagem de erro é exibida quando você tenta recuperar informações de identidade para mais do que o número máximo de [XIDs](#what-are-composite-identities-and-xids) permitidos em uma única chamada de API. Reduza o número de XIDs em sua solicitação para abaixo do limite exibido para resolver esse problema.


### Existe um limite para 1000 compostosXids em uma única chamada

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "There is a limit for 1000 compositeXids in a single call"
}
```

Esta mensagem de erro é exibida quando você tenta recuperar informações de identidade para mais do que o número máximo de identidades [](#what-are-composite-identities-and-xids) compostas permitido em uma única chamada de API. Reduza o número de identidades compostas na solicitação para abaixo do limite exibido para resolver esse problema.

### O tipo de gráfico especificado é inválido

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "The graph-type abc specified is invalid. Please provide a valid graph-type"
}
```

Esta mensagem de erro é exibida quando um parâmetro de `graph-type` query recebe um valor inválido no caminho da solicitação. Consulte a seção sobre gráficos [de](./home.md) identidade na [!DNL Identity Service] visão geral para saber quais tipos de gráficos são suportados.

### O token de serviço não tem um escopo válido

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Service token does not have valid scope. Either acp.core.identity or acp.foundation is required"
}
```

Esta mensagem de erro é exibida quando a Organização IMS não foi provisionada com as permissões apropriadas para [!DNL Identity Service]. Entre em contato com o administrador do sistema para resolver esse problema.

### O token de serviço de gateway não é válido

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Gateway service token is not valid"
}
```

No caso deste erro, o token de acesso é inválido. Os tokens de acesso expiram a cada 24 horas e devem ser regenerados para continuar usando [!DNL Platform] APIs. Consulte o tutorial [de](../tutorials/authentication.md) autenticação para obter instruções sobre como gerar novos tokens de acesso.

### O token do serviço de autorização não é válido

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Authorization service token is not valid"
}
```

No caso deste erro, o token de acesso é inválido. Os tokens de acesso expiram a cada 24 horas e devem ser regenerados para continuar usando [!DNL Platform] APIs. Consulte o tutorial [de](../tutorials/authentication.md) autenticação para obter instruções sobre como gerar novos tokens de acesso.

### O token de usuário não tem um contexto de produto válido

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "User token does not have valid product context"
}
```

Esta mensagem de erro é exibida quando o token de acesso não foi gerado a partir de uma [!DNL Experience Platform] integração. Consulte o tutorial [de](../tutorials/authentication.md) autenticação para obter instruções sobre como gerar novos tokens de acesso para uma [!DNL Experience Platform] integração.

### Erro interno ao obter o XID nativo do código de identidade e namespace

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Invalid IMS Token/IMS Org | Internal error - when tried to get native XID from identity and namespace code"
}
```

Quando [!DNL Identity Service] persiste uma identidade, a ID da identidade e a ID da namespace associada são atribuídas a um identificador exclusivo chamado XID. Essa mensagem é exibida quando ocorre um erro durante o processo de localizar o XID para um determinado valor de ID e namespace.

### A Organização IMS não está provisionada para [!DNL Identity Service] uso

```json
{
    "title": "AccountNotProvisioned",
    "status": 403,
    "detail": "The IMS Org. {IMS_ORG_NAME} is not provisioned for Identity Service usage"
}
```

Esta mensagem de erro é exibida quando a Organização IMS não foi provisionada com as permissões apropriadas para [!DNL Identity Service]. Entre em contato com o administrador do sistema para resolver esse problema.

### Erro de servidor interno

```json
{
    "title": "InternalError",
    "status": 500,
    "detail": "Internal Server Error. There was a problem processing your request"
}
```

Este erro é exibido quando ocorre uma exceção inesperada na execução de uma chamada de [!DNL Platform] serviço. A prática recomendada é programa de suas chamadas automatizadas para repetir as solicitações algumas vezes em um intervalo de tempo ao receber esse erro. Se o problema persistir, entre em contato com o administrador do sistema.

## Códigos de erro de ingestão em lote

[!DNL Identity Service] assimila dados de identidade de dados de registro e de série de tempo que são carregados para [!DNL Platform] usar a assimilação em lote. Como a ingestão em lote é um processo assíncrono, é necessário visualização os detalhes de um lote para erros de visualização. Os erros acumular-se-ão à medida que o lote avança até à conclusão do mesmo.

A seguir está uma lista de mensagens de erro relacionadas a [!DNL Identity Service] você pode encontrar ao usar a API [de ingestão de](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml)dados.

### Schema XDM desconhecido

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Unknown XDM schema"
}
```

[!DNL Identity Service] consome apenas identidades para dados de registros ou séries cronológicas que estejam em conformidade com as classes [!DNL Profile] ou [!DNL ExperienceEvent] classes, respectivamente. A tentativa de assimilar dados para [!DNL Identity Service] os quais não aderem a nenhuma das classes acionará esse erro.

### Houve 0 identidades válidas nas primeiras 100 linhas do lote processado

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "There were 0 valid identities in the first 100 rows of the processed batch"
}
```

Esse erro é exibido quando as primeiras 100 linhas de um lote não apresentam identidades. No entanto, este erro não indica de forma conclusiva que não foram encontradas identidades em registros subsequentes.

### Registros ignorados, pois eles tinham apenas 1 identidade por registro XDM

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Skipped {NUMBER_OF_RECORDS} records as they had only 1 identity per XDM record"
}
```

[!DNL Identity Service] somente vincula identidades quando registros únicos apresentam dois ou mais valores de identidade. Esta mensagem de erro ocorre uma vez para cada lote ingerido e exibe o número de registros em que apenas uma identidade foi encontrada e não resultou em nenhuma alteração no gráfico de identidade.

### O Código de namespace não está registrado para esta Organização IMS

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Namespace Code {ERRONEOUS_CODE} is not registered for this IMS Org"
}
```

Este erro é exibido quando um registro ingerido apresenta uma identidade cuja namespace associada não existe ou está inacessível para a sua Organização IMS.

### Ignorar ingestão em lote, pois a Organização IMS não está provisionada para o Gráfico de identidade privada

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

Este erro é exibido quando ocorre uma exceção inesperada durante uma ingestão em lote. A prática recomendada é programa de suas chamadas automatizadas para repetir as solicitações algumas vezes em um intervalo de tempo ao receber esse erro. Se o problema persistir, entre em contato com o administrador do sistema.
