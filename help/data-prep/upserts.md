---
keywords: Experience Platform;página inicial;tópicos populares;preparação de dados;Preparação de dados;streaming;substituição;substituição de streaming
title: Enviar Atualizações Parciais De Linha Ao Perfil Do Cliente Em Tempo Real Usando O Preparo De Dados
description: Saiba como enviar atualizações de linhas parciais para o Perfil do cliente em tempo real usando o Preparo de dados.
exl-id: f9f9e855-0f72-4555-a4c5-598818fc01c2
source-git-commit: f988d7665a40b589ca281d439b6fca508f23cd03
workflow-type: tm+mt
source-wordcount: '1363'
ht-degree: 0%

---

# Enviar atualizações parciais de linha para [!DNL Real-Time Customer Profile] usando [!DNL Data Prep]

>[!IMPORTANT]
>
>* A assimilação de mensagens de atualização de entidade do Experience Data Model (XDM) (com operações JSON PATCH) para atualizações de perfil por meio da entrada do DCS foi descontinuada. Siga as etapas descritas neste guia como uma alternativa.
>
>* Você também pode usar a fonte da API HTTP para [assimilar dados brutos na entrada do DCS](../sources/tutorials/api/create/streaming/http.md#sending-messages-to-an-authenticated-streaming-connection) e especificar os mapeamentos de dados necessários para transformar seus dados em mensagens compatíveis com XDM para atualizações de Perfil.
>
>* Ao usar matrizes em upserts de transmissão, você deve usar explicitamente `upsert_array_append` ou `upsert_array_replace` para definir a intenção clara da operação. Você poderá receber erros se essas funções estiverem ausentes.

Use upserts de streaming em [!DNL Data Prep] para enviar atualizações parciais de linha aos dados de [!DNL Real-Time Customer Profile], ao mesmo tempo em que cria e estabelece novos links de identidade com uma única solicitação de API.

Ao fazer a transmissão de upserts, você pode reter o formato dos dados enquanto traduz esses dados para [!DNL Real-Time Customer Profile] solicitações do PATCH durante a assimilação. Com base nas entradas que você fornece, o [!DNL Data Prep] permite enviar uma única carga de API e traduzir os dados para as solicitações de [!DNL Real-Time Customer Profile] PATCH e [!DNL Identity Service] CREATE.

[!DNL Data Prep] usa parâmetros de cabeçalho para distinguir entre inserções e substituições. Todas as linhas que usam sobreposições devem ter um cabeçalho. É possível usar sobreposições com ou sem descritores de identidade. Se você estiver usando sobreposições com identidades, siga as etapas de configuração descritas na seção em [configurando o conjunto de dados de identidade](#configure-the-identity-dataset). Se estiver usando upserts sem identidades, não será necessário fornecer configurações de identidade na solicitação. Leia a seção sobre [upserts de streaming sem identidades](#payload-without-identity-configuration) para obter mais informações.

>[!NOTE]
>
>Para aproveitar a funcionalidade de substituição, é recomendável desativar as configurações compatíveis com XDM durante a assimilação de dados e remapear a carga de entrada usando o [Mapeador de Preparo de Dados](./ui/mapping.md).

Este documento fornece informações sobre como fazer streaming de upserts no [!DNL Data Prep].

## Introdução

Esta visão geral requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Data Prep]](./home.md): [!DNL Data Prep] permite que os engenheiros de dados mapeiem, transformem e validem dados de e para o Experience Data Model (XDM).
* [[!DNL Identity Service]](../identity-service/home.md): obtenha uma melhor visão de clientes individuais e de seu comportamento ao unir as identidades de vários dispositivos e sistemas.
* [Perfil do cliente em tempo real](../profile/home.md): fornece um perfil de cliente unificado em tempo real com base em dados agregados de várias fontes.
* [Fontes](../sources/home.md): o Experience Platform permite a assimilação de dados de várias fontes, ao mesmo tempo em que fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços do Experience Platform.

## Usar upserts de streaming em [!DNL Data Prep] {#streaming-upserts-in-data-prep}

