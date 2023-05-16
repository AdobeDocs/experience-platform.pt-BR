---
description: Saiba como configurar uma política de agregação para determinar como as solicitações HTTP para seu destino devem ser agrupadas e armazenadas em lote.
title: Política de agregação
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '996'
ht-degree: 2%

---


# Política de agregação

Para garantir a eficiência máxima ao exportar dados para o endpoint da API, você pode usar várias configurações para agregar perfis exportados em lotes maiores ou menores, agrupá-los por identidade e outros casos de uso. Isso também permite adaptar as exportações de dados a quaisquer limitações de downstream no terminal da API (limitação de taxa, número de identidades por chamada de API etc.).

Use a agregação configurável para aprofundar as configurações fornecidas pelo Destination SDK ou use a melhor agregação de esforço para informar ao Destination SDK para agrupar as chamadas de API da melhor maneira possível.

Ao criar um destino em tempo real (streaming) com o Destination SDK, você pode configurar como os perfis exportados devem ser combinados nas exportações resultantes. Esse comportamento é determinado pelas configurações de política de agregação.

Para entender onde esse componente se encaixa em uma integração criada com o Destination SDK, consulte o diagrama no [opções de configuração](../configuration-options.md) ou consulte o guia sobre como [use o Destination SDK para configurar um destino de transmissão](../../guides/configure-destination-instructions.md#create-destination-configuration).

É possível definir as configurações da política de agregação por meio do `/authoring/destinations` endpoint . Consulte as páginas de referência da API a seguir para obter exemplos detalhados de chamadas de API, onde é possível configurar os componentes mostrados nesta página.

* [Criar uma configuração de destino](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Atualizar uma configuração de destino](../../authoring-api/destination-configuration/update-destination-configuration.md)

Este artigo descreve todas as configurações de política de agregação compatíveis que você pode usar para o seu destino.

Após ler esse documento, consulte a documentação em [uso de modelos](../../functionality/destination-server/message-format.md#using-templating) e [exemplos de chaves de agregação](../../functionality/destination-server/message-format.md#template-aggregation-key) para entender como incluir a política de agregação em seu template de transformação de mensagem com base em sua política de agregação selecionada.

>[!IMPORTANT]
>
>Todos os nomes de parâmetros e valores suportados pelo Destination SDK são **distinção entre maiúsculas e minúsculas**. Para evitar erros de diferenciação entre maiúsculas e minúsculas, use os nomes e valores dos parâmetros exatamente como mostrado na documentação.

## Tipos de integração compatíveis {#supported-integration-types}

Consulte a tabela abaixo para obter detalhes sobre quais tipos de integrações oferecem suporte à funcionalidade descrita nesta página.

| Tipo de integração | Oferece suporte à funcionalidade |
|---|---|
| Integrações em tempo real (streaming) | Sim |
| Integrações baseadas em arquivo (em lote) | Não |

## Melhor agregação de esforço {#best-effort-aggregation}

A melhor agregação de esforço funciona melhor para destinos que preferem menos perfis por solicitação e preferem aceitar mais solicitações com menos dados do que menos solicitações com mais dados.

A configuração de exemplo abaixo mostra uma configuração de agregação de esforço melhor. Para obter um exemplo de agregação configurável, consulte o [agregação configurável](#configurable-aggregation) seção. Os parâmetros aplicáveis à melhor agregação de esforço são documentados no quadro abaixo.

```json
"aggregation":{
   "aggregationType":"BEST_EFFORT",
   "bestEffortAggregation":{
      "maxUsersPerRequest":10,
      "splitUserById":false
   }
}
```

| Parâmetro | Tipo | Descrição |
|---------|----------|------|
| `aggregationType` | String | Indica o tipo de política de agregação que seu destino deve usar. Tipos de agregação compatíveis: <ul><li>`BEST_EFFORT`</li><li>`CONFIGURABLE_AGGREGATION`</li></ul> |
| `bestEffortAggregation.maxUsersPerRequest` | Número inteiro | O Experience Platform pode agregar vários perfis exportados em uma única chamada HTTP. <br><br>Esse valor indica o número máximo de perfis que seu terminal deve receber em uma única chamada HTTP. Observe que esta é a melhor agregação de esforço. Por exemplo, se você especificar o valor 100, a Platform poderá enviar qualquer número de perfis menor que 100 em uma chamada. <br><br> Se o servidor não aceitar vários usuários por solicitação, defina esse valor como `1`. |
| `bestEffortAggregation.splitUserById` | Booleano | Use esse sinalizador se a chamada para o destino deve ser dividida por identidade. Defina este sinalizador como `true` se o servidor aceitar apenas uma identidade por chamada, para um determinado namespace de identidade. |

{style="table-layout:auto"}

>[!TIP]
>
>Use a melhor agregação de esforço se o terminal da API aceitar menos de 100 perfis por chamada de API.

## Agregação configurável {#configurable-aggregation}

A agregação configurável funciona melhor se você preferir aceitar grandes lotes, com milhares de perfis na mesma chamada. Essa opção também permite agregar os perfis exportados com base em regras de agregação complexas.

A configuração de exemplo abaixo mostra uma configuração de agregação configurável. Para obter um exemplo de agregação de melhor esforço, consulte o [melhor agregação de esforço](#best-effort-aggregation) seção. Os parâmetros aplicáveis à agregação configurável são documentados na tabela abaixo.

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
| `configurableAggregation.splitUserById` | Booleano | Use esse sinalizador se a chamada para o destino deve ser dividida por identidade. Defina este sinalizador como `true` se o servidor aceitar apenas uma identidade por chamada, para um determinado namespace de identidade. |
| `configurableAggregation.maxBatchAgeInSecs` | Número inteiro | Usado em conjunto com `maxNumEventsInBatch`, esse parâmetro determina por quanto tempo o Experience Platform deve aguardar até enviar uma chamada de API para o terminal. <ul><li>Valor mínimo (segundos): 1800</li><li>Valor máximo (segundos): 3600</li></ul> Por exemplo, se você usar o valor máximo para ambos os parâmetros, o Experience Platform aguardará 3600 segundos OU até que haja 10000 perfis qualificados antes de fazer a chamada da API, o que ocorrer primeiro. |
| `configurableAggregation.maxNumEventsInBatch` | Número inteiro | Usado em conjunto com `maxBatchAgeInSecs`, esse parâmetro determina quantos perfis qualificados devem ser agregados em uma chamada de API. <ul><li>Valor mínimo: 1000</li><li>Valor máximo: 10000</li></ul> Por exemplo, se você usar o valor máximo para ambos os parâmetros, o Experience Platform aguardará 3600 segundos OU até que haja 10000 perfis qualificados antes de fazer a chamada da API, o que ocorrer primeiro. |
| `configurableAggregation.aggregationKey` | - | Permite agregar os perfis exportados mapeados para o destino com base nos parâmetros descritos abaixo. |
| `configurableAggregation.aggregationKey.includeSegmentId` | Booleano | Defina este parâmetro como `true` se desejar agrupar perfis exportados para seu destino por ID de segmento. |
| `configurableAggregation.aggregationKey.includeSegmentStatus` | Booleano | Defina este parâmetro e `includeSegmentId` para `true`, se desejar agrupar perfis exportados para seu destino por ID de segmento e status de segmento. |
| `configurableAggregation.aggregationKey.includeIdentity` | Booleano | Defina este parâmetro como `true` se quiser agrupar perfis exportados para seu destino pelo namespace de identidade. |
| `configurableAggregation.aggregationKey.oneIdentityPerGroup` | Booleano | Defina este parâmetro como `true` se desejar que os perfis exportados sejam agregados em grupos com base em uma única identidade (GAID, IDFA, números de telefone, email, etc.). |
| `configurableAggregation.aggregationKey.groups` | Matriz | Crie listas de grupos de identidade se quiser agrupar perfis exportados para seu destino por grupos de namespaces de identidade. Por exemplo, você pode combinar perfis que contêm os identificadores móveis IDFA e GAID em uma chamada para seu destino e emails em outra usando a configuração mostrada no exemplo acima. |

{style="table-layout:auto"}

## Próximas etapas {#next-steps}

Após ler este artigo, você deve ter uma melhor compreensão de como pode configurar políticas de agregação para seu destino.

Para saber mais sobre os outros componentes de destino, consulte os seguintes artigos:

* [Configuração de autenticação do cliente](customer-authentication.md)
* [Autenticação OAuth2](oauth2-authentication.md)
* [Campos de dados do cliente](customer-data-fields.md)
* [Atributos da interface do usuário](ui-attributes.md)
* [Configuração do esquema](schema-configuration.md)
* [Configuração do namespace de identidade](identity-namespace-configuration.md)
* [Configurações de mapeamento suportadas](supported-mapping-configurations.md)
* [Delivery de destino](destination-delivery.md)
* [Configuração de metadados de público-alvo](audience-metadata-configuration.md)
* [Configuração em lote](batch-configuration.md)
* [Qualificações de perfil histórico](historical-profile-qualifications.md)