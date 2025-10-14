---
keywords: Experience Platform;página inicial;tópicos populares;namespace de identidade;namespace de identidade
solution: Experience Platform
title: Guia de solução de problemas do serviço de identidade
description: Este documento fornece respostas a perguntas frequentes sobre o Adobe Experience Platform Identity Service, bem como um guia de solução de problemas para erros comuns.
exl-id: dac31bc3-7003-46d6-9d41-9f6fd3645c2c
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2168'
ht-degree: 0%

---

# Guia de solução de problemas do Serviço de identidade

Este documento fornece respostas a perguntas frequentes sobre o Adobe Experience Platform [!DNL Identity Service], bem como um guia de solução de problemas para erros comuns. Para perguntas e soluções de problemas relacionadas às APIs do [!DNL Experience Platform] em geral, consulte o [guia de solução de problemas da API do Adobe Experience Platform](../landing/troubleshooting.md).

Os dados que identificam um único cliente geralmente são fragmentados em vários dispositivos e sistemas que eles usam para interagir com sua marca. O [!DNL Identity Service] reúne essas identidades fragmentadas, facilitando uma compreensão completa do comportamento do cliente para que você possa oferecer experiências digitais impactantes em tempo real. Para obter mais informações, consulte a [visão geral do Serviço de Identidade](./home.md).

## Perguntas frequentes

Esta é uma lista de respostas para perguntas frequentes sobre [!DNL Identity Service].

## O que são dados de identidade?

Dados de identidade são quaisquer dados que possam ser usados para identificar uma pessoa individual. Dependendo do contexto de como os dados são usados em sua organização, os dados de identidade podem incluir nomes de usuário, endereços de email e IDs de sistemas CRM. Os dados de identidade não estão limitados aos usuários registrados do seu site ou serviço, pois os usuários anônimos também podem ser identificados pelo dispositivo ou pela ID do cookie.

## Qual é o benefício de rotular campos de dados como identidades?

Rotular determinados campos de dados como identidades nos dados de registro e série temporal permite mapear relações de identidade na estrutura natural dos dados e reconciliar dados duplicados entre canais. Consulte a [visão geral do Serviço de identidade](./home.md) para obter mais informações.

## O que são identidades conhecidas e anônimas?

Uma identidade conhecida se refere a um valor de identidade que pode ser usado sozinho ou com outras informações para identificar, entrar em contato ou localizar uma pessoa individual. Exemplos de identidades conhecidas podem incluir endereços de email, números de telefone e CRMIDs.

Uma identidade anônima refere-se a um valor de identidade que não pode ser usado isoladamente ou com outras informações para identificar, entrar em contato ou localizar uma pessoa individual (como uma ID de cookie).

## O que é um Gráfico de identidade privada?

Um Gráfico de identidade privada é um mapa privado dos relacionamentos entre identidades compiladas e vinculadas, visível apenas para sua organização.

Quando mais de uma identidade é incluída em qualquer dado assimilado de um ponto de extremidade de transmissão ou enviado a um conjunto de dados habilitado para [!DNL Identity Service], essas identidades são vinculadas no Gráfico de identidade privada. O [!DNL Identity Service] usa esse gráfico para obter identidades de um determinado consumidor ou entidade, permitindo a identificação de identidades e a mesclagem de perfis.

## Como criar vários campos de identidade em um esquema XDM?

Os esquemas [Experience Data Model (XDM)](../xdm/home.md) oferecem suporte a vários campos de identidade. Qualquer campo de dados do tipo `string` em um esquema que implementa o Perfil Individual XDM ou a classe XDM ExperienceEvent pode ser rotulado como um campo de identidade. Depois de rotulados, os dados contidos nesses campos são adicionados ao mapa de identidade do perfil.

Para obter etapas sobre como rotular um campo XDM como um campo de identidade usando a interface do usuário, consulte a [seção Identidade](../xdm/tutorials/create-schema-ui.md) no tutorial do Editor de esquemas. Se você estiver usando a API, consulte a [seção do descritor de identidade](../xdm/tutorials/create-schema-api.md) no tutorial da API do Registro de esquemas.

## Existem contextos em que alguns campos não devem ser rotulados como identidades?

Os campos de identidade devem ser reservados para valores exclusivos de cada indivíduo. Por exemplo, considere um conjunto de dados para um programa de fidelidade do cliente. O campo &quot;nível de fidelidade&quot; (ouro, prata, bronze) não seria um campo de identidade útil, enquanto a ID de fidelidade — um valor único — seria.