>[!NOTE]
>
>As seguintes fontes oferecem suporte ao uso de upserts de transmissão:<ul><li>[[!DNL Amazon Kinesis]](../sources/connectors/cloud-storage/kinesis.md)</li><li>[[!DNL Azure Event Hubs]](../sources/connectors/cloud-storage/eventhub.md)</li><li>[[!DNL HTTP API]](../sources/connectors/streaming/http.md)</li></ul>

### Streaming substitui o fluxo de trabalho de alto nível

Os upserts de streaming em [!DNL Data Prep] funcionam da seguinte forma:

* Primeiro, você deve criar e habilitar um conjunto de dados para consumo de [!DNL Profile]. Consulte o manual sobre [habilitação de um conjunto de dados para [!DNL Profile]](../catalog/datasets/enable-for-profile.md) para obter mais informações.
* Se novas identidades precisarem ser vinculadas, você também deverá criar um conjunto de dados adicional **com o mesmo esquema** do seu conjunto de dados [!DNL Profile].
* Depois que os conjuntos de dados forem preparados, você deverá criar um fluxo de dados para mapear a solicitação recebida para o conjunto de dados [!DNL Profile].
* Em seguida, você deve atualizar a solicitação de entrada para incluir os cabeçalhos necessários. Esses cabeçalhos definem:
   * A operação de dados que precisa ser executada com [!DNL Profile]: `create`, `merge` e `delete`.
   * A operação de identidade opcional a ser executada com [!DNL Identity Service]: `create`.

### Configurar o conjunto de dados de identidade {#configure-the-identity-dataset}

Se novas identidades precisarem ser vinculadas, você deverá criar e transmitir um conjunto de dados adicional na carga recebida. Ao criar um conjunto de dados de identidade, você deve garantir que os seguintes requisitos sejam atendidos:

* O conjunto de dados de identidade deve ter seu esquema associado como o conjunto de dados [!DNL Profile]. Uma incompatibilidade de esquemas pode levar a um comportamento inconsistente do sistema.
* No entanto, você deve garantir que o conjunto de dados de identidade seja diferente do conjunto de dados [!DNL Profile]. Se os conjuntos de dados forem iguais, os dados serão substituídos em vez de atualizados.
* Embora o conjunto de dados inicial deva ser habilitado para [!DNL Profile], o conjunto de dados de identidade **não deve ser habilitado** para [!DNL Profile]. Caso contrário, os dados também serão substituídos em vez de atualizados. No entanto, o conjunto de dados de identidade **deve ser habilitado** para [!DNL Identity Service].

#### Campos obrigatórios nos esquemas associados ao conjunto de dados de identidade {#identity-dataset-required-fileds}

Se o esquema contiver campos obrigatórios, a validação do conjunto de dados deverá ser suprimida para permitir que [!DNL Identity Service] receba apenas as identidades. Você pode suprimir a validação aplicando o valor `disabled` ao parâmetro `acp_validationContext`. Consulte o exemplo abaixo:

```shell
curl -X POST 'https://platform.adobe.io/data/foundation/catalog/dataSets/62257bef7a75461948ebcaaa' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "tags": {
        "acp_validationContext": [
            "disabled"
        ],
        "unifiedProfile": [
            "enabled:false"
        ],
        "unifiedIdentity": [
            "enabled:true"
        ]
    }
}'
```

>[!TIP]
>
>Não é necessário fazer qualquer configuração adicional se o esquema associado ao conjunto de dados de identidade não tiver campos obrigatórios.

## Estrutura de carga de entrada

A seguir é mostrado um exemplo de uma estrutura de payload de entrada que estabelece novos links de identidade.

### Carga com configuração de identidade

```shell
{
  "header": {
    "flowId": "923e2ac3-3869-46ec-9e6f-7012c4e23f69",
    "imsOrgId": "{ORG_ID}",
    "datasetId": "621fc19ab33d941949af16c8",
    "operations": {
        "data": "create" (default)/"merge"/"delete",
        "identity": "create",
        "identityDatasetId": "621fc19ab33d941949af16d9"
    }
  }
... //The raw data attributes are included here as the key/value pairs of the "body" property.
}
```

