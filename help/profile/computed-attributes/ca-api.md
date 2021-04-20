---
keywords: Experience Platform;perfil;perfil do cliente em tempo real;solução de problemas;API
title: Ponto Final da API de Atributos Calculados
topic: guide
type: Documentation
description: No Adobe Experience Platform, os atributos calculados são funções usadas para agregação de dados no nível do evento em atributos no nível do perfil. Essas funções são computadas automaticamente para que possam ser usadas em segmentação, ativação e personalização. Este guia mostra como criar, visualização, atualizar e excluir atributos calculados usando a API de Perfil do cliente em tempo real.
translation-type: tm+mt
source-git-commit: 4ed2b80ebfd87f8920462ae0a918b01bb13d4210
workflow-type: tm+mt
source-wordcount: '2279'
ht-degree: 2%

---


# (Alfa) Ponto final da API de atributos calculados

>[!IMPORTANT]
>
>A funcionalidade de atributo calculado descrita neste documento está atualmente em alfa e não está disponível para todos os usuários. A documentação e a funcionalidade estão sujeitas a alterações.

Atributos calculados são funções usadas para agregação de dados no nível do evento em atributos no nível do perfil. Essas funções são computadas automaticamente para que possam ser usadas em segmentação, ativação e personalização. Este guia inclui exemplos de chamadas de API para executar operações CRUD básicas usando o terminal `/computedAttributes`.

Para saber mais sobre os atributos calculados, comece lendo a [visão geral dos atributos calculados](overview.md).

## Introdução

O endpoint da API usado neste guia faz parte da [API do Perfil do cliente em tempo real](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml).

Antes de continuar, reveja o guia de introdução da API de documento [para obter links para a documentação recomendada, um guia para ler as chamadas de API de amostra que aparecem neste Perfil e informações importantes sobre os cabeçalhos necessários que são necessários para fazer chamadas com êxito para qualquer API de Experience Platform.](../api/getting-started.md)

## Configurar um campo de atributo calculado

Para criar um atributo calculado, primeiro é necessário identificar o campo em um schema que manterá o valor do atributo calculado.

Consulte a documentação em [configurar um atributo calculado](configure-api.md) para obter um guia completo sobre a criação de um campo de atributo calculado em um schema.

>[!WARNING]
>
>Para continuar com o guia da API, é necessário ter um campo de atributo calculado configurado.

## Criar um atributo calculado {#create-a-computed-attribute}

Com o campo de atributo calculado definido no schema ativado pelo Perfil, agora é possível configurar um atributo calculado. Se você ainda não tiver feito isso, siga o fluxo de trabalho descrito na documentação [configurar um atributo calculado](configure-api.md).

Para criar um atributo calculado, comece fazendo uma solicitação POST ao terminal `/config/computedAttributes` com um corpo de solicitação contendo os detalhes do atributo calculado que você deseja criar.

**Formato da API**

```http
POST /config/computedAttributes
```

**Solicitação**

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/computedAttributes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}'\
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name" : "birthdayCurrentMonth",
        "path" : "_{TENANT_ID}",
        "description" : "Computed attribute to capture if the customer birthday is in the current month.",
        "expression" : {
            "type" : "PQL", 
            "format" : "pql/text", 
            "value":  "person.birthDate.getMonth() = currentMonth()"
        },
        "schema": 
          {
            "name":"_xdm.context.profile"
          }
          
      }'
