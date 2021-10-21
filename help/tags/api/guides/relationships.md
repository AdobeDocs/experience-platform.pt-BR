---
title: Relações na API do reator
description: Saiba como as relações de recursos são estabelecidas na API do reator, incluindo os requisitos de relação para cada recurso.
exl-id: 23976978-a639-4eef-91b6-380a29ec1c14
source-git-commit: 7e4bc716e61b33563e0cb8059cb9f1332af7fd36
workflow-type: tm+mt
source-wordcount: '807'
ht-degree: 99%

---

# Relações na API do reator

Os recursos na API do reator são frequentemente relacionados entre si. Este documento fornece uma visão geral de como as relações de recursos são estabelecidas na API e os requisitos de relação de cada tipo de recurso.

Dependendo do tipo de recurso em questão, algumas relações são necessárias. Um relacionamento necessário implica que o recurso pai não pode existir sem o relacionamento. Todas as outras relações são opcionais.

Independentemente de serem obrigatórias ou opcionais, as relações são estabelecidas automaticamente pelo sistema quando os recursos relevantes são criados ou devem ser criadas manualmente. No caso de criar relações manualmente, há dois métodos possíveis dependendo do recurso em questão:

* [Criar por carga](#payload)
* [Criar por URL](#url) (somente para bibliotecas)

Consulte a seção [requisitos de relacionamento](#requirements) para obter uma lista de relacionamentos compatíveis com cada tipo de recurso e os métodos necessários para estabelecer esses relacionamentos, quando aplicável.

## Criar uma relação por carga {#payload}

Algumas relações devem ser estabelecidas manualmente ao criar inicialmente um recurso. Para fazer isso, você deve fornecer um objeto `relationship` na carga da solicitação ao criar o recurso pai pela primeira vez. Exemplos dessas relações:

* [Criação de um elemento de dados](../endpoints/data-elements.md#create) com as extensões necessárias
* [Criação de um ambiente](../endpoints/environments.md#create) com o relacionamento de host necessário

**Formato da API**

```http
POST /properties/{PROPERTY_ID}/{RESOURCE_TYPE}
```

| Parâmetro | Descrição |
| --- | --- |
| `{PROPERTY_ID}` | A ID da propriedade à qual o recurso pertence. |
| `{RESOURCE_TYPE}` | O tipo de recurso a ser criado. |

{style=&quot;table-layout:auto&quot;}

**Solicitação**

A solicitação a seguir cria um novo `rule_component`, estabelecendo relacionamentos com `rules` e um `extension`.

```shell
curl -X POST \
  https://reactor.adobe.io/properties/PRf606dbddfbdc44f580fc6f342b5ff9be/rule_components \
  -H 'Authorization: Bearer [TOKEN]' \
  -H 'x-api-key: [KEY]' \
  -H 'x-gw-ims-org-id: [ORG_ID]' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -H 'Content-Type: application/vnd.api+json' \
  -d '{
        "data": {
          "attributes": {
            "delegate_descriptor_id": "kessel-test::events::click",
            "name": "My Example Click Event",
            "settings": "{\"elementSelector\":\".accordion\",\"bubbleFireIfChildFired\":true}"
          },
          "relationships": {
            "extension": {
              "data": {
                "id": "EXa2865f4d14204fa094f247406424371b",
                "type": "extensions"
              }
            },
            "rules": {
              "data": [
                {
                  "id": "RLd53598e3f1884e63bbc8e9c95e463dcf",
                  "type": "rules"
                }
              ]
            }
          },
          "type": "rule_components"
        }
      }'
```

| Propriedade | Descrição |
| --- | --- |
| `relationships` | Um objeto que deve ser fornecido ao criar relações por carga. Cada chave nesse objeto representa um tipo de relacionamento específico. No exemplo acima, são estabelecidos os relacionamentos `extension` e `rules`, que são específicos a `rule_components`. Para obter mais informações sobre tipos de relacionamentos compatíveis com recursos diferentes, consulte a seção sobre [requisitos de relacionamento por recurso](#relationship-requirements-by-resource). |
| `data` | Cada tipo de relação fornecido no objeto `relationship` deve conter uma propriedade `data`, que faz referência a `id` e `type` do recurso com o qual uma relação está sendo estabelecida. Você pode criar uma relação com vários recursos do mesmo tipo formatando a propriedade `data` como uma matriz de objetos, com cada objeto contendo os `id` e `type` de um recurso aplicável. |
| `id` | O identificador exclusivo de um recurso. Cada `id` deve ser acompanhado por uma propriedade irmã `type`, indicando o tipo de recurso em questão. |
| `type` | O tipo de recurso conforme referenciado por um campo `id` irmão. Os valores aceitos são `data_elements`, `rules`, `extensions` e `environments`. |

{style=&quot;table-layout:auto&quot;}

## Criar uma relação por URL {#url}

Ao contrário de outros recursos, as bibliotecas estabelecem relações por meio de seus próprios pontos de extremidade dedicados `/relationship`. São exemplos:

* [Adicionar extensões, elementos de dados e regras a uma biblioteca](../endpoints/libraries.md#add-resources)
* [Atribuição de uma biblioteca a um ambiente](../endpoints/libraries.md#environment)

**Formato da API**

```http
POST /properties/{PROPERTY_ID}/libraries/{LIBRARY_ID}/relationships/{RESOURCE_TYPE}
```

| Parâmetro | Descrição |
| --- | --- |
| `{PROPERTY_ID}` | A ID da propriedade à qual a biblioteca pertence. |
| `{LIBRARY_ID}` | A ID da biblioteca para a qual você deseja criar uma relação. |
| `{RESOURCE_TYPE}` | O tipo de recurso para o qual o relacionamento está sendo direcionado. Os valores disponíveis são `environment`, `data_elements`, `extensions` e `rules`. |

**Solicitação**

A solicitação a seguir usa o ponto de extremidade `/relationships/environment` para uma biblioteca para criar uma relação com um ambiente.

```shell
curl -X POST \
  https://reactor.adobe.io/properties/PRf606dbddfbdc44f580fc6f342b5ff9be/libraries/LB10c1fd171cd347f19fcb8659a8d679ef/relationships/environment \
  -H 'Authorization: Bearer [TOKEN]' \
  -H 'x-api-key: [KEY]' \
  -H 'x-gw-ims-org-id: [ORG_ID]' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -H 'Content-Type: application/vnd.api+json' \
  -d '{
        "data": {
          "id": "ENf395a477d2b24ad696d65b901055b9dc",
          "type": "environments",
        }
      }'
```

| Propriedade | Descrição |
| --- | --- |
| `data` | Um objeto que faz referência ao `id` e `type` do recurso do target para o relacionamento. Se você estiver criando uma relação com vários recursos do mesmo tipo (como `extensions` e `rules`), a propriedade `data` deverá ser formatada como uma matriz de objetos, com cada objeto contendo os `id` e `type` de um recurso aplicável. |
| `id` | O identificador exclusivo de um recurso. Cada `id` deve ser acompanhado por uma propriedade irmã `type`, indicando o tipo de recurso em questão. |
| `type` | O tipo de recurso conforme referenciado por um campo `id` irmão. Os valores aceitos são `data_elements`, `rules`, `extensions` e `environments`. |

{style=&quot;table-layout:auto&quot;}

## Requisitos de relação por recurso {#requirements}

As tabelas a seguir descrevem as relações disponíveis para cada tipo de recurso, sejam essas relações necessárias ou não, e o método aceito para criar manualmente a relação, onde aplicável.

>[!NOTE]
>
>Se uma relação não estiver listada como sendo criada por carga ou URL, ela será automaticamente atribuída pelo sistema.

### Eventos de auditoria

| Relação | Obrigatório | Criar por carga | Criar por URL |
| :--- | :---: | :---: | :---: |
| `property` | ✓ |  |  |
| `entity` | Instantâneo |  |  |

{style=&quot;table-layout:auto&quot;}

### Builds

| Relação | Obrigatório | Criar por carga | Criar por URL |
| :--- | :---: | :---: | :---: |
| `data_elements` |  |  |  |
| `extensions` |  |  |  |
| `rules` |  |  |  |
| `environment` | Instantâneo |  |  |
| `library` | Instantâneo |  |  |
| `property` | Instantâneo |  |  |

{style=&quot;table-layout:auto&quot;}

### Retornos de chamada

| Relação | Obrigatório | Criar por carga | Criar por URL |
| :--- | :---: | :---: | :---: |
| `property` | Instantâneo |  |  |

{style=&quot;table-layout:auto&quot;}

### Empresas

| Relação | Obrigatório | Criar por carga | Criar por URL |
| :--- | :---: | :---: | :---: |
| `properties` |  |  |  |

{style=&quot;table-layout:auto&quot;}

### Elementos de dados

| Relação | Obrigatório | Criar por carga | Criar por URL |
| :--- | :---: | :---: | :---: |
| `libraries` |  |  |  |
| `revisions` | Instantâneo |  |  |
| `notes` |  |  |  |
| `property` | Instantâneo |  |  |
| `origin` | Instantâneo |  |  |
| `extension` | Instantâneo | Instantâneo |  |
| `updated_with_extension` | Instantâneo |  |  |
| `updated_with_extension_package` | Instantâneo |  |  |

{style=&quot;table-layout:auto&quot;}

### Ambientes

| Relação | Obrigatório | Criar por carga | Criar por URL |
| :--- | :---: | :---: | :---: |
| `library` |  |  |  |
| `builds` |  |  |  |
| `host` | Instantâneo | Instantâneo |  |
| `property` | Instantâneo |  |  |

{style=&quot;table-layout:auto&quot;}

### Extensões

| Relação | Obrigatório | Criar por carga | Criar por URL |
| :--- | :---: | :---: | :---: |
| `libraries` |  |  |  |
| `revisions` | Instantâneo |  |  |
| `notes` |  |  |  |
| `property` | Instantâneo |  |  |
| `origin` | Instantâneo |  |  |
| `extension_package` | Instantâneo | Instantâneo |  |
| `updated_with_extension_package` | Instantâneo |  |  |

{style=&quot;table-layout:auto&quot;}

### Hosts

| Relação | Obrigatório | Criar por carga | Criar por URL |
| :--- | :---: | :---: | :---: |
| `property` | Instantâneo |  |  |

{style=&quot;table-layout:auto&quot;}

### Bibliotecas

| Relação | Obrigatório | Criar por carga | Criar por URL |
| :--- | :---: | :---: | :---: |
| `builds` |  |  |  |
| `environment` |  |  | Instantâneo |
| `data_elements` |  |  | Instantâneo |
| `extensions` |  |  | Instantâneo |
| `rules` |  |  | Instantâneo |
| `notes` |  |  |  |
| `upstream_library` | Instantâneo |  |  |
| `property` | Instantâneo |  |  |
| `last_build` |  |  |  |

{style=&quot;table-layout:auto&quot;}

### Notas

| Relação | Obrigatório | Criar por carga | Criar por URL |
| :--- | :---: | :---: | :---: |
| `resource` | Instantâneo |  |  |

{style=&quot;table-layout:auto&quot;}

### Propriedades

| Relação | Obrigatório | Criar por carga | Criar por URL |
| :--- | :---: | :---: | :---: |
| `company` | Instantâneo |  |  |
| `callbacks` |  |  |  |
| `environments` |  |  |  |
| `libraries` |  |  |  |
| `data_elements` |  |  |  |
| `extensions` |  |  |  |
| `extensions` |  |  |  |

{style=&quot;table-layout:auto&quot;}

### Componentes da regra

| Relação | Obrigatório | Criar por carga | Criar por URL |
| :--- | :---: | :---: | :---: |
| `updated_with_extensions_package` | Instantâneo |  |  |
| `updated_with_extension` | Instantâneo |  |  |
| `extension` | Instantâneo | Instantâneo |  |
| `notes` |  |  |  |
| `origin` | Instantâneo |  |  |
| `property` | Instantâneo |  |  |
| `rules` | Instantâneo | Instantâneo |  |
| `revisions` | Instantâneo |  |  |

{style=&quot;table-layout:auto&quot;}

### Regras

| Relação | Obrigatório | Criar por carga | Criar por URL |
| :--- | :---: | :---: | :---: |
| `libraries` |  |  |  |
| `revisions` | Instantâneo |  |  |
| `notes` |  |  |  |
| `property` | Instantâneo |  |  |
| `origin` | Instantâneo |  |  |
| `rule_components` |  |  |  |

### Segredos

| Relação | Obrigatório | Criar por carga | Criar por URL |
| :--- | :---: | :---: | :---: |
| `property` | Instantâneo |  | Instantâneo |
| `environment` | Instantâneo | Instantâneo |  |

