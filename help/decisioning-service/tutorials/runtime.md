---
keywords: Experience Platform;home;popular topics;decision events;decision event;Decision events
solution: Experience Platform
title: Trabalhar com tempo de execução do serviço de decisão usando APIs
topic: tutorial
description: 'Este documento fornece um tutorial para trabalhar com os serviços de tempo de execução do serviço de decisão usando APIs da Adobe Experience Platform. '
translation-type: tm+mt
source-git-commit: 1b398e479137a12bcfc3208d37472aae3d6721e1
workflow-type: tm+mt
source-wordcount: '2017'
ht-degree: 0%

---


# Trabalhar com tempo de execução do serviço de decisão usando APIs

Este documento fornece um tutorial para trabalhar com os serviços de tempo de execução do [!DNL Decisioning Service] uso de APIs da Adobe Experience Platform.

## Introdução

Este tutorial requer uma compreensão do trabalho dos [!DNL Experience Platform] serviços envolvidos na tomada de decisões e na determinação da próxima melhor oferta a ser apresentada durante as experiências do cliente. Antes de iniciar este tutorial, reveja a documentação do seguinte:

- [[!Serviço de Decisão DNL]](./../home.md): Fornece a estrutura para adicionar e remover ofertas e criar algoritmos para escolher o melhor para apresentar durante a experiência do cliente.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): A estrutura padronizada pela qual a Plataforma organiza os dados de experiência do cliente.
- [[!Linguagem de Query de Perfil DNL (PQL)](../../segmentation/pql/overview.md): O PQL é usado para definir regras e filtros.
- [Gerencie objetos e regras de decisão usando APIs](./entities.md): Antes de usar o tempo de execução dos Serviços de tomada de decisão, será necessário configurar as entidades relacionadas.

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
>Para obter mais informações sobre caixas de proteção em [!DNL Platform], consulte a documentação [de visão geral da](../../tutorials/authentication.md)caixa de proteção.

Todas as solicitações que contêm uma carga (POST, PUT, PATCH) exigem um cabeçalho adicional:

- Tipo de conteúdo: application/json

Também é necessário para solicitações de tempo de execução:

- x-request-id: `{UUID}`

>[!NOTE]
>
>`UUID` é uma string no formato UUID que é globalmente exclusiva e não deve ser reutilizada para chamadas de API diferentes

[!DNL Decisioning Service] é controlada por vários objetos de negócios relacionados entre si. Todos os objetos de negócios são armazenados no repositório de objetos de negócios, Repositório de objetos principais do XDM. [!DNL Platform’s] Um recurso importante desse repositório é que as APIs são ortogonais em relação ao tipo de objeto de negócios. Em vez de usar uma API POST, GET, PUT, PATCH ou DELETE que indica o tipo de recurso em seu endpoint de API, há apenas 6 endpoints genéricos, mas eles aceitam ou retornam um parâmetro que indica o tipo de objeto quando essa indicação é necessária. O schema deve ser registrado no repositório, mas além disso o repositório pode ser usado para um conjunto ilimitado de tipos de objetos.

Os caminhos de ponto de extremidade para todos os start de APIs do Repositório de objetos principais do XDM com `https://platform.adobe.io/data/core/ode/`.

O primeiro elemento de caminho após o terminal é o `containerId`. Esse identificador é obtido por meio do endpoint raiz do Repositório de objetos principais do XDM `GET https://platform.adobe.io/data/core/xcore/`.

## Compilação de modelos de decisão

A ativação das entidades de lógica comercial acontece automática e continuamente. Assim que uma nova opção for salva no repositório e for marcada como &quot;aprovada&quot;, ela será candidata à inclusão do conjunto de opções disponíveis. Assim que uma regra de decisão for atualizada, o conjunto de regras será remontado e preparado para execução em tempo de execução. Nesta etapa de ativação automática, todas as restrições definidas pela lógica de negócios que não dependem do contexto de tempo de execução serão avaliadas. Os resultados desta etapa de ativação são enviados para um cache onde estão disponíveis para o [!DNL Decisioning Service] tempo de execução.

### Efeitos de disposições, filtros e estados do ciclo de vida

As ofertas são criadas continuamente, as alterações ocorrem em seu status de ciclo de vida ou podem ter novas representações de conteúdo. O filtro de oferta de uma atividade pode mudar ou corresponder ou filtrar ofertas cujos conjuntos de tags foram atualizados. Este processo pode estar bastante envolvido e as aplicações e os serviços precisam de saber qual será o conjunto de candidatos resultante de uma atividade. O tempo de execução de decisão fornece uma API de atividade para oferta que filtros ofertas que não foram aprovadas, não correspondem ao filtro de oferta ou não têm uma representação para a disposição referenciada pela atividade.

**Solicitação**

```shell
curl -X GET {DECISION_SERVICE_ENDPOINT_PATH}/{CONTAINER_ID}/offers?activityId={ACTIVITY_URI}' \
  -H 'Accept: application/vnd.adobe.xdm+json \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'x-request-id: {NEW_UUID}'
```

**Resposta**

O parâmetro `activityId` pode ser repetido no url e até 30 referências de atividade diferentes podem ser fornecidas em uma solicitação. A resposta será útil para detectar quaisquer circunstâncias inesperadas resultantes da configuração e terá a seguinte aparência:

```json
{
  "xdm:activityOffers": [
    {
      "xdm:offerActivity": {
        "@id": "{ACTIVITY_URI}",
        "_links": {
          "self": {
            "href": "{repository_endpoint}/{CONTAINER_ID}/instances/{ACTIVITY_INSTANCE_ID}"
          }
        },
        "repo:etag": "1"
      },
      "xdm:offers": [
        {
          "@id": "{OFFER_URI_1}",
          "_links": {
            "self": {
              "href": "{REPOSITORY_ENDPOINT}/{CONTAINER_ID}/instances/{OFFER_INSTANCE_ID_1}"
            }
          },
          "repo:etag": "15"
        },
        {
          "@id": "{OFFER_URI_2}",
          "_links": {
            "self": {
              "href": "{REPOSITORY_ENDPOINT}/{CONTAINER_ID}/instances/{OFFER_INSTANCE_ID_2}"
            }
          },
          "repo:etag": "5"
        }
      ],
      "xdm:fallbackOffer": {
        "@id": "{FALLBACK_URI}",
        "_links": {
          "self": {
            "href": "{REPOSITORY_ENDPOINT}/{CONTAINER_ID}/instances/{FALLBACK_INSTANCE_ID}"
          }
        },
        "repo:etag": "2"
      }
    }
  ]
}
```

Há um pequeno atraso de alguns segundos entre o momento em que os objetos foram atualizados e o momento em que a resposta da API reflete o mapeamento de atividade para oferta. A revisão de cada objeto é fornecida na resposta para que os clientes possam verificar se há uma atualização nos objetos que não foi refletida.

### API de diagnóstico e solução de problemas

Atividades, ofertas e regras de elegibilidade são compilados em um formato interno (catálogo de oferta de tempo de execução) usado pelo tempo de execução do serviço de decisão. A compilação pode detectar erros que não foram detectados pelas verificações realizadas quando os objetos foram armazenados e os links foram estabelecidos no Repositório de objetos principais do XDM.

Uma API de diagnóstico é fornecida para obter quaisquer erros de compilação que ocorreram nessa etapa e, no caso de não haver erros para obter informações sobre quando as regras e atividades foram recompiladas pela última vez.

**Solicitação**

```shell
curl -X GET {DECISION_SERVICE_ENDPOINT_PATH}/{CONTAINER_ID}/diagnostics \
  -H 'Accept: application/vnd.adobe.xdm+json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'x-request-id: {NEW_UUID}'
```

O único parâmetro para esta chamada de API é `containerId`. Os resultados de todas as atualizações de todos os clientes que modificaram regras de decisão, ofertas, atividades ou filtros de oferta nesse container. Há um pequeno atraso de alguns segundos entre o momento em que os objetos foram atualizados e o momento em que a compilação é concluída. O último carimbo de data e hora da atualização e quaisquer erros são retornados na resposta à chamada de diagnóstico.

**Resposta**

```json
{
  "xdm:operations": {
    "xdm:offerCatalogUpdate": {
      "xdm:date": "2019-06-19T23:28:44.855Z",
      "xdm:errors": []
    },
    "xdm:activitiesUpdate": {
      "xdm:date": "2019-06-19T23:28:40.114Z",
      "xdm:errors": []
    }
  }
}
```

## Chamadas REST API para executar decisões

A REST API é uma das rotas para aplicativos em execução no topo do para obter [!DNL Platform] a próxima melhor experiência com base nas regras, modelos e restrições que a organização definiu para seus usuários. Os aplicativos enviam uma das identidades do perfil (ID do perfil e namespace de identidade) e [!DNL Decisioning Service] pesquisam o perfil e as informações são usadas para aplicar a lógica comercial. Dados de contexto adicionais podem ser passados para a solicitação e, se especificados nas regras de negócios, serão incluídos nos dados para tomar a decisão.

Os aplicativos podem obter melhor desempenho, solicitando uma decisão de até 30 atividades de uma só vez. Os URIs das atividades são passados na mesma solicitação. A REST API é síncrona e retornará as opções propostas para todas essas atividades ou a opção de fallback se nenhuma opção de personalização atender às restrições.

É possível que duas atividades diferentes tenham a mesma opção que a &quot;melhor&quot;. Para evitar a repetição de uma experiência composta, por padrão, [!DNL Decisioning Service] as taxas de bits entre as atividades referenciadas na mesma solicitação. Arbitragem significa que, para cada uma das atividades, as suas opções de nível N são consideradas, mas nenhuma opção será proposta mais de uma vez entre essas atividades. Se duas atividades tiverem a mesma opção de primeira categoria, uma delas será selecionada para usar a segunda melhor opção ou a terceira melhor e assim por diante. Essas regras de eliminação de duplicação tentam evitar que qualquer uma das atividades use sua opção de fallback.

O pedido de decisão contém os argumentos que fundamentam um pedido POST. O corpo é formatado como valor `Content-Type` de cabeçalho JSON `application/vnd.adobe.xdm+json; schema="{REQUEST_SCHEMA_AND_VERSION}"`

O schema e a versão de solicitação suportados no momento são `https://ns.adobe.com/experience/offer-management/decision-request;version=0.9`. No futuro, schemas ou versões de solicitação adicionais serão fornecidos.

**Solicitação**

```shell
curl -X POST {DECISION_SERVICE_ENDPOINT_PATH}/{CONTAINER_ID}/decisions \
  -H 'Accept: application/json, application/problem+json \
  -H '
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'x-request-id: {NEW_UUID}' \
  -d '{
  "xdm:dryRun": {DRY_RUN_TRUE_FALSE},
  "xdm:validateContextData": {VALIDATE_CONTEXT_DATA_TRUE_FALSE},

  "xdm:offerActivities":[
    {
      "xdm:offerActivity": "{ACTIVITY_URI_1}"
    },
  ],
  "xdm:identityMap":{
    "{PROFILE_ID_NAMESPACE_CODE}":[
      {
        "xdm:id":"{PROFILE_ID}"
      }
    ]
  },
  "xdm:profileModel":"{PROFILE_MODEL}",
  "xdm:contextData": [
    {
      "@type": "{CONTEXT_DATASSCHEMA_ID}"
      "xdm:data": { JSON PROPERTIES OF CONTEXT ENTITY }
    }
  ] ,
  "xdm:allowDuplicatePropositions": {
    "xdm:acrossActivities": {DUPLICATE_OFFER_IDS_OF_TRUE_FALSE},
  }
}’
```

- **`xdm:dryRun`** - Quando o valor desta propriedade opcional for definido como true, o pedido de decisão obedecerá a restrições de limitação, mas não determinará efetivamente esses contadores, é de esperar que o chamador nunca tencione apresentar a proposta ao perfil. O não [!DNL Decisioning Service] registrará a proposta como um evento de decisão XDM oficial e ela não aparecerá nos conjuntos de dados do relatórios. O valor padrão desta propriedade é falso e quando a propriedade é omitida a decisão não é considerada uma execução de teste e, portanto, deve ser apresentada ao usuário final.
- **`xdm:validateContextData`** - Essa propriedade opcional ativa ou desativa a validação dos dados de contexto. Se a validação estiver ativada, para cada item de dados de contexto fornecido, o schema (com base no `@type` campo) será obtido do registro XDM e o `xdm:data` objeto será validado em relação a ele.

A solicitação por esse schema contém uma matriz de URIs que fazem referência a atividades de oferta, uma identidade de perfil e uma matriz de itens de dados de contexto:

- **`xdm:offerActivities`** - Essa propriedade obrigatória é uma matriz de objetos em que cada item contém dados sobre a atividade da oferta. A atividade de oferta tem as seguintes propriedades:
   - **`xdm:offerActivity`** - O identificador exclusivo (URI) da atividade. Esse é o valor da propriedade da `@id` atividade da oferta.
- **`xdm:identityMap`** - Uma propriedade obrigatória que contém um objeto JSON que está em conformidade com o schema XDM `https://ns.adobe.com/xdm/context/identitymap`. A propriedade define um mapa no qual a chave é um código de namespace de identidade e o valor é uma lista de identificadores de usuário final em determinada namespace. Se m.
- **`xdm:contextData`** - Uma propriedade opcional que contém itens que são descritos por uma referência ao seu schema. Cada item de dados de contexto na matriz deve ter as seguintes propriedades:
   - **`@type`** - Uma propriedade obrigatória que faz referência ao schema XDM do objeto neste item.
   - **`xdm:data`** - Uma propriedade obrigatória que contém as propriedades de objetos de acordo com o schema XDM fornecido na `@type` propriedade.

## Dados de contexto dinâmicos em solicitações de decisão

A seção anterior indicou como os objetos XDM podem ser passados para uma solicitação de decisão. A seguir está um exemplo dessa matriz de objetos de contexto:

```json
"xdm:contextData": [
  {
    "@type":" https://ns.adobe.com/{TENANT_ID_OF_ORG}/schemas/{NUMERIC_SCHEMA_ID};version=1",
    "xdm:data":{ 
      "{TENANT_ID_OF_ORG}": {
        "productDetails":{ 
          "xdm:gender":      "unisex",
          "xdm:fabrication": "leather",
          "xdm:category":    "wallets",
        }
      }
    }
  }
]
```

O schema deve ter sido construído pela sua organização. Para saber mais sobre como construir schemas, consulte o Tutorial [do Editor de](../../xdm/tutorials/create-schema-ui.md)Schemas. Seu schema estará em uma namespace `https://ns.adobe.com/{TENANT_ID}/schemas`.

O guia [do desenvolvedor da API de Registro de](../../xdm/tutorials/create-schema-api.md) Schemas explica como os schemas podem ser acessados de forma programática e como um desenvolvedor obtém a ID do locatário e o identificador numérico do schema. O número da versão é obrigatório e também é fornecido pelas APIs do Registro do schema.

Um schema definido por uma organização normalmente terá uma propriedade raiz chamada `_{TENANT_ID}`, também chamada de sequência de namespace do locatário.
Observe que as propriedades usadas de um componente de schema global, como _`https://ns.adobe.com/xdm/context/product` , têm um prefixo de namespace `xdm:`. Nesse caso, a propriedade definida pela organização `productDetails` foi construída com esse tipo de dados. Embora as propriedades do locatário estejam aninhadas em uma propriedade nomeada após a namespace do locatário, os tipos de dados que estão globalmente disponíveis usam o prefixo reservado `xdm:` para evitar colisões de nomes de propriedades.

Vários objetos de dados podem ser listados na `xdm:contextData` propriedade. Cada objeto deve identificar seu tipo por meio da `@type` propriedade.
Os valores dos objetos de dados de contexto estão disponíveis para serem usados nas expressões PQL, por exemplo, na condição de uma regra de elegibilidade. O objeto de dados de contexto deve ser abordado por meio da expressão de referência de caminho especial `@{schemaId}`. As expressões que seguem essa expressão de referência são expressões de caminho comuns que acessam as propriedades do objeto de dados:

```json
{
  "xdm:name": "Eligible for a free gender-specific item of interest",
  "xdm:condition": {
    "xdm:value":
      "gender in (\"female\",\"non-specific\")  
       and (
         select p from
           @{https://ns.adobe.com/{TENANT_ID}/schemas/{NUMERIC_SCHEMA_ID}}._{TENANT_ID}
         select e from xEvent 
            where e.type = \"productSearch\" 
              and e.category = p.category 
              and p.gender in (\"female\",\"unisex\")
       )",
    "xdm:format": "pql/text",
    "xdm:type": "PQL"
  }
}
```

No exemplo acima, a variável `p` está repetindo sobre a matriz de objetos que foram marcados com o `@type` = `https://ns.adobe.com/{TENANT_ID}/schemas/{NUMERIC_SCHEMA_ID}}`.

Observe que a sintaxe PQL não usa prefixos em nomes de propriedades. As propriedades globais, por padrão, são simplesmente referenciadas sem o `xdm:` prefixo. As propriedades que sua organização define são aninhadas dentro de uma propriedade **adicional** chamada após a namespace do locatário (no exemplo indicado pela variável `{TENANT_ID}`). Para poder fazer referência direta às propriedades definidas pelo cliente, a variável `p` é vinculada ao resultado do caminho que faz referência à propriedade de aninhamento adicional.

## Utilização de registros de perfis

Todos os registros de entidades de evento de perfis e experiências já são gerenciados na loja de perfis. Ao passar uma ou mais identidades de perfil para o pedido, o perfil dessas identidades será identificado e procurado da loja. Os dados são então automaticamente disponibilizados para as regras e modelos de decisão avaliados pela estratégia de decisão.

Para recuperar os registros de perfil e experiência, a política de mesclagem padrão é aplicada.
Observe que, depois de fazer upload dos registros do perfil para o [!DNL Platform] datalake, há um pequeno atraso até que os registros do perfil possam ser pesquisados. O mesmo vale para a assimilação de registros de perfis e experiências por meio das APIs de transmissão, somente após alguns segundos os dados estarão disponíveis para avaliar as regras de decisão que avaliam os dados de perfis e eventos de experiência.