| Parâmetro | Descrição |
| --- | --- |
| `flowId` | Uma ID exclusiva para identificar um fluxo de dados. Esta ID de fluxo de dados deve corresponder à conexão de origem criada com [!DNL Amazon Kinesis], [!DNL Azure Event Hubs] ou [!DNL HTTP API]. Esse fluxo de dados também deve ter um conjunto de dados habilitado para [!DNL Profile] como o conjunto de dados de destino. **Observação**: a ID do conjunto de dados de destino habilitado para [!DNL Profile] também é usada como seu parâmetro `datasetId`. |
| `imsOrgId` | A ID que corresponde à sua organização. |
| `datasetId` | A ID do conjunto de dados de destino habilitado para [!DNL Profile] do seu fluxo de dados. **Observação**: esta é a mesma ID que a ID do conjunto de dados de destino habilitado para [!DNL Profile] encontrada em seu fluxo de dados. |
| `operations` | Este parâmetro descreve as ações que [!DNL Data Prep] executará com base na solicitação recebida. |
| `operations.data` | Define as ações que devem ser executadas em [!DNL Real-Time Customer Profile]. |
| `operations.identity` | Define as operações permitidas nos dados por [!DNL Identity Service]. |
| `operations.identityDatasetId` | (Opcional) A ID do conjunto de dados de identidade que será necessária somente se novas identidades precisarem ser vinculadas. |

#### Operações suportadas

As seguintes operações são suportadas por [!DNL Real-Time Customer Profile]:

| Operações | Descrição |
| --- | --- | 
| `create` | A operação padrão. Isso gera um método de criação de entidade XDM para [!DNL Real-Time Customer Profile]. |
| `merge` | Isso gera um método de atualização de entidade XDM para [!DNL Real-Time Customer Profile]. |
| `delete` | Isso gera um método de exclusão de entidade XDM para [!DNL Real-Time Customer Profile] e remove permanentemente os dados de [!DNL Profile store]. |

As seguintes operações são suportadas por [!DNL Identity Service]:

| Operações | Descrições |
| --- | --- |
| `create` | A única operação permitida para este parâmetro. Se `create` for passado como valor para `operations.identity`, [!DNL Data Prep] gerará uma solicitação de criação de entidade XDM para [!DNL Identity Service]. Se a identidade já existir, ela será ignorada. **Observação:** se `operations.identity` estiver definido como `create`, então `identityDatasetId` também deve ser especificado. A mensagem de criação da entidade XDM gerada internamente pelo componente [!DNL Data Prep] será gerada para esta ID de conjunto de dados. |

### Carga sem configuração de identidade {#payload-without-identity-configuration}

Se novas identidades não precisarem ser vinculadas, você poderá omitir os parâmetros `identity` e `identityDatasetId` nas operações. Isso envia dados somente para [!DNL Real-Time Customer Profile] e ignora o [!DNL Identity Service]. Consulte a carga abaixo para obter um exemplo:

```shell
{
  "header": {
    "flowId": "923e2ac3-3869-46ec-9e6f-7012c4e23f69",
    "imsOrgId": "{ORG_ID}",
    "datasetId": "621fc19ab33d941949af16c8",
    "operations": {
        "data": "create"/"merge"/"delete",
    }
  }
... //The raw data attributes are included here as the key/value pairs of the "body" property.
}
```

## Transmitir dinamicamente as identidades principais

Para atualizações XDM, o esquema deve ser habilitado para [!DNL Profile] e conter uma identidade primária. Você pode especificar a identidade principal de um esquema XDM de duas maneiras:

* Designar um campo estático como a identidade principal no esquema XDM;
* Designe um dos campos de identidade como a identidade primária por meio do grupo de campos do mapa de identidade no esquema XDM.

### Designar um campo estático como o campo de identidade principal no esquema XDM

No exemplo abaixo, `state`, `homePhone.number` e outros atributos são substituídos por seus respectivos valores fornecidos na [!DNL Profile] com a identidade primária de `sampleEmail@gmail.com`. Uma mensagem de atualização de entidade XDM é gerada pelo componente de streaming [!DNL Data Prep]. [!DNL Real-Time Customer Profile] então confirma que a mensagem de atualização do XDM deve substituir o registro do perfil.

>[!NOTE]
>
>Neste exemplo, as identidades não serão vinculadas, pois não há operações definidas para a identidade.

