---
keywords: Experience Platform;tópicos populares;XDM;sistema XDM;perfil individual XDM;XDM ExperienceEvent;Evento de experiência XDM;evento experienceEvent;evento experienceExperience;Evento de experiência XDM;XDM ExperienceEvent;modelo de dados de experiência;modelo de dados de experiência;modelo de dados de experiência;modelo de dados;modelo de dados;esquema;solução de problemas;perguntas frequentes;esquema de união;PERFIL DE UNIÃO;perfil de união;http://ns.adobe.com/aep/errors/XDM-1010-404;http://ns.adobe.com/aep/errors/XDM-1011-404;http://ns.adobe.com/aep/errors/XDM-1012-404;http://ns.adobe.com/aep/errors/XDM-1013-404;http://ns.adobe.com/aep/errors/XDM-1014-404;http://ns.adobe.com/aep/errors/XDM-1015-404;http://ns.adobe.com/aep/errors/XDM-1016-404;http://ns.adobe.com/aep/errors/XDM-1017-404;http://ns.adobe.com/aep/errors/XDM-1521-400;http://ns.adobe.com/aep/errors/XDM-1020-400;http://ns.adobe.com/aep/errors/XDM-1021-400;http://ns.adobe.com/aep/errors/XDM-1022-400;http://ns.adobe.com/aep/errors/XDM-1023-400;http://ns.adobe.com/aep/errors/XDM-1024-400;http://ns.adobe.com/aep/errors/XDM-1006-400;http://ns.adobe.com/aep/errors/XDM-1007-400;http://ns.adobe.com/aep/errors/XDM-1008-400;http://ns.adobe.com/aep/errors/XDM-1009-400;http://ns.adobe.com/aep/errors/XDM-1526-400;http://ns.adobe.com/aep/errors/XDM-1527-400;http://ns.adobe.com/aep/errors/XDM-1528-400;XDM-1010-404;XDM-1011-404;XDM-1012-404;XDM-1013-404;XDM-1014-404;XDM-1015-404;XDM-1016-404;XDM-1017-404;XDM-1521-400;XDM-1020-400;XDM-1021-400;XDM-1022-400;XDM-1023-400;XDM-1024-400;XDM-1006-400;XDM-1007-400;XDM-1008-400;XDM-1009-400;XDM-1413-400;XDM-1526-400;XDM-1527-400;XDM-1528-400;
solution: Experience Platform
title: Guia de solução de problemas do sistema XDM
description: Encontre respostas para perguntas frequentes sobre o Experience Data Model (XDM), incluindo etapas para resolver erros comuns de API.
exl-id: a0c7c661-bee8-4f66-ad5c-f669c52c9de3
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '2073'
ht-degree: 0%

---

# Guia de solução de problemas do sistema XDM

Este documento fornece respostas a perguntas frequentes sobre [!DNL Experience Data Model] (XDM) e Sistema XDM no Adobe Experience Platform, incluindo um guia de solução de problemas para erros comuns. Para perguntas e solução de problemas relacionados a outros serviços da Platform, consulte o [guia de solução de problemas do Experience Platform](../landing/troubleshooting.md).

**[!DNL Experience Data Model](XDM)** é uma especificação de código aberto que define esquemas padronizados para o gerenciamento da experiência do cliente. A metodologia com base na qual [!DNL Experience Platform] é criado, **Sistema XDM**, operacionaliza [!DNL Experience Data Model] esquemas para uso por [!DNL Platform] serviços. A variável **[!DNL Schema Registry]** O fornece uma interface de usuário e uma API RESTful para acessar o **[!DNL Schema Library]** no prazo de [!DNL Experience Platform]. Consulte a [Documentação XDM](home.md) para obter mais informações.

## Perguntas frequentes

Veja a seguir uma lista de respostas para perguntas frequentes sobre o Sistema XDM e o uso do [!DNL Schema Registry] API.

### Como adicionar campos a um esquema?

Você pode adicionar campos a um esquema usando um grupo de campos de esquema. Cada grupo de campos é compatível com uma ou mais classes, permitindo que o grupo de campos seja usado em qualquer esquema que implemente uma dessas classes compatíveis. Embora a Adobe Experience Platform forneça vários grupos de campos do setor com seus próprios campos predefinidos, você pode adicionar seus próprios campos a um esquema criando grupos de campos personalizados usando a API ou a interface do usuário.

