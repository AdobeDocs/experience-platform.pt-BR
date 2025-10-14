---
title: Conectar o PostgreSQL ao Experience Platform usando a API do serviço de fluxo
description: Saiba como conectar o banco de dados do  [!DNL PostgreSQL]  ao Experience Platform usando APIs.
exl-id: 5225368a-08c1-421d-aec2-d50ad09ae454
source-git-commit: f4200ca71479126e585ac76dd399af4092fdf683
workflow-type: tm+mt
source-wordcount: '749'
ht-degree: 3%

---

# Conectar o [!DNL PostgreSQL] ao Experience Platform usando a API [!DNL Flow Service]

Leia este guia para saber como conectar seu banco de dados do [!DNL PostgreSQL] ao Adobe Experience Platform usando a [[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/).

## Introdução

Este guia requer uma compreensão funcional dos seguintes componentes do Experience Platform:

* [Fontes](../../../../home.md): o Experience Platform permite a assimilação de dados de várias fontes, ao mesmo tempo em que fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços do Experience Platform.
* [Sandboxes](../../../../../sandboxes/home.md): a Experience Platform fornece sandboxes virtuais que particionam uma única instância do Experience Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito ao [!DNL PostgreSQL] usando a API [!DNL Flow Service].

### Uso de APIs do Experience Platform

Leia o manual sobre [introdução às APIs do Experience Platform](../../../../../landing/api-guide.md) para obter informações sobre como fazer chamadas com êxito para as APIs do Experience Platform.

### Coletar credenciais necessárias

Leia a [[!DNL PostgreSQL] visão geral](../../../../connectors/databases/postgres.md) para obter mais informações sobre autenticação.

### Habilitar criptografia SSL para sua cadeia de conexão

Você pode habilitar a criptografia SSL para a cadeia de conexão [!DNL PostgreSQL] anexando sua cadeia de conexão com as seguintes propriedades:

| Propriedade | Descrição | Exemplo |
| --- | --- | --- |
| `EncryptionMethod` | Permite habilitar a criptografia SSL nos dados do [!DNL PostgreSQL]. | <uL><li>`EncryptionMethod=0`(Desabilitado)</li><li>`EncryptionMethod=1`(Habilitado)</li><li>`EncryptionMethod=6`(RequestSSL)</li></ul> |
| `ValidateServerCertificate` | Valida o certificado enviado pelo banco de dados [!DNL PostgreSQL] quando `EncryptionMethod` é aplicado. | <uL><li>`ValidationServerCertificate=0`(Desabilitado)</li><li>`ValidationServerCertificate=1`(Habilitado)</li></ul> |

Este é um exemplo de uma cadeia de conexão [!DNL PostgreSQL] anexada com criptografia SSL: `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD};EncryptionMethod=1;ValidateServerCertificate=1`.

## Conectar [!DNL PostgreSQL] ao Experience Platform no Azure {#azure}

Leia as etapas abaixo para saber como conectar sua conta do [!DNL PostgreSQL] à Experience Platform no Azure.

### Criar uma conexão básica {#azure-base}

Uma conexão base retém informações entre sua origem e a Experience Platform, incluindo as credenciais de autenticação da origem, o estado atual da conexão e a ID de conexão base exclusiva. A ID de conexão básica permite explorar e navegar pelos arquivos de dentro da origem e identificar os itens específicos que deseja assimilar, incluindo informações sobre os tipos de dados e formatos.

Para criar uma ID de conexão base, faça uma solicitação POST para o ponto de extremidade `/connections` ao fornecer suas credenciais de autenticação [!DNL PostgreSQL] como parte dos parâmetros de solicitação.

**Formato da API**

```https
POST /connections
```

>[!BEGINTABS]

>[!TAB Autenticação baseada na chave da conta]

**Solicitação**

A solicitação a seguir cria uma conexão base para [!DNL PostgreSQL] usando a autenticação baseada em chave de conta:

+++Exibir exemplo de solicitação

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "PostgreSQL base connection",
      "description": "PostgreSQL base connection via connection string",
      "auth": {
          "specName": "Connection String Based Authentication",
          "params": {
              "connectionString": "Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}"
          }
      },
      "connectionSpec": {
          "id": "74a1c565-4e59-48d7-9d67-7c03b8a13137",
          "version": "1.0"
      }
  }'
```

| Propriedade | Descrição |
| ------------- | --------------- |
| `auth.params.connectionString` | A cadeia de conexão associada à sua conta [!DNL PostgreSQL]. O padrão da cadeia de conexão [!DNL PostgreSQL] é: `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}`. |
| `connectionSpec.id` | As IDs de especificação de conexão [!DNL PostgreSQL]: `74a1c565-4e59-48d7-9d67-7c03b8a13137`. |

+++

**Resposta**

Uma resposta bem-sucedida retorna o identificador exclusivo (`id`) da conexão base recém-criada.

+++Exibir exemplo de resposta

```json
{
    "id": "056dd1b4-da33-42f9-add1-b4da3392f94e",
    "etag": "\"1700e582-0000-0200-0000-5e3c85180000\""
}
```

+++

>[!TAB Autenticação básica]

**Solicitação**

A solicitação a seguir cria uma conexão base para [!DNL PostgreSQL] usando autenticação básica:

+++Exibir exemplo de solicitação

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "PostgreSQL base connection",
      "description": "PostgreSQL base connection via basic authentication",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "server": "localhost",
              "port": "3306",
              "database": "postgresql-acme",
              "username": "acme",
              "password": "xxxx",
              "sslMode": "Allow"
          }
      },
      "connectionSpec": {
          "id": "74a1c565-4e59-48d7-9d67-7c03b8a13137",
          "version": "1.0"
      }
  }'
```

