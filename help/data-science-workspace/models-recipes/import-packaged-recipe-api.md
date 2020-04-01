---
keywords: Experience Platform;import packaged recipe;Data Science Workspace;popular topics
solution: Experience Platform
title: Importar uma fórmula empacotada (API)
topic: Tutorial
translation-type: tm+mt
source-git-commit: 92dad525123d321e987de527ae6c7aab40b22bc4

---


# Importar uma fórmula empacotada (API)

Este tutorial usa a API [de aprendizado de máquina](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) Sensei para criar um [mecanismo](../api/engines.md), também conhecido como Receita na interface do usuário.

Antes de começar, é importante observar que a Adobe Experience Platform Data Science Workspace usa termos diferentes para fazer referência a elementos similares na API e na interface do usuário. Os termos da API são usados neste tutorial e a tabela a seguir descreve os termos correspondentes:

| Termo da interface do usuário | Termo da API |
| ---- | ---- |
| Receita | [Mecanismo](../api/engines.md) |
| Modelo | [Instância MLI](../api/mlinstances.md) |
| Formação e avaliação | [Experimento](../api/experiments.md) |
| Serviço de | [MLService](../api/mlservices.md) |

Um Mecanismo contém algoritmos e lógica de aprendizado de máquina para resolver problemas específicos. O diagrama abaixo fornece uma visualização mostrando o fluxo de trabalho da API na Data Science Workspace. Este tutorial foca na criação de um Mecanismo, o cérebro de um Modelo de aprendizado de máquina.

![](../images/models-recipes/import-package-api/engine_hierarchy_api.png)

## Introdução

Este tutorial requer um arquivo de Receita empacotado na forma de um artefato binário ou um URL de Docker. Siga os arquivos de origem do [pacote em um tutorial de Receita](./package-source-files-recipe.md) para criar um arquivo de Receita empacotado ou fornecer seu próprio.

- Artefato binário: O artefato binário (por exemplo, JAR, EGG) usado para criar um Mecanismo.
- `{DOCKER_URL}` : Um endereço de URL para uma imagem do Docker de um serviço inteligente.

Este tutorial requer que você tenha concluído o tutorial [](../../tutorials/authentication.md) Autenticação para a plataforma Adobe Experience para fazer chamadas com êxito para as APIs da plataforma. A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas da API da plataforma da experiência, como mostrado abaixo:

- `{ACCESS_TOKEN}`: O valor do token do portador específico fornecido após a autenticação.
- `{IMS_ORG}`: Suas credenciais organizacionais IMS encontradas na integração exclusiva da Adobe Experience Platform.
- `{API_KEY}`: O valor da chave da API específica encontrado na integração exclusiva da Adobe Experience Platform.

## Criar um mecanismo

