---
keywords: Experience Platform;página inicial;tópicos populares
solution: Experience Platform
title: Conectar-se a destinos em lote e ativar dados usando a API do Serviço de fluxo
description: Instruções detalhadas sobre como usar a API do Serviço de fluxo para criar um armazenamento em nuvem em lote ou um destino de marketing por email no Experience Platform e ativar dados
type: Tutorial
exl-id: 41fd295d-7cda-4ab1-a65e-b47e6c485562
source-git-commit: 833e38559f7150c579840c69fa2658761fc9472c
workflow-type: tm+mt
source-wordcount: '3450'
ht-degree: 3%

---

# Conecte-se aos destinos de marketing por email baseado em arquivo e ative os dados usando a API do Serviço de fluxo

>[!IMPORTANT]
> 
>* Para se conectar a um destino, você precisa de **[!UICONTROL Exibir Destinos]** e **[!UICONTROL Gerenciar Destinos]** [permissões de controle de acesso](/help/access-control/home.md#permissions).
>
>* Para ativar dados, você precisa de **[!UICONTROL Exibir Destinos]**, **[!UICONTROL Ativar Destinos]**, **[!UICONTROL Exibir Perfis]** e **[!UICONTROL Exibir Segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions).
>
>* Para exportar *identidades*, você precisa da **[!UICONTROL permissão Exibir Gráfico de Identidade]** [controle de acesso](/help/access-control/home.md#permissions). <br> ![Selecione o namespace de identidade realçado no fluxo de trabalho para ativar as audiências para os destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Selecione o namespace de identidade realçado no fluxo de trabalho para ativar as audiências para os destinos."){width="100" zoomable="yes"}
>
>Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.

Este tutorial demonstra como usar a API de Serviço de Fluxo para criar um [destino de marketing por email](../catalog/email-marketing/overview.md) baseado em arquivo, criar um fluxo de dados para o destino recém-criado e exportar dados para o destino recém-criado por meio de arquivos CSV.

>[!TIP]
> 
>Para saber como ativar dados para destinos de armazenamento na nuvem usando a API do Serviço de Fluxo, leia o [tutorial de API dedicado](/help/destinations/api/activate-segments-file-based-destinations.md).

Este tutorial usa o destino [!DNL Adobe Campaign] em todos os exemplos, mas as etapas são idênticas para destinos de marketing por email baseados em arquivo.

![Visão geral - as etapas para criar um destino e ativar públicos](../assets/api/email-marketing/overview.png)

Se preferir usar a interface do Experience Platform para se conectar a um destino e ativar dados, consulte os tutoriais [Conectar um destino](../ui/connect-destination.md) e [Ativar dados de público-alvo para destinos de exportação de perfil em lote](../ui/activate-batch-profile-destinations.md).

## Introdução {#get-started}

Este manual necessita de uma compreensão funcional dos seguintes componentes da Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): a estrutura padronizada pela qual o [!DNL Experience Platform] organiza os dados de experiência do cliente.
* [[!DNL Segmentation Service]](../../segmentation/api/overview.md): [!DNL Adobe Experience Platform Segmentation Service] permite que você crie públicos-alvo em [!DNL Adobe Experience Platform] a partir dos dados de [!DNL Real-Time Customer Profile].
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] fornece sandboxes virtuais que particionam uma única instância do [!DNL Experience Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisa saber para ativar dados para destinos em lote no Experience Platform.

### Coletar credenciais necessárias {#gather-required-credentials}

Para concluir as etapas deste tutorial, você deve ter as credenciais a seguir prontas, dependendo do tipo de destino ao qual você está se conectando e ativando públicos.

* Para [!DNL Amazon S3] conexões: `accessId`, `secretKey`
* Para [!DNL Amazon S3] conexões com [!DNL Adobe Campaign]: `accessId`, `secretKey`
* Para conexões SFTP: `domain`, `port`, `username`, `password` ou `sshKey` (dependendo do método de conexão para o local FTP)
* Para [!DNL Azure Blob] conexões: `connectionString`

>[!NOTE]
>
>As credenciais `accessId`, `secretKey` para [!DNL Amazon S3] conexões e `accessId`, `secretKey` para [!DNL Amazon S3] conexões com [!DNL Adobe Campaign] são idênticas.

### Leitura de chamadas de API de amostra {#reading-sample-api-calls}

Este tutorial fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e conteúdos de solicitação formatados corretamente. Também fornece exemplos de JSON retornado nas respostas da API. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler chamadas de API de exemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) no guia de solução de problemas [!DNL Experience Platform].

### Colete valores para cabeçalhos obrigatórios e opcionais {#gather-values-headers}

Para fazer chamadas para APIs do [!DNL Experience Platform], primeiro complete o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). Concluir o tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API da [!DNL Experience Platform], conforme mostrado abaixo:

* Autorização: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id `{ORG_ID}`

Os recursos em [!DNL Experience Platform] podem ser isolados em sandboxes virtuais específicas. Em solicitações para [!DNL Experience Platform] APIs, é possível especificar o nome e a ID da sandbox em que a operação ocorrerá. Esses parâmetros são opcionais.

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre sandboxes em [!DNL Experience Platform], consulte a [documentação de visão geral da sandbox](../../sandboxes/home.md).

Todas as solicitações que contêm uma carga (POST, PUT, PATCH) exigem um cabeçalho de tipo de mídia adicional:

* Tipo de conteúdo: `application/json`

### Documentação de referência da API {#api-reference-documentation}

