---
solution: Experience Platform
title: Ative públicos para destinos baseados em arquivo usando a API do Serviço de fluxo
description: Saiba como usar a API do Serviço de fluxo para exportar arquivos com perfis qualificados para destinos de armazenamento na nuvem.
type: Tutorial
exl-id: 62028c7a-3ea9-4004-adb7-5e27bbe904fc
source-git-commit: eb7d1b9c167839db39cbb28bf497edac706c0b6c
workflow-type: tm+mt
source-wordcount: '4911'
ht-degree: 3%

---

# Ative públicos para destinos baseados em arquivo usando a API do Serviço de fluxo

Use os recursos aprimorados de exportação de arquivos para acessar a funcionalidade aprimorada de personalização ao exportar arquivos do Experience Platform:

* [Opções de nomenclatura de arquivo](/help/destinations/ui/activate-batch-profile-destinations.md#file-names) adicionais.
* Capacidade de definir cabeçalhos de arquivos personalizados em seus arquivos exportados por meio da [etapa de mapeamento aprimorado](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).
* Capacidade de selecionar o [tipo de arquivo](/help/destinations/ui/connect-destination.md#file-formatting-and-compression-options) do arquivo exportado.
* [Capacidade de personalizar a formatação de arquivos de dados CSV exportados](/help/destinations/ui/batch-destinations-file-formatting-options.md).

Essa funcionalidade é compatível com os seis cartões de armazenamento em nuvem listados abaixo:

* [[!DNL Azure Data Lake Storage Gen2]](../../destinations/catalog/cloud-storage/adls-gen2.md)
* [[!DNL Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md)
* [[!DNL Google Cloud Storage]](../../destinations/catalog/cloud-storage/google-cloud-storage.md)
* [[!DNL Amazon S3]](../../destinations/catalog/cloud-storage/amazon-s3.md#changelog)
* [[!DNL Azure Blob]](../../destinations/catalog/cloud-storage/azure-blob.md#changelog)
* [[!DNL SFTP]](../../destinations/catalog/cloud-storage/sftp.md#changelog)

Este artigo explica o fluxo de trabalho necessário para usar a [API de Serviço de Fluxo](https://developer.adobe.com/experience-platform-apis/references/destinations/) para exportar perfis qualificados do Adobe Experience Platform para um dos locais de armazenamento na nuvem vinculados acima.

>[!TIP]
>
>Você também pode usar a interface do usuário do Experience Platform para exportar perfis para destinos de armazenamento na nuvem. Leia o [tutorial sobre ativação de destinos baseados em arquivo](/help/destinations/ui/activate-batch-profile-destinations.md) para obter mais informações.

<!--

## API users migration {#api-migration}

If you were already using the Flow Service API to export profiles to the Amazon S3, Azure Blob, or SFTP cloud storage destinations, read the [API migration guide](/help/destinations/api/api-migration-guide-cloud-storage-destinations.md) for necessary migration steps as Adobe transitions users from the legacy destinations to the new destinations. 

-->

## Introdução {#get-started}

![Etapas para ativar públicos destacando a etapa atual em que o usuário está](/help/destinations/assets/api/file-based-segment-export/segment-export-overview.png)

Este manual necessita de uma compreensão funcional dos seguintes componentes da Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): a estrutura padronizada pela qual o [!DNL Experience Platform] organiza os dados de experiência do cliente.
* [[!DNL Segmentation Service]](../../segmentation/api/overview.md): [!DNL Adobe Experience Platform Segmentation Service] permite que você compile públicos e gere públicos no [!DNL Adobe Experience Platform] a partir dos dados do [!DNL Real-Time Customer Profile].
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] fornece sandboxes virtuais que particionam uma única instância do [!DNL Experience Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisa saber para ativar dados para destinos baseados em arquivo no Experience Platform.

### Permissões necessárias {#permissions}

Para exportar perfis, você precisa de **[!UICONTROL Exibir Destinos]**, **[!UICONTROL Ativar Destinos]**, **[!UICONTROL Exibir Perfis]** e **[!UICONTROL Exibir Segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.

Para exportar *identidades*, você precisa da **[!UICONTROL permissão Exibir Gráfico de Identidade]** [controle de acesso](/help/access-control/home.md#permissions). <br> ![Selecione o namespace de identidade realçado no fluxo de trabalho para ativar as audiências para os destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Selecione o namespace de identidade realçado no fluxo de trabalho para ativar as audiências para os destinos."){width="100" zoomable="yes"}

### Leitura de chamadas de API de amostra {#reading-sample-api-calls}

Este tutorial fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e conteúdos de solicitação formatados corretamente. Também fornece exemplos de JSON retornado nas respostas da API. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler chamadas de API de exemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) no guia de solução de problemas [!DNL Experience Platform].

### Colete valores para cabeçalhos obrigatórios e opcionais {#gather-values-headers}

Para fazer chamadas para APIs do [!DNL Experience Platform], primeiro complete o [tutorial de autenticação do Experience Platform](https://www.adobe.com/go/platform-api-authentication-en). Concluir o tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API da [!DNL Experience Platform], conforme mostrado abaixo:

* Autorização: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id `{ORG_ID}`

Os recursos em [!DNL Experience Platform] podem ser isolados em sandboxes virtuais específicas. Em solicitações para [!DNL Experience Platform] APIs, é possível especificar o nome e a ID da sandbox em que a operação ocorrerá. Esses parâmetros são opcionais.

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre sandboxes em [!DNL Experience Platform], consulte a [documentação de visão geral da sandbox](../../sandboxes/home.md).

Todas as solicitações que contêm uma carga (`POST`, `PUT`, `PATCH`) exigem um cabeçalho de tipo de mídia adicional:

* Tipo de conteúdo: `application/json`

### Documentação de referência da API {#api-reference-documentation}

Você pode encontrar a documentação de referência de acompanhamento para todas as operações de API neste tutorial. Consulte a [Documentação da API de Destinos do Flow Service no site da Adobe Developer](https://developer.adobe.com/experience-platform-apis/references/destinations/). Recomendamos que você use este tutorial e a documentação de referência da API em paralelo.

### Glossário {#glossary}

Para obter descrições dos termos que você encontrará neste tutorial de API, leia a [seção de glossário](https://developer.adobe.com/experience-platform-apis/references/destinations/#tag/Glossary) da documentação de referência da API.

## Selecionar destino para o qual exportar públicos {#select-destination}

![Etapas para ativar públicos destacando a etapa atual em que o usuário está](/help/destinations/assets/api/file-based-segment-export/step1.png)

Antes de iniciar o fluxo de trabalho para exportar perfis, identifique a especificação da conexão e as IDs de especificação do fluxo do destino para o qual você pretende exportar públicos. Use a tabela abaixo como referência.

| Destino | Especificação da conexão | Especificação de fluxo |
---------|----------|---------|
| Amazon S3 | `4fce964d-3f37-408f-9778-e597338a21ee` | `1a0514a6-33d4-4c7f-aff8-594799c47549` |
| Armazenamento Azure Blob | `6d6b59bf-fb58-4107-9064-4d246c0e5bb2` | `752d422f-b16f-4f0d-b1c6-26e448e3b388` |
| Azure Data Lake Gen 2(ADLS Gen2) | `be2c3209-53bc-47e7-ab25-145db8b873e1` | `17be2013-2549-41ce-96e7-a70363bec293` |
| Zona de aterrissagem de dados (DLZ) | `10440537-2a7b-4583-ac39-ed38d4b848e8` | `cd2fc47e-e838-4f38-a581-8fff2f99b63a` |
| Google Cloud Storage | `c5d93acb-ea8b-4b14-8f53-02138444ae99` | `585c15c4-6cbf-4126-8f87-e26bff78b657` |
| SFTP | `36965a81-b1c6-401b-99f8-22508f1e6a26` | `fd36aaa4-bf2b-43fb-9387-43785eeeb799` |

{style="table-layout:auto"}

Você precisa dessas IDs para criar várias entidades do serviço de fluxo nas próximas etapas deste tutorial. Você também precisa consultar partes da especificação da conexão para configurar determinadas entidades para que possa recuperar a especificação da conexão das APIs do serviço de fluxo. Veja os exemplos abaixo de recuperação das especificações de conexão para todos os destinos na tabela:

>[!BEGINTABS]

>[!TAB Amazon S3]

**Solicitação**

+++Recuperar [!DNL connection spec] para [!DNL Amazon S3]

```shell
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs/4fce964d-3f37-408f-9778-e597338a21ee' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}'
```

+++

**Resposta**

+++[!DNL Amazon S3] - Especificação da conexão

```json
{
    "items": [
        {
            "id": "4fce964d-3f37-408f-9778-e597338a21ee",
            "name": "Amazon S3",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
//...
```

+++

>[!TAB Armazenamento Azure Blob]

**Solicitação**

+++Recuperar [!DNL connection spec] para [!DNL Azure Blob Storage]

```shell
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs/6d6b59bf-fb58-4107-9064-4d246c0e5bb2' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}'
```

+++

**Resposta**

+++[!DNL Azure Blob Storage] - [!DNL Connection spec]

```json
{
    "items": [
        {
            "id": "6d6b59bf-fb58-4107-9064-4d246c0e5bb2",
            "name": "Azure Blob Storage",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
//...
```

+++

>[!TAB Azure Data Lake Gen 2(ADLS Gen2)]

**Solicitação**

+++Recuperar [!DNL connection spec] para [!DNL Azure Data Lake Gen 2(ADLS Gen2])

```shell
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs/be2c3209-53bc-47e7-ab25-145db8b873e1' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}'
```

+++

**Resposta**

+++[!DNL Azure Data Lake Gen 2(ADLS Gen2)] - [!DNL Connection spec]

```json
{
    "items": [
        {
            "id": "be2c3209-53bc-47e7-ab25-145db8b873e1",
            "name": "Azure Data Lake Gen2",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
//...
```

+++

>[!TAB Zona de Aterrissagem de Dados(DLZ)]

**Solicitação**

+++Recuperar [!DNL connection spec] para [!DNL Data Landing Zone(DLZ)]

```shell
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs/10440537-2a7b-4583-ac39-ed38d4b848e8' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}'
```

+++

**Resposta**

+++[!DNL Data Landing Zone(DLZ)] - [!DNL Connection spec]

```json
{
    "items": [
        {
            "id": "10440537-2a7b-4583-ac39-ed38d4b848e8",
            "name": "Data Landing Zone",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
//...
```

+++

>[!TAB Armazenamento na nuvem do Google]

**Solicitação**

+++Recuperar [!DNL connection spec] para [!DNL Google Cloud Storage]

```shell
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs/c5d93acb-ea8b-4b14-8f53-02138444ae99' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}'
```

+++

**Resposta**

+++[!DNL Google Cloud Storage] - [!DNL Connection spec]

```json
{
    "items": [
        {
            "id": "c5d93acb-ea8b-4b14-8f53-02138444ae99",
            "name": "Google Cloud Storage",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
//...
```

+++

>[!TAB SFTP]

**Solicitação**

+++Recuperar [!DNL connection spec] para SFTP

```shell
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs/36965a81-b1c6-401b-99f8-22508f1e6a26' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}'
```

+++

**Resposta**

+++SFTP - [!DNL Connection spec]

```json
{
    "items": [
        {
            "id": "36965a81-b1c6-401b-99f8-22508f1e6a26",
            "name": "SFTP",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
//...
```

+++

>[!ENDTABS]

Siga as etapas abaixo para configurar um fluxo de dados de exportação de público-alvo para um destino de armazenamento na nuvem. Para algumas etapas, as solicitações e respostas diferem entre os vários destinos de armazenamento na nuvem. Nesses casos, use as guias na página para recuperar as solicitações e respostas específicas ao destino ao qual você deseja se conectar e exportar públicos. Certifique-se de usar o `connection spec` e o `flow spec` corretos para o destino que você está configurando.

## Criar uma conexão com o Source {#create-source-connection}

![Etapas para ativar públicos destacando a etapa atual em que o usuário está](/help/destinations/assets/api/file-based-segment-export/step2.png)

Depois de decidir para qual destino você está exportando públicos, é necessário criar uma conexão de origem. A [conexão de origem](https://developer.adobe.com/experience-platform-apis/references/destinations/#tag/Glossary) representa a conexão com o [repositório de Perfis da Experience Platform](/help/profile/home.md#profile-data-store) interno.

>[!BEGINSHADEBOX]

**Solicitação**

+++Criar conexão de origem - Solicitação

Observe as linhas destacadas com comentários em linha no exemplo de solicitação, que fornecem informações adicionais. Remova os comentários em linha ao copiar e colar a solicitação no terminal de sua escolha.

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
   "name":"Connect to Profile store",
   "description":"Optional",
   "connectionSpec":{
      "id":"8a9c3494-9708-43d7-ae3f-cda01e5030e1", // this connection spec ID is always the same for Source Connections
      "version":"1.0"
   }
}'
```

+++

**Resposta**

+++Criar conexão de origem - Resposta

```json
{
    "id": "900df191-b983-45cd-90d5-4c7a0326d650",
    "etag": "\"0500ebe1-0000-0200-0000-63e28d060000\""
}
```

+++

>[!ENDSHADEBOX]

Uma resposta bem-sucedida retorna a ID (`id`) da conexão de origem recém-criada e um `etag`. Anote a ID da conexão de origem, pois ela será necessária posteriormente ao criar o fluxo de dados.

## Criar uma conexão básica {#create-base-connection}

![Etapas para ativar públicos destacando a etapa atual em que o usuário está](/help/destinations/assets/api/file-based-segment-export/step3.png)

Uma [conexão base](https://developer.adobe.com/experience-platform-apis/references/destinations/#tag/Glossary) armazena com segurança as credenciais no seu destino. Dependendo do tipo de destino, as credenciais necessárias para a autenticação nesse destino podem variar. Para localizar esses parâmetros de autenticação, primeiro recupere o `connection spec` do destino desejado, conforme descrito na seção [Selecione o destino para o qual exportar públicos](#select-destination) e, em seguida, verifique a `authSpec` da resposta. Consulte as guias abaixo para obter as propriedades `authSpec` de todos os destinos com suporte.

>[!BEGINTABS]

>[!TAB Amazon S3]

+++[!DNL Amazon S3] - [!DNL Connection spec] mostrando [!DNL auth spec]

Observe a linha destacada com comentários embutidos no exemplo [!DNL connection spec] abaixo, que fornece informações adicionais sobre onde encontrar os parâmetros de autenticação no [!DNL connection spec].

```json {line-numbers="true" start-line="1" highlight="8"}
{
    "items": [
        {
        "id": "4fce964d-3f37-408f-9778-e597338a21ee",
        "name": "amazon-s3",
        "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
        "version": "1.0",
        "authSpec": [
            {
            "name": "Access Key",
            "type": "KeyBased",
            "spec": {
                "$schema": "http://json-schema.org/draft-07/schema#",
                "description": "Defines auth params required for connecting to amazon-s3",
                "type": "object",
                "properties": {
                "s3AccessKey": {
                    "description": "Access key id",
                    "type": "string",
                    "pattern": "^[A-Z2-7]{20}$"
                },
                "s3SecretKey": {
                    "description": "Secret access key for the user account",
                    "type": "string",
                    "format": "password",
                    "pattern": "^[A-Za-z0-9\\/\\+]{40}$"
                }
                },
                "required": [
                "s3SecretKey",
                "s3AccessKey"
                ]
            }
            },
            {
            "name": "Assumed Role",
            "type": "S3RoleBased",
            "spec": {
                "$schema": "http://json-schema.org/draft-07/schema#",
                "description": "Defines role based auth params required for connecting to amazon-s3",
                "type": "object",
                "properties": {
                "s3Role": {
                    "title": "Role",
                    "description": "S3 role",
                    "type": "string",
                    "format": "password"
                }
                },
                "required": [
                "s3Role"
                ]
            }
            }
        ],
//...
```

+++

>[!TAB Armazenamento Azure Blob]

+++[!DNL Azure Blob Storage] - [!DNL Connection spec] mostrando [!DNL auth spec]

Observe a linha destacada com comentários embutidos no exemplo [!DNL connection spec] abaixo, que fornece informações adicionais sobre onde encontrar os parâmetros de autenticação no [!DNL connection spec].

```json {line-numbers="true" start-line="1" highlight="8"}
{
    "items": [
        {
            "id": "6d6b59bf-fb58-4107-9064-4d246c0e5bb2",
            "name": "Azure Blob Storage",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
            "authSpec": [ // describes the authentication parameters
                {
                    "name": "ConnectionString",
                    "type": "ConnectionString",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "description": "Connection String for Azure Blob based destinations",
                        "type": "object",
                        "properties": {
                            "connectionString": {
                                "description": "connection string for login",
                                "type": "string",
                                "format": "password"
                            }
                        },
                        "required": [
                            "connectionString"
                        ]
                    }
                }
            ],
//...
```

+++


>[!TAB Azure Data Lake Gen 2(ADLS Gen2)]

+++[!DNL Azure Data Lake Gen 2(ADLS Gen2)] - [!DNL Connection spec] mostrando [!DNL auth spec]

Observe a linha destacada com comentários embutidos no exemplo [!DNL connection spec] abaixo, que fornece informações adicionais sobre onde encontrar os parâmetros de autenticação no [!DNL connection spec].

```json {line-numbers="true" start-line="1" highlight="8"}
{
    "items": [
        {
            "id": "be2c3209-53bc-47e7-ab25-145db8b873e1",
            "name": "Azure Data Lake Gen2",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
            "authSpec": [ // describes the authentication parameters
                {
                    "name": "Azure Service Principal Auth",
                    "type": "AzureServicePrincipal",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "description": "defines auth params required for connecting to adlsgen2 using service principal",
                        "type": "object",
                        "properties": {
                            "url": {
                                "description": "Endpoint for Azure Data Lake Storage Gen2.",
                                "type": "string"
                            },
                            "servicePrincipalId": {
                                "description": "Service Principal Id to connect to ADLSGen2.",
                                "type": "string"
                            },
                            "servicePrincipalKey": {
                                "description": "Service Principal Key to connect to ADLSGen2.",
                                "type": "string",
                                "format": "password"
                            },
                            "tenant": {
                                "description": "Tenant information(domain name or tenant ID).",
                                "type": "string"
                            }
                        },
                        "required": [
                            "servicePrincipalKey",
                            "url",
                            "tenant",
                            "servicePrincipalId"
                        ]
                    }
                }
            ],
//...
```

+++


>[!TAB Zona de Aterrissagem de Dados(DLZ)]

+++[!DNL Data Landing Zone(DLZ)] - [!DNL Connection spec] mostrando [!DNL auth spec]

>[!NOTE]
>
>O destino da Data Landing Zone não requer um [!DNL auth spec].

```json
{
    "items": [
        {
            "id": "10440537-2a7b-4583-ac39-ed38d4b848e8",
            "name": "Data Landing Zone",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
            "authSpec": [],
//...
```

+++

>[!TAB Armazenamento na nuvem do Google]

+++[!DNL Google Cloud Storage] - [!DNL Connection spec] mostrando [!DNL auth spec]

Observe a linha destacada com comentários embutidos no exemplo [!DNL connection spec] abaixo, que fornece informações adicionais sobre onde encontrar os parâmetros de autenticação no [!DNL connection spec].

```json {line-numbers="true" start-line="1" highlight="8"}
{
    "items": [
        {
            "id": "c5d93acb-ea8b-4b14-8f53-02138444ae99",
            "name": "Google Cloud Storage",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
            "authSpec": [ // describes the authentication parameters
                {
                    "name": "Google Cloud Storage authentication credentials",
                    "type": "GoogleCloudStorageAuth",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "description": "defines auth params required for connecting to google cloud storage connector.",
                        "type": "object",
                        "properties": {
                            "accessKeyId": {
                                "description": "Access Key Id for the user account",
                                "type": "string"
                            },
                            "secretAccessKey": {
                                "description": "Secret Access Key for the user account",
                                "type": "string",
                                "format": "password"
                            }
                        },
                        "required": [
                            "accessKeyId",
                            "secretAccessKey"
                        ]
                    }
                }
            ],
//...
```

+++

>[!TAB SFTP]

+++SFTP - [!DNL Connection spec] mostrando [!DNL auth spec]

>[!NOTE]
>
>O destino SFTP contém dois itens separados no [!DNL auth spec], pois ele oferece suporte à autenticação de senha e de chave SSH.

Observe a linha destacada com comentários embutidos no exemplo [!DNL connection spec] abaixo, que fornece informações adicionais sobre onde encontrar os parâmetros de autenticação no [!DNL connection spec].

```json {line-numbers="true" start-line="1" highlight="8"}
{
    "items": [
        {
            "id": "36965a81-b1c6-401b-99f8-22508f1e6a26",
            "name": "SFTP",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
            "authSpec": [ // describes the authentication parameters
                {
                    "name": "SFTP with Password",
                    "type": "SFTP",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "description": "defines auth params required for connecting to sftp locations with a password",
                        "type": "object",
                        "properties": {
                            "domain": {
                                "description": "Domain of server",
                                "type": "string"
                            },
                            "username": {
                                "description": "Username",
                                "type": "string"
                            },
                            "password": {
                                "description": "Password",
                                "type": "string",
                                "format": "password"
                            }
                        },
                        "required": [
                            "password",
                            "domain",
                            "username"
                        ]
                    }
                },
                {
                    "name": "SFTP with SSH Key",
                    "type": "SFTP",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "description": "defines auth params required for connecting to sftp locations using SSH Key",
                        "type": "object",
                        "properties": {
                            "domain": {
                                "description": "Domain of server",
                                "type": "string"
                            },
                            "username": {
                                "description": "Username",
                                "type": "string"
                            },
                            "sshKey": {
                                "description": "Base64 string of the private SSH key",
                                "type": "string",
                                "format": "password",
                                "contentEncoding": "base64",
                                "uiAttributes": {
                                    "tooltip": {
                                        "id": "platform_destinations_connect_sftp_ssh",
                                        "fallbackUrl": "http://www.adobe.com/go/destinations-sftp-connection-parameters-en "
                                    }
                                }
                            }
                        },
                        "required": [
                            "sshKey",
                            "domain",
                            "username"
                        ]
                    }
                }
            ],
//...
```

+++

>[!ENDTABS]

Usando as propriedades especificadas na especificação de autenticação (ou seja, `authSpec` da resposta), você pode criar uma conexão base com as credenciais necessárias, específicas para cada tipo de destino, conforme mostrado nos exemplos abaixo:

>[!BEGINTABS]

>[!TAB Amazon S3]

**Solicitação**

+++[!DNL Amazon S3] - Solicitação de conexão básica com autenticação de chave de acesso e chave secreta

>[!TIP]
>
>Para obter informações sobre como obter as credenciais de autenticação necessárias, consulte a seção [autenticar no destino](/help/destinations/catalog/cloud-storage/amazon-s3.md#authenticate) da página da documentação de destino do Amazon S3.

Observe as linhas destacadas com comentários em linha no exemplo de solicitação, que fornecem informações adicionais. Remova os comentários em linha na solicitação ao copiar e colar a solicitação no terminal de sua escolha.

```shell {line-numbers="true" start-line="1" highlight="18"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'accept: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
  "name": "Amazon S3 Base Connection",
  "auth": {
    "specName": "Access Key",
    "params": {
      "s3SecretKey": "<Add secret key>",
      "s3AccessKey": "<Add access key>"
    }
  },
  "connectionSpec": {
    "id": "4fce964d-3f37-408f-9778-e597338a21ee", // Amazon S3 connection spec
    "version": "1.0"
  }
}'
```

+++

+++[!DNL Amazon S3] - Solicitação de conexão base com autenticação de função assumida

>[!TIP]
>
>Para obter informações sobre como obter as credenciais de autenticação necessárias, consulte a seção [autenticar no destino](/help/destinations/catalog/cloud-storage/amazon-s3.md#authenticate) da página da documentação de destino do Amazon S3.

Observe as linhas destacadas com comentários em linha no exemplo de solicitação, que fornecem informações adicionais. Remova os comentários em linha na solicitação ao copiar e colar a solicitação no terminal de sua escolha.

```shell {line-numbers="true" start-line="1" highlight="17"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'accept: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
  "name": "Amazon S3 Base Connection",
  "auth": {
    "specName": "Assumed Role",
    "params": {
      "s3Role": "<Add s3 role>"
    }
  },
  "connectionSpec": {
    "id": "4fce964d-3f37-408f-9778-e597338a21ee", // Amazon S3 connection spec
    "version": "1.0"
  }
}'
```

+++

**Resposta**

+++[!DNL Amazon S3] Resposta de conexão base

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Armazenamento Azure Blob]

**Solicitação**

+++[!DNL Azure Blob Storage] - Solicitação de conexão básica

>[!TIP]
>
>Para obter informações sobre como obter as credenciais de autenticação necessárias, consulte a seção [autenticar no destino](/help/destinations/catalog/cloud-storage/azure-blob.md#authenticate) da página de documentação de destino do Armazenamento de Blob do Azure.

Observe as linhas destacadas com comentários em linha no exemplo de solicitação, que fornecem informações adicionais. Remova os comentários em linha na solicitação ao copiar e colar a solicitação no terminal de sua escolha.

```shell {line-numbers="true" start-line="1" highlight="17"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'accept: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
  "name": "Azure Blob Storage Base Connection",
  "auth": {
    "specName": "ConnectionString",
    "params": {
      "connectionString": "<Add Azure Blob connection string>"
    }
  },
  "connectionSpec": {
    "id": "6d6b59bf-fb58-4107-9064-4d246c0e5bb2", // Azure Blob Storage connection spec
    "version": "1.0"
  }
}'
```

+++

**Resposta**

+++[!DNL Azure Blob Storage] - Resposta da conexão base

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Azure Data Lake Gen 2(ADLS Gen2)]

**Solicitação**

+++[!DNL Azure Data Lake Gen 2(ADLS Gen2)] - Solicitação de conexão básica

>[!TIP]
>
>Para obter informações sobre como obter as credenciais de autenticação necessárias, consulte a seção [autenticar para destino](/help/destinations/catalog/cloud-storage/adls-gen2.md#authenticate) da página de documentação de destino do Azure Data Lake Gen 2(ADLS Gen2).

Observe as linhas destacadas com comentários em linha no exemplo de solicitação, que fornecem informações adicionais. Remova os comentários em linha na solicitação ao copiar e colar a solicitação no terminal de sua escolha.

```shell {line-numbers="true" start-line="1" highlight="20"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'accept: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
  "name": "Azure Data Lake Gen 2(ADLS Gen2) Base Connection",
  "auth": {
    "specName": "Azure Service Principal Auth",
    "params": {
      "servicePrincipalKey": "<Add servicePrincipalKey>",
      "url": "<Add url>",
      "tenant": "<Add tenant>",
      "servicePrincipalId": "<Add servicePrincipalId>"
    }
  },
  "connectionSpec": {
    "id": "be2c3209-53bc-47e7-ab25-145db8b873e1", // Azure Data Lake Gen 2(ADLS Gen2) connection spec
    "version": "1.0"
  }
}'
```

+++

**Resposta**

+++[!DNL Azure Data Lake Gen 2(ADLS Gen2)] - Resposta da conexão base

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Zona de Aterrissagem de Dados(DLZ)]

**Solicitação**

+++[!DNL Data Landing Zone(DLZ)] - Solicitação de conexão básica

>[!TIP]
>
>Nenhuma credencial de autenticação é necessária para o destino da Data Landing Zone. Para obter mais informações, consulte a seção [autenticar no destino](/help/destinations/catalog/cloud-storage/data-landing-zone.md#authenticate) da página de documentação de destino da Zona de Aterrissagem de Dados.

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'accept: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
  "name": "Data Landing Zone(DLZ) Base Connection"
}'
```

+++

**Resposta**

+++[!DNL Data Landing Zone] - Resposta da conexão base

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Armazenamento na nuvem do Google]

**Solicitação**

+++[!DNL Google Cloud Storage] - Solicitação de conexão básica

>[!TIP]
>
>Para obter informações sobre como obter as credenciais de autenticação necessárias, consulte a seção [autenticar no destino](/help/destinations/catalog/cloud-storage/google-cloud-storage.md#authenticate) da página de documentação de destino do Google Cloud Storage.

Observe as linhas destacadas com comentários em linha no exemplo de solicitação, que fornecem informações adicionais. Remova os comentários em linha na solicitação ao copiar e colar a solicitação no terminal de sua escolha.

```shell {line-numbers="true" start-line="1" highlight="18"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'accept: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
  "name": "Google Cloud Storage Base Connection",
  "auth": {
    "specName": "Google Cloud Storage authentication credentials",
    "params": {
      "accessKeyId": "<Add accessKeyId>",
      "secretAccessKey": "<Add secret Access Key>"
    }
  },
  "connectionSpec": {
    "id": "c5d93acb-ea8b-4b14-8f53-02138444ae99", // Google Cloud Storage connection spec
    "version": "1.0"
  }
}'
```

+++

**Resposta**

+++[!DNL Google Cloud Storage] - Resposta da conexão base

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB SFTP]

**Solicitação**

+++SFTP com senha - Solicitação de conexão básica

>[!TIP]
>
>Para obter informações sobre como obter as credenciais de autenticação necessárias, consulte a seção [autenticar no destino](/help/destinations/catalog/cloud-storage/sftp.md#authentication-information) da página de documentação do destino SFTP.

Observe as linhas destacadas com comentários em linha no exemplo de solicitação, que fornecem informações adicionais. Remova os comentários em linha na solicitação ao copiar e colar a solicitação no terminal de sua escolha.

```shell {line-numbers="true" start-line="1" highlight="19"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'accept: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
  "name": "SFTP with password Base Connection",
  "auth": {
    "specName": "SFTP with Password",
    "params": {
      "domain": "<Add domain>",
      "username": "<Add username>",
      "password": "<Add password>",
      "port": "<Add port>"      
    }
  },
  "connectionSpec": {
    "id": "36965a81-b1c6-401b-99f8-22508f1e6a26", // SFTP connection spec
    "version": "1.0"
  }
}'
```

| Propriedade | Descrição |
| --------- | ----------- |
| `specName` | Usar `SFTP with Password`. |
| `domain` | O endereço IP ou o nome de domínio do local de armazenamento SFTP. |
| `username` | O nome de usuário para fazer logon no local de armazenamento SFTP. |
| `password` | A senha para fazer logon no local de armazenamento SFTP. |
| `port` | A porta usada pelo local de armazenamento SFTP. |

{style="table-layout:auto"}

+++

+++SFTP com chave SSH - Solicitação de conexão básica

>[!TIP]
>
>Para obter informações sobre como obter as credenciais de autenticação necessárias, consulte a seção [autenticar no destino](/help/destinations/catalog/cloud-storage/sftp.md#authentication-information) da página de documentação do destino SFTP.

Observe as linhas destacadas com comentários em linha no exemplo de solicitação, que fornecem informações adicionais. Remova os comentários em linha na solicitação ao copiar e colar a solicitação no terminal de sua escolha.

```shell {line-numbers="true" start-line="1" highlight="19"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'accept: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
  "name": "SFTP with SSH key Base Connection",
  "auth": {
    "specName": "SFTP with SSH Key",
    "params": {
      "domain": "<Add domain>",
      "username": "<Add username>",
      "sshKey": "<Add SSH key>",
      "port": "<Add port>"
    }
  },
  "connectionSpec": {
    "id": "36965a81-b1c6-401b-99f8-22508f1e6a26", // SFTP connection spec
    "version": "1.0"
  }
}'
```

| Propriedade | Descrição |
| --------- | ----------- |
| `specName` | Usar `SFTP with Password`. |
| `domain` | O endereço IP ou o nome de domínio do local de armazenamento SFTP. |
| `username` | O nome de usuário para fazer logon no local de armazenamento SFTP. |
| `sshKey` | A chave SSH privada usada para fazer logon no local de armazenamento SFTP. A chave privada deve ser formatada como uma cadeia de caracteres codificada em Base64 e não deve ser protegida por senha. |
| `port` | A porta usada pelo local de armazenamento SFTP. |

{style="table-layout:auto"}

+++

**Resposta**

+++SFTP - Resposta de conexão básica

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!ENDTABS]

### Adicionar criptografia aos arquivos exportados

Como opção, você pode adicionar criptografia aos arquivos exportados. Para fazer isso, você precisa adicionar itens de `encryptionSpecs`. Consulte o exemplo de solicitação abaixo com os parâmetros obrigatórios destacados:


>[!BEGINSHADEBOX]

+++ Exibir especificações de criptografia para destinos de armazenamento na nuvem

```json {line-numbers="true" start-line="1" highlight="26-27"}
           "encryptionSpecs": [
                {
                    "name": "File PGP/GPG Encryption",
                    "type": "FileAsymmetric",
                    "spec": {
                        "$schema": "http://json-schema.org/draft-07/schema#",
                        "description": "Defines parameters required for capturing user's inputs for encryption",
                        "type": "object",
                        "properties": {
                            "publicKey": {
                                "description": "Base64 encoded RSA public key",
                                "type": "string",
                                "contentEncoding": "base64"
                            },
                            "encryptionAlgo": {
                                "description": "Algorithm for encryption.",
                                "type": "string",
                                "default": "PGPGPG",
                                "enum": [
                                    "PGPGPG",
                                    "NONE"
                                ]
                            }
                        },
                        "required": [
                            "encryptionAlgo",
                            "publicKey"
                        ]
                    }
                }
            ]
```

+++ 

**Solicitação**

+++Adicionar criptografia à conexão básica - Solicitação

Observe as linhas destacadas com comentários em linha no exemplo de solicitação, que fornecem informações adicionais. Remova os comentários em linha ao copiar e colar a solicitação no terminal de sua escolha.

```shell {line-numbers="true" start-line="1" highlight="19"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/connections' \
--header 'accept: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--data-raw '{
  "name": "SFTP with SSH key Base Connection",
  "auth": {
    "specName": "SFTP with SSH Key",
    "params": {
      "domain": "<Add domain>",
      "username": "<Add username>",
      "sshKey": "<Add SSH key>"
      }
    },
  "encryptionSpecs":{
     "specName": "Encryption spec",
     "params": {
         "encryptionAlgo":"PGPGPG",
         "publicKey":"<Add public key>"
      }            
    },
  "connectionSpec": {
    "id": "36965a81-b1c6-401b-99f8-22508f1e6a26", // SFTP connection spec
    "version": "1.0"
  }
}'
```

+++

**Resposta**

+++Adicionar criptografia à conexão base - Resposta

```json
{
    "id": "900df191-b983-45cd-90d5-4c7a0326d650",
    "etag": "\"0500ebe1-0000-0200-0000-63e28d060000\""
}
```

+++

>[!ENDSHADEBOX]

Observe a ID de conexão da resposta. Essa ID será necessária na próxima etapa ao criar a conexão de destino.

## Criar uma conexão de destino {#create-target-connection}

![Etapas para ativar públicos destacando a etapa atual em que o usuário está](/help/destinations/assets/api/file-based-segment-export/step4.png)

Em seguida, é necessário criar uma conexão de destino. [As conexões de destino](https://developer.adobe.com/experience-platform-apis/references/destinations/#tag/Glossary) armazenam os parâmetros de exportação para os públicos exportados. Os parâmetros de exportação incluem local de exportação, formato de arquivo, compactação e outros detalhes. Por exemplo, para arquivos CSV, é possível selecionar várias opções de exportação. Obtenha informações abrangentes sobre todas as opções de exportação de CSV compatíveis na [página de configurações de formatação de arquivo](/help/destinations/ui/batch-destinations-file-formatting-options.md).

Consulte as propriedades `targetSpec` fornecidas no `connection spec` do destino para entender as propriedades com suporte para cada tipo de destino. Consulte as guias abaixo para obter as propriedades `targetSpec` de todos os destinos com suporte.

>[!BEGINTABS]

>[!TAB Amazon S3]

+++[!DNL Amazon S3] - [!DNL Connection spec] mostrando parâmetros de conexão de destino

Observe as linhas destacadas com comentários embutidos no exemplo [!DNL connection spec] abaixo, que fornecem informações adicionais sobre onde encontrar os parâmetros [!DNL target spec] na especificação da conexão. Você também pode ver no exemplo abaixo quais parâmetros de destino são *não* aplicáveis a destinos de exportação de público.

```json {line-numbers="true" start-line="1" highlight="10,56"}
{
    "items": [
        {
            "id": "4fce964d-3f37-408f-9778-e597338a21ee",
            "name": "Amazon S3",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
            "authSpec": [...],
            "encryptionSpecs": [...],
            "targetSpec": { //describes the target connection parameters
                "name": "User based target",
                "type": "UserNamespace",
                "spec": {
                    "$schema": "http://json-schema.org/draft-07/schema#",
                    "type": "object",
                    "properties": {
                        "bucketName": {
                            "title": "Bucket name",
                            "description": "Bucket name",
                            "type": "string",
                            "pattern": "(?=^.{3,63}$)(?!^(\\d+\\.)+\\d+$)(^(([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])\\.)*([a-z0-9]|[a-z0-9][a-z0-9\\-]*[a-z0-9])$)",
                            "uiAttributes": {
                                "tooltip": {
                                    "id": "platform_destinations_connect_s3_bucket",
                                    "fallbackUrl": "http://www.adobe.com/go/destinations-amazon-s3-connection-parameters-en"
                                }
                            }
                        },
                        "path": {
                            "title": "Folder path",
                            "description": "Output path for copying files",
                            "type": "string",
                            "pattern": "^[0-9a-zA-Z\/\\!\\-_\\.\\*\\''\\(\\)]*((\\%SEGMENT_(NAME|ID)\\%)?\/?)+$",
                            "uiAttributes": {
                                "tooltip": {
                                    "id": "platform_destinations_connect_s3_folderpath",
                                    "fallbackUrl": "http://www.adobe.com/go/destinations-amazon-s3-connection-parameters-en"
                                }
                            }
                        },
                        "fileType": {
                            "conditional": {
                                "field": "flowSpec.attributes._workflow",
                                "operator": "NOT_CONTAINS",
                                "value": "DATASETS"
                            },
                            "title": "File Type",
                            "description": "Select file format",
                            "type": "string",
                            "enum": [
                                "CSV",
                                "JSON",
                                "PARQUET"
                            ]
                        },
                        "datasetFileType": { // does not apply to audience export destinations
                            "conditional": {
                                "field": "flowSpec.attributes._workflow",
                                "operator": "CONTAINS",
                                "value": "DATASETS"
                            },
                            "title": "File Type",
                            "description": "Select file format",
                            "type": "string",
                            "enum": [
                                "JSON",
                                "PARQUET"
                            ]
                        },
                        "csvOptions": {
                            "conditional": {
                                "field": "fileType",
                                "operator": "EQUALS",
                                "value": "CSV"
                            },
                            "title": "CSV Options",
                            "description": "Select your CSV options",
                            "type": "object",
                            "properties": {
                                "quote": {
                                    "title": "Quote Character",
                                    "description": "Select your Quote character",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "Double Quotes (\")",
                                            "const": "\""
                                        },
                                        {
                                            "title":"Null Character (\\)",
                                            "const": ""
                                        }
                                    ],
                                    "default": ""
                                },
                                "escape": {
                                    "title": "Escape Character",
                                    "description": "Select your Escape character",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "Back Slash (\\)",
                                            "const": "\\"
                                        },
                                        {
                                            "title": "Single Quote (')",
                                            "const": "'"
                                        }
                                    ],
                                    "default": "\\"
                                },
                                "delimiter": {
                                    "title": "Delimiter",
                                    "description": "Select your Delimiter",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "Comma (,)",
                                            "const": ","
                                        },
                                        {
                                            "title": "Tab (\\t)",
                                            "const": "\t"
                                        },
                                        {
                                            "title": "Pipe (|)",
                                            "const": "|"
                                        },
                                        {
                                            "title": "Semicolon (;)",
                                            "const": ";"
                                        },
                                        {
                                            "title": "Colon (:)",
                                            "const": ":"
                                        }
                                    ],
                                    "default": ","
                                },
                                "nullValue": {
                                    "title": "Null Value",
                                    "description": "Select the output value of 'null' fields",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "null",
                                            "const": "null"
                                        },
                                        {
                                            "title": "\"\"",
                                            "const": "\"\""
                                        },
                                        {
                                            "title": "Empty String",
                                            "const": ""
                                        }
                                    ],
                                    "default": "null"
                                },
                                "emptyValue": {
                                    "title": "Empty Value",
                                    "description": "Select the output value of blank fields",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "null",
                                            "const": "null"
                                        },
                                        {
                                            "title": "\"\"",
                                            "const": "\"\""
                                        },
                                        {
                                            "title": "Empty String",
                                            "const": ""
                                        }
                                    ],
                                    "default": ""
                                }
                            }
                        },
                        "compression": {
                            "title": "Compression format",
                            "description": "Select the desired file compression format.",
                            "type": "string",
                            "enum": [
                                "NONE",
                                "GZIP"
                            ]
                        }
                    },
                    "required": [
                        "bucketName",
                        "path",
                        "datasetFileType",
                        "compression",
                        "fileType"
                    ]
                }
//...
```

+++

>[!TAB Armazenamento Azure Blob]

+++[!DNL Azure Blob Storage] - [!DNL Connection spec] mostrando parâmetros de conexão de destino

Observe as linhas destacadas com comentários embutidos no exemplo [!DNL connection spec] abaixo, que fornecem informações adicionais sobre onde encontrar os parâmetros [!DNL target spec] na especificação da conexão. Você também pode ver no exemplo abaixo quais parâmetros de destino são *não* aplicáveis a destinos de exportação de público.

```json {line-numbers="true" start-line="1" highlight="10,44"}
{
    "items": [
        {
            "id": "6d6b59bf-fb58-4107-9064-4d246c0e5bb2",
            "name": "Azure Blob Storage",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
            "authSpec": [...],
            "encryptionSpecs": [...],
            "targetSpec": { // describes the target connection parameters
                "name": "User based target",
                "type": "UserNamespace",
                "spec": {
                    "$schema": "http://json-schema.org/draft-07/schema#",
                    "type": "object",
                    "properties": {
                        "path": {
                            "title": "Folder path",
                            "description": "Output path (relative) indicating where to upload the data",
                            "type": "string",
                            "pattern": "^[0-9a-zA-Z\/\\!\\-_\\.\\*\\'\\(\\)]+$"
                        },
                        "container": {
                            "title": "Container",
                            "description": "Container within the storage where to upload the data",
                            "type": "string",
                            "pattern": "^[a-z0-9](?!.*--)[a-z0-9-]{1,61}[a-z0-9]$"
                        },
                        "fileType": {
                            "conditional": {
                                "field": "flowSpec.attributes._workflow",
                                "operator": "NOT_CONTAINS",
                                "value": "DATASETS"
                            },
                            "title": "File Type",
                            "description": "Select file format",
                            "type": "string",
                            "enum": [
                                "CSV",
                                "JSON",
                                "PARQUET"
                            ]
                        },
                        "datasetFileType": { // does not apply to audience export destinations
                            "conditional": {
                                "field": "flowSpec.attributes._workflow",
                                "operator": "CONTAINS",
                                "value": "DATASETS"
                            },
                            "title": "File Type",
                            "description": "Select file format",
                            "type": "string",
                            "enum": [
                                "JSON",
                                "PARQUET"
                            ]
                        },
                        "csvOptions": {
                            "conditional": {
                                "field": "fileType",
                                "operator": "EQUALS",
                                "value": "CSV"
                            },
                            "title": "CSV Options",
                            "description": "Select your CSV options",
                            "type": "object",
                            "properties": {
                                "quote": {
                                    "title": "Quote Character",
                                    "description": "Select your Quote character",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "Double Quotes (\")",
                                            "const": "\""
                                        },
                                        {
                                            "title":"Null Character (\\)",
                                            "const": ""
                                        }
                                    ],
                                    "default": ""
                                },
                                "escape": {
                                    "title": "Escape Character",
                                    "description": "Select your Escape character",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "Back Slash (\\)",
                                            "const": "\\"
                                        },
                                        {
                                            "title": "Single Quote (')",
                                            "const": "'"
                                        }
                                    ],
                                    "default": "\\"
                                },
                                "delimiter": {
                                    "title": "Delimiter",
                                    "description": "Select your Delimiter",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "Comma (,)",
                                            "const": ","
                                        },
                                        {
                                            "title": "Tab (\\t)",
                                            "const": "\t"
                                        },
                                        {
                                            "title": "Pipe (|)",
                                            "const": "|"
                                        },
                                        {
                                            "title": "Semicolon (;)",
                                            "const": ";"
                                        },
                                        {
                                            "title": "Colon (:)",
                                            "const": ":"
                                        }
                                    ],
                                    "default": ","
                                },
                                "nullValue": {
                                    "title": "Null Value",
                                    "description": "Select the output value of 'null' fields",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "null",
                                            "const": "null"
                                        },
                                        {
                                            "title": "\"\"",
                                            "const": "\"\""
                                        },
                                        {
                                            "title": "Empty String",
                                            "const": ""
                                        }
                                    ],
                                    "default": "null"
                                },
                                "emptyValue": {
                                    "title": "Empty Value",
                                    "description": "Select the output value of blank fields",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "null",
                                            "const": "null"
                                        },
                                        {
                                            "title": "\"\"",
                                            "const": "\"\""
                                        },
                                        {
                                            "title": "Empty String",
                                            "const": ""
                                        }
                                    ],
                                    "default": ""
                                }
                            }
                        },
                        "compression": {
                            "title": "Compression format",
                            "description": "Select the desired file compression format.",
                            "type": "string",
                            "enum": [
                                "NONE",
                                "GZIP"
                            ]
                        }
                    },
                    "required": [
                        "container",
                        "path",
                        "datasetFileType",
                        "compression",
                        "fileType"
                    ]
                }
//...
```

+++


>[!TAB Azure Data Lake Gen 2(ADLS Gen2)]

+++[!DNL Azure Data Lake Gen 2(ADLS Gen2)] - [!DNL Connection spec] mostrando parâmetros de conexão de destino

Observe as linhas destacadas com comentários embutidos no exemplo [!DNL connection spec] abaixo, que fornecem informações adicionais sobre onde encontrar os parâmetros [!DNL target spec] na especificação da conexão. Você também pode ver no exemplo abaixo quais parâmetros de destino são *não* aplicáveis a destinos de exportação de público.

```json {line-numbers="true" start-line="1" highlight="10,22,37"}
{
    "items": [
        {
            "id": "be2c3209-53bc-47e7-ab25-145db8b873e1",
            "name": "Azure Data Lake Gen2",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
            "authSpec": [...],
            "encryptionSpecs": [...],
            "targetSpec": { // describes the target connection parameters
                "name": "User based target",
                "type": "UserNamespace",
                "spec": {
                    "$schema": "http://json-schema.org/draft-07/schema#",
                    "type": "object",
                    "properties": {
                        "path": {
                            "title": "Folder path",
                            "description": "Enter the path to your Azure Data Lake Storage folder",
                            "type": "string"
                        },
                        "fileType": {
                            "conditional": {
                                "field": "flowSpec.attributes._workflow",
                                "operator": "NOT_CONTAINS",
                                "value": "DATASETS"
                            },
                            "title": "File Type",
                            "description": "Select file format",
                            "type": "string",
                            "enum": [
                                "CSV",
                                "JSON",
                                "PARQUET"
                            ]
                        },
                        "datasetFileType": { // does not apply to audience export destinations
                            "conditional": {
                                "field": "flowSpec.attributes._workflow",
                                "operator": "CONTAINS",
                                "value": "DATASETS"
                            },
                            "title": "File Type",
                            "description": "Select file format",
                            "type": "string",
                            "enum": [
                                "JSON",
                                "PARQUET"
                            ]
                        },
                        "csvOptions": {
                            "conditional": {
                                "field": "fileType",
                                "operator": "EQUALS",
                                "value": "CSV"
                            },
                            "title": "CSV Options",
                            "description": "Select your CSV options",
                            "type": "object",
                            "properties": {
                                "quote": {
                                    "title": "Quote Character",
                                    "description": "Select your Quote character",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "Double Quotes (\")",
                                            "const": "\""
                                        },
                                        {
                                            "title":"Null Character (\\)",
                                            "const": ""
                                        }
                                    ],
                                    "default": ""
                                },
                                "escape": {
                                    "title": "Escape Character",
                                    "description": "Select your Escape character",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "Back Slash (\\)",
                                            "const": "\\"
                                        },
                                        {
                                            "title": "Single Quote (')",
                                            "const": "'"
                                        }
                                    ],
                                    "default": "\\"
                                },
                                "delimiter": {
                                    "title": "Delimiter",
                                    "description": "Select your Delimiter",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "Comma (,)",
                                            "const": ","
                                        },
                                        {
                                            "title": "Tab (\\t)",
                                            "const": "\t"
                                        },
                                        {
                                            "title": "Pipe (|)",
                                            "const": "|"
                                        },
                                        {
                                            "title": "Semicolon (;)",
                                            "const": ";"
                                        },
                                        {
                                            "title": "Colon (:)",
                                            "const": ":"
                                        }
                                    ],
                                    "default": ","
                                },
                                "nullValue": {
                                    "title": "Null Value",
                                    "description": "Select the output value of 'null' fields",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "null",
                                            "const": "null"
                                        },
                                        {
                                            "title": "\"\"",
                                            "const": "\"\""
                                        },
                                        {
                                            "title": "Empty String",
                                            "const": ""
                                        }
                                    ],
                                    "default": "null"
                                },
                                "emptyValue": {
                                    "title": "Empty Value",
                                    "description": "Select the output value of blank fields",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "null",
                                            "const": "null"
                                        },
                                        {
                                            "title": "\"\"",
                                            "const": "\"\""
                                        },
                                        {
                                            "title": "Empty String",
                                            "const": ""
                                        }
                                    ],
                                    "default": ""
                                }
                            }
                        },
                        "compression": {
                            "title": "Compression format",
                            "description": "Select the desired file compression format.",
                            "type": "string",
                            "enum": [
                                "NONE",
                                "GZIP"
                            ]
                        }
                    },
                    "required": [
                        "path",
                        "datasetFileType",
                        "compression",
                        "fileType"
                    ]
                }
//...
```

+++

>[!TAB Zona de Aterrissagem de Dados(DLZ)]

+++[!DNL Data Landing Zone(DLZ)] - [!DNL Connection spec] mostrando parâmetros de conexão de destino

Observe as linhas destacadas com comentários embutidos no exemplo [!DNL connection spec] abaixo, que fornecem informações adicionais sobre onde encontrar os parâmetros [!DNL target spec] na especificação da conexão. Você também pode ver no exemplo abaixo quais parâmetros de destino são *não* aplicáveis a destinos de exportação de público.

```json {line-numbers="true" start-line="1" highlight="9,36"}
"items": [
    {
        "id": "10440537-2a7b-4583-ac39-ed38d4b848e8",
        "name": "Data Landing Zone",
        "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
        "version": "1.0",
        "authSpec": [],
        "encryptionSpecs": [],
            "targetSpec": { // describes the target connection parameters
                "name": "User based target",
                "type": "UserNamespace",
                "spec": {
                    "$schema": "http://json-schema.org/draft-07/schema#",
                    "type": "object",
                    "properties": {
                        "path": {
                            "title": "Folder path",
                            "description": "Enter the path to your Azure Data Lake Storage folder",
                            "type": "string"
                        },
                        "fileType": {
                            "conditional": {
                                "field": "flowSpec.attributes._workflow",
                                "operator": "NOT_CONTAINS",
                                "value": "DATASETS"
                            },
                            "title": "File Type",
                            "description": "Select file format",
                            "type": "string",
                            "enum": [
                                "CSV",
                                "JSON",
                                "PARQUET"
                            ]
                        },
                        "datasetFileType": { // does not apply to audience export destinations
                            "conditional": {
                                "field": "flowSpec.attributes._workflow",
                                "operator": "CONTAINS",
                                "value": "DATASETS"
                            },
                            "title": "File Type",
                            "description": "Select file format",
                            "type": "string",
                            "enum": [
                                "JSON",
                                "PARQUET"
                            ]
                        },
                        "csvOptions": {
                            "conditional": {
                                "field": "fileType",
                                "operator": "EQUALS",
                                "value": "CSV"
                            },
                            "title": "CSV Options",
                            "description": "Select your CSV options",
                            "type": "object",
                            "properties": {
                                "quote": {
                                    "title": "Quote Character",
                                    "description": "Select your Quote character",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "Double Quotes (\")",
                                            "const": "\""
                                        },
                                        {
                                            "title":"Null Character (\\)",
                                            "const": ""
                                        }
                                    ],
                                    "default": ""
                                },
                                "escape": {
                                    "title": "Escape Character",
                                    "description": "Select your Escape character",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "Back Slash (\\)",
                                            "const": "\\"
                                        },
                                        {
                                            "title": "Single Quote (')",
                                            "const": "'"
                                        }
                                    ],
                                    "default": "\\"
                                },
                                "delimiter": {
                                    "title": "Delimiter",
                                    "description": "Select your Delimiter",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "Comma (,)",
                                            "const": ","
                                        },
                                        {
                                            "title": "Tab (\\t)",
                                            "const": "\t"
                                        },
                                        {
                                            "title": "Pipe (|)",
                                            "const": "|"
                                        },
                                        {
                                            "title": "Semicolon (;)",
                                            "const": ";"
                                        },
                                        {
                                            "title": "Colon (:)",
                                            "const": ":"
                                        }
                                    ],
                                    "default": ","
                                },
                                "nullValue": {
                                    "title": "Null Value",
                                    "description": "Select the output value of 'null' fields",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "null",
                                            "const": "null"
                                        },
                                        {
                                            "title": "\"\"",
                                            "const": "\"\""
                                        },
                                        {
                                            "title": "Empty String",
                                            "const": ""
                                        }
                                    ],
                                    "default": "null"
                                },
                                "emptyValue": {
                                    "title": "Empty Value",
                                    "description": "Select the output value of blank fields",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "null",
                                            "const": "null"
                                        },
                                        {
                                            "title": "\"\"",
                                            "const": "\"\""
                                        },
                                        {
                                            "title": "Empty String",
                                            "const": ""
                                        }
                                    ],
                                    "default": ""
                                }
                            }
                        },
                        "compression": {
                            "title": "Compression format",
                            "description": "Select the desired file compression format.",
                            "type": "string",
                            "enum": [
                                "NONE",
                                "GZIP"
                            ]
                        }
                    },
                    "required": [
                        "path",
                        "datasetFileType",
                        "compression",
                        "fileType"
                    ]
                }
//...
```

+++

>[!TAB Armazenamento na nuvem do Google]

+++[!DNL Google Cloud Storage] - [!DNL Connection spec] mostrando parâmetros de conexão de destino

Observe as linhas destacadas com comentários embutidos no exemplo [!DNL connection spec] abaixo, que fornecem informações adicionais sobre onde encontrar os parâmetros [!DNL target spec] na especificação da conexão. Você também pode ver no exemplo abaixo quais parâmetros de destino são *não* aplicáveis a destinos de exportação de público.

```json {line-numbers="true" start-line="1" highlight="10,44"}
{
    "items": [
        {
            "id": "c5d93acb-ea8b-4b14-8f53-02138444ae99",
            "name": "Google Cloud Storage",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
            "authSpec": [...],
            "encryptionSpecs": [...],
            "targetSpec": { // describes the target connection parameters
                "name": "User based target",
                "type": "UserNamespace",
                "spec": {
                    "$schema": "http://json-schema.org/draft-07/schema#",
                    "type": "object",
                    "properties": {
                        "bucketName": {
                            "title": "Bucket name",
                            "description": "Bucket name",
                            "type": "string",
                            "pattern": "(?!^goog.*$)(?!^.*g(o|0)(o|0)gle.*$)(((?=^.{3,63}$)(^([a-z0-9]|[a-z0-9][a-z0-9\\-_]*)[a-z0-9]$))|((?=^.{3,222}$)(?!^(\\d+\\.)+\\d+$)(^(([a-z0-9]{1,63}|[a-z0-9][a-z0-9\\-_]{1,61}[a-z0-9])\\.)*([a-z0-9]{1,63}|[a-z0-9][a-z0-9\\-_]{1,61}[a-z0-9])$)))"
                        },
                        "path": {
                            "title": "Folder path",
                            "description": "Output path for copying files",
                            "type": "string",
                            "pattern": "^[0-9a-zA-Z\/\\!\\-_\\.\\*\\''\\(\\)]*((\\%SEGMENT_(NAME|ID)\\%)?\/?)+$"
                        },
                        "fileType": {
                            "conditional": {
                                "field": "flowSpec.attributes._workflow",
                                "operator": "NOT_CONTAINS",
                                "value": "DATASETS"
                            },
                            "title": "File Type",
                            "description": "Select file format",
                            "type": "string",
                            "enum": [
                                "CSV",
                                "JSON",
                                "PARQUET"
                            ]
                        },
                        "datasetFileType": { // does not apply to audience export destinations
                            "conditional": {
                                "field": "flowSpec.attributes._workflow",
                                "operator": "CONTAINS",
                                "value": "DATASETS"
                            },
                            "title": "File Type",
                            "description": "Select file format",
                            "type": "string",
                            "enum": [
                                "JSON",
                                "PARQUET"
                            ]
                        },
                        "csvOptions": {
                            "conditional": {
                                "field": "fileType",
                                "operator": "EQUALS",
                                "value": "CSV"
                            },
                            "title": "CSV Options",
                            "description": "Select your CSV options",
                            "type": "object",
                            "properties": {
                                "quote": {
                                    "title": "Quote Character",
                                    "description": "Select your Quote character",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "Double Quotes (\")",
                                            "const": "\""
                                        },
                                        {
                                            "title":"Null Character (\\)",
                                            "const": ""
                                        }
                                    ],
                                    "default": ""
                                },
                                "escape": {
                                    "title": "Escape Character",
                                    "description": "Select your Escape character",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "Back Slash (\\)",
                                            "const": "\\"
                                        },
                                        {
                                            "title": "Single Quote (')",
                                            "const": "'"
                                        }
                                    ],
                                    "default": "\\"
                                },
                                "delimiter": {
                                    "title": "Delimiter",
                                    "description": "Select your Delimiter",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "Comma (,)",
                                            "const": ","
                                        },
                                        {
                                            "title": "Tab (\\t)",
                                            "const": "\t"
                                        },
                                        {
                                            "title": "Pipe (|)",
                                            "const": "|"
                                        },
                                        {
                                            "title": "Semicolon (;)",
                                            "const": ";"
                                        },
                                        {
                                            "title": "Colon (:)",
                                            "const": ":"
                                        }
                                    ],
                                    "default": ","
                                },
                                "nullValue": {
                                    "title": "Null Value",
                                    "description": "Select the output value of 'null' fields",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "null",
                                            "const": "null"
                                        },
                                        {
                                            "title": "\"\"",
                                            "const": "\"\""
                                        },
                                        {
                                            "title": "Empty String",
                                            "const": ""
                                        }
                                    ],
                                    "default": "null"
                                },
                                "emptyValue": {
                                    "title": "Empty Value",
                                    "description": "Select the output value of blank fields",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "null",
                                            "const": "null"
                                        },
                                        {
                                            "title": "\"\"",
                                            "const": "\"\""
                                        },
                                        {
                                            "title": "Empty String",
                                            "const": ""
                                        }
                                    ],
                                    "default": ""
                                }
                            }
                        },
                        "compression": {
                            "title": "Compression format",
                            "description": "Select the desired file compression format.",
                            "type": "string",
                            "enum": [
                                "NONE",
                                "GZIP"
                            ]
                        }
                    },
                    "required": [
                        "bucketName",
                        "path",
                        "datasetFileType",
                        "compression",
                        "fileType"
                    ]
                }
//...
```

+++

>[!TAB SFTP]

+++SFTP - [!DNL Connection spec] mostrando parâmetros de conexão de destino

Observe as linhas destacadas com comentários embutidos no exemplo [!DNL connection spec] abaixo, que fornecem informações adicionais sobre onde encontrar os parâmetros [!DNL target spec] na especificação da conexão. Você também pode ver no exemplo abaixo quais parâmetros de destino são *não* aplicáveis a destinos de exportação de público.

```json {line-numbers="true" start-line="1" highlight="10,37"}
{
    "items": [
        {
            "id": "36965a81-b1c6-401b-99f8-22508f1e6a26",
            "name": "SFTP",
            "providerId": "14e34fac-d307-11e9-bb65-2a2ae2dbcce4",
            "version": "1.0",
            "authSpec": [...],
            "encryptionSpecs": [...],
            "targetSpec": { // describes the target connection parameters
                "name": "User based target",
                "type": "UserNamespace",
                "spec": {
                    "$schema": "http://json-schema.org/draft-07/schema#",
                    "type": "object",
                    "properties": {
                        "remotePath": {
                            "title": "Folder path",
                            "description": "Enter your folder path",
                            "type": "string"
                        },
                        "fileType": {
                            "conditional": {
                                "field": "flowSpec.attributes._workflow",
                                "operator": "NOT_CONTAINS",
                                "value": "DATASETS"
                            },
                            "title": "File Type",
                            "description": "Select file format",
                            "type": "string",
                            "enum": [
                                "CSV",
                                "JSON",
                                "PARQUET"
                            ]
                        },
                        "datasetFileType": { // does not apply to audience export destinations
                            "conditional": {
                                "field": "flowSpec.attributes._workflow",
                                "operator": "CONTAINS",
                                "value": "DATASETS"
                            },
                            "title": "File Type",
                            "description": "Select file format",
                            "type": "string",
                            "enum": [
                                "JSON",
                                "PARQUET"
                            ]
                        },
                        "csvOptions": {
                            "conditional": {
                                "field": "fileType",
                                "operator": "EQUALS",
                                "value": "CSV"
                            },
                            "title": "CSV Options",
                            "description": "Select your CSV options",
                            "type": "object",
                            "properties": {
                                "quote": {
                                    "title": "Quote Character",
                                    "description": "Select your Quote character",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "Double Quotes (\")",
                                            "const": "\""
                                        },
                                        {
                                            "title":"Null Character (\\)",
                                            "const": ""
                                        }
                                    ],
                                    "default": ""
                                },
                                "escape": {
                                    "title": "Escape Character",
                                    "description": "Select your Escape character",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "Back Slash (\\)",
                                            "const": "\\"
                                        },
                                        {
                                            "title": "Single Quote (')",
                                            "const": "'"
                                        }
                                    ],
                                    "default": "\\"
                                },
                                "delimiter": {
                                    "title": "Delimiter",
                                    "description": "Select your Delimiter",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "Comma (,)",
                                            "const": ","
                                        },
                                        {
                                            "title": "Tab (\\t)",
                                            "const": "\t"
                                        },
                                        {
                                            "title": "Pipe (|)",
                                            "const": "|"
                                        },
                                        {
                                            "title": "Semicolon (;)",
                                            "const": ";"
                                        },
                                        {
                                            "title": "Colon (:)",
                                            "const": ":"
                                        }
                                    ],
                                    "default": ","
                                },
                                "nullValue": {
                                    "title": "Null Value",
                                    "description": "Select the output value of 'null' fields",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "null",
                                            "const": "null"
                                        },
                                        {
                                            "title": "\"\"",
                                            "const": "\"\""
                                        },
                                        {
                                            "title": "Empty String",
                                            "const": ""
                                        }
                                    ],
                                    "default": "null"
                                },
                                "emptyValue": {
                                    "title": "Empty Value",
                                    "description": "Select the output value of blank fields",
                                    "type": "string",
                                    "oneOf": [
                                        {
                                            "title": "null",
                                            "const": "null"
                                        },
                                        {
                                            "title": "\"\"",
                                            "const": "\"\""
                                        },
                                        {
                                            "title": "Empty String",
                                            "const": ""
                                        }
                                    ],
                                    "default": ""
                                }
                            }
                        },
                        "compression": {
                            "title": "Compression format",
                            "description": "Select the desired file compression format.",
                            "type": "string",
                            "enum": [
                                "GZIP",
                                "NONE"
                            ]
                        }
                    },
                    "required": [
                        "remotePath",
                        "datasetFileType",
                        "compression",
                        "fileType"
                    ]
                },
//...
```

+++

>[!ENDTABS]

Usando a especificação acima, você pode criar uma solicitação de conexão de destino específica para seu destino de armazenamento na nuvem desejado, como mostrado nas guias abaixo.

>[!BEGINTABS]

>[!TAB Amazon S3]

**Solicitação**

+++[!DNL Amazon S3] - Solicitação de conexão de destino

>[!TIP]
>
>Para obter informações sobre como obter os parâmetros de destino necessários, consulte a seção [preencher detalhes do destino](/help/destinations/catalog/cloud-storage/amazon-s3.md#destination-details) da página de documentação do destino [!DNL Amazon S3].

Observe as linhas destacadas com comentários em linha no exemplo de solicitação, que fornecem informações adicionais. Remova os comentários em linha na solicitação ao copiar e colar a solicitação no terminal de sua escolha.

```shell {line-numbers="true" start-line="1" highlight="19"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "Amazon S3 Target Connection",
    "baseConnectionId": "<FROM_STEP_CREATE_BASE_CONNECTION>",
    "params": {
        "mode": "Server-to-server",
        "bucketName": "your-bucket-name",
        "path": "folder/subfolder",
        "compression": "NONE",
        "fileType": "JSON",
        "includeFileManifest": true // Include this parameter if you want to enable manifest file generation for your destination
    },
    "connectionSpec": {
        "id": "4fce964d-3f37-408f-9778-e597338a21ee", // Amazon S3 connection spec id
        "version": "1.0"
    }
}'
```

+++

+++[!DNL Amazon S3] - Solicitação de conexão de destino com opções CSV

>[!TIP]
>
>Para obter informações abrangentes sobre as opções de CSV disponíveis para exportação de arquivos, consulte a [página de configurações de formatação de arquivo](/help/destinations/ui/batch-destinations-file-formatting-options.md).

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
   "name":"Amazon S3 Target Connection",
   "baseConnectionId":"<FROM_STEP_CREATE_BASE_CONNECTION>",
   "params":{
      "mode":"Server-to-server",
      "bucketName":"your-bucket-name",
      "path":"folder/subfolder",
      "compression":"GZIP",
      "fileType":"CSV",
      "includeFileManifest": true, //Include this parameter if you want to enable manifest file generation for your destination
      "csvOptions":{
         "nullValue":"null",
         "emptyValue":"",
         "escape":"\\",
         "quote":"",
         "delimiter":","
      }
   },
   "connectionSpec":{
      "id":"4fce964d-3f37-408f-9778-e597338a21ee",
      "version":"1.0"
   }
}'
```

+++

**Resposta**

+++Conexão do Target - Resposta

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Armazenamento Azure Blob]

**Solicitação**

+++[!DNL Azure Blob Storage] - Solicitação de conexão de destino

>[!TIP]
>
>Para obter informações sobre como obter os parâmetros de destino necessários, consulte a seção [preencher detalhes do destino](/help/destinations/catalog/cloud-storage/azure-blob.md#destination-details) da página de documentação do destino [!DNL Azure Blob Storage].

Observe as linhas destacadas com comentários em linha no exemplo de solicitação, que fornecem informações adicionais. Remova os comentários em linha na solicitação ao copiar e colar a solicitação no terminal de sua escolha.

```shell {line-numbers="true" start-line="1" highlight="19"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "Azure Blob Storage Target Connection",
    "baseConnectionId": "<FROM_STEP_CREATE_BASE_CONNECTION>",
    "params": {
        "mode": "Server-to-server",
        "container": "your-container-name",
        "path": "folder/subfolder",
        "compression": "NONE",
        "fileType": "JSON",
        "includeFileManifest": true // Include this parameter if you want to enable manifest file generation for your destination
    },
    "connectionSpec": {
        "id": "6d6b59bf-fb58-4107-9064-4d246c0e5bb2", // Azure Blob Storage connection spec id
        "version": "1.0"
    }
}'
```

+++

+++[!DNL Azure Blob Storage] - Solicitação de conexão de destino com opções CSV

>[!TIP]
>
>Para obter informações abrangentes sobre as opções de CSV disponíveis para exportação de arquivos, consulte a [página de configurações de formatação de arquivo](/help/destinations/ui/batch-destinations-file-formatting-options.md).

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
   "name":"Azure Blob Storage Target Connection",
   "baseConnectionId":"<FROM_STEP_CREATE_BASE_CONNECTION>",
   "params":{
      "mode":"Server-to-server",
      "bucketName":"your-bucket-name",
      "path":"folder/subfolder",
      "compression":"GZIP",
      "fileType":"CSV",
      "includeFileManifest": true, //Include this parameter if you want to enable manifest file generation for your destination
      "csvOptions":{
         "nullValue":"null",
         "emptyValue":"",
         "escape":"\\",
         "quote":"",
         "delimiter":","
      }
   },
   "connectionSpec":{
      "id":"6d6b59bf-fb58-4107-9064-4d246c0e5bb2",
      "version":"1.0"
   }
}'
```

+++

**Resposta**

+++Conexão do Target - Resposta

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Azure Data Lake Gen 2(ADLS Gen2)]

**Solicitação**

+++[!DNL Azure Data Lake Gen 2(ADLS Gen2)] - Solicitação de conexão de destino

>[!TIP]
>
>Para obter informações sobre como obter os parâmetros de destino necessários, consulte a seção [preencher detalhes do destino](/help/destinations/catalog/cloud-storage/adls-gen2.md#destination-details) da página de documentação do Azure [!DNL Data Lake Gen 2(ADLS Gen2)].

Observe as linhas destacadas com comentários em linha no exemplo de solicitação, que fornecem informações adicionais. Remova os comentários em linha na solicitação ao copiar e colar a solicitação no terminal de sua escolha.

```shell {line-numbers="true" start-line="1" highlight="18"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "Azure Data Lake Gen 2(ADLS Gen2) Target Connection",
    "baseConnectionId": "<FROM_STEP_CREATE_BASE_CONNECTION>",
    "params": {
        "mode": "Server-to-server",
        "path": "folder/subfolder",
        "compression": "NONE",
        "fileType": "JSON",
        "includeFileManifest": true // Include this parameter if you want to enable manifest file generation for your destination
    },
    "connectionSpec": {
        "id": "be2c3209-53bc-47e7-ab25-145db8b873e1", // Azure Data Lake Gen 2(ADLS Gen2) connection spec id
        "version": "1.0"
    }
}'
```

+++

+++[!DNL Azure Data Lake Gen 2(ADLS Gen2)] - Solicitação de conexão de destino com opções CSV

>[!TIP]
>
>Para obter informações abrangentes sobre as opções de CSV disponíveis para exportação de arquivos, consulte a [página de configurações de formatação de arquivo](/help/destinations/ui/batch-destinations-file-formatting-options.md).

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
   "name":"Azure Data Lake Gen 2(ADLS Gen2)",
   "baseConnectionId":"<FROM_STEP_CREATE_BASE_CONNECTION>",
   "params":{
      "mode":"Server-to-server",
      "bucketName":"your-bucket-name",
      "path":"folder/subfolder",
      "compression":"GZIP",
      "fileType":"CSV",
      "includeFileManifest": true, //Include this parameter if you want to enable manifest file generation for your destination
      "csvOptions":{
         "nullValue":"null",
         "emptyValue":"",
         "escape":"\\",
         "quote":"",
         "delimiter":","
      }
   },
   "connectionSpec":{
      "id":"be2c3209-53bc-47e7-ab25-145db8b873e1",
      "version":"1.0"
   }
}'
```

+++

**Resposta**

+++Conexão do Target - Resposta

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Zona de Aterrissagem de Dados(DLZ)]

**Solicitação**

+++[!DNL Data Landing Zone] - Solicitação de conexão de destino

>[!TIP]
>
>Para obter informações sobre como obter os parâmetros de destino necessários, consulte a seção [preencher detalhes do destino](/help/destinations/catalog/cloud-storage/data-landing-zone.md#destination-details) da página de documentação do destino [!DNL Data Landing Zone].

Observe as linhas destacadas com comentários em linha no exemplo de solicitação, que fornecem informações adicionais. Remova os comentários em linha na solicitação ao copiar e colar a solicitação no terminal de sua escolha.

```shell {line-numbers="true" start-line="1" highlight="18"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "Data Landing Zone Target Connection",
    "baseConnectionId": "<FROM_STEP_CREATE_BASE_CONNECTION>",
    "params": {
        "mode": "Server-to-server",
        "path": "folder/subfolder",
        "compression": "NONE",
        "fileType": "JSON",
        "includeFileManifest": true // Include this parameter if you want to enable manifest file generation for your destination
    },
    "connectionSpec": {
        "id": "10440537-2a7b-4583-ac39-ed38d4b848e8", // Data Landing Zone connection spec id
        "version": "1.0"
    }
}'
```

+++

+++[!DNL Data Landing Zone] - Solicitação de conexão de destino com opções CSV

>[!TIP]
>
>Para obter informações abrangentes sobre as opções de CSV disponíveis para exportação de arquivos, consulte a [página de configurações de formatação de arquivo](/help/destinations/ui/batch-destinations-file-formatting-options.md).

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
   "name":"Data Landing Zone Target Connection",
   "baseConnectionId":"<FROM_STEP_CREATE_BASE_CONNECTION>",
   "params":{
      "mode":"Server-to-server",
      "bucketName":"your-bucket-name",
      "path":"folder/subfolder",
      "compression":"GZIP",
      "fileType":"CSV",
      "includeFileManifest": true, //Include this parameter if you want to enable manifest file generation for your destination
      "csvOptions":{
         "nullValue":"null",
         "emptyValue":"",
         "escape":"\\",
         "quote":"",
         "delimiter":","
      }
   },
   "connectionSpec":{
      "id":"10440537-2a7b-4583-ac39-ed38d4b848e8",
      "version":"1.0"
   }
}'
```

+++

**Resposta**

+++Conexão do Target - Resposta

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Armazenamento na nuvem do Google]

**Solicitação**

+++[!DNL Google Cloud Storage] - Solicitação de conexão de destino

>[!TIP]
>
>Para obter informações sobre como obter os parâmetros de destino necessários, consulte a seção [preencher detalhes do destino](/help/destinations/catalog/cloud-storage/google-cloud-storage.md#destination-details) da página de documentação do destino [!DNL Google Cloud Storage].

Observe as linhas destacadas com comentários em linha no exemplo de solicitação, que fornecem informações adicionais. Remova os comentários em linha na solicitação ao copiar e colar a solicitação no terminal de sua escolha.

```shell {line-numbers="true" start-line="1" highlight="19"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "Google Cloud Storage Target Connection",
    "baseConnectionId": "<FROM_STEP_CREATE_BASE_CONNECTION>",
    "params": {
        "mode": "Server-to-server",
        "bucketName": "your-bucket-name",
        "path": "folder/subfolder",
        "compression": "NONE",
        "fileType": "JSON",
        "includeFileManifest": true // Include this parameter if you want to enable manifest file generation for your destination
    },
    "connectionSpec": {
        "id": "c5d93acb-ea8b-4b14-8f53-02138444ae99", // Google Cloud Storage connection spec id
        "version": "1.0"
    }
}'
```

+++

+++[!DNL Google Cloud Storage] - Solicitação de conexão de destino com opções CSV

>[!TIP]
>
>Para obter informações abrangentes sobre as opções de CSV disponíveis para exportação de arquivos, consulte a [página de configurações de formatação de arquivo](/help/destinations/ui/batch-destinations-file-formatting-options.md).

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
   "name":"Google Cloud Storage Target Connection",
   "baseConnectionId":"<FROM_STEP_CREATE_BASE_CONNECTION>",
   "params":{
      "mode":"Server-to-server",
      "bucketName":"your-bucket-name",
      "path":"folder/subfolder",
      "compression":"GZIP",
      "fileType":"CSV",
      "includeFileManifest": true, //Include this parameter if you want to enable manifest file generation for your destination
      "csvOptions":{
         "nullValue":"null",
         "emptyValue":"",
         "escape":"\\",
         "quote":"",
         "delimiter":","
      }
   },
   "connectionSpec":{
      "id":"c5d93acb-ea8b-4b14-8f53-02138444ae99",
      "version":"1.0"
   }
}'
```

+++

**Resposta**

+++Conexão do Target - Resposta

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB SFTP]

**Solicitação**

+++SFTP - Solicitação de conexão do Target

>[!TIP]
>
>Para obter informações sobre como obter os parâmetros de destino necessários, consulte a seção [preencher detalhes do destino](/help/destinations/catalog/cloud-storage/google-cloud-storage.md#destination-details) da página de documentação do SFTP de destino.

Observe as linhas destacadas com comentários em linha no exemplo de solicitação, que fornecem informações adicionais. Remova os comentários em linha na solicitação ao copiar e colar a solicitação no terminal de sua escolha.

```shell {line-numbers="true" start-line="1" highlight="18"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "SFTP Target Connection",
    "baseConnectionId": "<FROM_STEP_CREATE_BASE_CONNECTION>",
    "params": {
        "mode": "Server-to-server",
        "remotePath": "folder/subfolder",
        "compression": "NONE",
        "fileType": "JSON",
        "includeFileManifest": true // Include this parameter if you want to enable manifest file generation for your destination
    },
    "connectionSpec": {
        "id": "36965a81-b1c6-401b-99f8-22508f1e6a26", // SFTP connection spec id
        "version": "1.0"
    }
}'
```

+++

+++SFTP - Solicitação de conexão do Target com opções CSV

>[!TIP]
>
>Para obter informações abrangentes sobre as opções de CSV disponíveis para exportação de arquivos, consulte a [página de configurações de formatação de arquivo](/help/destinations/ui/batch-destinations-file-formatting-options.md).

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
   "name":"SFTP Target Connection",
   "baseConnectionId":"<FROM_STEP_CREATE_BASE_CONNECTION>",
   "params":{
      "mode":"Server-to-server",
      "bucketName":"your-bucket-name",
      "path":"folder/subfolder",
      "compression":"GZIP",
      "fileType":"CSV",
      "includeFileManifest": true, //Include this parameter if you want to enable manifest file generation for your destination
      "csvOptions":{
         "nullValue":"null",
         "emptyValue":"",
         "escape":"\\",
         "quote":"",
         "delimiter":","
      }
   },
   "connectionSpec":{
      "id":"36965a81-b1c6-401b-99f8-22508f1e6a26",
      "version":"1.0"
   }
}'
```

+++

**Resposta**

+++Conexão do Target - Resposta

```json
{
    "id": "12401496-2573-4ca7-8137-fef1aeb9dd4c",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!ENDTABS]

Anote o `target connection ID` da resposta. Essa ID será necessária na próxima etapa, ao criar o fluxo de dados para exportar públicos.

Uma resposta bem-sucedida retorna a ID (`id`) da conexão de origem de destino recém-criada e um `etag`. Anote a ID de conexão de destino, pois ela será necessária posteriormente ao criar o fluxo de dados.

## Criar um fluxo de dados {#create-dataflow}

![Etapas para ativar públicos destacando a etapa atual em que o usuário está](/help/destinations/assets/api/file-based-segment-export/step5.png)

A próxima etapa na configuração de destino é criar um fluxo de dados. Um [fluxo de dados](https://developer.adobe.com/experience-platform-apis/references/destinations/#tag/Glossary) une entidades criadas anteriormente e também fornece opções para configurar o agendamento de exportação de público. Para criar o fluxo de dados, use as cargas abaixo, dependendo do destino do armazenamento na nuvem desejado, e substitua as IDs de entidade de fluxo das etapas anteriores. Observe que, nessa etapa, você não está adicionando informações relacionadas ao mapeamento de atributo ou identidade para o fluxo de dados. Isso seguirá na próxima etapa.

>[!BEGINTABS]

>[!TAB Amazon S3]

**Solicitação**

+++Criar fluxo de dados de exportação de público para [!DNL Amazon S3] destino - Solicitação

Observe as linhas destacadas com comentários em linha no exemplo de solicitação, que fornecem informações adicionais. Remova os comentários em linha na solicitação ao copiar e colar a solicitação no terminal de sua escolha.

```shell {line-numbers="true" start-line="1" highlight="12,22-25"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/flows' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "Activate audiences to an Amazon S3 cloud storage destination",
    "description": "This operation creates a dataflow to export audiences to an Amazon S3 cloud storage destination",
    "flowSpec": {
        "id": "1a0514a6-33d4-4c7f-aff8-594799c47549", // Amazon S3 flow spec ID
        "version": "1.0"
    },
    "sourceConnectionIds": [
        "<FROM_STEP_CREATE_SOURCE_CONNECTION>"
    ],
    "targetConnectionIds": [
        "<FROM_STEP_CREATE_TARGET_CONNECTION>"
    ],
    "transformations": []
}'
```

+++

**Resposta**

+++Criar fluxo de dados - Resposta

```json
{
    "id": "eb54b3b3-3949-4f12-89c8-64eafaba858f",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Armazenamento Azure Blob]

**Solicitação**

+++Criar fluxo de dados de exportação de público para [!DNL Azure Blob Storage] destino - Solicitação

Observe as linhas destacadas com comentários em linha no exemplo de solicitação, que fornecem informações adicionais. Remova os comentários em linha na solicitação ao copiar e colar a solicitação no terminal de sua escolha.

```shell {line-numbers="true" start-line="1" highlight="12,22-25"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/flows' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "Activate audiences to an Azure Blob Storage cloud storage destination",
    "description": "This operation creates a dataflow to export audiences to an Azure Blob Storage cloud storage destination",
    "flowSpec": {
        "id": "752d422f-b16f-4f0d-b1c6-26e448e3b388", // Azure Blob Storage flow spec ID
        "version": "1.0"
    },
    "sourceConnectionIds": [
        "<FROM_STEP_CREATE_SOURCE_CONNECTION>"
    ],
    "targetConnectionIds": [
        "<FROM_STEP_CREATE_TARGET_CONNECTION>"
    ],
    "transformations": [
        {
        "name": "GeneralTransform",
        "params": {
            "mandatoryFields": [],
            "primaryFields": [],
            "profileMapping": {},
            "segmentSelectors": {
            "selectors": []
            }
        }
        }
    ]
}'
```

+++

**Resposta**

+++Criar fluxo de dados - Resposta

```json
{
    "id": "eb54b3b3-3949-4f12-89c8-64eafaba858f",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Azure Data Lake Gen 2(ADLS Gen2)]

**Solicitação**

+++Criar fluxo de dados de exportação de público para [!DNL Azure Data Lake Gen 2(ADLS Gen2)] destino - Solicitação

Observe as linhas destacadas com comentários em linha no exemplo de solicitação, que fornecem informações adicionais. Remova os comentários em linha na solicitação ao copiar e colar a solicitação no terminal de sua escolha.

```shell {line-numbers="true" start-line="1" highlight="12,22-25"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/flows' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "Activate audiences to an Azure Data Lake Gen 2(ADLS Gen2) cloud storage destination",
    "description": "This operation creates a dataflow to export audiences to an Azure Data Lake Gen 2(ADLS Gen2) cloud storage destination",
    "flowSpec": {
        "id": "17be2013-2549-41ce-96e7-a70363bec293", // Azure Data Lake Gen 2(ADLS Gen2) flow spec ID
        "version": "1.0"
    },
    "sourceConnectionIds": [
        "<FROM_STEP_CREATE_SOURCE_CONNECTION>"
    ],
    "targetConnectionIds": [
        "<FROM_STEP_CREATE_TARGET_CONNECTION>"
    ],
    "transformations": []
}'
```

+++

**Resposta**

+++Criar fluxo de dados - Resposta

```json
{
    "id": "eb54b3b3-3949-4f12-89c8-64eafaba858f",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Zona de Aterrissagem de Dados(DLZ)]

**Solicitação**

+++Criar fluxo de dados de exportação de público para [!DNL Data Landing Zone] destino - Solicitação

Observe as linhas destacadas com comentários em linha no exemplo de solicitação, que fornecem informações adicionais. Remova os comentários em linha na solicitação ao copiar e colar a solicitação no terminal de sua escolha.

```shell {line-numbers="true" start-line="1" highlight="12,22-25"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/flows' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "Activate audiences to a Data Landing Zone cloud storage destination",
    "description": "This operation creates a dataflow to export audiences to a Data Landing Zone cloud storage destination",
    "flowSpec": {
        "id": "cd2fc47e-e838-4f38-a581-8fff2f99b63a", // Data Landing Zone flow spec ID
        "version": "1.0"
    },
    "sourceConnectionIds": [
        "<FROM_STEP_CREATE_SOURCE_CONNECTION>"
    ],
    "targetConnectionIds": [
        "<FROM_STEP_CREATE_TARGET_CONNECTION>"
    ],
    "transformations": []
}'
```

+++

**Resposta**

+++Criar fluxo de dados - Resposta

```json
{
    "id": "eb54b3b3-3949-4f12-89c8-64eafaba858f",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB Armazenamento na nuvem do Google]

**Solicitação**

+++Criar fluxo de dados de exportação de público para [!DNL Google Cloud Storage] destino - Solicitação

Observe as linhas destacadas com comentários em linha no exemplo de solicitação, que fornecem informações adicionais. Remova os comentários em linha na solicitação ao copiar e colar a solicitação no terminal de sua escolha.

```shell {line-numbers="true" start-line="1" highlight="12,22-25"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/flows' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "Activate audiences to a Google Cloud Storage cloud storage destination",
    "description": "This operation creates a dataflow to export audiences to a Google Cloud Storage destination",
    "flowSpec": {
        "id": "585c15c4-6cbf-4126-8f87-e26bff78b657", // Google Cloud Storage flow spec ID
        "version": "1.0"
    },
    "sourceConnectionIds": [
        "<FROM_STEP_CREATE_SOURCE_CONNECTION>"
    ],
    "targetConnectionIds": [
        "<FROM_STEP_CREATE_TARGET_CONNECTION>"
    ],
    "transformations": []
}'
```

+++

**Resposta**

+++Criar fluxo de dados - Resposta

```json
{
    "id": "eb54b3b3-3949-4f12-89c8-64eafaba858f",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!TAB SFTP]

**Solicitação**

+++Criar fluxo de dados de exportação de público para destino SFTP - Solicitação

Observe as linhas destacadas com comentários em linha no exemplo de solicitação, que fornecem informações adicionais. Remova os comentários em linha na solicitação ao copiar e colar a solicitação no terminal de sua escolha.

```shell {line-numbers="true" start-line="1" highlight="12,22-25"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/flowservice/flows' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw '{
    "name": "Activate audiences to an SFTP cloud storage destination",
    "description": "This operation creates a dataflow to export audiences to an SFTP cloud storage destination",
    "flowSpec": {
        "id": "fd36aaa4-bf2b-43fb-9387-43785eeeb799", // SFTP flow spec ID
        "version": "1.0"
    },
    "sourceConnectionIds": [
        "<FROM_STEP_CREATE_SOURCE_CONNECTION>"
    ],
    "targetConnectionIds": [
        "<FROM_STEP_CREATE_TARGET_CONNECTION>"
    ],
    "transformations": []
}'
```

+++

**Resposta**

+++Criar fluxo de dados - Resposta

```json
{
    "id": "eb54b3b3-3949-4f12-89c8-64eafaba858f",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!ENDTABS]

Observe a ID de fluxo de dados na resposta. Essa ID será necessária em etapas posteriores.

### Adicionar públicos-alvo à exportação

Nesta etapa, também é possível selecionar quais públicos-alvo você deseja exportar para o destino. Para obter informações abrangentes sobre esta etapa e o formato da solicitação para adicionar um público-alvo ao fluxo de dados, veja os exemplos na seção [Atualizar um fluxo de dados de destino](https://developer.adobe.com/experience-platform-apis/references/destinations/#tag/Dataflows/operation/patchFlowById) da documentação de referência da API.


## Configurar mapeamento de atributo e identidade {#attribute-and-identity-mapping}

![Etapas para ativar públicos destacando a etapa atual em que o usuário está](/help/destinations/assets/api/file-based-segment-export/step6.png)

Depois de criar o fluxo de dados, é necessário configurar o mapeamento dos atributos e identidades que deseja exportar. Isso consiste em três etapas, listadas abaixo:

1. Criar um esquema de entrada
2. Criar um esquema de saída
3. Configurar um conjunto de mapeamento para conectar os esquemas criados

Por exemplo, para obter o mapeamento a seguir mostrado na interface do usuário do, seria necessário percorrer as três etapas listadas acima e detalhadas nos próximos cabeçalhos.

![Exemplo de etapa de mapeamento](/help/destinations/assets/api/file-based-segment-export/mapping-example.png)

### Criar um esquema de entrada

Para criar um esquema de entrada, primeiro é necessário recuperar o [esquema de união](/help/profile/ui/union-schema.md) e as identidades que podem ser exportadas para o destino. Este é o esquema de atributos e identidades que você pode selecionar como mapeamento de origem.

![Gravação mostrando as opções de atributo e identidade na exibição de campo de origem selecionada](/help/destinations/assets/api/file-based-segment-export/select-source-field.gif)

Veja abaixo exemplos de solicitações e respostas para recuperar atributos e identidades.

>[!BEGINSHADEBOX]

**Solicitação para obter atributos**

+++Obter atributos disponíveis do seu esquema de união - Solicitação

```shell
curl --location --request GET 'https://platform.adobe.io/data/core/ups/config/entityTypes/_xdm.context.profile?property=fullSchema==true&property=includeRelationshipDescriptors==true' \ 
--header 'x-gw-ims-org-id: {ORG_ID}' \ 
--header 'x-api-key: {API_KEY}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \ 
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
```

+++

**Resposta**

+++Obter atributos disponíveis do esquema de união - Resposta

A resposta abaixo foi encurtada por questões de brevidade.

```json
       "person": {
            "title": "Person",
            "description": "An individual actor, contact, or owner.",
            "meta:referencedFrom": [
                "https://ns.adobe.com/xdm/context/person"
            ],
            "type": "object",
            "meta:xdmType": "object",
            "properties": {
                "birthDate": {
                    "meta:xdmType": "date",
                    "type": "string",
                    "format": "date",
                    "title": "Birth date(YYYY-MM-DD)",
                    "description": "The full date a person was born."
                },
                "birthDayAndMonth": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "title": "Birth date (MM-DD)",
                    "description": "The day and month a person was born, in the format MM-DD. This field should be used when the day and month of a person's birth is known, but not the year."
                },
                "birthYear": {
                    "meta:xdmType": "short",
                    "type": "integer",
                    "minimum": 1,
                    "maximum": 32767,
                    "title": "Birth year",
                    "description": "The year a person was born including the century, for example, 1983.  This field should be used when only the person's age is known, not the full birth date."
                },
                "gender": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "title": "Gender",
                    "description": "Gender identity of the person.\n",
                    "enum": [
                        "male",
                        "female",
                        "not_specified",
                        "non_specific"
                    ],
                    "meta:enum": {
                        "male": "Male",
                        "female": "Female",
                        "not_specified": "Not Specified",
                        "non_specific": "Non-specific"
                    },
                    "default": "not_specified"
                },
                "maritalStatus": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "title": "Marital Status",
                    "description": "Describes a person's relationship with a significant other.",
                    "enum": [
                        "married",
                        "single",
                        "divorced",
                        "widowed",
                        "not_specified"
                    ],
                    "meta:enum": {
                        "divorced": "Divorced",
                        "not_specified": "Not Specified",
                        "married": "Married",
                        "single": "Single",
                        "widowed": "Widowed"
                    },
                    "default": "not_specified"
                },
                "name": {
                    "title": "Full name",
                    "description": "The person's full name.",
                    "meta:referencedFrom": [
                        "https://ns.adobe.com/xdm/context/person-name"
                    ],
                    "type": "object",
                    "meta:xdmType": "object",
                    "properties": {
                        "courtesyTitle": {
                            "type": "string",
                            "meta:xdmType": "string",
                            "title": "Courtesy title",
                            "description": "Normally an abbreviation of a persons title, honorific, or salutation. The `courtesyTitle` is used in front of full or last name in opening texts. For example, Mr. Miss. or Dr."
                        },
                        "firstName": {
                            "type": "string",
                            "meta:xdmType": "string",
                            "title": "First name",
                            "description": "The first audience of the name in the writing order most commonly accepted in the language of the name. In many cultures this is the preferred personal or given name. The `firstName` and `lastName` properties have been introduced to maintain compatibility with existing systems that model names in a simplified, non-semantic, and non-internationalizable way. Using `xdm:fullName` is always preferable."
                        },
                        "fullName": {
                            "type": "string",
                            "meta:xdmType": "string",
                            "title": "Full name",
                            "description": "The full name of the person, in writing order most commonly accepted in the language of the name."
                        },
                        "lastName": {
                            "type": "string",
                            "meta:xdmType": "string",
                            "title": "Last name",
                            "description": "The last audience of the name in the writing order most commonly accepted in the language of the name. In many cultures this is the inherited family name, surname, patronymic, or matronymic name. The `firstName` and `lastName` properties have been introduced to maintain compatibility with existing systems that model names in a simplified, non-semantic, and non-internationalizable way. Using `xdm:fullName` is always preferable."
                        },
                        "middleName": {
                            "type": "string",
                            "meta:xdmType": "string",
                            "title": "Middle name",
                            "description": "Middle, alternative, or additional names supplied between the first name and last name."
                        },
                        "suffix": {
                            "type": "string",
                            "meta:xdmType": "string",
                            "title": "Suffix",
                            "description": "A group of letters provided after a person's name to provide additional information. The `suffix` is used at the end of someones name. For example Jr., Sr., M.D., PhD, I, II, III, etc."
                        }
                    }
                },
                "nationality": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "title": "Nationality",
                    "description": "The legal relationship between a person and their state represented using the ISO 3166-1 Alpha-2 code."
                },
                "taxId": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "title": "Tax ID",
                    "description": "The Tax / Fiscal ID of the person, e.g. the TIN in the US or the CIF/NIF in Spain.",
                    "meta:status": "deprecated"
                },
                "type": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "title": "Type",
                    "description": "The type of individual in different business contexts like B2C."
                }
            }
        }
```

+++

>[!ENDSHADEBOX]



>[!BEGINSHADEBOX]

**Solicitação para obter identidades**

+++Obter identidades disponíveis que você pode usar na etapa de mapeamento

```shell
curl --location --request GET 'https://platform.adobe.io/data/core/idnamespace/identities' \ 
--header 'x-gw-ims-org-id: {ORG_ID}' \ 
--header 'x-api-key: {API_KEY}' \ 
--header 'x-sandbox-name: {SANDBOX_NAME}' \ 
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
```

+++

**Resposta**

+++ Exibir identidades disponíveis para usar no esquema de entrada

A resposta retorna as identidades que você pode usar ao criar o esquema de entrada. Observe que esta resposta retorna os namespaces de identidade [padrão](/help/identity-service/features/namespaces.md#standard) e [personalizados](/help/identity-service/features/namespaces.md#manage-namespaces) configurados no Experience Platform.

```json
[
    {
        "updateTime": 1551688425455,
        "code": "CORE",
        "status": "ACTIVE",
        "description": "Adobe Audience Manger UUID",
        "id": 0,
        "createTime": 1551688425455,
        "idType": "COOKIE",
        "namespaceType": "Standard",
        "name": "CORE",
        "custom": false
    },
    {
        "updateTime": 1551688425455,
        "code": "ECID",
        "status": "ACTIVE",
        "description": "Adobe Experience Cloud ID",
        "id": 4,
        "createTime": 1551688425455,
        "idType": "COOKIE",
        "namespaceType": "Standard",
        "name": "ECID",
        "custom": false
    },
    {
        "updateTime": 1551688425455,
        "code": "AdCloud",
        "status": "ACTIVE",
        "description": "Adobe AdCloud - ID Syncing Partner",
        "id": 411,
        "createTime": 1551688425455,
        "idType": "COOKIE",
        "namespaceType": "Standard",
        "name": "AdCloud",
        "custom": false
    },
    {
        "updateTime": 1551688425455,
        "code": "Email_LC_SHA256",
        "status": "ACTIVE",
        "description": "Email addresses need to be hashed using SHA256 and lowercased. Please also note that leading and trailing spaces need to be trimmed before an email address is normalized. You won't be able to change this setting later",
        "id": 11,
        "createTime": 1551688425455,
        "idType": "Email",
        "namespaceType": "Standard",
        "name": "Emails (SHA256, lowercased)",
        "custom": false,
        "hashFunction": "SHA256",
        "transform": "lowercase"
    },
    {
        "updateTime": 1597996026101,
        "code": "Phone_E.164",
        "status": "ACTIVE",
        "description": "Namespace for raw phone numbers in E.164 format. + sign is required",
        "id": 17,
        "createTime": 1597996026101,
        "idType": "Phone",
        "namespaceType": "Standard",
        "name": "Phone (E.164)",
        "custom": false
    },
    {
        "updateTime": 1551688425455,
        "code": "GAID",
        "status": "ACTIVE",
        "description": "This datasource is associated to a Google Ad ID",
        "id": 20914,
        "createTime": 1551688425455,
        "idType": "DEVICE",
        "namespaceType": "Standard",
        "name": "Google Ad ID (GAID)",
        "custom": false
    },
    {
        "updateTime": 1476993749000,
        "code": "IDFA",
        "status": "ACTIVE",
        "description": "Apple ID for Advertisers. See: https://support.apple.com/en-us/HT202074 for more info.",
        "id": 20915,
        "createTime": 1476993749000,
        "idType": "DEVICE",
        "namespaceType": "Standard",
        "name": "Apple IDFA (ID for Advertisers)",
        "custom": false
    },
    {
        "updateTime": 1551688425455,
        "code": "AAID",
        "status": "ACTIVE",
        "description": "Adobe Analytics (Legacy ID)",
        "id": 10,
        "createTime": 1551688425455,
        "idType": "COOKIE",
        "namespaceType": "Standard",
        "name": "Adobe Analytics (Legacy ID)",
        "custom": false
    },
    {
        "updateTime": 1551688425455,
        "code": "Email",
        "status": "ACTIVE",
        "description": "Email",
        "id": 6,
        "createTime": 1551688425455,
        "idType": "Email",
        "namespaceType": "Standard",
        "name": "Email",
        "custom": false
    },
    {
        "updateTime": 1551688425455,
        "code": "WAID",
        "status": "ACTIVE",
        "description": "Windows AID",
        "id": 8,
        "createTime": 1551688425455,
        "idType": "DEVICE",
        "namespaceType": "Standard",
        "name": "Windows AID",
        "custom": false
    },
    {
        "updateTime": 1551688425455,
        "code": "TNTID",
        "status": "ACTIVE",
        "description": "Adobe Target (TNTID)",
        "id": 9,
        "createTime": 1551688425455,
        "idType": "COOKIE",
        "namespaceType": "Standard",
        "name": "TNTID",
        "custom": false
    },
    {
        "updateTime": 1556676464714,
        "code": "Google",
        "status": "ACTIVE",
        "id": 771,
        "createTime": 1556676464714,
        "idType": "COOKIE",
        "namespaceType": "Integration",
        "name": "Google",
        "custom": false
    },
    {
        "updateTime": 1604597776019,
        "code": "Phone_SHA256_E.164",
        "status": "ACTIVE",
        "description": "Phone numbers need to be hashed using SHA256 without any dashes. Hash should be completed by customers on raw phone numbers in E.164 format. Please note that some destinations may have different phone number formatting requirements. Refer to documentation or consult your Adobe representative",
        "id": 18,
        "createTime": 1604597776019,
        "idType": "Phone",
        "namespaceType": "Standard",
        "name": "Phone (SHA256_E.164)",
        "custom": false,
        "hashFunction": "SHA256"
    },
    {
        "updateTime": 1604597776019,
        "code": "Phone_SHA256",
        "status": "ACTIVE",
        "description": "Remove symbols, letters, and any leading zeroes before hashing. Prefix the country code before hashing. Please note that some destinations may have different phone number formatting requirements. Refer to documentation or consult your Adobe representative",
        "id": 15,
        "createTime": 1597995542594,
        "idType": "Phone",
        "namespaceType": "Standard",
        "name": "Phone (SHA256)",
        "custom": false,
        "hashFunction": "SHA256"
    },
    {
        "updateTime": 1551688425455,
        "code": "Phone",
        "status": "ACTIVE",
        "description": "Phone",
        "id": 7,
        "createTime": 1551688425455,
        "idType": "PHONE_NUMBER",
        "namespaceType": "Standard",
        "name": "Phone",
        "custom": false
    }
]
```

+++

>[!ENDSHADEBOX]

Em seguida, é necessário copiar a resposta acima e usá-la para criar o esquema de entrada. Você pode copiar toda a resposta JSON da resposta acima e colocá-la no objeto `jsonSchema` indicado abaixo.

>[!BEGINSHADEBOX]

**Solicitação para criar o esquema de entrada**

+++Criar um esquema de entrada - solicitação

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/conversion/schemas/' \ 
--header 'x-gw-ims-org-id: {ORG_ID}' \ 
--header 'x-api-key: {API_KEY}' \ 
--header 'x-sandbox-name: {SANDBOX_NAME}' \ 
--header 'Authorization: Bearer {ACCESS_TOKEN}' \ 
--header 'Content-Type: application/json' \ 
--data-raw '{
    "name":"Sample Schema for Flow Mapping",
    "jsonSchema":{...insert response from union schema response here}
    '
```

+++

**Resposta**

+++Criar um esquema de entrada - Resposta

```json
{
   "id":"8db56468c2ab475dbf17c2621f92c0f8",
   "version":0,
   "jsonSchema":{
      "title":"XDM Individual Profile",
      "description":"An XDM Individual Profile forms a singular representation of the attributes and interests of both identified and partially-identified individuals. Less-identified profiles may contain only anonymous behavioral signals, such as browser cookies, while highly-identified profiles may contain detailed personal information such as name, date of birth, location, and email address. As a profile grows, it becomes a robust repository of personal information, identification information, contact details, and communication preferences for an individual.",
      "type":"object",
      "properties":{ // this section returns the contents that you have added to the jsonSchema object in the request
      }
   }
}
```

+++

>[!ENDSHADEBOX]

A ID na resposta representa o identificador exclusivo do esquema de entrada criado. Copie a ID da resposta, pois você reutilizará isso em uma etapa posterior.

### Criar um esquema de saída

Em seguida, você deve configurar o schema de saída para sua exportação. Primeiro, é necessário encontrar e inspecionar o esquema de parceiro existente.

>[!BEGINSHADEBOX]

**Solicitação**

+++Solicitação para obter o esquema do parceiro para o esquema de saída

Observe que o exemplo abaixo usa `connection spec ID` para Amazon S3. Substitua esse valor pela ID de especificação da conexão específica ao seu destino.

```shell
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs/4fce964d-3f37-408f-9778-e597338a21ee' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-api-key: {API_KEY}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
```

+++

**Resposta com um exemplo de esquema**

Inspecione a resposta obtida ao executar a chamada acima. Você precisa detalhar a resposta para localizar o objeto `targetSpec.attributes.partnerSchema.jsonSchema`

+++ Resposta para obter esquema do parceiro para o esquema de saída

```json
{
   "title":"defaultschema",
   "type":"object",
   "properties":{
      "attributes":{
         "type":"object",
         "meta:xdmType":"map",
         "additionalProperties":{
            "type":"object",
            "properties":{
               "value":{
                  "type":"string",
                  "title":"Value"
               }
            },
            "meta:xdmType":"object"
         }
      },
      "identityMap":{
         "type":"object",
         "meta:xdmField":"xdm:identityMap",
         "meta:xdmType":"map",
         "additionalProperties":{
            "type":"array",
            "items":{
               "type":"object",
               "properties":{
                  "id":{
                     "type":"string",
                     "title":"Identifier",
                     "description":"Identity of the consumer in the related namespace.",
                     "meta:xdmType":"string",
                     "meta:xdmField":"xdm:id"
                  },
                  "primary":{
                     "type":"boolean",
                     "title":"Primary",
                     "default":false,
                     "description":"Indicates this identity is the preferred identity. Is used as a hint to help systems better organize how identities are queried.",
                     "meta:xdmType":"boolean",
                     "meta:xdmField":"xdm:primary"
                  },
                  "authenticatedState":{
                     "enum":[
                        "ambiguous",
                        "authenticated",
                        "loggedOut"
                     ],
                     "type":"string",
                     "default":"ambiguous",
                     "meta:enum":{
                        "ambiguous":"Ambiguous",
                        "loggedOut":"User was identified by a login action at some point of time previously, but is not currently logged in.",
                        "authenticated":"User identified by a login or similar action that was valid at the time of the event observation."
                     },
                     "description":"The state this identity is authenticated as for this observed ExperienceEvent.",
                     "meta:xdmType":"string",
                     "meta:xdmField":"xdm:authenticatedState"
                  }
               },
               "meta:xdmType":"object",
               "meta:referencedFrom":"https://ns.adobe.com/xdm/context/identityitem"
            },
            "meta:xdmType":"array"
         }
      },
      "segmentMembership":{
         "title":"Segment membership map",
         "type":"object",
         "meta:xdmField":"xdm:segmentMembership",
         "meta:xdmType":"map",
         "additionalProperties":{
            "type":"object",
            "title":"Segment membership per namespace",
            "meta:xdmType":"map",
            "additionalProperties":{
               "type":"object",
               "properties":{
                  "status":{
                     "enum":[
                        "realized",
                        "exited"
                     ],
                     "type":"string",
                     "title":"Status",
                     "default":"realized",
                     "meta:enum":{
                        "exited":"Entity is exiting the segment.",
                        "realized":"Entity is entering the segment."
                     },
                     "description":"Is the audience participation realized as part of the current request.",
                     "meta:xdmType":"string",
                     "meta:xdmField":"xdm:status"
                  },
                  "payload":{
                     "type":"object",
                     "title":"Payload",
                     "required":[
                        "payloadType"
                     ],
                     "properties":{
                        "payloadType":{
                           "enum":[
                              "boolean",
                              "number",
                              "propensity",
                              "string"
                           ],
                           "type":"string",
                           "title":"Payload Type",
                           "meta:enum":{
                              "number":"Number",
                              "string":"String",
                              "boolean":"Boolean",
                              "propensity":"Propensity"
                           },
                           "description":"The type of payload.",
                           "meta:xdmType":"string",
                           "meta:xdmField":"xdm:payloadType"
                        },
                        "payloadNumberValue":{
                           "type":"number",
                           "title":"Value",
                           "description":"The number.",
                           "meta:xdmType":"number",
                           "meta:xdmField":"xdm:payloadNumberValue"
                        },
                        "payloadStringValue":{
                           "type":"string",
                           "title":"Value",
                           "description":"The string value.",
                           "meta:xdmType":"string",
                           "meta:xdmField":"xdm:payloadStringValue"
                        },
                        "payloadBooleanValue":{
                           "type":"boolean",
                           "title":"Value",
                           "description":"The boolean value.",
                           "meta:xdmType":"boolean",
                           "meta:xdmField":"xdm:payloadBooleanValue"
                        },
                        "payloadPropensityValue":{
                           "type":"number",
                           "title":"Value",
                           "maximum":1,
                           "description":"The propensity.",
                           "meta:xdmType":"number",
                           "meta:xdmField":"xdm:payloadPropensityValue",
                           "exclusiveMinimum":0
                        }
                     },
                     "description":"Values that are directly related with the audience realization. This payload exists with the same 'validUntil' as the audience realization. Note that the intention is that exactly one payload value be included, as indicated by the payload type. This was originally modeled using 'oneOf', but due to limitations in our tooling that was removed. This more semantically meaningful representation will be re-introduced in the future.",
                     "meta:xdmType":"object",
                     "meta:xdmField":"xdm:payload"
                  },
                  "version":{
                     "type":"string",
                     "title":"Version",
                     "description":"The version of the audience definition used in this audience assertion. Version can be omitted in audience lists when all memberships versions are the same.",
                     "meta:xdmType":"string",
                     "meta:xdmField":"xdm:version"
                  },
                  "segmentID":{
                     "type":"object",
                     "title":"Segment ID",
                     "properties":{
                        "_id":{
                           "type":"string",
                           "title":"Identifier",
                           "format":"uri-reference",
                           "description":"Identity of the audience in the related namespace.",
                           "meta:xdmType":"string",
                           "meta:xdmField":"@id"
                        },
                        "xid":{
                           "type":"string",
                           "title":"Experience identifier",
                           "description":"When present, this value represents a cross-namespace identifier that is unique across all namespace-scoped identifiers in all namespaces.",
                           "meta:xdmType":"string",
                           "meta:xdmField":"xdm:xid"
                        },
                        "namespace":{
                           "type":"object",
                           "title":"Namespace",
                           "required":[
                              "code"
                           ],
                           "properties":{
                              "code":{
                                 "type":"string",
                                 "title":"Code",
                                 "description":"The code is a human readable identifier for the namespace and can be used to request the technical namespace id which is used for identity graph processing.",
                                 "meta:xdmType":"string",
                                 "meta:xdmField":"xdm:code"
                              }
                           },
                           "description":"The namespace associated with the `xid` attribute.",
                           "meta:xdmType":"object",
                           "meta:xdmField":"xdm:namespace",
                           "meta:referencedFrom":"https://ns.adobe.com/xdm/context/namespace"
                        }
                     },
                     "description":"The identity of the audience or snapshot definition in with the domain of the specific system that processes that type of segment. Deprecated.",
                     "meta:status":"deprecated",
                     "meta:xdmType":"object",
                     "meta:xdmField":"xdm:segmentID",
                     "meta:referencedFrom":"https://ns.adobe.com/xdm/context/segmentidentity"
                  },
                  "validUntil":{
                     "type":"string",
                     "title":"Valid until",
                     "format":"date-time",
                     "description":"The timestamp for when the audienceassertion should no longer be assumed to be valid and should either be ignored or revalidated.",
                     "meta:xdmType":"date-time",
                     "meta:xdmField":"xdm:validUntil"
                  },
                  "profileStitchID":{
                     "type":"object",
                     "properties":{
                        "_id":{
                           "type":"string",
                           "title":"Identifier",
                           "format":"uri-reference",
                           "description":"Identity of the profile stitch in the related namespace.",
                           "meta:xdmType":"string",
                           "meta:xdmField":"@id"
                        },
                        "xid":{
                           "type":"string",
                           "title":"Experience identifier",
                           "description":"When present, this value represents a cross-namespace identifier that is unique across all namespace-scoped identifiers in all namespaces.",
                           "meta:xdmType":"string",
                           "meta:xdmField":"xdm:xid"
                        },
                        "namespace":{
                           "type":"object",
                           "title":"Namespace",
                           "required":[
                              "code"
                           ],
                           "properties":{
                              "code":{
                                 "type":"string",
                                 "title":"Code",
                                 "description":"The code is a human readable identifier for the namespace and can be used to request the technical namespace id which is used for identity graph processing.",
                                 "meta:xdmType":"string",
                                 "meta:xdmField":"xdm:code"
                              }
                           },
                           "description":"The namespace associated with the `xid` attribute.",
                           "meta:xdmType":"object",
                           "meta:xdmField":"xdm:namespace",
                           "meta:referencedFrom":"https://ns.adobe.com/xdm/context/namespace"
                        }
                     },
                     "meta:xdmType":"object",
                     "meta:xdmField":"xdm:profileStitchID",
                     "meta:referencedFrom":"https://ns.adobe.com/xdm/context/profileStitchIdentity"
                  },
                  "lastQualificationTime":{
                     "type":"string",
                     "title":"Last qualification time",
                     "format":"date-time",
                     "description":"The timestamp when the assertion of audience membership was made.",
                     "meta:xdmType":"date-time",
                     "meta:xdmField":"xdm:lastQualificationTime"
                  }
               },
               "meta:xdmType":"object",
               "meta:referencedFrom":"https://ns.adobe.com/xdm/context/segmentmembership"
            }
         }
      }
   }
}
```

+++

>[!ENDSHADEBOX]

Em seguida, é necessário criar um schema de saída. Copie a resposta JSON recebida acima e cole-a no objeto `jsonSchema` abaixo.

>[!BEGINSHADEBOX]

**Solicitação**

+++Criar um esquema de saída - Solicitação

```shell
curl --location --request POST 'https://platform.adobe.io/data/foundation/conversion/schemas' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer TOKEN' \
--header 'Content-Type: application/json' \
--data-raw '{
    "name": "Sample Schema for Flow Mapping",
"jsonSchema":{...insert JSON from the response above here}
}
'
```

+++

**Resposta**

+++Criar esquema de saída - Resposta

```json
{
    "id": "2f4fd51934c1409fb1d8207dd9f43dc9",
    "version": 0,
    "jsonSchema": {
        "title": "defaultschema",
        "type": "object",
        "properties": {
            "identityMap": {
                "type": "object",
                "meta:xdmField": "xdm:identityMap",
                "meta:xdmType": "map",
                "additionalProperties": {
                    "meta:xdmType": "array",
                    "items": {
                        "meta:referencedFrom": "https://ns.adobe.com/xdm/context/identityitem",
                        "properties": {
                            "primary": {
                                "meta:xdmField": "xdm:primary",
                                "meta:xdmType": "boolean",
                                "description": "Indicates this identity is the preferred identity. Is used as a hint to help systems better organize how identities are queried.",
                                "default": false,
                                "type": "boolean",
                                "title": "Primary"
                            },
                            "id": {
                                "meta:xdmField": "xdm:id",
                                "meta:xdmType": "string",
                                "description": "Identity of the consumer in the related namespace.",
                                "type": "string",
                                "title": "Identifier"
                            },
                            "authenticatedState": {
                                "meta:xdmField": "xdm:authenticatedState",
                                "meta:xdmType": "string",
                                "meta:enum": {
                                    "loggedOut": "User was identified by a login action at some point of time previously, but is not currently logged in.",
                                    "authenticated": "User identified by a login or similar action that was valid at the time of the event observation.",
                                    "ambiguous": "Ambiguous"
                                },
                                "enum": [
                                    "ambiguous",
                                    "authenticated",
                                    "loggedOut"
                                ],
                                "default": "ambiguous",
                                "type": "string",
                                "description": "The state this identity is authenticated as for this observed ExperienceEvent."
                            }
                        },
                        "meta:xdmType": "object",
                        "type": "object"
                    },
                    "type": "array"
                }
            },
            "segmentMembership": {
                "title": "Segment membership map",
                "type": "object",
                "meta:xdmField": "xdm:segmentMembership",
                "meta:xdmType": "map",
                "additionalProperties": {
                    "additionalProperties": {
                        "meta:referencedFrom": "https://ns.adobe.com/xdm/context/segmentmembership",
                        "properties": {
                            "version": {
                                "meta:xdmField": "xdm:version",
                                "meta:xdmType": "string",
                                "description": "The version of the audience definition used in this audience assertion. Version can be omitted in audience lists when all memberships versions are the same.",
                                "type": "string",
                                "title": "Version"
                            },
                            "validUntil": {
                                "meta:xdmField": "xdm:validUntil",
                                "meta:xdmType": "date-time",
                                "description": "The timestamp for when the audienceassertion should no longer be assumed to be valid and should either be ignored or revalidated.",
                                "format": "date-time",
                                "type": "string",
                                "title": "Valid until"
                            },
                            "status": {
                                "meta:xdmField": "xdm:status",
                                "meta:xdmType": "string",
                                "meta:enum": {
                                    "exited": "Entity is exiting the segment.",
                                    "realized": "Entity is entering the segment."
                                },
                                "enum": [
                                    "realized",
                                    "exited"
                                ],
                                "default": "realized",
                                "description": "Is the audience participation realized as part of the current request.",
                                "type": "string",
                                "title": "Status"
                            },
                            "segmentID": {
                                "meta:xdmField": "xdm:segmentID",
                                "meta:referencedFrom": "https://ns.adobe.com/xdm/context/segmentidentity",
                                "properties": {
                                    "xid": {
                                        "meta:xdmField": "xdm:xid",
                                        "meta:xdmType": "string",
                                        "description": "When present, this value represents a cross-namespace identifier that is unique across all namespace-scoped identifiers in all namespaces.",
                                        "type": "string",
                                        "title": "Experience identifier"
                                    },
                                    "namespace": {
                                        "meta:xdmField": "xdm:namespace",
                                        "required": [
                                            "code"
                                        ],
                                        "meta:referencedFrom": "https://ns.adobe.com/xdm/context/namespace",
                                        "properties": {
                                            "code": {
                                                "meta:xdmField": "xdm:code",
                                                "meta:xdmType": "string",
                                                "description": "The code is a human readable identifier for the namespace and can be used to request the technical namespace id which is used for identity graph processing.",
                                                "type": "string",
                                                "title": "Code"
                                            }
                                        },
                                        "meta:xdmType": "object",
                                        "type": "object",
                                        "description": "The namespace associated with the `xid` attribute.",
                                        "title": "Namespace"
                                    },
                                    "_id": {
                                        "meta:xdmField": "@id",
                                        "meta:xdmType": "string",
                                        "description": "Identity of the audience in the related namespace.",
                                        "format": "uri-reference",
                                        "type": "string",
                                        "title": "Identifier"
                                    }
                                },
                                "meta:xdmType": "object",
                                "type": "object",
                                "description": "The identity of the audience or snapshot definition in with the domain of the specific system that processes that type of segment. Deprecated.",
                                "meta:status": "deprecated",
                                "title": "Segment ID"
                            },
                            "profileStitchID": {
                                "meta:xdmField": "xdm:profileStitchID",
                                "meta:referencedFrom": "https://ns.adobe.com/xdm/context/profileStitchIdentity",
                                "properties": {
                                    "xid": {
                                        "meta:xdmField": "xdm:xid",
                                        "meta:xdmType": "string",
                                        "description": "When present, this value represents a cross-namespace identifier that is unique across all namespace-scoped identifiers in all namespaces.",
                                        "type": "string",
                                        "title": "Experience identifier"
                                    },
                                    "namespace": {
                                        "meta:xdmField": "xdm:namespace",
                                        "required": [
                                            "code"
                                        ],
                                        "meta:referencedFrom": "https://ns.adobe.com/xdm/context/namespace",
                                        "properties": {
                                            "code": {
                                                "meta:xdmField": "xdm:code",
                                                "meta:xdmType": "string",
                                                "description": "The code is a human readable identifier for the namespace and can be used to request the technical namespace id which is used for identity graph processing.",
                                                "type": "string",
                                                "title": "Code"
                                            }
                                        },
                                        "meta:xdmType": "object",
                                        "type": "object",
                                        "description": "The namespace associated with the `xid` attribute.",
                                        "title": "Namespace"
                                    },
                                    "_id": {
                                        "meta:xdmField": "@id",
                                        "meta:xdmType": "string",
                                        "description": "Identity of the profile stitch in the related namespace.",
                                        "format": "uri-reference",
                                        "type": "string",
                                        "title": "Identifier"
                                    }
                                },
                                "meta:xdmType": "object",
                                "type": "object"
                            },
                            "payload": {
                                "meta:xdmField": "xdm:payload",
                                "meta:xdmType": "object",
                                "required": [
                                    "payloadType"
                                ],
                                "properties": {
                                    "payloadType": {
                                        "meta:xdmField": "xdm:payloadType",
                                        "meta:xdmType": "string",
                                        "description": "The type of payload.",
                                        "meta:enum": {
                                            "string": "String",
                                            "propensity": "Propensity",
                                            "number": "Number",
                                            "boolean": "Boolean"
                                        },
                                        "enum": [
                                            "boolean",
                                            "number",
                                            "propensity",
                                            "string"
                                        ],
                                        "type": "string",
                                        "title": "Payload Type"
                                    },
                                    "payloadStringValue": {
                                        "meta:xdmField": "xdm:payloadStringValue",
                                        "meta:xdmType": "string",
                                        "description": "The string value.",
                                        "type": "string",
                                        "title": "Value"
                                    },
                                    "payloadPropensityValue": {
                                        "meta:xdmField": "xdm:payloadPropensityValue",
                                        "meta:xdmType": "number",
                                        "maximum": 1,
                                        "exclusiveMinimum": 0,
                                        "description": "The propensity.",
                                        "type": "number",
                                        "title": "Value"
                                    },
                                    "payloadNumberValue": {
                                        "meta:xdmField": "xdm:payloadNumberValue",
                                        "meta:xdmType": "number",
                                        "description": "The number.",
                                        "type": "number",
                                        "title": "Value"
                                    },
                                    "payloadBooleanValue": {
                                        "meta:xdmField": "xdm:payloadBooleanValue",
                                        "meta:xdmType": "boolean",
                                        "description": "The boolean value.",
                                        "type": "boolean",
                                        "title": "Value"
                                    }
                                },
                                "type": "object",
                                "description": "Values that are directly related with the audience realization. This payload exists with the same 'validUntil' as the audience realization. Note that the intention is that exactly one payload value be included, as indicated by the payload type. This was originally modeled using 'oneOf', but due to limitations in our tooling that was removed. This more semantically meaningful representation will be re-introduced in the future.",
                                "title": "Payload"
                            },
                            "lastQualificationTime": {
                                "meta:xdmField": "xdm:lastQualificationTime",
                                "meta:xdmType": "date-time",
                                "description": "The timestamp when the assertion of audience membership was made.",
                                "format": "date-time",
                                "type": "string",
                                "title": "Last qualification time"
                            }
                        },
                        "meta:xdmType": "object",
                        "type": "object"
                    },
                    "meta:xdmType": "map",
                    "type": "object",
                    "title": "Segment membership per namespace"
                }
            },
            "attributes": {
                "type": "object",
                "meta:xdmType": "map",
                "additionalProperties": {
                    "properties": {
                        "value": {
                            "type": "string",
                            "title": "Value"
                        }
                    },
                    "meta:xdmType": "object",
                    "type": "object"
                }
            },
            "firstName": {
                "title": "firstName",
                "type": "string"
            },
            "Email": {
                "title": "Email",
                "type": "array",
                "items": {
                    "type": "object",
                    "properties": {
                        "id": {
                            "title": "id",
                            "type": "string",
                            "meta:xdmType": "string"
                        }
                    },
                    "meta:xdmType": "object"
                },
                "meta:xdmType": "array"
            }
        }
    }
}
```

A ID na resposta representa o identificador exclusivo do esquema de entrada criado. Copie a ID da resposta, pois você reutilizará isso em uma etapa posterior.

>[!ENDSHADEBOX]

### Criar conjunto de mapeamento {#create-mapping-set}

Em seguida, use a [API de preparação de dados](https://developer.adobe.com/experience-platform-apis/references/data-prep/#tag/Mapping-sets/operation/createMappingSet) para criar o conjunto de mapeamento usando a ID do esquema de entrada, a ID do esquema de saída e os mapeamentos de campo desejados.

>[!BEGINSHADEBOX]

**Solicitação**

+++Criar conjunto de mapeamento - Solicitação

>[!IMPORTANT]
>
>* No objeto de mapeamentos mostrado abaixo, o parâmetro `destination` não aceita pontos `"."`. Por exemplo, você precisaria usar personalEmail_address ou segmentMembership_status como destacado no exemplo de configuração.
>* Há um caso específico quando o atributo de origem é um atributo de identidade e contém um ponto. Nesse caso, o atributo precisa ser escapado com `//`, como destacado abaixo.
>* Observe também que, mesmo que a configuração de exemplo abaixo inclua `Email` e `Phone_E.164`, você só poderá exportar um atributo de identidade por fluxo de dados.

```shell {line-numbers="true" start-line="1" highlight="16-38"}
curl --location --request POST 'https://platform.adobe.io/data/foundation/conversion/mappingSets' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer TOKEN' \
--header 'Content-Type: application/json' \
--data-raw '{
    "inputSchema": {
        "id": "81d7fc5376e54eb58d5186fd30d5a8c9"
    },  
    "outputSchema": {
        "id": "2f4fd51934c1409fb1d8207dd9f43dc9"
    },
    "mappings": [
        {
            "destination": "firstName",
            "source": "person.name.firstName",
            "sourceType": "ATTRIBUTE"
        }, 
        {
            "destination": "Email",
            "source": "identityMap.Email",
            "sourceType": "ATTRIBUTE"
        },
        {
            "destination": "Phone_E_164",
            "source": "identityMap.Phone_E//.164",
            "sourceType": "ATTRIBUTE"
        },
        {
            "destination": "personalEmail_address",
            "source": "personalEmail.address",
            "sourceType": "ATTRIBUTE"
        },        
        {
            "destination": "segmentMembership_status",
            "source": "segmentMembership.ups.seg_id.status",
            "sourceType": "ATTRIBUTE"
        }        
    ],
    "xdmVersion": "1.0"
}'
```

+++

**Resposta**

+++ Criar conjunto de mapeamento - Resposta

```json
{
    "id": "5f0031f8ccd4444dac9c5c391389e9e8",
    "version": 0,
    "createdDate": 1678999005197,
    "modifiedDate": 1678999005197,
    "createdBy": "example@AdobeID",
    "modifiedBy": "example@AdobeID"
}
```

+++

>[!ENDSHADEBOX]

Observe a ID do conjunto de mapeamento, pois será necessário na próxima etapa para atualizar o fluxo de dados existente com a ID do conjunto de mapeamento.

Em seguida, obtenha a ID do fluxo de dados que você deseja atualizar.

>[!BEGINSHADEBOX]

Consulte [recuperar os detalhes de um fluxo de dados de destino](https://developer.adobe.com/experience-platform-apis/references/destinations/#tag/Dataflows/operation/getFlowById) para obter informações sobre como recuperar a ID de um fluxo de dados.

>[!ENDSHADEBOX]

Finalmente, é necessário `PATCH` o fluxo de dados com as informações do conjunto de mapeamento que você acabou de criar.

>[!BEGINSHADEBOX]

**Solicitação**

+++ Atualizar fluxo de dados com informações do conjunto de mapeamento - Solicitação

```shell
curl --location --request PATCH 'https://platform.adobe.io/data/foundation/flowservice/flows/df8245a8-dd8f-42da-a04a-2d3a92654d9e' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'If-Match: ETAG_HERE' \
--data-raw '[
   {
      "op":"ADD",
      "path":"/transformations/0/params/profileMapping",
      "value":{
         "mappingId":"304ca6a2fff244949c956cad1cd9eae6",
         "mappingVersion":0
      }
   }
]'
```

+++

**Resposta**

+++ Atualizar fluxo de dados com informações do conjunto de mapeamento - Resposta

A resposta da API do Serviço de fluxo retorna a ID do fluxo de dados atualizado.

```json
{
    "id": "1c246ae4-ba0d-43cd-a0ec-f16fe0a56b55",
    "etag": "\"1500c67f-0000-0200-0000-64137ee00000\""
}
```

+++

>[!ENDSHADEBOX]

## Fazer outras atualizações de fluxo de dados {#other-dataflow-updates}

![Etapas para ativar públicos destacando a etapa atual em que o usuário está](/help/destinations/assets/api/file-based-segment-export/step7.png)

Para fazer atualizações no fluxo de dados, use a operação `PATCH`. Por exemplo, você pode adicionar uma ação de marketing aos fluxos de dados, atualizar seus fluxos de dados para selecionar campos como chaves obrigatórias ou chaves de desduplicação ou adicionar a geração de manifesto de arquivo aos destinos existentes.

### Adicionar uma ação de marketing {#add-marketing-action}

Para adicionar uma [ação de marketing](/help/data-governance/api/marketing-actions.md), consulte os exemplos de solicitação e resposta abaixo.

>[!IMPORTANT]
>
>O cabeçalho `If-Match` é necessário ao fazer uma solicitação `PATCH`. O valor desse cabeçalho é a versão exclusiva do fluxo de dados que você deseja atualizar. O valor da tag é atualizado com cada atualização bem-sucedida de uma entidade de fluxo, como fluxo de dados, conexão de destino e outras.
>
> Para obter a versão mais recente do valor da tag, execute uma solicitação GET para o ponto de extremidade `https://platform.adobe.io/data/foundation/flowservice/flows/{ID}`, em que `{ID}` é a ID do fluxo de dados que você deseja atualizar.
>
> Certifique-se de colocar o valor do cabeçalho `If-Match` entre aspas duplas, como nos exemplos abaixo, ao fazer solicitações `PATCH`.

>[!BEGINSHADEBOX]

**Solicitação**

>[!TIP]
>
>Antes de adicionar uma ação de marketing a um fluxo de dados, você pode pesquisar suas ações de marketing principais e personalizadas. Exiba [como recuperar uma lista de ações de marketing existentes](/help/data-governance/api/marketing-actions.md#list).

+++Adicionar uma ação de marketing a um fluxo de dados de destino - Solicitação

```shell
curl --location --request PATCH 'https://platform.adobe.io/data/foundation/flowservice/flows/{DATAFLOW_ID}' \
--header 'accept: application/json' \
--header 'Content-Type: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'If-Match: "{ETAG_HERE}"' \
--data-raw '[
   {
      "op":"add",
      "path":"/policy",
      "value":{
         "enforcementRefs":[
            
         ]
      }
   },
   {
      "op":"add",
      "path":"/policy/enforcementRefs/-",
      "value":"/dulepolicy/marketingActions/custom/6b935bc8-bb9e-451b-a327-0ffddfb91e66/constraints"
   }
]'
```

+++


**Resposta**

+++Adicionar uma ação de marketing - Resposta

Uma resposta bem-sucedida retorna o código de resposta `200` junto com a ID do fluxo de dados atualizado e a eTag atualizada.

```json
{
    "id": "eb54b3b3-3949-4f12-89c8-64eafaba858f",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!ENDSHADEBOX]

### Adicionar uma chave obrigatória {#add-mandatory-key}

Para adicionar uma [chave obrigatória](/help/destinations/ui/activate-batch-profile-destinations.md#mandatory-attributes), consulte os exemplos de solicitação e resposta abaixo.

>[!IMPORTANT]
>
>O cabeçalho `If-Match` é necessário ao fazer uma solicitação `PATCH`. O valor desse cabeçalho é a versão exclusiva do fluxo de dados que você deseja atualizar. O valor da tag é atualizado com cada atualização bem-sucedida de uma entidade de fluxo, como fluxo de dados, conexão de destino e outras.
>
> Para obter a versão mais recente do valor da tag, execute uma solicitação GET para o ponto de extremidade `https://platform.adobe.io/data/foundation/flowservice/flows/{ID}`, em que `{ID}` é a ID do fluxo de dados que você deseja atualizar.
>
> Certifique-se de colocar o valor do cabeçalho `If-Match` entre aspas duplas, como nos exemplos abaixo, ao fazer solicitações `PATCH`.

>[!BEGINSHADEBOX]

**Solicitação**

+++Adicionar uma identidade como campo obrigatório - Solicitação

```shell
curl --location --request PATCH 'https://platform.adobe.io/data/foundation/flowservice/flows/{DATAFLOW_ID}' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'If-Match: "{ETAG_HERE}"' \
--data-raw '
[
  {
    "op": "add",
    "path": "/transformations/0/params/mandatoryFields",
    "value": [
      "GAID"
    ]
  }
]'
```

+++

+++Adicionar um atributo XDM como campo obrigatório - Solicitação

```shell
curl --location --request PATCH 'https://platform.adobe.io/data/foundation/flowservice/flows/{DATAFLOW_ID}' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'If-Match: "{ETAG_HERE}"' \
--data-raw '
[
  {
    "op": "add",
    "path": "/transformations/0/params/mandatoryFields",
    "value": [
      "GAID"
    ]
  }
]'
```

+++

**Resposta**

+++Adicionar um campo obrigatório - Resposta

```json
{
    "id": "eb54b3b3-3949-4f12-89c8-64eafaba858f",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!ENDSHADEBOX]

### Adicionar uma chave de desduplicação {#add-deduplication-key}

Para adicionar uma [chave de desduplicação](/help/destinations/ui/activate-batch-profile-destinations.md#deduplication-keys), consulte os exemplos de solicitação e resposta abaixo

>[!IMPORTANT]
>
>O cabeçalho `If-Match` é necessário ao fazer uma solicitação `PATCH`. O valor desse cabeçalho é a versão exclusiva do fluxo de dados que você deseja atualizar. O valor da tag é atualizado com cada atualização bem-sucedida de uma entidade de fluxo, como fluxo de dados, conexão de destino e outras.
>
> Para obter a versão mais recente do valor da tag, execute uma solicitação GET para o ponto de extremidade `https://platform.adobe.io/data/foundation/flowservice/flows/{ID}`, em que `{ID}` é a ID do fluxo de dados que você deseja atualizar.
>
> Certifique-se de colocar o valor do cabeçalho `If-Match` entre aspas duplas, como nos exemplos abaixo, ao fazer solicitações `PATCH`.

>[!BEGINSHADEBOX]

**Solicitação**

+++Adicionar uma identidade como chave de desduplicação - Solicitação

```shell
curl --location --request PATCH 'https://platform.adobe.io/data/foundation/flowservice/flows/{DATAFLOW_ID}' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'If-Match: "{ETAG_HERE}"' \
--data-raw '
[
  {
    "op": "add",
    "path": "/transformations/0/params/primaryFields",
    "value": [
      {
        "identityNamespace": "GAID",
        "fieldType": "IDENTITY"
      }
    ]
  }
]'
```

+++

+++Adicionar um atributo XDM como chave de desduplicação - Solicitação

```shell
curl --location --request PATCH 'https://platform.adobe.io/data/foundation/flowservice/flows/{DATAFLOW_ID}' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'If-Match: "{ETAG_HERE}"' \
--data-raw '
[
  {
    "op": "add",
    "path": "/transformations/0/params/primaryFields",
    "value": [
      {
        "identityNamespace": "GAID",
        "fieldType": "IDENTITY"
      }
    ]
  }
]'
```

+++

**Resposta**

+++Adicionar um campo obrigatório - Resposta

```json
{
    "id": "eb54b3b3-3949-4f12-89c8-64eafaba858f",
    "etag": "\"0000d781-0000-0200-0000-63e29f420000\""
}
```

+++

>[!ENDSHADEBOX]

### Adicionar geração de manifesto de arquivo ao destino existente {#add-file-manifest}

Para adicionar a geração de manifesto de arquivo a um destino existente, é necessário atualizar os parâmetros de conexão de destino usando a operação `PATCH`. Isso habilita a geração de arquivo de manifesto para o seu destino, que fornece metadados sobre os arquivos exportados.

>[!IMPORTANT]
>
>O cabeçalho `If-Match` é necessário ao fazer uma solicitação `PATCH`. O valor desse cabeçalho é a versão exclusiva da conexão de destino que você deseja atualizar. O valor da tag é atualizado com cada atualização bem-sucedida de uma entidade de fluxo, como fluxo de dados, conexão de destino e outras.
>
> Para obter a versão mais recente do valor da tag, execute uma solicitação GET para o ponto de extremidade `https://platform.adobe.io/data/foundation/flowservice/targetConnections/{ID}`, em que `{ID}` é a ID de conexão de destino que você deseja atualizar.
>
> Certifique-se de colocar o valor do cabeçalho `If-Match` entre aspas duplas, como nos exemplos abaixo, ao fazer solicitações `PATCH`.

>[!BEGINSHADEBOX]

**Solicitação**

+++Adicionar manifesto de arquivo à conexão de destino existente - Solicitação

```shell
curl --location --request PATCH 'https://platform.adobe.io/data/foundation/flowservice/targetConnections/{TARGET_CONNECTION_ID}' \
--header 'accept: application/json' \
--header 'Content-Type: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'If-Match: "{ETAG_HERE}"' \
--data-raw '[
  {
    "op": "add",
    "path": "/params/includeFileManifest",
    "value": true
  }
]'
```

>[!ENDSHADEBOX]

## Validar fluxo de dados (obter as execuções do fluxo de dados) {#get-dataflow-runs}

![Etapas para ativar públicos destacando a etapa atual em que o usuário está](/help/destinations/assets/api/file-based-segment-export/step8.png)

Para verificar as execuções de um fluxo de dados, use a API de execuções de fluxo de dados:

>[!BEGINSHADEBOX]

**Solicitação**

+++Obter execuções de fluxo de dados - Solicitação

```shell
curl --location --request GET 'https://platform.adobe.io/data/foundation/flowservice/runs?property=flowId==eb54b3b3-3949-4f12-89c8-64eafaba858f' \
--header 'accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--data-raw ''
```

+++

**Resposta**

+++Obter execuções de fluxo de dados - Resposta

```json
{
    "items": [
        {
            "id": "4b7728dd-83c9-4c38-95a4-24ddab545404",
            "createdAt": 1675807718296,
            "updatedAt": 1675807731834,
            "createdBy": "aep_activation_batch@AdobeID",
            "updatedBy": "acp_foundation_connectors@AdobeID",
            "createdClient": "aep_activation_batch",
            "updatedClient": "acp_foundation_connectors",
            "sandboxId": "7dfdcd30-0a09-11ea-8ea6-7bf93ce86c28",
            "sandboxName": "sand-1",
            "imsOrgId": "5555467B5D8013E50A494220@AdobeOrg",
            "flowId": "aae5ec63-b0ac-4808-9a44-abf2ea67bd5a",
            "flowSpec": {
                "id": "615d3489-36d2-4671-9467-4ae1129facd3",
                "version": "1.0"
            },
            "providerRefId": "ba56f98e0c49b572adb249980c39b1c7",
            "etag": "\"08005e9e-0000-0200-0000-63e2cbf30000\"",
            "metrics": {
                "durationSummary": {
                    "startedAtUTC": 1675807719411,
                    "completedAtUTC": 1675807719416
                },
                "sizeSummary": {
                    "inputBytes": 0
                },
                "recordSummary": {
                    "inputRecordCount": 0,
                    "skippedRecordCount": 0,
                    "sourceSummaries": [
                        {
                            "id": "ea2b1205-4692-49de-b448-ebf75b1d188a",
                            "inputRecordCount": 0,
                            "skippedRecordCount": 0,
                            "entitySummaries": [
                                {
//...
```

+++

>[!ENDSHADEBOX]

Você pode encontrar informações sobre os [vários parâmetros retornados pela API de execuções do Fluxo de Dados](https://developer.adobe.com/experience-platform-apis/references/destinations/#tag/Dataflow-runs/operation/getFlowRuns) na documentação de referência da API.

## Manipulação de erros de API {#api-error-handling}

Os endpoints de API neste tutorial seguem os princípios gerais de mensagem de erro da API do Experience Platform. Consulte [códigos de status da API](/help/landing/troubleshooting.md#api-status-codes) e [erros no cabeçalho da solicitação](/help/landing/troubleshooting.md#request-header-errors) no guia de solução de problemas do Experience Platform para obter mais informações sobre como interpretar respostas de erro.

## Próximas etapas {#next-steps}

Seguindo este tutorial, você conectou com êxito o Experience Platform a um dos destinos de armazenamento na nuvem de sua preferência e configurou um fluxo de dados para o respectivo destino para exportar públicos. Consulte as seguintes páginas para obter mais detalhes, como editar fluxos de dados existentes usando a API do Serviço de fluxo:

* [Visão geral dos destinos](../home.md)
* [Visão geral do Catálogo de destinos](../catalog/overview.md)
* [Atualizar fluxos de dados de destino usando a API de serviço de fluxo](../api/update-destination-dataflows.md)
