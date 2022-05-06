---
keywords: Experience Platform, importar receita empacotada, Data Science Workspace, tópicos populares, receitas, api, aprendizado de máquina do sensei, criar mecanismo
solution: Experience Platform
title: Importar uma Receita Empacotada Usando a API de Aprendizagem de Máquina do Sensei
topic-legacy: tutorial
type: Tutorial
description: Este tutorial usa a API do Sensei Machine Learning para criar um Mecanismo, também conhecido como Receita na interface do usuário.
exl-id: c8dde30b-5234-448d-a597-f1c8d32f23d4
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '1007'
ht-degree: 2%

---

# Importe uma receita empacotada usando a API de aprendizado de máquina do Sensei

Este tutorial usa o [[!DNL Sensei Machine Learning API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) para criar um [Mecanismo](../api/engines.md), também conhecida como Receita na interface do usuário do .

Antes de começar, é importante observar que o Adobe Experience Platform [!DNL Data Science Workspace] O usa termos diferentes para se referir a elementos semelhantes na API e na interface do usuário do . Os termos da API são usados em todo este tutorial e a tabela a seguir descreve os termos correlacionados:

| Termo da interface do usuário | Termo da API |
| ---- | ---- |
| Receita | [Mecanismo](../api/engines.md) |
| Modelo | [InstânciaMLI](../api/mlinstances.md) |
| Formação e avaliação | [Experimento](../api/experiments.md) |
| Serviço de | [MLService](../api/mlservices.md) |

Um Mecanismo contém algoritmos e lógica de aprendizado de máquina para resolver problemas específicos. O diagrama abaixo fornece uma visualização que mostra o fluxo de trabalho da API em [!DNL Data Science Workspace]. Este tutorial foca na criação de um Mecanismo, o cérebro de um Modelo de aprendizado de máquina.

![](../images/models-recipes/import-package-api/engine_hierarchy_api.png)

## Introdução

Este tutorial requer um arquivo de Receita empacotado na forma de um URL Docker. Siga as [Compactar arquivos de origem em uma Receita](./package-source-files-recipe.md) tutorial para criar um arquivo de Receita empacotada ou fornecer o seu próprio.

- `{DOCKER_URL}`: Um endereço de URL para uma imagem Docker de um serviço inteligente.

Este tutorial requer que você tenha completado o [Tutorial de autenticação para o Adobe Experience Platform](https://www.adobe.com/go/platform-api-authentication-en) para fazer chamadas para [!DNL Platform] APIs. A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todos [!DNL Experience Platform] Chamadas de API, conforme mostrado abaixo:

- `{ACCESS_TOKEN}`: O valor do token portador específico fornecido após a autenticação.
- `{ORG_ID}`: Suas credenciais da organização IMS encontradas na integração exclusiva do Adobe Experience Platform.
- `{API_KEY}`: Seu valor específico da chave de API encontrado na integração exclusiva do Adobe Experience Platform.

## Criar um mecanismo

Os mecanismos podem ser criados fazendo uma solicitação POST para o endpoint /engines . O Mecanismo criado é configurado com base no formulário do arquivo de Receita empacotado que deve ser incluído como parte da solicitação da API.

### Criar um mecanismo com um URL de Docker {#create-an-engine-with-a-docker-url}

Para criar um Mecanismo com um arquivo de Receita empacotado armazenado em um container Docker, você deve fornecer o URL do Docker ao arquivo de Receita empacotada.

>[!CAUTION]
>
> Se estiver usando [!DNL Python] Utilizar a solicitação abaixo. Se você estiver usando PySpark ou Scala, use o exemplo de solicitação PySpark/Scala localizado abaixo do exemplo Python/R.

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
| `engine.name` | O nome desejado para o Mecanismo. A Receita correspondente a este Mecanismo herdará esse valor a ser exibido em [!DNL Data Science Workspace] interface de usuário como o nome da Receita. |
| `engine.description` | Uma descrição opcional do mecanismo. A Receita correspondente a este Mecanismo herdará esse valor a ser exibido em [!DNL Data Science Workspace] interface do usuário como a descrição da Receita. Não remova essa propriedade, deixe esse valor como uma sequência vazia se você optar por não fornecer uma descrição. |
| `engine.type` | O tipo de execução do mecanismo. Esse valor corresponde ao idioma em que a imagem do Docker é desenvolvida. Quando um URL do Docker é fornecido para criar um Mecanismo, `type` é `Python`, `R`, `PySpark`, `Spark` (Escala) ou `Tensorflow`. |
| `artifacts.default.image.location` | Seu `{DOCKER_URL}` vai aqui. Um URL completo do Docker tem a seguinte estrutura: `your_docker_host.azurecr.io/docker_image_file:version` |
| `artifacts.default.image.name` | Um nome adicional para o arquivo de imagem Docker. Não remova essa propriedade. Deixe esse valor como uma sequência vazia se você optar por não fornecer um nome de arquivo de imagem Docker adicional. |
| `artifacts.default.image.executionType` | O tipo de execução desse mecanismo. Esse valor corresponde ao idioma em que a imagem do Docker é desenvolvida. Quando um URL do Docker é fornecido para criar um Mecanismo, `executionType` é `Python`, `R`, `PySpark`, `Spark` (Escala) ou `Tensorflow`. |

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
| `name` | O nome desejado para o Mecanismo. A Receita correspondente a este Mecanismo herdará esse valor a ser exibido na interface do usuário como o nome da Receita. |
| `description` | Uma descrição opcional do mecanismo. A Receita correspondente a este Mecanismo herdará esse valor a ser exibido na interface do usuário como a descrição da Receita. Esta propriedade é obrigatória. Se não quiser fornecer uma descrição, defina seu valor como uma string vazia. |
| `type` | O tipo de execução do mecanismo. Esse valor corresponde ao idioma no qual a imagem do Docker é criada a partir de &quot;PySpark&quot;. |
| `mlLibrary` | Um campo necessário ao criar mecanismos para fórmulas PySpark e Scala. |
| `artifacts.default.image.location` | O local da imagem do Docker vinculada a um URL do Docker. |
| `artifacts.default.image.executionType` | O tipo de execução do mecanismo. Esse valor corresponde ao idioma no qual a imagem do Docker é criada em &quot;Spark&quot;. |

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
| `name` | O nome desejado para o Mecanismo. A Receita correspondente a este Mecanismo herdará esse valor a ser exibido na interface do usuário como o nome da Receita. |
| `description` | Uma descrição opcional do mecanismo. A Receita correspondente a este Mecanismo herdará esse valor a ser exibido na interface do usuário como a descrição da Receita. Esta propriedade é obrigatória. Se não quiser fornecer uma descrição, defina seu valor como uma string vazia. |
| `type` | O tipo de execução do mecanismo. Esse valor corresponde ao idioma no qual a imagem do Docker é criada em &quot;Spark&quot;. |
| `mlLibrary` | Um campo necessário ao criar mecanismos para fórmulas PySpark e Scala. |
| `artifacts.default.image.location` | O local da imagem do Docker vinculada a um URL do Docker. |
| `artifacts.default.image.executionType` | O tipo de execução do mecanismo. Esse valor corresponde ao idioma no qual a imagem do Docker é criada em &quot;Spark&quot;. |

**Resposta**

Uma resposta bem-sucedida retorna uma carga contendo os detalhes do mecanismo recém-criado, incluindo seu identificador exclusivo (`id`). O exemplo de resposta a seguir é para um [!DNL Python] Motor. O `executionType` e `type` as chaves mudam de acordo com o POST fornecido.

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

Uma resposta bem-sucedida mostra uma carga JSON com informações sobre o mecanismo recém-criado. O `id` A chave representa o identificador exclusivo do mecanismo e é necessária no próximo tutorial para criar uma instância MLI. Verifique se o identificador do mecanismo foi salvo antes de continuar com as próximas etapas.

## Próximas etapas {#next-steps}

Você criou um mecanismo usando a API e um identificador exclusivo de mecanismo foi obtido como parte do corpo da resposta. Você pode usar esse identificador de mecanismo no próximo tutorial ao saber como [criar, treinar e avaliar um Modelo usando a API](./train-evaluate-model-api.md).