Para obter detalhes sobre a criação de grupos de campos no [!DNL Schema Registry] , consulte a [guia de ponto de extremidade do grupo de campos](api/field-groups.md#create). Se estiver usando a interface do usuário, consulte a [Tutorial do Editor de esquemas](./tutorials/create-schema-ui.md).

### Quais são os melhores usos para grupos de campos em relação aos tipos de dados?

[Grupos de campos](./schema/composition.md#field-group) são componentes que definem um ou mais campos em um esquema. Os grupos de campos impõem como os campos aparecem na hierarquia do esquema e, portanto, exibem a mesma estrutura em cada esquema em que estão incluídos. Os grupos de campos são compatíveis apenas com classes específicas, conforme identificado por seus `meta:intendedToExtend` atributo.

[Tipos de dados](./schema/composition.md#data-type) O também pode fornecer um ou mais campos para um esquema. No entanto, diferentemente dos grupos de campos, os tipos de dados não estão restritos a uma classe específica. Isso torna os tipos de dados uma opção mais flexível para descrever estruturas de dados comuns que são reutilizáveis em vários esquemas com classes potencialmente diferentes.

### Qual é o identificador exclusivo de um esquema?

Todos [!DNL Schema Registry] Os recursos do (esquemas, grupos de campos, tipos de dados, classes) têm um URI que atua como uma ID exclusiva para fins de referência e pesquisa. Ao visualizar um esquema na API, ele pode ser encontrado no painel `$id` e `meta:altId` atributos.

Para obter mais informações, consulte [identificação de recursos](api/getting-started.md#resource-identification) na seção [!DNL Schema Registry] Guia da API.

### Quando um esquema começa a impedir alterações?

Alterações interruptivas podem ser feitas em um esquema, desde que ele nunca tenha sido usado na criação de um conjunto de dados ou esteja habilitado para uso no [[!DNL Real-Time Customer Profile]](../profile/home.md). Depois que um esquema tiver sido usado na criação do conjunto de dados ou ativado para uso com [!DNL Real-Time Customer Profile], as regras de [Evolução do esquema](schema/composition.md#evolution) seja estritamente aplicado pelo sistema.

### Qual é o tamanho máximo de um tipo de campo longo?

Um tipo de campo longo é um inteiro com um tamanho máximo de 53(+1) bits, dando a ele um intervalo potencial entre -9007199254740992 e 9007199254740992. Isso se deve a uma limitação de como as implementações JavaScript do JSON representam números inteiros longos.

Para obter mais informações sobre tipos de campo, consulte o documento sobre [Restrições de tipo de campo XDM](./schema/field-constraints.md).

### Como definir identidades para meu esquema?

Entrada [!DNL Experience Platform], as identidades são usadas para identificar um assunto (normalmente uma pessoa), independentemente das fontes de dados que estão sendo interpretadas. Eles são definidos em esquemas ao marcar campos principais como &quot;Identidade&quot;. Os campos comumente usados para identidade incluem endereço de email, número de telefone, [[!DNL Experience Cloud ID (ECID)]](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=pt-BR), ID do CRM e outros campos de ID exclusiva.

Os campos podem ser marcados como identidades usando a API ou a interface do usuário.

#### Definição de identidades na API

Na API, as identidades são estabelecidas por meio da criação de descritores de identidade. Os descritores de identidade sinalizam que uma propriedade específica de um esquema é um identificador exclusivo.

Os descritores de identidade são criados por uma solicitação POST para o endpoint /descriptors. Se for bem-sucedido, você receberá um Status HTTP 201 (Criado) e um objeto de resposta contendo os detalhes do novo descritor.

Para obter mais detalhes sobre como criar descritores de identidade na API, consulte o documento em [descritores](api/descriptors.md) na seção [!DNL Schema Registry] guia do desenvolvedor.

#### Definição de identidades na interface

Com seu esquema aberto no Editor de esquemas, selecione o campo no **[!UICONTROL Estrutura]** seção do editor que você deseja marcar como uma identidade. Em **[!UICONTROL Propriedades do campo]** no lado direito, selecione o **[!UICONTROL Identidade]** caixa de seleção

Para obter mais detalhes sobre o gerenciamento de identidades na interface do usuário, consulte a seção sobre [definição de campos de identidade](./tutorials/create-schema-ui.md#identity-field) no tutorial do Editor de esquemas.

### Meu esquema precisa de uma identidade principal?

As identidades primárias são opcionais, pois os esquemas podem ter zero ou uma delas. No entanto, um esquema deve ter uma identidade primária para que seja ativado para uso no [!DNL Real-Time Customer Profile]. Consulte a [identidade](./tutorials/create-schema-ui.md#identity-field) seção do tutorial Editor de esquemas para obter mais informações.

### Como ativar um esquema para uso no [!DNL Real-Time Customer Profile]?

Os esquemas estão ativados para uso no [[!DNL Real-Time Customer Profile]](../profile/home.md) por meio da adição de uma tag de &quot;união&quot; no `meta:immutableTags` atributo do esquema. Ativar um esquema para uso com [!DNL Profile] pode ser feito usando a API ou a interface do usuário.

#### Ativação de um esquema existente para [!DNL Profile] uso da API

Faça uma solicitação PATCH para atualizar o esquema e adicionar o `meta:immutableTags` atributo como uma matriz contendo o valor &quot;union&quot;. Se a atualização for bem-sucedida, a resposta mostrará o esquema atualizado que agora contém a tag de união.

Para obter mais informações sobre como usar a API para ativar um esquema para uso no [!DNL Real-Time Customer Profile], consulte o [uniões](./api/unions.md) documento do [!DNL Schema Registry] guia do desenvolvedor.

#### Ativação de um esquema existente para [!DNL Profile] uso da interface

Entrada [!DNL Experience Platform], selecione **[!UICONTROL Esquemas]** no menu de navegação esquerdo, e selecione o nome do schema que deseja ativar na lista de schemas. Em seguida, no lado direito do editor, em **[!UICONTROL Propriedades do esquema]**, selecione **[!UICONTROL Perfil]** para ativá-lo.


Para obter mais informações, consulte a seção sobre [usar no Perfil do cliente em tempo real](./tutorials/create-schema-ui.md#profile) no [!UICONTROL Editor de esquema] tutorial.

### Posso editar um esquema de união diretamente?

Os esquemas de união são somente leitura e são gerados automaticamente pelo sistema. Eles não podem ser editados diretamente. Os esquemas de união são criados para uma classe específica quando uma tag de &quot;união&quot; é adicionada ao esquema que implementa essa classe.

Para obter mais informações sobre uniões no XDM, consulte o [uniões](./api/unions.md) na seção [!DNL Schema Registry] Guia da API.

### Como devo formatar meu arquivo de dados para assimilar dados no meu esquema?

[!DNL Experience Platform] aceita arquivos de dados em [!DNL Parquet] ou JSON. O conteúdo desses arquivos deve estar em conformidade com o esquema referenciado pelo conjunto de dados. Para obter detalhes sobre as práticas recomendadas para assimilação de arquivos de dados, consulte o [visão geral da assimilação em lote](../ingestion/home.md).

## Erros e solução de problemas

Veja a seguir uma lista de mensagens de erro que você pode encontrar ao trabalhar com o [!DNL Schema Registry] API.

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


Para obter mais informações sobre como construir caminhos de pesquisa na API, consulte a [container](./api/getting-started.md#container) e [identificação de recursos](api/getting-started.md#resource-identification) seções na [!DNL Schema Registry] guia do desenvolvedor.

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
>Dependendo da natureza específica do erro de namespace, esse erro pode usar qualquer um dos seguintes `type` URIs juntamente com diferentes detalhes da mensagem:
>
>* `http://ns.adobe.com/aep/errors/XDM-1020-400`
>* `http://ns.adobe.com/aep/errors/XDM-1021-400`
>* `http://ns.adobe.com/aep/errors/XDM-1022-400`
>* `http://ns.adobe.com/aep/errors/XDM-1023-400`
>* `http://ns.adobe.com/aep/errors/XDM-1024-400`


Exemplos detalhados de estruturas de dados adequadas para recursos XDM podem ser encontrados no guia da API do registro de esquema:

* [Criar uma classe personalizada](./api/classes.md#create)
* [Criar um grupo de campos personalizado](./api/field-groups.md#create)
* [Criar um tipo de dados personalizado](./api/data-types.md#create)

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

solicitações do GET no [!DNL Schema Registry] A API exige um `Accept` para que o sistema determine como formatar a resposta. Esse erro ocorre quando uma solicitação `Accept` cabeçalho inválido ou ausente.

Dependendo do endpoint que você estiver usando, a variável `detailed-message` indica o que uma propriedade válida `Accept` O cabeçalho deve parecer com para uma resposta bem-sucedida. Verifique se você inseriu corretamente um `Accept` cabeçalho compatível com a solicitação de API que você está tentando fazer antes de tentar novamente.

>[!NOTE]
>
>Dependendo do endpoint que está sendo usado, esse erro pode usar um dos seguintes `type` URIs:
>
>* `http://ns.adobe.com/aep/errors/XDM-1006-400`
>* `http://ns.adobe.com/aep/errors/XDM-1007-400`
>* `http://ns.adobe.com/aep/errors/XDM-1008-400`
>* `http://ns.adobe.com/aep/errors/XDM-1009-400`


Para obter listas de cabeçalhos Accept compatíveis para diferentes solicitações de API, consulte as seções correspondentes no [Guia do desenvolvedor do Registro de esquema](./api/overview.md).

### [!DNL Real-Time Customer Profile] erros

As seguintes mensagens de erro estão associadas às operações envolvidas na ativação de esquemas para [!DNL Real-Time Customer Profile]. Consulte a [uniões](./api/unions.md) na seção [!DNL Schema Registry] Guia de API para obter mais informações.

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

Esta mensagem de erro é exibida quando você tenta ativar um esquema para [!DNL Profile] e uma de suas propriedades contém um descritor de relacionamento sem um descritor de identidade de referência. Adicione um descritor de identidade de referência ao campo de esquema em questão para resolver esse erro.

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

Certifique-se de que o `xdm:namespace` valor do campo de identidade do esquema de referência corresponde ao do `xdm:identityNamespace` no descritor de identidade de referência do campo de origem para resolver esse problema.

Para obter uma lista de códigos de namespace de identidade padrão, consulte a seção sobre [namespaces padrão](../identity-service/namespaces.md) na visão geral do namespace de identidade.

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

Antes de habilitar um esquema para o Perfil, primeiro você deve [criar um descritor de identidade principal](./api/descriptors.md#create) para o esquema ou inclua um campo de mapa de identidade para agir na identidade principal.

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