Você pode encontrar a documentação de referência de acompanhamento para todas as operações de API neste tutorial. Consulte a [Documentação da API de Serviço de Fluxo no Adobe I/O](https://www.adobe.io/experience-platform-apis/references/flow-service/). Recomendamos que você use este tutorial e a documentação de referência da API em paralelo.

## Obter a lista de destinos disponíveis {#get-the-list-of-available-destinations}

![Etapa de visão geral das etapas de destino 1](../assets/api/batch-destination/step1.png)

Como primeira etapa, você deve decidir para qual destino ativar os dados. Para começar, execute uma chamada para solicitar uma lista de destinos disponíveis aos quais você pode se conectar e ativar públicos. Execute a seguinte solicitação GET para o ponto de extremidade `connectionSpecs` para retornar uma lista de destinos disponíveis:

**Formato da API**

```http
GET /connectionSpecs
```

**Solicitação**

```shell
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs' \
--header 'accept: application/json' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}'
```


**Resposta**

Uma resposta bem-sucedida contém uma lista de destinos disponíveis e seus identificadores exclusivos (`id`). Armazene o valor do destino que você planeja usar, pois ele será necessário em outras etapas. Por exemplo, se você deseja conectar e entregar públicos para [!DNL Adobe Campaign], procure o seguinte trecho na resposta:

```json
{
    "id": "0b23e41a-cb4a-4321-a78f-3b654f5d7d97",
  "name": "Adobe Campaign",
  ...
  ...
}
```

Para sua referência, a tabela abaixo contém as IDs de especificação da conexão para destinos em lote de uso comum:

| Destino | ID de especificação da conexão |
---------|----------|
| [!DNL Adobe Campaign] | `0b23e41a-cb4a-4321-a78f-3b654f5d7d97` |
| [!DNL Oracle Eloqua] | `c1e44b6b-e7c8-404b-9031-58f0ef760604` |
| [!DNL Oracle Responsys] | `a5e28ddf-e265-426e-83a1-9d03a3a6822b` |
| [!DNL Salesforce Marketing Cloud] | `f599a5b3-60a7-4951-950a-cc4115c7ea27` |

{style="table-layout:auto"}

## Conectar aos dados do [!DNL Experience Platform] {#connect-to-your-experience-platform-data}

![Etapa 2](../assets/api/batch-destination/step2.png) da visão geral das etapas de destino

Em seguida, conecte-se aos dados do [!DNL Experience Platform] para poder exportar dados de perfil e ativá-los no seu destino preferido. Consiste em duas subetapas descritas abaixo.

1. Primeiro, você deve executar uma chamada para autorizar o acesso aos seus dados no [!DNL Experience Platform], configurando uma conexão base.
2. Em seguida, usando a ID de conexão básica, execute outra chamada na qual você cria uma *conexão de origem*, que estabelece a conexão com seus dados do [!DNL Experience Platform].

### Autorizar acesso aos seus dados no [!DNL Experience Platform]

**Formato da API**

```http
POST /connections
```

**Solicitação**

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
            "name": "Base connection to Experience Platform",
            "description": "This call establishes the connection to Experience Platform data",
            "connectionSpec": {
                "id": "{CONNECTION_SPEC_ID}",
                "version": "1.0"
            }
}'
```

| Propriedade | Descrição |
| --------- | ----------- |
| `name` | Forneça um nome para a conexão básica com o Experience Platform [!DNL Profile store]. |
| `description` | Como opção, você pode fornecer uma descrição para a conexão base. |
| `connectionSpec.id` | Use a ID de especificação de conexão para o [repositório de Perfis da Experience Platform](/help/profile/home.md#profile-data-store) - `8a9c3494-9708-43d7-ae3f-cda01e5030e1`. |

{style="table-layout:auto"}

**Resposta**

Uma resposta bem-sucedida contém o identificador exclusivo da conexão base (`id`). Armazene esse valor conforme necessário na próxima etapa para criar a conexão de origem.

```json
{
    "id": "1ed86558-59b5-42f7-9865-5859b552f7f4"
}
```

### Conectar aos dados do [!DNL Experience Platform] {#connect-to-platform-data}

**Formato da API**

```http
POST /sourceConnections
```

**Solicitação**

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
            "name": "Connecting to Profile store",
            "description": "Optional",
            "connectionSpec": {
                "id": "{CONNECTION_SPEC_ID}",
                "version": "1.0"
            },
            "baseConnectionId": "{BASE_CONNECTION_ID}",
            "data": {
                "format": "CSV",
                "schema": null
            },
            "params" : {}
}'
```

| Propriedade | Descrição |
| --------- | ----------- |
| `name` | Forneça um nome para a conexão de origem com a Experience Platform [!DNL Profile store]. |
| `description` | Como opção, você pode fornecer uma descrição para a conexão de origem. |
| `connectionSpec.id` | Use a ID de especificação de conexão para o [repositório de Perfis da Experience Platform](/help/profile/home.md#profile-data-store) - `8a9c3494-9708-43d7-ae3f-cda01e5030e1`. |
| `baseConnectionId` | Use a ID de conexão básica obtida na etapa anterior. |
| `data.format` | No momento, `CSV` é o único formato de exportação de arquivo com suporte. |

{style="table-layout:auto"}

**Resposta**

Uma resposta bem-sucedida retorna o identificador exclusivo (`id`) da conexão de origem recém-criada para [!DNL Profile store]. Isso confirma que você se conectou com êxito aos dados do [!DNL Experience Platform]. Armazene esse valor conforme necessário em uma etapa posterior.

```json
{
    "id": "ed48ae9b-c774-4b6e-88ae-9bc7748b6e97"
}
```

## Conectar ao destino do lote {#connect-to-batch-destination}

![Etapa de visão geral das etapas de destino 3](../assets/api/batch-destination/step3.png)

Nesta etapa, você está configurando uma conexão com o armazenamento em nuvem em lote ou destino de marketing por email desejado. Consiste em duas subetapas descritas abaixo.

1. Primeiro, você deve executar uma chamada para autorizar o acesso à plataforma de destino, configurando uma conexão básica.
2. Em seguida, usando a ID de conexão básica, você fará outra chamada na qual criará uma *conexão de destino*, que especifica o local da conta de armazenamento em que os arquivos de dados exportados serão entregues, bem como o formato dos dados que serão exportados.

### Autorizar acesso ao destino do lote {#authorize-access-to-batch-destination}

**Formato da API**

```http
POST /connections
```

**Solicitação**

A solicitação abaixo estabelece uma conexão básica com [!DNL Adobe Campaign] destinos. Dependendo do local de armazenamento para o qual você deseja exportar arquivos ([!DNL Amazon S3], SFTP, [!DNL Azure Blob]), mantenha a especificação `auth` apropriada e exclua as outras.

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "S3 Connection for Adobe Campaign",
    "description": "summer advertising campaign",
    "connectionSpec": {
        "id": "0b23e41a-cb4a-4321-a78f-3b654f5d7d97",
        "version": "1.0"
    },
    "auth": {
        "specName": "S3",
        "params": {
            "accessId": "{ACCESS_ID}",
            "secretKey": "{SECRET_KEY}"
        }
    }
    "auth": {
        "specName": "SFTP with Password",
        "params": {
            "domain": "{DOMAIN}",
            "host": "{HOST}",
            "username": "{USERNAME}",
            "password": "{PASSWORD}"
        }
    }
    "auth": {
        "specName": "SFTP with SSH Key",
        "params": {
            "domain": "{DOMAIN}",
            "host": "{HOST}",
            "username": "{USERNAME}",
            "sshKey": "{SSH_KEY}"
        }
    }        
    "auth": {
        "specName": "Azure Blob",
        "params": {
            "connectionString": "{AZURE_BLOB_CONNECTION_STRING}"
        }
    }    
}'
```

Consulte as solicitações de exemplo abaixo para se conectar a outros destinos de armazenamento em nuvem em lote e marketing por email compatíveis.

+++ Exemplo de solicitação para conectar a [!DNL Amazon S3] destinos

A solicitação abaixo estabelece uma conexão básica com [!DNL Amazon S3] destinos.

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "Connect to Amazon S3",
    "description": "summer advertising campaign",
    "connectionSpec": {
        "id": "4890fc95-5a1f-4983-94bb-e060c08e3f81",
        "version": "1.0"
    },
    "auth": {
        "specName": "Access Key",
        "params": {
            "s3AccessKey": "{AMAZON_S3_ACCESS_KEY}",
            "s3SecretKey": "{AMAZON_S3_SECRET_KEY}"
        }
    }
}'
```

