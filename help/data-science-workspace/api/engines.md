---
keywords: Experience Platform;developer guide;endpoint;Data Science Workspace;popular topics
solution: Experience Platform
title: Motores
topic: Developer guide
translation-type: tm+mt
source-git-commit: 19823c7cf0459e045366f0baae2bd8a98416154c

---


# Motores

Os mecanismos são a base para Modelos de aprendizado de máquina na Data Science Workspace. Eles contêm algoritmos de aprendizado de máquina que resolvem problemas específicos, pipelines de recursos para executar engenharia de recursos, ou ambos.

## Procure seu registro do Docker

>[!TIP]
>Se você não tiver um URL do Docker, visite os arquivos de origem do [pacote em um tutorial de fórmula](../models-recipes/package-source-files-recipe.md) para obter uma explicação passo a passo sobre como criar um URL de host do Docker.

Suas credenciais de registro do Docker são necessárias para carregar um arquivo de Receita empacotado, incluindo o URL do host do Docker, nome de usuário e senha. Você pode procurar essas informações executando a seguinte solicitação GET:

**Formato da API**

```http
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
>Sua senha do Docker muda sempre que `{ACCESS_TOKEN}` é atualizada.

```json
{
    "host": "docker_host.azurecr.io",
    "username": "00000000-0000-0000-0000-000000000000",
    "password": "password"
}
```

## Criar um mecanismo usando URLs do Docker {#docker-image}

Você pode criar um Mecanismo executando uma solicitação POST ao fornecer seus metadados e um URL do Docker que faz referência a uma imagem do Docker em formulários multipart.

**Formato da API**

```http
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
                    "location": "{DOCKER_URL}",
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

Ao fazer uma solicitação de receitas do PySpark, o e `executionType` é `type` &quot;PySpark&quot;. Ao solicitar receitas Scala, o e `executionType` `type` é &quot;Spark&quot;. O exemplo de fórmula Scala a seguir usa o Spark:

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
| `artifacts.default.image.location` | O local da imagem do Docker. Somente o Azure ACR ou o Dockerhub Público (não autenticado) são suportados. |
| `artifacts.default.image.executionType` | O tipo de execução do Mecanismo. Esse valor corresponde ao idioma no qual a imagem do Docker foi criada. Pode ser &quot;Spark&quot; ou &quot;PySpark&quot;. |

**Resposta**

Uma resposta bem-sucedida retorna uma carga contendo os detalhes do mecanismo recém-criado, incluindo seu identificador exclusivo (`id`). O exemplo de resposta a seguir é para um Mecanismo Python. Todas as respostas do mecanismo seguem este formato:

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

## Recuperar uma lista de mecanismos

