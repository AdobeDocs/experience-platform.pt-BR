---
title: Azure Databricks
description: Saiba mais sobre as etapas de pré-requisito necessárias para conectar o Azure Databricks ao Experience Platform.
badgeUltimate: label="Ultimate" type="Positive"
badgeBeta: label="Beta" type="Informative"
last-substantial-update: 2025-06-17T00:00:00Z
exl-id: 2f082898-aa0e-47a1-a4bf-077c21afdfee
source-git-commit: e5ece120329a550204174b7bf588f06cdff45846
workflow-type: tm+mt
source-wordcount: '631'
ht-degree: 3%

---

# [!DNL Azure Databricks]

>[!AVAILABILITY]
>
>* A origem [!DNL Azure Databricks] está disponível no catálogo de origens para usuários que compraram o Real-Time CDP Ultimate.
>
>* A origem [!DNL Azure Databricks] está na versão beta. Leia os [termos e condições](../../home.md#terms-and-conditions) na visão geral das fontes para obter mais informações sobre como usar fontes com rótulo beta.

[!DNL Azure Databricks] é uma plataforma baseada em nuvem projetada para análise de dados, aprendizado de máquina e IA. Você pode usar o [!DNL Databricks] para integrar com o [!DNL Azure] e fornecer um ambiente holístico para criar, implantar e gerenciar soluções de dados em escala.

Use a fonte [!DNL Databricks] para conectar sua conta e assimilar os dados do [!DNL Databricks] na Adobe Experience Platform.

## Pré-requisitos

Conclua as etapas de pré-requisito para conectar com êxito sua conta do [!DNL Databricks] à Experience Platform.

### Recuperar credenciais do container

Recupere as credenciais do Experience Platform [!DNL Azure Blob Storage] para habilitar a conta do [!DNL Databricks] para acessá-la mais tarde.

Para recuperar suas credenciais, faça uma solicitação do GET para o ponto de extremidade `/credentials` da API [!DNL Connectors].

**Formato da API**

```http
GET /data/foundation/connectors/landingzone/credentials?type=dlz_databricks_source
```

**Solicitação**

A solicitação a seguir recupera as credenciais para o Experience Platform [!DNL Azure Blob Storage].

+++Exibir exemplo de solicitação

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=dlz_databricks_source' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**Resposta**

Uma resposta bem-sucedida fornece suas credenciais (`containerName`, `SASToken`, `storageAccountName`) para uso posterior na configuração [!DNL Apache Spark] para [!DNL Databricks].

+++Exibir exemplo de resposta

```json
{
    "containerName": "dlz-databricks-container",
    "SASToken": "sv=2020-10-02&si=dlz-b1f4060b-6bbd-4043-9bd9-a5f5be72de30&sr=c&sp=racwdlm&sig=zVQfmuElZJzOKkUk8z5lChrJ3YQUE2h6EShDZOsVeMc%3D",
    "storageAccountName": "sndbxdtlndga8m7ajbvgc64k",
    "SASUri": "https://sndbxdtlndga8m7ajbvgc64k.blob.core.windows.net/dlz-databricks-container?sv=2020-10-02&si=dlz-b1f4060b-6bbd-4043-9bd9-a5f5be72de30&sr=c&sp=racwdlm&sig=zVQfmuElZJzOKkUk8z5lChrJ3YQUE2h6EShDZOsVeMc%3D",
    "expiryDate": "2025-07-05"
}
```

| Propriedade | Descrição |
| --- | --- |
| `containerName` | O nome do seu container [!DNL Azure Blob Storage]. Você usará esse valor posteriormente ao concluir a configuração do [!DNL Apache Spark] para [!DNL Databricks]. |
| `SASToken` | O token de assinatura de acesso compartilhado para o seu [!DNL Azure Blob Storage]. Esta cadeia de caracteres contém todas as informações necessárias para autorizar uma solicitação. |
| `storageAccountName` | O nome da sua conta de armazenamento. |
| `SASUri` | O URI de assinatura de acesso compartilhado para o seu [!DNL Azure Blob Storage]. Esta cadeia de caracteres é uma combinação do URI para o [!DNL Azure Blob Storage] para o qual você está sendo autenticado e seu token SAS correspondente. |
| `expiryDate` | A data em que o token SAS expirará. Você deve atualizar seu token antes da data de expiração para continuar usando-o em seu aplicativo para carregar dados para o [!DNL Azure Blob Storage]. Se você não atualizar manualmente o token antes da data de expiração declarada, ele será atualizado automaticamente e fornecerá um novo token quando a chamada de credenciais do GET for executada. |

+++

### Atualizar suas credenciais

>[!NOTE]
>
>Suas credenciais existentes serão revogadas assim que você atualizar suas credenciais. Portanto, você deve atualizar suas configurações do [!DNL Spark] adequadamente sempre que atualizar suas credenciais de armazenamento. Caso contrário, seu fluxo de dados falhará.

Para atualizar suas credenciais, faça uma solicitação POST e inclua `action=refresh` como parâmetro de consulta.

**Formato da API**

```http
POST /data/foundation/connectors/landingzone/credentials?type=dlz_databricks_source&action=refresh
```

**Solicitação**

A solicitação a seguir atualiza as credenciais para o [!DNL Azure Blob Storage].

+++Exibir exemplo de solicitação

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=dlz_databricks_source&action=refresh' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**Resposta**

Uma resposta bem-sucedida retorna suas novas credenciais.

+++Exibir exemplo de resposta

```json
{
    "containerName": "dlz-databricks-container",
    "SASToken": "sv=2020-10-02&si=dlz-6e17e5d6-de18-4efc-88c7-45f37d242617&sr=c&sp=racwdlm&sig=wvA4K3fcEmqAA%2FPvcMhB%2FA8y8RLwVJ7zhdWbxvT1uFM%3D",
    "storageAccountName": "sndbxdtlndga8m7ajbvgc64k",
    "SASUri": "https://sndbxdtlndga8m7ajbvgc64k.blob.core.windows.net/dlz-databricks-container?sv=2020-10-02&si=dlz-6e17e5d6-de18-4efc-88c7-45f37d242617&sr=c&sp=racwdlm&sig=wvA4K3fcEmqAA%2FPvcMhB%2FA8y8RLwVJ7zhdWbxvT1uFM%3D",
    "expiryDate": "2025-07-20"
}
```

+++

### Configurar acesso ao seu [!DNL Azure Blob Storage]

>[!IMPORTANT]
>
>* Se o cluster tiver sido encerrado, o serviço o reiniciará automaticamente durante uma execução de fluxo. No entanto, você deve garantir que seu cluster esteja ativo ao criar uma conexão ou um fluxo de dados. Além disso, seu cluster deverá estar ativo se você estiver executando ações como visualização ou exploração de dados, pois essas ações não podem solicitar a reinicialização automática de um cluster encerrado.
>
>* O contêiner [!DNL Azure] inclui uma pasta chamada `adobe-managed-staging`. Para garantir a assimilação perfeita de dados, **não** modifique esta pasta.


Em seguida, verifique se o cluster [!DNL Databricks] tem acesso à conta [!DNL Azure Blob Storage] do Experience Platform. Ao fazer isso, você pode usar [!DNL Azure Blob Storage] como um local temporário para gravar dados da tabela [!DNL delta lake].

Para fornecer acesso, você deve configurar um token SAS no cluster [!DNL Databricks] como parte de sua configuração [!DNL Apache Spark].

Na interface [!DNL Databricks], selecione **[!DNL Advanced options]** e insira o seguinte na caixa de entrada [!DNL Spark config].

```shell
fs.azure.sas.{CONTAINER_NAME}.{STORAGE-ACCOUNT}.blob.core.windows.net {SAS-TOKEN}
```

| Propriedade | Descrição |
| --- | --- |
| Nome do container | O nome do seu container. Você pode obter esse valor recuperando suas credenciais do [!DNL Azure Blob Storage]. |
| Conta de armazenamento | O nome da sua conta de armazenamento. Você pode obter esse valor recuperando suas credenciais do [!DNL Azure Blob Storage]. |
| Token SAS | O token de assinatura de acesso compartilhado para o seu [!DNL Azure Blob Storage]. Você pode obter esse valor recuperando suas credenciais do [!DNL Azure Blob Storage]. |

![A interface do usuário do Databricks no Azure.](../../images/tutorials/create/databricks/databricks-ui.png)

Se não for fornecida, a atividade de cópia na execução do fluxo falhará e retornará o seguinte erro:

```shell
Unable to access container '{CONTAINER_NAME}' in account '{STORAGE_ACCOUNT}.blob.core.windows.net' using anonymous credentials. No credentials found in the configuration. Public access is not permitted on this storage account.
```

## Conectar [!DNL Databricks] ao Experience Platform

Agora que você concluiu as etapas de pré-requisito, pode prosseguir e conectar sua conta do [!DNL Databricks] à Experience Platform:

* [Conectar-se por meio da API](../../tutorials/api/create/databases/databricks.md)
* [Conectar-se por meio do espaço de trabalho de origens na interface](../../tutorials/ui/create/databases/databricks.md)
