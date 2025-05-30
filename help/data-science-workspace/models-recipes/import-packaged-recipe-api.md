---
keywords: Experience Platform;importar receita empacotada;Data Science Workspace;tópicos populares;receitas;api;aprendizado de máquina do sensei;criar mecanismo;;import packaged revenue;Data Science;popular topics;recipes;api;sensei machine learning;create engine
solution: Experience Platform
title: Importar uma fórmula empacotada usando a API de aprendizado de máquina do Sensei
type: Tutorial
description: Este tutorial usa a API de aprendizado de máquina do Sensei para criar um mecanismo, também conhecido como fórmula na interface do usuário.
exl-id: c8dde30b-5234-448d-a597-f1c8d32f23d4
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '1018'
ht-degree: 3%

---

# Importe uma fórmula em pacote usando a API do Sensei Machine Learning

>[!NOTE]
>
>O Data Science Workspace não está mais disponível para compra.
>
>Esta documentação destina-se aos clientes existentes com direitos anteriores ao Data Science Workspace.

Este tutorial usa o [[!DNL Sensei Machine Learning API]](https://developer.adobe.com/experience-platform-apis/references/sensei-machine-learning/) para criar um [Engine](../api/engines.md), também conhecido como Receita na interface do usuário.

Antes de começar, é importante observar que o Adobe Experience Platform [!DNL Data Science Workspace] usa termos diferentes para se referir a elementos semelhantes na API e na interface. Os termos da API são usados neste tutorial e a tabela a seguir descreve os termos correlacionados:

| Termo da interface | Termo da API |
| ---- | ---- |
| Fórmula | [Mecanismo](../api/engines.md) |
| Modelo | [MLInstance](../api/mlinstances.md) |
| Treinamento e avaliação | [Experimento](../api/experiments.md) |
| Serviço | [ServiçoMLS](../api/mlservices.md) |

Um mecanismo contém algoritmos e lógica de aprendizado de máquina para resolver problemas específicos. O diagrama abaixo fornece uma visualização mostrando o fluxo de trabalho da API em [!DNL Data Science Workspace]. Este tutorial foca em criar um mecanismo, o cérebro de um modelo de aprendizado de máquina.

![](../images/models-recipes/import-package-api/engine_hierarchy_api.png)

## Introdução

Este tutorial requer um arquivo de fórmula empacotado na forma de um URL Docker. Siga o tutorial [Empacotar arquivos de origem em uma Receita](./package-source-files-recipe.md) para criar um arquivo de Receita empacotado ou fornecer o seu próprio arquivo.

- `{DOCKER_URL}`: Um endereço de URL para uma imagem Docker de um serviço inteligente.

Este tutorial requer que você tenha concluído o [tutorial de Autenticação para Adobe Experience Platform](https://www.adobe.com/go/platform-api-authentication-en) para fazer chamadas com êxito para APIs [!DNL Experience Platform]. Concluir o tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API da [!DNL Experience Platform], conforme mostrado abaixo:

- `{ACCESS_TOKEN}`: Seu valor de token de portador específico fornecido após a autenticação.
- `{ORG_ID}`: as credenciais da sua organização foram encontradas em sua integração exclusiva com o Adobe Experience Platform.
- `{API_KEY}`: O valor da sua chave de API específica foi encontrado na sua integração exclusiva do Adobe Experience Platform.

## Criar um mecanismo

Os mecanismos podem ser criados fazendo uma solicitação POST para o endpoint /engines. O mecanismo criado é configurado com base no formulário do arquivo de receita empacotado que deve ser incluído como parte da solicitação de API.

### Criar um mecanismo com um URL Docker {#create-an-engine-with-a-docker-url}

Para criar um mecanismo com um arquivo de fórmula empacotado armazenado em um contêiner do Docker, você deve fornecer o URL do Docker para o arquivo de fórmula empacotado.

>[!CAUTION]
>
> Se você estiver usando [!DNL Python] ou R, use a solicitação abaixo. Se você estiver usando PySpark ou Scala, use o exemplo de solicitação PySpark/Scala localizado abaixo do exemplo Python/R.

**Formato da API**

```http
POST /engines
```

**Solicitar Python/R**

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: {ACCESS_TOKEN}' \
    -H 'X-API-KEY: {API_KEY}' \
    -H 'content-type: multipart/form-data' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H `x-sandbox-name: {SANDBOX_NAME}` \
    -F 'engine={
        "name": "Retail Sales Engine Python",
        "description": "A description for Retail Sales Engine, this Engines execution type is Python",
        "type": "Python"
        "artifacts": {
            "default": {
                "image": {
                    "location": "{DOCKER_URL}",
                    "name": "retail_sales_python",
                    "executionType": "Python"
                }
            }
        }
    }' 
```

| Propriedade | Descrição |
| -------  | ----------- |
| `engine.name` | O nome desejado para o mecanismo. A fórmula correspondente a este mecanismo herdará esse valor para ser exibido na interface do usuário [!DNL Data Science Workspace] como o nome da fórmula. |
| `engine.description` | Uma descrição opcional do mecanismo. A fórmula correspondente a este mecanismo herdará esse valor para ser exibido na interface do usuário [!DNL Data Science Workspace] como a descrição da fórmula. Não remova essa propriedade, deixe esse valor ser uma string vazia se você optar por não fornecer uma descrição. |
| `engine.type` | O tipo de execução do Mecanismo. Esse valor corresponde ao idioma em que a imagem do Docker é desenvolvida no. Quando uma URL do Docker é fornecida para criar um Mecanismo, `type` é `Python`, `R`, `PySpark`, `Spark` (Scala) ou `Tensorflow`. |
| `artifacts.default.image.location` | Seu `{DOCKER_URL}` entra aqui. Uma URL completa do Docker tem a seguinte estrutura: `your_docker_host.azurecr.io/docker_image_file:version` |
| `artifacts.default.image.name` | Um nome adicional para o arquivo de imagem do Docker. Não remova essa propriedade, deixe esse valor ser uma string vazia se você optar por não fornecer um nome adicional de arquivo de imagem do Docker. |
| `artifacts.default.image.executionType` | O tipo de execução deste Mecanismo. Esse valor corresponde ao idioma em que a imagem do Docker é desenvolvida no. Quando uma URL do Docker é fornecida para criar um Mecanismo, `executionType` é `Python`, `R`, `PySpark`, `Spark` (Scala) ou `Tensorflow`. |

**Solicitar PySpark**

```shell
curl -X POST \
  https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: multipart/form-data' \
    -F 'engine={
    "name": "PySpark retail sales recipe",
    "description": "A description for this Engine",
    "type": "PySpark",
    "mlLibrary":"databricks-spark",
    "artifacts": {
        "default": {
            "image": {
                "name": "modelspark",
                "executionType": "PySpark",
                "packagingType": "docker",
                "location": "v1d2cs4mimnlttw.azurecr.io/sarunbatchtest:0.0.1"
            }
        }
    }
}'
```

| Propriedade | Descrição |
| --- | --- |
| `name` | O nome desejado para o mecanismo. A fórmula correspondente a este mecanismo herdará esse valor para ser exibido na interface do usuário como o nome da fórmula. |
| `description` | Uma descrição opcional do mecanismo. A fórmula correspondente a este mecanismo herdará esse valor para ser exibido na interface do usuário como a descrição da fórmula. Esta propriedade é obrigatória. Se não quiser fornecer uma descrição, defina o valor como uma cadeia de caracteres vazia. |
| `type` | O tipo de execução do Mecanismo. Esse valor corresponde ao idioma no qual a imagem do Docker é criada em &quot;PySpark&quot;. |
| `mlLibrary` | Um campo necessário ao criar mecanismos para receitas do PySpark e Scala. |
| `artifacts.default.image.location` | A localização da imagem do Docker vinculada por um URL do Docker. |
| `artifacts.default.image.executionType` | O tipo de execução do Mecanismo. Esse valor corresponde ao idioma no qual a imagem do Docker é criada no &quot;Spark&quot;. |

**Solicitar Escala**

```shell
curl -X POST \
  https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: multipart/form-data' \
    -F 'engine={
    "name": "Spark retail sales recipe",
    "description": "A description for this Engine",
    "type": "Spark",
    "mlLibrary":"databricks-spark",
    "artifacts": {
        "default": {
            "image": {
                "name": "modelspark",
                "executionType": "Spark",
                "packagingType": "docker",
                "location": "v1d2cs4mimnlttw.azurecr.io/sarunbatchtest:0.0.1"
            }
        }
    }
}'
```

| Propriedade | Descrição |
| --- | --- |
| `name` | O nome desejado para o mecanismo. A fórmula correspondente a este mecanismo herdará esse valor para ser exibido na interface do usuário como o nome da fórmula. |
| `description` | Uma descrição opcional do mecanismo. A fórmula correspondente a este mecanismo herdará esse valor para ser exibido na interface do usuário como a descrição da fórmula. Esta propriedade é obrigatória. Se não quiser fornecer uma descrição, defina o valor como uma cadeia de caracteres vazia. |
| `type` | O tipo de execução do Mecanismo. Esse valor corresponde ao idioma no qual a imagem do Docker é criada no &quot;Spark&quot;. |
| `mlLibrary` | Um campo necessário ao criar mecanismos para receitas do PySpark e Scala. |
| `artifacts.default.image.location` | A localização da imagem do Docker vinculada por um URL do Docker. |
| `artifacts.default.image.executionType` | O tipo de execução do Mecanismo. Esse valor corresponde ao idioma no qual a imagem do Docker é criada no &quot;Spark&quot;. |

**Resposta**

Uma resposta bem-sucedida retorna uma carga contendo os detalhes do Mecanismo recém-criado, incluindo seu identificador exclusivo (`id`). O exemplo de resposta a seguir é para um Mecanismo [!DNL Python]. As chaves `executionType` e `type` são alteradas com base no POST fornecido.

```json
{
    "id": "{ENGINE_ID}",
    "name": "A name for this Engine",
    "description": "A description for this Engine",
    "type": "Python",
    "algorithm": "Classification",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "artifacts": {
        "default": {
            "image": {
                "location": "{DOCKER_URL}",
                "name": "An additional name for the Docker image",
                "executionType": "Python",
                "packagingType": "docker"
            }
        }
    }
}
```

Uma resposta bem-sucedida mostra uma carga JSON com informações sobre o mecanismo recém-criado. A chave `id` representa o identificador de Mecanismo exclusivo e é necessária no próximo tutorial para criar uma MLInstance. Verifique se o identificador de Mecanismo está salvo antes de prosseguir para as próximas etapas.

## Próximas etapas {#next-steps}

Você criou um mecanismo usando a API e um identificador de mecanismo exclusivo foi obtido como parte do corpo da resposta. Você pode usar esse identificador de Mecanismo no próximo tutorial enquanto aprende a [criar, treinar e avaliar um Modelo usando a API](./train-evaluate-model-api.md).