Dependendo do formulário do arquivo de Receita empacotado a ser incluído como parte da solicitação de API, um Mecanismo é criado de uma das duas maneiras:
- [Criar um mecanismo com um artefato binário](#create-an-engine-with-a-binary-artifact)
- [Criar um mecanismo com um URL de docking](#create-an-engine-with-a-docker-url)

### Criar um mecanismo com um artefato binário

Para criar um Mecanismo usando um artefato empacotado `.jar` ou `.egg` binário local, é necessário fornecer o caminho absoluto para o arquivo de artefato binário no sistema de arquivos local. Considere navegar até o diretório que contém o artefato binário em um ambiente Terminal e executar o comando `pwd` Unix para o caminho absoluto.

A chamada a seguir cria um Mecanismo com um artefato binário:

#### Formato da API

```http
POST /engines
```

#### Solicitação

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: {ACCESS_TOKEN}' \
    -H 'X-API-KEY: {API_KEY}' \
    -H 'content-type: multipart/form-data' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -F 'engine={
        "name": "Retail Sales Engine PySpark",
        "description": "A description for Retail Sales Engine, this Engines execution type is PySpark",
        "type": "PySpark"
    }' \
    -F 'defaultArtifact=@path/to/binary/artifact/file/pysparkretailapp-0.1.0-py3.7.egg'
```

- `engine > name` : O nome desejado para o Mecanismo. A Receita correspondente a este Mecanismo herdará esse valor para ser exibido na interface do usuário da Data Science Workspace como o nome da Receita.
- `engine > description` : Uma descrição opcional para o mecanismo. A Receita correspondente a este Mecanismo herdará esse valor para ser exibido na interface do usuário da Data Science Workspace como a descrição da Receita. Não remova essa propriedade, deixe esse valor ser uma string vazia se você optar por não fornecer uma descrição.
- `engine > type`: O tipo de execução do Mecanismo. Esse valor corresponde à linguagem em que o artefato binário foi desenvolvido.

   >[!NOTE] Ao fazer upload de um artefato binário para criar um Mecanismo, ele `type` é `Spark` ou `PySpark`.

- `defaultArtifact` : O caminho absoluto para o arquivo de artefato binário usado para criar o Mecanismo.

   >[!NOTE] Certifique-se de incluir `@` antes do caminho do arquivo.

#### Resposta

```JSON
{
    "id": "00000000-1111-2222-3333-abcdefghijkl",
    "name": "Retail Sales Engine PySpark",
    "description": "A description for Retail Sales Engine, this Engines execution type is PySpark",
    "type": "PySpark",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "your_user_id@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "artifacts": {
        "default": {
            "image": {
                "location": "wasbs://some-storage-location.net/some-path/your-uploaded-binary-artifact.egg",
                "name": "pysparkretailapp-0.1.0-py3.7.egg",
                "executionType": "PySpark",
                "packagingType": "egg"
            }
        }
    }
}
```

Uma resposta bem-sucedida mostra uma carga JSON com informações relacionadas ao mecanismo recém-criado. A `id` chave representa o identificador exclusivo do Mecanismo e é necessária no próximo tutorial para criar uma instância MLI. Certifique-se de que o identificador de mecanismo esteja salvo antes de continuar com as [próximas etapas](#next-steps).

### Criar um mecanismo com um URL de docking

Para criar um Mecanismo com um arquivo de Receita empacotado armazenado em um container Docker, é necessário fornecer o URL do Docker ao arquivo de Receita empacotado.

A chamada a seguir cria um Mecanismo com um URL Docker:

#### Formato da API

```http
POST /engines
```

#### Solicitação

```shell
curl -X POST \
    https://platform.adobe.io/data/sensei/engines \
    -H 'Authorization: {ACCESS_TOKEN}' \
    -H 'X-API-KEY: {API_KEY}' \
    -H 'content-type: multipart/form-data' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

- `engine > name` : O nome desejado para o Mecanismo. A Receita correspondente a este Mecanismo herdará esse valor para ser exibido na interface do usuário da Data Science Workspace como o nome da Receita.
- `engine > description` : Uma descrição opcional para o mecanismo. A Receita correspondente a este Mecanismo herdará esse valor para ser exibido na interface do usuário da Data Science Workspace como a descrição da Receita. Não remova essa propriedade, deixe esse valor ser uma string vazia se você optar por não fornecer uma descrição.
- `engine > type`: O tipo de execução do Mecanismo. Esse valor corresponde ao idioma no qual a imagem do Docker é desenvolvida.

   >[!NOTE] Quando um URL do Docker é fornecido para criar um Mecanismo, `type` é `Python`, `R`ou `Tensorflow`.

- `artifacts > default > image > location` : O seu `{DOCKER_URL}` vai aqui. Um URL completo do Docker tem a seguinte estrutura:

   ```
   your_docker_host.azurecr.io/docker_image_file:version
   ```

- `artifacts > default > image > name` : Um nome adicional para o arquivo de imagem Docker. Não remova essa propriedade, deixe esse valor ser uma string vazia se você optar por não fornecer um nome de arquivo de imagem do Docker adicional.
- `artifacts > default > image > executionType` : O tipo de execução deste Mecanismo. Esse valor corresponde ao idioma no qual a imagem do Docker é desenvolvida.

   >[!NOTE] Quando um URL do Docker é fornecido para criar um Mecanismo, `executionType` é `Python`, `R`ou `Tensorflow`.

#### Resposta

```JSON
{
    "id": "00000000-1111-2222-3333-abcdefghijkl",
    "name": "Retail Sales Engine Python",
    "description": "A description for Retail Sales Engine, this Engines execution type is Python",
    "type": "Python",
    "created": "2019-01-01T00:00:00.000Z",
    "createdBy": {
        "userId": "your_user_id@AdobeID"
    },
    "updated": "2019-01-01T00:00:00.000Z",
    "artifacts": {
        "default": {
            "image": {
                "location": "{DOCKER_URL}",
                "name": "retail_sales_python",
                "executionType": "Python",
                "packagingType": "docker"
            }
        }
    }
}
```

Uma resposta bem-sucedida mostra uma carga JSON com informações relacionadas ao mecanismo recém-criado. A `id` chave representa o identificador exclusivo do Mecanismo e é necessária no próximo tutorial para criar uma instância MLI. Certifique-se de que o identificador de mecanismo esteja salvo antes de continuar com as próximas etapas.

## Próximas etapas

Você criou um Mecanismo usando a API e um identificador exclusivo do Mecanismo foi obtido como parte do corpo da resposta. Você pode usar esse identificador de Mecanismo no próximo tutorial à medida que aprende a [criar, treinar e avaliar um Modelo usando a API](./train-evaluate-model-api.md).