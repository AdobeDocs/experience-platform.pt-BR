---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Guia do desenvolvedor da API do Perfil do cliente em tempo real
topic: guide
translation-type: tm+mt
source-git-commit: d0ccaa5511375253a2eca8f1235c2f953b734709

---


# (Alfa) Atributos calculados

>[!IMPORTANT]
>A funcionalidade de atributo calculado descrita neste documento está atualmente em alfa e não está disponível para todos os usuários. A documentação e a funcionalidade estão sujeitas a alterações.

Os atributos calculados permitem calcular automaticamente o valor dos campos com base em outros valores, cálculos e expressões. Os atributos calculados operam no nível do perfil, o que significa que você pode agregação valores em todos os registros e eventos.

Cada atributo calculado contém uma expressão, ou &quot;regra&quot;, que avalia os dados recebidos e armazena o valor resultante em um atributo de perfil ou em um evento. Esses cálculos ajudam você a responder facilmente perguntas relacionadas a coisas como valor de compra vitalícia, tempo entre compras ou número de aberturas de aplicativos, sem exigir a execução manual de cálculos complexos sempre que as informações forem necessárias.

Este guia o ajudará a entender melhor os atributos calculados na Adobe Experience Platform e inclui exemplos de chamadas de API para executar operações CRUD básicas usando o `/config/computedAttributes` endpoint.

## Introdução

Os pontos de extremidade da API usados neste guia fazem parte da API do Perfil do cliente em tempo real. Antes de continuar, leia o guia [do desenvolvedor do Perfil do cliente em tempo](getting-started.md)real.

Em particular, a seção [de](getting-started.md) introdução do guia do desenvolvedor do Perfil inclui links para tópicos relacionados, um guia para ler as chamadas de API de amostra neste documento e informações importantes sobre os cabeçalhos necessários que são necessários para fazer chamadas com êxito para quaisquer APIs da plataforma de experiência.

## Noções básicas sobre atributos calculados

A plataforma Adobe Experience permite importar e mesclar facilmente dados de várias fontes para gerar Perfis de clientes em tempo real. Cada perfil contém informações importantes relacionadas a um indivíduo, como informações de contato, preferências e histórico de compras, fornecendo uma visualização de 360 graus do cliente.

Algumas das informações coletadas no perfil são facilmente compreendidas ao ler os campos de dados diretamente (por exemplo, &quot;primeiro nome&quot;), enquanto outros dados exigem a execução de vários cálculos ou a confiança em outros campos e valores para gerar as informações (por exemplo, &quot;total da compra vitalícia&quot;). Para facilitar a compreensão desses dados rapidamente, a Plataforma permite que você crie atributos **** calculados que executam automaticamente essas referências e cálculos, retornando o valor no campo apropriado.

Os atributos calculados incluem a criação de uma expressão, ou &quot;regra&quot;, que opera em dados recebidos e armazena o valor resultante em um atributo ou evento de perfil. As Expressões podem ser definidas de várias maneiras diferentes, permitindo especificar que uma regra avalie somente eventos recebidos, dados de evento e perfil recebidos ou evento recebido, dados de perfil e eventos históricos.

### Casos de uso

Casos de uso para atributos calculados podem variar de cálculos simples a referências muito complexas. Estes são alguns exemplos de casos de uso para atributos calculados:

1. **Porcentagens:** Um atributo calculado simples pode incluir a captura de dois campos numéricos em um registro e a divisão deles para criar uma porcentagem. Por exemplo, você pode pegar o número total de emails enviados para um indivíduo e dividi-lo pelo número de emails que o indivíduo abre. Olhar para o campo de atributo calculado resultante mostraria rapidamente a porcentagem do total de emails abertos pelo indivíduo.
1. **Uso do aplicativo:** Outro exemplo inclui a capacidade de agregação do número de vezes que um usuário abre seu aplicativo. Rastreando o número total de aberturas do aplicativo, com base em eventos individuais abertos, você pode fornecer ofertas ou mensagens especiais aos usuários em seus 100 anos abertos, encorajando um envolvimento mais profundo com a sua marca.
1. **Valores da duração:** A coleta de totais em execução, como um valor de compra vitalício para um cliente, pode ser muito difícil. Isso requer a atualização do total histórico sempre que ocorrer um novo evento de compra. Um atributo calculado permite que você faça isso com muito mais facilidade, mantendo o valor do tempo de vida em um único campo que é atualizado automaticamente após cada evento de compra bem-sucedido relacionado ao cliente.

