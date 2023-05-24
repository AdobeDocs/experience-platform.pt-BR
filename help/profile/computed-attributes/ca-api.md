---
keywords: Experience Platform;perfil;perfil de cliente em tempo real;solução de problemas;API
title: Endpoint da API de atributos computados
type: Documentation
description: No Adobe Experience Platform, os atributos computados são funções usadas para agregar dados no nível do evento em atributos no nível do perfil. Essas funções são computadas automaticamente para que possam ser usadas na segmentação, ativação e personalização. Este guia mostra como criar, exibir, atualizar e excluir atributos calculados usando a API de perfil do cliente em tempo real.
exl-id: 6b35ff63-590b-4ef5-ab39-c36c39ab1d58
hide: true
hidefromtoc: true
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '2274'
ht-degree: 3%

---

# (Alfa) Endpoint da API de atributos computados

>[!IMPORTANT]
>
>A funcionalidade de atributo calculado descrita neste documento está atualmente em alfa e não está disponível para todos os usuários. A documentação e a funcionalidade estão sujeitas a alterações.

Os atributos computados são funções usadas para agregar dados no nível do evento em atributos no nível do perfil. Essas funções são computadas automaticamente para que possam ser usadas na segmentação, ativação e personalização. Este guia inclui exemplos de chamadas de API para executar operações básicas de CRUD usando o `/computedAttributes` terminal.

Para saber mais sobre atributos computados, comece lendo o [visão geral dos atributos computados](overview.md).

## Introdução

