---
title: Guia de solução de problemas para regras de vinculação do gráfico de identidade
description: Saiba como solucionar problemas comuns nas Regras de vinculação do gráfico de identidade.
exl-id: 98377387-93a8-4460-aaa6-1085d511cacc
source-git-commit: 10cdbef8281ec43a21af9fead80345f1c78b9d2c
workflow-type: tm+mt
source-wordcount: '3451'
ht-degree: 0%

---

# Guia de solução de problemas para [!DNL Identity Graph Linking Rules]

Ao testar e validar o [!DNL Identity Graph Linking Rules], você pode se deparar com alguns problemas relacionados à assimilação de dados e ao comportamento do gráfico. Leia este documento para saber como solucionar alguns problemas comuns que você pode encontrar ao trabalhar com o [!DNL Identity Graph Linking Rules].

## Visão geral do fluxo de assimilação de dados {#data-ingestion-flow-overview}

O diagrama a seguir é uma representação simplificada de como os dados fluem para o Adobe Experience Platform e os aplicativos. Use este diagrama como referência para ajudá-lo a entender melhor o conteúdo desta página.

![Um diagrama de como a assimilação de dados flui no Serviço de identidade.](../images/troubleshooting/dataflow_in_identity.png "Um diagrama de como a assimilação de dados flui no Serviço de identidade."){zoomable="yes"}

É importante observar os seguintes fatores:

* Para dados de transmissão, o Perfil do cliente em tempo real, o Serviço de identidade e o data lake iniciarão o processamento dos dados quando os dados forem enviados. No entanto, a latência para concluir o processamento dos dados depende do serviço. Normalmente, o data lake levará um tempo maior para processar, em comparação ao Perfil e à Identidade.
   * Se os dados não aparecerem ao executar um query em um conjunto de dados mesmo após algumas horas, é provável que os dados não tenham sido assimilados na Experience Platform.
* Para dados em lote, todos os dados fluirão para o data lake primeiro e, em seguida, os dados serão propagados para o Perfil e a Identidade se o conjunto de dados estiver habilitado para Perfil e Identidade.
* Para problemas relacionados à assimilação, é importante que o problema seja isolado em um nível de serviço para uma depuração e solução de problemas precisas. Há três tipos de problemas em potencial a serem considerados:

| Tipo de problema de assimilação | Os dados são assimilados no data lake? | Os dados são assimilados no Perfil? | Os dados são assimilados no Serviço de identidade? |
| --- | --- | --- | --- |
| Problema geral de assimilação | Não | Não | Não |
| Problema de gráfico | Sim | Sim | Não |
| Problema de fragmento de perfil | Sim | Não | Sim |

## Problemas de assimilação de dados {#data-ingestion-issues}

>[!NOTE]
>
>* Esta seção presume que os dados foram assimilados com êxito no data lake e que não houve sintaxe ou outros erros que impediriam que os dados fossem assimilados no Experience Platform em primeiro lugar.
>
>* Os exemplos usam a ECID como o namespace do cookie e a CRMID como o namespace da pessoa.

### Minhas identidades não estão sendo assimiladas no Serviço de identidade{#my-identities-are-not-getting-ingested-into-identity-service}

Há várias razões pelas quais isso pode acontecer, incluindo, mas não limitado ao seguinte:

