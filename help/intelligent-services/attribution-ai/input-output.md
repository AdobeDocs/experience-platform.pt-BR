---
keywords: Experience Platform;getting started;Attribution ai;popular topics;Attribution ai input;Attribution ai output;
solution: Experience Platform
title: Entrada e saída de Attribution AI
topic: Input and Output data for Attribution AI
description: O documento a seguir descreve as diferentes entradas e saídas utilizadas no Attribution AI.
translation-type: tm+mt
source-git-commit: 5126ef74330d9cee7234ccd1ee7260b09db9e78c
workflow-type: tm+mt
source-wordcount: '2174'
ht-degree: 3%

---


# [!DNL Attribution AI] entrada e saída

O documento a seguir descreve as diferentes entradas e saídas utilizadas em [!DNL Attribution AI].

## [!DNL Attribution AI] dados de entrada

[!DNL Attribution AI] usa [!DNL Consumer Experience Event] dados para calcular pontuações algorítmicas. Para obter mais detalhes sobre [!DNL Consumer Experience Event], consulte [Preparar dados para uso na documentação](../data-preparation.md)dos Serviços inteligentes.

Nem todas as colunas no schema [!DNL Consumer Experience Event] (CEE) são obrigatórias para o Attribution AI.

>[!NOTE]
>
> As 9 colunas a seguir são obrigatórias, outras são opcionais, mas são recomendadas/necessárias se você quiser usar os mesmos dados para outras soluções de Adobe, como [!DNL Customer AI] e [!DNL Journey AI].

| Colunas obrigatórias | Necessário para |
| --- | --- |
| Campo de identidade principal | Ponto de contato / Conversão |
| Carimbo de data e hora | Ponto de contato / Conversão |
| Channel._type | Ponto de contato |
| Channel.mediaAction | Ponto de contato |
| Channel.mediaType | Ponto de contato |
| Marketing.trackingCode | Ponto de contato |
| Marketing.campaignname | Ponto de contato |
| Marketing.campaigngroup | Ponto de contato |
| Comércio | Conversão |

Normalmente, a atribuição é executada em colunas de conversão, como ordem, compras e finalizações em &quot;comércio&quot;. As colunas &quot;canal&quot; e &quot;marketing&quot; são altamente recomendadas para definir pontos de contato para obter bons insights. No entanto, é possível incluir qualquer outra coluna adicional junto com as colunas acima para configurar como uma conversão ou definição de ponto de contato.

As colunas abaixo não são obrigatórias, mas é recomendável incluí-las no schema CEE se você tiver as informações disponíveis.

**Colunas recomendadas adicionais:**
- web.webReferer
- web.webInteraction
- web.webPageDetails
- xdm:productListItems

### Dados históricos

>[!IMPORTANT]
>
> A quantidade mínima de dados necessária para que o Attribution AI funcione é a seguinte:
> - É necessário fornecer pelo menos 3 meses (90 dias) de dados para executar um bom modelo.
> - Você precisa de pelo menos 1000 conversões.


O Attribution AI requer dados históricos como entrada para treinamento de modelo. A duração dos dados exigidos é principalmente determinada por dois fatores chave: janela de treinamento e janela de retrospectiva. As entradas com janelas de treinamento mais curtas são mais sensíveis às tendências recentes, enquanto janelas de treinamento mais longas ajudam a produzir modelos mais estáveis e precisos. É importante modelar o objetivo com dados históricos que melhor representem suas metas de negócios.

