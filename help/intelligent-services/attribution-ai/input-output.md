---
keywords: Experience Platform, introdução, Attribution ai, tópicos populares, Attribution ai input, Attribution ai output,
feature: Attribution AI
title: Entrada e saída no Attribution AI
topic-legacy: Input and Output data for Attribution AI
description: O documento a seguir descreve as diferentes entradas e saídas utilizadas no Attribution AI.
exl-id: d6dbc9ee-0c1a-4a5f-b922-88c7a36a5380
source-git-commit: 9ce5a383bed24c4bfe9245521149443a57764da5
workflow-type: tm+mt
source-wordcount: '2450'
ht-degree: 3%

---

# Entrada e saída em [!DNL Attribution AI]

O documento a seguir descreve as diferentes entradas e saídas utilizadas em [!DNL Attribution AI].

## [!DNL Attribution AI] dados de entrada

O Attribution AI funciona analisando os seguintes conjuntos de dados para calcular pontuações algorítmicas:

- Conjuntos de dados do Adobe Analytics usando o [Conector de origem do Analytics](../../sources/tutorials/ui/create/adobe-applications/analytics.md)
- Conjuntos de dados do Evento de experiência (EE) em geral do esquema Adobe Experience Platform
- Conjuntos de dados CEE (Consumer Experience Event)