+++

+++ Exemplo de solicitação para conectar a [!DNL Azure Blob] destinos

A solicitação abaixo estabelece uma conexão básica com [!DNL Azure Blob] destinos.

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "Connect to Azure Blob",
    "description": "Summer advertising campaign",
    "connectionSpec": {
        "id": "e258278b-a4cf-43ac-b158-4fa0ca0d948b",
        "version": "1.0"
    },
    "auth": {
        "specName": "ConnectionString",
        "params": {
            "connectionString": "{AZURE_BLOB_CONNECTION_STRING}"
        }
    }
}'
```

+++

+++ Exemplo de solicitação para conectar a [!DNL Oracle Eloqua] destinos

A solicitação abaixo estabelece uma conexão básica com [!DNL Oracle Eloqua] destinos. Dependendo do local de armazenamento para o qual você deseja exportar arquivos, mantenha a especificação `auth` apropriada e exclua as outras.

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "Connect to Eloqua destination",
    "description": "summer advertising campaign",
    "connectionSpec": {
        "id": "c1e44b6b-e7c8-404b-9031-58f0ef760604",
        "version": "1.0"
    },
    "auth": {
        "specName": "SFTP with Password",
        "params": {
            "domain": "{DOMAIN}",
            "host": "{HOST}",
            "username": "{USERNAME}",
            "password": "{PASSWORD}"
        }
    }
    "auth": {
        "specName": "SFTP with SSH Key",
        "params": {
            "domain": "{DOMAIN}",
            "host": "{HOST}",
            "username": "{USERNAME}",
            "sshKey": "{SSH_KEY}"
        }
    }    
}'
```

+++

+++ Exemplo de solicitação para conectar a [!DNL Oracle Responsys] destinos

A solicitação abaixo estabelece uma conexão básica com [!DNL Oracle Responsys] destinos. Dependendo do local de armazenamento para o qual você deseja exportar arquivos, mantenha a especificação `auth` apropriada e exclua as outras.

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "Connect to Responsys destination",
    "description": "summer advertising campaign",
    "connectionSpec": {
        "id": "a5e28ddf-e265-426e-83a1-9d03a3a6822b",
        "version": "1.0"
    },
    "auth": {
        "specName": "SFTP with Password",
        "params": {
            "domain": "{DOMAIN}",
            "host": "{HOST}",
            "username": "{USERNAME}",
            "password": "{PASSWORD}"
        }
    }
    "auth": {
        "specName": "SFTP with SSH Key",
        "params": {
            "domain": "{DOMAIN}",
            "host": "{HOST}",
            "username": "{USERNAME}",
            "sshKey": "{SSH_KEY}"
        }
    }    
}'
```

+++

+++ Exemplo de solicitação para conectar a [!DNL Salesforce Marketing Cloud] destinos

A solicitação abaixo estabelece uma conexão básica com [!DNL Salesforce Marketing Cloud] destinos. Dependendo do local de armazenamento para o qual você deseja exportar arquivos, mantenha a especificação `auth` apropriada e exclua as outras.

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "Connect to Salesforce Marketing Cloud",
    "description": "summer advertising campaign",
    "connectionSpec": {
        "id": "f599a5b3-60a7-4951-950a-cc4115c7ea27",
        "version": "1.0"
    },
    "auth": {
        "specName": "SFTP with Password",
        "params": {
            "domain": "{DOMAIN}",
            "host": "{HOST}",
            "username": "{USERNAME}",
            "password": "{PASSWORD}"
        }
    }
    "auth": {
        "specName": "SFTP with SSH Key",
        "params": {
            "domain": "{DOMAIN}",
            "host": "{HOST}",
            "username": "{USERNAME}",
            "sshKey": "{SSH_KEY}"
        }
    }    
}'
```

+++

+++ Exemplo de solicitação de conexão com SFTP com destinos de senha

