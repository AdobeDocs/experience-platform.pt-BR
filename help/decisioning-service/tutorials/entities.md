---
keywords: Experience Platform;home;popular topics;manage decisioning;decisioning objects api;manage decisioning objects
solution: Experience Platform
title: Gerenciar entidades do serviço de decisão usando APIs
topic: tutorial
description: 'Este documento fornece um tutorial para trabalhar com as entidades de negócios do Serviço de tomada de decisão usando APIs da Adobe Experience Platform. '
translation-type: tm+mt
source-git-commit: f4a4e65a087313dc4e2414f999e021e3f6e17137
workflow-type: tm+mt
source-wordcount: '7239'
ht-degree: 0%

---


# Gerenciar objetos e regras de decisão usando APIs

Este documento fornece um tutorial para trabalhar com as entidades de negócios do [!DNL Decisioning Service] uso de APIs da Adobe Experience Platform.

O tutorial tem duas partes:

- As APIs de repositório genéricas para gerenciar objetos de negócios são introduzidas na [primeira parte](#managing-repository-entities-using-apis). Essas APIs são genéricas no sentido de que fornecem recursos de criação, leitura, atualização, exclusão e pesquisa para **qualquer** tipo de objetos de negócios. O modelo de API geral é descrito e a relação com a HAL (Hypertext Application Language) é explicada.

- Aplicando o conhecimento sobre as APIs do repositório, a [segunda parte](#creating-and-managing-offer-decisioning-entities-using-apis) se concentra nas entidades de negócios que são gerenciadas por meio das APIs do repositório. Com as mesmas APIs aplicadas, a única diferença entre o gerenciamento de duas entidades diferentes, como uma atividade e uma regra de negócios, é a carga de solicitação e resposta, além dos valores de cabeçalho necessários que indicam o tipo de objeto gerenciado.

## Introdução

Este tutorial requer uma compreensão funcional dos [!DNL Experience Platform] serviços e das convenções da API. O [!DNL Platform] repositório é um serviço usado por vários outros [!DNL Platform] serviços para armazenar objetos de negócios e vários tipos de metadados. Ele oferece uma maneira segura e flexível de gerenciar e query desses objetos para uso por vários serviços de tempo de execução. O [!DNL Decisioning Service] é um desses. Antes de iniciar este tutorial, reveja a documentação do seguinte:

- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): A estrutura padronizada pela qual a Plataforma organiza os dados de experiência do cliente.
- [[!Serviço de Decisão DNL]](./../home.md): Explica os conceitos e componentes utilizados para a Decisão de Experiência em geral e para a decisão Oferta em particular. Ilustra as estratégias usadas para escolher a melhor opção para apresentar durante a experiência de um cliente.
- [[!Linguagem de Query de Perfil DNL (PQL)](../../segmentation/pql/overview.md): O PQL é um idioma avançado para gravar expressões em instâncias do XDM. O PQL é usado para definir regras de decisão.

As seções a seguir fornecem informações adicionais que você precisará saber para fazer chamadas bem-sucedidas para as [!DNL Platform] APIs.

### Lendo chamadas de exemplo da API

Este tutorial fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de amostra retornado em respostas de API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de amostra, consulte a seção sobre [como ler chamadas](../../landing/troubleshooting.md#how-do-i-format-an-api-request) de API de exemplo no guia de [!DNL Experience Platform] solução de problemas.

### Reunir valores para cabeçalhos necessários

Para fazer chamadas para [!DNL Platform] APIs, você deve primeiro concluir o tutorial [de](../../tutorials/authentication.md)autenticação. A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de [!DNL Experience Platform] API, como mostrado abaixo:

- Autorização: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Todos os recursos em [!DNL Experience Platform] são isolados para caixas de proteção virtuais específicas. Todas as solicitações para [!DNL Platform] APIs exigem um cabeçalho que especifique o nome da caixa de proteção em que a operação ocorrerá:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre caixas de proteção em [!DNL Platform], consulte a documentação [de visão geral da](../../sandboxes/home.md)caixa de proteção.

Todas as solicitações que contêm uma carga (POST, PUT, PATCH) exigem um cabeçalho adicional:

- Tipo de conteúdo: application/json

## Convenções da API do repositório

[!DNL Decisioning Service] é controlada por vários objetos de negócios relacionados entre si. Todos os objetos de negócios são armazenados no Repositório de objetos de negócios. [!DNL Platform’s] Um recurso importante desse repositório é que as APIs são ortogonais em relação ao tipo de objeto de negócios. Em vez de usar uma API POST, GET, PUT, PATCH ou DELETE que indica o tipo de recurso em seu endpoint de API, há apenas 6 endpoints genéricos, mas eles aceitam ou retornam um parâmetro que indica o tipo de objeto quando essa indicação é necessária. O schema deve ser registrado no repositório, mas além disso o repositório pode ser usado para um conjunto ilimitado de tipos de objetos.

Além dos cabeçalhos listados acima, as APIs para criar, ler, atualizar, excluir e query objetos do repositório têm as seguintes convenções:

- Os caminhos de ponto de extremidade para todas as APIs do repositório com `https://platform.adobe.io/data/core/xcore/`.

Os formatos de carga da API são negociados com um cabeçalho `Accept` ou `Content-Type` . Os formatos de mensagem no cabeçalho `Accept` ou `Content-Type` são indicados por um valor `application/vnd.adobe.platform.xcore.{FORMAT}+json` em que {FORMAT} depende da solicitação de API ou da mensagem de resposta do repositório específico, de acordo com a tabela a seguir.

| Variante FORMAT | Descrição da entidade de solicitação ou resposta |
| --- | --- |
| seguido<br>por um parâmetro `schema={schemaId}` | A mensagem contém uma instância descrita por um Schema JSON que é indicada pelo schema de parâmetro format. A instância está envolvida em uma propriedade JSON `_instance`. As outras propriedades de nível superior na carga da resposta especificam informações do repositório que estão disponíveis para todos os recursos.  As mensagens que estão em conformidade com o formato HAL têm uma `_links` propriedade que contém referências no formato HAL. |
| `patch.hal` | A mensagem contém uma carga de PATCH JSON com o pressuposto de que a instância a ser corrigida é compatível com HAL. Isso significa que não apenas as próprias propriedades de instância da instância, mas também os links HAL da instância podem ser corrigidos. Observe que existem restrições sobre quais propriedades podem ser atualizadas pelo cliente. |
| `home.hal` | A mensagem contém uma representação formatada JSON de um recurso de documento inicial para o repositório. |
| xdm.receipt | A mensagem contém uma resposta formatada JSON para uma operação de criação, atualização (completa e correção) ou exclusão. Os recibos contêm dados de controle que indicam a revisão da instância na forma de um ETag. |

O uso de cada variante **de** formato depende da API específica:

| API | Cabeçalho Content-Type | Aceitar cabeçalho |
| --- | --- | --- |
| Criar Container de <br/>Criação de Instância | `hal`<br/>com parâmetro schema | `xdm.receipt` |
| Atualizar Container<br/>InstanceUpdate | `hal`<br/>com parâmetro schema | `xdm.receipt` |
| Instância do patch | `patch.hal` | `xdm.receipt` |
| Excluir container<br/>instanceDelete | N/D | `xdm.receipt` |
| Ler Container<br/>InstanceRead | N/D | `hal` com `schema` parâmetro |
| Lista<br/>instanceList container | N/D | `hal` com um `schema` parâmetro especial `https://ns.adobe.com/experience/xcore/hal/results` |
| Instâncias de pesquisa | N/D | hal com parâmetro especial `schema` `https://ns.adobe.com/experience/xcore/hal/results` |
| Ler raiz do repo | N/D | `home.hal` |

Para criar, atualizar e ler APIs do container, o schema de parâmetro format tem o valor `https://ns.adobe.com/experience/xcore/container`.

`ContainerId` é o primeiro parâmetro de caminho para as APIs de instância. Todas as entidades de negócios residem no que é chamado de container. Um container é um mecanismo de isolamento para manter diferentes preocupações separadas. O primeiro elemento de caminho para as APIs de instância do repositório após o terminal geral é o `containerId`. O identificador é obtido da lista de container acessíveis ao chamador. Por exemplo, a API para criar uma instância em um container é `POST https://platform.adobe.io/data/core/xcore/{containerId}/instances`.

A lista de container acessíveis é obtida chamando o terminal raiz do repositório &quot;/&quot; com uma solicitação de GET HTTP usando os cabeçalhos padrão.

## Gerenciamento do acesso a container

Um administrador pode agrupar principais, recursos e permissões de acesso semelhantes em perfis. Isso reduz a carga de gerenciamento e é compatível com a interface do usuário [Admin Console do](https://adminconsole.adobe.com)Adobe. Você deve ser um administrador de produto da Adobe Experience Platform em sua organização para criar perfis e atribuir usuários a eles.

É suficiente criar perfis de produtos que correspondam a determinadas permissões em uma única etapa e simplesmente adicionar usuários a esses perfis. Os perfis atuam como grupos aos quais foram concedidas permissões e cada usuário real ou técnico do grupo herda essas permissões.

### Container de lista acessíveis aos usuários e integrações

Quando o administrador conceder acesso a container para usuários regulares ou integrações, esses container aparecerão na lista chamada &quot;Início&quot; do repositório. A lista pode ser diferente para usuários ou integrações diferentes, pois é um subconjunto de todos os container acessíveis ao chamador. A lista de container pode ser filtrada pela associação a contextos de produtos. O parâmetro de filtro é chamado `product` e pode ser repetido. Se mais de um filtro de contexto do produto for fornecido, a união dos container que têm associações com qualquer um dos contextos do produto será retornada. Observe que um único container pode ser associado a vários contextos de produtos.

O contexto dos [!DNL Platform] container está atualmente [!DNL Decisioning Service] definido `dma_offers`.

>[!NOTE]
>
>O contexto para [!DNL Platform Decisioning Containers] está prestes a mudar para `acp`. A filtragem é opcional, mas os filtros somente `dma_offers` exigirão edições em uma versão futura. Para se preparar para essa alteração, os clientes não devem usar filtros ou aplicar ambos os contextos de produto como filtro.

**Solicitação**

```shell
curl -X GET {ENDPOINT_PATH}/?product=dma_offers&product=acp \ 
  -H 'Accept: application/vnd.adobe.platform.xcore.home.hal+json' \ 
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}' 
```

**Resposta**

```json
{ 
    "_embedded": { 
        "https://ns.adobe.com/experience/xcore/container": [ 
            { 
              "instanceId": "82d1f250-85b6-11e9-ac80-99ba4655b277", 
              "schemas": [ 
                "https://ns.adobe.com/experience/xcore/container;version=0.1" 
              ], 
              "productContexts": [ 
                "dma_offers" 
              ], 
              "repo:etag": 1, 
              "repo:createdDate": "2019-06-03T04:17:33.684Z", 
              "repo:lastModifiedDate": "2019-06-03T04:17:33.684Z", 
              "repo:createdBy": "CREATOR_ACCOUNT_ID", 
              "repo:lastModifiedBy": "LAST_UPDATE_ACCOUNT_ID", 
              "repo:createdByClientId": "CLIENT_ID_OR_API_KEY", 
              "repo:lastModifiedByClientId": "CLIENT_ID_OR_API_KEY", 
              "_instance": { 
                "repo:name": "My Organization's container", 
                "dataCenter": "VA7" 
              }, 
              "_links": { 
                "self": { 
                  "href": "/containers/82d1f250-85b6-11e9-ac80-99ba4655b277" 
                } 
              } 
            } 
        ] 
    }, 
    "_links": { 
        "self": { 
            "href": "/"  
        } 
    } 
}  
```

Observe os itens `instanceId` listados nos resultados. É usado como o `containerId` parâmetro nas APIs para ler e manipular objetos comerciais comuns.

A lista já está filtrada para os usuários por seus privilégios de acesso, mas pode ser filtrada ainda mais por um query de propriedade.

## APIs genéricas para gerenciar entidades

### Criar instâncias

A API para criar uma nova instância no repositório usa um parâmetro de `containerId` caminho e identifica o tipo da instância no cabeçalho com o parâmetro de schema `Content-Type` .

As propriedades da instância são fornecidas na carga encapsulada na `_instance` propriedade. As propriedades da instância devem ser válidas em relação ao schema JSON com o identificador de schema especificado.

A `_links` propriedade HAL deve estar presente, mas pode estar vazia. Isso significa que não há links personalizados definidos para essa instância.

**Solicitação**

```shell
curl -X POST {ENDPOINT_PATH}/{CONTAINER_ID}/instances \ 
  -H 'Content-Type: application/vnd.adobe.platform.xcore.hal+json; schema="{SCHEMA_ID}"' \  
  -H 'Accept: application/vnd.adobe.platform.xcore.xdm.receipt+json \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}' \ 
  -d '{ 
    "_instance": { 
        {JSON_PAYLOAD} 
    }, 
    "_links": { 
    } 
}' 
```

**Resposta**

```json
{ 
  "instanceId": "3684ceb0-8744-11e9-a989-89f60b24f6cc", 
  "@id": "GENERATED_URI", 
  "repo:etag": 1, 
  "repo:createdDate": "2019-06-05T03:44:25.343Z", 
  "repo:lastModifiedDate": "2019-06-05T03:44:25.343Z", 
  "repo:createdBy": "YOUR_TECHNICAL_ACCOUNT_ID", 
  "repo:lastModifiedBy": "YOUR_TECHNICAL_ACCOUNT_ID", 
  "repo:createdByClientId": "YOUR_API_KEY", 
  "repo:lastModifiedByClientId": "YOUR_API_KEY" 
}
```

A resposta contém a instanceId do objeto que acabou de ser criado. Essa instanceId é imutável, sempre atribuída pelo repositório e globalmente exclusiva. O valor serve como um identificador físico.

Além disso, um URI (identificador de recurso universal) é retornado na `@id` propriedade da carga de resposta se o schema tiver essa propriedade. Cada instância deve ter uma propriedade que serve como URI e a chave primária da instância. Esse identificador é usado por outra instância para formar relações com a nova instância, incluindo tipos diferentes. Na versão atual, os URIs são gerados pelo repositório e estão contidos na `@id` propriedade. Versões futuras podem relaxar essa regra e permitir que os clientes gerenciem seus próprios valores de URI e nomeiem a propriedade que a contém.

Observe que esses URIs não são URLs e não fornecem uma maneira de recuperar diretamente o recurso. Para indicar esse aspecto, o URI recebe o prefixo de um esquema URI que não especifica um protocolo de recuperação. No entanto, os URIs podem ser usados para pesquisar a instância com um query.

A resposta REST terá um cabeçalho Location que contém um componente de URL que pode ser usado para recuperar a instância recém-criada. Este componente é uma Referência de URI relativa e precisa ser aplicado ao URI básico do repositório. O URI de base é retornado no `Content-Base` cabeçalho.

A `repo:etag` propriedade especifica a revisão da instância. Esse valor pode ser usado em operações de atualização para reforçar a consistência. O cabeçalho HTTP `If-Match` pode ser usado para adicionar uma condição a uma chamada de API PUT ou PATCH que garanta que não houve outra alteração na instância que possa ser substituída acidentalmente. O `repo:etag` valor é retornado com cada chamada de criação, leitura, atualização, exclusão e query. O valor é usado como o valor no ` If-Match` cabeçalho, de acordo com a seção 3.1 [do](https://tools.ietf.org/html/rfc7232#section-3.1)RFC7232.

As propriedades restantes indicam qual conta e chave de API foram usadas para criar e modificar a instância pela última vez. Como a instância foi criada por essa chamada, os respectivos valores são os da solicitação.

### Pesquisar uma instância por ID

Usando o URL no cabeçalho Location retornado com a chamada Create, um aplicativo pode procurar uma instância.

**Solicitação**

```shell
curl -X GET {ENDPOINT_PATH}/{CONTAINER_ID}/instances/{INSTANCE_ID} \ 
  -H 'Accept: *, application/vnd.adobe.platform.xcore.hal+json; schema="{SCHEMA_ID}" \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}'  
```

>[!NOTE]
>
>Embora `instanceId` seja fornecido como um parâmetro de caminho, os aplicativos não devem, sempre que possível, construir o caminho em si e, em vez disso, seguir links para instâncias contidas em operações de lista e pesquisa. Ver seções ‎ 6.4.4 e ‎ 6.4.6 para mais pormenores.

**Resposta**

```json
{ 
  "instanceId": "ID_OF_THIS_INSTANCE", 
  "schemas": [ 
    "SCHEMA_ID_OF_INSTANCE" 
  ], 
  "repo:etag": 1, 
  "repo:createdDate": "2019-03-24T15:52:12.725Z", 
  "repo:lastModifiedDate": "2019-03-24T15:52:12.725Z", 
  "repo:createdBy": "CREATOR_ACCOUNT_ID", 
  "repo:lastModifiedBy": "LAST_UPDATE_ACCOUNT_ID", 
  "_instance": { 
    JSON_PROPERTIES_OF_THIS_INSTANCE 
  }, 
  "_links": { 
    "self": { 
      "name": "GENERATED_UNIQUE_LINK_NAME", 
      "href": "RELATIVE_URL_TO_INSTANCE" 
    } 
  } 
} 
```

As propriedades JSON da instância são vinculadas na `_instance` propriedade e as outras propriedades de nível raiz contêm metadados sobre a instância.

O recurso também contém uma matriz de IDs de schema JSON. Essa matriz indica os schemas JSON com os quais essa instância é validada.

Cada instância contém um link HAL do tipo de relação auto que corresponde à autorelação registrada do IANA (conforme definido pelo [RFC5988]).

**Testar revisões mais recentes de uma instância**

O `eTag` valor atual da instância é retornado com a resposta, ela permite que os clientes emitam operações condicionais contra a instância, para evitar recuperar o mesmo estado de recurso novamente ou para evitar substituir os valores de uma revisão posterior sem o conhecimento do cliente.

A API de pesquisa permite que um cliente especifique um parâmetro de `If-None-Match` cabeçalho. Consulte a definição deste parâmetro HTTP padrão [RFC2616]. O valor da tag da entidade especificado por um cliente é o valor recebido com a resposta mais recente de uma chamada de API de atualização, leitura, lista ou pesquisa. Observe que o `etag` valor deve ser opaco para o cliente e deve ser fornecido como uma string, entre aspas.

**Solicitação**

```shell
curl -X GET {ENDPOINT_PATH}/{CONTAINER_ID}/instances/{INSTANCE_ID} \ 
  -H 'Accept: *, application/vnd.adobe.platform.xcore.hal+json; schema="{SCHEMA_ID}" \ 
  -H 'If-None-Match: "{LAST_RECEIVED_ETAG}" \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}'  
```

A API do repositório responderá com um status 304 Not Momodified (Não modificado) quando a última revisão da instância for aquela com a tag fornecida.

### Instâncias de lista para um schema - Classificação e paginação

Os clientes não poderão rastrear as instâncias que estão criando e, portanto, acessá-las por meio de sua instanceId física. O uso da API de instância de leitura será a exceção. Os clientes também não sabem quais instâncias outros clientes criaram.

Um padrão de acesso mais comum será a página por meio do conjunto de todas as instâncias.

**Solicitação**

```shell
curl -X GET {ENDPOINT_PATH}/{CONTAINER_ID}/instances?schema="{SCHEMA_ID}" \ 
  -H 'Accept: *, application/vnd.adobe.platform.xcore.hal+json; schema="https://ns.adobe.com/experience/xcore/hal/results" \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}'  
```

**Resposta**

A resposta depende do `{schemaId}` especificado. Por exemplo, para &quot;https<span></span>://ns.adobe.com/experience/oferta-management/oferta-atividade&amp;id=xcore:oferta-atividade:fa24f9e8fc15c73&quot;, a resposta se assemelha ao seguinte.

```json
{
"requestTime": "2019-06-28T06:54:05.606Z",
"_embedded": {
  "results": [],
  "total": 0,
  "count": 0
  },
  "_links": {
  "self": {
  "href": "/653da250-71b8-11e9-a3fe-9b1d0913f3ed/instances?schema=https://ns.adobe.com/experience/offer-management/offer-activity&id=xcore:offer-activity:fa24f9e8fc15c73",
"@type": "https://ns.adobe.com/experience/xcore/hal/results"
  }
  },
  "containerId": "653da250-71b8-11e9-a3fe-9b1d0913f3ed",
  "schemaNs": "https://ns.adobe.com/experience/offer-management/offer-activity;version=0.1"
}
```

>[!NOTE]
>
>O resultado contém as instâncias para o schema em questão ou a primeira página dessa lista. Observe que as instâncias podem estar em conformidade com mais de um schema e, portanto, podem aparecer em mais de uma lista.

Os recursos da página são transitórios e são somente leitura; eles não podem ser atualizados ou excluídos. O modelo de paginação fornece acesso aleatório a subconjuntos de listas grandes durante um longo período de tempo sem manter nenhum estado por cliente.

Para acessar uma lista de instância por página dessa maneira, deve ser possível definir uma classificação estável em relação às entradas enumeradas pela lista de instância. Observe que &quot;estável&quot; não significa que as instâncias aparecerão em uma página predeterminada. Na verdade, quando um pedido de página é formado pela classificação de instâncias de acordo com uma propriedade P e um cliente atualiza essa propriedade P, então outro cliente pode acessar essa instância novamente em uma página diferente ao navegar pela lista. Em outras palavras, o modelo favorece o retorno de resultados mais atuais.

No entanto, quando a ordem de classificação é baseada em uma propriedade não modificável, uma ordem de classificação &quot;estável&quot; garante que todas as instâncias que existiam no início da operação de paginação sejam atingidas (a menos que tenham sido excluídas no momento em que a página é atingida). Quando essa ordem de classificação estiver em uma propriedade que aumenta monotonamente, as instâncias criadas após a operação de paginação ser iniciada também serão atingidas.

Um cliente pode fornecer dicas sobre o tamanho de página que desejar, mas é inteiramente ao repositório que cabe fornecer mais ou menos instâncias com a página que retorna. Para garantir a ordem estável, o serviço deve adicionar ou remover itens da página para que o valor da propriedade sort seja diferente entre os limites da página. Dessa forma, a próxima página não conterá alguns itens da última página novamente ou em um pior cenário, ficará presa aos mesmos itens em cada página.

A paginação é controlada pelos seguintes parâmetros:

- **`orderBy`**: Contém uma lista de propriedades separada por vírgulas e ordenada pela qual a lista de instância é classificada. A primeira propriedade é usada para classificação primária, a segunda propriedade para resolver vínculos na classificação primária e assim por diante. Quando uma propriedade que tem um valor exclusivo por instância é especificada, os vínculos não são possíveis e uma quebra de página pode ocorrer após cada item. O nome de uma propriedade pode receber um prefixo com `+` o objetivo de indicar uma ordem crescente ou `-` para indicar uma ordem decrescente por essa propriedade. Se o nome da propriedade não tiver o prefixo, o resultado será classificado em ordem crescente. Se não `orderBy` for especificado na solicitação, o repositório usará a propriedade physical instanceId.
- **`start`**: Os clientes usam o parâmetro start para definir a página que desejam recuperar. O parâmetro start determina o início da página desejada. A resposta conterá instâncias que começam com aquelas que têm um valor de `orderBy` propriedade estritamente maior que (para ascendente) ou estritamente menor que (para descendente) o valor especificado. Quando o parâmetro query não é especificado, ele assume como padrão um valor instanceId que classifica antes do primeiro identificador de instância possível e, portanto, esse valor é omitido da primeira página.
- **`limit`**: especifica um número inteiro positivo como uma dica sobre o número máximo de itens que devem ser retornados para uma determinada solicitação. O tamanho da resposta real pode ser menor ou maior, conforme restringido pela necessidade de fornecer uma operação confiável do parâmetro do start

### Filtrar listas

A filtragem dos resultados da lista é possível e acontece independentemente do mecanismo de paginação. Os filtros simplesmente ignoram as instâncias na ordem do lista ou solicitam explicitamente que incluam apenas as instâncias que satisfazem uma determinada condição. Um cliente pode solicitar que a expressão de propriedade seja usada como filtro ou pode especificar uma lista de URIs a serem usados como valores da chave primária das instâncias.

- **`property`**: Contém um caminho de nome de propriedade seguido por um operador de comparação seguido por um valor. <br/>
A lista de instâncias retornadas contém aquelas para as quais a expressão é avaliada como true. Por exemplo, supondo que a instância tenha uma propriedade payload 
`status` e os valores possíveis são `draft`, `approved`, `archived` e `deleted` o parâmetro do query `property=_instance.status==approved` retorna somente as instâncias para as quais o status é aprovado. <br/>
<br/>
A propriedade a ser comparada com o valor fornecido é identificada como um caminho. Os componentes individuais do caminho são separados por ".", como: '_instance.xdm:prop1.xdm:prop1_1.xdm:prop1_1_1`<br/>

Para propriedades que têm valores de string, numéricos ou de data/hora, os operadores permitidos são: `==`, `!=`, `<`, `<=`, `>` e `>=`. Além disso, para propriedades com um valor de string, um operador `~` pode ser usado. O `~` operador corresponde à propriedade em questão de acordo com uma expressão regular. O valor da string da propriedade deve corresponder à expressão **inteira** para que as entidades sejam incluídas nos resultados filtrados. Por exemplo, procurar a string `cars` em qualquer lugar dentro do valor da propriedade requer que a expressão regular seja `.*cars.*`. Sem a entrelinha ou a direita `.*`, somente as entidades corresponderiam que tinham um valor de propriedade começando ou terminando com `cars`, respectivamente. Para o `~` operador, a comparação de caracteres de letras não diferencia maiúsculas de minúsculas. Para todos os outros operadores, a comparação faz distinção entre maiúsculas e minúsculas.<br/><br/>
Não apenas as propriedades de carga de instância podem ser usadas em expressões de filtro. As propriedades de envelopes são comparadas da mesma maneira, por exemplo, `property=repo:lastModifiedDate>=2019-02-23T16:30:00.000Z`. <br/>
<br/>
O parâmetro `property` query pode ser repetido para que várias condições de filtro sejam aplicadas, por exemplo, para retornar todas as instâncias que foram modificadas pela última vez após uma determinada data e antes de uma determinada data. Os valores nessas expressões devem ser codificados em URL. Se nenhuma expressão for fornecida e o nome da propriedade for listado, os itens que se qualificam são aqueles que têm uma propriedade com o nome especificado.<br/>
<br/>

- **`id`**: Às vezes, uma lista precisa ser filtrada pelo URI das instâncias. O parâmetro `property` query pode ser usado para filtrar uma instância, mas para obter mais de uma instância, uma lista de URIs pode ser fornecida à solicitação. O `id` parâmetro é repetido e cada ocorrência especifica um valor de URI. `id={URI_1}&id={URI_2},…` Os valores de URI devem ser codificados por URL.

Os resultados paginados serão retornados como um tipo MIME especial `application/vnd.adobe.platform.xcore.hal+json; schema="https://ns.adobe.com/experience/xcore/hal/results"`.

**Solicitação**

```shell
curl -X GET {ENDPOINT_PATH}/{CONTAINER_ID}/instances?schema="{SCHEMA_ID}"&orderby${ORDER_BY_PROPERTY_PATH}&property={TIMESTAMP_PROPERTY_PATH}>=2019-02-19T03:19:03.627Z&property${TIMESTAMP_PROPERTY_PATH}<=2019-06-19T03:19:03.627Z \ 
  -H 'Accept: *, application/vnd.adobe.platform.xcore.hal+json; schema="https://ns.adobe.com/experience/xcore/hal/results" \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}'  
```

**Resposta**

```json
{ 
  "requestTime": "2019-06-10T22:12:13.642Z", 
  "_embedded": { 
    "results": [ 
      { 
        "instanceId": "ID_OF_THIS_INSTANCE", 
        "schemas": [ 
          "SCHEMA_ID_OF_INSTANCE" 
        ], 
        "repo:etag": 1, 
        "repo:createdDate": "2019-04-19T03:19:03.627Z", 
        "repo:lastModifiedDate": "2019-04-19T03:19:03.627Z", 
        "repo:createdBy": "CREATOR_ACCOUNT_ID", 
        "repo:lastModifiedBy": "LAST_UPDATE_ACCOUNT_ID", 
        "_instance": { 
          JSON_PROPERTIES_OF_THIS_INSTANCE 
        }, 
        "_links": { 
          "self": { 
            "name": "GENERATED_UNIQUE_LINK_NAME", 
            "href": "RELATIVE_URL_TO_INSTANCE" 
          } 
        } 
      }, 
      { 
        "instanceId": "ID_OF_THIS_INSTANCE", 
        "schemas": [ 
          "SCHEMA_ID_OF_INSTANCE" 
        ], 
        "repo:etag": 1, 
        "repo:createdDate": "2019-04-19T20:30:31.361Z", 
        "repo:lastModifiedDate": "2019-04-19T20:30:31.361Z", 
        "repo:createdBy": "CREATOR_ACCOUNT_ID", 
        "repo:lastModifiedBy": "LAST_UPDATE_ACCOUNT_ID", 
        "_instance": { 
          JSON_PROPERTIES_OF_THIS_INSTANCE 
        }, 

        "_links": { 
          "self": { 
            "name": "GENERATED_UNIQUE_LINK_NAME", 
            "href": "RELATIVE_URL_TO_INSTANCE" 
          } 
        } 
      } 
    ], 
    "total": 2, 
    "count": 2 
  }, 
  "_links": { 
    "self": { 
      "href": "RELATIVE_URL_TO_THIS_RESULT" 
    } 
  }, 
  "containerId": "CONTAINER_ID_OF_THIS_LIST", 
  "schemaNs": "SCHEMA_ID_OF_INSTANCE_LIST" 
} 
```

A resposta contém a lista de itens de resultado dentro dos resultados da propriedade JSON ao lado de duas propriedades que indicam o número de resultados nesta página e o número total de itens na lista filtrada começando com a página que acabou de ser retornada.

### Pesquisa de texto completo e query estruturados

Nos casos em que os clientes desejam fornecer condições de filtro mais complexas e instâncias de pesquisa por termos contidos em propriedades de sequência de caracteres, o repositório oferta uma API de pesquisa mais potente.

**Solicitação**

```shell
curl -X GET {ENDPOINT_PATH}/{CONTAINER_ID}/queries/core/search?schema="{SCHEMA_ID}"&… \ 
  -H 'Accept: *, application/vnd.adobe.platform.xcore.hal+json; schema="https://ns.adobe.com/experience/xcore/hal/results" \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}'  
```

<!-- TODO: needs example response -->

Além dos parâmetros de paginação e filtragem das APIs de lista, essa API permite que os clientes adicionem parâmetros de texto completo e query booleano.

A pesquisa de texto completo é controlada pelos seguintes parâmetros:

- **`q`**: Contém uma lista de termos não ordenados, separada por espaços, que são normalizados antes de serem correspondidos com qualquer propriedade de string das instâncias. As propriedades de string são analisadas para termos e esses termos também são normalizados. O query de pesquisa tenta corresponder a um ou mais dos termos especificados no `q` parâmetro. Os caracteres +, -, =, &amp;&amp;, ||, >, &lt;,!, (,), {, }, [,], ^, &quot;, ~, *, ?, :, / têm um significado especial para determinar os limites de palavras dentro da string de query e devem ser evitados com uma barra invertida ao aparecerem em em um token que deve corresponder ao caractere. A string de query pode ser cercada por aspas de duplo para a correspondência exata da string e para evitar caracteres especiais.
- **`field`**: Se os termos de pesquisa só devem ser comparados com um subconjunto das propriedades, o parâmetro field pode indicar o caminho para essa propriedade. O parâmetro pode ser repetido para indicar mais de uma propriedade que deve ser comparada.
- **`qop`**: Contém um parâmetro de controle usado para modificar o comportamento correspondente da pesquisa. Quando o parâmetro é definido como e todos os termos de pesquisa devem corresponder e quando o parâmetro está ausente ou seu valor é definido como ou então qualquer um dos termos pode contar para uma correspondência.

### Atualização e correção de instâncias

Para atualizar uma instância, um cliente pode substituir a lista completa das propriedades de uma vez ou usar uma solicitação de PATCH JSON para manipular valores de propriedade individuais, incluindo listas.

Em ambos os casos, o URL da solicitação especifica o caminho para a instância física e, em ambos os casos, a resposta será uma carga de recebimento JSON como a retornada da operação [de](#create-instances)criação. De preferência, um cliente deve usar o `Location` cabeçalho ou um link HAL recebido de uma chamada de API anterior para esse objeto como o caminho de URL completo para essa API. Se isso não for possível, o cliente poderá criar o URL a partir do `containerId` e do `instanceId`.

**Solicitação** (PUT)

```shell
curl -X PUT {ENDPOINT_PATH}/{CONTAINER_ID}/instances/{INSTANCE_ID} \ 
  -H 'Content-Type: application/vnd.adobe.platform.xcore.hal+json; schema="{SCHEMA_ID}"' \  
  -H 'Accept: application/vnd.adobe.platform.xcore.xdm.receipt+json \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}'\ 
  -d '{ 
  "_instance": { 
    {JSON_PROPERTIES_OF_THIS_INSTANCE} 
  }, 
  "_links": { 
    {HAL_LINKS_OF_THIS_INSTANCE} 
  } 
}'  
```

**Solicitação** (PATCH)

```shell
curl -X PATCH {ENDPOINT_PATH}/{CONTAINER_ID}/instances/{INSTANCE_ID} \ 
  -H 'Content-Type: application/vnd.adobe.platform.xcore.patch.hal+json; schema="{SCHEMA_ID}"' \  
  -H 'Accept: application/vnd.adobe.platform.xcore.xdm.receipt+json \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}' \ 
  -d '[ 
  { 
    {JSON_PATCH_INSTRUCTIONS_FOR_THIS_INSTANCE} 
  } 
]'
```

A solicitação de PATCH aplica as instruções e valida a entidade resultante em relação ao schema e as mesmas regras de entidade e integridade referencial que a solicitação de PUT.

**Controle de edições de valor de propriedade**

Você pode impedir que as propriedades sejam definidas ao criar e/ou ao atualizar, usando as seguintes anotações:

- **`"meta:usereditable"`**: Booliano - Quando uma solicitação se origina de um agente de usuário que identifica o chamador com um token de acesso de conta técnica ou de usuário, as propriedades com as quais você está anotado não `"meta:usereditable": false` devem estar presentes na carga. Se estiverem, não devem ter um valor diferente daquele que está definido no momento. Se os valores forem diferentes, a solicitação de atualização ou patch será rejeitada com um status 422 Entidade não processável.
- **`"meta:immutable"`**: Booliano - As propriedades anotadas com `"meta:immutable": true` não podem ser alteradas depois de definidas. Isso se aplica a solicitações provenientes de um usuário final, integração de conta técnica ou um serviço especial.

**Teste para atualização simultânea**

Há condições nas quais vários clientes tentam atualizar uma instância simultaneamente. O repositório é operado em um cluster de nós de computação sem gerenciamento central de transações. Para evitar que um cliente escreva uma instância que é escrita simultaneamente por outra, os clientes podem usar uma atualização condicional ou solicitação de patch. Ao especificar a `etag` string no cabeçalho, `If-Match` o repositório garante que somente a primeira solicitação seja bem-sucedida e que as solicitações de continuação por outros clientes que usam o mesmo `etag` valor falhem. O `etag` valor muda a cada modificação da instância. Os clientes devem recuperar a instância para obter o `etag` valor mais recente e, em seguida, somente um cliente de entre muitos que tentam a atualização pode ter êxito com esse valor. Outros clientes serão rejeitados com uma mensagem de conflito 409.

### Excluindo instâncias

As instâncias podem ser excluídas com uma chamada de DELETE. De preferência, um cliente deve usar o `Location` cabeçalho ou um link HAL recebido de uma chamada de API anterior para isso como o caminho de URL completo. Se isso não for possível, o cliente poderá criar o URL a partir do `containerId` e do físico `instanceId`.

**Solicitação**

```shell
curl -X DELETE {ENDPOINT_PATH}/{CONTAINER_ID}/instances/{INSTANCE_ID} \ 
  -H 'Accept: application/vnd.adobe.platform.xcore.xdm.receipt+json \ 
  -H 'x-api-key: {API_KEY}' \ 
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \ 
  -H 'x-request-id: {NEW_UUID}'  
```

**Resposta**

```json
{ 
  "instanceId": "3684ceb0-8744-11e9-a989-89f60b24f6cc", 
  "@id": "INSTANCE_URI", 
  "repo:etag": 1, 
  "repo:createdDate": "2019-06-05T03:44:25.343Z", 
  "repo:lastModifiedDate": "2019-06-05T03:44:25.343Z", 
  "repo:createdBy": "CREATOR_ACCOUNT_ID", 
  "repo:lastModifiedBy": "YOUR_TECHNICAL_ACCOUNT_ID", 
  "repo:createdByClientId": "CREATOR_API_KEY", 
  "repo:lastModifiedByClientId": "YOUR_API_KEY" 
} 
```

Ao receber uma solicitação de exclusão, o repositório verifica se há outras instâncias, de qualquer schema, ainda referenciam a instância a ser excluída. Em um sistema distribuído e altamente disponível, a integridade referencial não pode ser verificada imediatamente. Quando houver relações de chave estrangeira definidas, as verificações serão feitas de forma assíncrona. Isso resulta em uma resposta ligeiramente atrasada ao resultado da solicitação de exclusão. Quando essas verificações são executadas, a resposta imediata inclui o status 202 Aceito e um link para verificar o resultado da operação de exclusão no `Location` cabeçalho. Um cliente deve então verificar o link para o resultado.

Se for encontrada uma instância que referencie a instância que está sendo excluída, o resultado será uma rejeição da operação de exclusão. Se nenhuma outra referência de chave estrangeira for descoberta, a exclusão será concluída. Se o resultado ainda não for decidido, a resposta indicará que em outra resposta 202 Aceita com o mesmo cabeçalho `Location` e solicitará que o cliente continue verificando. Quando o resultado for determinado, a resposta indicará que com um status 200 Ok e a carga da resposta conterá o resultado da solicitação de exclusão original. Observe que a resposta 200 Ok significa apenas que o resultado é conhecido e o corpo da resposta conterá a confirmação ou rejeição da solicitação de exclusão.

## Criação de ofertas e seus subcomponentes

As APIs descritas na seção anterior aplicam-se uniformemente a todos os tipos de objetos de negócios. A única diferença entre, digamos, criar uma oferta e uma atividade seria o cabeçalho que `content-type` anota o schema JSON na carga JSON da solicitação que está em conformidade com o schema. Portanto, as seções a seguir só precisarão se concentrar nesses schemas e nas relações entre eles.

Ao usar as APIs com o tipo de conteúdo `application/vnd.adobe.platform.xcore.hal+json; schema="{SCHEMA_ID}"`, as próprias propriedades da instância são incorporadas na `_instance` propriedade próxima à qual há uma `_links` propriedade. Esse será o formato geral no qual todas as instâncias serão representadas:

```json
{ 
  … ENVELOPE PROPERTIES 
  "_instance": { 
    INSTANCE PROPERTIES 
  }, 
  "_links": {
    HAL PROPERTIES 
  } 
}
```

>[!NOTE]
>
>Por motivos de brevidade, em todos os trechos JSON, somente as propriedades da instância são ilustradas e somente quando necessário, as propriedades do envelope e a seção _links são mostradas.

### Propriedades gerais da oferta

O Oferta é um tipo de opção de decisão e o schema JSON do oferta herda as propriedades de opção padrão que cada instância de opção terá.

- **`@id`** - Um identificador exclusivo para cada opção que é a chave primária e usada para referenciar a opção de outros objetos. Essa propriedade é atribuída quando a instância é criada, é imutável e não é editável.
- **`xdm:name`** - Cada opção tem um nome que é usado para fins de pesquisa e exibição. O nome não é imutável e não pode ser usado para identificar exclusivamente a instância. O nome pode ser selecionado livremente, mas deve ser exclusivo em instâncias de oferta.

```json
{ 
  "@id": "INSTANCE_URI",                         // meta:immutable=true, meta:usereditable=false 
  "xdm:name": "A name for the Decision Option",  // meta:immutable=false 
  "xdm:characteristics": { 
    properties specific to this instance         // property names can vary per instance 
  } 
}
```

Consulte [Atualização e correção de instâncias](#updating-and-patching-instances) para obter a sintaxe completa de cURL. O `schemaId` parâmetro deve ser `https://ns.adobe.com/experience/offer-management/personalized-offer` ou `https://ns.adobe.com/experience/offer-management/fallback-offer` se a oferta for uma oferta de fallback.

Cada instância de oferta pode ter um conjunto opcional de propriedades que são características apenas para essa instância. Ofertas diferentes podem ter chaves diferentes para essas propriedades, mas os valores devem ser strings. Essas propriedades podem ser usadas em regras de decisão e segmentação. Eles também estão acessíveis para reunir a experiência decidida para personalizar ainda mais as mensagens.

### Ciclo de vida da oferta

Há um fluxo de transição de estado simples que todas as Opções seguirão. Eles start em um estado de rascunho e quando estiverem prontos seu estado será definido para aprovação. Quando a data final for ultrapassada, eles poderão ser movidos para o estado arquivado. Nesse estado, podem ser eliminados ou reutilizados, transferindo-os para o estado de redação.

![](../images/entities/offer-lifecycle.png)

- **`xdm:status`** - Essa propriedade é usada para o gerenciamento do ciclo de vida da instância. O valor representa um estado de fluxo de trabalho que é usado para indicar se a oferta ainda está em construção (valor = rascunho), pode ser considerado pelo tempo de execução (valor = aprovado) ou se não deve ser usada por mais tempo (valor = arquivado).

Uma operação simples de PATCH na instância é normalmente usada para manipular uma `xdm:status` propriedade:

```json
[
  {
    "op":    "replace",
    "path":  "/_instance/xdm:status",
    "value": "approved" 
  }
]
```

Consulte [Atualização e correção de instâncias](#updating-and-patching-instances) para obter a sintaxe completa de cURL. O `schemaId` parâmetro deve ser `https://ns.adobe.com/experience/offer-management/personalized-offer` ou `https://ns.adobe.com/experience/offer-management/fallback-offer` se a oferta for uma oferta de fallback.

### Representações e disposições

Ofertas são opções de decisão que têm representações de conteúdo. Quando uma decisão é tomada, a opção é selecionada e seu identificador é usado para obter o conteúdo ou as referências de conteúdo para a disposição que precisa ser fornecida. Uma oferta pode ter mais de uma representação, mas cada uma delas precisa ter uma referência de posicionamento diferente. Isso garante que, com uma determinada disposição, a representação possa ser determinada de forma inequívoca.
Durante a operação de decisão, a disposição é determinada em conjunto com o objeto de atividade. Ofertas que não têm uma representação com essa disposição como referência são automaticamente eliminadas da lista de opções.

Antes que as representações possam ser adicionadas a uma oferta, as instâncias de posicionamento devem existir. Essas instâncias são criadas com o identificador`https://ns.adobe.com/experience/offer-management/offer-placement`do schema.

```json
{
  "xdm:name": "Kiosk Placement 1",
  "xdm:channel": "https://ns.adobe.com/xdm/channels/web",
  "xdm:componentType": 
     "https://ns.adobe.com/experience/offer-management/content-component-imagelink",
  "xdm:contentTypes": [
    "image/png", "image/png"
  ],
  "xdm:description": "Generic placeholder for offers in the Kiosk application. \nTechnical constraints: max width 530dpi, min width 480 dpi, aspect ratio 12:5. \nStylistic constraints: single background color with text block in complementary colors, \nNo magenta, please!"
} 
```

Consulte [Atualização e correção de instâncias](#updating-and-patching-instances) para obter a sintaxe completa de cURL. O `schemaId` parâmetro deve ser `https://ns.adobe.com/experience/offer-management/personalized-offer` ou `https://ns.adobe.com/experience/offer-management/fallback-offer` se a oferta for uma oferta de fallback.

Uma instância **de Disposição** pode ter as seguintes propriedades:

- **`xdm:name`** - Contém o nome atribuído para a disposição para se referir a ela em interações humanas e interfaces do usuário.
- **`xdm:description`** - Usado para transmitir intenções legíveis humanas de como o conteúdo nesta disposição é usado no delivery geral de mensagens. Quando os canais de delivery definem novas disposições, eles podem adicionar mais informações nesta propriedade para que um criador de conteúdo possa criar ou selecionar o conteúdo de acordo. Essas instruções não são formalmente interpretadas ou aplicadas. Essa propriedade serve apenas como um lugar para comunicar as intenções.
- **`xdm:channel`** - O URI de um canal. O canal indica onde o conteúdo dinâmico deve ser entregue. A restrição de canal é usada para transmitir não apenas onde a oferta será usada, mas também para determinar o editor ou validador de conteúdo usado para a experiência.
- **`xdm:componentType`** - Um identificador de modelo, ou seja, URI, para o conteúdo que pode ser exibido no local descrito por essa disposição. Os tipos de componentes são: link de imagem, html ou texto sem formatação. Cada tipo de componente pode implicar um conjunto específico de propriedades (um modelo) que o item de conteúdo pode ter. A lista de tipos de componentes pode ser estendida. Há três valores predefinidos de tipo de componente:
   - `https://ns.adobe.com/experience/offer-management/content-component-imagelink`
   - `https://ns.adobe.com/experience/offer-management/content-component-text`
   - `https://ns.adobe.com/experience/offer-management/content-component-html`
- **`xdm:contentTypes`**, uma restrição para os tipos de mídia dos componentes que são esperados nesta disposição. Pode haver mais de um tipo de mídia para um tipo de componente, como formatos de imagem diferentes.

**Os itens de representação** em uma oferta têm uma estrutura de objeto na propriedade array `xdm:representations`. Cada item pode ter as seguintes propriedades:

- **`xdm:placement`** - Essa propriedade contém a referência à instância de posicionamento. O valor é verificado quando a representação é adicionada à oferta. Uma instância de disposição com esse URI deve existir e não deve ser marcada como excluída. Além disso, uma verificação é executada para garantir que uma instância oferta não tenha duas representações com o mesmo valor para sua referência de posicionamento.
- **`xdm:components`** - Os componentes de conteúdo são os fragmentos associados a uma representação da oferta específica. Esses fragmentos são usados posteriormente para compor a experiência do usuário final. Observe que o Serviço de decisão por si só não compõe a experiência completa do usuário final. As seguintes propriedades fazem parte do modelo de cada componente.
   - **`@type`** - essa propriedade identifica o tipo de componente. Outro nome para esse conceito é o modelo de fragmento de conteúdo. O `@type` de um componente é simplesmente um URI para um modelo definido pelo aplicativo ou serviço que está montando a experiência do usuário final.
   - **`repo:id`** - essa propriedade contém um identificador global exclusivo para o recurso principal do componente no repositório em que o ativo é armazenado.
   - **`repo:name`** - Essa propriedade contém um nome legível para o ativo no repositório. Esse nome é definido pelo usuário e não é garantido que seja exclusivo.
   - **`repo:resolveURL`** - esta propriedade contém um localizador de recursos exclusivo para ler o ativo em um repositório de conteúdo. Isso facilitará a obtenção do ativo sem que o cliente entenda quais APIs chamar. O URL retorna os bytes do recurso principal do ativo.
   - **`dc:format`** - esta propriedade provém da iniciativa Dublin Core Metadata. O formato pode ser usado para determinar o software, hardware ou outro equipamento necessário para exibir ou operar o recurso. A prática recomendada é selecionar um valor de um vocabulário controlado (por exemplo, a lista de tipos de mídia da Internet que definem formatos de mídia do computador).
   - **`dc:language`** - Essa propriedade contém o idioma ou os idiomas do recurso. Os idiomas são especificados no código de idioma, conforme definido em IETF RFC 3066.

Há três tipos de componentes predefinidos expressos na `@type` propriedade:

- https<span></span>://ns.adobe.com/experience/oferta-management/content-component-imagelink
- https<span></span>://ns.adobe.com/experience/oferta-management/content-component-text
- https<span></span>://ns.adobe.com/experience/oferta-management/content-component-html

Dependendo do valor da `@type` propriedade, `xdm:components` conterão propriedades adicionais:

- **`xdm:linkURL`** - Presente quando o componente for um link de imagem. Essa propriedade conterá o link associado à imagem e para o qual o usuário final `user-agent` navegará quando interagir com o conteúdo da oferta.
- **`xdm:copyline`** - Usado quando o componente é um texto. Além de fazer referência a um ativo de texto, por exemplo, para Ofertas de texto de formulário longo que podem ter formatação nele, uma string de texto curta pode ser armazenada diretamente na propriedade xdm:copyline.

Propriedades adicionais podem ser usadas pelos clientes para definir e avaliar as instruções de manuseio de contexto. Por exemplo, o cliente Biblioteca da interface de Oferta adiciona as seguintes propriedades opcionais para lidar com a exibição com mais facilidade:

- Dentro de cada item na `xdm:components` matriz, o cliente da interface de usuário da biblioteca de Ofertas adiciona as seguintes propriedades. Essas propriedades não devem ser excluídas ou manipuladas sem compreender o impacto na interface do usuário:
   - **`offerui:previewThumbnail`** - Essa é uma propriedade opcional que a interface do usuário da biblioteca de Ofertas usa para exibir uma renderização do ativo. Essa representação não é igual ao próprio ativo. Por exemplo, o conteúdo pode ser HTML e a execução é uma imagem bitmap que mostra apenas uma aproximação dele. Essa representação (qualidade inferior) é exibida no bloco de representação da oferta.

Um exemplo de operação de PATCH em uma instância de oferta mostra como manipular as representações:

```json
[
  {
    "op":    "add",
    "path":  "/_instance/xdm:representations/-",
    "value": {
      "xdm:placement": "xcore:offer-placement:e51944a87919861",
      "xdm:components": [
        {
          "xdm:copyline": "Get what you want!",
          "@type": "https://ns.adobe.com/experience/offer-management/content-component-text",
          "dc:format": "text/plain"
        }
      ]
    } 
  }
]' 
```

Consulte [Atualização e correção de instâncias](#updating-and-patching-instances) para obter a sintaxe completa de cURL. O `schemaId` parâmetro deve ser `https://ns.adobe.com/experience/offer-management/personalized-offer` ou `https://ns.adobe.com/experience/offer-management/fallback-offer` se a oferta for uma oferta de fallback.

A operação PATCH pode falhar quando ainda não há propriedade `xdm:representations` . Nesse caso, a operação de adição acima pode ser precedida por outra operação de adição que cria a `xdm:representations` matriz ou a operação de adição única define a matriz diretamente.
Os schemas e as propriedades descritas são usados para todos os tipos de oferta, ofertas de personalização e ofertas de fallback. As duas seções a seguir sobre restrições e regras de decisão explicam os aspectos das ofertas de personalização.

## Configuração de restrições de oferta

### Restrições do calendário

As opções de decisão em geral podem receber um start e data e hora de término que serve como uma restrição de calendário. As propriedades são incorporadas na propriedade `xdm:selectionConstraint`:

- **`xdm:startDate`** - Essa propriedade indica a data e a hora do start. O valor é uma string formatada de acordo com as regras RFC 3339, ou seja, como este carimbo de data e hora: &quot;2019-06-13T11:21:23.356Z&quot;.
As opções de decisão que não atingiram a data e hora de start ainda não são consideradas elegíveis na decisão.
- **`xdm:endDate`** - Essa propriedade indica a data e a hora de término. O valor é uma string formatada de acordo com as regras RFC 3339, ou seja, como este carimbo de data e hora: &quot;2019-07-13T11:00:00.000Z&quot;As opções de decisão que passaram na data e hora de término não são mais consideradas elegíveis no processo de decisão.

A alteração de uma restrição de calendário pode ser realizada com a seguinte chamada de PATCH:

```json
[
  {
    "op":   "replace",
    "path": "/_instance/xdm:selectionConstraint",
    "value": {
      "xdm:startDate": "2019-06-13T00:00:00.000Z",
      "xdm:endDate":   "2019-07-13T00:00:00.000Z"
    } 
  }
]' 
```

Consulte [Atualização e correção de instâncias](#updating-and-patching-instances) para obter a sintaxe completa de cURL. O `schemaId` parâmetro deve ser `https://ns.adobe.com/experience/offer-management/personalized-offer`. As ofertas de fallback não têm restrições.

### Limitação de restrições

Uma restrição de limite é um componente em uma opção de decisão que define os parâmetros para o limite. A limitação é o processo de limitar quantas vezes uma opção pode ser proposta, para um perfil individual e para todos os perfis. As propriedades têm um valor inteiro que deve ser maior ou igual a 1. As propriedades são aninhadas dentro de uma propriedade `xdm:cappingConstraint`:

- **`xdm:globalCap`** - Um limite máximo global é um limite para o número total de vezes que uma oferta pode ser proposta.
- **`xdm:profileCap`** - Um limite máximo para o perfil é um limite para o número de vezes que uma oferta pode ser proposta a um determinado perfil.

A configuração ou alteração da restrição de limite em uma oferta de personalização pode ser realizada com a seguinte chamada de PATCH:

```json
[
  {
    "op":   "add",
    "path": "/_instance/xdm:cappingConstraint",
    "value": {
      "xdm:globalCap":  1000000,
      "xdm:profileCap": 5
    } 
  }
]' 
```

Consulte [Atualização e correção de instâncias](#updating-and-patching-instances) para obter a sintaxe completa de cURL. O `schemaId` parâmetro deve ser `https://ns.adobe.com/experience/offer-management/personalized-offer`. As ofertas de fallback não têm restrições.

Para remover os valores de limite, a operação &quot;adicionar&quot; é substituída pela operação &quot;remover&quot;. Observe que os valores de limite existem individualmente e também podem ser definidos ou removidos individualmente.

### Restrições de elegibilidade

Ofertas podem ser selecionadas condicionalmente no processo de decisão. Quando uma oferta de personalização tem uma referência a uma regra de elegibilidade, a condição da regra deve ser avaliada como true para que o objeto de oferta seja considerado para um determinado perfil. As regras de elegibilidade são criadas e gerenciadas independentemente das opções de decisão e a mesma regra pode ser referenciada de várias ofertas de personalização.

A referência à regra é incorporada na propriedade `xdm:selectionConstraint`:

- **`xdm:eligibilityRule`** - Esta propriedade contém uma referência a uma regra de elegibilidade. O valor é a `@id` de uma instância de schemahttps://ns.adobe.com/experience/offer-management/eligibility-rule.

A adição e exclusão de uma regra também pode ser realizada com uma operação de PATCH:

```json
[
  {
    "op":   "replace",
    "path": "/_instance/xdm:selectionConstraint/xdm:eligibilityRule",
    "value": "xcore:eligibility-rule:f84c6b33cc63c65" 
  }
]'
```

Consulte [Atualização e correção de instâncias](#updating-and-patching-instances) para obter a sintaxe completa de cURL. O `schemaId` parâmetro deve ser `https://ns.adobe.com/experience/offer-management/personalized-offer`. As ofertas de fallback não têm restrições.

Observe que a regra de elegibilidade é incorporada na `xdm:selectionConstraint` propriedade juntamente com as restrições do calendário. As operações de PATCH não devem tentar remover toda a `SelectionConstraint` propriedade.

## Definição da prioridade de uma oferta

As opções de decisão de qualificação serão classificadas para determinar a melhor opção para o perfil em questão. Para suportar a classificação e fornecer um padrão caso a classificação não possa ser determinada por outro mecanismo, uma prioridade básica pode ser definida para cada oferta de personalização.
A prioridade básica é incorporada na propriedade `xdm:rank`:

- **`xdm:priority`** - Essa propriedade representa a ordem padrão na qual uma oferta é selecionada sobre outra caso não haja nenhuma ordem de classificação específica do perfil conhecida. Se, após comparar o valor de prioridade, duas ou mais ofertas de personalização ainda estiverem ligadas, uma é escolhida aleatoriamente e usada na apresentação da oferta. O valor para essa propriedade deve ser um número inteiro maior ou igual a 0.

O ajuste da prioridade básica pode ser feito com a seguinte chamada de PATCH:

```shell
curl -X PATCH {ENDPOINT_PATH}/{CONTAINER_ID}/instances/{INSTANCE_ID} \
  -H 'Content-Type: application/vnd.adobe.platform.xcore.patch.hal+json; schema="{SCHEMA_ID}"' \ 
  -H 'Accept: application/vnd.adobe.platform.xcore.xdm.receipt+json \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  _H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'x-request-id: {NEW_UUID}' \
  -d '[
  {
    "op":   "replace",
    "path": "/_instance/xdm:rank/xdm:priority",
    "value": 0 
  }
]'
```

Consulte [Atualização e correção de instâncias](#updating-and-patching-instances) para obter a sintaxe completa de cURL. O `schemaId` parâmetro deve ser `https://ns.adobe.com/experience/offer-management/personalized-offer`. As ofertas de fallback não têm propriedades de classificação.

## Gerenciar regras de decisão

As regras de elegibilidade mantêm as condições que são avaliadas para determinar se uma determinada opção de decisão é qualificada para um determinado perfil. Anexar uma regra a uma ou mais opções de decisão define implicitamente que para essa opção a regra deve ser avaliada como true para que a opção seja considerada para esse usuário. A regra pode conter testes em atributos de perfil, pode avaliar expressões envolvendo eventos de experiência para esse perfil e pode incluir dados de contexto que foram passados para a solicitação de decisão. Por exemplo, uma condição pode ser descrita como:

> &quot;Incluir indivíduos que tenham status de elite e tenham voado em um voo três vezes nos últimos seis meses que tenha o número de voo do voo atual.&quot;

As instâncias são criadas com o identificador de schemahttps://ns.adobe.com/experience/offer-management/eligibility-rule. A `_instance` propriedade para a chamada de criação ou atualização é semelhante:

```json
{
  "xdm:name": "Eligible for a free flight upgrade",
  "xdm:condition": {
    "xdm:value": 
      "membership.status = \"elite\" 
       and (select e from xEvent 
            where e.type = \"flight\" 
              and e.flightnumber = @{{SCHEMA_ID}}.flightnumber
              and (e.timestamp occurs <= 6 months before now).count() > 3
           )",
    "xdm:format": "pql/text",
    "xdm:type": "PQL"
  }
}
```

Consulte [Atualização e correção de instâncias](#updating-and-patching-instances) para obter a sintaxe completa de cURL. O `schemaId` parâmetro deve ser `https://ns.adobe.com/experience/offer-management/eligibility-rule`.

O valor na propriedade de condição da regra contém uma expressão PQL. Os dados de contexto são referenciados por meio da expressão de caminho especial @{schemaID}.

As regras são alinhadas naturalmente com os segmentos no [!DNL Experience Platform] e, muitas vezes, uma regra simplesmente reutiliza a intenção de um segmento testando a `segmentMembership` propriedade de um perfil. A `segmentMembership` propriedade contém os resultados de condições de segmentos que já foram avaliadas. Isso permite que uma organização defina suas audiências específicas de domínio uma vez, nomeie-as e avalie as condições uma vez.

## Gerenciamento de coleções de ofertas

### Criação de tags e ofertas de marcação

As ofertas podem ser organizadas em coleções nas quais cada coleção define a condição do filtro que deve ser aplicada. Atualmente, a expressão de filtro em uma coleção pode ter um de dois formulários:

1. O `@id` parâmetro da oferta deve corresponder a um em uma lista de identificadores para que a oferta esteja na coleção. Esse filtro é simplesmente uma lista discriminada dos URIs das ofertas na coleção.
2. Uma oferta pode ter uma lista de referências de tags e o filtro da coleção consiste em uma lista de tags. A oferta está na coleção quando:\
   a. qualquer tag do filtro corresponde a uma das tags da oferta\
   b. todas as tags do filtro correspondem a uma das tags da oferta

As tags são instâncias simples às quais as instâncias de oferta podem ser vinculadas. São instâncias próprias com um nome para exibi-las. O nome deve ser exclusivo entre instâncias para facilitar a exibição na interface do usuário.

Os objetos de tag servem para estabelecer uma categorização entre as opções de decisão (oferta). Uma tag pode ser vinculada por muitas ofertas e uma oferta pode ter muitas referências de tag. Uma categoria de ofertas é estabelecida fazendo referência a todas as ofertas relacionadas a um determinado conjunto de instâncias de tags.

As instâncias de tag são criadas com o identificador de schemahttps://ns.adobe.com/experience/offer-management/tag. A `_instance` propriedade para a chamada de criação ou atualização é semelhante:

```json
{
  "xdm:name": "credit card"
} 
```

Consulte [Atualização e correção de instâncias](#updating-and-patching-instances) para obter a sintaxe completa de cURL. O `schemaId` parâmetro deve ser `https://ns.adobe.com/experience/offer-management/tag`.


Uma instância de oferta pode ser criada com a lista de referências de tag, como:

```json
{
  "xdm:name": "ABC Bank Credit Card",
  "xdm:tags": [
    "xcore:tag:f66f67dbe6d6ee1",
    "xcore:tag:f2df943c428b6f7"
  ]
}
```

Como alternativa, uma oferta pode ser corrigida para alterar sua lista de tags:

```json
[
  {
    "op":    "add",
    "path":  "/_instance/xdm:tags/-",
    "value": "xcore:tag:f66f677ad3c0ba7" 
  }
]' 
```

Para ambos os casos, consulte [Atualização e correção de instâncias](#updating-and-patching-instances) para a sintaxe cURL completa. O `schemaId` parâmetro deve ser `https://ns.adobe.com/experience/offer-management/personalized-offer`.

Observe que a `xdm:tags` propriedade já deve existir para que a operação de adição tenha êxito. Não existem tags em uma instância, a operação PATCH pode primeiro adicionar a propriedade array e depois adicionar uma referência de tag a essa matriz.

### Definir filtros para coleções de ofertas

As instâncias de filtro são criadas com o identificador de schemahttps://ns.adobe.com/experience/offer-management/offer-filter. A `_instance` propriedade para a chamada de criação ou atualização pode ser semelhante a:

```json
{
  "xdm:name": "All Upgrade offers",
  "xdm:filterType": "allTags",
  "ids": [
    "xcore:tag:f66f67dbe6d6ee1",
    "xcore:tag:f66f677ad3c0ba7"
  ]
}
```

Consulte [Atualização e correção de instâncias](#updating-and-patching-instances) para obter a sintaxe completa de cURL. O `schemaId` parâmetro deve ser `https://ns.adobe.com/experience/offer-management/offer-filter`.

- **`xdm:filterType`** - Essa propriedade indica se o filtro está configurado usando tags ou se faz referência direta a ofertas por suas ids. Quando o filtro é configurado para usar tags, o tipo de filtro pode indicar ainda mais se todas as tags devem corresponder às tags em uma oferta específica ou se qualquer uma dessas tags for suficiente para que a oferta se qualifique para o filtro. Os valores válidos desta propriedade enum são:
   - `offers`
   - `anyTags`
   - `allTags`
- **`ids`** - Uma propriedade contém uma matriz de URIs que são referências a instâncias de oferta ou a instâncias de tag, dependendo do valor de `xdm:filterType`. .

A chamada a seguir ilustra a aparência da propriedade `_instance` para a chamada de criação ou atualização caso as ofertas sejam referenciadas diretamente:

```json
{
  "xdm:name": "All Upgrade offers",
  "xdm:filterType": "offers",
  "ids": [
    "xcore:personalized-offer:f85e8298e53398d",
    "xcore:personalized-offer:f83a85c2bca3f1f",
    "xcore:personalized-offer:f9195bd412180b1",
    "xcore:personalized-offer:f67be37b6ad6ee6",
    "xcore:personalized-offer:f87bcc710ba6e93",
    "xcore:personalized-offer:f8855c30c0b20f8",
    "xcore:personalized-offer:f67bca7032d6ee5",
    "xcore:personalized-offer:f67bab756ed6ee4",
    "xcore:personalized-offer:f65281d506d6edf"
  ] 
} 
```

## Gerenciamento de atividades

Uma atividade oferta é usada para controlar o processo de decisão. Ela especifica o filtro de oferta aplicado ao inventário total para restringir ofertas por tópico/categoria, a disposição para restringir o inventário às ofertas que se encaixam no espaço reservado e especifica uma opção de fallback se as restrições combinadas desqualificarem todas as opções de personalização disponíveis (oferta).

As instâncias de atividade são criadas com o identificador`https://ns.adobe.com/experience/offer-management/offer-activity`de schema. A `_instance` propriedade para a chamada de criação ou atualização é semelhante:

```json
{
  "xdm:name": "Call center IVR Personalization",
  "xdm:startDate": "2019-03-01T05:59:59.999Z",
  "xdm:endDate":   "2019-12-27T00:00:00.000Z",
  "xdm:status":    "live",
  "xdm:placement": "xcore:offer-placement:f652486959731ff",
  "xdm:filter":    "xcore:offer-filter:f6998eb62ed6f15",
  "xdm:fallback":  "xcore:fallback-offer:f6529b31b3c0ba6"
}
```

Consulte [Atualização e correção de instâncias](#updating-and-patching-instances) para obter a sintaxe completa de cURL. O `schemaId` parâmetro deve ser `https://ns.adobe.com/experience/offer-management/offer-activity`.

- **`xdm:name`** - Esta propriedade obrigatória contém o nome da atividade. O nome é exibido em várias interfaces do usuário.
- **`xdm:status`** - Essa propriedade é usada para o gerenciamento do ciclo de vida da instância. O valor representa um estado de fluxo de trabalho que é usado para indicar se a atividade ainda está em construção (valor = rascunho), pode ser considerado pelo tempo de execução (valor = live) ou se não deve ser usada por mais tempo (valor = arquivado).
- **`xdm:placement`** - Uma propriedade obrigatória que contenha uma referência a uma disposição de oferta aplicada ao inventário quando uma decisão é tomada no contexto dessa atividade. O valor é o URI (`@id`) da disposição da oferta usada.
- **`xdm:filter`** - Uma propriedade obrigatória que contenha uma referência a um filtro de oferta aplicado ao inventário quando uma decisão é tomada no contexto desta atividade. O valor é o URI (`@id`) do filtro de oferta usado.
- **`xdm:fallback`** - Uma propriedade obrigatória contendo uma referência a uma oferta de fallback. Uma oferta de fallback é usada quando a decisão para essa atividade não qualifica nenhuma das ofertas de personalização. O valor é o URI (`@id`) de uma instância de oferta de fallback.

### Gerenciando ofertas de fallback

Antes que as instâncias de atividade possam ser criadas, é necessário que exista uma oferta de fallback qualificada para o posicionamento da atividade. As instâncias de oferta de fallback são criadas com o identificador`https://ns.adobe.com/experience/offer-management/fallback-offer`de schema. A `_instance` propriedade para a chamada de criação ou atualização contém as mesmas propriedades gerais que uma oferta de personalização possui, mas não pode ter outras restrições.

```json
{
  "xdm:name": "Default for Kiosk Placements",
  "xdm:status": "approved",
  "xdm:representations": [
    {
      "xdm:placement": "xcore:offer-placement:e91afcf81bad130"
      "xdm:components": [
        {
          "dc:language": ["en" ],
          "@type": "https://ns.adobe.com/experience/offer-management/content-component-html",
          "dc:format": "text/html"
        }
      ]
    }
  ]
}  
```

Consulte [Atualização e correção de instâncias](#updating-and-patching-instances) para obter a sintaxe completa de cURL. O `schemaId` parâmetro deve ser `https://ns.adobe.com/experience/offer-management/fallback-offer`.