| Propriedade | Descrição |
| ---| --- |
| `auth.params.server` | O nome ou endereço IP do banco de dados [!DNL PostgreSQL]. |
| `auth.params.port` | O número da porta do servidor de banco de dados. |
| `auth.params.database` | O nome do banco de dados [!DNL PostgreSQL]. |
| `auth.params.username` | O nome de usuário associado à autenticação do banco de dados do [!DNL PostgreSQL]. |
| `auth.params.password` | A senha associada à autenticação do banco de dados do [!DNL PostgreSQL]. |
| `auth.params.sslMode` | O método pelo qual os dados são criptografados durante a transferência. Os valores disponíveis incluem: `Disable`, `Allow`, `Prefer`, `Verify Ca` e `Verify Full`. |
| `connectionSpec.id` | As IDs de especificação de conexão [!DNL PostgreSQL]: `74a1c565-4e59-48d7-9d67-7c03b8a13137`. |

+++

**Resposta**

Uma resposta bem-sucedida retorna o identificador exclusivo (`id`) da conexão base recém-criada.

+++Exibir exemplo de resposta

```json
{
    "id": "2c15b1c5-73bf-47ab-9098-0467fcd854d9",
    "etag": "\"2600fc39-0000-0200-0000-67dd48f80000\""
}
```

+++

>[!ENDTABS]

## Conectar o [!DNL PostgreSQL] ao Experience Platform no Amazon Web Services {#aws}

>[!AVAILABILITY]
>
>Esta seção se aplica às implementações do Experience Platform em execução no Amazon Web Services (AWS). O Experience Platform em execução no AWS está disponível atualmente para um número limitado de clientes. Para saber mais sobre a infraestrutura do Experience Platform compatível, consulte a [visão geral da nuvem múltipla do Experience Platform](../../../../../landing/multi-cloud.md).

Leia as etapas abaixo para obter informações sobre como conectar o banco de dados do [!DNL PostgreSQL] ao Experience Platform no AWS.

### Criar uma conexão básica {#aws-base}

Para criar uma ID de conexão base, faça uma solicitação POST para o ponto de extremidade `/connections` ao fornecer suas credenciais de autenticação [!DNL PostgreSQL] como parte dos parâmetros de solicitação.

**Formato da API**

```https
POST /connections
```

**Solicitação**

A solicitação a seguir cria uma conexão base para [!DNL PostgreSQL] se conectar ao Experience Platform no AWS.

+++Exibir exemplo de solicitação

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "PostgreSQL base connection",
      "description": "PostgreSQL base connection via basic authentication",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "server": "localhost",
              "port": "3306",
              "database": "postgresql-acme",
              "username": "acme",
              "password": "xxxx",
              "sslMode": "false"
          }
      },
      "connectionSpec": {
          "id": "74a1c565-4e59-48d7-9d67-7c03b8a13137",
          "version": "1.0"
      }
  }'
```

| Propriedade | Descrição |
| ---| --- |
| `auth.params.server` | O nome ou endereço IP do banco de dados [!DNL PostgreSQL]. |
| `auth.params.port` | O número da porta do servidor de banco de dados. |
| `auth.params.database` | O nome do banco de dados [!DNL PostgreSQL]. |
| `auth.params.username` | O nome de usuário associado à autenticação do banco de dados do [!DNL PostgreSQL]. |
| `auth.params.password` | A senha associada à autenticação do banco de dados do [!DNL PostgreSQL]. |
| `sslMode` | Um valor booleano que controla se o SSL é imposto ou não, dependendo do suporte do servidor. O padrão dessa configuração é `false`. |
| `connectionSpec.id` | As IDs de especificação de conexão [!DNL PostgreSQL]: `74a1c565-4e59-48d7-9d67-7c03b8a13137`. |

+++

**Resposta**

Uma resposta bem-sucedida retorna o identificador exclusivo (`id`) da conexão base recém-criada.

+++Exibir exemplo de resposta

```json
{
    "id": "2c15b1c5-73bf-47ab-9098-0467fcd854d9",
    "etag": "\"2600fc39-0000-0200-0000-67dd48f80000\""
}
```

+++

## Próximas etapas

Agora que você criou uma conexão entre o banco de dados do [!DNL PostgreSQL] e o Experience Platform, poderá prosseguir para as próximas etapas e trazer seus dados do [!DNL PostgreSQL] para o Experience Platform. Para obter mais informações, leia a seguinte documentação:

* [Explore a estrutura e o conteúdo das tabelas de dados usando a API  [!DNL Flow Service] &#x200B;](../../explore/tabular.md)
* [Crie um fluxo de dados para trazer dados do banco de dados para a Experience Platform usando a API  [!DNL Flow Service] &#x200B;](../../collect/database-nosql.md)
