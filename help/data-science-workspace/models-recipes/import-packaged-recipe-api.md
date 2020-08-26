---
keywords: Experience Platform;import packaged recipe;Data Science Workspace;popular topics
solution: Experience Platform
title: Importar uma fórmula empacotada (API)
topic: Tutorial
translation-type: tm+mt
source-git-commit: 690ddbd92f0a2e4e06b988e761dabff399cd2367
workflow-type: tm+mt
source-wordcount: '955'
ht-degree: 2%

---


# Importar uma fórmula empacotada (API)

Este tutorial usa o para [!DNL Sensei Machine Learning API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) criar um [Mecanismo](../api/engines.md), também conhecido como Receita na interface do usuário.

Antes de começar, é importante observar que a Adobe Experience Platform [!DNL Data Science Workspace] usa termos diferentes para fazer referência a elementos semelhantes dentro da API e da interface do usuário. Os termos da API são usados neste tutorial e a tabela a seguir descreve os termos correspondentes:

| Termo da interface do usuário | Termo da API |
| ---- | ---- |
| Receita | [Mecanismo](../api/engines.md) |
| Modelo | [Instância MLI](../api/mlinstances.md) |
| Formação e avaliação | [Experimento](../api/experiments.md) |
| Serviço de | [MLService](../api/mlservices.md) |

Um Mecanismo contém algoritmos e lógica de aprendizado de máquina para resolver problemas específicos. O diagrama abaixo fornece uma visualização mostrando o fluxo de trabalho da API em [!DNL Data Science Workspace]. Este tutorial foca na criação de um Mecanismo, o cérebro de um Modelo de aprendizado de máquina.

![](../images/models-recipes/import-package-api/engine_hierarchy_api.png)

## Introdução

Este tutorial requer um arquivo de Receita empacotado na forma de um URL do Docker. Siga os arquivos de origem do [pacote em um tutorial de Receita](./package-source-files-recipe.md) para criar um arquivo de Receita empacotado ou fornecer seu próprio.

- `{DOCKER_URL}`: Um endereço de URL para uma imagem do Docker de um serviço inteligente.

Este tutorial requer que você tenha concluído o tutorial [](../../tutorials/authentication.md) Autenticação para Adobe Experience Platform para fazer chamadas com êxito para [!DNL Platform] APIs. A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de [!DNL Experience Platform] API, como mostrado abaixo:

- `{ACCESS_TOKEN}`: O valor do token do portador específico fornecido após a autenticação.
- `{IMS_ORG}`: Suas credenciais organizacionais IMS encontradas na sua integração exclusiva ao Adobe Experience Platform.
- `{API_KEY}`: O valor da sua chave de API específica foi encontrado na sua integração exclusiva ao Adobe Experience Platform.

## Criar um mecanismo

Os mecanismos podem ser criados fazendo uma solicitação POST para o terminal /mecanismos. O Mecanismo criado é configurado com base no formulário do arquivo de Receita empacotado que deve ser incluído como parte da solicitação de API.

### Criar um mecanismo com um URL de docking {#create-an-engine-with-a-docker-url}

Para criar um Mecanismo com um arquivo de Receita empacotado armazenado em um container Docker, é necessário fornecer o URL do Docker ao arquivo de Receita empacotado.

>[!CAUTION]
>
> Se você estiver usando [!DNL Python] ou usando R, use a solicitação abaixo. Se você estiver usando PySpark ou Scala, use o exemplo de solicitação PySpark/Scala localizado abaixo do exemplo Python/R.

**Formato da API**

```http
POST /engines
```

**Python/R de solicitação**

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: {ACCESS_TOKEN}' \
    -H 'X-API-KEY: {API_KEY}' \
    -H 'content-type: multipart/form-data' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `engine.name` | O nome desejado para o Mecanismo. A Receita correspondente a este Mecanismo herdará esse valor para ser exibido na interface [!DNL Data Science Workspace] do usuário como o nome da Receita. |
