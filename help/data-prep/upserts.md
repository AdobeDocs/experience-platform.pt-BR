---
keywords: Experience Platform;início;tópicos populares;preparação de dados;Preparação de dados;streaming;upsert;upsert de streaming
title: Enviar Atualizações Parciais De Linha Para O Serviço De Perfil Usando O Preparo De Dados
description: Este documento fornece informações sobre como enviar atualizações de linhas parciais para o Serviço de perfil usando o Preparo de dados.
exl-id: f9f9e855-0f72-4555-a4c5-598818fc01c2
source-git-commit: d167975c9c7a267f2888153a05c5857748367822
workflow-type: tm+mt
source-wordcount: '1177'
ht-degree: 1%

---

# Enviar atualizações de linhas parciais para [!DNL Profile Service] usar [!DNL Data Prep]

Upserts de transmissão em [!DNL Data Prep] permite enviar atualizações parciais de linha para [!DNL Profile Service] enquanto também cria e estabelece novos links de identidade com uma única solicitação de API.

Ao fazer a transmissão de upserts, você pode reter o formato dos dados enquanto os traduz para [!DNL Profile Service] solicitações PATCH durante a assimilação. Com base nas informações fornecidas, [!DNL Data Prep] permite enviar uma única carga de API e traduzir os dados para ambos [!DNL Profile Service] PATCH e [!DNL Identity Service] CRIAR solicitações.

Este documento fornece informações sobre como fazer stream de upserts no [!DNL Data Prep].

## Introdução

Esta visão geral requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Data Prep]](./home.md): [!DNL Data Prep] O permite que os engenheiros de dados mapeiem, transformem e validem dados de e para o Experience Data Model (XDM).
* [[!DNL Identity Service]](../identity-service/home.md): obtenha uma melhor visualização dos clientes individuais e do comportamento deles ao unir as identidades de vários dispositivos e sistemas.
* [Perfil do cliente em tempo real](../profile/home.md): fornece um perfil de cliente unificado em tempo real com base em dados agregados de várias fontes.
* [Origens](../sources/home.md): o Experience Platform permite que os dados sejam assimilados de várias fontes e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma.

## Usar upserts de transmissão no [!DNL Data Prep] {#streaming-upserts-in-data-prep}

>[!NOTE]
>
>As seguintes fontes oferecem suporte ao uso de upserts de transmissão:<ul><li>[[!DNL Amazon Kinesis]](../sources/connectors/cloud-storage/kinesis.md)</li><li>[[!DNL Azure Event Hubs]](../sources/connectors/cloud-storage/eventhub.md)</li><li>[[!DNL HTTP API]](../sources/connectors/streaming/http.md)</li></ul>

### Streaming substitui o fluxo de trabalho de alto nível

Upserts de transmissão em [!DNL Data Prep] funciona da seguinte forma:

* Primeiro, você deve criar e habilitar um conjunto de dados para [!DNL Profile] consumo. Consulte o guia sobre [habilitar um conjunto de dados para [!DNL Profile]](../catalog/datasets/enable-for-profile.md) para obter mais informações.
* Se novas identidades precisarem ser vinculadas, você também deverá criar um conjunto de dados adicional **com o mesmo esquema** como seu [!DNL Profile] conjunto de dados.
* Depois que os conjuntos de dados forem preparados, você deverá criar um fluxo de dados para mapear a solicitação recebida para o [!DNL Profile] conjunto de dados;
* Em seguida, você deve atualizar a solicitação de entrada para incluir os cabeçalhos necessários. Esses cabeçalhos definem:
   * A operação de dados que precisa ser executada com [!DNL Profile]: `create`, `merge`, e `delete`.
   * A operação de identidade opcional a ser executada com [!DNL Identity Service]: `create`.

### Configurar o conjunto de dados de identidade

Se novas identidades precisarem ser vinculadas, você deverá criar e transmitir um conjunto de dados adicional na carga recebida. Ao criar um conjunto de dados de identidade, você deve garantir que os seguintes requisitos sejam atendidos:

* O conjunto de dados de identidade deve ter seu esquema associado como o [!DNL Profile] conjunto de dados. Uma incompatibilidade de esquemas pode levar a um comportamento inconsistente do sistema.
* No entanto, você deve garantir que o conjunto de dados de identidade seja diferente da variável [!DNL Profile] conjunto de dados. Se os conjuntos de dados forem iguais, os dados serão substituídos em vez de atualizados.
* Embora o conjunto de dados inicial deva ser habilitado para [!DNL Profile], o conjunto de dados de identidade **não deve ser ativado** para [!DNL Profile]. Caso contrário, os dados também serão substituídos em vez de atualizados. No entanto, o conjunto de dados de identidade **deve ser ativado** para [!DNL Identity Service].

#### Campos obrigatórios nos esquemas associados ao conjunto de dados de identidade {#identity-dataset-required-fileds}