Agora é possível adicionar vários conjuntos de dados de diferentes fontes com base na variável **mapa de identidade** (campo) se cada um dos conjuntos de dados compartilhar o mesmo tipo de identidade (namespace), como uma ECID. Após selecionar uma identidade e um namespace, as métricas de integridade da coluna de ID são exibidas, indicando o volume de dados que estão sendo compilados. Para saber mais sobre como adicionar vários conjuntos de dados, visite o [Guia do usuário do Attribution AI](./user-guide.md#identity).

As informações do canal nem sempre são mapeadas por padrão. Em alguns casos, se mediaChannel (campo) estiver em branco, você não poderá &quot;continuar&quot; até mapear um campo para mediaChannel, pois é uma coluna obrigatória. Se o canal for detectado no conjunto de dados, ele será mapeado para mediaChannel por padrão. As outras colunas, como **tipo de mídia** e **ação de mídia** ainda são opcionais.

Depois de mapear o campo de canal, continue para a etapa &quot;Definir eventos&quot;, onde é possível selecionar eventos de conversão, eventos de ponto de contato e escolher campos específicos em conjuntos de dados individuais.

>[!IMPORTANT]
>
>O conector de origem do Adobe Analytics pode levar até quatro semanas para preencher dados. Se você configurar um conector recentemente, deve verificar se o conjunto de dados tem o comprimento mínimo de dados necessário para o Attribution AI. Revise o [dados históricos](#data-requirements) para verificar se há dados suficientes para calcular pontuações algorítmicas precisas.

Para obter mais detalhes sobre a configuração da variável [!DNL Consumer Experience Event] (CEE), consulte o [Preparação de dados dos Serviços inteligentes](../data-preparation.md) guia. Para obter mais informações sobre o mapeamento de dados do Adobe Analytics, visite o [Mapeamentos de campo do Analytics](../../sources/connectors/adobe-applications/analytics.md) documentação.

Nem todas as colunas na [!DNL Consumer Experience Event] (CEE) são obrigatórios para o Attribution AI.

Você pode configurar os pontos de contato usando qualquer campo recomendado abaixo no esquema ou no conjunto de dados selecionado.

| Colunas recomendadas | Necessário para |
| --- | --- |
| Campo de identidade primária | Ponto de contato / Conversão |
| Carimbo de data e hora | Ponto de contato / Conversão |
| Canal._Tipo | Ponto de contato |
| Channel.mediaAction | Ponto de contato |
| Channel.mediaType | Ponto de contato |
| Marketing.trackingCode | Ponto de contato |
| Marketing.campaignname | Ponto de contato |
| Marketing.campaigngroup | Ponto de contato |
| Commerce | Conversão |

Normalmente, a atribuição é executada em colunas de conversão, como pedido, compras e check-outs em &quot;comércio&quot;. As colunas para &quot;canal&quot; e &quot;marketing&quot; são usadas para definir pontos de contato para o Attribution AI (por exemplo, `channel._type = 'https://ns.adobe.com/xdm/channel-types/email'`). Para obter resultados e insights ideais, é altamente recomendável incluir o máximo possível de colunas de conversão e ponto de contato. Além disso, você não está limitado apenas às colunas acima. Você pode incluir qualquer outra coluna recomendada ou personalizada como conversão ou definição de ponto de contato.

Os conjuntos de dados de eventos de experiência (EE) não precisam ter combinações de canal e marketing explicitamente, desde que as informações de canal ou campanha relevantes para configurar um ponto de contato estejam presentes em um dos campos mixin ou pass through .

>[!TIP]
>
>Se você estiver usando dados do Adobe Analytics no esquema CEE, as informações do ponto de contato do Analytics normalmente serão armazenadas em `channel.typeAtSource` (por exemplo, `channel.typeAtSource = 'email'`).

## Dados históricos {#data-requirements}

>[!IMPORTANT]
>
> A quantidade mínima de dados necessária para o Attribution AI funcionar é a seguinte:
> - Você precisa fornecer pelo menos 3 meses (90 dias) de dados para executar um bom modelo.
> - Você precisa de pelo menos 1000 conversões.


O Attribution AI requer dados históricos como entrada para treinamento de modelo. A duração exigida dos dados é determinada principalmente por dois fatores principais: janela de treinamento e janela de retrospectiva. Os dados com janelas de treinamento mais curtas são mais sensíveis às tendências recentes, enquanto janelas de treinamento mais longas ajudam a produzir modelos mais estáveis e precisos. É importante modelar o objetivo com dados históricos que melhor representem suas metas de negócios.

O [configuração da janela de treinamento](./user-guide.md#training-window) filtros eventos de conversão definidos para serem incluídos no treinamento do modelo com base no tempo de ocorrência. Atualmente, a janela mínima de treinamento é de 1 trimestre (90 dias). O [janela de retrospectiva](./user-guide.md#lookback-window) fornece um período que indica quantos dias antes dos pontos de contato do evento de conversão relacionados a esse evento de conversão devem ser incluídos. Juntos, esses dois conceitos determinam a quantidade de dados de entrada (medidos por dias) necessária para um aplicativo.

Por padrão, o Attribution AI define a janela de treinamento como os 2 trimestres mais recentes (6 meses) e a janela de lookback como 56 dias. Em outras palavras, o modelo levará em consideração todos os eventos de conversão definidos que ocorreram nos últimos 2 trimestres e procurará todos os pontos de contato que ocorreram nos 56 dias anteriores ao(s) evento(s) de conversão associado(s).

**Fórmula**:

Comprimento mínimo dos dados necessários = janela de treinamento + janela de lookback

>[!TIP]
>
> O comprimento mínimo de dados necessário para um aplicativo com configurações padrão é: 2 trimestres (180 dias) + 56 dias = 236 dias.

Exemplo:

- Você deseja atribuir os eventos de conversão que ocorreram nos últimos 90 dias (3 meses) e rastrear todos os pontos de contato que ocorreram dentro de 4 semanas antes do evento de conversão. A duração dos dados de entrada deve abranger os últimos 90 dias + 28 dias (4 semanas). A janela de treinamento é de 90 dias e a janela de lookback é de 28 dias, totalizando 118 dias.

## Dados de saída do Attribution AI

O Attribution AI gera o seguinte:

- [Pontuações granulares brutas](#raw-granular-scores)
- [Pontuações agregadas](#aggregated-attribution-scores)

**Exemplo de schema de saída:**

![](./images/input-output/schema_output.gif)

### Pontuações granulares brutas {#raw-granular-scores}

O Attribution AI gera pontuações de atribuição no nível mais granular possível, para que você possa dividir e dividir as pontuações por qualquer coluna de pontuação. Para exibir essas pontuações na interface do usuário, leia a seção sobre [como visualizar caminhos de pontuação brutos](#raw-score-path). Para baixar as pontuações usando a API, acesse a [download de pontuações no Attribution AI](./download-scores.md) documento.

>[!NOTE]
>
> Você pode ver qualquer coluna de relatório desejada do conjunto de dados de entrada no conjunto de dados de saída da pontuação somente se um dos seguintes for verdadeiro:
> - A coluna de relatório é incluída na página de configuração como parte do ponto de contato ou da configuração de definição de conversão.
> - A coluna de relatório é incluída em colunas adicionais de conjunto de dados de pontuação.


A tabela a seguir descreve os campos de esquema na saída de exemplo de pontuações brutas:

| Nome da coluna (DataType) | Nulável | Descrição |
| --- | --- | --- |
| timestamp (DateTime) | Falso | A hora em que ocorreu um evento de conversão ou observação. <br> **Exemplo:** 2020-06-09T00:01:51.000Z |
| identityMap (Map) | Verdadeiro | identityMap do usuário semelhante ao formato CEE XDM. |
| eventType (String) | Verdadeiro | O tipo de evento principal para este registro de série de tempo. <br> **Exemplo:** &quot;Pedido&quot;, &quot;Compra&quot;, &quot;Visita&quot; |
| eventMergeId (Cadeia de caracteres) | Verdadeiro | Uma ID para correlacionar ou mesclar várias [!DNL Experience Events] juntos que são essencialmente o mesmo evento ou devem ser mesclados. Isso deve ser preenchido pelo produtor de dados antes da ingestão. <br> **Exemplo:** 575525617716-0-edc2ed37-1aab-4750-a820-1c2b3844b8c4 |
| _id (Cadeia de caracteres) | Falso | Um identificador exclusivo para o evento da série de tempo. <br> **Exemplo:** 4461-edc2ed37-1aab-4750-a820-1c2b3844b8c4 |
| _tenantId (Objeto) | Falso | O contêiner de objeto de nível superior correspondente à ID do tentante. <br> **Exemplo:** _atsdsnrmsv2 |
| nome_do_esquema (Objeto) | Falso | Pontuar a linha com o evento de conversão com todos os eventos de ponto de contato associados a ela e seus metadados. <br> **Exemplo:** Pontuações do Attribution AI - Nome do Modelo__2020 |
| segmentação (cadeia de caracteres) | Verdadeiro | Segmento de conversão, como segmentação geográfica, contra a qual o modelo foi criado. No caso de ausência de segmentos, o segmento é o mesmo que conversionName. <br> **Exemplo:** ORDER_US |
| conversionName (String) | Verdadeiro | Nome da conversão configurada durante a configuração. <br> **Exemplo:** Pedido, Cliente Potencial, Visita |
| conversão (Objeto) | Falso | Colunas de metadados de conversão. |
| dataSource (String) | Verdadeiro | Identificação global exclusiva de uma fonte de dados. <br> **Exemplo:** Adobe Analytics |
| eventSource (String) | Verdadeiro | A fonte quando o evento real aconteceu. <br> **Exemplo:** Adobe.com |
| eventType (String) | Verdadeiro | O tipo de evento principal para este registro de série de tempo. <br> **Exemplo:** Pedido |
| geo (cadeia de caracteres) | Verdadeiro | A localização geográfica onde a conversão foi entregue `placeContext.geo.countryCode`. <br> **Exemplo:** US |
| priceTotal (Double) | Verdadeiro | Receitas provenientes da conversão <br> **Exemplo:** 99,9 |
| produto (cadeia de caracteres) | Verdadeiro | O identificador XDM do próprio produto. <br> **Exemplo:** RX 1080 ti |
| productType (String) | Verdadeiro | O nome de exibição do produto, conforme apresentado ao usuário para esta exibição de produto. <br> **Exemplo:** Gpus |
| quantidade (número inteiro) | Verdadeiro | Quantidade comprada durante a conversão. <br> **Exemplo:** 1 1080 ti |
| receiveTimestamp (DateTime) | Verdadeiro | Carimbo de data e hora da conversão recebido. <br> **Exemplo:** 2020-06-09T00:01:51.000Z |
| skuId (cadeia de caracteres) | Verdadeiro | Unidade de manutenção de estoque (SKU), o identificador exclusivo de um produto definido pelo fornecedor. <br> **Exemplo:** MJ-03-XS-Black |
| timestamp (DateTime) | Verdadeiro | Carimbo de data e hora da conversão. <br> **Exemplo:** 2020-06-09T00:01:51.000Z |
| passThrough (Objeto) | Verdadeiro | Colunas Adicionais do Conjunto de Dados de Pontuação especificadas pelo usuário ao configurar o modelo. |
| commerce_order_purchaseCity (String) | Verdadeiro | Coluna adicional do conjunto de dados da pontuação. <br> **Exemplo:** cidade: San Jose |
| customerProfile (Objeto) | Falso | Detalhes de identidade do usuário usado para criar o modelo. |
| identidade (Objeto) | Falso | Contém os detalhes do usuário usado para criar o modelo, como `id` e `namespace`. |
| id (cadeia de caracteres) | Verdadeiro | ID de identidade do usuário, como ID de cookie ou AAID ou MCID etc. <br> **Exemplo:** 17348762725408656344688320891369597404 |
| namespace (cadeia de caracteres) | Verdadeiro | Namespace de identidade usado para criar os caminhos e, portanto, o modelo. <br> **Exemplo:** aaid |
| touchpointsDetail (Matriz de objetos) | Verdadeiro | A lista de detalhes do ponto de contato que levam à conversão solicitada por | ocorrência de ponto de contato ou carimbo de data e hora. |
| touchpointName (String) | Verdadeiro | Nome do ponto de contato que foi configurado durante a configuração. <br> **Exemplo:** PAID_SEARCH_CLICK |
| pontuações (Objeto) | Verdadeiro | Contribuição do ponto de contato para essa conversão como pontuação. Para obter mais informações sobre as pontuações produzidas nesse objeto, consulte a [pontuações de atribuição agregada](#aggregated-attribution-scores) seção. |
| touchPoint (objeto) | Verdadeiro | Metadados de ponto de contato. Para obter mais informações sobre as pontuações produzidas nesse objeto, consulte a [pontuações agregadas](#aggregated-scores) seção. |

### Visualização de caminhos de pontuação bruta (UI) {#raw-score-path}

Você pode visualizar o caminho para suas pontuações brutas na interface do usuário do . Comece selecionando **[!UICONTROL Esquemas]** na interface do usuário da plataforma , procure e selecione o esquema de pontuações do AI de atribuição no **[!UICONTROL Procurar]** guia .

![Escolha seu esquema](./images/input-output/schemas_browse.png)

Em seguida, selecione um campo dentro da variável **[!UICONTROL Estrutura]** da interface do usuário, a **[!UICONTROL Propriedades do campo]** será aberta. Within **[!UICONTROL Propriedades do campo]** é o campo de caminho que mapeia suas pontuações brutas.

![Escolha um esquema](./images/input-output/field_properties.png)

### Pontuações de atribuição agregadas {#aggregated-attribution-scores}

As pontuações agregadas podem ser baixadas no formato CSV da interface do usuário da plataforma se o intervalo de datas for inferior a 30 dias.

O Attribution AI suporta duas categorias de pontuações de atribuição, pontuações algorítmicas e baseadas em regras.

O Attribution AI produz dois tipos diferentes de pontuações algorítmicas, incrementais e influenciáveis. Uma pontuação influenciada é a fração da conversão pela qual cada ponto de contato de marketing é responsável. Uma pontuação incremental é a quantidade de impacto marginal causado diretamente pelo ponto de contato de marketing. A principal diferença entre a pontuação incremental e a pontuação influenciada é que a pontuação incremental leva o efeito da linha de base em consideração. Não é considerado que uma conversão seja causada apenas pelos pontos de contato de marketing anteriores.

Este é um exemplo rápido de saída de schema de Attribution AI da interface do usuário do Adobe Experience Platform:

![](./images/input-output/schema_screenshot.png)

Consulte a tabela abaixo para obter mais detalhes sobre cada uma dessas pontuações de atribuição:

| Pontuações de atribuição | Descrição |
| ----- | ----------- |
| Influenciado (algorítmico) | A pontuação influenciada é a fração da conversão pela qual cada ponto de contato de marketing é responsável. |
| Incremental (algorítmico) | A pontuação incremental é a quantidade de impacto marginal causado diretamente por um ponto de contato de marketing. |
| Primeiro contato | A pontuação de atribuição baseada em regras que atribui todos os créditos ao ponto de contato inicial em um caminho de conversão. |
| Último contato | A pontuação de atribuição baseada em regras que atribui todo o crédito ao ponto de contato mais próximo da conversão. |
| Linear | Pontuação de atribuição baseada em regras que atribui crédito igual a cada ponto de contato em um caminho de conversão. |
| Forma de U | Pontuação de atribuição baseada em regras que atribui 40% do crédito ao primeiro ponto de contato e 40% do crédito ao último ponto de contato, com os outros pontos de contato dividindo os 20% restantes igualmente. |
| Declínio de tempo | A pontuação de atribuição baseada em regras na qual os pontos de contato mais próximos da conversão recebem mais crédito do que os pontos de contato mais distantes no tempo da conversão. |

**Referência de pontuação bruta (pontuações de atribuição)**

A tabela abaixo mapeia as pontuações de atribuição para as pontuações brutas. Se quiser baixar suas pontuações brutas, visite a [download de pontuações no Attribution AI](./download-scores.md) documentação.

| Pontuações de atribuição | Coluna de referência de pontuação bruta |
| --- | --- |
| Influenciado (algorítmico) | _tenantID.your_schema_name.element.touchpoint.algorithmicInfluenced |
| Incremental (algorítmico) | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.algorithmicInfluenced |
| Primeiro contato | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.firstTouch |
| Último contato | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.lastTouch |
| Linear | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.linear |
| Forma de U | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.Shape |
| Declínio de tempo | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.decayUnits |

### Pontuações agregadas {#aggregated-scores}

As pontuações agregadas podem ser baixadas no formato CSV da interface do usuário da plataforma se o intervalo de datas for inferior a 30 dias. Consulte a tabela abaixo para obter mais detalhes sobre cada uma dessas colunas agregadas.

| Nome da coluna | Restrição | Nulável | Descrição |
| --- | --- | --- | --- |
| customerevents_date (DateTime) | Formato definido pelo usuário e fixo | Falso | Data do evento do cliente no formato AAAA-MM-DD. <br> **Exemplo**: 2016-05-02 |
| mediatouchpoints_date (DateTime) | Formato definido pelo usuário e fixo | Verdadeiro | Data do ponto de contato da mídia no formato AAAA-MM-DD <br> **Exemplo**: 2017-04-21 |
| segment (cadeia de caracteres) | Calculado | Falso | Segmento de conversão, como segmentação geográfica, contra a qual o modelo é criado. No caso de ausência de segmentos, o segmento é igual a conversion_scope. <br> **Exemplo**: ORDER_AMER |
| conversion_scope (String) | Definido pelo usuário | Falso | Nome da Conversão conforme configurado pelo usuário. <br> **Exemplo**: ORDEM |
| touchpoint_scope (String) | Definido pelo usuário | Verdadeiro | Nome do ponto de contato como configurado pelo usuário <br> **Exemplo**: PAID_SEARCH_CLICK |
| produto (cadeia de caracteres) | Definido pelo usuário | Verdadeiro | O identificador XDM do produto. <br> **Exemplo**: CC |
| product_type (cadeia de caracteres) | Definido pelo usuário | Verdadeiro | O nome de exibição do produto, conforme apresentado ao usuário para esta exibição de produto. <br> **Exemplo**: gpus, laptops |
| geo (cadeia de caracteres) | Definido pelo usuário | Verdadeiro | A localização geográfica onde a conversão foi entregue (placeContext.geo.countryCode) <br> **Exemplo**: US |
| event_type (String) | Definido pelo usuário | Verdadeiro | O tipo de evento principal para este registro de série de tempo <br> **Exemplo**: Conversão paga |
| media_type (String) | ENUM | Falso | Descreve se o tipo de mídia é pago, de propriedade ou ganho. <br> **Exemplo**: PAGO, PROPRIETÁRIO |
| channel (String) | ENUM | Falso | O `channel._type` propriedade que é usada para fornecer uma classificação aproximada de canais com propriedades semelhantes no [!DNL Consumer Experience Event] XDM. <br> **Exemplo**: PESQUISA |
| action (String) | ENUM | Falso | O `mediaAction` é usada para fornecer um tipo de ação de mídia de evento de experiência. <br> **Exemplo**: CLIQUE EM |
| campaign_group (String) | Definido pelo usuário | Verdadeiro | Nome do grupo de campanha no qual várias campanhas são agrupadas como &#39;50%_DISCOUNT&#39;. <br> **Exemplo**: COMERCIAL |
| campaign_name (String) | Definido pelo usuário | Verdadeiro | Nome da campanha usada para identificar a campanha de marketing como &#39;50%_DISCOUNT_USA&#39; ou &#39;50%_DISCOUNT_ASIA&#39;. <br> **Exemplo**: Venda de Ação de Graças |

**Referência de pontuação bruta (agregada)**

A tabela abaixo mapeia as pontuações agregadas para as pontuações brutas. Se quiser baixar suas pontuações brutas, visite a [download de pontuações no Attribution AI](./download-scores.md) documentação. Para visualizar os caminhos de pontuação bruta na interface do usuário, visite a seção em [como visualizar caminhos de pontuação brutos](#raw-score-path) neste documento.

| Nome da coluna | Coluna de referência da pontuação bruta |
| --- | --- |
| customerevents_date | carimbo de data e hora |
| mediatouchpoints_date | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.timestamp |
| segmento | _tenantID.your_schema_name.segmentation |
| conversion_scope | _tenantID.your_schema_name.conversion.conversionName |
| touchpoint_scope | _tenantID.your_schema_name.touchpointsDetail.element.touchpointName |
| produto | _tenantID.your_schema_name.conversion.product |
| product_type | _tenantID.your_schema_name.conversion.product_type |
| geografia | _tenantID.your_schema_name.conversion.geo |
| event_type | eventType |
| media_type | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.mediaType |
| channel | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.mediaChannel |
| ação | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.mediaAction |
| campaign_group | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.campaignGroup |
| campaign_name | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.campaignName |

>[!IMPORTANT]
>
> - Para ajudar a facilitar a conformidade com o GDPR no Attribution AI, você pode usar o Adobe Experience Platform Privacy Service para configurar protocolos para atender às solicitações do cliente para acessar e excluir seus dados no lago de dados, no Serviço de identidade e no Perfil do cliente em tempo real.
> - Todos os dados são criptografados em trânsito e em repouso. Consulte a documentação para saber mais sobre [criptografia de dados](../../../help/landing/governance-privacy-security/encryption.md)


## Próximas etapas {#next-steps}

Depois de preparar seus dados e ter todas as credenciais e esquemas em vigor, comece seguindo a [Guia do usuário do Attribution AI](./user-guide.md). Este guia aborda a criação de uma instância para o Attribution AI.