A solicitação abaixo estabelece uma conexão básica com destinos SFTP.

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "Connect to SFTP with password",
    "description": "summer advertising campaign",
    "connectionSpec": {
        "id": "64ef4b8b-a6e0-41b5-9677-3805d1ee5dd0",
        "version": "1.0"
    },
    "auth": {
        "specName": "Basic Authentication for sftp",
        "params": {
            "host": "{HOST}",
            "username": "{USERNAME}",
            "password": "{PASSWORD}"
        }
    }
}'
```

+++

| Propriedade | Descrição |
| --------- | ----------- |
| `name` | Forneça um nome para a conexão básica com o destino do lote. |
| `description` | Como opção, você pode fornecer uma descrição para a conexão base. |
| `connectionSpec.id` | Use a ID de especificação da conexão para o destino em lote desejado. Você obteve essa ID na etapa [Obter a lista de destinos disponíveis](#get-the-list-of-available-destinations). |
| `auth.specname` | Indica o formato de autenticação do destino. Para descobrir o specName do seu destino, execute uma [chamada do GET para o ponto de extremidade de especificações de conexão](https://developer.adobe.com/experience-platform-apis/references/flow-service/#operation/retrieveConnectionSpec), fornecendo a especificação de conexão do seu destino desejado. Procure o parâmetro `authSpec.name` na resposta. <br> Por exemplo, para destinos Adobe Campaign, você pode usar qualquer um dos `S3`, `SFTP with Password`, ou `SFTP with SSH Key`. |
| `params` | Dependendo do destino ao qual você está se conectando, você deve fornecer diferentes parâmetros de autenticação necessários. Para conexões do Amazon S3, você deve fornecer sua ID de acesso e chave secreta ao local de armazenamento do Amazon S3. <br> Para descobrir os parâmetros necessários para o seu destino, execute uma [chamada do GET para o ponto de extremidade de especificações de conexão](https://developer.adobe.com/experience-platform-apis/references/flow-service/#operation/retrieveConnectionSpec), fornecendo a especificação de conexão do seu destino desejado. Procure o parâmetro `authSpec.spec.required` na resposta. |

{style="table-layout:auto"}

**Resposta**

Uma resposta bem-sucedida contém o identificador exclusivo da conexão base (`id`). Armazene esse valor conforme necessário na próxima etapa para criar uma conexão de destino.

```json
{
    "id": "1ed86558-59b5-42f7-9865-5859b552f7f4"
}
```

### Especificar local de armazenamento e formato de dados {#specify-storage-location-data-format}

O [!DNL Adobe Experience Platform] exporta dados para destinos de marketing por email em lote e de armazenamento na nuvem na forma de [!DNL CSV] arquivos. Nesta etapa, você pode determinar o caminho no local de armazenamento para onde os arquivos serão exportados.

>[!IMPORTANT]
> 
>O [!DNL Adobe Experience Platform] divide automaticamente os arquivos de exportação em 5 milhões de registros (linhas) por arquivo. Cada linha representa um perfil.
>
>Nomes de arquivos divididos são anexados com um número que indica que o arquivo é parte de uma exportação maior, como: `filename.csv`, `filename_2.csv`, `filename_3.csv`.

**Formato da API**

```http
POST /targetConnections
```

**Solicitação**

A solicitação abaixo estabelece uma conexão de destino com [!DNL Adobe Campaign] destinos, para determinar para onde os arquivos exportados chegarão em seu local de armazenamento. Dependendo do local de armazenamento para o qual você deseja exportar arquivos, mantenha a especificação `params` apropriada e exclua as outras.

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "TargetConnection for Adobe Campaign",
    "description": "Connection to Adobe Campaign",
    "baseConnectionId": "{BASE_CONNECTION_ID}",
    "connectionSpec": {
        "id": "0b23e41a-cb4a-4321-a78f-3b654f5d7d97",
        "version": "1.0"
    },
    "data": {
        "format": "json",
        "schema": {
            "id": "1.0",
            "version": "1.0"
        }
    },
    "params": {
        "mode": "S3",
        "bucketName": "{BUCKET_NAME}",
        "path": "{FILEPATH}",
        "format": "CSV",
        "includeFileManifest": true // Include this parameter if you want to enable manifest file generation for your destination
    }
    "params": {
        "mode": "AZURE_BLOB",
        "container": "{CONTAINER}",
        "path": "{FILEPATH}",
        "format": "CSV",
        "includeFileManifest": true // Include this parameter if you want to enable manifest file generation for your destination
    }
    "params": {
        "mode": "FTP",
        "remotePath": "{REMOTE_PATH}",
        "format": "CSV",
        "includeFileManifest": true // Include this parameter if you want to enable manifest file generation for your destination
    }        
}'
```

Consulte as solicitações de exemplo abaixo para configurar um local de armazenamento para outros destinos de armazenamento na nuvem em lote e de marketing por email compatíveis.

+++ Exemplo de solicitação para configurar um local de armazenamento para [!DNL Amazon S3] destinos

A solicitação abaixo estabelece uma conexão de destino com [!DNL Amazon S3] destinos, para determinar para onde os arquivos exportados chegarão em seu local de armazenamento.

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "TargetConnection for Amazon S3",
    "description": "Connection to Amazon S3",
    "baseConnectionId": "{BASE_CONNECTION_ID}",
    "connectionSpec": {
        "id": "4890fc95-5a1f-4983-94bb-e060c08e3f81",
        "version": "1.0"
    },
    "data": {
        "format": "json",
        "schema": {
            "id": "1.0",
            "version": "1.0"
        }
    },
    "params": {
        "mode": "S3",
        "bucketName": "{BUCKET_NAME}",
        "path": "{FILEPATH}",
        "format": "CSV",
        "includeFileManifest": true // Include this parameter if you want to enable manifest file generation for your destination
    }
}'
```

+++

+++ Exemplo de solicitação para configurar um local de armazenamento para [!DNL Azure Blob] destinos

A solicitação abaixo estabelece uma conexão de destino com [!DNL Azure Blob] destinos, para determinar para onde os arquivos exportados chegarão em seu local de armazenamento.

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "TargetConnection for Azure Blob",
    "description": "Connection to Azure Blob",
    "baseConnectionId": "{BASE_CONNECTION_ID}",
    "connectionSpec": {
        "id": "e258278b-a4cf-43ac-b158-4fa0ca0d948b",
        "version": "1.0"
    },
    "data": {
        "format": "json",
        "schema": {
            "id": "1.0",
            "version": "1.0"
        }
    },
    "params": {
        "mode": "AZURE_BLOB",
        "container": "{CONTAINER}",
        "path": "{FILEPATH}",
        "format": "CSV",
        "includeFileManifest": true // Include this parameter if you want to enable manifest file generation for your destination
    }
}'
```

+++

+++ Exemplo de solicitação para configurar um local de armazenamento para [!DNL Oracle Eloqua] destinos

A solicitação abaixo estabelece uma conexão de destino com [!DNL Oracle Eloqua] destinos, para determinar para onde os arquivos exportados chegarão em seu local de armazenamento. Dependendo do local de armazenamento para o qual você deseja exportar arquivos, mantenha a especificação `params` apropriada e exclua as outras.

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "TargetConnection for Oracle Eloqua",
    "description": "Connection to Oracle Eloqua",
    "baseConnectionId": "{BASE_CONNECTION_ID}",
    "connectionSpec": {
        "id": "c1e44b6b-e7c8-404b-9031-58f0ef760604",
        "version": "1.0"
    },
    "data": {
        "format": "json",
        "schema": {
            "id": "1.0",
            "version": "1.0"
        }
    },
    "params": {
        "mode": "S3",
        "bucketName": "{BUCKET_NAME}",
        "path": "{FILEPATH}",
        "format": "CSV",
        "includeFileManifest": true // Include this parameter if you want to enable manifest file generation for your destination
    }
    "params": {
        "mode": "FTP",
        "remotePath": "{REMOTE_PATH}",
        "format": "CSV",
        "includeFileManifest": true // Include this parameter if you want to enable manifest file generation for your destination
    }        
}'
```

+++

+++ Exemplo de solicitação para configurar um local de armazenamento para [!DNL Oracle Responsys] destinos

A solicitação abaixo estabelece uma conexão de destino com [!DNL Oracle Responsys] destinos, para determinar para onde os arquivos exportados chegarão em seu local de armazenamento. Dependendo do local de armazenamento para o qual você deseja exportar arquivos, mantenha a especificação `params` apropriada e exclua as outras.

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "TargetConnection for Oracle Responsys",
    "description": "Connection to Oracle Responsys",
    "baseConnectionId": "{BASE_CONNECTION_ID}",
    "connectionSpec": {
        "id": "a5e28ddf-e265-426e-83a1-9d03a3a6822b",
        "version": "1.0"
    },
    "data": {
        "format": "json",
        "schema": {
            "id": "1.0",
            "version": "1.0"
        }
    },
    "params": {
        "mode": "S3",
        "bucketName": "{BUCKET_NAME}",
        "path": "{FILEPATH}",
        "format": "CSV",
        "includeFileManifest": true // Include this parameter if you want to enable manifest file generation for your destination
    }
    "params": {
        "mode": "FTP",
        "remotePath": "{REMOTE_PATH}",
        "format": "CSV",
        "includeFileManifest": true // Include this parameter if you want to enable manifest file generation for your destination
    }        
}'
```

