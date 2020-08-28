---
keywords: Experience Platform;developer guide;endpoint;Data Science Workspace;popular topics;engines;sensei machine learning api
solution: Experience Platform
title: Motores
topic: Developer guide
description: Os mecanismos são a base para Modelos de aprendizado de máquina na Data Science Workspace. Eles contêm algoritmos de aprendizado de máquina que resolvem problemas específicos, pipelines de recursos para executar engenharia de recursos, ou ambos.
translation-type: tm+mt
source-git-commit: 6e4a3ebe84c82790f58f8ec54e6f72c2aca0b7da
workflow-type: tm+mt
source-wordcount: '1147'
ht-degree: 3%

---


# Motores

Os mecanismos são a base para Modelos de aprendizado de máquina na Data Science Workspace. Eles contêm algoritmos de aprendizado de máquina que resolvem problemas específicos, pipelines de recursos para executar engenharia de recursos, ou ambos.

## Procure seu registro do Docker

>[!TIP]
>
>Se você não tiver um URL do Docker, visite os arquivos de origem do [pacote em um tutorial de fórmula](../models-recipes/package-source-files-recipe.md) para obter uma explicação passo a passo sobre como criar um URL de host do Docker.

Suas credenciais de registro do Docker são necessárias para carregar um arquivo de Receita empacotado, incluindo o URL do host do Docker, nome de usuário e senha. Você pode pesquisar essas informações executando a seguinte solicitação de GET:

**Formato da API**

```https
GET /engines/dockerRegistry
```

**Solicitação**

```shell
curl -X GET https://platform.adobe.io/data/sensei/engines/dockerRegistry \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna uma carga contendo os detalhes do registro do Docker, incluindo o URL do Docker (`host`), nome de usuário (`username`) e senha (`password`).

>[!NOTE]
>
>Sua senha do Docker muda sempre que `{ACCESS_TOKEN}` é atualizada.

```json
{
    "host": "docker_host.azurecr.io",
    "username": "00000000-0000-0000-0000-000000000000",
    "password": "password"
}
```

## Criar um mecanismo usando URLs do Docker {#docker-image}

Você pode criar um Mecanismo executando uma solicitação de POST ao fornecer seus metadados e um URL do Docker que faz referência a uma imagem do Docker em formulários de várias partes.

**Formato da API**

```https
POST /engines
```

**Python/R de solicitação**

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: multipart/form-data' \
    -F 'engine={
        "name": "A name for this Engine",
        "description": "A description for this Engine",
        "type": "Python",
        "algorithm": "Classification",
        "artifacts": {
            "default": {
                "image": {
                    "location": "v1rsvj32smc4wbs.azurecr.io/ml-featurepipeline-pyspark:1.0",
                    "name": "An additional name for the Docker image",
                    "executionType": "Python"
                }
            }
        }
    }' 
```

| Propriedade | Descrição |
| --- | --- |
| `name` | O nome desejado para o Mecanismo. A Receita correspondente a este Mecanismo herdará esse valor para ser exibido na interface do usuário como o nome da Receita. |
| `description` | Uma descrição opcional para o mecanismo. A Receita correspondente a este Mecanismo herdará esse valor para ser exibido na interface do usuário como a descrição da Receita. Esta propriedade é obrigatória. Se você não quiser fornecer uma descrição, defina seu valor como uma string vazia. |
| `type` | O tipo de execução do Mecanismo. Esse valor corresponde ao idioma no qual a imagem do Docker é criada e pode ser &quot;Python&quot;, &quot;R&quot; ou &quot;Tensorflow&quot;. |
| `algorithm` | Uma string que especifica o tipo de algoritmo de aprendizado da máquina. Os tipos de algoritmos suportados incluem &quot;Classificação&quot;, &quot;Regressão&quot; ou &quot;Personalizado&quot;. |
| `artifacts.default.image.location` | O local da imagem do Docker vinculada por um URL do Docker. |
| `artifacts.default.image.executionType` | O tipo de execução do Mecanismo. Esse valor corresponde ao idioma no qual a imagem do Docker é criada e pode ser &quot;Python&quot;, &quot;R&quot; ou &quot;Tensorflow&quot;. |

