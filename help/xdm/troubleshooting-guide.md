---
keywords: Experience Platform;tópicos populares;XDM;sistema XDM;perfil individual XDM;XDM ExperienceEvent;Evento de experiência XDM;evento experienceEvent;evento experienceExperience;Evento de experiência XDM;XDM ExperienceEvent;modelo de dados de experiência;modelo de dados de experiência;modelo de dados de experiência;modelo de dados;modelo de dados;esquema;solução de problemas;perguntas frequentes;esquema de união;PERFIL DA UNIÃO;perfil da união;http://ns.adobe.com/aep/errors/XDM-1010-404;http://ns.adobe.com/aep/errors/XDM-1011-404;http://ns.adobe.com/aep/errors/XDM-1012-404;http://ns.adobe.com/aep/errors/XDM-1013-404;http://ns.adobe.com/aep/errors/XDM-1014-404;http://ns.adobe.com/aep/errors/XDM-1015-404;http://ns.adobe.com/aep/errors/XDM-1016-404;http://ns.adobe.com/aep/errors/XDM-1017-404;http://ns.adobe.com/aep/errors/XDM-1521-400;http://ns.adobe.com/aep/errors/XDM-1020-400;http://ns.adobe.com/aep/errors/XDM-1021-400;http://ns.adobe.com/aep/errors/XDM-1022-400;http://ns.adobe.com/aep/errors/XDM-1023-400;http://ns.adobe.com/aep/errors/XDM-1024-400;http://ns.adobe.com/aep/errors/XDM-1006-400;http://ns.adobe.com/aep/errors/XDM-1007-400;http://ns.adobe.com/aep/errors/XDM-1008-400;http://ns.adobe.com/aep/errors/XDM-1009-400;http://ns.adobe.com/aep/errors/XDM-1526-400;http://ns.adobe.com/aep/errors/XDM-1527-400;http://ns.adobe.com/aep/errors/XDM-1528-400;XDM-1010-404;XDM-1011-404;XDM-1012-404;XDM-1013-404;XDM-1014-404;XDM-1015-404;XDM-1016-404;XDM-1017-404;XDM-1521-400;XDM-1020-400;XDM-1021-400;XDM-1022-400;XDM-1023-400;XDM-1024-400;XDM-1006-400;XDM-1007-400;XDM-1008-400;XDM-1009-400;XDM-1413-400;XDM-1526-400;XDM-1527-400;XDM-1528-400;
solution: Experience Platform
title: Guia de solução de problemas do sistema XDM
description: Encontre respostas para perguntas frequentes sobre o Experience Data Model (XDM), incluindo etapas para resolver erros comuns de API.
exl-id: a0c7c661-bee8-4f66-ad5c-f669c52c9de3
source-git-commit: 8ba80a1cc4529f9d4693e3f7cbd7584193915410
workflow-type: tm+mt
source-wordcount: '2368'
ht-degree: 0%

---

# Guia de solução de problemas do sistema XDM

Este documento fornece respostas a perguntas frequentes sobre o [!DNL Experience Data Model] (XDM) e o Sistema XDM no Adobe Experience Platform, incluindo um guia de solução de problemas para erros comuns. Para perguntas e soluções de problemas relacionadas a outros serviços da Experience Platform, consulte o [guia de solução de problemas do Experience Platform](../landing/troubleshooting.md).

**[!DNL Experience Data Model] (XDM)** é uma especificação de código aberto que define esquemas padronizados para o gerenciamento da experiência do cliente. A metodologia na qual [!DNL Experience Platform] é criado, **Sistema XDM**, operacionaliza [!DNL Experience Data Model] esquemas para uso pelos serviços [!DNL Experience Platform]. O **[!DNL Schema Registry]** fornece uma interface de usuário e uma API RESTful para acessar o **[!DNL Schema Library]** em [!DNL Experience Platform]. Consulte a [documentação do XDM](home.md) para obter mais informações.

## Perguntas frequentes

Veja a seguir uma lista de respostas para perguntas frequentes sobre o Sistema XDM e o uso da API [!DNL Schema Registry].

## Noções básicas de esquema