O endpoint da API usado neste guia faz parte da [API do Perfil do cliente em tempo real](https://www.adobe.com/go/profile-apis-en).

Antes de continuar, reveja o [Guia de introdução à API de perfil](../api/getting-started.md) para obter links para a documentação recomendada, um guia para ler as chamadas de API de amostra que aparecem neste documento e informações importantes sobre os cabeçalhos necessários para fazer chamadas com êxito para qualquer API de Experience Platform.

## Configurar um campo de atributo calculado

Para criar um atributo calculado, primeiro é necessário identificar o campo em um esquema que conterá o valor do atributo calculado.

Consulte a documentação em [configuração de um atributo calculado](configure-api.md) para obter um guia completo sobre como criar um campo de atributo calculado em um esquema.

>[!WARNING]
>
>Para continuar com o guia de API, você deve ter um campo de atributo calculado configurado.

## Criar um atributo calculado {#create-a-computed-attribute}

Com o campo de atributo calculado definido no esquema ativado por perfil, agora é possível configurar um atributo calculado. Se ainda não tiver feito isso, siga o fluxo de trabalho descrito na seção [configuração de um atributo calculado](configure-api.md) documentação.

Para criar um atributo calculado, comece fazendo uma solicitação POST ao `/config/computedAttributes` ponto de extremidade com um corpo de solicitação que contém os detalhes do atributo calculado que você deseja criar.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "birthdayCurrentMonth",
        "path": "_{TENANT_ID}",
        "description": "Computed attribute to capture if the customer birthday is in the current month.",
        "expression": {
            "type": "PQL", 
            "format": "pql/text", 
            "value": "person.birthDate.getMonth() = currentMonth()"
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
| `path` | O caminho para o campo que contém o atributo calculado. Esse caminho é encontrado dentro do `properties` atributo do esquema e NÃO deve incluir o nome do campo no caminho. Ao gravar o caminho, omita os vários níveis de `properties` atributos. |
| `{TENANT_ID}` | Se você não estiver familiarizado com sua ID de locatário, consulte as etapas para encontrar sua ID de locatário no [Guia do desenvolvedor do Registro de esquema](../../xdm/api/getting-started.md#know-your-tenant_id). |
| `description` | Uma descrição do atributo calculado. Isso é especialmente útil depois que vários atributos computados são definidos, pois ajudará outras pessoas em sua organização a determinar o atributo calculado correto a ser usado. |
| `expression.value` | Um válido [!DNL Profile Query Language] (PQL). Atualmente, os atributos computados são compatíveis com as seguintes funções: sum, count, min, max e booleano. Para obter uma lista de expressões de amostra, consulte [exemplos de expressões PQL](expressions.md) documentação. |
| `schema.name` | A classe em que se baseia o esquema que contém o campo de atributo calculado. Exemplo: `_xdm.context.experienceevent` para um esquema com base na classe XDM ExperienceEvent. |

**Resposta**

Um atributo calculado criado com êxito retorna o Status HTTP 200 (OK) e um corpo de resposta que contém os detalhes do atributo calculado recém-criado. Esses detalhes incluem um arquivo exclusivo, somente leitura, gerado pelo sistema `id` que pode ser usado para fazer referência ao atributo calculado durante outras operações de API.

```json
{
    "id": "2afcf410-450e-4a39-984d-2de99ab58877",
    "imsOrgId": "{ORG_ID}",
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
| `id` | Uma ID exclusiva, somente leitura, gerada pelo sistema que pode ser usada para fazer referência ao atributo calculado durante outras operações da API. |
| `imsOrgId` | A Organização IMS relacionada ao atributo calculado deve corresponder ao valor enviado na solicitação. |
| `sandbox` | O objeto de sandbox contém detalhes da sandbox na qual o atributo calculado foi configurado. Essas informações são retiradas do cabeçalho da sandbox enviado na solicitação. Para obter mais informações, consulte [visão geral das sandboxes](../../sandboxes/home.md). |
| `positionPath` | Uma matriz que contém a variável desconstruída `path` para o campo que foi enviado na solicitação. |
| `returnSchema.meta:xdmType` | O tipo de campo onde o atributo calculado será armazenado. |
| `definedOn` | Uma matriz que mostra os esquemas de união nos quais o atributo calculado foi definido. Contém um objeto por esquema de união, o que significa que pode haver vários objetos na matriz se o atributo calculado tiver sido adicionado a vários esquemas com base em classes diferentes. |
| `active` | Um valor booleano que exibe se o atributo calculado está ou não ativo no momento. Por padrão, o valor é `true`. |
| `type` | O tipo de recurso criado, neste caso &quot;ComputedAttribute&quot; é o valor padrão. |
| `createEpoch` e `updateEpoch` | A hora em que o atributo calculado foi criado e atualizado pela última vez, respectivamente. |

## Criar um atributo calculado que faça referência aos atributos calculados existentes

Também é possível criar um atributo calculado que faça referência aos atributos calculados existentes. Para fazer isso, comece fazendo uma solicitação POST ao `/config/computedAttributes` terminal. O corpo da solicitação conterá referências aos atributos computados na `expression.value` conforme mostrado no exemplo a seguir.

**Formato da API**

```http
POST /config/computedAttributes
```

**Solicitação**

Neste exemplo, dois atributos computados já foram criados e serão usados para definir um terceiro. Os atributos computados existentes são:

* **`totalSpend`:** Registra o valor total em dólares gasto por um cliente.
* **`countPurchases`:** Conta o número de compras feitas por um cliente.

A solicitação abaixo faz referência aos dois atributos calculados existentes, usando um PQL válido para dividir a fim de calcular os novos `averageSpend` atributo calculado.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/computedAttributes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}'\
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "averageSpend",
        "path": "_{TENANT_ID}.purchaseSummary",
        "description": "Computed attribute to capture the average dollar amount that a customer spends on each purchase.",
        "expression": {
            "type": "PQL", 
            "format": "pql/text", 
            "value": "_{TENANT_ID}.purchaseSummary.totalSpend/_{TENANT_ID}.purchaseSummary.countPurchases"
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
| `path` | O caminho para o campo que contém o atributo calculado. Esse caminho é encontrado dentro do `properties` atributo do esquema e NÃO deve incluir o nome do campo no caminho. Ao gravar o caminho, omita os vários níveis de `properties` atributos. |
| `{TENANT_ID}` | Se você não estiver familiarizado com sua ID de locatário, consulte as etapas para encontrar sua ID de locatário no [Guia do desenvolvedor do Registro de esquema](../../xdm/api/getting-started.md#know-your-tenant_id). |
| `description` | Uma descrição do atributo calculado. Isso é especialmente útil depois que vários atributos calculados são definidos, pois ajudará outros em sua Organização IMS a determinar o atributo calculado correto a ser usado. |
| `expression.value` | Uma expressão PQL válida. Atualmente, os atributos computados são compatíveis com as seguintes funções: sum, count, min, max e booleano. Para obter uma lista de expressões de amostra, consulte [exemplos de expressões PQL](expressions.md) documentação.<br/><br/>Neste exemplo, a expressão faz referência a dois atributos computados existentes. Os atributos são referenciados usando a variável `path` e a variável `name` do atributo calculado conforme aparecem no esquema em que os atributos calculados foram definidos. Por exemplo, a variável `path` do primeiro atributo calculado referenciado é `_{TENANT_ID}.purchaseSummary` e a variável `name` é `totalSpend`. |
| `schema.name` | A classe em que se baseia o esquema que contém o campo de atributo calculado. Exemplo: `_xdm.context.experienceevent` para um esquema com base na classe XDM ExperienceEvent. |

**Resposta**

Um atributo calculado criado com êxito retorna o Status HTTP 200 (OK) e um corpo de resposta que contém os detalhes do atributo calculado recém-criado. Esses detalhes incluem um arquivo exclusivo, somente leitura, gerado pelo sistema `id` que pode ser usado para fazer referência ao atributo calculado durante outras operações de API.

```json
{
    "id": "2afcf410-450e-4a39-984d-2de99ab58877",
    "imsOrgId": "{ORG_ID}",
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
    "expression": {
            "type": "PQL", 
            "format": "pql/text", 
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
| `id` | Uma ID exclusiva, somente leitura, gerada pelo sistema que pode ser usada para fazer referência ao atributo calculado durante outras operações da API. |
| `imsOrgId` | A Organização IMS relacionada ao atributo calculado deve corresponder ao valor enviado na solicitação. |
| `sandbox` | O objeto de sandbox contém detalhes da sandbox na qual o atributo calculado foi configurado. Essas informações são retiradas do cabeçalho da sandbox enviado na solicitação. Para obter mais informações, consulte [visão geral das sandboxes](../../sandboxes/home.md). |
| `positionPath` | Uma matriz que contém a variável desconstruída `path` para o campo que foi enviado na solicitação. |
| `returnSchema.meta:xdmType` | O tipo de campo onde o atributo calculado será armazenado. |
| `definedOn` | Uma matriz que mostra os esquemas de união nos quais o atributo calculado foi definido. Contém um objeto por esquema de união, o que significa que pode haver vários objetos na matriz se o atributo calculado tiver sido adicionado a vários esquemas com base em classes diferentes. |
| `active` | Um valor booleano que exibe se o atributo calculado está ou não ativo no momento. Por padrão, o valor é `true`. |
| `type` | O tipo de recurso criado, neste caso &quot;ComputedAttribute&quot; é o valor padrão. |
| `createEpoch` e `updateEpoch` | A hora em que o atributo calculado foi criado e atualizado pela última vez, respectivamente. |

## Acessar atributos calculados

Ao trabalhar com atributos computados usando a API, há duas opções para acessar atributos computados que foram definidas por sua organização. A primeira é listar todos os atributos computados, a segunda é visualizar um atributo computado específico pelo seu único `id`.

As etapas para ambos os padrões de acesso são descritas neste documento. Selecione uma das seguintes opções para começar:

* **[Listar todos os atributos computados existentes](#list-all-computed-attributes):** Retorne uma lista de todos os atributos computados existentes que sua organização criou.
* **[Exibir um atributo calculado específico](#view-a-computed-attribute):** Retorne os detalhes de um único atributo calculado especificando sua ID durante a solicitação.

### Listar todos os atributos computados {#list-all-computed-attributes}

Sua Organização IMS pode criar vários atributos computados e executar uma solicitação GET para o `/config/computedAttributes` O endpoint permite listar todos os atributos computados existentes para sua organização.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Resposta**

Uma resposta bem-sucedida inclui uma `_page` atributo que fornece o número total de atributos computados (`totalCount`) e o número de atributos computados na página (`pageSize`).

A resposta também inclui uma `children` matriz composta por um ou mais objetos, cada um contendo os detalhes de um atributo calculado. Se sua organização não tiver atributos calculados, a variável `totalCount` e `pageSize` será 0 (zero) e a variável `children` A matriz estará vazia.

```json
{
    "_page": {
        "totalCount": 2,
        "pageSize": 2
    },
    "children": [
        {
            "id": "2afcf410-450e-4a39-984d-2de99ab58877",
            "imsOrgId": "{ORG_ID}",
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
            "imsOrgId": "{ORG_ID}",
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
                "type": "PQL", 
                "format": "pql/text", 
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
| `_page.totalCount` | O número total de atributos computados definidos por sua Organização IMS. |
| `_page.pageSize` | O número de atributos computados retornados nesta página de resultados. Se `pageSize` é igual a `totalCount`, isso significa que há apenas uma página de resultados e todos os atributos calculados foram retornados. Se não forem iguais, há páginas adicionais de resultados que podem ser acessadas. Consulte `_links.next` para obter detalhes. |
| `children` | Uma matriz composta por um ou mais objetos, cada um contendo os detalhes de um único atributo calculado. Se nenhum atributo calculado tiver sido definido, a variável `children` matriz está vazia. |
| `id` | Um valor exclusivo, somente leitura, gerado pelo sistema, atribuído automaticamente a um atributo calculado quando ele é criado. Para obter mais informações sobre os componentes de um objeto de atributo calculado, consulte a seção sobre [criação de um atributo calculado](#create-a-computed-attribute) anteriormente neste tutorial. |
| `_links.next` | Se uma única página de atributos computados for retornada, `_links.next` é um objeto vazio, como mostrado na resposta de amostra acima. Se sua organização tiver muitos atributos calculados, eles serão retornados em várias páginas que você pode acessar fazendo uma solicitação GET para o `_links.next` valor. |

### Exibir um atributo calculado {#view-a-computed-attribute}

Você pode visualizar um atributo calculado específico fazendo uma solicitação GET para o `/config/computedAttributes` e incluindo a ID de atributo calculada no caminho da solicitação.

**Formato da API**

```http
GET /config/computedAttributes/{ATTRIBUTE_ID}
```

| Parâmetro | Descrição |
|---|---|
| `{ATTRIBUTE_ID}` | A ID do atributo calculado que você deseja exibir. |

**Solicitação**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/computedAttributes/2afcf410-450e-4a39-984d-2de99ab58877 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Resposta**

```json
{
    "id": "2afcf410-450e-4a39-984d-2de99ab58877",
    "imsOrgId": "{ORG_ID}",
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

Caso você precise atualizar um atributo calculado existente, isso pode ser feito fazendo uma solicitação PATCH para o `/config/computedAttributes` e incluindo a ID do atributo calculado que você deseja atualizar no caminho da solicitação.

**Formato da API**

```http
PATCH /config/computedAttributes/{ATTRIBUTE_ID}
```

| Parâmetro | Descrição |
|---|---|
| `{ATTRIBUTE_ID}` | A ID do atributo calculado que você deseja atualizar. |

**Solicitação**

Esta solicitação usa [Formatação de patch de JSON](https://datatracker.ietf.org/doc/html/rfc6902) para atualizar o &quot;value&quot; do campo &quot;expression&quot;.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/core/ups/config/computedAttributes/ae0c6552-cf49-4725-8979-116366e8e8d3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}'\
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \  
  -d '[
        {
          "op": "add",
          "path": "/expression",
          "value": 
          {
            "type": "PQL", 
            "format": "pql/text", 
            "value":  "{NEW_EXPRESSION_VALUE}"
          }
        }
      ]'
```

| Propriedade | Descrição |
|---|---|
| `{NEW_EXPRESSION_VALUE}` | Um válido [!DNL Profile Query Language] (PQL). Atualmente, os atributos computados são compatíveis com as seguintes funções: sum, count, min, max e booleano. Para obter uma lista de expressões de amostra, consulte [exemplos de expressões PQL](expressions.md) documentação. |

**Resposta**

Uma atualização bem-sucedida retorna o Status HTTP 204 (Sem conteúdo) e um corpo de resposta vazio. Se desejar confirmar que a atualização foi bem-sucedida, você pode executar uma solicitação do GET para exibir o atributo calculado por sua ID.

## Excluir um atributo calculado

Também é possível excluir um atributo calculado usando a API. Isso é feito fazendo uma solicitação DELETE para o `/config/computedAttributes` e incluindo a ID do atributo calculado que você deseja excluir no caminho da solicitação.

>[!NOTE]
>
>Tenha cuidado ao excluir um atributo calculado, pois ele pode estar em uso em mais de um esquema e a operação DELETE não pode ser desfeita.

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
  -H 'x-gw-ims-org-id: {ORG_ID}'
  -H 'x-sandbox-name: {SANDBOX_NAME}' \ 
```

**Resposta**

Uma solicitação de exclusão bem-sucedida retorna o Status HTTP 200 (OK) e um corpo de resposta vazio. Para confirmar que a exclusão foi bem-sucedida, você pode executar uma solicitação GET para pesquisar o atributo calculado pela respectiva ID. Se o atributo foi excluído, você receberá um erro de Status HTTP 404 (Não encontrado).

## Criar uma definição de segmento que faça referência a um atributo calculado

O Adobe Experience Platform permite criar segmentos que definem um grupo de atributos ou comportamentos específicos a partir de um grupo de perfis. Uma definição de segmento inclui uma expressão que encapsula uma consulta gravada em PQL. Essas expressões também podem fazer referência a atributos computados.

O exemplo a seguir cria uma definição de segmento que faz referência a um atributo calculado existente. Para saber mais sobre as definições de segmento e como trabalhar com elas na API do Serviço de segmentação, consulte [manual de endpoint da API de definições de segmento](../../segmentation/api/segment-definitions.md).

Para começar, faça uma solicitação POST para o `/segment/definitions` endpoint, fornecendo o atributo calculado no corpo da solicitação.

**Formato da API**

```http
POST /segment/definitions
```

**Solicitação**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/definitions
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
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
        }
    }'
```

| Propriedade | Descrição |
| -------- | ----------- |
| `name` | Um nome exclusivo para o segmento, como uma string. |
| `description` | Uma descrição legível da definição. |
| `schema.name` | O schema associado às entidades no segmento. Consiste em um `id` ou `name` campo. |
| `expression` | Um objeto que contém campos com informações sobre a definição do segmento. |
| `expression.type` | Especifica o tipo de expressão. No momento, somente o &quot;PQL&quot; é compatível. |
| `expression.format` | Indica a estrutura da expressão no valor. Atualmente, somente `pql/text` é compatível. |
| `expression.value` | Uma expressão PQL válida; neste exemplo, ela inclui uma referência a um atributo calculado existente. |

Para obter mais informações sobre atributos de definição de esquema, consulte os exemplos fornecidos na [manual de endpoint da API de definições de segmento](../../segmentation/api/segment-definitions.md).

**Resposta**

Uma resposta bem-sucedida retorna o status HTTP 200 com detalhes da definição de segmento recém-criada. Para saber mais sobre objetos de resposta de definição de segmento, consulte a [manual de endpoint da API de definições de segmento](../../segmentation/api/segment-definitions.md).

```json
{
    "id": "add3933f-ac5c-4240-8259-3a4528ee4885",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 60,
    "id": "119835c3-5fab-4c18-ae01-4ccab328fc5c",
    "imsOrgId": "{ORG_ID}",
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

Agora que você aprendeu as noções básicas sobre atributos computados, você está pronto para começar a defini-los para sua organização.