Os eventos de conversão de filtros de configuração [da janela de](./user-guide.md#training-window) treinamento estão definidos para serem incluídos no treinamento de modelo com base no tempo de ocorrência. Atualmente, a janela mínima de treinamento é de 1 trimestre (90 dias). A janela [de](./user-guide.md#lookback-window) pesquisa fornece um período que indica quantos dias antes dos pontos de contato do evento de conversão relacionados a esse evento de conversão devem ser incluídos. Esses dois conceitos juntos determinam a quantidade de dados de entrada (medidos por dias) necessária para um aplicativo.

Por padrão, o Attribution AI define a janela de treinamento como os 2 trimestres mais recentes (6 meses) e a janela de retrospectiva como 56 dias. Em outras palavras, o modelo levará em consideração todos os eventos de conversão definidos que ocorreram nos últimos 2 trimestres e procurará todos os pontos de contato que ocorreram dentro de 56 dias antes dos eventos de conversão associados.

**Fórmula**:

Comprimento mínimo dos dados necessários = janela de treinamento + janela de pesquisa

>[!TIP]
> O comprimento mínimo de dados necessário para um aplicativo com configurações padrão é: 2 trimestres (180 dias) + 56 dias = 236 dias.

Exemplo :

- Você deseja atribuir eventos de conversão que ocorreram nos últimos 90 dias (3 meses) e rastrear todos os pontos de contato que ocorreram dentro de 4 semanas antes do evento de conversão. A duração dos dados de entrada deve ser de 90 dias + 28 dias (4 semanas). A janela de treinamento é de 90 dias e a janela de pesquisa é de 28 dias, totalizando 118 dias.

## dados de saída do Attribution AI

O Attribution AI gera o seguinte:

- [Pontuações granulares brutas](#raw-granular-scores)
- [Pontuações agregadas](#aggregated-attribution-scores)

Nos exemplos abaixo, uma saída CSV de amostra foi usada para fins ilustrativos. Estas são algumas das características do arquivo de amostra.

- O arquivo não tinha nenhum evento token.
- O arquivo não tinha nenhum evento somente de conversão (não continha linhas de pontuação com 0 como pontuação marginal).
- Características dos dados:
   - Total de 368 linhas de amostra.
   - Pelo menos 8 conversões com 3 canais diferentes cada.
   - 151 conversões do tipo de conversão `“Digital_Product_Purchase”`.
   - 10 pontos de contato distintos, EMAIL, SOCIAL_LINKEDIN, ADS_GOOGLE, SOCIAL_OTHER, ADS_OTHER, SOCIAL_TWITTER, LANDINGPAGE, SOCIAL_FB, ADS_BING, IMPRESSÃO.
   - As conversões e os pontos de contato variam entre 8 e 9 meses, respectivamente.
   - As linhas são ordenadas por `id`, `conversion_timestamp` e `touchpoint_timestamp`.

**Exemplo de schema de saída:**

![](./images/input-output/schema_output.gif)

### Pontuações granulares brutas {#raw-granular-scores}

O Attribution AI gera pontuações de atribuição no nível mais granular possível para que você possa dividir e cortar as pontuações por qualquer coluna de pontuação. Para visualização dessas pontuações na interface do usuário, leia a seção sobre a [exibição de caminhos](#raw-score-path)de pontuação brutos. Para baixar as pontuações usando a API, visite o [download das pontuações no documento do Attribution AI](./download-scores.md) .

>[!NOTE]
>
> Você pode ver qualquer coluna de relatórios desejada do conjunto de dados de entrada no conjunto de dados de saída da pontuação somente se uma das seguintes opções for verdadeira:
> - A coluna relatórios é incluída na página de configuração como parte do ponto de contato ou da configuração de definição de conversão.
> - A coluna relatórios é incluída em colunas adicionais de conjunto de dados de pontuação.


A tabela a seguir descreve os campos de schema na saída de exemplo de pontuação bruta:

| Nome da coluna (DataType) | Nulo | Descrição |
| --- | --- | --- |
| timestamp (DateTime) | Falso | A hora em que ocorreu um evento de conversão ou observação. <br> **Exemplo:** 2020-06-09T00:01:51.000Z |
| identityMap (Map) | Verdadeiro | identityMap do usuário semelhante ao formato XDM CEE. |
| eventType (String) | Verdadeiro | O tipo de evento principal para este registro de série de tempo. <br> **Exemplo:** &quot;Pedido&quot;, &quot;Compra&quot;, &quot;Visita&quot; |
| eventMergeId (String) | Verdadeiro | Uma ID para correlacionar ou mesclar vários [!DNL Experience Events] juntos que são essencialmente o mesmo evento ou devem ser mesclados. Este deve ser preenchido pelo produtor de dados antes da ingestão. <br> **Exemplo:** 575525617716-0-edc2ed37-1aab-4750-a820-1c2b3844b8c4 |
| _id (String) | Falso | Um identificador exclusivo para o evento da série de tempo. <br> **Exemplo:** 4461-edc2ed37-1aab-4750-a820-1c2b3844b8c4 |
| _locatárioId (Objeto) | Falso | O container de objeto de nível superior correspondente à sua ID do tentant. <br> **Exemplo:** _atsdsnrmsv2 |
| your_schema_name (Objeto) | Falso | Ponha a linha com o evento de conversão em todos os eventos de ponto de contato associados a ela e seus metadados. <br> **Exemplo:** Pontuações do Attribution AI - Nome do modelo__2020 |
| segmentação (string) | Verdadeiro | Segmento de conversão, como a segmentação geográfica, contra a qual o modelo foi criado. Em caso de ausência de segmentos, o segmento é igual a conversionName. <br> **Exemplo:** ORDER_US |
| conversionName (String) | Verdadeiro | Nome da conversão configurada durante a configuração. <br> **Exemplo:** Pedido, cliente potencial, visita |
| conversão (Objeto) | Falso | Colunas de metadados de conversão. |
| dataSource (String) | Verdadeiro | Identificação global exclusiva de uma fonte de dados. <br> **Exemplo:** Adobe Analytics |
| eventSource (String) | Verdadeiro | A fonte quando o evento real aconteceu. <br> **Exemplo:** Adobe.com |
| eventType (String) | Verdadeiro | O tipo de evento principal para este registro de série de tempo. <br> **Exemplo:** Pedido |
| geo (String) | Verdadeiro | A localização geográfica onde a conversão foi entregue `placeContext.geo.countryCode`. <br> **Exemplo:** EUA |
| priceTotal (Duplo) | Verdadeiro | Receitas obtidas através da conversão <br> **Exemplo:** 99,9 |
| product (String) | Verdadeiro | O identificador XDM do próprio produto. <br> **Exemplo:** RX 1080 ti |
| productType (String) | Verdadeiro | O nome de exibição do produto conforme apresentado ao usuário para esta visualização de produto. <br> **Exemplo:** Gpus |
| quantidade (número inteiro) | Verdadeiro | Quantidade comprada durante a conversão. <br> **Exemplo:** 1 1080 ti |
| receiveTimestamp (DateTime) | Verdadeiro | Carimbo de data e hora da conversão recebido. <br> **Exemplo:** 2020-06-09T00:01:51.000Z |
| skuId (String) | Verdadeiro | Unidade de manutenção de estoque (SKU), o identificador exclusivo de um produto definido pelo fornecedor. <br> **Exemplo:** MJ-03-XS-Black |
| timestamp (DateTime) | Verdadeiro | Carimbo de data e hora da conversão. <br> **Exemplo:** 2020-06-09T00:01:51.000Z |
| passThrough (Objeto) | Verdadeiro | Colunas Adicionais do conjunto de dados de Pontuação especificadas pelo usuário ao configurar o modelo. |
| commerce_order_purchaseCity (String) | Verdadeiro | Coluna de conjunto de dados de pontuação adicional. <br> **Exemplo:** cidade : San Jose |
| customerProfile (Object) | Falso | Detalhes de identificação do usuário usado para criar o modelo. |
| identity (Object) | Falso | Contém os detalhes do usuário usado para criar o modelo, como `id` e `namespace`. |
| id (String) | Verdadeiro | ID de identificação do usuário, como ID de cookie ou AAID ou MCID etc. <br> **Exemplo:** 17348762725408656344688320891369597404 |
| namespace (string) | Verdadeiro | namespace de identidade usada para criar os caminhos e, consequentemente, o modelo. <br> **Exemplo:** auxílio |
| touchpointsDetail (Object Array) | Verdadeiro | A lista dos detalhes do ponto de contato que levam à conversão ordenada pela ocorrência do ponto de contato ou pelo carimbo de data e hora. |
| touchpointName (String) | Verdadeiro | Nome do ponto de contato configurado durante a configuração. <br> **Exemplo:** PAID_SEARCH_CLICK |
| pontuações (Objeto) | Verdadeiro | Contribuição do ponto de contato para essa conversão como pontuação. Para obter mais informações sobre as pontuações produzidas dentro desse objeto, consulte a seção Pontuações [de atribuição](#aggregated-attribution-scores) agregadas. |
| touchPoint (Objeto) | Verdadeiro | Metadados de ponto de contato. Para obter mais informações sobre as pontuações produzidas dentro desse objeto, consulte a seção Pontuações [](#aggregated-scores) agregadas. |

### Exibição de caminhos de pontuação brutos (IU) {#raw-score-path}

Você pode visualização o caminho para suas pontuações brutas na interface do usuário. Start selecionando **[!UICONTROL Schemas]** na interface do usuário do Platform e, em seguida, procure e selecione o schema de pontuações AI de sua atribuição na guia *[!UICONTROL Procurar]* .

![Escolha seu schema](./images/input-output/schemas_browse.png)

Em seguida, selecione um campo na janela *[!UICONTROL Estrutura]* da interface do usuário, a guia Propriedades *[!UICONTROL de]* campo será aberta. Dentro das propriedades ** de campo é o campo *[!UICONTROL Caminho]* que mapeia para suas pontuações brutas.

![Escolha um Schema](./images/input-output/field_properties.png)


### Pontuações de atribuição agregadas {#aggregated-attribution-scores}

As pontuações agregadas podem ser baixadas no formato CSV da interface do usuário do Platform se o intervalo de datas for inferior a 30 dias.

O Attribution AI suporta duas categorias de pontuações de atribuição, pontuações algorítmicas e baseadas em regras.

O Attribution AI produz dois tipos diferentes de pontuações algorítmicas, incrementais e influenciadas. Uma pontuação influenciada é a fração da conversão pela qual cada ponto de contato de marketing é responsável. Uma pontuação incremental é a quantidade de impacto marginal causado diretamente pelo ponto de contato de marketing. A principal diferença entre a pontuação incremental e a pontuação influenciada é que a pontuação incremental leva o efeito da linha de base em consideração. Não presume que a conversão seja causada apenas pelos pontos de contato de marketing anteriores.

Veja um exemplo rápido de saída de schema da interface do Adobe Experience Platform:

![](./images/input-output/schema_screenshot.png)

Consulte a tabela abaixo para obter mais detalhes sobre cada uma dessas pontuações de atribuição:

| Pontuações de atribuição | Descrição |
| ----- | ----------- |
| Influenciado (algorítmico) | A pontuação influenciada é a fração da conversão pela qual cada ponto de contato de marketing é responsável. |
| Incremental (algorítmico) | A pontuação incremental é a quantidade de impacto marginal causado diretamente por um ponto de contato de marketing. |
| Primeiro contato | A pontuação de atribuição baseada em regras que atribui todos os créditos ao ponto de contato inicial em um caminho de conversão. |
| Último contato | A pontuação de atribuição baseada em regras que atribui todo o crédito ao ponto de contato mais próximo da conversão. |
| Linear | A pontuação de atribuição baseada em regras que atribui crédito igual a cada ponto de contato em um caminho de conversão. |
| Forma de U | Pontuação de atribuição baseada em regras que atribui 40% do crédito ao primeiro ponto de contato e 40% do crédito ao último ponto de contato, com os outros pontos de contato dividindo os restantes 20% igualmente. |
| Declínio de tempo | A pontuação de atribuição baseada em regras na qual os pontos de contato mais próximos da conversão recebem mais crédito do que os pontos de contato mais distantes no tempo da conversão. |

**Referência de pontuação bruta (pontuações de atribuição)**

A tabela abaixo mapeia as pontuações de atribuição para as pontuações brutas. Se você quiser baixar suas pontuações brutas, visite as pontuações de [download na documentação do Attribution AI](./download-scores.md) .

| Pontuações de atribuição | Coluna de referência de pontuação bruta |
| --- | --- |
| Influenciado (algorítmico) | _locatárioID.your_schema_name.element.touchpoint.algorithmicInfluenciado |
| Incremental (algorítmico) | _locatárioID.your_schema_name.touchpointsDetail.element.touchpoint.algorithmicInfluenciado |
| Primeiro contato | _locatárioID.your_schema_name.touchpointsDetail.element.touchpoint.firstTouch |
| Último contato | _locatárioID.your_schema_name.touchpointsDetail.element.touchpoint.lastTouch |
| Linear | _locatárioID.your_schema_name.touchpointsDetail.element.touchpoint.linear |
| Forma de U | _locatárioID.your_schema_name.touchpointsDetail.element.touchpoint.uShape |
| Declínio de tempo | _locatárioID.your_schema_name.touchpointsDetail.element.touchpoint.decayUnits |

### Pontuações agregadas {#aggregated-scores}

As pontuações agregadas podem ser baixadas no formato CSV da interface do usuário do Platform se o intervalo de datas for inferior a 30 dias. Consulte a tabela abaixo para obter mais detalhes sobre cada uma dessas colunas de agregação.

| Nome da coluna | Restrição | Nulo | Descrição |
| --- | --- | --- | --- |
| customerevents_date (DateTime) | Formato definido pelo usuário e fixo | Falso | Data do Evento do cliente no formato AAAA-MM-DD. <br> **Exemplo**: 02/05/2016 |
| mediatouchpoints_date (DateTime) | Formato definido pelo usuário e fixo | Verdadeiro | Data do ponto de contato da mídia no formato AAAA-MM-DD <br> **Exemplo**: 2017-04-21 |
| segment (String) | Calculado | Falso | Segmento de conversão, como a segmentação geográfica, contra a qual o modelo foi criado. Em caso de ausência de segmentos, o segmento é o mesmo que conversion_scope. <br> **Exemplo**: ORDER_AMER |
| conversion_scope (String) | Definido pelo usuário | Falso | Nome da Conversão conforme configurado pelo usuário. <br> **Exemplo**: PEDIDO |
| touchpoint_scope (String) | Definido pelo usuário | Verdadeiro | Nome do ponto de contato como configurado pelo usuário <br> **Exemplo**: PAID_SEARCH_CLICK |
| product (String) | Definido pelo usuário | Verdadeiro | O identificador XDM do produto. <br> **Exemplo**: CC |
| product_type (String) | Definido pelo usuário | Verdadeiro | O nome de exibição do produto conforme apresentado ao usuário para esta visualização de produto. <br> **Exemplo**: gpus, laptops |
| geo (String) | Definido pelo usuário | Verdadeiro | A localização geográfica onde a conversão foi entregue (placeContext.geo.countryCode) <br> **Exemplo**: EUA |
| evento_type (String) | Definido pelo usuário | Verdadeiro | O tipo de evento principal para este registro de série de tempo <br> **Exemplo**: Conversão paga |
| media_type (String) | ENUM | Falso | Descreve se o tipo de mídia é pago, de propriedade ou ganho. <br> **Exemplo**: PAGO, PROPRIEDADE |
| canal (String) | ENUM | Falso | A `channel._type` propriedade usada para fornecer uma classificação aproximada de canais com propriedades semelhantes no [!DNL Consumer Experience Event] XDM. <br> **Exemplo**: PESQUISA |
| action (String) | ENUM | Falso | A `mediaAction` propriedade é usada para fornecer um tipo de ação de mídia de evento de experiência. <br> **Exemplo**: CLIQUE EM |
| campanha_group (String) | Definido pelo usuário | Verdadeiro | Nome do grupo de campanhas no qual várias campanhas são agrupadas como &#39;50%_DISCOUNT&#39;. <br> **Exemplo**: COMERCIAL |
| campanha_name (String) | Definido pelo usuário | Verdadeiro | Nome da campanha usada para identificar a campanha de marketing como &#39;50%_DISCOUNT_USA&#39; ou &#39;50%_DISCOUNT_ASIA&#39;. <br> **Exemplo**: Venda de Ação de Graças |

**Referência de pontuação bruta (agregada)**

A tabela abaixo mapeia as pontuações agregadas para as pontuações brutas. Se você quiser baixar suas pontuações brutas, visite as pontuações de [download na documentação do Attribution AI](./download-scores.md) . Para visualização dos caminhos de pontuação bruta na interface do usuário, visite a seção sobre como [visualizar caminhos](#raw-score-path) de pontuação bruta nesse documento.

| Nome da coluna | Coluna de referência de Pontuação Bruta |
| --- | --- |
| customerevents_date | carimbo de data e hora |
| mediatouchpoints_date | _locatárioID.your_schema_name.touchpointsDetail.element.touchpoint.timestamp |
| segmento | _locatárioID.your_schema_name.segmentation |
| conversion_scope | _locatárioID.your_schema_name.conversion.conversionName |
| touchpoint_scope | _locatárioID.your_schema_name.touchpointsDetail.element.touchpointName |
| produto | _locatárioID.your_schema_name.conversion.product |
| product_type | _locatárioID.your_schema_name.conversion.product_type |
| geo | _locatárioID.your_schema_name.conversion.geo |
| evento_type | eventType |
| media_type | _locatárioID.your_schema_name.touchpointsDetail.element.touchpoint.mediaType |
| canal | _locatárioID.your_schema_name.touchpointsDetail.element.touchpoint.mediaChannel |
| ação | _locatárioID.your_schema_name.touchpointsDetail.element.touchpoint.mediaAction |
| campanha_group | _locatárioID.your_schema_name.touchpointsDetail.element.touchpoint.campaignGroup |
| nome_da_campanha | _locatárioID.your_schema_name.touchpointsDetail.element.touchpoint.campaignName |


## Próximas etapas {#next-steps}

Depois de preparar seus dados e ter todas as suas credenciais e schemas no lugar, start seguindo o guia [do usuário do](./user-guide.md)Attribution AI. Este guia o orienta a criar uma instância para o Attribution AI.