## Configurar um atributo calculado

Para configurar um atributo calculado, primeiro é necessário identificar o campo que manterá o valor do atributo calculado. Esse campo pode ser criado usando uma combinação para adicionar o campo a um schema existente ou selecionando um campo que você já definiu dentro de um schema.

>[!NOTE]
>Atributos calculados não podem ser adicionados a campos em combinações definidas pela Adobe. O campo deve estar dentro da `tenant` namespace, o que significa que deve ser um campo definido e adicionado a um schema.

Para definir com êxito um campo de atributo calculado, o schema deve ser ativado para o Perfil e aparecer como parte do schema da união para a classe na qual o schema se baseia. Para obter mais informações sobre schemas e uniões habilitados para o Perfil, consulte a seção do guia do desenvolvedor do Registro do Schema sobre como [habilitar um schema para Perfil e exibir schemas](../../xdm/api/getting-started.md)de união. Também é recomendável revisar a [seção sobre união](../../xdm/schema/composition.md) na documentação básica da composição do schema.

O fluxo de trabalho neste tutorial usa um schema habilitado para Perfis e segue as etapas para definir uma nova combinação que contém o campo de atributo calculado e garante que seja a namespace correta. Se você já tiver um campo que esteja na namespace correta dentro de um schema habilitado para Perfis, poderá prosseguir diretamente para a etapa de [criação de um atributo](#create-a-computed-attribute)calculado.

### Visualização de um schema

As etapas a seguir usam a interface do usuário da plataforma Adobe Experience para localizar um schema, adicionar uma combinação e definir um campo. Se você preferir usar a API do Registro do Schema, consulte o guia [do desenvolvedor do Registro do](../../xdm/api/getting-started.md) Schema para obter as etapas sobre como criar uma combinação, adicionar uma mistura a um schema e habilitar um schema para uso com o Perfil do Cliente em tempo real.

Na interface do usuário, clique em **Schemas** no painel esquerdo e use a barra de pesquisa na guia *Procurar* para encontrar rapidamente o schema que deseja atualizar.

![](../images/computed-attributes/Schemas-Browse.png)

Depois de localizar o schema, clique no seu nome para abrir o Editor de Schemas, onde você pode fazer edições no schema.

![](../images/computed-attributes/Schema-Editor.png)

### Criar uma mistura

Para criar uma nova mistura, clique em **Adicionar** ao lado de *Misturas* na seção *Composição* no lado esquerdo do editor. Isso abre a caixa de diálogo **Adicionar mixagem** , onde você pode ver as misturas existentes. Clique no botão de opção para **Criar nova combinação** para definir sua nova combinação.

Dê um nome e uma descrição ao mixin e clique em **Adicionar mixin** quando concluído.

![](../images/computed-attributes/Add-mixin.png)

### Adicionar um campo de atributo calculado ao schema

A sua nova mistura deve aparecer agora na seção *Misturas* em *Composição*. Clique no nome do mixin e vários botões de campo **** Adicionar aparecerão na seção *Estrutura* do editor.

Selecione **Adicionar campo** ao lado do nome do schema para adicionar um campo de nível superior ou selecione para adicionar o campo em qualquer lugar no schema que você preferir.

Depois de clicar em **Adicionar campo** , um novo objeto é aberto, nomeado para sua ID de locatário, mostrando que o campo está na namespace correta. Dentro desse objeto, um campo *Novo* é exibido. Isso se o campo no qual você definirá o atributo calculado.

![](../images/computed-attributes/New-field.png)

### Configurar o campo

Usando a seção Propriedades *de* campo no lado direito do editor, forneça as informações necessárias para o novo campo, incluindo seu nome, nome de exibição e tipo.

>[!NOTE]
>O tipo do campo deve ser do mesmo tipo que o valor do atributo calculado. Por exemplo, se o valor do atributo calculado for uma string, o campo que está sendo definido no schema deverá ser uma string.

Quando terminar, clique em **Aplicar** e o nome do campo, bem como seu tipo, aparecerão na seção *Estrutura* do editor.

![](../images/computed-attributes/Apply.png)

### Ativar schema para Perfil

Antes de continuar, verifique se o schema foi ativado para o Perfil. Clique no nome do schema na seção *Estrutura* do editor para que a guia Propriedades *do* Schema seja exibida. Se o controle deslizante do **Perfil** estiver azul, o schema foi ativado para Perfil.

>[!NOTE]
>Não é possível desfazer a habilitação de um schema para Perfil. Portanto, se você clicar no controle deslizante depois que ele for habilitado, não será necessário arriscar desabilitá-lo.

![](../images/computed-attributes/Profile.png)

Agora você pode clicar em **Salvar** para salvar o schema atualizado e continuar com o restante do tutorial usando a API.

### Criar um atributo calculado {#create-a-computed-attribute}

Com o campo de atributo calculado identificado e a confirmação de que o schema está ativado para o Perfil, agora é possível configurar um atributo calculado.

Comece fazendo uma solicitação POST para o `/config/computedAttributes` ponto de extremidade com um corpo de solicitação contendo os detalhes do atributo calculado que você deseja criar.

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
| `path` | O caminho para o campo que contém o atributo calculado. Esse caminho é encontrado no `properties` atributo do schema e NÃO deve incluir o nome do campo no caminho. Ao gravar o caminho, omita os vários níveis de `properties` atributos. |
| `{TENANT_ID}` | Se você não estiver familiarizado com sua ID de locatário, consulte as etapas para localizar sua ID de locatário no guia [do desenvolvedor do Registro de](../../xdm/api/getting-started.md#know-your-tenant_id)Schemas. |
| `description` | Uma descrição do atributo calculado. Isso é especialmente útil depois que vários atributos calculados forem definidos, pois ajudará outras pessoas na organização IMS a determinar o atributo calculado correto a ser usado. |
| `expression.value` | Uma expressão válida de Linguagem de Query de Perfil (PQL). Para obter mais informações sobre o PQL e links para query suportados, leia a visão geral [do](../../segmentation/pql/overview.md)PQL. |
| `schema.name` | A classe na qual o schema que contém o campo de atributo calculado se baseia. Exemplo: `_xdm.context.experienceevent` para um schema com base na classe XDM ExperienceEvent. |

**Resposta**

Um atributo calculado criado com êxito retorna o Status HTTP 200 (OK) e um corpo de resposta contendo os detalhes do atributo calculado recém-criado. Esses detalhes incluem um sistema exclusivo, somente leitura, gerado `id` que pode ser usado para fazer referência ao atributo calculado durante outras operações da API.

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

| Propriedade | Descrição |
|---|---|
| `id` | Uma ID exclusiva, somente leitura, gerada pelo sistema, que pode ser usada para fazer referência ao atributo calculado durante outras operações da API. |
| `imsOrgId` | A Organização IMS relacionada ao atributo calculado deve corresponder ao valor enviado na solicitação. |
| `sandbox` | O objeto sandbox contém detalhes da caixa de proteção na qual o atributo calculado foi configurado. Essas informações são extraídas do cabeçalho da caixa de proteção enviado na solicitação. Para obter mais informações, consulte a visão geral [das](../../sandboxes/home.md)caixas de proteção. |
| `positionPath` | Uma matriz que contém o campo desconstruído `path` enviado na solicitação. |
| `returnSchema.meta:xdmType` | O tipo de campo no qual o atributo calculado será armazenado. |
| `definedOn` | Uma matriz que mostra os schemas de união nos quais o atributo calculado foi definido. Contém um objeto por schema de união, o que significa que pode haver vários objetos dentro da matriz se o atributo calculado tiver sido adicionado a vários schemas com base em classes diferentes. |
| `active` | Um valor booliano que exibe se o atributo calculado está ou não ativo no momento. Por padrão, o valor é `true`. |
| `type` | O tipo de recurso criado, neste caso &quot;ComputedAttribute&quot; é o valor padrão. |
| `createEpoch` e `updateEpoch` | A hora em que o atributo calculado foi criado e atualizado pela última vez, respectivamente. |


## Acessar atributos calculados

Ao trabalhar com atributos calculados usando a API, há duas opções para acessar atributos calculados que foram definidas pela organização. A primeira é lista de todos os atributos calculados, a segunda é visualização de um atributo calculado específico por seu único `id`.

As etapas para listar todos os atributos calculados e visualizar um atributo calculado específico são descritas nas seções a seguir.

### Lista de atributos calculados {#list-computed-attributes}

Sua Organização IMS pode criar vários atributos calculados e a execução de uma solicitação GET ao `/config/computedAttributes` endpoint permite que você lista todos os atributos calculados existentes para sua organização.

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

Uma resposta bem-sucedida inclui um `_page` atributo que fornece o número total de atributos calculados (`totalCount`) e o número de atributos calculados na página (`pageSize`).

A resposta também inclui uma `children` matriz composta de um ou mais objetos, cada um contendo os detalhes de um atributo calculado. Se sua organização não tiver atributos calculados, o `totalCount` e `pageSize` será 0 (zero) e a `children` matriz ficará vazia.

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
| `children` | Uma matriz composta de um ou mais objetos, cada um contendo os detalhes de um único atributo calculado. Se nenhum atributo calculado tiver sido definido, a `children` matriz ficará vazia. |
| `id` | Um valor exclusivo, somente leitura, gerado pelo sistema, atribuído automaticamente a um atributo calculado quando ele é criado. Para obter mais informações sobre os componentes de um objeto de atributo calculado, consulte a seção sobre como [criar um atributo](#create-a-computed-attribute) calculado anteriormente neste tutorial. |
| `_links.next` | Se uma única página de atributos calculados for retornada, `_links.next` será um objeto vazio, como mostra a resposta de amostra acima. Se sua organização tiver muitos atributos calculados, eles serão retornados em várias páginas que você pode acessar, fazendo uma solicitação GET para o `_links.next` valor. |

### Visualização de um atributo calculado {#view-a-computed-attribute}

Você também pode visualização um atributo calculado específico fazendo uma solicitação GET ao ponto de extremidade `/config/computedAttributes` e incluindo a ID do atributo computada no caminho da solicitação.

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

Se você achar que precisa atualizar um atributo calculado existente, isso pode ser feito realizando uma solicitação PATCH para o `/config/computedAttributes` endpoint e incluindo a ID do atributo calculado que você deseja atualizar no caminho da solicitação.

**Formato da API**

```http
PATCH /config/computedAttributes/{ATTRIBUTE_ID}
```

| Parâmetro | Descrição |
|---|---|
| `{ATTRIBUTE_ID}` | A ID do atributo calculado que você deseja atualizar. |

**Solicitação**

Esta solicitação usa a formatação [de Patch](http://jsonpatch.com/) JSON para atualizar o &quot;valor&quot; do campo &quot;expressão&quot;.

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
| `{NEW_EXPRESSION_VALUE}` | Uma expressão válida de Linguagem de Query de Perfil (PQL). Para obter mais informações sobre o PQL e links para query suportados, leia a visão geral [do](../../segmentation/pql/overview.md)PQL. |

**Resposta**

Uma atualização bem-sucedida retorna o Status HTTP 204 (Sem conteúdo) e um corpo de resposta vazio. Se desejar confirmar que a atualização foi bem-sucedida, você pode executar uma solicitação GET para visualização do atributo calculado pela ID.

## Excluir um atributo calculado

Também é possível excluir um atributo calculado usando a API. Isso é feito fazendo uma solicitação DELETE para o `/config/computedAttributes` ponto de extremidade e incluindo a ID do atributo calculado que você deseja excluir no caminho da solicitação.

>[!Note]
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

Uma solicitação de exclusão bem-sucedida retorna o Status HTTP 200 (OK) e um corpo de resposta vazio. Para confirmar se a exclusão foi bem-sucedida, é possível executar uma solicitação GET para pesquisar o atributo calculado pela ID. Se o atributo foi excluído, você receberá um erro HTTP Status 404 (Não encontrado).

## Próximas etapas

Agora que você aprendeu as noções básicas dos atributos calculados, você está pronto para começar a defini-los para sua organização.