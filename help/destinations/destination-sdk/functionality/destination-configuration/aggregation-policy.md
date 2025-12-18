---
description: Saiba como configurar uma política de agregação para determinar como as solicitações HTTP para o seu destino devem ser agrupadas e armazenadas em lote.
title: Política de agregação
exl-id: 2dfa8815-2d69-4a22-8938-8ea41be8b9c5
source-git-commit: 92d7abcbd642cea4e0fa041d2926ba8868f506e5
workflow-type: tm+mt
source-wordcount: '1235'
ht-degree: 2%

---

# Política de agregação

Para garantir a máxima eficiência ao exportar dados para o endpoint da API, você pode usar várias configurações para agregar perfis exportados em lotes maiores ou menores, agrupá-los por identidade e outros casos de uso. Isso também permite personalizar as exportações de dados para qualquer limitação downstream no endpoint da API (limitação de taxa, número de identidades por chamada de API etc.).

Use a agregação configurável para se aprofundar nas configurações fornecidas pelo Destination SDK ou use a agregação de melhor esforço para instruir o Destination SDK a agrupar as chamadas de API da melhor maneira possível.

Ao criar um destino em tempo real (transmissão) com o Destination SDK, você pode configurar como os perfis exportados devem ser combinados nas exportações resultantes. Esse comportamento é determinado pelas configurações de política de agregação.