+++

+++ Exemplo de solicitação para configurar um local de armazenamento para [!DNL Salesforce Marketing Cloud] destinos

A solicitação abaixo estabelece uma conexão de destino com [!DNL Salesforce Marketing Cloud] destinos, para determinar para onde os arquivos exportados chegarão em seu local de armazenamento. Dependendo do local de armazenamento para o qual você deseja exportar arquivos, mantenha a especificação `params` apropriada e exclua as outras.

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "TargetConnection for Salesforce Marketing Cloud",
    "description": "Connection to Salesforce Marketing Cloud",
    "baseConnectionId": "{BASE_CONNECTION_ID}",
    "connectionSpec": {
        "id": "f599a5b3-60a7-4951-950a-cc4115c7ea27",
        "version": "1.0"
    },
    "data": {
        "format": "json",
        "schema": {
            "id": "1.0",
            "version": "1.0"
        }
    },
    "params": {
        "mode": "S3",
        "bucketName": "{BUCKET_NAME}",
        "path": "{FILEPATH}",
        "format": "CSV",
        "includeFileManifest": true // Include this parameter if you want to enable manifest file generation for your destination
    }
    "params": {
        "mode": "FTP",
        "remotePath": "{REMOTE_PATH}",
        "format": "CSV",
        "includeFileManifest": true // Include this parameter if you want to enable manifest file generation for your destination
    }        
}'
```

+++

+++ Exemplo de solicitação para configurar um local de armazenamento para destinos SFTP

A solicitação abaixo estabelece uma conexão de destino com destinos SFTP para determinar onde os arquivos exportados chegarão em seu local de armazenamento.

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "TargetConnection for SFTP",
    "description": "Connection to SFTP",
    "baseConnectionId": "{BASE_CONNECTION_ID}",
    "connectionSpec": {
        "id": "64ef4b8b-a6e0-41b5-9677-3805d1ee5dd0",
        "version": "1.0"
    },
    "data": {
        "format": "json",
        "schema": {
            "id": "1.0",
            "version": "1.0"
        }
    },
    "params": {
        "mode": "FTP",
        "remotePath": "{REMOTE_PATH}",
        "includeFileManifest": true // Include this parameter if you want to enable manifest file generation for your destination
    }
}'
```

+++