Nesta seção, você pode encontrar respostas para perguntas fundamentais sobre a estrutura do esquema, o uso de campo e a identificação no Sistema XDM.

### Como adicionar campos a um esquema?

Você pode adicionar campos a um esquema usando um grupo de campos de esquema. Cada grupo de campos é compatível com uma ou mais classes, permitindo que o grupo de campos seja usado em qualquer esquema que implemente uma dessas classes compatíveis. Embora a Adobe Experience Platform forneça vários grupos de campos do setor com seus próprios campos predefinidos, você pode adicionar seus próprios campos a um esquema criando grupos de campos personalizados usando a API ou a interface do usuário.

Para obter detalhes sobre como criar grupos de campos na API [!DNL Schema Registry], consulte o [manual de ponto de extremidade do grupo de campos](api/field-groups.md#create). Se você estiver usando a interface, consulte o [tutorial do Editor de esquemas](./tutorials/create-schema-ui.md).

### Quais são os melhores usos para grupos de campos em relação aos tipos de dados?

[Grupos de campos](./schema/composition.md#field-group) são componentes que definem um ou mais campos em um esquema. Os grupos de campos impõem como os campos aparecem na hierarquia do esquema e, portanto, exibem a mesma estrutura em cada esquema em que estão incluídos. Os grupos de campos são compatíveis apenas com classes específicas, conforme identificado pelo seu atributo `meta:intendedToExtend`.

[Os tipos de dados](./schema/composition.md#data-type) também podem fornecer um ou mais campos para um esquema. No entanto, diferentemente dos grupos de campos, os tipos de dados não estão restritos a uma classe específica. Isso torna os tipos de dados uma opção mais flexível para descrever estruturas de dados comuns que são reutilizáveis em vários esquemas com classes potencialmente diferentes.

### Qual é o identificador exclusivo de um esquema?

Todos os recursos do [!DNL Schema Registry] (esquemas, grupos de campos, tipos de dados, classes) têm um URI que atua como uma ID exclusiva para fins de referência e pesquisa. Ao visualizar um esquema na API, ele pode ser encontrado nos atributos `$id` e `meta:altId` de nível superior.

Para obter mais informações, consulte a seção [identificação de recursos](api/getting-started.md#resource-identification) no guia de API [!DNL Schema Registry].

### Qual é o tamanho máximo de um tipo de campo longo?

Um tipo de campo longo é um inteiro com um tamanho máximo de 53(+1) bits, dando a ele um intervalo potencial entre -9007199254740992 e 9007199254740992. Isso se deve a uma limitação de como as implementações do JavaScript de JSON representam números inteiros longos.

Para obter mais informações sobre tipos de campos, consulte o documento sobre [Restrições de tipo de campo XDM](./schema/field-constraints.md).

### O que é meta:AltId?

`meta:altId` é um identificador exclusivo para um esquema. O `meta:altId` fornece uma ID de referência fácil para uso em chamadas de API. Essa ID evita a necessidade de ser codificada/decodificada sempre que for usada como com o formato JSON URI.
<!-- (Needs clarification - How do I retrieve it INCOMPLETE) ... -->

<!-- ### How can I generate a sample payload for a schema? -->

<!-- No Answer available.  -->
<!-- INCOMPLETE ... -->

### Quais são as restrições de uso para um tipo de dados de mapa?

O XDM impõe as seguintes restrições ao uso desse tipo de dados:

- Os tipos de mapa DEVEM ser do tipo `object`.
- Os tipos de mapa NÃO DEVEM ter propriedades definidas (em outras palavras, eles definem objetos &quot;vazios&quot;).
- Os tipos de mapa DEVEM incluir um campo `additionalProperties.type` que descreva os valores que podem ser colocados no mapa, `string` ou `integer`.
- A segmentação de várias entidades só pode ser definida com base nas chaves do mapa, e não nos valores.
- Os mapas não são compatíveis com os públicos-alvo da conta.
- Os mapas definidos em objetos XDM personalizados são limitados a um único nível. Não é possível criar mapas aninhados. Essa restrição não se aplica a mapas definidos em objetos XDM padrão.
- Matrizes de mapas não são compatíveis.

Consulte as [restrições de uso para mapear objetos](./ui/fields/map.md#restrictions) para obter mais detalhes.

>[!NOTE]
>
>Não há suporte para mapas de vários níveis ou mapas de mapas.

<!-- You cannot create a complex map object. However, you can define map fields in the Schema Editor. See the guide on [defining map fields in the UI](./ui/fields/map.md) for more information. -->

<!-- ### How do I create a complex map object using APIs? -->

<!-- You cannot create a complex map object. -->

<!-- ### How can I manage schema inheritance in Adobe Experience Platform? -->

<!-- No Answer available.  -->
<!-- INCOMPLETE ... -->

## Schema Identity Management

Esta seção contém respostas a perguntas comuns sobre a definição e o gerenciamento de identidades em seus esquemas.

### Como definir identidades para meu esquema?

Em [!DNL Experience Platform], as identidades são usadas para identificar um assunto (normalmente uma pessoa física) independentemente das fontes de dados que estão sendo interpretadas. Eles são definidos em esquemas ao marcar campos principais como &quot;Identidade&quot;. Os campos comumente usados para identidade incluem endereço de email, número de telefone, [[!DNL Experience Cloud ID (ECID)]](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=pt-BR), ID de CRM e outros campos de ID exclusivos.

Os campos podem ser marcados como identidades usando a API ou a interface do usuário.

### Definição de identidades na API

Na API, as identidades são estabelecidas por meio da criação de descritores de identidade. Os descritores de identidade sinalizam que uma propriedade específica de um esquema é um identificador exclusivo.

Os descritores de identidade são criados por uma solicitação POST para o endpoint /descriptors. Se for bem-sucedido, você receberá um Status HTTP 201 (Criado) e um objeto de resposta contendo os detalhes do novo descritor.

Para obter mais detalhes sobre como criar descritores de identidade na API, consulte o documento na seção [descritores](api/descriptors.md) no guia do desenvolvedor [!DNL Schema Registry].

### Definição de identidades na interface

Com o esquema aberto no Editor de esquemas, selecione o campo na seção **[!UICONTROL Structure]** do editor que você deseja marcar como uma identidade. Em **[!UICONTROL Field Properties]**, no lado direito, marque a caixa de seleção **[!UICONTROL Identity]**.

Para obter mais detalhes sobre como gerenciar identidades na interface, consulte a seção sobre [definição de campos de identidade](./tutorials/create-schema-ui.md#identity-field) no tutorial do Editor de esquemas.

### Meu esquema precisa de uma identidade principal?

As identidades primárias são opcionais, pois os esquemas podem ter zero ou uma delas. No entanto, um esquema deve ter uma identidade primária para que o esquema seja habilitado para uso em [!DNL Real-Time Customer Profile]. Consulte a seção [identity](./tutorials/create-schema-ui.md#identity-field) do tutorial do Editor de esquemas para obter mais informações.

## Ativação do perfil de esquema

Esta seção fornece orientação sobre como ativar esquemas para uso com o Perfil de cliente em tempo real.

### Como habilitar um esquema para uso no [!DNL Real-Time Customer Profile]?

Os esquemas estão habilitados para uso em [[!DNL Real-Time Customer Profile]](../profile/home.md) por meio da adição de uma tag de &quot;união&quot; no atributo `meta:immutableTags` do esquema. A habilitação de um esquema para uso com [!DNL Profile] pode ser feita usando a API ou a interface do usuário.

### Habilitando um esquema existente para [!DNL Profile] usando a API

Faça uma solicitação PATCH para atualizar o esquema e adicionar o atributo `meta:immutableTags` como uma matriz contendo o valor &quot;union&quot;. Se a atualização for bem-sucedida, a resposta mostrará o esquema atualizado que agora contém a tag de união.

Para obter mais informações sobre como usar a API para habilitar um esquema para uso em [!DNL Real-Time Customer Profile], consulte o documento [unions](./api/unions.md) do guia do desenvolvedor [!DNL Schema Registry].

### Habilitando um esquema existente para [!DNL Profile] usando a interface

Em [!DNL Experience Platform], selecione **[!UICONTROL Schemas]** no menu de navegação esquerdo e selecione o nome do esquema que deseja habilitar na lista de esquemas. Em seguida, no lado direito do editor, em **[!UICONTROL Schema Properties]**, selecione **[!UICONTROL Profile]** para ativá-lo.

Para obter mais informações, consulte a seção sobre [usar em Perfil de Cliente em Tempo Real](./tutorials/create-schema-ui.md#profile) no tutorial [!UICONTROL Schema Editor].

### Quando os dados do Adobe Analytics são importados como uma origem, o esquema criado automaticamente é ativado para o Perfil?

O esquema não é ativado automaticamente para o Perfil de cliente em tempo real. Você precisa ativar explicitamente o conjunto de dados para o Perfil com base no esquema que está ativado para o Perfil. Consulte a documentação para saber as [etapas e os requisitos necessários para habilitar um conjunto de dados para uso no Perfil do Cliente em Tempo Real](../catalog/datasets/user-guide.md#enable-profile).

### Posso excluir esquemas habilitados para perfil? {#delete-profile-enabled}

Não é possível excluir um esquema depois que ele é ativado para o Perfil de cliente em tempo real. Depois que um esquema é ativado para o Perfil, ele não pode ser desativado ou excluído e os campos não podem ser removidos do esquema. Portanto, é crucial planejar e verificar cuidadosamente a configuração do esquema antes de habilitá-lo para o Perfil. No entanto, você pode excluir um conjunto de dados habilitado para perfil. Informações encontradas aqui: <https://experienceleague.adobe.com/en/docs/experience-platform/catalog/datasets/user-guide#delete-a-profile-enabled-dataset>

Se você não quiser mais que um esquema habilitado para perfil seja usado, é recomendável renomear o esquema para incluir **Não usar** ou **Inativo**.

## Modificação e restrições do esquema

Esta seção fornece esclarecimentos sobre as regras de modificação de schema e sobre a prevenção de alterações.

### Quando um esquema começa a impedir alterações?

Alterações interruptivas podem ser feitas em um esquema desde que ele nunca tenha sido usado na criação de um conjunto de dados ou esteja habilitado para uso no [[!DNL Real-Time Customer Profile]](../profile/home.md). Depois que um esquema é usado na criação do conjunto de dados ou habilitado para uso com [!DNL Real-Time Customer Profile], as regras de [Evolução do Esquema](schema/composition.md#evolution) tornam-se estritamente aplicadas pelo sistema.

### Posso editar um esquema de união diretamente?

Os esquemas de união são somente leitura e são gerados automaticamente pelo sistema. Eles não podem ser editados diretamente. Os esquemas de união são criados para uma classe específica quando uma tag de &quot;união&quot; é adicionada ao esquema que implementa essa classe.

Para obter mais informações sobre uniões no XDM, consulte a seção [uniões](./api/unions.md) no guia de API [!DNL Schema Registry].

### Como devo formatar meu arquivo de dados para assimilar dados no meu esquema?

[!DNL Experience Platform] aceita arquivos de dados no formato [!DNL Parquet] ou JSON. O conteúdo desses arquivos deve estar em conformidade com o esquema referenciado pelo conjunto de dados. Para obter detalhes sobre as práticas recomendadas para assimilação de arquivos de dados, consulte a [visão geral de assimilação em lote](../ingestion/home.md).

### Como posso converter um esquema em um esquema somente leitura?

No momento, não é possível converter um esquema em somente leitura.

## Erros e solução de problemas

Esta é uma lista de mensagens de erro que você pode encontrar ao trabalhar com a API [!DNL Schema Registry].

### Recurso não encontrado

```json
{
    "type": "http://ns.adobe.com/aep/errors/XDM-1010-404",
    "title": "Resource not found",
    "status": 404,
    "report": {
        "registryRequestId": "a15996b5-5133-4cec-9bf7-7d1207904ae3",
        "timestamp": "06-01-2021 04:11:06",
        "detailed-message": "The requested class resource https://ns.adobe.com/{TENANT_ID}/classes/11447bb484d4599d2cd9b0aseefff78b463cbbde1527f498 with version 1 is not found.",
        "sub-errors": []
    },
    "detail": "The requested class resource https://ns.adobe.com/{TENANT_ID}/classes/11447bb484d4599d2cd9b0aseefff78b463cbbde1527f498 with version 1 is not found."
}
```

Esse erro é exibido quando o sistema não consegue encontrar um recurso específico. O recurso pode ter sido excluído ou o caminho na chamada à API é inválido. Verifique se você inseriu um caminho válido para a chamada de API antes de tentar novamente. Você pode verificar se inseriu a ID correta para o recurso e se o caminho foi namespace corretamente com o container apropriado (global ou locatário).

>[!NOTE]
>
>Dependendo do tipo de recurso que está sendo recuperado, esse erro pode usar qualquer um dos `type` URIs a seguir:
>
>- `http://ns.adobe.com/aep/errors/XDM-1010-404`
>- `http://ns.adobe.com/aep/errors/XDM-1011-404`
>- `http://ns.adobe.com/aep/errors/XDM-1012-404`
>- `http://ns.adobe.com/aep/errors/XDM-1013-404`
>- `http://ns.adobe.com/aep/errors/XDM-1014-404`
>- `http://ns.adobe.com/aep/errors/XDM-1015-404`
>- `http://ns.adobe.com/aep/errors/XDM-1016-404`
>- `http://ns.adobe.com/aep/errors/XDM-1017-404`

Para obter mais informações sobre como construir caminhos de pesquisa na API, consulte as seções [contêiner](./api/getting-started.md#container) e [identificação de recursos](api/getting-started.md#resource-identification) no guia do desenvolvedor [!DNL Schema Registry].

### Título não exclusivo

```json
{
    "type": "http://ns.adobe.com/aep/errors/XDM-1521-400",
    "title": "Title not unique",
    "status": 400,
    "report": {
        "registryRequestId": "a15996b5-5133-4cec-9bf7-7d1207904ae3",
        "timestamp": "06-01-2021 04:11:06",
        "detailed-message": "Object titles must be unique. An object https://ns.adobe.com/{TENANT_ID}/classes/11447bb484d4599d2cd9b0aseefff78b463cbbde1527f498 already exists with the same title",
        "sub-errors": []
    },
    "detail": "Object titles must be unique. An object https://ns.adobe.com/{TENANT_ID}/classes/11447bb484d4599d2cd9b0aseefff78b463cbbde1527f498 already exists with the same title"
}
```

Essa mensagem de erro é exibida quando você tenta criar um recurso com um título que já está sendo usado por outro recurso. Os títulos devem ser exclusivos em todos os tipos de recursos. Por exemplo, se você tentar criar um grupo de campos com um título que já está sendo usado por um esquema, você receberá esse erro.

### Erro de validação de namespace

```json
{
    "type": "http://ns.adobe.com/aep/errors/XDM-1021-400",
    "title": "Namespace validation error",
    "status": 400,
    "report": {
        "registryRequestId": "a15996b5-5133-4cec-9bf7-7d1207904ae3",
        "timestamp": "06-01-2021 04:11:06",
        "detailed-message": "A custom field is defined under an invalid namespace. All custom fields must be defined under a top-level field named {TENANT_ID}.",
        "sub-errors": []
    },
    "detail": "A custom field is defined under an invalid namespace. All custom fields must be defined under a top-level field named {TENANT_ID}."
}
```

Essa mensagem de erro é exibida quando você tenta criar um recurso com campos com namespace incorretamente ou adicionar campos com namespace incorretamente a um recurso existente.

Os recursos definidos pela organização devem incluir os namespaces dos campos na ID do locatário para evitar conflitos com outros recursos do setor e do fornecedor. Ao criar um esquema usando grupos de campos padrão, todos os campos personalizados adicionados na estrutura desses grupos de campos também devem ter o namespace sob a ID do locatário.

>[!NOTE]
>
>Dependendo da natureza específica do erro de namespace, esse erro pode usar qualquer um dos `type` URIs a seguir, juntamente com diferentes detalhes da mensagem:
>
>- `http://ns.adobe.com/aep/errors/XDM-1020-400`
>- `http://ns.adobe.com/aep/errors/XDM-1021-400`
>- `http://ns.adobe.com/aep/errors/XDM-1022-400`
>- `http://ns.adobe.com/aep/errors/XDM-1023-400`
>- `http://ns.adobe.com/aep/errors/XDM-1024-400`

Exemplos detalhados de estruturas de dados adequadas para recursos XDM podem ser encontrados no guia da API do registro de esquema:

- [Criar uma classe personalizada](./api/classes.md#create)
- [Criar um grupo de campos personalizado](./api/field-groups.md#create)
- [Criar um tipo de dados personalizado](./api/data-types.md#create)

### Cabeçalho Aceitar inválido

```json
{
    "type": "http://ns.adobe.com/aep/errors/XDM-1006-400",
    "title": "Accept header invalid",
    "status": 400,
    "report": {
        "registryRequestId": "a15996b5-5133-4cec-9bf7-7d1207904ae3",
        "timestamp": "06-01-2021 04:11:06",
        "detailed-message": "The supplied Accept header is not valid: application/vnd.adobe.xed+json;version=1 - A valid Accept value should look like application/vnd.adobe.{xed|xdm}+json",
        "sub-errors": []
    },
    "detail": "The supplied Accept header is not valid: application/vnd.adobe.xed+json;version=1 - A valid Accept value should look like application/vnd.adobe.{xed|xdm}+json"
}
```

As solicitações do GET na API [!DNL Schema Registry] exigem um cabeçalho `Accept` para que o sistema determine como formatar a resposta. Este erro ocorre quando um cabeçalho `Accept` necessário é inválido ou está ausente.

Dependendo do ponto de extremidade que você está usando, a propriedade `detailed-message` indica como um cabeçalho `Accept` válido deve ser exibido para uma resposta bem-sucedida. Verifique se você inseriu corretamente um cabeçalho `Accept` que seja compatível com a solicitação de API que você está tentando fazer antes de tentar novamente.

>[!NOTE]
>
>Dependendo do ponto de extremidade sendo usado, esse erro pode usar qualquer um dos `type` URIs a seguir:
>
>- `http://ns.adobe.com/aep/errors/XDM-1006-400`
>- `http://ns.adobe.com/aep/errors/XDM-1007-400`
>- `http://ns.adobe.com/aep/errors/XDM-1008-400`
>- `http://ns.adobe.com/aep/errors/XDM-1009-400`

Para obter listas de cabeçalhos Accept compatíveis para diferentes solicitações de API, consulte as seções correspondentes no [guia do desenvolvedor do Registro de Esquemas](./api/overview.md).

### [!DNL Real-Time Customer Profile] erros

As mensagens de erro a seguir estão associadas a operações envolvidas na habilitação de esquemas para [!DNL Real-Time Customer Profile]. Consulte a seção [unions](./api/unions.md) no guia de API [!DNL Schema Registry] para obter mais informações.

#### Deve haver um descritor de identidade de referência

```json
{
    "type": "http://ns.adobe.com/aep/errors/XDM-1526-400",
    "title": "Union descriptor validation error",
    "status": 400,
    "report": {
        "registryRequestId": "a15996b5-5133-4cec-9bf7-7d1207904ae3",
        "timestamp": "06-01-2021 04:11:06",
        "detailed-message": "If a schema contains properties that are associated with an xdm:descriptorOneToOne descriptor, those properties must also have a xdm:descriptorReferenceIdentity descriptor for that schema to participate in a union.",
        "sub-errors": []
    },
    "detail": "If a schema contains properties that are associated with an xdm:descriptorOneToOne descriptor, those properties must also have a xdm:descriptorReferenceIdentity descriptor for that schema to participate in a union."
}
```

Esta mensagem de erro é exibida quando você tenta habilitar um esquema para [!DNL Profile] e uma de suas propriedades contém um descritor de relacionamento sem um descritor de identidade de referência. Adicione um descritor de identidade de referência ao campo de esquema em questão para resolver esse erro.

#### Os namespaces do campo do descritor de identidade de referência e do esquema de destino devem corresponder

```json
{
    "type": "http://ns.adobe.com/aep/errors/XDM-1527-400",
    "title": "Union descriptor validation error",
    "status": 400,
    "report": {
        "registryRequestId": "a15996b5-5133-4cec-9bf7-7d1207904ae3",
        "timestamp": "06-01-2021 04:11:06",
        "detailed-message": "If both schemas from an existing xdm:descriptorOneToOne descriptor are promoted to union, and one of those schemas contains a primary identity, the xdm:identityNamespace of the source schema's descriptorReferenceIdentity field must match the xdm:namespace field of destination schema's xdm:descriptorIdentity field.",
        "sub-errors": []
    },
    "detail": "If both schemas from an existing xdm:descriptorOneToOne descriptor are promoted to union, and one of those schemas contains a primary identity, the xdm:identityNamespace of the source schema's descriptorReferenceIdentity field must match the xdm:namespace field of destination schema's xdm:descriptorIdentity field."
}
```

>[!NOTE]
>
>Para esse erro, o &quot;schema de destino&quot; se refere ao schema de referência no relacionamento.

Para habilitar esquemas que contenham descritores de relacionamento para uso em [!DNL Profile], o namespace do campo de origem e o namespace primário do campo de referência devem ser os mesmos. Esta mensagem de erro é exibida quando você tenta ativar um esquema que contém um namespace sem correspondência para seu descritor de identidade de referência.

Para resolver esse problema, verifique se o valor `xdm:namespace` do campo de identidade do esquema de referência corresponde ao valor da propriedade `xdm:identityNamespace` no descritor de identidade de referência do campo de origem.

Para obter uma lista de códigos de namespace de identidade padrão, consulte a seção sobre [namespaces padrão](../identity-service/features/namespaces.md) na visão geral do namespace de identidade.

#### O esquema deve incluir um identityMap ou identidade primária

```json
{
    "type": "http://ns.adobe.com/aep/errors/XDM-1528-400",
    "title": "Union descriptor validation error",
    "status": 400,
    "report": {
        "registryRequestId": "a15996b5-5133-4cec-9bf7-7d1207904ae3",
        "timestamp": "06-01-2021 04:11:06",
        "detailed-message": "To participate in a union, a schema must include an identityMap fieldgroup or a primary identity descriptor.",
        "sub-errors": []
    },
    "detail": "To participate in a union, a schema must include an identityMap fieldgroup or a primary identity descriptor."
}
```

Antes de habilitar um esquema para Perfil, primeiro [crie um descritor de identidade primário](./api/descriptors.md#create) para o esquema ou inclua um campo de mapa de identidade para agir na identidade primária.

#### Não é possível mesclar tipos de dados incompatíveis

```json
{
    "type": "http://ns.adobe.com/aep/errors/XDM-1413-400",
    "title": "Merge Schema Error",
    "status": 400,
    "report": {
        "registryRequestId": "a15996b5-5133-4cec-9bf7-7d1207904ae3",
        "timestamp": "06-01-2021 04:11:06",
        "detailed-message": "Cannot merge incompatible data types. The path /person/name has already been defined in schema (id=0238be93d3e7a06aec5e0655955901ec) using a different data type. Types: string, object",
        "sub-errors": []
    },
    "detail": "Cannot merge incompatible data types. The path /person/name has already been defined in schema (id=0238be93d3e7a06aec5e0655955901ec) using a different data type. Types: string, object"
}
```

Todos os esquemas habilitados para perfil pertencentes à mesma classe devem poder se mesclar para construir o esquema de união para essa classe. Esse erro aparece quando você tenta adicionar um campo a um esquema cujo caminho é compartilhado por outro esquema habilitado para perfil e o tipo de dados é diferente do original. Como os esquemas são habilitados para perfil e contêm o mesmo caminho de campo, o Perfil tentaria mesclar esses dois campos em um ao construir o esquema de união. Como tipos de dados diferentes não podem ser mesclados juntos, isso seria considerado um conflito de mesclagem e não é permitido.

Para resolver o problema, escolha um nome diferente para o campo ou aninhe-o em um objeto com namespace exclusivo para evitar conflitos de mesclagem com outros esquemas habilitados para perfil na mesma classe com campos semelhantes.
