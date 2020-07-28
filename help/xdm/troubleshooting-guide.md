---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guia de solução de problemas do sistema do Experience Data Model (XDM)
topic: troubleshooting
translation-type: tm+mt
source-git-commit: d04bf35e49488ab7d5e07de91eb77d0d9921b6fa
workflow-type: tm+mt
source-wordcount: '1826'
ht-degree: 0%

---


# [!DNL Experience Data Model] (XDM) Guia de solução de problemas do sistema

Este documento fornece respostas para perguntas frequentes sobre o sistema [!DNL Experience Data Model] (XDM), bem como um guia de solução de problemas para erros comuns. Para questões e solução de problemas relacionados a outros serviços no Adobe Experience Platform, consulte o guia [de solução de problemas do](../landing/troubleshooting.md)Experience Platform.

**[!DNL Experience Data Model](XDM)**é uma especificação de código aberto que define schemas padronizados para o gerenciamento da experiência do cliente. A metodologia na qual[!DNL Experience Platform]está construído, o Sistema****XDM, opera[!DNL Experience Data Model]schemas para uso pelos[!DNL Platform]serviços. O **[!DNL Schema Registry]**fornece uma interface de usuário e uma RESTful API para acessar o **[!DNL Schema Library]**dentro[!DNL Experience Platform]. See the[XDM documentation](home.md)for more information.

## Perguntas frequentes

Veja a seguir uma lista de respostas para perguntas frequentes sobre o sistema XDM e o uso da [!DNL Schema Registry] API.

### Como faço para adicionar campos a um schema?

É possível adicionar campos a um schema usando uma combinação. Cada mistura é compatível com uma ou mais classes, permitindo que a mistura seja usada em qualquer schema que implemente uma dessas classes compatíveis. Embora o Adobe Experience Platform forneça várias combinações do setor com seus próprios campos predefinidos, você pode adicionar seus próprios campos a um schema criando novas combinações usando a API ou a interface do usuário.

Para obter detalhes sobre como criar novas combinações na API, consulte [criar um documento de combinação](api/create-mixin.md) no guia do desenvolvedor da [!DNL Schema Registry] API. Se você estiver usando a interface do usuário, consulte o tutorial [do Editor de](./tutorials/create-schema-ui.md)Schemas.

### Quais são os melhores usos para misturas e tipos de dados?

