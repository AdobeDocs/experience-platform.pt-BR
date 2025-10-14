---
keywords: Experience Platform;página inicial;tópicos populares;Apache Spark;apache spark;Azure HDInsights
solution: Experience Platform
title: Criar uma conexão de base do Apache Spark no Azure HDInsights usando a API do serviço de fluxo
type: Tutorial
description: Saiba como conectar o Apache Spark no Azure HDInsights ao Adobe Experience Platform usando a API do Serviço de Fluxo.
exl-id: 1f7ca86e-32f4-45f7-92c2-f87c5c0c4ea4
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '495'
ht-degree: 5%

---

# Criar uma conexão base de [!DNL Apache Spark] em [!DNL Azure] HDInsights usando a API [!DNL Flow Service]

>[!NOTE]
>
>O conector [!DNL Apache Spark] em [!DNL Azure HDInsights] está na versão beta. Consulte a [Visão geral das fontes](../../../../home.md#terms-and-conditions) para obter mais informações sobre o uso de conectores rotulados com beta.

Uma conexão base representa a conexão autenticada entre uma origem e o Adobe Experience Platform.

Este tutorial guiará você pelas etapas para criar uma conexão básica para [!DNL Apache Spark] em [!DNL Azure HDInsights] (doravante denominada &quot;[!DNL Spark]&quot;) usando a [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Introdução

Este manual necessita de uma compreensão funcional dos seguintes componentes da Adobe Experience Platform:

* [Fontes](../../../../home.md): [!DNL Experience Platform] permite que os dados sejam assimilados de várias fontes e fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços do [!DNL Experience Platform].
* [Sandboxes](../../../../../sandboxes/home.md): [!DNL Experience Platform] fornece sandboxes virtuais que particionam uma única instância do [!DNL Experience Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito ao [!DNL Spark] usando a API [!DNL Flow Service].

### Coletar credenciais necessárias

Para que [!DNL Flow Service] se conecte a [!DNL Spark], você deve fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| `host` | O endereço IP ou o nome de host do servidor [!DNL Spark]. |
| `username` | O nome de usuário que você usa para acessar o Servidor [!DNL Spark]. |
| `password` | A senha correspondente ao usuário. |
| `connectionSpec.id` | A especificação de conexão retorna as propriedades do conector de uma origem, incluindo especificações de autenticação relacionadas à criação das conexões de base e de origem. A ID da especificação de conexão para [!DNL Spark] é: `6a8d82bc-1caf-45d1-908d-cadabc9d63a6` |

Para obter mais informações sobre como começar, consulte [este documento do Spark](https://docs.microsoft.com/en-us/azure/hdinsight/spark/apache-spark-overview).

### Uso de APIs do Experience Platform

Para obter informações sobre como fazer chamadas para APIs do Experience Platform com êxito, consulte o manual sobre [introdução às APIs do Experience Platform](../../../../../landing/api-guide.md).

## Criar uma conexão básica

Uma conexão base retém informações entre sua origem e a Experience Platform, incluindo as credenciais de autenticação da origem, o estado atual da conexão e a ID de conexão base exclusiva. A ID de conexão básica permite explorar e navegar pelos arquivos de dentro da origem e identificar os itens específicos que deseja assimilar, incluindo informações sobre os tipos de dados e formatos.

Para criar uma ID de conexão base, faça uma solicitação POST para o ponto de extremidade `/connections` ao fornecer suas credenciais de autenticação [!DNL Spark] como parte dos parâmetros de solicitação.

**Formato da API**

```https
POST /connections
```

**Solicitação**

A solicitação a seguir cria uma conexão base para [!DNL Spark]:


```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Spark test connection",
        "description": "A Spark test connection",
        "auth": {
            "specName": "HDInsights Basic Authentication",
        "params": {
            "host":  "{HOST}",
            "username": "{USERNAME}",
            "password":"{PASSWORD}"
            }
        },
        "connectionSpec": {
            "id": "6a8d82bc-1caf-45d1-908d-cadabc9d63a6",
            "version": "1.0"
        }
    }'
```

| Parâmetro | Descrição |
| --------- | ----------- |
| `auth.params.host` | O host do servidor [!DNL Spark]. |
| `auth.params.username` | O nome de usuário associado à sua conexão [!DNL Spark]. |
| `auth.params.password` | A senha associada à sua conexão [!DNL Spark]. |
| `connectionSpec.id` | A ID da especificação de conexão [!DNL Spark]: `6a8d82bc-1caf-45d1-908d-cadabc9d63a6`. |

**Resposta**

Uma resposta bem-sucedida retorna detalhes da conexão recém-criada, incluindo seu identificador exclusivo (`id`). Essa ID é necessária para explorar seus dados no próximo tutorial.

```json
{
    "id": "a45f2f58-e3a2-46ba-9f2f-58e3a2b6baf2",
    "etag": "\"900009d6-0000-0200-0000-5e8500010000\""
}
```

## Próximas etapas

Seguindo este tutorial, você criou uma conexão de base [!DNL Spark] usando a API [!DNL Flow Service]. Você pode usar essa ID de conexão básica nos seguintes tutoriais:

* [Explore a estrutura e o conteúdo das tabelas de dados usando a API  [!DNL Flow Service] &#x200B;](../../explore/tabular.md)
* [Crie um fluxo de dados para trazer dados do banco de dados para a Experience Platform usando a API  [!DNL Flow Service] &#x200B;](../../collect/database-nosql.md)
