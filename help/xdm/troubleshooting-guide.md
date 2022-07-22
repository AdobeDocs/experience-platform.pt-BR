---
keywords: Experience Platform; tópicos populares; XDM; sistema XDM; perfil individual XDM; XDM ExperienceEvent; Evento de experiência XDM; experienceEvent; evento de experiência; Evento de experiência XDM; modelo de dados de experiência; modelo de dados de experiência; Modelo de dados de experiência; modelo de dados; modelo de dados; esquema; solução de problemas; perguntas frequentes; esquema de União; PROFIL DE UNIÃO; perfil de união; http://ns.adobe.com/aep/errors/XDM-1010-404;http://ns.adobe.com/aep/errors/XDM-1011-404;http://ns.adobe.com/aep/errors/XDM-1012-404;http://ns.adobe.com/aep/errors/XDM-1013-404;http://ns.adobe.com/aep/errors/XDM-1014-404;http://ns.adobe.com/aep/errors/XDM-1015-404;http://ns.adobe.com/aep/errors/XDM-1016-404;http://ns.adobe.com/aep/errors/XDM-1017-404;http://ns.adobe.com/aep/errors/XDM-1521-400;http://ns.adobe.com/aep/errors/XDM-1020-400;http://ns.adobe.com/aep/errors/XDM-1021-400;http://ns.adobe.com/aep/errors/XDM-1022-400;http://ns.adobe.com/aep/errors/XDM-1023-400;http://ns.adobe.com/aep/errors/XDM-1024-400;http://ns.adobe.com/aep/errors/XDM-1006-400;http://ns.adobe.com/aep/errors/XDM-1007-400;http://ns.adobe.com/aep/errors/XDM-1008-400;http://ns.adobe.com/aep/errors/XDM-1009-400;http://ns.adobe.com/aep/errors/XDM-1526-400;http://ns.adobe.com/aep/errors/XDM-1527-400;http://ns.adobe.com/aep/errors/XDM-1528-400;XDM-1010-404;XDM-1011-404;XDM-1012-404;XDM-1013-404;XDM-1014-404;XDM-1015-404;XDM-1016-404;XDM-1017-404;XDM-1521-400;XDM-1020-400;XDM-1021-400;XDM-1022-400;XDM-1023-400;XDM-1024-400;XDM-1006-400;XDM-1007-400;XDM-1008-400;XDM-1009-400;XDM-1413-400;XDM-1526-400;XDM-1527-400;XDM-1528-400;
solution: Experience Platform
title: Guia de solução de problemas do sistema XDM
description: Encontre respostas para perguntas frequentes sobre o Experience Data Model (XDM), incluindo etapas para resolver erros comuns da API.
topic-legacy: troubleshooting
exl-id: a0c7c661-bee8-4f66-ad5c-f669c52c9de3
source-git-commit: 5ffc93c8715d1184b2a239c1d631b117a531e5c1
workflow-type: tm+mt
source-wordcount: '2060'
ht-degree: 0%

---

# Guia de solução de problemas do sistema XDM

Este documento fornece respostas para perguntas frequentes sobre [!DNL Experience Data Model] (XDM) e Sistema XDM na Adobe Experience Platform, incluindo um guia de solução de problemas para erros comuns. Para dúvidas e solução de problemas relacionados a outros serviços da plataforma, consulte o [Guia de solução de problemas do Experience Platform](../landing/troubleshooting.md).

**[!DNL Experience Data Model](XDM)** é uma especificação de código aberto que define esquemas padronizados para o gerenciamento de experiência do cliente. A metodologia sobre a qual [!DNL Experience Platform] é construído, **Sistema XDM**, operacionaliza [!DNL Experience Data Model] esquemas a serem usados por [!DNL Platform] serviços. O **[!DNL Schema Registry]** fornece uma interface de usuário e uma RESTful API para acessar o **[!DNL Schema Library]** within [!DNL Experience Platform]. Consulte a [Documentação XDM](home.md) para obter mais informações.

## Perguntas frequentes

Veja a seguir uma lista das respostas às perguntas mais frequentes sobre o Sistema XDM e o uso do [!DNL Schema Registry] API.

### Como adiciono campos a um esquema?

É possível adicionar campos a um schema usando um grupo de campos de esquema. Cada grupo de campos é compatível com uma ou mais classes, permitindo que o grupo de campos seja usado em qualquer schema que implemente uma dessas classes compatíveis. Embora o Adobe Experience Platform forneça vários grupos de campos do setor com seus próprios campos predefinidos, é possível adicionar seus próprios campos a um schema criando grupos de campos personalizados usando a API ou a interface do usuário.

