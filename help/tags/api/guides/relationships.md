---
title: Relações na API do Reator
description: Saiba como os relacionamentos de recursos são estabelecidos na API do Reator, incluindo os requisitos de relacionamento para cada recurso.
source-git-commit: 6a1728bd995137a7cd6dc79313762ae6e665d416
workflow-type: tm+mt
source-wordcount: '798'
ht-degree: 10%

---

# Relações na API do Reator

Os recursos na API do reator são frequentemente relacionados entre si. Este documento fornece uma visão geral de como os relacionamentos de recursos são estabelecidos na API e os requisitos de relacionamento de cada tipo de recurso.

Dependendo do tipo de recurso em questão, algumas relações são necessárias. Um relacionamento necessário implica que o recurso pai não pode existir sem o relacionamento. Todas as outras relações são opcionais.

Independentemente de serem obrigatórios ou opcionais, as relações são estabelecidas automaticamente pelo sistema quando os recursos relevantes são criados ou devem ser criadas manualmente. No caso de criar relações manualmente, há dois métodos possíveis dependendo do recurso em questão:

* [Criar por carga](#payload)
* [Criar por URL](#url)  (somente para bibliotecas)

Consulte a seção [requisitos de relacionamento](#requirements) para obter uma lista dos relacionamentos compatíveis para cada tipo de recurso, e os métodos necessários para estabelecer esses relacionamentos, quando aplicável.

## Criar uma relação por carga {#payload}

Alguns relacionamentos devem ser estabelecidos manualmente quando você cria inicialmente um recurso. Para fazer isso, você deve fornecer um objeto `relationship` no payload da solicitação ao criar o recurso pai pela primeira vez. Exemplos desses relacionamentos incluem:

* [Criação de um elemento de dados ](../endpoints/data-elements.md#create) com as extensões necessárias
* [Criar um ](../endpoints/environments.md#create) ambiente com a relação de host necessária

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

A solicitação a seguir cria um novo `rule_component`, estabelecendo relações com `rules` e um `extension`.

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
| `relationships` | Um objeto que deve ser fornecido ao criar relações por carga. Cada chave nesse objeto representa um tipo de relacionamento específico. No exemplo acima, os relacionamentos `extension` e `rules` são estabelecidos, que são específicos de `rule_components`. Para obter mais informações sobre tipos de relacionamento compatíveis para recursos diferentes, consulte a seção sobre [requisitos de relacionamento por recurso](#relationship-requirements-by-resource). |
| `data` | Cada tipo de relacionamento fornecido no objeto `relationship` deve conter uma propriedade `data`, que faz referência a `id` e `type` do recurso com o qual uma relação está sendo estabelecida. Você pode criar uma relação com vários recursos do mesmo tipo formatando a propriedade `data` como uma matriz de objetos, com cada objeto contendo os `id` e `type` de um recurso aplicável. |
| `id` | A ID exclusiva de um recurso. Cada `id` deve ser acompanhado por uma propriedade irmão `type`, indicando o tipo de recurso em questão. |
| `type` | O tipo de recurso conforme referenciado por um campo `id` irmão. Os valores aceitos incluem `data_elements`, `rules`, `extensions` e `environments`. |

{style=&quot;table-layout:auto&quot;}

## Criar uma relação por URL {#url}

Ao contrário de outros recursos, as bibliotecas estabelecem relações por meio de seus próprios endpoints dedicados `/relationship`. São exemplos:

* [Adicionar extensões, elementos de dados e regras a uma biblioteca](../endpoints/libraries.md#add-resources)
* [Atribuição de uma biblioteca a um ambiente](../endpoints/libraries.md#environment)

**Formato da API**

```http
POST /properties/{PROPERTY_ID}/libraries/{LIBRARY_ID}/relationships/{RESOURCE_TYPE}
```

| Parâmetro | Descrição |
| --- | --- |
| `{PROPERTY_ID}` | A ID da propriedade à qual a biblioteca pertence. |
| `{LIBRARY_ID}` | A ID da biblioteca para a qual você deseja criar um relacionamento. |
| `{RESOURCE_TYPE}` | O tipo de recurso para o qual a relação está sendo direcionada. Os valores disponíveis incluem `environment`, `data_elements`, `extensions` e `rules`. |

**Solicitação**

A solicitação a seguir usa o endpoint `/relationships/environment` para uma biblioteca para criar uma relação com um ambiente.

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
| `data` | Um objeto que faz referência a `id` e `type` do recurso de destino para a relação. Se estiver criando uma relação com vários recursos do mesmo tipo (como `extensions` e `rules`), a propriedade `data` deverá ser formatada como uma matriz de objetos, com cada objeto contendo os `id` e `type` de um recurso aplicável. |
| `id` | A ID exclusiva de um recurso. Cada `id` deve ser acompanhado por uma propriedade irmão `type`, indicando o tipo de recurso em questão. |
| `type` | O tipo de recurso conforme referenciado por um campo `id` irmão. Os valores aceitos incluem `data_elements`, `rules`, `extensions` e `environments`. |

{style=&quot;table-layout:auto&quot;}

## Requisitos de relacionamento por recurso {#requirements}

As tabelas a seguir descrevem os relacionamentos disponíveis para cada tipo de recurso, sejam esses relacionamentos ou não necessários, e o método aceito para criar manualmente a relação, onde aplicável.

>[!NOTE]
>
>Se um relacionamento não estiver listado como sendo criado por carga ou URL, ele será automaticamente atribuído pelo sistema.

### Eventos de auditoria

| Relação | Obrigatório | Criar por carga | Criar por URL |
| :--- | :---: | :---: | :---: |
| `property` | Instantâneo |  |  |
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