Se o esquema contiver campos obrigatórios, a validação do conjunto de dados deverá ser suprimida para habilitar [!DNL Identity Service] para receber apenas as identidades. É possível suprimir a validação aplicando o `disabled` para o `acp_validationContext` parâmetro. Consulte o exemplo abaixo:

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
| `flowId` | Uma ID exclusiva para identificar um fluxo de dados. Essa ID de fluxo de dados deve corresponder à conexão de origem criada com [!DNL Amazon Kinesis], [!DNL Azure Event Hubs]ou [!DNL HTTP API]. Esse fluxo de dados também deve ter uma [!DNL Profile]conjunto de dados habilitado para como o conjunto de dados de destino. **Nota**: A ID do [!DNL Profile]O conjunto de dados de destino habilitado para também é usado como `datasetId` parâmetro. |
| `imsOrgId` | A ID que corresponde à sua organização. |
| `datasetId` | A ID do [!DNL Profile]Conjunto de dados de destino habilitado para do seu fluxo de dados. **Nota**: Essa é a mesma ID da variável [!DNL Profile]ID do conjunto de dados de destino habilitada para foi encontrada em seu fluxo de dados. |
| `operations` | Esse parâmetro descreve as ações que [!DNL Data Prep] terá com base na solicitação recebida. |
| `operations.data` | Define as ações que devem ser executadas em [!DNL Profile Service]. |
| `operations.identity` | Define as operações permitidas nos dados por [!DNL Identity Service]. |
| `operations.identityDatasetId` | (Opcional) A ID do conjunto de dados de identidade que será necessária somente se novas identidades precisarem ser vinculadas. |

#### Operações suportadas

As seguintes operações são suportadas pela [!DNL Profile Service]:

| Operações | Descrição |
| --- | --- | 
| `create` | A operação padrão. Isso gera um método de criação de entidade XDM para [!DNL Profile Service]. |
| `merge` | Isso gera um método de atualização de entidade XDM para [!DNL Profile Service]. |
| `delete` | Isso gera um método de exclusão de entidade XDM para [!DNL Profile Service] e remove permanentemente os dados do [!DNL Profile Store]. |

As seguintes operações são suportadas pela [!DNL Identity Service]:

| Operações | Descrições |
| --- | --- |
| `create` | A única operação permitida para este parâmetro. Se `create` é transmitido como um valor para `operations.identity`, depois [!DNL Data Prep] gera uma solicitação de criação de entidade XDM para [!DNL Identity Service]. Se a identidade já existir, ela será ignorada. **Nota:** Se `operations.identity` está definida como `create`, depois o `identityDatasetId` também deve ser especificado. A entidade XDM cria a mensagem gerada internamente pelo [!DNL Data Prep] O componente será gerado para esta id de conjunto de dados. |

### Carga sem configuração de identidade

Se novas identidades não precisarem ser vinculadas, você poderá omitir a variável `identity` e `identityDatasetId` nas operações. Isso envia dados somente para o [!DNL Profile Service] e ignora o [!DNL Identity Service]. Consulte a carga abaixo para obter um exemplo:

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

Para atualizações do XDM, o esquema deve ser ativado para [!DNL Profile] e contêm uma identidade principal. Você pode especificar a identidade principal de um esquema XDM de duas maneiras:

* Designar um campo estático como a identidade principal no esquema XDM;
* Designe um dos campos de identidade como a identidade primária por meio do grupo de campos do mapa de identidade no esquema XDM.

### Designar um campo estático como o campo de identidade principal no esquema XDM

No exemplo abaixo, `state`, `homePhone.number` e outros atributos são substituídos por seus respectivos valores na variável [!DNL Profile] com a identidade principal de `sampleEmail@gmail.com`. Uma mensagem de atualização de entidade XDM é gerada pela transmissão [!DNL Data Prep] componente. [!DNL Profile Service] em seguida, confirma que a mensagem de atualização do XDM deve substituir o registro do perfil.

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

Neste exemplo, o cabeçalho contém a variável `operations` atributo com o `identity` e `identityDatasetId` propriedades. Isso permite que os dados sejam mesclados com [!DNL Profile Service] e também para que as identidades sejam passadas para [!DNL Identity Service].

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

A seguir, é apresentada uma lista de limitações conhecidas a serem consideradas ao transmitir upserts com [!DNL Data Prep]:

* O método de streaming upserts deve ser usado somente ao enviar atualizações de linhas parciais para o [!DNL Profile Service]. As atualizações de linha parcial são **não** consumido pelo data lake.
* O método de upserts de transmissão não oferece suporte à atualização, substituição e remoção de identidades. Novas identidades serão criadas se não existirem. Por conseguinte, a `identity` a operação deve ser sempre definida como criar. Se uma identidade já existir, a operação será no-op.
* O método de upserts de streaming não oferece suporte no momento [Adobe Experience Platform Web SDK](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=pt-BR) e [Adobe Experience Platform Mobile SDK](https://aep-sdks.gitbook.io/docs/).

## Próximas etapas

Após a leitura deste documento, você deve entender como fazer streaming de upserts no [!DNL Data Prep] para enviar atualizações parciais de linha ao seu [!DNL Profile Service] ao mesmo tempo em que cria e vincula identidades com uma única solicitação de API. Para obter mais informações sobre outras [!DNL Data Prep] recursos, leia os [[!DNL Data Prep] visão geral](./home.md). Para saber como usar conjuntos de mapeamento na [!DNL Data Prep] API, leia as [[!DNL Data Prep] guia do desenvolvedor](./api/overview.md).