```shell
curl -X POST 'https://dcs.adobedc.net/collection/9aba816d350a69c4abbd283eb5818ec3583275ffce4880ffc482be5a9d810c4b' \
  -H 'Content-Type: application/json' \
  -H 'x-adobe-flow-id: d5262d48-0f47-4949-be6d-795f06933527' \
  -d '{
    "header": {
        "flowId" : "d5262d48-0f47-4949-be6d-795f06933527",
        "imsOrgId": "{ORG_ID}",
        "datasetId": "62259f817f62d71947929a7b",
        "operations": {
         "data": "create"
     }
    },
    {
        "body": {
        "homeAddress": {
            "country": "US",
            "state": "GA",
            "region": "va7"
        },
        "homePhone": {
            "number": "123.456.799"
        },
        "identityMap": {
            "Email": [{
                "id": "sampleEmail@gmail.com",
                "primary": true
            }]
        },
      "personalEmail": {
            "address": "sampleEmail@gmail.com",
            "primary": true
       },
      "personID": "346576345",
      "_id": "346576345",
      "timestamp": "2021-05-05T17:51:45.1880+02",
      "workEmail": "sampleWorkEmail@gmail.com"
  }
}'
```

### Designar um dos campos de identidade como a identidade primária por meio do grupo de campos do mapa de identidade no esquema XDM

Neste exemplo, o cabeçalho contém o atributo `operations` com as propriedades `identity` e `identityDatasetId`. Isso permite que os dados sejam mesclados com [!DNL Real-Time Customer Profile] e também que as identidades sejam passadas para [!DNL Identity Service].

```shell
curl -X POST 'https://dcs.adobedc.net/collection/9aba816d350a69c4abbd283eb5818ec3583275ffce4880ffc482be5a9d810c4b' \
  -H 'Content-Type: application/json' \
  -H 'x-adobe-flow-id: d5262d48-0f47-4949-be6d-795f06933527' \
  -d '{
    "header": {
        "flowId" : "d5262d48-0f47-4949-be6d-795f06933527",
        "imsOrgId": "{ORG_ID}",
        "datasetId": "62259f817f62d71947929a7b",
        "operations": {          
            "data": "merge",
            "identity": "create",
            "identityDatasetId": "6254a93b851ecd194b64af9e"
      }
    },
    {        
       "body": {
        "homeAddress": {
            "country": "US",
            "state": "GA",
            "region": "va7"
        },
        "homePhone": {
            "number": "123.456.799"
        },
        "identityMap": {
            "Email": [{
                "id": "sampleEmail@gmail.com",
                "primary": true
            }]
        },
      "personalEmail": {
            "address": "sampleEmail@gmail.com",
            "primary": true
       },
      "personID": "346576345",
      "_id": "346576345",
      "timestamp": "2021-05-05T17:51:45.1880+02",
      "workEmail": "sampleWorkEmail@gmail.com"
  }
 }'
```

## Limitações conhecidas e principais considerações

A seguir, uma lista de limitações conhecidas a serem consideradas ao transmitir upserts com [!DNL Data Prep]:

* O método de streaming upserts deve ser usado somente ao enviar atualizações de linhas parciais para [!DNL Real-Time Customer Profile]. As atualizações de linha parciais são **não** consumidas pelo data lake.
* O método de upserts de transmissão não oferece suporte à atualização, substituição e remoção de identidades. Novas identidades serão criadas se não existirem. Portanto, a operação `identity` sempre deve ser definida como criar. Se uma identidade já existir, a operação será no-op.
* Atualmente, o método de upserts de streaming não oferece suporte ao [Adobe Experience Platform Web SDK](/help/collection/js/js-overview.md) ou ao [Adobe Experience Platform Mobile SDK](https://developer.adobe.com/client-sdks/documentation/).

## Próximas etapas

Após a leitura deste documento, você deve entender como fazer streaming de upserts no [!DNL Data Prep] para enviar atualizações parciais de linhas aos seus dados do [!DNL Real-Time Customer Profile], além de criar e vincular identidades com uma única solicitação de API. Para obter mais informações sobre outros recursos do [!DNL Data Prep], leia a [[!DNL Data Prep] visão geral](./home.md). Para saber como usar conjuntos de mapeamento na API [!DNL Data Prep], leia o [[!DNL Data Prep] guia do desenvolvedor](./api/overview.md).