**Solicitar PySpark/Scala**

Ao fazer uma solicitação de receitas do PySpark, o e `executionType` é `type` &quot;PySpark&quot;. Ao fazer um pedido para receitas Scala, o e `executionType` é `type` &quot;Spark&quot;. O exemplo de fórmula Scala a seguir usa o Spark:

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
| `type` | O tipo de execução do Mecanismo. Esse valor corresponde ao idioma no qual a imagem do Docker foi criada. O valor pode ser definido como Spark ou PySpark. |
| `mlLibrary` | Um campo que é necessário ao criar mecanismos para fórmulas PySpark e Scala. Esse campo deve ser definido como `databricks-spark`. |
| `artifacts.default.image.location` | O local da imagem do Docker. Somente o ACR do Azure ou o Dockerhub Público (não autenticado) são suportados. |
| `artifacts.default.image.executionType` | O tipo de execução do Mecanismo. Esse valor corresponde ao idioma no qual a imagem do Docker foi criada. Pode ser &quot;Spark&quot; ou &quot;PySpark&quot;. |

**Resposta**

Uma resposta bem-sucedida retorna uma carga contendo os detalhes do mecanismo recém-criado, incluindo seu identificador exclusivo (`id`). A seguinte resposta de exemplo é para um Mecanismo Python. Todas as respostas do mecanismo seguem este formato:

```json
{
    "id": "22f4166f-85ba-4130-a995-a2b8e1edde32",
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
                "location": "v1rsvj32smc4wbs.azurecr.io/ml-featurepipeline-pyspark:1.0",
                "name": "An additional name for the Docker image",
                "executionType": "Python",
                "packagingType": "docker"
            }
        }
    }
}
```

## Criar um mecanismo de pipeline de recursos usando URLs Docker {#feature-pipeline-docker}

Você pode criar um mecanismo de pipeline de recursos executando uma solicitação de POST ao fornecer seus metadados e um URL do Docker que faz referência a uma imagem do Docker.

**Formato da API**

```https
POST /engines
```

**Solicitação**

```shell
curl -X POST \
 https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: Bearer ' \
    -H 'x-gw-ims-org-id: 20655D0F5B9875B20A495E23@AdobeOrg' \
    -H 'Content-Type: application/vnd.adobe.platform.sensei+json;profile=engine.v1.json' \
    -H 'x-api-key: acp_foundation_machineLearning' \
    -H 'Content-Type: text/plain' \
    -F '{
    "type": "PySpark",
    "algorithm":"fp",
    "name": "Feature_Pipeline_Engine",
    "description": "Feature_Pipeline_Engine",
    "mlLibrary": "databricks-spark",
    "artifacts": {
       "default": {
           "image": {
                "location": "v7d1cs2mimnlttw.azurecr.io/ml-featurepipeline-pyspark:0.2.1",
                "name": "datatransformation",
                "executionType": "PySpark",
                "packagingType": "docker"
            },
           "defaultMLInstanceConfigs": [ ...
           ]
       }
   }
}'
```

