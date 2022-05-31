---
keywords: Experience Platform, home, tópicos populares, preparação de dados, Preparação de dados, transmissão, upsert, atualização de fluxo
title: Enviar Atualizações Parciais De Linha Para O Serviço De Perfil Usando A Preparação De Dados
description: Este documento fornece informações sobre como enviar atualizações de linha parciais ao Serviço de perfil usando a Preparação de dados.
exl-id: f9f9e855-0f72-4555-a4c5-598818fc01c2
source-git-commit: 93c95fce45dc034c0b9c53d9893a8e38e752ec0f
workflow-type: tm+mt
source-wordcount: '1175'
ht-degree: 0%

---

# Enviar atualizações de linha parciais para o [!DNL Profile Service] usar [!DNL Data Prep]

Streaming de upserts em [!DNL Data Prep] permite enviar atualizações de linha parciais para o [!DNL Profile Service] dados, além de criar e estabelecer novos links de identidade com uma única solicitação de API.

Ao fazer o streaming de upserts, você pode manter o formato de seus dados e, ao mesmo tempo, traduzir esses dados para [!DNL Profile Service] Solicitações de PATCH durante a assimilação. Com base nas entradas fornecidas, [!DNL Data Prep] permite enviar uma única carga da API e traduzir os dados para ambos [!DNL Profile Service] PATCH e [!DNL Identity Service] CRIAR solicitações.

Este documento fornece informações sobre como fazer o stream de ascendentes em [!DNL Data Prep].

## Introdução

Essa visão geral requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Data Prep]](./home.md): [!DNL Data Prep] O permite que os engenheiros de dados mapeiem, transformem e validem dados de e para o Experience Data Model (XDM).
* [[!DNL Identity Service]](../identity-service/home.md): Obtenha uma melhor visão de clientes individuais e seu comportamento ao unir identidades em dispositivos e sistemas.
* [Perfil do cliente em tempo real](../profile/home.md): Fornece um perfil de cliente unificado em tempo real com base em dados agregados de várias fontes.
* [Fontes](../sources/home.md): O Experience Platform permite que os dados sejam assimilados de várias fontes, fornecendo a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma.

## Use upserts de transmissão em [!DNL Data Prep] {#streaming-upserts-in-data-prep}

>[!NOTE]
>
>As seguintes fontes oferecem suporte para o uso de upserts de transmissão:<ul><li>[[!DNL Amazon Kinesis]](../sources/connectors/cloud-storage/kinesis.md)</li><li>[[!DNL Azure Event Hubs]](../sources/connectors/cloud-storage/eventhub.md)</li><li>[[!DNL HTTP API]](../sources/connectors/streaming/http.md)</li></ul>

### Fluxo de trabalho de alto nível otimiza o fluxo de trabalho

Streaming de upserts em [!DNL Data Prep] funciona da seguinte forma:

* Primeiro, você deve criar e ativar um conjunto de dados para [!DNL Profile] consumo. Consulte o guia sobre [habilitar um conjunto de dados para [!DNL Profile]](../catalog/datasets/enable-for-profile.md) Para mais informações;
* Se novas identidades precisarem ser vinculadas, você também deverá criar um conjunto de dados adicional **com o mesmo schema** como seu [!DNL Profile] Conjunto de dados;
* Depois que seus conjuntos de dados estiverem preparados, você deverá criar um fluxo de dados para mapear sua solicitação de entrada para o [!DNL Profile] Conjunto de dados;
* Em seguida, você deve atualizar a solicitação de entrada para incluir os cabeçalhos necessários. Esses cabeçalhos definem:
   * A operação de dados que precisa ser executada com [!DNL Profile]: `create`, `merge`e `delete`;
   * A operação de identidade opcional a efetuar com [!DNL Identity Service]: `create`.

### Configurar o conjunto de dados de identidade

Se novas identidades precisarem ser vinculadas, você deverá criar e transmitir um conjunto de dados adicional na carga útil recebida. Ao criar um conjunto de dados de identidade, você deve garantir que os seguintes requisitos sejam atendidos:

* O conjunto de dados de identidade deve ter seu esquema associado como [!DNL Profile] conjunto de dados. Uma incompatibilidade de esquemas pode levar a um comportamento inconsistente do sistema;
* No entanto, você deve garantir que o conjunto de dados de identidade seja diferente do [!DNL Profile] conjunto de dados. Se os conjuntos de dados forem iguais, os dados serão substituídos em vez de atualizados;
* Enquanto o conjunto de dados inicial deve ser ativado para [!DNL Profile], o conjunto de dados de identidade **não deve** estar habilitado para [!DNL Profile]. Caso contrário, os dados também serão substituídos em vez de atualizados.

#### Campos obrigatórios nos esquemas associados ao conjunto de dados de identidade {#identity-dataset-required-fileds}

Se o esquema contiver campos obrigatórios, a validação do conjunto de dados deverá ser suprimida para ativar [!DNL Identity Service] para receber apenas as identidades. É possível suprimir a validação aplicando o `disabled` para `acp_validationContext` parâmetro. Veja o exemplo abaixo:

```shell
curl -X POST 'https://platform.adobe.io/data/foundation/catalog/dataSets/62257bef7a75461948ebcaaa' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "tags":{
        "acp_validationContext": ["disabled"]
        }
}'
```

