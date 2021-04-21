---
keywords: Experience Platform; home; tópicos populares; XDM; sistema XDM; perfil individual XDM; XDM ExperienceEvent; Evento de experiência XDM; evento de experiência; evento de experiência; Evento de experiência XDM; Evento de experiência XDM; modelo de dados de experiência; Modelo de dados de experiência; Modelo de dados; modelo de dados; esquema; solução de problemas; perguntas frequentes; esquema de União; PERFIL DE UNIÃO; perfil de união
solution: Experience Platform
title: Guia de solução de problemas do sistema XDM
description: Este documento fornece respostas a perguntas frequentes sobre o Experience Data Model (XDM) e o Sistema XDM na Adobe Experience Platform, bem como um guia de solução de problemas para erros comuns.
topic-legacy: troubleshooting
exl-id: a0c7c661-bee8-4f66-ad5c-f669c52c9de3
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1869'
ht-degree: 0%

---

# Guia de solução de problemas do sistema XDM

Este documento fornece respostas a perguntas frequentes sobre [!DNL Experience Data Model] (XDM) e o sistema XDM no Adobe Experience Platform, bem como um guia de solução de problemas para erros comuns. Para dúvidas e solução de problemas relacionados a outros serviços da plataforma, consulte o [Guia de solução de problemas do Experience Platform](../landing/troubleshooting.md).

**[!DNL Experience Data Model](XDM)** é uma especificação de código aberto que define esquemas padronizados para o gerenciamento da experiência do cliente. A metodologia na qual [!DNL Experience Platform] é criado, **Sistema XDM**, opera [!DNL Experience Data Model] esquemas para uso pelos serviços [!DNL Platform]. O **[!DNL Schema Registry]** fornece uma interface de usuário e uma RESTful API para acessar o **[!DNL Schema Library]** dentro de [!DNL Experience Platform]. Consulte a [documentação XDM](home.md) para obter mais informações.

## Perguntas frequentes

Veja a seguir uma lista de respostas para perguntas frequentes sobre o Sistema XDM e o uso da API [!DNL Schema Registry].

### Como adiciono campos a um esquema?

É possível adicionar campos a um schema usando uma combinação. Cada mixin é compatível com uma ou mais classes, permitindo que a mixin seja usada em qualquer schema que implemente uma dessas classes compatíveis. Embora o Adobe Experience Platform forneça vários mixins do setor com seus próprios campos predefinidos, você pode adicionar seus próprios campos a um schema criando novos mixins usando a API ou a interface do usuário.