| Propriedade | Descrição |
| --- | --- |
| `type` | O tipo de execução do Mecanismo. Esse valor corresponde ao idioma no qual a imagem do Docker foi criada. O valor pode ser definido como Spark ou PySpark. |
| `algorithm` | O algoritmo que está sendo usado define esse valor como `fp` (pipeline de recursos). |
| `name` | O nome desejado para o Mecanismo de pipeline de recursos. A Receita correspondente a este Mecanismo herdará esse valor para ser exibido na interface do usuário como o nome da Receita. |
| `description` | Uma descrição opcional para o mecanismo. A Receita correspondente a este Mecanismo herdará esse valor para ser exibido na interface do usuário como a descrição da Receita. Esta propriedade é obrigatória. Se você não quiser fornecer uma descrição, defina seu valor como uma string vazia. |
| `mlLibrary` | Um campo que é necessário ao criar mecanismos para fórmulas PySpark e Scala. Esse campo deve ser definido como `databricks-spark`. |
| `artifacts.default.image.location` | O local da imagem do Docker. Somente o ACR do Azure ou o Dockerhub Público (não autenticado) são suportados. |
| `artifacts.default.image.executionType` | O tipo de execução do Mecanismo. Esse valor corresponde ao idioma no qual a imagem do Docker foi criada. Pode ser &quot;Spark&quot; ou &quot;PySpark&quot;. |
| `artifacts.default.image.packagingType` | O tipo de empacotamento do Mecanismo. Esse valor deve ser definido como `docker`. |
| `artifacts.default.defaultMLInstanceConfigs` | Parâmetros `pipeline.json` do arquivo de configuração. |

**Resposta**

Uma resposta bem-sucedida retorna uma carga contendo os detalhes do mecanismo de pipeline de recursos recém-criado, incluindo seu identificador exclusivo (`id`). O exemplo de resposta a seguir é para um Mecanismo de pipeline de recurso PySpark.

```json
{
    "id": "88236891-4309-4fd9-acd0-3de7827cecd1",
    "name": "Feature_Pipeline_Engine",
    "description": "Feature_Pipeline_Engine",
    "type": "PySpark",
    "algorithm": "fp",
    "mlLibrary": "databricks-spark",
    "created": "2020-04-24T20:46:58.382Z",
    "updated": "2020-04-24T20:46:58.382Z",
    "deprecated": false,
    "artifacts": {
        "default": {
            "image": {
                "location": "v7d1cs3mimnlttw.azurecr.io/ml-featurepipeline-pyspark:0.2.1",
                "name": "datatransformation",
                "executionType": "PySpark",
                "packagingType": "docker"
            },
        "defaultMLInstanceConfigs": [ ... ]
        }
    }
}
```

## Recuperar uma lista de mecanismos