Para obter detalhes sobre a criação de grupos de campos na [!DNL Schema Registry] API, consulte o [guia de endpoint de grupo de campos](api/field-groups.md#create). Se você estiver usando a interface do usuário do , consulte o [Tutorial do Editor de esquemas](./tutorials/create-schema-ui.md).

### Quais são os melhores usos para grupos de campos vs tipos de dados?

[Grupos de campos](./schema/composition.md#field-group) são componentes que definem um ou mais campos em um schema. Os grupos de campos impõem como seus campos aparecem na hierarquia do esquema e, portanto, exibem a mesma estrutura em cada esquema em que estão incluídos. Os grupos de campos são compatíveis apenas com classes específicas, conforme identificado por seus `meta:intendedToExtend` atributo.

[Tipos de dados](./schema/composition.md#data-type) também pode fornecer um ou mais campos para um schema. No entanto, ao contrário de grupos de campos, os tipos de dados não estão restritos a uma classe específica. Isso torna os tipos de dados uma opção mais flexível para descrever estruturas de dados comuns que são reutilizáveis em vários esquemas com classes potencialmente diferentes.

### Qual é a ID exclusiva para um esquema?

Todos [!DNL Schema Registry] os recursos (esquemas, grupos de campos, tipos de dados, classes) têm um URI que atua como uma ID exclusiva para fins de referência e pesquisa. Ao visualizar um esquema na API, ele pode ser encontrado no nível superior `$id` e `meta:altId` atributos.

Para obter mais informações, consulte o [identificação de recursos](api/getting-started.md#resource-identification) na seção [!DNL Schema Registry] Guia da API.

### Quando um esquema começa a impedir a quebra de alterações?

As alterações de detalhamento podem ser feitas em um schema, desde que nunca tenha sido usado na criação de um conjunto de dados ou habilitado para uso em [[!DNL Real-time Customer Profile]](../profile/home.md). Depois que um schema é usado na criação do conjunto de dados ou ativado para uso com [!DNL Real-time Customer Profile], as regras de [Evolução do esquema](schema/composition.md#evolution) se torne estritamente aplicado pelo sistema.

### Qual é o tamanho máximo de um tipo de campo longo?

Um tipo de campo longo é um inteiro com um tamanho máximo de 53(+1) bits, fornecendo um intervalo potencial entre -9007199254740992 e 9007199254740992. Isso se deve a uma limitação de como as implementações JavaScript do JSON representam números inteiros longos.

Para obter mais informações sobre tipos de campos, consulte o documento em [Restrições do tipo de campo XDM](./schema/field-constraints.md).

### Como defino identidades para meu esquema?

Em [!DNL Experience Platform], as identidades são usadas para identificar um assunto (normalmente uma pessoa individual) independentemente das fontes de dados que estão sendo interpretadas. Eles são definidos em esquemas, marcando os campos principais como &quot;Identidade&quot;. Os campos usados frequentemente para identidade incluem endereço de email, número de telefone, [[!DNL Experience Cloud ID (ECID)]](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=pt-BR), ID do CRM e outros campos de ID exclusivos.

Os campos podem ser marcados como identidades usando a API ou a interface do usuário.

#### Definição de identidades na API

Na API, as identidades são estabelecidas criando descritores de identidade. Os descritores de identidade sinalizam que uma propriedade específica de um schema é um identificador exclusivo.

Os descritores de identidade são criados por uma solicitação POST para o endpoint /descriptors. Se bem-sucedido, você receberá um Status HTTP 201 (Criado) e um objeto de resposta contendo os detalhes do novo descritor.

Para obter mais detalhes sobre como criar descritores de identidade na API, consulte o documento em [descritores](api/descriptors.md) na seção [!DNL Schema Registry] guia do desenvolvedor.

#### Definição de identidades na interface do usuário

Com o esquema aberto no Editor de esquemas, selecione o campo no **[!UICONTROL Estrutura]** seção do editor que você deseja marcar como uma identidade. Em **[!UICONTROL Propriedades do campo]** no lado direito, selecione a opção **[!UICONTROL Identidade]** caixa de seleção.

Para obter mais detalhes sobre o gerenciamento de identidades na interface do usuário, consulte a seção sobre [definição de campos de identidade](./tutorials/create-schema-ui.md#identity-field) no tutorial do Editor de esquemas.

### Meu esquema precisa de uma identidade primária?

As identidades primárias são opcionais, uma vez que os esquemas podem ter zero ou um deles. No entanto, um schema deve ter uma identidade primária para que o schema seja ativado para uso em [!DNL Real-time Customer Profile]. Consulte a [identidade](./tutorials/create-schema-ui.md#identity-field) seção do tutorial do Editor de esquemas para obter mais informações.

### Como ativar um esquema para uso em [!DNL Real-time Customer Profile]?

Os esquemas são habilitados para uso em [[!DNL Real-time Customer Profile]](../profile/home.md) por meio da adição de uma tag &quot;union&quot; no `meta:immutableTags` do schema. Ativação de um esquema para usar com [!DNL Profile] pode ser feito usando a API ou a interface do usuário.

#### Ativação de um esquema existente para [!DNL Profile] uso da API

Faça uma solicitação do PATCH para atualizar o esquema e adicionar o `meta:immutableTags` como uma matriz contendo o valor &quot;union&quot;. Se a atualização for bem-sucedida, a resposta mostrará o schema atualizado que agora contém a tag de união.

Para obter mais informações sobre como usar a API para ativar um schema para uso em [!DNL Real-time Customer Profile], consulte o [sindicatos](./api/unions.md) documento do [!DNL Schema Registry] guia do desenvolvedor.

#### Ativação de um esquema existente para [!DNL Profile] uso da interface do usuário

Em [!DNL Experience Platform], selecione **[!UICONTROL Esquemas]** no menu de navegação à esquerda e selecione o nome do schema que deseja ativar na lista de schemas. Em seguida, no lado direito do editor sob **[!UICONTROL Propriedades do esquema]**, selecione **[!UICONTROL Perfil]** para ativá-lo.


Para obter mais informações, consulte a seção em [uso no Perfil do cliente em tempo real](./tutorials/create-schema-ui.md#profile) no [!UICONTROL Editor de esquema] tutorial.

### Posso editar um esquema de união diretamente?

Os esquemas de união são somente leitura e são gerados automaticamente pelo sistema. Eles não podem ser editados diretamente. Esquemas de união são criados para uma classe específica quando uma tag &quot;união&quot; é adicionada ao schema que implementa essa classe.

Para obter mais informações sobre uniões no XDM, consulte o [sindicatos](./api/unions.md) na seção [!DNL Schema Registry] Guia da API.

### Como devo formatar meu arquivo de dados para assimilar dados no esquema?

[!DNL Experience Platform] aceita arquivos de dados em [!DNL Parquet] ou formato JSON. O conteúdo desses arquivos deve estar em conformidade com o schema referenciado pelo conjunto de dados. Para obter detalhes sobre as práticas recomendadas para assimilação de arquivos de dados, consulte o [visão geral da ingestão em lote](../ingestion/home.md).

## Erros e solução de problemas

Veja a seguir uma lista de mensagens de erro que podem ser encontradas ao trabalhar com o [!DNL Schema Registry] API.

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

Esse erro é exibido quando o sistema não conseguiu encontrar um recurso específico. O recurso pode ter sido excluído ou o caminho na chamada da API é inválido. Certifique-se de ter inserido um caminho válido para sua chamada de API antes de tentar novamente. Você pode verificar se inseriu a ID correta para o recurso e se o caminho foi nomeado corretamente com o contêiner apropriado (global ou locatário).

>[!NOTE]
>
>Dependendo do tipo de recurso que está sendo recuperado, esse erro pode usar qualquer um dos seguintes `type` URIs:
>
>* `http://ns.adobe.com/aep/errors/XDM-1010-404`
>* `http://ns.adobe.com/aep/errors/XDM-1011-404`
>* `http://ns.adobe.com/aep/errors/XDM-1012-404`
>* `http://ns.adobe.com/aep/errors/XDM-1013-404`
>* `http://ns.adobe.com/aep/errors/XDM-1014-404`
>* `http://ns.adobe.com/aep/errors/XDM-1015-404`
>* `http://ns.adobe.com/aep/errors/XDM-1016-404`
>* `http://ns.adobe.com/aep/errors/XDM-1017-404`


Para obter mais informações sobre a construção de caminhos de pesquisa na API, consulte o [container](./api/getting-started.md#container) e [identificação de recursos](api/getting-started.md#resource-identification) nas seções da [!DNL Schema Registry] guia do desenvolvedor.

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

Essa mensagem de erro é exibida ao tentar criar um recurso com um título que já está sendo usado por outro recurso. Os títulos devem ser exclusivos em todos os tipos de recursos. Por exemplo, se você tentar criar um grupo de campos com um título que já está sendo usado por um esquema, você receberá esse erro.

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

Essa mensagem de erro é exibida ao tentar criar um recurso com campos com nomes inadequados ou adicionar campos com nomes inadequados a um recurso existente.

Os recursos que são definidos pela organização IMS devem namespace dos campos sob a ID do locatário para evitar conflitos com outros recursos do setor e do fornecedor. Ao criar um esquema usando grupos de campos padrão, todos os campos personalizados adicionados dentro da estrutura desses grupos de campos também devem ser namespacados sob a ID do locatário.

>[!NOTE]
>
>Dependendo da natureza específica do erro de namespace, esse erro pode usar qualquer um dos seguintes `type` URIs juntamente com diferentes detalhes de mensagem:
>
>* `http://ns.adobe.com/aep/errors/XDM-1020-400`
>* `http://ns.adobe.com/aep/errors/XDM-1021-400`
>* `http://ns.adobe.com/aep/errors/XDM-1022-400`
>* `http://ns.adobe.com/aep/errors/XDM-1023-400`
>* `http://ns.adobe.com/aep/errors/XDM-1024-400`


Exemplos detalhados de estruturas de dados adequadas para recursos XDM podem ser encontrados no guia da API do Registro de Schema:

* [Criar uma classe personalizada](./api/classes.md#create)
* [Criar um grupo de campos personalizado](./api/field-groups.md#create)
* [Criar um tipo de dados personalizado](./api/data-types.md#create)

### Aceitar cabeçalho inválido

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

As solicitações do GET na [!DNL Schema Registry] A API requer um `Accept` para que o sistema determine como formatar a resposta. Esse erro ocorre quando um `Accept` cabeçalho inválido ou ausente.

Dependendo do terminal que você estiver usando, a variável `detailed-message` a propriedade indica o que é válido `Accept` deve ser semelhante a uma resposta bem-sucedida. Certifique-se de ter inserido corretamente uma `Accept` cabeçalho compatível com a solicitação da API que você está tentando fazer antes de tentar novamente.

>[!NOTE]
>
>Dependendo do ponto de extremidade que está sendo usado, esse erro pode usar qualquer um dos seguintes `type` URIs:
>
>* `http://ns.adobe.com/aep/errors/XDM-1006-400`
>* `http://ns.adobe.com/aep/errors/XDM-1007-400`
>* `http://ns.adobe.com/aep/errors/XDM-1008-400`
>* `http://ns.adobe.com/aep/errors/XDM-1009-400`


Para obter listas de cabeçalhos Accept compatíveis para diferentes solicitações de API, consulte as seções correspondentes na seção [Guia do desenvolvedor do Registro de Schema](./api/overview.md).

### [!DNL Real-time Customer Profile] erros

As mensagens de erro a seguir estão associadas às operações envolvidas na ativação de schemas para o [!DNL Real-time Customer Profile]. Consulte a [sindicatos](./api/unions.md) na seção [!DNL Schema Registry] Guia de API para obter mais informações.

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

Essa mensagem de erro é exibida ao tentar ativar um esquema para [!DNL Profile] e uma de suas propriedades contém um descritor de relacionamento sem um descritor de identidade de referência. Adicione um descritor de identidade de referência ao campo de esquema em questão para resolver esse erro.

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

Para ativar schemas que contêm descritores de relacionamento para uso em [!DNL Profile], o namespace do campo de origem e o namespace primário do campo de destino devem ser iguais. Essa mensagem de erro é exibida ao tentar ativar um esquema que contém um namespace sem correspondência para seu descritor de identidade de referência. Certifique-se de que `xdm:namespace` o valor do campo de identidade do schema de destino corresponde ao do `xdm:identityNamespace` no descritor de identidade de referência do campo de origem para resolver esse problema.

Para obter uma lista de códigos de namespace de identidade padrão, consulte a seção em [namespaces padrão](../identity-service/namespaces.md) na visão geral do namespace de identidade.

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

Antes de habilitar um esquema para o Perfil, primeiro você deve [criar um descritor de identidade primário](./api/descriptors.md#create) para o esquema ou inclua um campo de mapa de identidade para agir na identidade primária.

#### Não é possível unir tipos de dados incompatíveis

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

Todos os esquemas ativados por perfil pertencentes à mesma classe devem ser capazes de mesclar para construir o schema de união para essa classe. Esse erro é exibido quando você tenta adicionar um campo a um esquema cujo caminho é compartilhado por outro esquema habilitado para perfil e o tipo de dados é diferente do original. Como os esquemas são ativados por Perfil e contêm o mesmo caminho de campo, o Perfil tentaria mesclar esses dois campos em um ao construir o esquema de união. Como tipos de dados diferentes não podem ser mesclados, isso seria considerado um conflito de mesclagem e não seria permitido.

Para resolver o problema, escolha um nome diferente para o campo ou aninhe-o em um objeto com namespaced exclusivo para evitar conflitos de mesclagem com outros esquemas ativados por perfil na mesma classe com campos semelhantes.