[As misturas](./schema/composition.md#mixin) são componentes que definem um ou mais campos em um schema. As misturas impõem como seus campos aparecem na hierarquia do schema e, portanto, exibem a mesma estrutura em cada schema em que estão incluídos. As misturas só são compatíveis com classes específicas, identificadas pelo seu `meta:intendedToExtend` atributo.

[Os tipos](./schema/composition.md#data-type) de dados também podem fornecer um ou mais campos para um schema. No entanto, ao contrário das combinações, os tipos de dados não são restritos a uma classe específica. Isso torna os tipos de dados uma opção mais flexível para descrever estruturas de dados comuns que são reutilizáveis em vários schemas com classes potencialmente diferentes.

### Qual é a ID exclusiva de um schema?

Todos os [!DNL Schema Registry] recursos (schemas, misturas, tipos de dados, classes) têm um URI que atua como uma ID exclusiva para fins de referência e pesquisa. Ao exibir um schema na API, ele pode ser encontrado nos atributos de nível superior `$id` e `meta:altId` .

Para obter mais informações, consulte a seção Identificação [do](api/getting-started.md#schema-identification) schema no guia do desenvolvedor da [!DNL Schema Registry] API.

### Quando um start de schema impede a quebra de alterações?

Alterações de quebra podem ser feitas em um schema, desde que nunca tenham sido usadas na criação de um conjunto de dados ou estejam habilitadas para uso em [!DNL Real-time Customer Profile](../profile/home.md). Depois que um schema é usado na criação do conjunto de dados ou ativado para uso com [!DNL Real-time Customer Profile], as regras da Evolução [do](schema/composition.md#evolution) Schema se tornam rigorosamente aplicadas pelo sistema.

### Qual é o tamanho máximo de um tipo de campo longo?

Um tipo de campo longo é um número inteiro com um tamanho máximo de 53(+1) bits, dando a ele um intervalo potencial entre -9007199254740992 e 9007199254740992. Isso se deve a uma limitação de como as implementações JavaScript do JSON representam inteiros longos.

Para obter mais informações sobre tipos de campos, consulte a seção [Definição de tipos](api/appendix.md#field-types) de campos XDM no guia do desenvolvedor da [!DNL Schema Registry] API.

### Como definir identidades para o meu schema?

Em [!DNL Experience Platform]geral, as identidades são usadas para identificar um indivíduo (normalmente uma pessoa individual) independentemente das fontes de dados que estão sendo interpretadas. São definidos em schemas marcando os campos de chave como &quot;Identidade&quot;. Os campos usados frequentemente para identificação incluem endereço de email, número de telefone, [!DNL Experience Cloud ID (ECID)](https://docs.adobe.com/content/help/pt-BR/id-service/using/home.html)ID de CRM e outros campos de ID exclusivos.

Os campos podem ser marcados como identidades usando a API ou a interface do usuário.

#### Definição de identidades na API

Na API, as identidades são estabelecidas pela criação de descritores de identidade. Os descritores de identidade sinalizam que uma propriedade específica de um schema é um identificador exclusivo.

Os descritores de identidade são criados por uma solicitação de POST para o terminal /descriptors. Se bem-sucedido, você receberá um Status HTTP 201 (Criado) e um objeto de resposta contendo os detalhes do novo descritor.

Para obter mais detalhes sobre como criar descritores de identidade na API, consulte a seção documento sobre [descritores](api/descriptors.md) no guia do [!DNL Schema Registry] desenvolvedor.

#### Definição de identidades na interface do usuário

Com o schema aberto no Editor de Schemas, clique no campo na seção **[!UICONTROL Estrutura]** do editor que você deseja marcar como uma identidade. Em Propriedades **[!UICONTROL do]** campo, no lado direito, clique na caixa de seleção **[!UICONTROL Identidade]** .

Para obter mais detalhes sobre como gerenciar identidades na interface do usuário, consulte a seção sobre [definição de campos](./tutorials/create-schema-ui.md#identity-field) de identidade no tutorial do Editor de Schemas.

### Meu schema precisa de uma identidade primária?

As identidades primárias são opcionais, já que os schemas podem ter 0 ou 1 delas. No entanto, um schema deve ter uma identidade primária para que o schema seja habilitado para uso no [!DNL Real-time Customer Profile]. Consulte a seção de [identidade](./tutorials/create-schema-ui.md#identity-field) do tutorial do Editor de Schemas para obter mais informações.

### Como ativar um schema para uso em [!DNL Real-time Customer Profile]?

Os Schemas são ativados para uso [!DNL Real-time Customer Profile](../profile/home.md) por meio da adição de uma tag &quot;união&quot;, localizada no `meta:immutableTags` atributo do schema. A habilitação de um schema para uso com [!DNL Profile] pode ser feita usando a API ou a interface do usuário.

#### Habilitar um schema existente para [!DNL Profile] usar a API

Faça uma solicitação de PATCH para atualizar o schema e adicione o `meta:immutableTags` atributo como uma matriz que contém o valor &quot;união&quot;. Se a atualização for bem-sucedida, a resposta mostrará o schema atualizado que agora contém a tag de união.

Para obter mais informações sobre como usar a API para ativar um schema para uso em [!DNL Real-time Customer Profile], consulte o documento [união](./api/unions.md) do guia do [!DNL Schema Registry] desenvolvedor.

#### Habilitar um schema existente para [!DNL Profile] usar a interface do usuário

Em [!DNL Experience Platform], clique em **[!UICONTROL Schemas]** na navegação à esquerda e selecione o nome do schema que deseja ativar na lista de schemas. Em seguida, no lado direito do editor, em Propriedades **[!UICONTROL do]** Schema, clique no **[!UICONTROL Perfil]** para ativá-lo.


Para obter mais informações, consulte a seção sobre [uso em Perfil](./tutorials/create-schema-ui.md#profile) de cliente em tempo real no tutorial do Editor [!UICONTROL de] Schemas.

### Posso editar uma schema de união diretamente?

schemas de União são somente leitura e são gerados automaticamente pelo sistema. Eles não podem ser editados diretamente. schemas de União são criados para uma classe específica quando uma tag &quot;união&quot; é adicionada ao schema que implementa essa classe.

Para obter mais informações sobre o união no XDM, consulte a seção [união](./api/unions.md) no guia do desenvolvedor da [!DNL Schema Registry] API.

### Como devo formatar meu arquivo de dados para assimilar dados em meu schema?

[!DNL Experience Platform] aceita arquivos de dados no formato JSON [!DNL Parquet] ou JSON. O conteúdo desses arquivos deve estar em conformidade com o schema referenciado pelo conjunto de dados. Para obter detalhes sobre as práticas recomendadas para a ingestão de arquivos de dados, consulte a visão geral [da ingestão de](../ingestion/home.md)lote.

## Erros e solução de problemas

A seguir está uma lista de mensagens de erro que podem ser encontradas ao trabalhar com a [!DNL Schema Registry] API.

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

Este erro é exibido quando o sistema não conseguiu localizar um recurso específico. O recurso pode ter sido excluído ou o caminho na chamada da API é inválido. Verifique se você inseriu um caminho válido para sua chamada de API antes de tentar novamente. Você pode verificar se digitou a ID correta para o recurso e se o caminho foi nomeado corretamente com o container apropriado (global ou locatário).

Para obter mais informações sobre como construir caminhos de pesquisa na API, consulte as seções de identificação [de](./api/getting-started.md#container) container [e](api/getting-started.md#schema-identification) schemas no guia do [!DNL Schema Registry] desenvolvedor.

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

Esta mensagem de erro é exibida quando você tenta criar um recurso com um título que já está sendo usado por outro recurso. Os títulos devem ser exclusivos em todos os tipos de recursos. Por exemplo, se você tentar criar uma combinação com um título que já está sendo usado por um schema, você receberá esse erro.

### Campos personalizados devem usar um campo de nível superior

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "For custom fields, you must use a top level field named _{TENANT_ID}
       and all the other fields must be defined under it"
}
```

Esta mensagem de erro é exibida quando você tenta criar uma nova combinação com campos com nomes inadequados. As misturas que são definidas pela organização do IMS devem namespace seus campos a um `TENANT_ID` para evitar conflitos com outros recursos do setor e do fornecedor. Exemplos detalhados de estruturas de dados adequadas para misturas podem ser encontrados no documento sobre a [criação de uma seção de mixin](api/create-mixin.md) no guia do desenvolvedor da [!DNL Schema Registry] API.


### [!DNL Real-time Customer Profile] erros

As mensagens de erro a seguir estão associadas a operações envolvidas na ativação de schemas para [!DNL Real-time Customer Profile]. Consulte a seção [união](./api/unions.md) no guia do desenvolvedor da [!DNL Schema Registry] API para obter mais informações.

#### Para habilitar conjuntos de dados de perfil, o schema deve ser válido

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "To enable profile datasets the schema should be valid"
}
```

Esta mensagem de erro é exibida quando você tenta habilitar um conjunto de dados de perfil para um schema que não foi habilitado para [!DNL Real-time Customer Profile]. Verifique se o schema contém uma tag de união antes de habilitar o conjunto de dados.

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

Esta mensagem de erro é exibida quando você tenta ativar um schema para [!DNL Profile] e uma de suas propriedades contém um descritor de relação sem um descritor de identidade de referência. Adicione um descritor de identidade de referência ao campo de schema em questão para resolver esse erro.

#### As namespaces do campo do descritor de identidade de referência e do schema de destino devem corresponder

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

Para habilitar schemas que contêm descritores de relacionamento para uso em [!DNL Profile], a namespace do campo de origem e a namespace primária do campo público alvo devem ser as mesmas. Esta mensagem de erro é exibida quando você tenta ativar um schema que contém uma namespace não correspondente para seu descritor de identidade de referência. Verifique se o `xdm:namespace` `xdm:identityNamespace` valor do campo de identidade do schema de destino corresponde ao da propriedade no descritor de identidade de referência do campo de origem para resolver esse problema.

Para obter uma lista de códigos de namespace de identidade suportados, consulte a seção sobre namespaces [](../identity-service/namespaces.md) padrão na visão geral da namespace de identidade.

### Aceitar erros de cabeçalho

A maioria das solicitações de GET na [!DNL Schema Registry] API requer um cabeçalho Accept (Aceitar) para que o sistema determine como formatar a resposta. A seguir está uma lista de erros comuns associados ao cabeçalho Accept (Aceitar). Para obter listas de cabeçalhos Accept compatíveis para solicitações de API diferentes, consulte as seções correspondentes no guia [do desenvolvedor do Registro do](api/getting-started.md)Schema.

#### Aceitar parâmetro de cabeçalho é obrigatório

```json
{
    "type": "/placeholder/type/uri",
    "status": 406,
    "title": "NotAcceptableError",
    "detail": "Accept header parameter is required"
}
```

Esta mensagem de erro é exibida quando um cabeçalho Accept está ausente de uma solicitação de API. Certifique-se de que um cabeçalho Accept esteja incluído antes de tentar novamente.

#### Mídia de aceitação desconhecida fornecida

```json
{
    "type": "/placeholder/type/uri",
    "status": 406,
    "title": "NotAcceptableError",
    "detail": "Unknown Accept media supplied: xed+json"
}
```

Esta mensagem de erro é exibida quando um cabeçalho Accept é inválido. Verifique se você inseriu corretamente um cabeçalho Accept compatível com a solicitação de API que você está tentando fazer antes de tentar novamente.

#### Formato de Aceitação Desconhecido disponível

```json
{
    "type": "/placeholder/type/uri",
    "status": 406,
    "title": "NotAcceptableError",
    "detail": "Unknown Accept format available "
}
```

Esta mensagem de erro é exibida quando o cabeçalho Accept (Aceitar) é fornecido incorretamente ao procurar um descritor. Verifique se você inseriu corretamente um dos cabeçalhos Aceitar [suportados para descritores](./api/descriptors.md) antes de tentar novamente.

#### A versão deve ser fornecida no cabeçalho Aceitar

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "version must be supplied in the accept header. Example: 
      application/vnd.adobe.xed-full-notext+json; version=1"
}
```

Esta mensagem de erro é exibida quando um número de versão não foi incluído no cabeçalho Aceitar. Determinados elementos, como schemas, exigem que uma versão seja especificada ao pesquisar instâncias individuais. Um cabeçalho Accept contendo um número de versão será semelhante ao seguinte:

```plaintext
application/vnd.adobe.xed+json; version=1
```

Para obter uma lista dos cabeçalhos Aceitar suportados, consulte a seção [Aceitar cabeçalho](api/getting-started.md#accept) no guia do [!DNL Schema Registry] desenvolvedor.

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

Se você tentar incluir uma versão no cabeçalho Aceitar ao listar os recursos (GET), você receberá esse erro. As versões são necessárias somente ao tentar uma solicitação de pesquisa em um único recurso. Remova a versão do cabeçalho Accept (Aceitar) para resolver o erro.