Você pode recuperar uma lista de mecanismos executando uma única solicitação GET. Para ajudar a filtrar os resultados, você pode especificar parâmetros de query no caminho da solicitação. Para obter uma lista de query disponíveis, consulte a seção do apêndice sobre parâmetros de [query para recuperação](./appendix.md#query)de ativos.

**Formato da API**

```http
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
            "id": "{ENGINE_ID}",
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
            "id": "{ENGINE_ID}",
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
            "id": "{ENGINE_ID}",
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

Você pode recuperar os detalhes de um Mecanismo específico executando uma solicitação GET que inclui a ID do Mecanismo desejado no caminho da solicitação.

**Formato da API**

```http
GET /engines/{ENGINE_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{ENGINE_ID}` | A ID de um mecanismo existente. |

**Solicitação**

```shell
curl -X GET \
    https://platform.adobe.io/data/sensei/engines/{ENGINE_ID} \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Resposta**

Uma resposta bem-sucedida retorna uma carga contendo os detalhes do Mecanismo desejado.

```json
{
    "id": "{ENGINE_ID}",
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
                "location": "wasbs://artifact-location.blob.core.windows.net/{ENGINE_ID}/default.egg",
                "name": "file.egg",
                "executionType": "PySpark",
                "packagingType": "egg"
            }
        }
    }
}
```

## Atualizar um mecanismo

Você pode modificar e atualizar um Mecanismo existente sobrescrevendo suas propriedades por meio de uma solicitação PUT que inclua a ID do Mecanismo de público alvo no caminho da solicitação e fornecendo uma carga JSON contendo propriedades atualizadas.

>[!NOTE] Para garantir o sucesso desta solicitação PUT, recomenda-se que primeiro você execute uma solicitação GET para [recuperar o Mecanismo por ID](#retrieve-specific). Em seguida, modifique e atualize o objeto JSON retornado e aplique a totalidade do objeto JSON modificado como carga para a solicitação PUT.

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

```http
PUT /engines/{ENGINE_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{ENGINE_ID}` | A ID de um mecanismo existente. |

**Solicitação**

```shell
curl -X PUT \
    https://platform.adobe.io/data/sensei/engines/{ENGINE_ID} \
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
    "id": "{ENGINE_ID}",
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

Você pode excluir um Mecanismo executando uma solicitação DELETE ao especificar a ID do Mecanismo de público alvo no caminho da solicitação. A exclusão de um mecanismo fará com que todas as MLInensões que fazem referência a esse mecanismo sejam excluídas em cascata, incluindo todas as execuções de Experimentos e Experimentos pertencentes a essas MLInSubstituições.

**Formato da API**

```http
DELETE /engines/{ENGINE_ID}
```

| Parâmetro | Descrição |
| --- | --- |
| `{ENGINE_ID}` | A ID de um mecanismo existente. |

**Solicitação**

```shell
curl -X DELETE \
    https://platform.adobe.io/data/sensei/engines/{ENGINE_ID} \
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

## Solicitações obsoletas

>[!IMPORTANT]
>Os artefatos binários não são mais suportados e estão definidos para serem removidos em uma data posterior. As novas receitas do PySpark e do Scala agora devem seguir os exemplos de imagem [do](#docker-image) encaixe para criar um Mecanismo.

## Criar um mecanismo usando artefatos binários - obsoleto

Você pode criar um Mecanismo usando artefatos locais `.jar` ou `.egg` binários executando uma solicitação POST enquanto fornece seus metadados e o caminho do artefato em formulários de várias partes.

**Formato da API**

```http
POST /engines
```

**Solicitação**

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
        "algorithm": "Classification",
        "type": "PySpark",
    }' \
    -F 'defaultArtifact=@path/to/binary/artifact/file.egg'
```

| Propriedade | Descrição |
| --- | --- |
| `name` | O nome desejado para o Mecanismo. A Receita correspondente a este Mecanismo herdará esse valor para ser exibido na interface do usuário como o nome da Receita. |
| `description` | Uma descrição opcional para o mecanismo. A Receita correspondente a este Mecanismo herdará esse valor para ser exibido na interface do usuário como a descrição da Receita. Esta propriedade é obrigatória. Se você não quiser fornecer uma descrição, defina seu valor como uma string vazia. |
| `algorithm` | Uma string que especifica o tipo de algoritmo de aprendizado da máquina. Os tipos de algoritmos suportados incluem &quot;Classificação&quot;, &quot;Regressão&quot; ou &quot;Personalizado&quot;. |
| `type` | O tipo de execução do Mecanismo. Esse valor corresponde ao idioma no qual o artefato binário é criado e pode ser &quot;PySpark&quot; ou &quot;Spark&quot;. |


**Resposta**

Uma resposta bem-sucedida retorna uma carga contendo os detalhes do mecanismo recém-criado, incluindo seu identificador exclusivo (`id`).

```json
{
    "id": "{ENGINE_ID}",
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
                "location": "wasbs://artifact-location.blob.core.windows.net/Engine_ID/default.egg",
                "name": "file.egg",
                "executionType": "PySpark",
                "packagingType": "egg"
            }
        }
    }
}
```

## Criar um mecanismo de pipeline de recurso usando artefatos binários - obsoleto {#create-a-feature-pipeline-engine-using-binary-artifacts}

>[!IMPORTANT]
>Os artefatos binários não são mais suportados e estão definidos para serem removidos em uma data posterior.

Você pode criar um Mecanismo de pipeline de recursos usando artefatos locais `.jar` ou `.egg` binários executando uma solicitação POST enquanto fornece seus metadados e os caminhos do artefato em formulários multicomponentes. Um PySpark ou Spark Engine tem a capacidade de especificar recursos de computação, como o número de núcleos ou a quantidade de memória. Consulte a seção do apêndice sobre as configurações [de recursos](./appendix.md#resource-config) PySpark e Spark para obter mais informações.

**Formato da API**

```http
POST /engines
```

**Solicitação**

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'content-type: multipart/form-data' \
    -F 'engine={
        "name": "Feature Pipeline Engine",
        "description": "A feature pipeline Engine",
        "algorithm":"fp",
        "type": "PySpark"
    }' \
    -F 'featurePipelineOverrideArtifact=@path/to/binary/artifact/feature_pipeline.egg' \
    -F 'defaultArtifact=@path/to/binary/artifact/feature_pipeline.egg'
```

| Propriedade | Descrição |
| --- | --- |
| `name` | O nome desejado para o Mecanismo. A Receita correspondente a este Mecanismo herdará esse valor para ser exibido na interface do usuário como o nome da Receita. |
| `description` | Uma descrição opcional para o mecanismo. A Receita correspondente a este Mecanismo herdará esse valor para ser exibido na interface do usuário como a descrição da Receita. Esta propriedade é obrigatória. Se você não quiser fornecer uma descrição, defina seu valor como uma string vazia. |
| `algorithm` | Uma string que especifica o tipo de algoritmo de aprendizado da máquina. Defina esse valor como &quot;fp&quot; para especificar essa criação como um Mecanismo de pipeline de recurso. |
| `type` | O tipo de execução do Mecanismo. Esse valor corresponde ao idioma no qual os artefatos binários são criados e podem ser &quot;PySpark&quot; ou &quot;Spark&quot;. |

**Resposta**

Uma resposta bem-sucedida retorna uma carga contendo os detalhes do mecanismo recém-criado, incluindo seu identificador exclusivo (`id`).

```json
{
    "id": "{ENGINE_ID}",
    "name": "Feature Pipeline Engine",
    "description": "A feature pipeline Engine",
    "type": "PySpark",
    "algorithm": "fp",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "Jane_Doe@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "artifacts": {
        "default": {
            "image": {
                "location": "wasbs://artifact-location.blob.core.windows.net/Engine_ID/default.egg",
                "name": "file.egg",
                "executionType": "PySpark",
                "packagingType": "egg"
            }
        }
    }
}
```