| Propriedade | Descrição |
| --------- | ----------- |
| `name` | Forneça um nome para a conexão de destino com o destino do lote. |
| `description` | Como opção, você pode fornecer uma descrição para a conexão de destino. |
| `baseConnectionId` | Use a ID da conexão base criada na etapa acima. |
| `connectionSpec.id` | Use a ID de especificação da conexão para o destino em lote desejado. Você obteve essa ID na etapa [Obter a lista de destinos disponíveis](#get-the-list-of-available-destinations). |
| `params` | Dependendo do destino ao qual você está se conectando, você deve fornecer diferentes parâmetros necessários para o local de armazenamento. Para conexões do Amazon S3, você deve fornecer sua ID de acesso e chave secreta ao local de armazenamento do Amazon S3. <br> Para descobrir os parâmetros necessários para o seu destino, execute uma [chamada do GET para o ponto de extremidade de especificações de conexão](https://developer.adobe.com/experience-platform-apis/references/flow-service/#operation/retrieveConnectionSpec), fornecendo a especificação de conexão do seu destino desejado. Procure o parâmetro `targetSpec.spec.required` na resposta. |
| `params.mode` | Dependendo do modo compatível com seu destino, você deve fornecer um valor diferente aqui. Para descobrir os parâmetros necessários para o seu destino, execute uma [chamada do GET para o ponto de extremidade de especificações de conexão](https://developer.adobe.com/experience-platform-apis/references/flow-service/#operation/retrieveConnectionSpec), fornecendo a especificação de conexão do seu destino desejado. Procure o parâmetro `targetSpec.spec.properties.mode.enum` na resposta e selecione o modo desejado. |
| `params.bucketName` | Para conexões S3, forneça o nome do bucket para o qual os arquivos serão exportados. |
| `params.path` | Para conexões S3, forneça o caminho do arquivo no local de armazenamento para onde os arquivos serão exportados. |
| `params.format` | No momento, `CSV` é o único tipo de exportação de arquivo com suporte. |
| `params.includeFileManifest` | *Opcional*. Defina como `true` para habilitar a geração de arquivo de manifesto para o seu destino. Quando ativado, um arquivo de manifesto é criado junto com os arquivos de dados exportados, fornecendo metadados sobre os arquivos exportados. Exibir um [arquivo de manifesto de exemplo](/help/destinations/assets/common/manifest-d0420d72-756c-4159-9e7f-7d3e2f8b501e-0ac8f3c0-29bd-40aa-82c1-f1b7e0657b19.json). |

{style="table-layout:auto"}

**Resposta**

Uma resposta bem-sucedida retorna o identificador exclusivo (`id`) da conexão de destino recém-criada ao destino em lote. Armazene esse valor conforme necessário nas etapas posteriores.

```json
{
    "id": "12ab90c7-519c-4291-bd20-d64186b62da8"
}
```

## Criar um fluxo de dados {#create-dataflow}

![Etapa 4](../assets/api/batch-destination/step4.png) da visão geral das etapas de destino

Usando a especificação de fluxo, a conexão de origem e as IDs de conexão de destino obtidas nas etapas anteriores, agora é possível criar um fluxo de dados entre os dados do [!DNL Experience Platform] e o destino para o qual você exportará os arquivos de dados. Pense nessa etapa como a construção do pipeline pelo qual os dados fluirão posteriormente entre [!DNL Experience Platform] e o destino desejado.

Para criar um fluxo de dados, execute uma solicitação POST, como mostrado abaixo, enquanto fornece os valores mencionados abaixo na carga.

**Formato da API**

```http
POST /flows
```

**Solicitação**

```shell
curl -X POST \
'https://platform.adobe.io/data/foundation/flowservice/flows' \
-H 'Authorization: Bearer {ACCESS_TOKEN}' \
-H 'x-api-key: {API_KEY}' \
-H 'x-gw-ims-org-id: {ORG_ID}' \
-H 'x-sandbox-name: {SANDBOX_NAME}' \
-H 'Content-Type: application/json' \
-d  '{
   
        "name": "activate audiences to Adobe Campaign",
        "description": "This operation creates a dataflow which we will later use to activate audiences to Adobe Campaign",
        "flowSpec": {
            "id": "{FLOW_SPEC_ID}",
            "version": "1.0"
        },
        "sourceConnectionIds": [
            "{SOURCE_CONNECTION_ID}"
        ],
        "targetConnectionIds": [
            "{TARGET_CONNECTION_ID}"
        ],
        "transformations": [
            {
                "name": "GeneralTransform",
                "params": {
                    "segmentSelectors": {
                        "selectors": []
                    },
                    "profileSelectors": {
                        "selectors": []
                    }
                }
            }
        ]
    }
```

| Propriedade | Descrição |
| --------- | ----------- |
| `name` | Forneça um nome para o fluxo de dados que você está criando. |
| `description` | Como opção, você pode fornecer uma descrição para o fluxo de dados. |
| `flowSpec.Id` | Use a ID de especificação do fluxo para o destino do lote ao qual você deseja se conectar. Para recuperar a ID de especificação do fluxo, execute uma operação do GET no ponto de extremidade `flowspecs`, conforme mostrado na [documentação de referência da API de especificações do fluxo](https://www.adobe.io/experience-platform-apis/references/flow-service/#operation/retrieveFlowSpec). Na resposta, procure `upsTo` e copie a ID correspondente do destino do lote ao qual você deseja se conectar. Por exemplo, para o Adobe Campaign, procure `upsToCampaign` e copie o parâmetro `id`. |
| `sourceConnectionIds` | Use a ID de conexão de origem obtida na etapa [Conectar-se aos dados do Experience Platform](#connect-to-your-experience-platform-data). |
| `targetConnectionIds` | Use a ID de conexão de destino que você obteve na etapa [Conectar ao destino do lote](#connect-to-batch-destination). |
| `transformations` | Na próxima etapa, você preencherá esta seção com os públicos-alvo e atributos de perfil que serão ativados. |

Para sua referência, a tabela abaixo contém as IDs de especificação de fluxo para destinos em lote usados com frequência:

| Destino | ID de especificação de fluxo |
---------|----------|
| Todos os destinos de armazenamento na nuvem ([!DNL Amazon S3], SFTP, [!DNL Azure Blob]) e [!DNL Oracle Eloqua] | `71471eba-b620-49e4-90fd-23f1fa0174d8` |
| [!DNL Oracle Responsys] | `51d675ce-e270-408d-91fc-22717bdf2148` |
| [!DNL Salesforce Marketing Cloud] | `493b2bd6-26e4-4167-ab3b-5e910bba44f0` |

**Resposta**

Uma resposta bem-sucedida retorna a ID (`id`) do fluxo de dados recém-criado e um `etag`. Anote os dois valores, pois eles serão necessários na próxima etapa, para ativar públicos e exportar arquivos de dados.

```json
{
    "id": "8256cfb4-17e6-432c-a469-6aedafb16cd5",
    "etag": "8256cfb4-17e6-432c-a469-6aedafb16cd5"
}
```


## Ativar dados para o novo destino {#activate-data}

![Etapa de visão geral das etapas de destino 5](../assets/api/batch-destination/step5.png)

Após criar todas as conexões e o fluxo de dados, agora é possível ativar os dados do perfil na plataforma de destino. Nesta etapa, você seleciona quais públicos-alvo e atributos de perfil serão exportados para o destino.

Você também pode determinar o formato de nomenclatura dos arquivos exportados e quais atributos devem ser usados como [chaves de desduplicação](../ui/activate-batch-profile-destinations.md#mandatory-keys) ou [atributos obrigatórios](../ui/activate-batch-profile-destinations.md#mandatory-attributes). Nesta etapa, você também pode determinar o agendamento para enviar dados ao destino.

Para ativar públicos para o novo destino, você deve executar uma operação JSON PATCH, semelhante ao exemplo abaixo. Você pode ativar vários públicos-alvo e atributos de perfil em uma chamada. Para saber mais sobre o JSON PATCH, consulte a [especificação RFC](https://tools.ietf.org/html/rfc6902).

**Formato da API**

```http
PATCH /flows
```

**Solicitação**

```shell
curl --location --request PATCH 'https://platform.adobe.io/data/foundation/flowservice/flows/{DATAFLOW_ID}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'Content-Type: application/json' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'If-Match: "{ETAG}"' \
--data-raw '[
    {
        "op": "add",
        "path": "/transformations/0/params/segmentSelectors/selectors/-",
        "value": {
            "type": "PLATFORM_SEGMENT",
            "value": {
                "name": "Name of the audience that you are activating",
                "description": "Description of the audience that you are activating",
                "id": "{SEGMENT_ID}",
                "filenameTemplate": "%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%",
                "exportMode": "DAILY_FULL_EXPORT",
                "schedule": {
                    "frequency": "ONCE",
                    "startDate": "2021-12-20",
                    "startTime": "17:00"
                } 
            }
        }
    },
{
        "op": "add",
        "path": "/transformations/0/params/segmentSelectors/selectors/-",
        "value": {
            "type": "PLATFORM_SEGMENT",
            "value": {
                "name": "Name of the audience that you are activating",
                "description": "Description of the audience that you are activating",
                "id": "{SEGMENT_ID}",
                "filenameTemplate": "%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%",
                "exportMode": "DAILY_FULL_EXPORT",
                "schedule": {
                    "frequency": "ONCE",
                    "triggerType": "SCHEDULED",
                    "startDate": "2021-12-20",
                    "startTime": "17:00"
                },   
            }
        }
    },
{
        "op": "add",
        "path": "/transformations/0/params/profileSelectors/selectors/-",
        "value": {
            "type": "JSON_PATH",
            "value": {
                "path": "{PROFILE_ATTRIBUTE}"
            }
        }
    }
]
```

| Propriedade | Descrição |
| --------- | ----------- |
| `{DATAFLOW_ID}` | No URL, use a ID do fluxo de dados criado na etapa anterior. |
| `{ETAG}` | Obtenha o `{ETAG}` da resposta da etapa anterior, [Criar um fluxo de dados](#create-dataflow). O formato de resposta na etapa anterior tem aspas em escape. Você deve usar os valores sem escape no cabeçalho da solicitação. Veja o exemplo abaixo: <br> <ul><li>Exemplo de resposta: `"etag":""7400453a-0000-1a00-0000-62b1c7a90000""`</li><li>Valor a ser usado em sua solicitação: `"etag": "7400453a-0000-1a00-0000-62b1c7a90000"`</li></ul> <br> O valor da marca é atualizado com cada atualização bem-sucedida de um fluxo de dados. |
| `{SEGMENT_ID}` | Forneça a ID de público-alvo que você deseja exportar para este destino. Para recuperar as IDs de público-alvo para os públicos que você deseja ativar, consulte [recuperar uma definição de público-alvo](https://www.adobe.io/experience-platform-apis/references/segmentation/#operation/retrieveSegmentDefinitionById) na referência da API do Experience Platform. |
| `{PROFILE_ATTRIBUTE}` | Por exemplo, `"person.lastName"` |
| `op` | A chamada de operação usada para definir a ação necessária para atualizar o fluxo de dados. As operações incluem: `add`, `replace` e `remove`. Para adicionar uma audiência a um fluxo de dados, use a operação `add`. |
| `path` | Define a parte do fluxo que deve ser atualizada. Ao adicionar um público-alvo a um fluxo de dados, use o caminho especificado no exemplo. |
| `value` | O novo valor com o qual você deseja atualizar seu parâmetro. |
| `id` | Especifique a ID do público-alvo que você está adicionando ao fluxo de dados de destino. |
| `name` | *Opcional*. Especifique o nome do público-alvo que você está adicionando ao fluxo de dados de destino. Observe que esse campo não é obrigatório e que você pode adicionar um público-alvo ao fluxo de dados de destino com êxito sem fornecer seu nome. |
| `filenameTemplate` | Esse campo determina o formato do nome do arquivo dos arquivos exportados para o seu destino. <br> As seguintes opções estão disponíveis: <br> <ul><li>`%DESTINATION_NAME%`: Obrigatório. Os arquivos exportados contêm o nome de destino.</li><li>`%SEGMENT_ID%`: Obrigatório. Os arquivos exportados contêm a ID do público-alvo exportado.</li><li>`%SEGMENT_NAME%`: Opcional. Os arquivos exportados contêm o nome do público exportado.</li><li>`DATETIME(YYYYMMdd_HHmmss)` ou `%TIMESTAMP%`: Opcional. Selecione uma dessas duas opções para que seus arquivos incluam a hora em que são gerados pelo Experience Platform.</li><li>`custom-text`: Opcional. Substitua esse espaço reservado por qualquer texto personalizado que queira anexar ao final dos nomes de arquivo.</li></ul> <br> Para obter mais informações sobre como configurar nomes de arquivos, consulte a seção [configurar nomes de arquivos](/help/destinations/ui/activate-batch-profile-destinations.md#file-names) no tutorial de ativação de destinos em lote. |
| `exportMode` | Obrigatório. Selecione `"DAILY_FULL_EXPORT"` ou `"FIRST_FULL_THEN_INCREMENTAL"`. Para obter mais informações sobre as duas opções, consulte [exportar arquivos completos](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files) e [exportar arquivos incrementais](/help/destinations/ui/activate-batch-profile-destinations.md#export-incremental-files) no tutorial de ativação de destinos em lote. |
| `startDate` | Selecione a data em que o público-alvo deve começar a exportar perfis para o seu destino. |
| `frequency` | Obrigatório. <br> <ul><li>Para o modo de exportação `"DAILY_FULL_EXPORT"`, você pode selecionar `ONCE`, `DAILY`, `WEEKLY` ou `MONTHLY`.</li><li>Para o modo de exportação `"FIRST_FULL_THEN_INCREMENTAL"`, você pode selecionar `"DAILY"`, `"EVERY_3_HOURS"`, `"EVERY_6_HOURS"`, `"EVERY_8_HOURS"`, `"EVERY_12_HOURS"`.</li></ul> |
| `triggerType` | Somente para *destinos em lote*. Este campo é necessário somente ao selecionar o modo `"DAILY_FULL_EXPORT"` no seletor `frequency`. <br> Obrigatório. <br> <ul><li>Selecione `"AFTER_SEGMENT_EVAL"` para que o trabalho de ativação seja executado imediatamente após a conclusão diária do trabalho de segmentação em lote do Experience Platform. Isso garante que, quando o trabalho de ativação for executado, os perfis mais atualizados sejam exportados para o seu destino.</li><li>Selecione `"SCHEDULED"` para que o trabalho de ativação seja executado em um horário fixado. Isso garante que os dados de perfil do Experience Platform sejam exportados ao mesmo tempo todos os dias, mas os perfis exportados podem não ser os mais atualizados, dependendo se o trabalho de segmentação em lote foi concluído antes do início do trabalho de ativação. Ao selecionar essa opção, você também deve adicionar um `startTime` para indicar em que horário em UTC as exportações diárias devem ocorrer.</li></ul> |
| `endDate` | Somente para *destinos em lote*. Esse campo é necessário somente ao adicionar um público-alvo a um fluxo de dados em destinos de exportação de arquivos em lote, como Amazon S3, SFTP ou Azure Blob. <br> Não aplicável ao selecionar `"exportMode":"DAILY_FULL_EXPORT"` e `"frequency":"ONCE"`. <br> Define a data em que os membros do público-alvo param de ser exportados para o destino. |
| `startTime` | Somente para *destinos em lote*. Esse campo é necessário somente ao adicionar um público-alvo a um fluxo de dados em destinos de exportação de arquivos em lote, como Amazon S3, SFTP ou Azure Blob. <br> Obrigatório. Selecione a hora em que os arquivos que contêm membros do público-alvo devem ser gerados e exportados para o seu destino. |

{style="table-layout:auto"}

>[!TIP]
>
> Consulte [Atualizar componentes de um público em um fluxo de dados](/help/destinations/api/update-destination-dataflows.md#update-segment) para saber como atualizar vários componentes (modelo de nome de arquivo, tempo de exportação etc.) de públicos exportados.

**Resposta**

Procure uma resposta 202 Accepted. Nenhum corpo de resposta é retornado. Para validar se a solicitação estava correta, consulte a próxima etapa, [Validar o fluxo de dados](#validate-dataflow).

## Validar o fluxo de dados {#validate-dataflow}

![Etapa de visão geral das etapas de destino 6](../assets/api/batch-destination/step6.png)

Como etapa final do tutorial, você deve validar se os públicos-alvo e os atributos de perfil foram realmente mapeados corretamente para o fluxo de dados.

Para validar isso, execute a seguinte solicitação do GET:

**Formato da API**

```http
GET /flows
```

**Solicitação**

```shell
curl --location --request PATCH 'https://platform.adobe.io/data/foundation/flowservice/flows/{DATAFLOW_ID}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'Content-Type: application/json' \
--header 'x-sandbox-name: prod' \
--header 'If-Match: "{ETAG}"' 
```

* `{DATAFLOW_ID}`: Usar o fluxo de dados da etapa anterior.
* `{ETAG}`: Usar a marca da etapa anterior.

**Resposta**

A resposta retornada deve incluir no parâmetro `transformations` os públicos-alvo e atributos de perfil enviados na etapa anterior. Um exemplo de parâmetro `transformations` na resposta pode ser semelhante ao mostrado abaixo:

```json
"transformations":[
   {
      "name":"GeneralTransform",
      "params":{
         "profileSelectors":{
            "selectors":[
               {
                  "type":"JSON_PATH",
                  "value":{
                     "path":"homeAddress.countryCode",
                     "operator":"EXISTS",
                     "mapping":{
                        "sourceType":"text/x.schema-path",
                        "source":"homeAddress.countryCode",
                        "destination":"homeAddress.countryCode",
                        "identity":false,
                        "primaryIdentity":false,
                        "functionVersion":0,
                        "copyModeMapping":false,
                        "sourceAttribute":"homeAddress.countryCode",
                        "destinationXdmPath":"homeAddress.countryCode"
                     }
                  }
               },
               {
                  "type":"JSON_PATH",
                  "value":{
                     "path":"person.name.firstName",
                     "operator":"EXISTS",
                     "mapping":{
                        "sourceType":"text/x.schema-path",
                        "source":"person.name.firstName",
                        "destination":"person.name.firstName",
                        "identity":false,
                        "primaryIdentity":false,
                        "functionVersion":0,
                        "copyModeMapping":false,
                        "sourceAttribute":"person.name.firstName",
                        "destinationXdmPath":"person.name.firstName"
                     }
                  }
               },
               {
                  "type":"JSON_PATH",
                  "value":{
                     "path":"person.name.lastName",
                     "operator":"EXISTS",
                     "mapping":{
                        "sourceType":"text/x.schema-path",
                        "source":"person.name.lastName",
                        "destination":"person.name.lastName",
                        "identity":false,
                        "primaryIdentity":false,
                        "functionVersion":0,
                        "copyModeMapping":false,
                        "sourceAttribute":"person.name.lastName",
                        "destinationXdmPath":"person.name.lastName"
                     }
                  }
               },
               {
                  "type":"JSON_PATH",
                  "value":{
                     "path":"personalEmail.address",
                     "operator":"EXISTS",
                     "mapping":{
                        "sourceType":"text/x.schema-path",
                        "source":"personalEmail.address",
                        "destination":"personalEmail.address",
                        "identity":false,
                        "primaryIdentity":false,
                        "functionVersion":0,
                        "copyModeMapping":false,
                        "sourceAttribute":"personalEmail.address",
                        "destinationXdmPath":"personalEmail.address"
                     }
                  }
               },
               {
                  "type":"JSON_PATH",
                  "value":{
                     "path":"segmentMembership.status",
                     "operator":"EXISTS",
                     "mapping":{
                        "sourceType":"text/x.schema-path",
                        "source":"segmentMembership.status",
                        "destination":"segmentMembership.status",
                        "identity":false,
                        "primaryIdentity":false,
                        "functionVersion":0,
                        "copyModeMapping":false,
                        "sourceAttribute":"segmentMembership.status",
                        "destinationXdmPath":"segmentMembership.status"
                     }
                  }
               }
            ],
            "mandatoryFields":[
               "person.name.firstName",
               "person.name.lastName"
            ],
            "primaryFields":[
               {
                  "fieldType":"ATTRIBUTE",
                  "attributePath":"personalEmail.address"
               }
            ]
         },
         "segmentSelectors":{
            "selectors":[
               {
                  "type":"PLATFORM_SEGMENT",
                  "value":{
                     "id":"9f7d37fd-7039-4454-94ef-2b0cd6c3206a",
                     "name":"Interested in Mountain Biking",
                     "filenameTemplate":"%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%",
                     "exportMode":"DAILY_FULL_EXPORT",
                     "schedule":{
                        "frequency":"ONCE",
                        "startDate":"2021-12-20",
                        "startTime":"17:00"
                     },
                     "createTime":"1640016962",
                     "updateTime":"1642534355"
                  }
               },
               {
                  "type":"PLATFORM_SEGMENT",
                  "value":{
                     "id":"25768be6-ebd5-45cc-8913-12fb3f348613",
                     "name":"Loyalty Segment",
                     "filenameTemplate":"%DESTINATION_NAME%_%SEGMENT_ID%_%DATETIME(YYYYMMdd_HHmmss)%",
                     "exportMode":"FIRST_FULL_THEN_INCREMENTAL",
                     "schedule":{
                        "frequency":"EVERY_6_HOURS",
                        "startDate":"2021-12-22",
                        "endDate":"2021-12-31",
                        "startTime":"17:00"
                     },
                     "createTime":"1640016962",
                     "updateTime":"1642534355"
                  }
               }
            ]
         }
      }
   }
]
```

## Manipulação de erros de API {#api-error-handling}

Os endpoints de API neste tutorial seguem os princípios gerais de mensagem de erro da API do Experience Platform. Consulte [códigos de status da API](/help/landing/troubleshooting.md#api-status-codes) e [erros no cabeçalho da solicitação](/help/landing/troubleshooting.md#request-header-errors) no guia de solução de problemas do Experience Platform para obter mais informações sobre como interpretar respostas de erro.

## Próximas etapas {#next-steps}

Ao seguir este tutorial, você conectou com sucesso o Experience Platform a um dos seus destinos de marketing por email baseados em arquivos e configurou um fluxo de dados para o respectivo destino para exportar arquivos de dados. Os dados de saída agora podem ser usados no destino para campanhas por email, publicidade direcionada e muitos outros casos de uso. Consulte as seguintes páginas para obter mais detalhes, como editar fluxos de dados existentes usando a API do Serviço de fluxo:

* [Visão geral dos destinos](../home.md)
* [Visão geral do Catálogo de destinos](../catalog/overview.md)
* [Atualizar fluxos de dados de destino usando a API de serviço de fluxo](../api/update-destination-dataflows.md)