Para entender onde esse componente se encaixa em uma integração criada com o Destination SDK, consulte o diagrama na documentação de [opções de configuração](../configuration-options.md) ou consulte o guia sobre como [usar o Destination SDK para configurar um destino de streaming](../../guides/configure-destination-instructions.md#create-destination-configuration).

Você pode definir as configurações de política de agregação por meio do ponto de extremidade `/authoring/destinations`. Consulte as seguintes páginas de referência de API para obter exemplos detalhados de chamadas de API, onde é possível configurar os componentes mostrados nesta página.

* [Criar uma configuração de destino](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Atualizar uma configuração de destino](../../authoring-api/destination-configuration/update-destination-configuration.md)

Este artigo descreve todas as configurações de política de agregação compatíveis que você pode usar para o seu destino.

Depois de ler este documento, consulte a documentação sobre [uso do modelo](../../functionality/destination-server/message-format.md#using-templating) e os [exemplos de chave de agregação](../../functionality/destination-server/message-format.md#template-aggregation-key) para entender como incluir a política de agregação no seu modelo de transformação de mensagem com base na sua política de agregação selecionada.

>[!IMPORTANT]
>
>Todos os nomes e valores de parâmetros com suporte do Destination SDK diferenciam maiúsculas de minúsculas **1}.** Para evitar erros de diferenciação entre maiúsculas e minúsculas, use os nomes e valores dos parâmetros exatamente como mostrado na documentação.

## Tipos de integração compatíveis {#supported-integration-types}

Consulte a tabela abaixo para obter detalhes sobre quais tipos de integrações suportam a funcionalidade descrita nesta página.

| Tipo de integração | Suporte à funcionalidade |
|---|---|
| Integrações em tempo real (streaming) | Sim |
| Integrações baseadas em arquivo (lote) | Não |

## Agregação de melhor esforço {#best-effort-aggregation}

A melhor agregação de esforço funciona melhor para destinos que preferem menos perfis por solicitação e que prefeririam receber mais solicitações com menos dados do que menos solicitações com mais dados.

O exemplo de configuração abaixo mostra uma configuração de agregação de melhor esforço. Para obter um exemplo de agregação configurável, consulte a seção [agregação configurável](#configurable-aggregation). Os parâmetros aplicáveis à agregação do melhor esforço estão documentados no quadro abaixo.

```json
"aggregation":{
   "aggregationType":"BEST_EFFORT",
   "bestEffortAggregation":{
      "maxUsersPerRequest":10,
      "splitUserById":false,
      "aggregationKey":{
         "includeSegmentId":true,
         "includeSegmentStatus":true,
         "includeIdentity":true,
         "oneIdentityPerGroup":true,
         "groups":[
            {
               "namespaces":[
                  "IDFA",
                  "GAID"
               ]
            },
            {
               "namespaces":[
                  "EMAIL"
               ]
            }
         ]
      }
   }
}
```

| Parâmetro | Tipo | Descrição |
|---------|----------|------|
| `aggregationType` | String | Indica o tipo de política de agregação que seu destino deve usar. Tipos de agregação compatíveis: <ul><li>`BEST_EFFORT`</li><li>`CONFIGURABLE_AGGREGATION`</li></ul> |
| `bestEffortAggregation.maxUsersPerRequest` | Número inteiro | O Experience Platform pode agregar vários perfis exportados em uma única chamada HTTP. <br><br>Esse valor indica o número máximo de perfis que seu ponto de extremidade deve receber em uma única chamada HTTP. Observe que esta é uma agregação de melhor esforço. Por exemplo, se você especificar o valor 100, o Experience Platform pode enviar qualquer número de perfis menor que 100 em uma chamada. <br><br> Se o servidor não aceitar vários usuários por solicitação, defina esse valor como `1`. |
| `bestEffortAggregation.splitUserById` | Booleano | Use esse sinalizador se a chamada para o destino precisar ser dividida pela identidade. Defina esse sinalizador como `true` se o servidor aceitar apenas uma identidade por chamada para um determinado namespace de identidade. |
| `bestEffortAggregation.aggregationKey` | Objeto | *Opcional*. Permite agregar os perfis exportados mapeados para o destino com base nos parâmetros descritos abaixo. Esse parâmetro pode ser omitido ou definido como `null` se a agregação não for necessária. Quando fornecido, ele funciona de forma idêntica à chave de agregação na agregação configurável. |
| `bestEffortAggregation.aggregationKey.includeSegmentId` | Booleano | Defina esse parâmetro como `true` se desejar agrupar os perfis exportados para o seu destino pela ID de público-alvo. |
| `bestEffortAggregation.aggregationKey.includeSegmentStatus` | Booleano | Defina esse parâmetro e `includeSegmentId` como `true`, se desejar agrupar os perfis exportados para o seu destino pela ID do público-alvo e pelo status do público-alvo. |
| `bestEffortAggregation.aggregationKey.includeIdentity` | Booleano | Defina esse parâmetro como `true` se desejar agrupar perfis exportados para seu destino pelo namespace de identidade. |
| `bestEffortAggregation.aggregationKey.oneIdentityPerGroup` | Booleano | Defina esse parâmetro como `true` se desejar que os perfis exportados sejam agregados em grupos com base em uma única identidade (GAID, IDFA, números de telefone, email, etc.). Defina como `false` se você deseja usar o parâmetro `groups` para definir agrupamentos de namespace de identidade personalizados. |
| `bestEffortAggregation.aggregationKey.groups` | Matriz | Use este parâmetro quando `oneIdentityPerGroup` estiver definido como `false`. Crie listas de grupos de identidade se quiser agrupar perfis exportados para o seu destino por grupos de namespaces de identidade. Por exemplo, você pode combinar perfis que contêm os identificadores móveis IDFA e GAID em uma chamada para o seu destino e enviar emails para outra usando a configuração mostrada no exemplo acima. |

{style="table-layout:auto"}

>[!TIP]
>
>Use a agregação de esforço se o endpoint da API aceitar menos de 100 perfis por chamada de API.

## Agregação configurável {#configurable-aggregation}

A agregação configurável funciona melhor se você preferir receber grandes lotes, com milhares de perfis na mesma chamada. Essa opção também permite agregar os perfis exportados com base em regras de agregação complexas.

O exemplo de configuração abaixo mostra uma configuração de agregação configurável. Para obter um exemplo de agregação de melhor esforço, consulte a seção [agregação de melhor esforço](#best-effort-aggregation). Os parâmetros aplicáveis à agregação configurável estão documentados na tabela abaixo.

```json
"aggregation":{
   "aggregationType":"CONFIGURABLE_AGGREGATION",
   "configurableAggregation":{
      "splitUserById":true,
      "maxBatchAgeInSecs":2400,
      "maxNumEventsInBatch":5000,
      "aggregationKey":{
         "includeSegmentId":true,
         "includeSegmentStatus":true,
         "includeIdentity":true,
         "oneIdentityPerGroup":true,
         "groups":[
            {
               "namespaces":[
                  "IDFA",
                  "GAID"
               ]
            },
            {
               "namespaces":[
                  "EMAIL"
               ]
            }
         ]
      }
   }
}
```

| Parâmetro | Tipo | Descrição |
|---------|----------|------|
| `aggregationType` | String | Indica o tipo de política de agregação que seu destino deve usar. Tipos de agregação compatíveis: <ul><li>`BEST_EFFORT`</li><li>`CONFIGURABLE_AGGREGATION`</li></ul> |
| `configurableAggregation.splitUserById` | Booleano | Use esse sinalizador se a chamada para o destino precisar ser dividida pela identidade. Defina esse sinalizador como `true` se o servidor aceitar apenas uma identidade por chamada para um determinado namespace de identidade. |
| `configurableAggregation.maxBatchAgeInSecs` | Número inteiro | Usado em conjunto com `maxNumEventsInBatch`, esse parâmetro determina por quanto tempo o Experience Platform deve esperar até enviar uma chamada de API para o seu ponto de extremidade. <ul><li>Valor mínimo (segundos): 301</li><li>Valor máximo (segundos): 3.600</li></ul> Por exemplo, se você usar o valor máximo para ambos os parâmetros, o Experience Platform aguardará 3.600 segundos OU até que haja 10.000 perfis qualificados antes de fazer a chamada de API, o que acontecer primeiro. |
| `configurableAggregation.maxNumEventsInBatch` | Número inteiro | Usado em conjunto com `maxBatchAgeInSecs`, este parâmetro determina quantos perfis qualificados devem ser agregados em uma chamada de API. <ul><li>Valor mínimo: 1.000</li><li>Valor máximo: 10.000</li></ul> Por exemplo, se você usar o valor máximo para ambos os parâmetros, o Experience Platform aguardará 3.600 segundos OU até que haja 10.000 perfis qualificados antes de fazer a chamada de API, o que acontecer primeiro. |
| `configurableAggregation.aggregationKey` | - | Permite agregar os perfis exportados mapeados para o destino com base nos parâmetros descritos abaixo. |
| `configurableAggregation.aggregationKey.includeSegmentId` | Booleano | Defina esse parâmetro como `true` se desejar agrupar os perfis exportados para o seu destino pela ID de público-alvo. |
| `configurableAggregation.aggregationKey.includeSegmentStatus` | Booleano | Defina esse parâmetro e `includeSegmentId` como `true`, se desejar agrupar os perfis exportados para o seu destino pela ID do público-alvo e pelo status do público-alvo. |
| `configurableAggregation.aggregationKey.includeIdentity` | Booleano | Defina esse parâmetro como `true` se desejar agrupar perfis exportados para seu destino pelo namespace de identidade. |
| `configurableAggregation.aggregationKey.oneIdentityPerGroup` | Booleano | Defina esse parâmetro como `true` se desejar que os perfis exportados sejam agregados em grupos com base em uma única identidade (GAID, IDFA, números de telefone, email, etc.). Defina como `false` se você deseja usar o parâmetro `groups` para definir agrupamentos de namespace de identidade personalizados. |
| `configurableAggregation.aggregationKey.groups` | Matriz | Use este parâmetro quando `oneIdentityPerGroup` estiver definido como `false`. Crie listas de grupos de identidade se quiser agrupar perfis exportados para o seu destino por grupos de namespaces de identidade. Por exemplo, você pode combinar perfis que contêm os identificadores móveis IDFA e GAID em uma chamada para o seu destino e enviar emails para outra usando a configuração mostrada no exemplo acima. |

{style="table-layout:auto"}

## Próximas etapas {#next-steps}

Depois de ler este artigo, você deverá entender melhor como configurar as políticas de agregação para seu destino.

Para saber mais sobre os outros componentes de destino, consulte os seguintes artigos:

* [Configuração de autenticação do cliente](customer-authentication.md)
* [Autorização OAuth2](oauth2-authorization.md)
* [Campos de dados do cliente](customer-data-fields.md)
* [Atributos da interface](ui-attributes.md)
* [Configuração do esquema](schema-configuration.md)
* [Configuração do namespace de identidade](identity-namespace-configuration.md)
* [Configurações de mapeamento compatíveis](supported-mapping-configurations.md)
* [Entrega de destino](destination-delivery.md)
* [Configuração de metadados de público](audience-metadata-configuration.md)
* [Configuração em lote](batch-configuration.md)
* [Qualificações do perfil histórico](historical-profile-qualifications.md)