| `engine.description` | Uma descrição opcional para o mecanismo. A Receita correspondente a este Mecanismo herdará esse valor para ser exibido na interface [!DNL Data Science Workspace] do usuário como a descrição da Receita. Não remova essa propriedade, deixe esse valor ser uma string vazia se você optar por não fornecer uma descrição. |
| `engine.type` | O tipo de execução do Mecanismo. Esse valor corresponde ao idioma no qual a imagem do Docker é desenvolvida. Quando um URL do Docker é fornecido para criar um Mecanismo, `type` é `Python`, `R`, `PySpark`, `Spark` (Scala) ou `Tensorflow`. |
| `artifacts.default.image.location` | O seu `{DOCKER_URL}` vai aqui. Um URL completo do Docker tem a seguinte estrutura: `your_docker_host.azurecr.io/docker_image_file:version` |
| `artifacts.default.image.name` | Um nome adicional para o arquivo de imagem Docker. Não remova essa propriedade, deixe esse valor ser uma string vazia se você optar por não fornecer um nome de arquivo de imagem do Docker adicional. |
| `artifacts.default.image.executionType` | O tipo de execução deste Mecanismo. Esse valor corresponde ao idioma no qual a imagem do Docker é desenvolvida. Quando um URL do Docker é fornecido para criar um Mecanismo, `executionType` é `Python`, `R`, `PySpark`, `Spark` (Scala) ou `Tensorflow`. |

**Solicitar PySpark**

```shell
curl -X POST \
  https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `name` | O nome desejado para o Mecanismo. A Receita correspondente a este Mecanismo herdará esse valor para ser exibido na interface do usuário como o nome da Receita. |
| `description` | Uma descrição opcional para o mecanismo. A Receita correspondente a este Mecanismo herdará esse valor para ser exibido na interface do usuário como a descrição da Receita. Esta propriedade é obrigatória. Se você não quiser fornecer uma descrição, defina seu valor como uma string vazia. |
| `type` | O tipo de execução do Mecanismo. Esse valor corresponde ao idioma no qual a imagem do Docker é criada em &quot;PySpark&quot;. |
| `mlLibrary` | Um campo que é necessário ao criar mecanismos para fórmulas PySpark e Scala. |
| `artifacts.default.image.location` | O local da imagem do Docker vinculada por um URL do Docker. |
| `artifacts.default.image.executionType` | O tipo de execução do Mecanismo. Esse valor corresponde ao idioma no qual a imagem do Docker é criada em &quot;Spark&quot;. |

**Solicitar Scala**

```shell
curl -X POST \
  https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `name` | O nome desejado para o Mecanismo. A Receita correspondente a este Mecanismo herdará esse valor para ser exibido na interface do usuário como o nome da Receita. |
| `description` | Uma descrição opcional para o mecanismo. A Receita correspondente a este Mecanismo herdará esse valor para ser exibido na interface do usuário como a descrição da Receita. Esta propriedade é obrigatória. Se você não quiser fornecer uma descrição, defina seu valor como uma string vazia. |
| `type` | O tipo de execução do Mecanismo. Esse valor corresponde ao idioma no qual a imagem do Docker é criada em &quot;Spark&quot;. |
| `mlLibrary` | Um campo que é necessário ao criar mecanismos para fórmulas PySpark e Scala. |
| `artifacts.default.image.location` | O local da imagem do Docker vinculada por um URL do Docker. |
| `artifacts.default.image.executionType` | O tipo de execução do Mecanismo. Esse valor corresponde ao idioma no qual a imagem do Docker é criada em &quot;Spark&quot;. |

**Resposta**

Uma resposta bem-sucedida retorna uma carga contendo os detalhes do mecanismo recém-criado, incluindo seu identificador exclusivo (`id`). O exemplo de resposta a seguir é para um [!DNL Python] Mecanismo. As teclas `executionType` e `type` mudam com base no POST fornecido.

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

Uma resposta bem-sucedida mostra uma carga JSON com informações relacionadas ao mecanismo recém-criado. A `id` chave representa o identificador exclusivo do Mecanismo e é necessária no próximo tutorial para criar uma instância MLI. Certifique-se de que o identificador de mecanismo esteja salvo antes de continuar com as próximas etapas.

## Próximas etapas {#next-steps}

Você criou um Mecanismo usando a API e um identificador exclusivo do Mecanismo foi obtido como parte do corpo da resposta. Você pode usar esse identificador de Mecanismo no próximo tutorial à medida que aprende a [criar, treinar e avaliar um Modelo usando a API](./train-evaluate-model-api.md).