---
title: Conectar o Capilar ao Experience Platform usando a API do Serviço de fluxo
description: Saiba como conectar o Capilary ao Experience Platform usando APIs.
badge: Beta
exl-id: 763792d0-d5dc-40ac-b86a-6a0d26463b71
source-git-commit: 91d6206c6ce387fde365fa72dc79ca79fc0e46fa
workflow-type: tm+mt
source-wordcount: '1150'
ht-degree: 2%

---

# Conectar o [!DNL Capillary Streaming Events] ao Experience Platform usando a API [!DNL Flow Service]

>[!AVAILABILITY]
>
>A origem [!DNL Capillary Streaming Events] está na versão beta. Leia os [termos e condições](../../../../home.md#terms-and-conditions) na visão geral das fontes para obter mais informações sobre como usar fontes com rótulo beta.

Leia este manual para saber como usar a [!DNL Capillary Streaming Events] e a [[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/) para transmitir dados da sua conta do [!DNL Capillary] para a Adobe Experience Platform.

## Introdução

Este guia requer uma compreensão funcional dos seguintes componentes do Experience Platform:

* [Fontes](../../../../home.md): o Experience Platform permite a assimilação de dados de várias fontes, ao mesmo tempo em que fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços do Experience Platform.
* [Sandboxes](../../../../../sandboxes/home.md): a Experience Platform fornece sandboxes virtuais que particionam uma única instância do Experience Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

### Coletar credenciais necessárias

Leia a [[!DNL Capillary Streaming Events] visão geral](../../../../connectors/loyalty/capillary.md) para obter informações sobre autenticação.

### Uso de APIs do Experience Platform

Leia o manual sobre [introdução às APIs do Experience Platform](../../../../../landing/api-guide.md) para obter informações sobre como fazer chamadas com êxito para as APIs do Experience Platform.

>[!BEGINSHADEBOX]

## Lista de verificação do processo do desenvolvedor

1. Crie ou escolha seu **esquema do Experience Data Model (XDM)** de destino usando o Registro de Esquemas. Use este esquema XDM para **criar um conjunto de dados** no Serviço de Catálogo.
2. Crie uma **conexão básica** para armazenar suas credenciais do [!DNL Capillary].
3. Crie uma **conexão de origem** para associar a seu `baseConnectionId`.
4. Crie uma **conexão de destino** para garantir que seus dados cheguem ao data lake.
5. Use o Preparo de Dados para criar mapeamentos que mapeiem seus campos de origem [!DNL Capillary] para os campos XDM corretos.
6. Criar um fluxo de dados usando `sourceConnectionId`, `targetConnectionId` e `mappingID`
7. Teste com eventos de perfil/transação de amostra única para verificar seu fluxo de dados.

>[!ENDSHADEBOX]

## Criar uma conexão básica {#base-connection}

Uma conexão base retém credenciais e detalhes de conexão. Para criar uma conexão base para [!DNL Capillary], faça uma solicitação POST para o ponto de extremidade `/connections` da API [!DNL Flow Service] e forneça suas credenciais [!DNL Capillary] no corpo da solicitação.

**Formato da API**

```https
POST /connections
```

**Solicitação**

A solicitação a seguir cria uma conexão base para [!DNL Capillary]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Capillary base connection",
    "description": "Base connection to authenticate the [!DNL Capillary] source.",
    "connectionSpec": {
      "id": "6360f136-5980-4111-8bdf-15d29eab3b5a",
      "version": "1.0"
    },
    "auth": {
      "specName": "OAuth generic-rest-connector",
      "params": {
        "clientId": "{CLIENT_ID}",
        "clientSecret": "{CLIENT_SECRET}",
        "accessToken": "{ACCESS_TOKEN}"
      }
    }
  }'
```

**Resposta**

```
A successful response returns the newly created base connection, including its unique connection identifier (id). This ID is required to explore your source's file structure and contents in the next step.

{
     "id": "70383d02-2777-4be7-a309-9dd6eea1b46d",
     "etag": "\"d64c8298-add4-4667-9a49-28195b2e2a84\""
}
```

### Criar uma conexão de origem

Para criar uma conexão de origem, faça uma solicitação POST para o ponto de extremidade `/sourceConnections` enquanto fornece a ID da conexão base.

**Formato da API**

```http
POST /flowservice/sourceConnections
```

**Solicitação**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
      "name": "Capillary Streaming",
      "description": "Capillary Streaming",
      "baseConnectionId": "70383d02-2777-4be7-a309-9dd6eea1b46d",
      "connectionSpec": {
          "id": "6360f136-5980-4111-8bdf-15d29eab3b5a",
          "version": "1.0"
      }
    }'
```

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 201 com detalhes da conexão de origem recém-criada, incluindo seu identificador exclusivo (`id`).

```json
{
  "id": "34ece231-294d-416c-ad2a-5a5dfb2bc69f",
  "etag": "\"d505125b-0000-0200-0000-637eb7790000\""
}
```

### Configurações de esquema

>[!BEGINTABS]

>[!TAB Assimilação de perfil]

Os perfis contêm atributos de identidade e fidelidade. Visualize a carga a seguir para obter um exemplo com base no esquema de perfil [!DNL Capillary]. Você pode configurar e mapear esse esquema para um Perfil individual XDM.

**Solicitação**

```json
{
  "identityMap": {
    "email": [
      {
        "authenticatedState": "ambiguous",
        "id": "john.doe@capillarytech.com",
        "primary": true
      }
    ]
  },
  "loyalty": {
    "tier": "gold",
    "points": 1250,
    "lifetimePoints": 122,
    "expiredPoints": 12,
    "pointsRedeemed": 500,
    "program": "loyalty program name",
    "status": "active"
  }
}
```

**Resposta**

```json
{
  "id": "8c19f1c3-4b91-47cd-8cb5-b152a93f7349",
  "status": "success",
  "message": "Profile record ingested successfully"
}
```

>[!TAB Assimilação de transação]

As transações capturam atividades comerciais. Veja a seguinte carga para um exemplo baseado no esquema de eventos [!DNL Capillary]. Você pode configurar e mapear esse esquema para um Evento de experiência XDM.

**Solicitação**

```json
{
  "_id": "T0001",
  "timestamp": "2025-07-14T12:00:00-06:00",
  "identityMap": {
    "email": [
      {
        "authenticatedState": "ambiguous",
        "id": "john@capillarytech.com",
        "primary": true
      }
    ]
  },
  "commerce": {
    "commerceScope": {
      "storeCode": "HSR"
    },
    "order": {
      "priceTotal": 90
    }
  },
  "productLineItems": [
    {
      "SKU": "sku_01",
      "quantity": 1,
      "priceTotal": 100,
      "name": "Kitkat",
      "discountAmount": 10
    }
  ]
}
```

**Resposta**

```json
{
  "id": "T0001",
  "status": "success",
  "message": "Transaction event ingested successfully"
}
```

>[!ENDTABS]

<!--### Supported Events

The [!DNL Capillary] source supports the following events:

* `pointsIssued`
* `tierDowngraded`
* `tierUpgraded`
* `pointsExpiryChange`
* `pointsExpired`
* `transactionUpdated`
* `customerAdded`
* `tierDowngradeReminder`
* `promotionEarned`
* `pointsExpiryReminder`
* `pointsRedeemed`
* `transactionAdded`
* `tierRenewed`
* `customerUpdated`-->

### Migração de dados históricos

Você pode trazer seus dados históricos de fidelidade e transação para a Experience Platform. Basta exportar seus dados como arquivos CSV estruturados do [!DNL Capillary], transferi-los com segurança usando o [!DNL SFTP] e assimilá-los em seus conjuntos de dados do Experience Platform. Após a migração inicial, seus dados permanecerão atualizados em tempo real por meio do conector orientado por eventos.

### Criar um esquema XDM de destino {#target-schema}

Um esquema do Experience Data Model (XDM) fornece uma maneira padronizada para organizar e descrever os dados de experiência do cliente no Experience Platform. Para assimilar os dados de origem na Experience Platform, primeiro você deve criar um esquema XDM de destino que defina a estrutura e os tipos de dados que deseja assimilar. Esse esquema serve de blueprint para o conjunto de dados do Experience Platform em que seus dados assimilados residirão.

Um esquema XDM de destino pode ser criado executando uma solicitação POST para a [API do Registro de Esquema](https://developer.adobe.com/experience-platform-apis/references/schema-registry/). Para obter etapas detalhadas sobre como criar um esquema XDM de destino, leia os seguintes guias:

* [Criar um esquema usando a API](../../../../../xdm/api/schemas.md).
* [Criar um esquema usando a interface](../../../../../xdm/tutorials/create-schema-ui.md).

Depois de criado, o esquema XDM de destino `$id` será necessário posteriormente para o conjunto de dados e o mapeamento de destino.

## Criar um conjunto de dados de destino {#target-dataset}

Um conjunto de dados é uma construção de armazenamento e gerenciamento para uma coleção de dados, normalmente estruturada como uma tabela com colunas (esquema) e linhas (campos). Os dados assimilados com sucesso na Experience Platform são armazenados no data lake como conjuntos de dados. Durante essa etapa, você pode criar um novo conjunto de dados ou usar um existente.

Você pode criar um conjunto de dados de destino fazendo uma solicitação POST para a [API de Serviço de Catálogo](https://developer.adobe.com/experience-platform-apis/references/catalog/) e, ao mesmo tempo, fornecendo a ID do esquema de destino na carga. Para obter etapas detalhadas sobre como criar um conjunto de dados de destino, leia o manual sobre [criação de um conjunto de dados usando a API](../../../../../catalog/api/create-dataset.md).


## Criar uma conexão de destino {#target}

Uma conexão de destino representa a conexão com o destino onde os dados assimilados chegam. Para criar uma conexão de destino, você deve fornecer a ID de especificação da conexão fixa associada ao data lake. Esta ID de especificação de conexão é: `c604ff05-7f1a-43c0-8e18-33bf874cb11c`.

**Formato da API**

```http
POST /targetConnections
```

**Solicitação**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Capillary Target Connection",
      "description": "Capillary Target Connection",
      "data": {
          "schema": {
              "id": "https://ns.adobe.com/{TENANT_ID}/schemas/52b59140414aa6a370ef5e21155fd7a686744b8739ecc168",
              "version": "application/vnd.adobe.xed-full+json;version=1"
          }
      },
      "params": {
          "dataSetId": "6889f4f89b982b2b90bc1207"
      },
      "connectionSpec": {
          "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
          "version": "1.0"
      }
    }'
```

### Criar um mapeamento {#mapping}

Em seguida, mapeie os dados de origem para o esquema de destino ao qual o conjunto de dados de destino adere. Para criar um mapeamento, faça uma solicitação POST para o ponto de extremidade `mappingSets` da [[!DNL Data Prep] API](https://developer.adobe.com/experience-platform-apis/references/data-prep/). Inclua a ID do esquema XDM do público-alvo e os detalhes dos conjuntos de mapeamento que deseja criar.

Mapeie os campos Capilar para os campos de esquema XDM correspondentes, da seguinte maneira:

| Esquema de origem | Esquema de destino |
|------------------------------|-------------------------------|
| `identityMap.email.id` | `xdm:identityMap.email[0].id` |
| `loyalty.points` | `xdm:loyalty.points` |
| `loyalty.tier` | `xdm:loyalty.tier` |
| `commerce.order.priceTotal` | `xdm:commerce.order.priceTotal` |
| `productLineItems.SKU` | `xdm:productListItems.SKU` |

>[!TIP]
>
>Você pode baixar os [Eventos e mapeamentos de perfil](../../../../images/tutorials/create/capillary/mappings.zip) para [!DNL Capillary] e [importar os arquivos para o Preparo de Dados](../../../../../data-prep/ui/mapping.md#import-mapping) quando estiver pronto para mapear seus dados.

### Criar um fluxo de dados {#flow}

Após criar a conexão de origem, o mapeamento e a conexão de destino, você pode configurar um fluxo de dados para mover dados do [!DNL Capillary] para o Experience Platform.

Os fluxos de dados típicos incluem:

* **Fluxo de dados de perfil**: assimila dados de perfil [!DNL Capillary] em um conjunto de dados de Perfil Individual XDM.
* **Fluxo de dados de transação**: assimila [!DNL Capillary] dados de transação em um conjunto de dados XDM ExperienceEvent.

**Solicitação**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Capillary dataflow",
    "description": "Capillary → Experience Platform dataflow",
    "flowSpec": {
      "id": "6499120c-0b15-42dc-936e-847ea3c24d72",
      "version": "1.0"
    },
    "sourceConnectionIds": "{SOURCE_CONNECTION_ID}",
    "targetConnectionIds": "{TARGET_CONNECTION_ID}",
    "transformations": [
      {
        "name": "Mapping",
        "params": {
          "mappingId": "{MAPPING_ID}",
          "mappingVersion": "0"
        }
      }
    ],
    "scheduleParams": {
      "startTime": "1625040887",
      "frequency": "minute",
      "interval": 15
    }
  }'
```

>[!NOTE]
>
>`startTime` está em segundos da época UNIX.

**Resposta**

Uma resposta bem-sucedida retorna o fluxo de dados com a ID de fluxo de dados correspondente.

```json
{
  "id": "92f11b8c-0a9f-45a9-8239-60b4e8430a88",
  "status": "enabled",
  "message": "Dataflow created successfully"
}
```

## Tratamento de erros

O conector inclui uma manipulação de erros robusta para os seguintes cenários:

* **Erros de autenticação**: atualiza automaticamente as credenciais do Adobe quando a autenticação falha.
* **Erros de limite de taxa**: implementa novas tentativas com retirada exponencial quando os limites de taxa da API são atingidos.
* **Erros de rede**: registros e tentativas com falha nas solicitações de rede.
* **Erros de validação de dados**: registra em log cargas inválidas para revisão e resolução manuais.

Todos os erros são registrados com detalhes como tipo de erro, carimbo de data e hora, carga da solicitação e resposta da API do Adobe para facilitar a solução de problemas e a depuração.

## Testar sua conexão

Siga as etapas abaixo para saber como testar sua conexão:

* Faça uma solicitação GET para `/connections/{BASE_CONNECTION_ID}` e forneça sua ID de conexão básica para verificar se sua conexão básica existe. Durante esta etapa, você também pode verificar se o status da sua conexão básica está definido como `active`.
* Faça uma solicitação GET para `/flowservice/sourceConnections/{SOURCE_CONNECTION_ID}` e forneça sua ID de conexão de origem para verificar sua conexão de origem.
* Use o URL do ponto de extremidade de transmissão para enviar uma amostra de carga do perfil (use o JSON de assimilação de perfil).
* Navegue até o conjunto de dados na interface do usuário do Experience Platform e execute um query no conjunto de dados para confirmar os registros.
* Use os logs do Preparo de dados para inspecionar se há erros.
* Se precisar abrir um tíquete de suporte, verifique se você tem o seguinte:
   * Carga da solicitação
   * Corpo da resposta
   * ID da solicitação
   * carimbo de data e hora
   * IDs de recursos.

## Apêndice

Consulte a documentação a seguir para obter guias sobre operações adicionais

* [Monitorar fluxos de dados](../../../../../dataflows/ui/monitor-sources.md)
* [Atualizar fluxos de dados](../../../ui/update-dataflows.md)
* [Excluir fluxos de dados](../../../ui/delete.md)
* [Atualizar conta de origem](../../../ui/update.md)