Você pode recuperar uma lista de mecanismos executando uma única solicitação de GET. Para ajudar a filtrar os resultados, você pode especificar parâmetros de query no caminho da solicitação. Para obter uma lista de query disponíveis, consulte a seção do apêndice sobre parâmetros de [query para recuperação](./appendix.md#query)de ativos.

**Formato da API**

```https
GET /engines
GET /engines?parameter_1=value_1
GET /engines?parameter_1=value_1&parameter_2=value_2
```

**Solicitação**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna uma lista de mecanismos e seus detalhes.

```json
{
    "children": [
        {
            "id": "22f4166f-85ba-4130-a995-a2b8e1edde31",
            "name": "A name for this Engine",
            "description": "A description for this Engine",
            "type": "PySpark",
            "algorithm": "Classification",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-01T00:00:00.000Z"
        },
        {
            "id": "22f4166f-85ba-4130-a995-a2b8e1edde32",
            "name": "A name for this Engine",
            "description": "A description for this Engine",
            "type": "Python",
            "algorithm": "Classification",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-01T00:00:00.000Z"
        },
        {
            "id": "22f4166f-85ba-4130-a995-a2b8e1edde33",
            "name": "Feature Pipeline Engine",
            "description": "A feature pipeline Engine",
            "type": "PySpark",
            "algorithm":"fp",
            "created": "2019-01-01T00:00:00.000Z",
            "createdBy": {
                "userId": "Jane_Doe@AdobeID"
            },
            "updated": "2019-01-01T00:00:00.000Z"
        }
    ],
    "_page": {
        "property": "deleted==false",
        "totalCount": 100,
        "count": 3
    }
}
```

### Recuperar um mecanismo específico {#retrieve-specific}

Você pode recuperar os detalhes de um Mecanismo específico executando uma solicitação de GET que inclui a ID do Mecanismo desejado no caminho da solicitação.

**Formato da API**

```https
GET /engines/{ENGINE_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{ENGINE_ID}` | A ID de um mecanismo existente. |

**Solicitação**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/engines/22f4166f-85ba-4130-a995-a2b8e1edde32 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna uma carga contendo os detalhes do Mecanismo desejado.

```json
{
    "id": "22f4166f-85ba-4130-a995-a2b8e1edde32",
    "name": "A name for this Engine",
    "description": "A description for this Engine",
    "type": "PySpark",
    "algorithm": "Classification",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "artifacts": {
        "default": {
            "image": {
                "location": "v7d1cs2mimnlttw.azurecr.io/ml-featurepipeline-pyspark:0.2.1",
                "name": "file.egg",
                "executionType": "PySpark",
                "packagingType": "docker"
            }
        }
    }
}
```

## Atualizar um mecanismo

Você pode modificar e atualizar um Mecanismo existente sobrescrevendo suas propriedades por meio de uma solicitação de PUT que inclua a ID do Mecanismo de público alvo no caminho da solicitação e fornecendo uma carga JSON contendo propriedades atualizadas.

>[!NOTE]
>
>Para garantir o sucesso dessa solicitação de PUT, recomenda-se que primeiro você execute uma solicitação de GET para [recuperar o Mecanismo por ID](#retrieve-specific). Em seguida, modifique e atualize o objeto JSON retornado e aplique a totalidade do objeto JSON modificado como carga para a solicitação de PUT.

A chamada de exemplo de API a seguir atualizará o nome e a descrição de um Mecanismo ao ter essas propriedades inicialmente:

```json
{
    "name": "A name for this Engine",
    "description": "A description for this Engine",
    "type": "Python",
    "algorithm": "Classification",
    "artifacts": {
        "default": {
            "image": {
                "executionType": "Python",
                "packagingType": "docker"
            }
        }
    }
}
```

**Formato da API**

```https
PUT /engines/{ENGINE_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{ENGINE_ID}` | A ID de um mecanismo existente. |

**Solicitação**

```shell
curl -X PUT \
    https://platform.adobe.io/data/sensei/engines/22f4166f-85ba-4130-a995-a2b8e1edde32 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: application/vnd.adobe.platform.sensei+json;profile=engine.v1.json' \
    -d '{
        "name": "An updated name for this Engine",
        "description": "An updated description",
        "type": "Python",
        "algorithm": "Classification",
        "artifacts": {
            "default": {
                "image": {
                    "executionType": "Python",
                    "packagingType": "docker"
                }
            }
        }
    }'
```

**Resposta**

Uma resposta bem-sucedida retorna uma carga contendo os detalhes atualizados do Mecanismo.

```json
{
    "id": "22f4166f-85ba-4130-a995-a2b8e1edde32",
    "name": "An updated name for this Engine",
    "description": "An updated description",
    "type": "Python",
    "algorithm": "Classification",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "displayName": "Jane Doe",
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-02T00:00:00.000Z",
    "artifacts": {
        "default": {
            "image": {
                "executionType": "Python",
                "packagingType": "docker"
            }
        }
    }
}
```

## Excluir um mecanismo

Você pode excluir um Mecanismo executando uma solicitação de DELETE ao especificar a ID do Mecanismo de público alvo no caminho da solicitação. A exclusão de um mecanismo fará com que todas as MLInensões que fazem referência a esse mecanismo sejam excluídas em cascata, incluindo todas as execuções de Experimentos e Experimentos pertencentes a essas MLInSubstituições.

**Formato da API**

```https
DELETE /engines/{ENGINE_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{ENGINE_ID}` | A ID de um mecanismo existente. |

**Solicitação**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/engines/22f4166f-85ba-4130-a995-a2b8e1edde32 \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

```json
{
    "title": "Success",
    "status": 200,
    "detail": "Engine deletion was successful"
}
```