* [O conjunto de dados não está habilitado para o Perfil](../../catalog/datasets/enable-for-profile.md).
* O registro é ignorado porque há apenas uma identidade no evento.
* [Falha de validação no Serviço de Identidade](../guardrails.md#identity-value-validation).
   * Por exemplo, uma ECID pode ter excedido o comprimento máximo de 38 caracteres.
* Por padrão, [as AAIDs estão bloqueadas para assimilação](../guardrails.md#identity-namespace-ingestion).
* A identidade foi removida devido a [medidas de proteção do sistema](../guardrails.md#understanding-the-deletion-logic-when-an-identity-graph-at-capacity-is-updated).

No contexto de [!DNL Identity Graph Linking Rules], um registro pode ser rejeitado do Serviço de Identidade porque o evento de entrada tem duas ou mais identidades com o mesmo namespace exclusivo, mas com valor de identidade diferente. Esse cenário geralmente ocorre devido a erros de implementação.

Considere o seguinte evento com duas suposições:

1. O nome de campo CRMID é marcado como uma identidade com o namespace CRMID.
2. O namespace CRMID é definido como um namespace exclusivo.

O evento a seguir retornará uma mensagem de erro indicando que a assimilação falhou.

<!-- because the ingestion of this erroneous event would have resulted in graph collapse. In the following event, two entities (Alice and Bob) are both associated with the same namespace (CRMID). -->

```json
{ 
  "_id": "random_string", 
  "eventType": "web browsing event", 
  "identityMap": { 
    "ECID": [ 
      { 
        "id": "11111111111111111111111111111111111111", 
        "primary": false 
      } 
    ], 
    "CRMID": [ 
      { 
        "id": "Alice", 
        "primary": true 
      } 
    ] 
  }, 
  "CRMID": "Bob", 
  "timestamp": "2024-08-17T15:22:51+00:00", 
  "web": { 
    "webPageDetails": { 
      "URL": "https://www.adobe.com/acrobat.html", 
      "name": "Adobe Acrobat" 
    } 
  } 
} 
```

**Etapas de solução de problemas**

Para resolver esse erro, primeiro você deve coletar as seguintes informações:

* O valor de identidade (`identity_value`) que você esperava assimilar no gráfico de identidade.
* O conjunto de dados (`dataset_name`) no qual o evento foi enviado.

Em seguida, use o [Serviço de consulta do Adobe Experience Platform](../../query-service/home.md) e execute a seguinte consulta:

>[!TIP]
>
>Substitua `dataset_name` e `identity_value` pelas informações coletadas.

```sql
  SELECT key, col.id as identityValue, timestamp, _id, identityMap, * 
  FROM (SELECT key, explode(value), * 
  FROM (SELECT explode(identityMap), * 
  FROM dataset_name)) WHERE col.id = 'identity_value' 
```

Após executar a consulta, localize o registro de evento que você esperava gerar um gráfico e, em seguida, valide se os valores de identidade são diferentes na mesma linha. Veja a imagem a seguir para ver um exemplo:

![Uma consulta sem título que resultou em namespaces duplicados.](../images/troubleshooting/duplicated_unique_namespace.png)

>[!NOTE]
>
>Se as duas identidades forem exatamente as mesmas e se o evento for assimilado por transmissão, a Identidade e o Perfil desduplicarão a identidade.

### ExperienceEvents pós-autenticação estão sendo atribuídos ao perfil autenticado incorreto

A prioridade de namespace desempenha um papel importante em como os fragmentos de evento determinam a identidade principal.

* Depois de definir e salvar suas [configurações de identidade](./identity-settings-ui.md) para uma determinada sandbox, o Perfil usará a [prioridade de namespace](namespace-priority.md#real-time-customer-profile-primary-identity-determination-for-experience-events) para determinar a identidade principal. No caso de identityMap, o perfil não usará mais o sinalizador `primary=true`.
* Embora o Perfil não se refira mais a esse sinalizador, outros serviços na Experience Platform podem continuar a usar o sinalizador `primary=true`.

Para que [eventos de usuário autenticados](implementation-guide.md#ingest-your-data) sejam vinculados ao namespace de pessoa, todos os eventos autenticados devem conter o namespace de pessoa (CRMID). Isso significa que mesmo depois que um usuário fizer logon, o namespace da pessoa ainda deverá estar presente em cada evento autenticado.

Você pode continuar a ver o sinalizador `primary=true` &#39;eventos&#39; ao pesquisar um perfil no visualizador de perfil. No entanto, isso é ignorado e não será usado pelo Perfil.

As AAIDs são bloqueadas por padrão. Portanto, se você estiver usando o [conector de origem do Adobe Analytics](../../sources/tutorials/ui/create/adobe-applications/analytics.md), certifique-se de que a ECID tenha uma prioridade maior do que a ECID, para que os eventos não autenticados tenham uma identidade principal de ECID.

**Etapas de solução de problemas**

1. Para validar se os eventos autenticados contêm a pessoa e o namespace do cookie, leia as etapas descritas na seção sobre [solução de problemas de erros relacionados à não assimilação de dados no Serviço de Identidade](#my-identities-are-not-getting-ingested-into-identity-service).
2. Para validar se os eventos autenticados têm a identidade principal do namespace de pessoa (por exemplo, CRMID), pesquise o namespace de pessoa no visualizador de perfil usando a política de mesclagem sem compilação (essa é a política de mesclagem que não usa gráfico privado). Esta pesquisa só retornará eventos associados ao namespace de pessoa.

### Meus fragmentos de evento de experiência não estão sendo assimilados no Perfil {#my-experience-event-fragments-are-not-getting-ingested-into-profile}

Há vários motivos que contribuem para que os fragmentos de evento de experiência não sejam assimilados no Perfil, incluindo, mas não limitados a:

* [O conjunto de dados não está habilitado para o Perfil](../../catalog/datasets/enable-for-profile.md).
* [Pode ter ocorrido uma falha de validação no Perfil](../../xdm/classes/experienceevent.md).
   * Por exemplo, um evento de experiência deve conter um `_id` e um `timestamp`.
   * Além disso, o `_id` deve ser exclusivo para cada evento (registro).

No contexto de prioridade de namespace, o Perfil rejeitará qualquer evento que contenha duas ou mais identidades com a maior prioridade de namespace no **determinado evento de entrada**. Por exemplo, suponha que suas configurações de identidade estejam definidas da seguinte maneira:

| Namespace | Único por gráfico | Prioridade |
| --- | --- | --- |
| CRMID | ✔️ | 1 |
| GAID | | 2 |
| ECID | | 3 |

Para cada cenário, suponha que Eventos de experiência contenham os seguintes eventos:

**Cenário 1: 2 GAIDs, 1 ECID**

* Nesse cenário, um Evento de experiência recebido contém 2 GAIDs e 1 ECID. Entre esses namespaces, o GAID é configurado como o namespace com a maior prioridade. No entanto, como há 2 GAIDs, o Perfil **não** armazena esse Evento de Experiência.

**Cenário 2: 2 CRMIDs, 1 GAID**

* Nesse cenário, um Evento de experiência de entrada contém dois CRMIDs e um GAID. Entre esses namespaces, o CRMID é configurado como o namespace com a maior prioridade de namespace. No entanto, como há 2 CRMIDs, o Perfil **não** armazena esse Evento de Experiência.

**Cenário 3: 1 CRMID, 2 GAIDs**

* Nesse cenário, um Evento de experiência de entrada contém 1 CRMID e 2 GAIDs. Entre esses namespaces, o CRMID é configurado como o namespace com a maior prioridade de namespace. Como há apenas um CRMID, o Perfil assimilará os Eventos de experiência porque há apenas uma identidade do namespace com a maior prioridade de namespace.

**Etapas de solução de problemas**

Se os dados forem enviados ao data lake, mas não ao Perfil, e você acreditar que isso se deve ao envio de duas ou mais identidades com a maior prioridade de namespace em um único evento, poderá executar a seguinte consulta para validar se há dois valores de identidade diferentes enviados para o mesmo namespace:

>[!TIP]
>
>Nas queries a seguir, você deve:
>
>* Substituir `_testimsorg.identification.core.email` pelo caminho que envia a identidade.
>* Substitua `Email` pelo namespace com a prioridade mais alta. Esse é o mesmo namespace que não está sendo assimilado.
>* Substitua `dataset_name` pelo conjunto de dados que você deseja consultar.

```sql
  SELECT identityMap, key, col.id as identityValue, _testimsorg.identification.core.email, _id, timestamp 
  FROM (SELECT key, explode(value), * 
  FROM (SELECT explode(identityMap), * 
  FROM dataset_name)) WHERE col.id != _testimsorg.identification.core.email and key = 'Email' 
```

Essa consulta pressupõe que:

* Uma identidade é enviada a partir do identityMap e outra identidade é enviada a partir de um descritor de identidade. **OBSERVAÇÃO**: em esquemas do Experience Data Model (XDM), o descritor de identidade é o campo marcado como uma identidade.
* O CRMID é enviado por identityMap. Se a CRMID for enviada como um campo, remova `key='Email'` da cláusula WHERE.

>[!NOTE]
>
>**Na implementação do SDK da Web e na duplicação da ECID**: se o campo da ECID estiver marcado como uma identidade (descritor de identidade) em vez do identityMap, uma segunda ECID será gerada no identityMap. Essa duplicação pode impedir que o Perfil do cliente em tempo real armazene eventos anônimos devido à presença de duas ECIDs em um único evento.

## Problemas relacionados ao comportamento do gráfico {#graph-behavior-related-issues}

Esta seção descreve problemas comuns que podem ser encontrados em relação ao comportamento do gráfico de identidade.

### ExperienceEvents não autenticados estão sendo anexados ao perfil autenticado incorreto

O Algoritmo de Otimização de Identidade respeitará [os links estabelecidos mais recentemente e removerá os links mais antigos](./identity-optimization-algorithm.md#identity-optimization-algorithm-details). Portanto, é possível que, uma vez habilitado esse recurso, as ECIDs possam ser reatribuídas (vinculadas novamente) de uma pessoa a outra. Para entender o histórico de como uma identidade é vinculada ao longo do tempo, siga as etapas abaixo:

**Etapas de solução de problemas**

>[!NOTE]
>
>As etapas a seguir recuperarão informações sob as seguintes premissas:
>
>* Um único conjunto de dados está em uso (isso não consultará vários conjuntos de dados).
>
>* Os dados não foram excluídos do data lake devido à exclusão por [Advanced Data Lifecycle Management](../../hygiene/home.md), [Privacy Service](../../privacy-service/home.md) ou outros serviços que realizam a exclusão.

Primeiro, você deve coletar as seguintes informações:

1. O símbolo de identidade (namespaceCode) do namespace de cookie (por exemplo, ECID) e o namespace de pessoa (por exemplo, CRMID) que foram enviados.
1.1. Para implementações do Web SDK, esses são geralmente os namespaces incluídos no identityMap.
1.2. Para implementações do conector de origem do Analytics, esses são os identificadores de cookies incluídos no identityMap. O identificador de pessoa é um campo do eVar marcado como uma identidade.
2. O conjunto de dados em que o evento foi enviado (dataset_name).
3. O valor de identidade do namespace do cookie a ser pesquisado (identity_value).

Os símbolos de identidade (namespaceCode) fazem distinção entre maiúsculas e minúsculas. Para recuperar todos os símbolos de identidade de um determinado conjunto de dados no identityMap, execute a seguinte consulta:

```sql
SELECT distinct explode(*)FROM (SELECT map_keys(identityMap) FROM dataset_name)
```

Se você não souber o valor de identidade do identificador de cookie e quiser procurar por uma ID de cookie que teria sido vinculada a vários identificadores de pessoa, será necessário executar a seguinte consulta. Essa consulta considera a ECID como o namespace do cookie e a CRMID como o namespace da pessoa.

>[!BEGINTABS]

>[!TAB Implementação do Web SDK]

```sql
  SELECT identityMap['ECID'][0]['id'], count(distinct identityMap['CRMID'][0]['id']) as crmidCount FROM dataset_name GROUP BY identityMap['ECID'][0]['id'] ORDER BY crmidCount desc 
```

>[!TAB Implementação do conector de origem do Analytics]

```sql
  SELECT identityMap['ECID'][0]['id'], count(distinct personID) as crmidCount FROM dataset_name group by identityMap['ECID'][0]['id'] ORDER BY crmidCount desc 
```

**Observação:** personID refere-se ao caminho do descritor. Você pode encontrar essas informações em schemas.

>[!ENDTABS]

Agora que você identificou os valores de cookie vinculados a várias IDs de pessoa, pegue um dos resultados e use-o na seguinte consulta para obter uma exibição cronológica de quando esse valor de cookie foi vinculado a um identificador de pessoa diferente:

>[!BEGINTABS]

>[!TAB Implementação do Web SDK]

```sql
  SELECT identityMap['CRMID'][0]['id'] as personEntity, * 
  FROM dataset_name 
  WHERE identitymap['ECID'][0].id ='identity_value' 
  ORDER BY timestamp desc 
```

>[!TAB Implementação do conector de origem do Analytics]

```sql
SELECT _experience.analytics.customDimensions.eVars.eVar10 as personEntity, * 
FROM dataset_name 
WHERE identitymap['ECID'][0].id ='identity_value' 
ORDER BY timestamp desc 
```

**Observação**: este exemplo pressupõe que `eVar10` está marcado como uma identidade. Para suas configurações, você deve alterar o eVar com base na implementação de sua própria organização.

>[!ENDTABS]

### O algoritmo de otimização de identidade não está &quot;funcionando&quot; como esperado

**Etapas de solução de problemas**

Consulte a documentação em [Algoritmo de Otimização de Identidade](./identity-optimization-algorithm.md), bem como os tipos de estruturas gráficas compatíveis.

* Leia o [guia de configuração de gráfico](./example-configurations.md) para ver exemplos de estruturas de gráfico com suporte.
* Você também pode ler o [guia de implementação](./implementation-guide.md#appendix) para ver exemplos de estruturas de gráfico não suportadas. Há dois cenários que podem acontecer:
   * Nenhum namespace único em todos os perfis.
   * Ocorre um cenário de [&quot;ID pendente&quot;](./implementation-guide.md#dangling-loginid-scenario). Nesse cenário, o Serviço de identidade não pode determinar se a ID pendente está associada a qualquer uma das entidades de pessoa nos gráficos.

Você também pode usar a [ferramenta de simulação de gráficos na interface](./graph-simulation.md) para simular eventos e definir suas próprias configurações de prioridade de namespace e namespace exclusivas. Isso pode ajudar a fornecer uma compreensão da linha de base de como o Algoritmo de otimização de identidade deve se comportar.

Se os resultados da simulação corresponderem às expectativas de comportamento do gráfico, você poderá verificar se as [configurações de identidade](./identity-settings-ui.md) correspondem às configurações definidas na simulação.

### Ainda vejo gráficos recolhidos em minha sandbox, mesmo após definir as configurações de identidade

Os gráficos de identidade seguirão seu namespace exclusivo e sua prioridade de namespace configurados _após_ salvar as configurações. Quaisquer gráficos &quot;recolhidos&quot; existentes _antes_ de salvar suas novas configurações não serão afetados, até que novos dados sejam assimilados de modo que o gráfico recolhido seja atualizado. A identidade principal dos fragmentos de evento no Perfil de cliente em tempo real não será atualizada mesmo após as alterações de prioridade do namespace.

**Etapas de solução de problemas**

Você pode usar o [visualizador de gráficos de identidade](../features/identity-graph-viewer.md) para verificar se o gráfico foi assimilado antes ou depois das configurações. Examine o carimbo de data/hora atualizado pela última vez em [!UICONTROL Propriedades do link] para ver quando o Serviço de Identidade assimilou o gráfico. Se o carimbo de data e hora for anterior à configuração, isso sugere que o gráfico &quot;recolhido&quot; foi criado antes da ativação do recurso.

![O visualizador de gráficos de identidade com um gráfico de exemplo.](../images/troubleshooting/graph_viewer.png)

### Quero saber quantos gráficos &quot;recolhidos&quot; existem em minha sandbox

Use o painel de identidade para obter insights sobre o estado do gráfico de identidade, como a contagem de identidades e gráficos. Consulte a métrica &quot;Contagem de gráficos com vários namespaces&quot; para obter uma contagem de gráficos que foram recolhidos, ou seja, gráficos que contêm duas ou mais identidades com o mesmo namespace. Supondo que a sandbox não tenha dados e você tenha configurado um namespace (por exemplo, CRMID) para ser exclusivo, a expectativa é que haja zero gráficos que tenham dois ou mais CRMIDs. No exemplo abaixo, há dois gráficos que contêm dois ou mais endereços de email.

![O painel de identidade com métricas sobre contagem de identidades, contagem de gráficos, contagem por namespace, contagem de gráficos por tamanho e contagem de gráficos de mais de dois namespaces.](../images/troubleshooting/identity_dashboard.png)

Você pode encontrar um detalhamento detalhado no [conjunto de dados de exportação de instantâneo de perfil](../../dashboards/query.md) no data lake executando a consulta abaixo:

>[!NOTE]
>
>* Substitua `dataset_name` pelo nome real do seu conjunto de dados.
>
>* As contagens podem não corresponder exatamente. O painel de identidade é baseado na contagem de gráficos de identidade e a consulta a seguir é baseada na contagem de perfis com duas ou mais identidades. Os dados são processados e atualizados de forma independente pelo serviço.

```sql
  SELECT key, identityCountInGraph, count(identityCountInGraph) as graphCount 
  FROM (SELECT key, cardinality(value) as identityCountInGraph 
  FROM (SELECT explode(identityMap) 
  FROM dataset_name 
  WHERE cardinality(identityMap) > 1)) /* by definition, graphs have 2 or more identities */ 
  WHERE key not in ('ecid', 'aaid', 'idfa', 'gaid') /* filter out common device/cookie namespaces */ 
  GROUP BY 1, 2 
  ORDER BY 1, 2 asc 
```

Você pode usar a seguinte consulta no conjunto de dados de exportação de instantâneo de perfil para obter identidades de amostra de gráficos &quot;recolhidos&quot;.

```sql
  SELECT identityMap 
  FROM dataset_name 
  WHERE cardinality(identityMap['CRMID'])>1 /* any graphs with 2+ CRMID. Change CRMID namespace if needed */ 
```

>[!TIP]
>
>As duas consultas listadas acima produzirão os resultados esperados se a sandbox não estiver habilitada para a abordagem temporária de dispositivo compartilhado e se comportará de forma diferente de [!DNL Identity Graph Linking Rules].

## Perguntas frequentes {#faq}

Esta seção descreve uma lista de respostas a perguntas frequentes sobre [!DNL Identity Graph Linking Rules].

## Algoritmo de otimização de identidades {#identity-optimization-algorithm}

Leia esta seção para obter respostas a perguntas frequentes sobre o [Algoritmo de Otimização de Identidade](./identity-optimization-algorithm.md).

### Tenho uma CRMID para cada uma das minhas unidades de negócios (CRMID B2C, CRMID B2B), mas não tenho um namespace exclusivo em todos os meus perfis. O que acontecerá se eu marcar a CRMID B2C e a CRMID B2B como exclusivas e ativar minhas configurações de identidade?

Este cenário não é compatível. Portanto, você pode ver gráficos recolhidos nos casos em que um usuário usa sua CRMID B2C para fazer logon e outro usuário usa sua CRMID B2B para fazer logon. Para obter mais informações, leia a seção sobre [requisito de namespace para uma única pessoa](./implementation-guide.md#single-person-namespace-requirement) na página de implementação.

### O algoritmo de otimização de identidade &quot;corrige&quot; os gráficos recolhidos existentes?

Os gráficos recolhidos existentes serão afetados (&quot;fixos&quot;) pelo algoritmo de gráfico somente se esses gráficos forem atualizados depois que você salvar as novas configurações.

### Se duas pessoas entrarem e saírem usando o mesmo dispositivo, o que acontece com os eventos? Todos os eventos serão transferidos para o último usuário autenticado?

* Eventos anônimos (eventos com ECID como identidade principal no Perfil do cliente em tempo real) serão transferidos para o último usuário autenticado. Isso ocorre porque a ECID será vinculada ao CRMID do último usuário autenticado (no Serviço de identidade).
* Todos os eventos autenticados (eventos com CRMID definido como identidade principal) permanecerão com a pessoa.

Para obter mais informações, leia o manual sobre [como determinar a identidade principal para eventos de experiência](../identity-graph-linking-rules/namespace-priority.md#real-time-customer-profile-primary-identity-determination-for-experience-events).

### Como as jornadas no Adobe Journey Optimizer serão afetadas quando a ECID for transferida de uma pessoa para outra?

A CRMID do último usuário autenticado será vinculada à ECID (dispositivo compartilhado). As ECIDs podem ser reatribuídas de uma pessoa para outra com base no comportamento do usuário. O impacto dependerá de como a jornada será construída, portanto, é importante que os clientes testem a jornada em um ambiente de sandbox de desenvolvimento para validar o comportamento.

Os principais pontos a serem destacados são os seguintes:

* Depois que um perfil entra em uma jornada, a reatribuição da ECID não resulta na saída do perfil no meio de uma jornada.
   * As saídas de jornada não são acionadas por alterações no gráfico.
* Se um perfil não estiver mais associado a uma ECID, isso poderá resultar na alteração do caminho da jornada se houver uma condição que use a qualificação de público-alvo.
   * A remoção da ECID pode alterar eventos associados a um perfil, o que pode resultar em alterações na qualificação do público-alvo.
* A reentrada de uma jornada depende das propriedades da jornada.
   * Se você desativar a reentrada de uma jornada, quando um perfil sair dessa jornada, o mesmo perfil não será reinserido por 91 dias (com base no tempo limite global da jornada).
* Se uma jornada começar com um namespace ECID, o perfil que entra e o perfil que recebe a ação (por exemplo, email, oferta) podem ser diferentes, dependendo de como a jornada foi projetada.
   * Por exemplo, se houver uma condição de espera entre as ações e as transferências da ECID durante o período de espera, um perfil diferente poderá ser direcionado.
   * Com esse recurso, a ECID nem sempre está associada a um perfil.
   * A recomendação é iniciar as jornadas com namespaces de pessoa (CRMID).

>[!TIP]
>
>O Jornada deve procurar um perfil com namespaces exclusivos porque um namespace não exclusivo pode ser reatribuído a outro usuário.
>
>* As ECIDs e os namespaces de email/telefone não exclusivos podem mudar de uma pessoa para outra.
>* Se uma jornada tiver uma condição de espera e se esses namespaces não exclusivos forem usados para pesquisar um perfil em uma jornada, a mensagem de jornada poderá ser enviada à pessoa incorreta.

## Prioridade de namespace

Leia esta seção para obter respostas a perguntas frequentes sobre [prioridade de namespace](./namespace-priority.md).

### Ativei minhas configurações de identidade. O que acontece com minhas configurações se eu quiser adicionar um namespace personalizado depois que as configurações forem ativadas?

Há dois &quot;buckets&quot; de namespaces: namespaces de pessoa e namespaces de dispositivo/cookie. O namespace personalizado recém-criado terá a prioridade mais baixa em cada &quot;bucket&quot; para que esse novo namespace personalizado não afete a assimilação de dados existente.

### Se o Perfil do cliente em tempo real não estiver mais usando o sinalizador &quot;principal&quot; no identityMap, esse valor ainda precisará ser enviado?

Sim, o sinalizador &quot;primário&quot; em identityMap é usado por outros serviços. Para obter mais informações, leia o manual sobre [as implicações da prioridade de namespace em outros serviços da Experience Platform](../identity-graph-linking-rules/namespace-priority.md#implications-on-other-experience-platform-services).

### A prioridade de namespace será aplicada aos conjuntos de dados de registro de Perfil no Perfil do cliente em tempo real?

Não. A prioridade de namespace será aplicada somente aos conjuntos de dados de Evento de experiência que usam a Classe XDM ExperienceEvent.

### Como esse recurso funciona em conjunto com as medidas de proteção de gráfico de identidade de 50 identidades por gráfico? A prioridade de namespace afeta esta garantia definida pelo sistema?

O algoritmo de otimização de identidade será aplicado primeiro para garantir a representação da entidade da pessoa. Posteriormente, se o gráfico tentar exceder a [proteção de gráfico de identidade](../guardrails.md) (50 identidades por gráfico), essa lógica será aplicada. A prioridade de namespace não afeta a lógica de exclusão da garantia de identidade/gráfico 50.

## Testes

Leia esta seção para obter respostas a perguntas frequentes sobre recursos de teste e depuração no [!DNL Identity Graph Linking Rules].

### Quais são alguns dos cenários que devo testar em um ambiente de sandbox de desenvolvimento?

De modo geral, testar uma sandbox de desenvolvimento deve imitar os casos de uso que você pretende executar em sua sandbox de produção. Consulte a tabela a seguir para obter algumas áreas principais a serem validadas ao realizar testes abrangentes:

| Caso de teste | Etapas de teste | Resultado esperado |
| --- | --- | --- |
| Representação de entidade de pessoa precisa | <ul><li>Imitar navegação anônima</li><li>Imitar duas pessoas (John, Jane) fazendo logon usando o mesmo dispositivo</li></ul> | <ul><li>John e Jane devem estar associados a seus atributos e eventos autenticados.</li><li>O último usuário autenticado deve ser associado aos eventos de navegação anônimos.</li></ul> |
| Segmentação | Criar quatro definições de segmento (**OBSERVAÇÃO**: cada par de definições de segmento deve ter uma avaliada usando lote e a outra transmissão.) <ul><li>Definição de segmento A: qualificação de segmento com base nos eventos e/ou atributos autenticados de John.</li><li>Definição de segmento B: qualificação de segmento com base nos eventos e/ou atributos autenticados da Jane.</li></ul> | Independentemente dos cenários de dispositivos compartilhados, John e Jane sempre devem se qualificar para seus respectivos segmentos. |
| Qualificação de público-alvo/jornadas unitárias no Adobe Journey Optimizer | <ul><li>Crie uma jornada começando com uma atividade de qualificação de público (como a segmentação por transmissão criada acima).</li><li>Crie uma jornada começando com um evento unitário. Esse evento unitário deve ser um evento autenticado.</li><li>Você deve desativar a reentrada ao criar essas jornadas.</li></ul> | <ul><li>Independentemente dos cenários de dispositivos compartilhados, John e Jane devem acionar as respectivas jornadas nas quais devem entrar.</li><li>John e Jane não devem entrar novamente na jornada quando a ECID for transferida de volta para eles.</li></ul> |

{style="table-layout:auto"}

### Como posso validar se esse recurso está funcionando como esperado?

Use a [ferramenta de simulação de gráficos](./graph-simulation.md) para validar se o recurso está funcionando em um nível de gráfico individual.

Para validar o recurso em um nível de sandbox, consulte a seção [!UICONTROL Contagem de gráficos com vários namespaces] no painel de identidade.