>[!TIP]
>
>Não é necessário fazer nenhuma configuração adicional se o esquema associado ao conjunto de dados de identidade não tiver campos obrigatórios.

## Estrutura de carga de entrada

A seguir, um exemplo de uma estrutura de payload de entrada que estabelece novos links de identidade.

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
| `flowId` | Uma ID exclusiva para identificar um fluxo de dados. Essa ID de fluxo de dados deve corresponder à conexão de origem criada com o [!DNL Amazon Kinesis], [!DNL Azure Event Hubs]ou [!DNL HTTP API]. Esse fluxo de dados também deve ter uma [!DNL Profile]Conjunto de dados habilitado para o Target como o conjunto de dados de destino. **Observação**: A ID do [!DNL Profile]O conjunto de dados de destino habilitado também é usado como `datasetId` parâmetro. |
| `imsOrgId` | A ID que corresponde à organização. |
| `datasetId` | A ID do [!DNL Profile]Conjunto de dados de destino habilitado para o seu fluxo de dados. **Observação**: Essa é a mesma ID da variável [!DNL Profile]ID do conjunto de dados de destino habilitado para o Target encontrada no seu fluxo de dados. |
| `operations` | Esse parâmetro descreve as ações que [!DNL Data Prep] O será baseado na solicitação de entrada. |
| `operations.data` | Define as ações que devem ser executadas em [!DNL Profile Service]. |
| `operations.identity` | Define as operações permitidas nos dados por [!DNL Identity Service]. |
| `operations.identityDatasetId` | (Opcional) A ID do conjunto de dados de identidade que é necessária somente se novas identidades tiverem de ser vinculadas. |

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
| `create` | A única operação permitida para este parâmetro. If `create` é passado como um valor para `operations.identity`, em seguida [!DNL Data Prep] gera uma solicitação de criação de entidade XDM para [!DNL Identity Service]. Se a identidade já existir, ela será ignorada. **Observação:** If `operations.identity` está definida como `create`, em seguida, o `identityDatasetId` também deve ser especificado. A mensagem de criação da entidade XDM gerada internamente por [!DNL Data Prep] será gerado para essa id de conjunto de dados. |

### Carga sem configuração de identidade

Se novas identidades não precisarem ser vinculadas, é possível omitir a variável `identity` e `identityDatasetId` nas operações. Isso envia dados somente para [!DNL Profile Service] e ignora o [!DNL Identity Service]. Consulte a carga abaixo para obter um exemplo:

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

## Passar identidades primárias dinamicamente

Para atualizações do XDM, o esquema deve ser ativado para [!DNL Profile] e contêm uma identidade primária. Você pode especificar a identidade primária de um esquema XDM de duas maneiras:

* Designar um campo estático como a identidade primária no esquema XDM;
* Designe um dos campos de identidade como a identidade primária através do grupo de campos do mapa de identidade no esquema XDM.

### Designar um campo estático como o campo de identidade primário no esquema XDM

No exemplo abaixo, `state`, `homePhone.number` e outros atributos são atualizados com seus respectivos valores fornecidos na variável [!DNL Profile] com a principal identidade de `sampleEmail@gmail.com`. Uma mensagem de atualização de entidade XDM é gerada pelo streaming [!DNL Data Prep] componente. [!DNL Profile Service] em seguida, confirma essa mensagem de atualização do XDM para atualizar o registro do perfil.

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

### Designar um dos campos de identidade como a identidade primária através do grupo de campos do mapa de identidade no esquema XDM

Neste exemplo, o cabeçalho contém a variável `operations` com o `identity` e `identityDatasetId` propriedades. Isso permite que os dados sejam mesclados com [!DNL Profile Service] e também para que as identidades sejam transmitidas para [!DNL Identity Service].

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

## Limitações conhecidas e considerações-chave

A seguir, uma lista de limitações conhecidas a serem consideradas ao fazer o streaming de atualizações com [!DNL Data Prep]:

* O método de atualização de fluxo só deve ser usado ao enviar atualizações de linha parciais para o [!DNL Profile Service]. Atualizações parciais de linha são **not** consumido pelo lago de dados.
* O método streaming upserts não oferece suporte à atualização, substituição e remoção de identidades. Novas identidades são criadas se elas não existirem. Daí o `identity` deve ser sempre definida para criar. Se uma identidade já existir, a operação será inoperante.
* Atualmente, o método de atualização de fluxo suporta apenas atributos primitivos de valor único (como números inteiros, datas, carimbos de data e hora e strings) e objetos. O método de atualização de fluxo não oferece suporte à substituição, anexação ou substituição de atributos de matriz e índices específicos de matriz.

## Próximas etapas

Ao ler este documento, agora você deve entender como fazer o stream de ascendentes no [!DNL Data Prep] para enviar atualizações de linha parciais ao seu [!DNL Profile Service] , enquanto também cria e vincula identidades com uma única solicitação de API. Para obter mais informações sobre outros [!DNL Data Prep] recursos, leia o [[!DNL Data Prep] visão geral](./home.md). Para saber como usar conjuntos de mapeamentos no [!DNL Data Prep] Leia a API [[!DNL Data Prep] guia do desenvolvedor](./api/overview.md).