Para obter detalhes sobre como criar novas combinações na API [!DNL Schema Registry], consulte o [guia de ponto de extremidade mixin](api/mixins.md#create). Se estiver usando a interface do usuário, consulte o [Tutorial do Editor de Esquema](./tutorials/create-schema-ui.md).

### Quais são os melhores usos para mixins e tipos de dados?

[](./schema/composition.md#mixin) Mixinssão componentes que definem um ou mais campos em um schema. As misturas impõem como seus campos aparecem na hierarquia do schema e, portanto, exibem a mesma estrutura em cada schema no qual estão incluídos. As misturas só são compatíveis com classes específicas, conforme identificadas pelo seu atributo `meta:intendedToExtend`.

[Os ](./schema/composition.md#data-type) tipos de dados também podem fornecer um ou mais campos para um esquema. No entanto, ao contrário de mixins, os tipos de dados não são restritos a uma classe específica. Isso torna os tipos de dados uma opção mais flexível para descrever estruturas de dados comuns que são reutilizáveis em vários esquemas com classes potencialmente diferentes.

### Qual é a ID exclusiva para um esquema?

Todos os recursos [!DNL Schema Registry] (esquemas, mixagens, tipos de dados, classes) têm um URI que atua como uma ID exclusiva para fins de referência e pesquisa. Ao visualizar um esquema na API, ele pode ser encontrado nos atributos de nível superior `$id` e `meta:altId`.

Para obter mais informações, consulte a seção [identificação de recursos](api/getting-started.md#resource-identification) no guia do desenvolvedor da API [!DNL Schema Registry].

### Quando um esquema começa a impedir a quebra de alterações?

É possível fazer alterações importantes em um schema, desde que nunca tenha sido usado na criação de um conjunto de dados ou habilitado para uso em [[!DNL Real-time Customer Profile]](../profile/home.md). Depois que um schema tiver sido usado na criação do conjunto de dados ou ativado para uso com [!DNL Real-time Customer Profile], as regras de [Evolução do esquema](schema/composition.md#evolution) se tornarão estritamente aplicadas pelo sistema.

### Qual é o tamanho máximo de um tipo de campo longo?

Um tipo de campo longo é um inteiro com um tamanho máximo de 53(+1) bits, fornecendo um intervalo potencial entre -9007199254740992 e 9007199254740992. Isso se deve a uma limitação de como as implementações JavaScript do JSON representam números inteiros longos.

Para obter mais informações sobre tipos de campos, consulte o documento sobre [restrições de tipo de campo XDM](./schema/field-constraints.md).

### Como defino identidades para meu esquema?

Em [!DNL Experience Platform], as identidades são usadas para identificar um assunto (normalmente uma pessoa individual) independentemente das fontes de dados que estão sendo interpretadas. Eles são definidos em esquemas, marcando os campos principais como &quot;Identidade&quot;. Os campos usados frequentemente para a identidade incluem endereço de email, número de telefone, [[!DNL Experience Cloud ID (ECID)]](https://experienceleague.adobe.com/docs/id-service/using/home.html), ID do CRM e outros campos de ID exclusivos.

Os campos podem ser marcados como identidades usando a API ou a interface do usuário.

#### Definição de identidades na API

Na API, as identidades são estabelecidas criando descritores de identidade. Os descritores de identidade sinalizam que uma propriedade específica de um schema é um identificador exclusivo.

Os descritores de identidade são criados por uma solicitação POST para o endpoint /descriptors. Se bem-sucedido, você receberá um Status HTTP 201 (Criado) e um objeto de resposta contendo os detalhes do novo descritor.

Para obter mais detalhes sobre como criar descritores de identidade na API, consulte o documento na seção [descritores](api/descriptors.md) no guia do desenvolvedor [!DNL Schema Registry].

#### Definição de identidades na interface do usuário

Com o esquema aberto no Editor de esquemas, selecione o campo na seção **[!UICONTROL Structure]** do editor que deseja marcar como uma identidade. Em **[!UICONTROL Field Properties]** no lado direito, marque a caixa de seleção **[!UICONTROL Identity]**.

Para obter mais detalhes sobre como gerenciar identidades na interface do usuário, consulte a seção [definindo campos de identidade](./tutorials/create-schema-ui.md#identity-field) no tutorial Editor de esquemas .

### Meu esquema precisa de uma identidade primária?

As identidades primárias são opcionais, uma vez que os esquemas podem ter 0 ou 1 delas. No entanto, um schema deve ter uma identidade primária para que o schema seja ativado para uso em [!DNL Real-time Customer Profile]. Consulte a seção [identity](./tutorials/create-schema-ui.md#identity-field) do tutorial do Editor de esquemas para obter mais informações.

### Como habilito um esquema para usar em [!DNL Real-time Customer Profile]?

Os esquemas são habilitados para uso em [[!DNL Real-time Customer Profile]](../profile/home.md) por meio da adição de uma tag &quot;union&quot;, localizada no atributo `meta:immutableTags` do esquema. Habilitar um esquema para usar com [!DNL Profile] pode ser feito usando a API ou a interface do usuário.

#### Habilitar um esquema existente para [!DNL Profile] usando a API

Faça uma solicitação PATCH para atualizar o schema e adicionar o atributo `meta:immutableTags` como uma matriz contendo o valor &quot;union&quot;. Se a atualização for bem-sucedida, a resposta mostrará o schema atualizado que agora contém a tag de união.

Para obter mais informações sobre como usar a API para ativar um schema para uso em [!DNL Real-time Customer Profile], consulte o documento [union](./api/unions.md) do guia do desenvolvedor [!DNL Schema Registry].

#### Ativar um esquema existente para [!DNL Profile] usando a interface do usuário

Em [!DNL Experience Platform], selecione **[!UICONTROL Schemas]** na navegação à esquerda e selecione o nome do schema que deseja ativar na lista de schemas. Em seguida, no lado direito do editor, em **[!UICONTROL Schema Properties]**, selecione **[!UICONTROL Profile]** para ativá-lo.


Para obter mais informações, consulte a seção em [usar no Perfil do cliente em tempo real](./tutorials/create-schema-ui.md#profile) no tutorial [!UICONTROL Schema Editor].

### Posso editar um esquema de união diretamente?

Os esquemas de união são somente leitura e são gerados automaticamente pelo sistema. Eles não podem ser editados diretamente. Esquemas de união são criados para uma classe específica quando uma tag &quot;união&quot; é adicionada ao schema que implementa essa classe.

Para obter mais informações sobre uniões no XDM, consulte a seção [Uniões](./api/unions.md) no guia do desenvolvedor da API [!DNL Schema Registry].

### Como devo formatar meu arquivo de dados para assimilar dados no esquema?

[!DNL Experience Platform] aceita arquivos de dados no formato  [!DNL Parquet] ou JSON. O conteúdo desses arquivos deve estar em conformidade com o schema referenciado pelo conjunto de dados. Para obter detalhes sobre as práticas recomendadas para assimilação de arquivo de dados, consulte a [visão geral da assimilação de lote](../ingestion/home.md).

## Erros e solução de problemas

Esta é uma lista de mensagens de erro que podem ser encontradas ao trabalhar com a API [!DNL Schema Registry].

### Objeto não encontrado

```json
{
    "type": "/placeholder/type/uri",
    "status": 404,
    "title": "NotFoundError",
    "detail": "Object https://ns.adobe.com/incorrectTenantId/schemas/ee067e31b08514d21e2b82577813409d 
      with version 1 not found"
}
```

Esse erro é exibido quando o sistema não conseguiu encontrar um recurso específico. O recurso pode ter sido excluído ou o caminho na chamada da API é inválido. Certifique-se de ter inserido um caminho válido para sua chamada de API antes de tentar novamente. Você pode verificar se inseriu a ID correta para o recurso e se o caminho foi nomeado corretamente com o contêiner apropriado (global ou locatário).

Para obter mais informações sobre como construir caminhos de pesquisa na API, consulte as seções [container](./api/getting-started.md#container) e [resource identification](api/getting-started.md#resource-identification) no guia do desenvolvedor [!DNL Schema Registry].

### O título deve ser exclusivo

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "Title must be unique. An object 
      https://ns.adobe.com/{TENANT_ID}/schemas/26f6833e55db1dd8308aa07a64f2042d 
      already exists with the same title."
}
```

Essa mensagem de erro é exibida ao tentar criar um recurso com um título que já está sendo usado por outro recurso. Os títulos devem ser exclusivos em todos os tipos de recursos. Por exemplo, se você tentar criar um mixin com um título que já está sendo usado por um schema, você receberá esse erro.

### Os campos personalizados devem usar um campo de nível superior

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "For custom fields, you must use a top level field named _{TENANT_ID}
       and all the other fields must be defined under it"
}
```

Esta mensagem de erro é exibida ao tentar criar uma nova combinação com campos com nomes inadequados. As misturas definidas pela organização IMS devem colocar os campos no nome com um `TENANT_ID` para evitar conflitos com outros recursos do setor e do fornecedor. Exemplos detalhados de estruturas de dados adequadas para mixins podem ser encontrados no [guia de ponto de extremidade mixins](./api/mixins.md#create).


### [!DNL Real-time Customer Profile] erros

As mensagens de erro a seguir estão associadas a operações envolvidas na ativação de schemas para [!DNL Real-time Customer Profile]. Consulte a seção [union](./api/unions.md) no guia do desenvolvedor da API [!DNL Schema Registry] para obter mais informações.

#### Para ativar os conjuntos de dados de perfil, o esquema deve ser válido

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "To enable profile datasets the schema should be valid"
}
```

Esta mensagem de erro é exibida ao tentar ativar um conjunto de dados de perfil para um esquema que não foi ativado para [!DNL Real-time Customer Profile]. Verifique se o esquema contém uma tag de união antes de habilitar o conjunto de dados.

#### Deve haver um descritor de identidade de referência

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "For a schema to be able to participate in union, if any of its 
      property is associated with a xdm:descriptorOneToOne descriptor, there must 
      be a xdm:descriptorReferenceIdentity descriptor for that property"
}
```

Esta mensagem de erro é exibida ao tentar ativar um esquema para [!DNL Profile] e uma de suas propriedades contém um descritor de relacionamento sem um descritor de identidade de referência. Adicione um descritor de identidade de referência ao campo de esquema em questão para resolver esse erro.

#### Os namespaces do campo do descritor de identidade de referência e do esquema de destino devem corresponder

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "If both schemas from an already defined xdm:descriptorOneToOne 
      descriptor are promoted to union, and if there is a primary identity on one of 
      the schemas from the xdm:descriptorOneToOne descriptor, the 
      xdm:identityNamespace of the sourceSchema's descriptorReferenceIdentity and the 
      xdm:namespace field of the xdm:descriptorIdentity for the destinationSchema must 
      match"
}
```

Para habilitar schemas que contêm descritores de relacionamento para uso em [!DNL Profile], o namespace do campo de origem e o namespace primário do campo de destino devem ser os mesmos. Essa mensagem de erro é exibida ao tentar ativar um esquema que contém um namespace sem correspondência para seu descritor de identidade de referência. Certifique-se de que o valor `xdm:namespace` do campo de identidade do schema de destino corresponda ao da propriedade `xdm:identityNamespace` no descritor de identidade de referência do campo de origem para resolver esse problema.

Para obter uma lista de códigos de namespace de identidade compatíveis, consulte a seção em [namespaces padrão](../identity-service/namespaces.md) na visão geral do namespace de identidade.

### Aceitar erros de cabeçalho

A maioria das solicitações do GET na API [!DNL Schema Registry] requer um cabeçalho Accept para que o sistema determine como formatar a resposta. Veja a seguir uma lista de erros comuns associados ao cabeçalho Accept . Para obter listas de cabeçalhos Accept compatíveis para solicitações de API diferentes, consulte as seções correspondentes no [Guia do desenvolvedor do Registro de Schema](api/getting-started.md).

#### É necessário aceitar o parâmetro do cabeçalho

```json
{
    "type": "/placeholder/type/uri",
    "status": 406,
    "title": "NotAcceptableError",
    "detail": "Accept header parameter is required"
}
```

Essa mensagem de erro é exibida quando um cabeçalho Accept está ausente de uma solicitação de API. Certifique-se de que um cabeçalho Accept esteja incluído antes de tentar novamente.

#### Mídia de Aceitação Desconhecida fornecida

```json
{
    "type": "/placeholder/type/uri",
    "status": 406,
    "title": "NotAcceptableError",
    "detail": "Unknown Accept media supplied: xed+json"
}
```

Esta mensagem de erro é exibida quando um cabeçalho Accept é inválido. Certifique-se de ter inserido corretamente um cabeçalho Accept compatível com a solicitação da API que você está tentando fazer antes de tentar novamente.

#### Formato Accept Desconhecido disponível

```json
{
    "type": "/placeholder/type/uri",
    "status": 406,
    "title": "NotAcceptableError",
    "detail": "Unknown Accept format available "
}
```

Essa mensagem de erro é exibida quando o cabeçalho Accept é fornecido incorretamente ao procurar um descritor. Certifique-se de ter inserido corretamente um dos [cabeçalhos Accept suportados para descritores](./api/descriptors.md) antes de tentar novamente.

#### A versão deve ser fornecida no cabeçalho Accept

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "version must be supplied in the accept header. Example: 
      application/vnd.adobe.xed-full-notext+json; version=1"
}
```

Essa mensagem de erro é exibida quando um número de versão não foi incluído no cabeçalho Accept (Aceitar). Determinados elementos, como schemas, exigem uma versão para ser especificada ao pesquisar instâncias individuais. Um cabeçalho Accept contendo um número de versão será semelhante ao seguinte:

```plaintext
application/vnd.adobe.xed+json; version=1
```

Para obter uma lista de cabeçalhos Accept suportados, consulte a seção [Accept header](api/getting-started.md#accept) no guia do desenvolvedor [!DNL Schema Registry].

#### A versão não deve ser fornecida no cabeçalho Accept

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "version must not be supplied in the accept header. Example: 
      application/vnd.adobe.xed-full+json"
}
```

Se tentar incluir uma versão no cabeçalho Aceitar ao listar (GET) recursos, você receberá esse erro. As versões são necessárias somente ao tentar uma solicitação de pesquisa em um único recurso. Remova a versão do cabeçalho Accept para resolver o erro.