Campos como CEPs e endereços IP não devem ser rotulados como identidades para indivíduos, pois esses valores podem se aplicar a mais de uma pessoa. Esses tipos de campos só devem ser rotulados como identidades para estratégias de marketing a nível doméstico.

## Por que os campos de identidade não estão vinculados da maneira esperada?

Usando o ponto de extremidade [`/cluster/members` &#x200B;](./api/list-cluster-identites.md) na API do serviço de identidade, você pode exibir as identidades associadas para um ou mais campos de identidade. Se a resposta não retornar as identidades vinculadas esperadas, forneça as informações de identidade apropriadas em seus dados XDM. Consulte a seção sobre [fornecendo dados XDM ao Serviço de identidade](./home.md) na visão geral do Serviço de identidade para obter mais informações.

## O que é um namespace de identidade?

Um namespace de identidade fornece o contexto de como os campos de identidade se relacionam com a identidade de um cliente. Por exemplo, os campos de identidade no namespace &quot;Email&quot; devem estar em conformidade com um formato de email padrão (nome<span>@emailprovider.com), enquanto os campos que usam o namespace &quot;Telefone&quot; devem estar em conformidade com um número de telefone padrão (como 987-555-1234 na América do Norte).

Os namespaces distinguem valores de identidade semelhantes entre sistemas de CRM diferentes. Por exemplo, considere um perfil que contenha uma ID numérica de Fidelidade associada ao programa de recompensas da sua empresa. Um namespace de &quot;Fidelidade&quot; separaria esse valor de uma ID numérica semelhante para o seu sistema de comércio eletrônico que também aparece no mesmo perfil.

Consulte a [visão geral do namespace de identidade](./home.md) para obter mais informações.

## Como associar uma identidade a um namespace de identidade?

Os campos de identidade devem ser associados a um namespace de identidade existente quando são criados. Qualquer novo namespace deve ser [criado usando a API](#how-do-i-create-a-custom-namespace-for-my-organization) antes de associá-lo a campos de identidade.

Para obter instruções passo a passo sobre como definir um namespace ao criar um descritor de identidade usando a API, consulte a seção sobre [criação de um descritor](../xdm/tutorials/create-schema-ui.md) no guia do desenvolvedor do Registro de Esquemas. Para marcar um campo de esquema como uma identidade na interface, siga as etapas no [tutorial do Editor de esquemas](../xdm/tutorials/create-schema-api.md).

## Quais são os namespaces de identidade padrão fornecidos pelo Experience Platform? {#standard-namespaces}

Os namespaces de identidade padrão são namespaces disponíveis para todas as organizações. Consulte a [visão geral dos namespaces de identidade](./features/namespaces.md) para obter uma lista completa dos namespaces padrão disponíveis.

## Onde posso encontrar a lista de namespaces de identidade disponíveis para minha organização?

Usando a [API do Serviço de Identidade](https://www.adobe.io/experience-platform-apis/references/identity-service), você pode listar todos os namespaces de identidade disponíveis para sua organização fazendo uma solicitação GET para o ponto de extremidade `/idnamespace/identities`. Consulte a seção sobre [listando os namespaces disponíveis](./api/list-namespaces.md) na visão geral da API do Serviço de Identidade para obter mais informações.

## Como criar um namespace personalizado para minha organização?

Usando a [API do Serviço de Identidade](https://www.adobe.io/experience-platform-apis/references/identity-service), você pode criar um namespace de identidade personalizado para sua organização fazendo uma solicitação POST para o ponto de extremidade `/idnamespace/identities`. Consulte a seção sobre [criação de um namespace personalizado](./api/create-custom-namespace.md) na visão geral da API do Serviço de identidade para obter mais informações.

## O que são identidades compostas e XIDs?

As identidades são referenciadas em chamadas de API pela identidade composta ou XID. Uma identidade composta é uma representação de uma identidade que contém um valor de ID e um namespace. Um XID é um identificador de valor único que representa a mesma construção que uma identidade composta (uma ID e um namespace) e é automaticamente atribuído a novas identidades quando persistidas pelo Serviço de identidade. Consulte a [Visão geral da API do serviço de identidade](./home.md) para obter mais informações.

## Como o Serviço de identidade lida com informações de identificação pessoal (PII)?

O Serviço de identidade tem namespaces padrão para oferecer suporte à assimilação de valores de identidade com hash para números de telefone e emails. No entanto, você é responsável pelo hash de valores. Para saber mais sobre os dados de hash assimilados na Experience Platform, consulte o [[!DNL Data Prep] guia de funções de mapeamento](../data-prep/functions.md#hashing).

## Há alguma consideração sobre o hash de identidades baseadas em PII?

Se estiver enviando valores de PII com hash para o Serviço de identidade, você deve usar o mesmo método de criptografia em seus conjuntos de dados. Isso garante que o mesmo valor de identidade nos conjuntos de dados gere os mesmos valores com hash e possa ser correspondido e vinculado corretamente no gráfico de identidade.

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

## Por que não consigo acessar a página ou as APIs do gráfico de identidade?

O administrador do Experience Platform deve provisionar com a permissão `view-identity-graph` para que você visualize os dados do gráfico de identidade. Sem essa permissão, você receberá uma mensagem de permissão negada na página do visualizador de gráficos de identidade e ao chamar as APIs do Experience Platform. Consulte a [visão geral do controle de acesso](../access-control/home.md) para obter mais informações sobre permissões.

## Solução de problemas

A seção a seguir fornece sugestões para a solução de problemas de códigos de erro específicos e comportamento inesperado que você pode encontrar ao trabalhar com a API [!DNL Identity Service].

## [!DNL Identity Service] mensagens de erro

Esta é uma lista de mensagens de erro que você pode encontrar ao usar a API [!DNL Identity Service].

### Parâmetro de consulta obrigatório ausente

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Missing required query parameter - namespace"
}
```

Este erro é exibido quando um parâmetro de consulta necessário não foi incluído no caminho da solicitação. O `detail` da mensagem de erro fornece o nome do parâmetro ausente. As variações dessa mensagem de erro incluem:

- Parâmetro de consulta obrigatório ausente - nsId
- Parâmetro de consulta obrigatório ausente - id
- Parâmetro de consulta obrigatório ausente - xid ou (nsid,id)
- Parâmetro de consulta obrigatório ausente - targetNs
- Parâmetro de consulta obrigatório ausente - xids ou compositeXids

Verifique se você está incluindo corretamente o parâmetro indicado no caminho da solicitação antes de tentar novamente.

### O carimbo de data/hora deve estar nos últimos 180 dias

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Timestamp should be within last 180 days"
}
```

[!DNL Identity Service] limpa dados com mais de 180 dias. Essa mensagem de erro é exibida quando você tenta acessar dados mais antigos que esse.

### Há um limite de 1000 XIDs em uma única chamada

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "There is a limit of 1000 XIDs in a single call"
}
```

Esta mensagem de erro é exibida quando você tenta recuperar informações de identidade para além do número máximo de [XIDs](#what-are-composite-identities-and-xids) permitidos em uma única chamada de API. Reduza o número de XIDs em sua solicitação para abaixo do limite exibido para resolver esse problema.


### Há um limite de 1000 compositeXids em uma única chamada

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "There is a limit for 1000 compositeXids in a single call"
}
```

Esta mensagem de erro é exibida quando você tenta recuperar informações de identidade para além do número máximo de [identidades compostas](#what-are-composite-identities-and-xids) permitido em uma única chamada de API. Reduza o número de identidades compostas em sua solicitação para abaixo do limite exibido para resolver esse problema.

### O tipo de gráfico especificado é inválido

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "The graph-type abc specified is invalid. Please provide a valid graph-type"
}
```

Esta mensagem de erro é exibida quando um parâmetro de consulta `graph-type` recebe um valor inválido no caminho da solicitação. Consulte a seção sobre [gráficos de identidade](./home.md) na visão geral de [!DNL Identity Service] para saber quais tipos de gráficos são compatíveis.

### O token de serviço não tem um escopo válido

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Service token does not have valid scope. Either acp.core.identity or acp.foundation is required"
}
```

Esta mensagem de erro é exibida quando sua organização não é provisionada com as permissões apropriadas para [!DNL Identity Service]. Contate o administrador do sistema para resolver esse problema.

### O token de serviço do gateway não é válido

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Gateway service token is not valid"
}
```

No caso desse erro, o token de acesso é inválido. Os tokens de acesso expiram a cada 24 horas e devem ser gerados novamente para continuar usando as APIs do [!DNL Experience Platform]. Consulte o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en) para obter instruções sobre como gerar novos tokens de acesso.

### O token do serviço de autorização não é válido

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Authorization service token is not valid"
}
```

No caso desse erro, o token de acesso é inválido. Os tokens de acesso expiram a cada 24 horas e devem ser gerados novamente para continuar usando as APIs do [!DNL Experience Platform]. Consulte o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en) para obter instruções sobre como gerar novos tokens de acesso.

### O token do usuário não tem um contexto de produto válido

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "User token does not have valid product context"
}
```

Esta mensagem de erro é exibida quando o token de acesso não foi gerado a partir de uma integração do [!DNL Experience Platform]. Consulte o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en) para obter instruções sobre como gerar novos tokens de acesso para uma integração [!DNL Experience Platform].

### Erro interno ao obter XID nativo do código de namespace e identidade

```json
{
    "title": "UnauthorizedAccess",
    "status": 401,
    "detail": "Invalid IMS Token/IMS Org | Internal error - when tried to get native XID from identity and namespace code"
}
```

Quando [!DNL Identity Service] persiste uma identidade, a ID da identidade e a ID do namespace associada recebem um identificador exclusivo chamado XID. Essa mensagem é exibida quando ocorre um erro durante o processo de localização do XID de um determinado valor de ID e namespace.

### A Organização IMS não está provisionada para uso de [!DNL Identity Service]

```json
{
    "title": "AccountNotProvisioned",
    "status": 403,
    "detail": "The IMS Org. {IMS_ORG_NAME} is not provisioned for Identity Service usage"
}
```

Esta mensagem de erro é exibida quando sua organização não é provisionada com as permissões apropriadas para [!DNL Identity Service]. Contate o administrador do sistema para resolver esse problema.

### Erro interno do servidor

```json
{
    "title": "InternalError",
    "status": 500,
    "detail": "Internal Server Error. There was a problem processing your request"
}
```

Este erro é exibido quando ocorre uma exceção inesperada na execução de uma chamada de serviço [!DNL Experience Platform]. A prática recomendada é programar suas chamadas automatizadas para repetir as solicitações algumas vezes em um intervalo de tempo ao receber esse erro. Se o problema persistir, entre em contato com o administrador do sistema.

## Códigos de erro de assimilação em lote

[!DNL Identity Service] assimila dados de identidade de dados de registro e série temporal que são carregados em [!DNL Experience Platform] usando a Assimilação em lote. Como a assimilação em lote é um processo assíncrono, você deve visualizar os detalhes de um lote para visualizar os erros. Os erros serão acumulados à medida que o lote avança até ser concluído.

Esta é uma lista de mensagens de erro relacionadas a [!DNL Identity Service] que você pode encontrar ao usar a [API de assimilação em lote](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/).

### Esquema XDM desconhecido

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Unknown XDM schema"
}
```