```

| Propriedade | Descrição |
|---|---|
| `name` | O nome do campo de atributo calculado, como uma string. |
| `path` | O caminho para o campo que contém o atributo calculado. Esse caminho é encontrado no atributo `properties` do schema e NÃO deve incluir o nome do campo no caminho. Ao gravar o caminho, omita os vários níveis dos atributos `properties`. |
| `{TENANT_ID}` | Se você não estiver familiarizado com sua ID de locatário, consulte as etapas para localizar sua ID de locatário no [guia do desenvolvedor do Registro de Schemas](../../xdm/api/getting-started.md#know-your-tenant_id). |
| `description` | Uma descrição do atributo calculado. Isso é especialmente útil depois que vários atributos calculados forem definidos, pois ajudará outras pessoas na organização IMS a determinar o atributo calculado correto a ser usado. |
| `expression.value` | Uma expressão válida [!DNL Profile Query Language] (PQL). Os atributos calculados suportam atualmente as seguintes funções: soma, contagem, mín, máx e booleano. Para obter uma lista de expressões de amostra, consulte a documentação [exemplo do PQL expressão](expressions.md). |
| `schema.name` | A classe na qual o schema que contém o campo de atributo calculado se baseia. Exemplo: `_xdm.context.experienceevent` para um schema com base na classe XDM ExperienceEvent. |

**Resposta**

Um atributo calculado criado com êxito retorna o Status HTTP 200 (OK) e um corpo de resposta contendo os detalhes do atributo calculado recém-criado. Esses detalhes incluem um `id` exclusivo, somente leitura, gerado pelo sistema, que pode ser usado para fazer referência ao atributo calculado durante outras operações da API.

```json
{
    "id": "2afcf410-450e-4a39-984d-2de99ab58877",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "{SANDBOX_ID}",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "birthdayCurrentMonth",
    "path": "_{TENANT_ID}",
    "positionPath": [
        "_{TENANT_ID}"
    ],
    "description": "Computed attribute to capture if the customer birthday is in the current month.",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "person.birthDate.getMonth() = currentMonth()"
    },
    "schema": {
        "name": "_xdm.context.profile"
    },
    "returnSchema": {
        "meta:xdmType": "string"
    },
    "definedOn": [
        {
            "meta:resourceType": "unions",
            "meta:containerId": "tenant",
            "$ref": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "encodedDefinedOn":"?\b?VR)JMS?R?())(????+?KL?OJ?K???H??O??+I?(?/(?O??I??/????S?8{?E:",
    "dependencies": [],
    "dependents": [],
    "active": true,
    "type": "ComputedAttribute",
    "createEpoch": 1572555223,
    "updateEpoch": 1572555225
}
```

| Propriedade | Descrição |
|---|---|
| `id` | Uma ID exclusiva, somente leitura, gerada pelo sistema, que pode ser usada para fazer referência ao atributo calculado durante outras operações da API. |
| `imsOrgId` | A Organização IMS relacionada ao atributo calculado deve corresponder ao valor enviado na solicitação. |
| `sandbox` | O objeto sandbox contém detalhes da caixa de proteção na qual o atributo calculado foi configurado. Essas informações são extraídas do cabeçalho da caixa de proteção enviado na solicitação. Para obter mais informações, consulte a [visão geral das caixas de proteção](../../sandboxes/home.md). |
| `positionPath` | Uma matriz contendo o `path` desconstruído para o campo que foi enviado na solicitação. |
| `returnSchema.meta:xdmType` | O tipo de campo no qual o atributo calculado será armazenado. |
| `definedOn` | Uma matriz que mostra os schemas de união nos quais o atributo calculado foi definido. Contém um objeto por schema de união, o que significa que pode haver vários objetos dentro da matriz se o atributo calculado tiver sido adicionado a vários schemas com base em classes diferentes. |
| `active` | Um valor booliano que exibe se o atributo calculado está ou não ativo no momento. Por padrão, o valor é `true`. |
| `type` | O tipo de recurso criado, neste caso &quot;ComputedAttribute&quot; é o valor padrão. |
| `createEpoch` e `updateEpoch` | A hora em que o atributo calculado foi criado e atualizado pela última vez, respectivamente. |

## Criar um atributo calculado que faz referência a atributos calculados existentes

Também é possível criar um atributo calculado que faz referência a atributos calculados existentes. Para fazer isso, comece fazendo uma solicitação POST para o terminal `/config/computedAttributes`. O corpo da solicitação conterá referências aos atributos calculados no campo `expression.value`, conforme mostrado no exemplo a seguir.

**Formato da API**

```http
POST /config/computedAttributes
```

**Solicitação**

Neste exemplo, dois atributos calculados já foram criados e serão usados para definir um terceiro. Os atributos calculados existentes são:

* **`totalSpend`:** Captura a quantia total em dólar que um cliente gastou.
* **`countPurchases`:** Conta o número de compras que um cliente fez.

A solicitação abaixo faz referência aos dois atributos calculados existentes, usando PQL válido para dividir para calcular o novo atributo calculado `averageSpend`.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/computedAttributes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}'\
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name" : "averageSpend",
        "path" : "_{TENANT_ID}.purchaseSummary",
        "description" : "Computed attribute to capture the average dollar amount that a customer spends on each purchase.",
        "expression" : {
            "type" : "PQL", 
            "format" : "pql/text", 
            "value":  "_{TENANT_ID}.purchaseSummary.totalSpend/_{TENANT_ID}.purchaseSummary.countPurchases"
        },
        "schema": 
          {
            "name":"_xdm.context.profile"
          }
          
      }'
```

| Propriedade | Descrição |
|---|---|
| `name` | O nome do campo de atributo calculado, como uma string. |
| `path` | O caminho para o campo que contém o atributo calculado. Esse caminho é encontrado no atributo `properties` do schema e NÃO deve incluir o nome do campo no caminho. Ao gravar o caminho, omita os vários níveis dos atributos `properties`. |
| `{TENANT_ID}` | Se você não estiver familiarizado com sua ID de locatário, consulte as etapas para localizar sua ID de locatário no [guia do desenvolvedor do Registro de Schemas](../../xdm/api/getting-started.md#know-your-tenant_id). |
| `description` | Uma descrição do atributo calculado. Isso é especialmente útil depois que vários atributos calculados forem definidos, pois ajudará outras pessoas na organização IMS a determinar o atributo calculado correto a ser usado. |
| `expression.value` | Uma expressão PQL válida. Os atributos calculados suportam atualmente as seguintes funções: soma, contagem, mín, máx e booleano. Para obter uma lista de expressões de amostra, consulte a documentação [exemplo do PQL expressão](expressions.md).<br/><br/>Neste exemplo, a expressão faz referência a dois atributos calculados existentes. Os atributos são referenciados usando `path` e `name` do atributo calculado, conforme aparecem no schema no qual os atributos calculados foram definidos. Por exemplo, `path` do primeiro atributo calculado referenciado é `_{TENANT_ID}.purchaseSummary` e `name` é `totalSpend`. |
| `schema.name` | A classe na qual o schema que contém o campo de atributo calculado se baseia. Exemplo: `_xdm.context.experienceevent` para um schema com base na classe XDM ExperienceEvent. |

**Resposta**

Um atributo calculado criado com êxito retorna o Status HTTP 200 (OK) e um corpo de resposta contendo os detalhes do atributo calculado recém-criado. Esses detalhes incluem um `id` exclusivo, somente leitura, gerado pelo sistema, que pode ser usado para fazer referência ao atributo calculado durante outras operações da API.

```json
{
    "id": "2afcf410-450e-4a39-984d-2de99ab58877",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "{SANDBOX_ID}",
        "sandboxName": "{SANDBOX_NAME}",
        "type": "production",
        "default": true
    },
    "name": "averageSpend",
    "path": "_{TENANT_ID}.purchaseSummary",
    "positionPath": [
        "_{TENANT_ID}",
        "purchaseSummary"
    ],
    "description": "Computed attribute to capture the average dollar amount that a customer spends on each purchase.",
    "expression" : {
            "type" : "PQL", 
            "format" : "pql/text", 
            "value":  "_{TENANT_ID}.purchaseSummary.totalSpend/_{TENANT_ID}.purchaseSummary.countPurchases"
    },
    "schema": {
        "name": "_xdm.context.profile"
    },
    "returnSchema": {
        "meta:xdmType": "number"
    },
    "definedOn": [
        {
          "meta:resourceType": "unions",
          "meta:containerId": "tenant",
          "$ref": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "encodedDefinedOn":"\bVR)JMSR())(+KLOJKկHO+I(/(OI/S8{E:",
    "dependencies": [
        "c08a92f3-2418-4a3d-89d0-96f15fda3e5d",
        "4ed9e3aa-57ae-4705-9e8a-7fba9a6a7010"
    ],
    "dependents": [],
    "active": true,
    "evaluationInfo": {
        "batch": {
          "enabled": false
        },
        "continuous": {
          "enabled": true
        },
        "synchronous": {
          "enabled": false
        }
      },
    "type": "ComputedAttribute",
    "createEpoch": 1613696592,
    "updateEpoch": 1613696593
}
```

| Propriedade | Descrição |
|---|---|
| `id` | Uma ID exclusiva, somente leitura, gerada pelo sistema, que pode ser usada para fazer referência ao atributo calculado durante outras operações da API. |
| `imsOrgId` | A Organização IMS relacionada ao atributo calculado deve corresponder ao valor enviado na solicitação. |
| `sandbox` | O objeto sandbox contém detalhes da caixa de proteção na qual o atributo calculado foi configurado. Essas informações são extraídas do cabeçalho da caixa de proteção enviado na solicitação. Para obter mais informações, consulte a [visão geral das caixas de proteção](../../sandboxes/home.md). |
| `positionPath` | Uma matriz contendo o `path` desconstruído para o campo que foi enviado na solicitação. |
| `returnSchema.meta:xdmType` | O tipo de campo no qual o atributo calculado será armazenado. |
| `definedOn` | Uma matriz que mostra os schemas de união nos quais o atributo calculado foi definido. Contém um objeto por schema de união, o que significa que pode haver vários objetos dentro da matriz se o atributo calculado tiver sido adicionado a vários schemas com base em classes diferentes. |
| `active` | Um valor booliano que exibe se o atributo calculado está ou não ativo no momento. Por padrão, o valor é `true`. |
| `type` | O tipo de recurso criado, neste caso &quot;ComputedAttribute&quot; é o valor padrão. |
| `createEpoch` e `updateEpoch` | A hora em que o atributo calculado foi criado e atualizado pela última vez, respectivamente. |

## Acessar atributos calculados

Ao trabalhar com atributos calculados usando a API, há duas opções para acessar atributos calculados que foram definidas pela organização. A primeira é lista de todos os atributos calculados, a segunda é visualização de um atributo calculado específico por seu `id` exclusivo.

As etapas para ambos os padrões de acesso são descritas neste documento. Selecione uma das seguintes opções para começar:

* **[Lista de todos os atributos](#list-all-computed-attributes) calculados existentes:** Retorna uma lista de todos os atributos calculados existentes que sua organização criou.
* **[Visualização de um atributo](#view-a-computed-attribute) calculado específico:** Retorna os detalhes de um único atributo calculado especificando sua ID durante a solicitação.

### Lista de todos os atributos calculados {#list-all-computed-attributes}

Sua Organização IMS pode criar vários atributos calculados e executar uma solicitação de GET para o terminal `/config/computedAttributes` permite que você lista todos os atributos calculados existentes para sua organização.

**Formato da API**

```http
GET /config/computedAttributes
```

**Solicitação**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/computedAttributes/ \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Resposta**

Uma resposta bem-sucedida inclui um atributo `_page` fornecendo o número total de atributos calculados (`totalCount`) e o número de atributos calculados na página (`pageSize`).

A resposta também inclui uma matriz `children` composta de um ou mais objetos, cada um contendo os detalhes de um atributo calculado. Se sua organização não tiver atributos calculados, as variáveis `totalCount` e `pageSize` serão 0 (zero) e a matriz `children` ficará vazia.

```json
{
    "_page": {
        "totalCount": 2,
        "pageSize": 2
    },
    "children": [
        {
            "id": "2afcf410-450e-4a39-984d-2de99ab58877",
            "imsOrgId": "{IMS_ORG}",
            "sandbox": {
                "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "name": "birthdayCurrentMonth",
            "path": "person._{TENANT_ID}",
            "positionPath": [
                "person",
                "_{TENANT_ID}"
            ],
            "description": "Computed attribute to capture if the customer birthday is in the current month.",
            "expression": {
                "type": "PQL",
                "format": "pql/text",
                "value": "person.birthDate.getMonth() = currentMonth()"
            },
            "schema": {
                "name": "_xdm.context.profile"
            },
            "returnSchema": {
                "meta:xdmType": "string"
            },
            "definedOn": [
                {
                    "meta:resourceType": "unions",
                    "meta:containerId": "tenant",
                    "$ref": "https://ns.adobe.com/xdm/context/profile__union"
                }
            ],
            "encodedDefinedOn":"?\b?VR)JMS?R?())(????+?KL?OJ?K???H??O??+I?(?/(?O??I??/????S?8{?E:",
            "dependencies": [],
            "dependents": [],
            "active": true,
            "type": "ComputedAttribute",
            "createEpoch": 1572555223,
            "updateEpoch": 1572555225
        },
        {
            "id": "ae0c6552-cf49-4725-8979-116366e8e8d3",
            "imsOrgId": "{IMS_ORG}",
            "sandbox": {
                "sandboxId": "",
                "sandboxName": "",
                "type": "production",
                "default": true
            },
            "name": "productDownloads",
            "path": "_{TENANT_ID}",
            "positionPath": [
                "_{TENANT_ID}"
            ],
            "description": "Calculate total product downloads.",
            "expression": {
                "type" : "PQL", 
                "format" : "pql/text", 
                "value":  "let Y = xEvent[_coresvc.event.subType = \"DOWNLOAD\"].groupBy(_coresvc.attributes[name = \"product\"].value).map({
                  \"downloaded\": this.head()._coresvc.attributes[name = \"product\"].head().value,
                  \"downloadsSum\": this.count(),
                  \"downloadsToday\": this[timestamp occurs today].count(),
                  \"downloadsPast30Days\": this[timestamp occurs < 30 days before now].count(),
                  \"downloadsPast60Days\": this[timestamp occurs < 60 days before now].count(),
                  \"downloadsPast90Days\": this[timestamp occurs < 90 days before now].count() }) in { \"uniqueProductDownloadSum\": Y.count(), \"products\": Y }"
            },
            "returnSchema": {
                "meta:xdmType": "string"
            },
            "definedOn": [
                {
                    "meta:resourceType": "unions",
                    "meta:containerId": "tenant",
                    "$ref": "https://ns.adobe.com/xdm/context/profile__union"
                }
            ],
            "schema": {
                "name": "_xdm.context.profile"
            },
            "encodedDefinedOn": "\u001f?\b\u0000\u0000\u0000\u0000\u0000\u0000\u0000?VR)JMS?R?())(????+?KL?OJ?K???H??O??+I?(?/(?O??I??/????S?\u0005\u00008{?E:\u0000\u0000\u0000",
            "dependencies": [],
            "dependents": [],
            "active": true,
            "type": "ComputedAttribute",
            "createEpoch": 1571945277,
            "updateEpoch": 1571945280
        }
    ],
    "_links": {
        "next": {}
    }
}
```

| Propriedade | Descrição |
|---|---|
| `_page.totalCount` | O número total de atributos calculados definidos pela Organização IMS. |
| `_page.pageSize` | O número de atributos calculados retornados nesta página de resultados. Se `pageSize` for igual a `totalCount`, isso significa que há apenas uma página de resultados e todos os atributos calculados foram retornados. Se não forem iguais, há páginas adicionais de resultados que podem ser acessadas. Consulte `_links.next` para obter detalhes. |
| `children` | Uma matriz composta de um ou mais objetos, cada um contendo os detalhes de um único atributo calculado. Se nenhum atributo calculado tiver sido definido, a matriz `children` estará vazia. |
| `id` | Um valor exclusivo, somente leitura, gerado pelo sistema, atribuído automaticamente a um atributo calculado quando ele é criado. Para obter mais informações sobre os componentes de um objeto de atributo calculado, consulte a seção em [criar um atributo calculado](#create-a-computed-attribute) anteriormente neste tutorial. |
| `_links.next` | Se uma única página de atributos calculados for retornada, `_links.next` será um objeto vazio, como mostra a resposta de amostra acima. Se sua organização tiver muitos atributos calculados, eles serão retornados em várias páginas que você pode acessar, fazendo uma solicitação de GET para o valor `_links.next`. |

### Visualização de um atributo calculado {#view-a-computed-attribute}

Você pode visualização um atributo calculado específico fazendo uma solicitação de GET ao ponto de extremidade `/config/computedAttributes` e incluindo a ID de atributo calculada no caminho da solicitação.

**Formato da API**

```http
GET /config/computedAttributes/{ATTRIBUTE_ID}
```

| Parâmetro | Descrição |
|---|---|
| `{ATTRIBUTE_ID}` | A ID do atributo calculado que você deseja visualização. |

**Solicitação**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/computedAttributes/2afcf410-450e-4a39-984d-2de99ab58877 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Resposta**

```json
{
    "id": "2afcf410-450e-4a39-984d-2de99ab58877",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "name": "birthdayCurrentMonth",
    "path": "_{TENANT_ID}",
    "positionPath": [
        "_{TENANT_ID}"
    ],
    "description": "Computed attribute to capture if the customer birthday is in the current month.",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "person.birthDate.getMonth() = currentMonth()"
    },
    "schema": {
        "name": "_xdm.context.profile"
    },
    "returnSchema": {
        "meta:xdmType": "string"
    },
    "definedOn": [
        {
            "meta:resourceType": "unions",
            "meta:containerId": "tenant",
            "$ref": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "encodedDefinedOn":"?\b?VR)JMS?R?())(????+?KL?OJ?K???H??O??+I?(?/(?O??I??/????S?8{?E:",
    "dependencies": [],
    "dependents": [],
    "active": true,
    "type": "ComputedAttribute",
    "createEpoch": 1572555223,
    "updateEpoch": 1572555225
}
```

## Atualizar um atributo calculado

Se você achar que precisa atualizar um atributo calculado existente, isso pode ser feito fazendo uma solicitação PATCH ao terminal `/config/computedAttributes` e incluindo a ID do atributo calculado que você deseja atualizar no caminho da solicitação.

**Formato da API**

```http
PATCH /config/computedAttributes/{ATTRIBUTE_ID}
```

| Parâmetro | Descrição |
|---|---|
| `{ATTRIBUTE_ID}` | A ID do atributo calculado que você deseja atualizar. |

**Solicitação**

Esta solicitação usa [formatação de Patch JSON](http://jsonpatch.com/) para atualizar o &quot;valor&quot; do campo &quot;expressão&quot;.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/core/ups/config/computedAttributes/ae0c6552-cf49-4725-8979-116366e8e8d3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'\
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \  
  -d '[
        {
          "op": "add",
          "path": "/expression",
          "value": 
          {
            "type" : "PQL", 
            "format" : "pql/text", 
            "value":  "{NEW_EXPRESSION_VALUE}"
          }
        }
      ]'
```

| Propriedade | Descrição |
|---|---|
| `{NEW_EXPRESSION_VALUE}` | Uma expressão válida [!DNL Profile Query Language] (PQL). Os atributos calculados suportam atualmente as seguintes funções: soma, contagem, mín, máx e booleano. Para obter uma lista de expressões de amostra, consulte a documentação [exemplo do PQL expressão](expressions.md). |

**Resposta**

Uma atualização bem-sucedida retorna o Status HTTP 204 (Sem conteúdo) e um corpo de resposta vazio. Se você quiser confirmar que a atualização foi bem-sucedida, poderá executar uma solicitação de GET para visualização do atributo calculado pela ID.

## Excluir um atributo calculado

Também é possível excluir um atributo calculado usando a API. Isso é feito fazendo uma solicitação DELETE ao ponto de extremidade `/config/computedAttributes` e incluindo a ID do atributo calculado que você deseja excluir no caminho da solicitação.

>[!NOTE]
>
>Tenha cuidado ao excluir um atributo calculado, pois ele pode estar em uso em mais de um schema e a operação DELETE não pode ser desfeita.

**Formato da API**

```http
DELETE /config/computedAttributes/{ATTRIBUTE_ID}
```

| Parâmetro | Descrição |
|---|---|
| `{ATTRIBUTE_ID}` | A ID do atributo calculado que você deseja excluir. |

**Solicitação**

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/ups/config/computedAttributes/ae0c6552-cf49-4725-8979-116366e8e8d3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
  -H 'x-sandbox-name: {SANDBOX_NAME}' \ 
```

**Resposta**

Uma solicitação de exclusão bem-sucedida retorna o Status HTTP 200 (OK) e um corpo de resposta vazio. Para confirmar se a exclusão foi bem-sucedida, é possível executar uma solicitação de GET para pesquisar o atributo calculado pela ID. Se o atributo foi excluído, você receberá um erro HTTP Status 404 (Não encontrado).

## Criar uma definição de segmento que faça referência a um atributo calculado

A Adobe Experience Platform permite criar segmentos que definem um grupo de atributos ou comportamentos específicos a partir de um grupo de perfis. Uma definição de segmento inclui uma expressão que encapsula um query gravado no PQL. Essas expressões também podem fazer referência aos atributos calculados.

O exemplo a seguir cria uma definição de segmento que faz referência a um atributo calculado existente. Para saber mais sobre as definições de segmentos e como trabalhar com elas na API do Serviço de Segmentação, consulte o [guia do endpoint da API de definições de segmentos](../../segmentation/api/segment-definitions.md).

Para começar, faça uma solicitação POST ao terminal `/segment/definitions`, fornecendo o atributo calculado no corpo da solicitação.

**Formato da API**

```http
POST /segment/definitions
```

**Solicitação**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/definitions
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '{
        "name": "downloadedInLast7Days",
        "description": "Has product been downloaded in last 7 days?",
        "schema": {
            "name": "_xdm.context.profile"
        },
        "ttlInDays": 30,
        "expression": {
            "type": "PQL",
            "format": "pql/text",
            "value": "_{TENANT_ID}.downloadsLast7Days > 0",
            "meta": "m"
        },
        "dataGovernancePolicy": {
            "excludeOptOut": true
        }
    }'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `name` | Um nome exclusivo para o segmento, como uma string. |
| `description` | Uma descrição legível da definição. |
| `schema.name` | O schema associado às entidades no segmento. Consiste em um campo `id` ou `name`. |
| `expression` | Um objeto que contém campos com informações sobre a definição do segmento. |
| `expression.type` | Especifica o tipo de expressão. Atualmente, apenas &quot;PQL&quot; é suportado. |
| `expression.format` | Indica a estrutura da expressão no valor. Atualmente, apenas `pql/text` é suportado. |
| `expression.value` | Uma expressão PQL válida, neste exemplo, inclui uma referência para um atributo calculado existente. |

Para obter mais informações sobre atributos de definição de schema, consulte os exemplos fornecidos no guia de ponto final da API [definições de segmento](../../segmentation/api/segment-definitions.md).

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com detalhes da definição do segmento recém-criado. Para saber mais sobre os objetos de resposta de definição de segmento, consulte [guia de ponto final da API de definições de segmento](../../segmentation/api/segment-definitions.md).

```json
{
    "id": "add3933f-ac5c-4240-8259-3a4528ee4885",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 60,
    "id": "119835c3-5fab-4c18-ae01-4ccab328fc5c",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "{SANDBOX_ID}",
        "sandboxName": "{SANDBOX_NAME}",
        "type": "production",
        "default": true
    },
    "name": "segment-downloadedInLast7Days",
    "description": "Has product been downloaded in last 7 days?",
    "expression": {
        "type": "PQL",
        "format": "pql/text",
        "value": "_{TENANT_ID}.downloadsLast7Days > 0",
        "meta": "m"
    },
    "evaluationInfo": {
        "batch": {
            "enabled": false
        },
        "continuous": {
            "enabled": true
        },
        "synchronous": {
            "enabled": false
        }
    },
    "dataGovernancePolicy": {
        "excludeOptOut": true
    },
    "creationTime": 1602016581000,
    "updateEpoch": 1610609459,
    "updateTime": 1610609459000,
    "createEpoch": 1602016554,
    "_etag": "\"8b01611a-0000-0200-0000-5ffff3330000\"",
    "dependents": [
        "023d46c9-a27c-4ea9-a887-2c91ba83f2d1"
    ],
    "definedOn": [
        {
            "meta:resourceType": "unions",
            "meta:containerId": "tenant",
            "$ref": "https://ns.adobe.com/xdm/context/profile__union"
        }
    ],
    "dependencies": [
    "103d46c9-a27c-4ea9-a887-2c91ba83f2d1"
    ],
    "type": "SegmentDefinition"
}
```

## Próximas etapas

Agora que você aprendeu as noções básicas dos atributos calculados, você está pronto para começar a defini-los para sua organização.