[!DNL Identity Service] consome somente identidades para registro ou dados de série temporal que estejam em conformidade com as classes [!DNL Profile] ou [!DNL ExperienceEvent], respectivamente. A tentativa de assimilar dados para [!DNL Identity Service] que não aderem a nenhuma das classes disparará esse erro.

### Havia 0 identidades válidas nas primeiras 100 linhas do lote processado

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "There were 0 valid identities in the first 100 rows of the processed batch"
}
```

Esse erro é exibido quando as primeiras 100 linhas de um lote não apresentaram identidades. No entanto, esse erro não indica de forma conclusiva que nenhuma identidade foi encontrada nos registros subsequentes.

### Registros ignorados, pois tinham apenas uma identidade por registro XDM

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Skipped {NUMBER_OF_RECORDS} records as they had only 1 identity per XDM record"
}
```

[!DNL Identity Service] vincula identidades somente quando registros únicos apresentam dois ou mais valores de identidade. Essa mensagem de erro ocorre uma vez para cada lote assimilado e exibe o número de registros em que apenas uma identidade pôde ser encontrada, não resultando em nenhuma alteração no gráfico de identidade.

### O código de namespace não está registrado para esta Organização IMS

```json
{
    "title": "InvalidInput",
    "status": 400,
    "detail": "Namespace Code {ERRONEOUS_CODE} is not registered for this IMS Org"
}
```

Esse erro é exibido quando um registro assimilado apresenta uma identidade cujo namespace associado não existe ou está inacessível para sua organização.

### Ignorar a assimilação em lote como a Organização IMS não está provisionada para o Gráfico de identidade privada

```json
{
    "title": "AccountNotProvisioned",
    "status": 403,
    "detail": "Skipping batch ingestion as IMS Org is not provisioned for Private Identity Graph"
}
```

Ao assimilar dados em lote, esta mensagem de erro é exibida quando sua organização não é provisionada com as permissões apropriadas para [!DNL Identity Service]. Contate o administrador do sistema para resolver esse problema.

### Erro interno

```json
{
    "title": "InternalError",
    "status": 500,
    "detail": "Internal Error. There was a problem during the ingestion"
}
```

Esse erro é exibido quando ocorre uma exceção inesperada durante uma assimilação em lote. A prática recomendada é programar suas chamadas automatizadas para repetir as solicitações algumas vezes em um intervalo de tempo ao receber esse erro. Se o problema persistir, entre em contato com o administrador do sistema.
