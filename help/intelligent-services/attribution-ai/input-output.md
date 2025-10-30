---
keywords: Experience Platform;introdução;IA de atribuição;tópicos populares;Entrada de ia de atribuição;Saída de ia de atribuição;
feature: Attribution AI
title: Entrada e saída na IA de atribuição
description: O documento a seguir descreve as diferentes entradas e saídas utilizadas na IA de atribuição.
exl-id: d6dbc9ee-0c1a-4a5f-b922-88c7a36a5380
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '2467'
ht-degree: 3%

---

# Entrada e saída em [!DNL Attribution AI]

O documento a seguir descreve as diferentes entradas e saídas utilizadas em [!DNL Attribution AI].

## [!DNL Attribution AI] dados de entrada

A IA de atribuição funciona analisando os seguintes conjuntos de dados para calcular pontuações algorítmicas:

- Conjuntos de dados do Adobe Analytics usando o [conector de origem do Analytics](../../sources/tutorials/ui/create/adobe-applications/analytics.md)
- Conjuntos de dados de Evento de experiência (EE) em geral do esquema do Adobe Experience Platform
- Conjuntos de dados do Evento de experiência do consumidor (CEE)

Agora é possível adicionar vários conjuntos de dados de diferentes fontes com base no **mapa de identidade** (campo) se cada um dos conjuntos de dados compartilhar o mesmo tipo de identidade (namespace), como uma ECID. Após selecionar uma identidade e um namespace, são exibidas métricas de integridade da coluna de ID, que indicam o volume de dados que está sendo compilado. Para saber mais sobre como adicionar vários conjuntos de dados, visite o [guia do usuário da IA de atribuição](./user-guide.md#identity).

As informações do canal nem sempre são mapeadas por padrão. Em alguns casos, se mediaChannel (campo) estiver em branco, você não poderá &quot;continuar&quot; até mapear um campo para mediaChannel como se fosse uma coluna obrigatória. Se o canal for detectado no conjunto de dados, ele será mapeado para mediaChannel por padrão. As outras colunas, como **tipo de mídia** e **ação de mídia**, ainda são opcionais.

Depois de mapear o campo de canal, continue para a etapa &quot;Definir eventos&quot;, onde é possível selecionar os eventos de conversão, eventos de ponto de contato e escolher campos específicos de conjuntos de dados individuais.

>[!IMPORTANT]
>
>O conector de origem do Adobe Analytics pode levar até quatro semanas para preencher os dados. Se você configurou um conector recentemente, deve verificar se o conjunto de dados tem o comprimento mínimo de dados necessário para a IA de atribuição. Revise a seção [dados históricos](#data-requirements) para verificar se você tem dados suficientes para calcular pontuações algorítmicas precisas.

Para obter mais detalhes sobre como configurar o esquema [!DNL Consumer Experience Event] (CEE), consulte o guia [Preparação de dados dos Serviços inteligentes](../data-preparation.md). Para obter mais informações sobre como mapear dados do Adobe Analytics, visite a documentação [Mapeamentos de campos do Analytics](../../sources/connectors/adobe-applications/analytics.md).

Nem todas as colunas no esquema [!DNL Consumer Experience Event] (CEE) são obrigatórias para a IA de atribuição.

Você pode configurar os pontos de contato usando qualquer campo recomendado abaixo no esquema ou conjunto de dados selecionado.

| Colunas recomendadas | Necessário para |
| --- | --- |
| Campo de identidade principal | Ponto de contato / Conversão |
| Carimbo de data e hora | Ponto de contato / Conversão |
| Canal._type | Ponto de contato |
| Channel.mediaAction | Ponto de contato |
| Channel.mediaType | Ponto de contato |
| Marketing.trackingCode | Ponto de contato |
| Marketing.campaignname | Ponto de contato |
| Marketing.campaigngroup | Ponto de contato |
| Commerce | Conversão |

Normalmente, a atribuição é executada em colunas de conversão, como pedido, compras e check-outs em &quot;comércio&quot;. As colunas para &quot;canal&quot; e &quot;marketing&quot; são usadas para definir pontos de contato para a IA de atribuição (por exemplo, `channel._type = 'https://ns.adobe.com/xdm/channel-types/email'`). Para obter ótimos resultados e insights, é altamente recomendável incluir o máximo possível de colunas de conversão e de ponto de contato. Além disso, você não está limitado apenas às colunas acima. É possível incluir qualquer outra coluna recomendada ou personalizada como uma conversão ou definição de ponto de contato.

Os conjuntos de dados de Evento de experiência (EE) não precisam ter explicitamente mixins de Canal e Marketing, desde que as informações de canal ou campanha relevantes para configurar um ponto de contato estejam presentes em um dos campos de mixin ou passagem.

>[!TIP]
>
>Se você estiver usando dados do Adobe Analytics no esquema CEE, as informações do ponto de contato do Analytics normalmente são armazenadas em `channel.typeAtSource` (por exemplo, `channel.typeAtSource = 'email'`).

## Dados históricos {#data-requirements}

>[!IMPORTANT]
>
> A quantidade mínima de dados necessária para que a IA de atribuição funcione é a seguinte:
>
> - Você precisa fornecer pelo menos 3 meses (90 dias) de dados para executar um bom modelo.
> - Você precisa de pelo menos 1000 conversões.

A IA de atribuição exige dados históricos como entrada para o treinamento de modelo. A duração dos dados necessários é determinada principalmente por dois fatores principais: janela de treinamento e janela de retrospectiva. Entradas com janelas de treinamento mais curtas são mais sensíveis às tendências recentes, enquanto janelas de treinamento mais longas ajudam a produzir modelos mais estáveis e precisos. É importante modelar o objetivo com dados históricos que melhor representem suas metas comerciais.

A [configuração da janela de treinamento](./user-guide.md#training-window) filtra os eventos de conversão definidos para serem incluídos no treinamento de modelo com base no tempo de ocorrência. Atualmente, a janela mínima de treinamento é de 1 trimestre (90 dias). A [janela de retrospectiva](./user-guide.md#lookback-window) fornece um intervalo de tempo que indica quantos dias antes dos pontos de contato do evento de conversão relacionados a este evento de conversão devem ser incluídos. Esses dois conceitos juntos determinam a quantidade de dados de entrada (medida por dias) necessária para um aplicativo.

Por padrão, a IA de atribuição define a janela de treinamento como os 2 trimestres mais recentes (6 meses) e a janela de pesquisa como 56 dias. Em outras palavras, o modelo levará em consideração todos os eventos de conversão definidos que ocorreram nos últimos dois trimestres e procurará todos os pontos de contato que ocorreram dentro de 56 dias antes dos eventos de conversão associados.

**Fórmula**:

Tamanho mínimo de dados necessário = janela de treinamento + janela de pesquisa

>[!TIP]
>
> O comprimento mínimo de dados necessário para um aplicativo com configurações padrão é: 2 trimestres (180 dias) + 56 dias = 236 dias.

Exemplo:

- Você deseja atribuir eventos de conversão que ocorreram nos últimos 90 dias (3 meses) e rastrear todos os pontos de contato que ocorreram dentro de 4 semanas antes do evento de conversão. A duração dos dados de entrada deve abranger os últimos 90 dias + 28 dias (4 semanas). A janela de treinamento é de 90 dias e a janela de pesquisa é de 28 dias, totalizando 118 dias.

## Dados de saída do Attribution AI

A IA de atribuição gera o seguinte:

- [Pontuações granulares brutas](#raw-granular-scores)
- [Pontuações agregadas](#aggregated-attribution-scores)

**Exemplo de esquema de saída:**

![](./images/input-output/schema_output.gif)

### Pontuações granulares brutas {#raw-granular-scores}

A IA de atribuição gera pontuações de atribuição no nível mais granular possível, para que você possa cortar e dividir as pontuações por qualquer coluna de pontuação. Para exibir essas pontuações na interface, leia a seção em [exibindo caminhos de pontuação brutos](#raw-score-path). Para baixar as pontuações usando a API, visite o documento [pontuações de download na IA de atribuição](./download-scores.md).

>[!NOTE]
>
>Você poderá ver qualquer coluna de relatório desejada do conjunto de dados de entrada no conjunto de dados de saída da pontuação somente se uma das seguintes opções for verdadeira:
>
>- A coluna de relatório é incluída na página de configuração como parte do ponto de contato ou da configuração de definição de conversão.
>- A coluna de relatório é incluída em colunas adicionais do conjunto de dados de pontuação.

A tabela a seguir descreve os campos de esquema na saída de exemplo de pontuações brutas:

| Nome da coluna (DataType) | Anulável | Descrição |
| --- | --- | --- |
| carimbo de data e hora (DateTime) | Falso | A hora em que um evento de conversão ou observação ocorreu. <br> **Exemplo:** 2020-06-09T00:01:51.000Z |
| identityMap (Mapa) | Verdadeiro | identityMap do usuário semelhante ao formato CEE XDM. |
| eventType (String) | Verdadeiro | O tipo de evento principal para este registro de série temporal. <br> **Exemplo:** &quot;Pedido&quot;, &quot;Compra&quot;, &quot;Visita&quot; |
| eventMergeId (Cadeia de caracteres) | Verdadeiro | Uma ID para correlacionar ou mesclar vários [!DNL Experience Events] que são essencialmente o mesmo evento ou devem ser mesclados. Deve ser preenchido pelo produtor de dados antes da assimilação. <br> **Exemplo:** 575525617716-0-edc2ed37-1aab-4750-a820-1c2b3844b8c4 |
| _id (String) | Falso | Um identificador exclusivo para o evento de série temporal. <br> **Exemplo:** 4461-edc2ed37-1aab-4750-a820-1c2b3844b8c4 |
| _tenantId (Objeto) | Falso | O contêiner de objeto de nível superior correspondente à ID do locatário. <br> **Exemplo:** _atsdsnrmmsv2 |
| your_schema_name (Objeto) | Falso | Pontuar linha com evento de conversão todos os eventos de ponto de contato associados a ele e seus metadados. <br> **Exemplo:** Pontuações da IA de atribuição - Nome do modelo__2020 |
| segmentação (string) | Verdadeiro | Segmento de conversão, como segmentação geográfica, em que o modelo é criado. Na ausência de segmentos, o segmento é o mesmo que conversionName. <br> **Exemplo:** ORDER_US |
| conversionName (String) | Verdadeiro | Nome da conversão configurada durante a instalação. <br> **Exemplo:** Ordem, Cliente Potencial, Visita |
| conversion (Objeto) | Falso | Colunas de metadados de conversão. |
| dataSource (String) | Verdadeiro | Identificação globalmente exclusiva de uma fonte de dados. <br> **Exemplo:** Adobe Analytics |
| eventSource (Cadeia de caracteres) | Verdadeiro | A origem quando o evento real ocorreu. <br> **Exemplo:** Adobe.com |
| eventType (String) | Verdadeiro | O tipo de evento principal para este registro de série temporal. <br> **Exemplo:** Ordem |
| geo (String) | Verdadeiro | A localização geográfica onde a conversão foi entregue `placeContext.geo.countryCode`. <br> **Exemplo:** EUA |
| priceTotal (Duplo) | Verdadeiro | Receita obtida por meio da conversão <br> **Exemplo:** 99.9 |
| produto (String) | Verdadeiro | O identificador XDM do próprio produto. <br> **Exemplo:** RX 1080 ti |
| productType (String) | Verdadeiro | O nome de exibição do produto conforme apresentado ao usuário para esta visualização do produto. <br> **Exemplo:** Gpus |
| quantidade (número inteiro) | Verdadeiro | Quantidade comprada durante a conversão. <br> **Exemplo:** 1 1080 ti |
| receivedTimestamp (DateTime) | Verdadeiro | Carimbo de data/hora da conversão recebido. <br> **Exemplo:** 2020-06-09T00:01:51.000Z |
| skuId (String) | Verdadeiro | Unidade de manutenção de estoque (SKU), o identificador exclusivo de um produto definido pelo fornecedor. <br> **Exemplo:** MJ-03-XS-Preto |
| carimbo de data e hora (DateTime) | Verdadeiro | Carimbo de data e hora da conversão. <br> **Exemplo:** 2020-06-09T00:01:51.000Z |
| passThrough (Objeto) | Verdadeiro | Colunas adicionais do conjunto de dados de Pontuação especificadas pelo usuário ao configurar o modelo. |
| commerce_order_purchaseCity (Cadeia de caracteres) | Verdadeiro | Coluna adicional do conjunto de dados de pontuação. <br> **Exemplo:** cidade: San Jose |
| customerProfile (Objeto) | Falso | Detalhes de identidade do usuário usado para criar o modelo. |
| identity (Objeto) | Falso | Contém os detalhes do usuário usado para criar o modelo, como `id` e `namespace`. |
| id (String) | Verdadeiro | ID de identidade do usuário, como ID de cookie, Adobe Analytics ID (AAID), Experience Cloud ID (ECID, também conhecida como MCID ou como ID de visitante) etc. <br> **Exemplo:** 1734876272540865634688320891369597404 |
| namespace (String) | Verdadeiro | Namespace de identidade usado para criar os caminhos e, portanto, o modelo. <br> **Exemplo:** aaid |
| touchpointsDetail (Matriz de objetos) | Verdadeiro | A lista de detalhes do ponto de contato que leva à conversão ordenada pela ocorrência do ponto de contato ou carimbo de data e hora. |
| touchpointName (String) | Verdadeiro | Nome do ponto de contato configurado durante a configuração. <br> **Exemplo:** PAID_SEARCH_CLICK |
| scores (Objeto) | Verdadeiro | Contribuição do ponto de contato para essa conversão como pontuação. Para obter mais informações sobre as pontuações produzidas nesse objeto, consulte a seção [pontuações de atribuição agregadas](#aggregated-attribution-scores). |
| touchPoint (Objeto) | Verdadeiro | Metadados do ponto de contato. Para obter mais informações sobre as pontuações produzidas nesse objeto, consulte a seção [pontuações agregadas](#aggregated-scores). |

### Exibição de caminhos de pontuação brutos (UI) {#raw-score-path}

Você pode visualizar o caminho para suas pontuações brutas na interface do usuário do. Comece selecionando **[!UICONTROL Schemas]** na interface do Experience Platform e depois procure e selecione seu esquema de pontuações da IA de atribuição na guia **[!UICONTROL Browse]**.

![Escolha seu esquema](./images/input-output/schemas_browse.png)

Em seguida, selecione um campo na janela **[!UICONTROL Structure]** da interface do usuário. A guia **[!UICONTROL Field properties]** é aberta. Dentro de **[!UICONTROL Field properties]** é o campo de caminho que mapeia para suas pontuações brutas.

![Escolher um esquema](./images/input-output/field_properties.png)

### Pontuações de atribuição agregadas {#aggregated-attribution-scores}

As pontuações agregadas podem ser baixadas no formato CSV da interface do usuário do Experience Platform se o intervalo de datas for inferior a 30 dias.

A IA de atribuição aceita duas categorias de pontuações de atribuição: pontuações algorítmicas e baseadas em regras.

A IA de atribuição produz dois tipos diferentes de pontuações algorítmicas, incrementais e influenciadas. Uma pontuação influenciada é a fração da conversão pela qual cada ponto de contato de marketing é responsável. Uma pontuação incremental é a quantidade de impacto marginal causado diretamente pelo ponto de contato de marketing. A principal diferença entre a pontuação incremental e a pontuação influenciada é que a pontuação incremental leva em consideração o efeito da linha de base. Não presume que uma conversão é causada puramente pelos pontos de contato de marketing anteriores.

Este é um exemplo de saída do esquema da IA de atribuição da interface do usuário do Adobe Experience Platform:

![](./images/input-output/schema_screenshot.png)

Consulte a tabela abaixo para obter mais detalhes sobre cada uma dessas pontuações de atribuição:

| Pontuações de atribuição | Descrição |
| ----- | ----------- |
| Influenciado (algorítmico) | A pontuação influenciada é a fração da conversão pela qual cada ponto de contato de marketing é responsável. |
| Incremental (algorítmico) | Pontuação incremental é a quantidade de impacto marginal causado diretamente por um ponto de contato de marketing. |
| Primeiro contato | Pontuação de atribuição baseada em regras que atribui todos os créditos ao ponto de contato inicial em um caminho de conversão. |
| Último contato | Pontuação de atribuição baseada em regras que atribui todo o crédito ao ponto de contato mais próximo da conversão. |
| Linear | Pontuação de atribuição baseada em regras que atribui crédito igual a cada ponto de contato em um caminho de conversão. |
| Forma de U | Pontuação de atribuição baseada em regras que atribui 40% do crédito ao primeiro ponto de contato e 40% do crédito ao último ponto de contato, com os outros pontos de contato dividindo os 20% restantes igualmente. |
| Declínio de tempo | Pontuação de atribuição baseada em regras, em que os pontos de contato mais próximos da conversão recebem mais crédito do que os pontos de contato mais distantes da conversão. |

**Referência de pontuação bruta (pontuações de atribuição)**

A tabela abaixo mapeia as pontuações de atribuição para as pontuações brutas. Se quiser baixar suas pontuações brutas, visite as [pontuações de download na documentação da IA de atribuição](./download-scores.md).

| Pontuações de atribuição | Coluna de referência de pontuação bruta |
| --- | --- |
| Influenciado (algorítmico) | _tenantID.your_schema_name.element.touchpoint.algorithmicInfluenced |
| Incremental (algorítmico) | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.algorithmicInfluenced |
| Primeiro contato | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.firstTouch |
| Último contato | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.lastTouch |
| Linear | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.linear |
| Forma de U | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.uShape |
| Declínio de tempo | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.decayUnits |

### Pontuações agregadas {#aggregated-scores}

As pontuações agregadas podem ser baixadas no formato CSV da interface do usuário do Experience Platform se o intervalo de datas for inferior a 30 dias. Consulte a tabela abaixo para obter mais detalhes sobre cada uma dessas colunas agregadas.

| Nome da coluna | Restrição | Anulável | Descrição |
| --- | --- | --- | --- |
| customer_data (DateTime) | Formato definido pelo usuário e fixo | Falso | Data do Evento do Cliente no formato AAAA-MM-DD. <br> **Exemplo**: 05/2016 |
| mediatouchpoints_date (DateTime) | Formato definido pelo usuário e fixo | Verdadeiro | Data do Ponto de Contato de Mídia no formato AAAA-MM-DD <br> **Exemplo**: 21/04/2017 |
| segmento (String) | Calculado | Falso | Segmento de conversão, como segmentação geográfica, em que o modelo é criado. No caso de ausência de segmentos, o segmento é o mesmo que conversion_scope. <br> **Exemplo**: ORDER_AMER |
| conversion_scope (Cadeia de caracteres) | Definido pelo usuário | Falso | Nome da conversão conforme configurado pelo usuário. <br> **Exemplo**: ORDEM |
| touchpoint_scope (Cadeia de caracteres) | Definido pelo usuário | Verdadeiro | Nome do Touchpoint conforme configurado pelo usuário <br> **Exemplo**: PAID_SEARCH_CLICK |
| produto (String) | Definido pelo usuário | Verdadeiro | O identificador XDM do produto. <br> **Exemplo**: CC |
| product_type (String) | Definido pelo usuário | Verdadeiro | O nome de exibição do produto conforme apresentado ao usuário para esta visualização do produto. <br> **Exemplo**: gpus, laptops |
| geo (String) | Definido pelo usuário | Verdadeiro | A localização geográfica onde a conversão foi entregue (placeContext.geo.countryCode) <br> **Exemplo**: EUA |
| event_type (String) | Definido pelo usuário | Verdadeiro | O tipo de evento primário para este registro de série temporal <br> **Exemplo**: Conversão Paga |
| media_type (String) | ENUM | Falso | Descreve se o tipo de mídia é pago, próprio ou ganho. <br> **Exemplo**: PAGO, PROPRIETÁRIO |
| channel (String) | ENUM | Falso | A propriedade `channel._type` que é usada para fornecer uma classificação aproximada de canais com propriedades semelhantes no XDM [!DNL Consumer Experience Event]. <br> **Exemplo**: SEARCH |
| action (String) | ENUM | Falso | A propriedade `mediaAction` é usada para fornecer um tipo de ação de mídia de evento de experiência. <br> **Exemplo**: CLIQUE |
| campaign_group (String) | Definido pelo usuário | Verdadeiro | Nome do grupo de campanhas onde várias campanhas são agrupadas como &quot;50%_DISCOUNT&quot;. <br> **Exemplo**: COMERCIAL |
| campaign_name (String) | Definido pelo usuário | Verdadeiro | Nome da campanha usado para identificar a campanha de marketing como &quot;50%_DISCOUNT_USA&quot; ou &quot;50%_DISCOUNT_ASIA&quot;. <br> **Exemplo**: Venda de Ação de Graças |

**Referência de Pontuação Bruta (agregada)**

A tabela abaixo mapeia as pontuações agregadas para as pontuações brutas. Se quiser baixar suas pontuações brutas, visite as [pontuações de download na documentação da IA de atribuição](./download-scores.md). Para exibir os caminhos de pontuação brutos na interface do usuário, visite a seção sobre [exibição de caminhos de pontuação brutos](#raw-score-path) neste documento.

| Nome da coluna | Coluna de referência de pontuação bruta |
| --- | --- |
| customer_events | carimbo de data e hora |
| mediatouchpoints_date | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.timestamp |
| segmento | _tenantID.your_schema_name.segmentation |
| conversion_scope | _tenantID.your_schema_name.conversion.conversionName |
| touchpoint_scope | _tenantID.your_schema_name.touchpointsDetail.element.touchpointName |
| produto | _tenantID.your_schema_name.conversion.product |
| product_type | _tenantID.your_schema_name.conversion.product_type |
| geo | _tenantID.your_schema_name.conversion.geo |
| event_type | eventType |
| media_type | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.mediaType |
| channel | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.mediaChannel |
| ação | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.mediaAction |
| campaign_group | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.campaignGroup |
| campaign_name | _tenantID.your_schema_name.touchpointsDetail.element.touchpoint.campaignName |

>[!IMPORTANT]
>
> - A IA de atribuição usa apenas dados atualizados para treinamento adicional e pontuação. Da mesma forma, quando você solicita a exclusão de dados, a IA do cliente evita usar os dados excluídos.
> - A IA de atribuição aproveita os conjuntos de dados do Experience Platform. Para atender às solicitações de direitos do consumidor que uma marca pode receber, as marcas devem usar o Experience Platform Privacy Service para enviar solicitações do consumidor de acesso e exclusão para remover seus dados no data lake, no Serviço de identidade e no Perfil do cliente em tempo real.
> - Todos os conjuntos de dados que usamos para entrada/saída de modelos seguirão as diretrizes da Experience Platform. A Criptografia de dados da Experience Platform se aplica a dados inativos e em trânsito. Consulte a documentação para saber mais sobre [criptografia de dados](../../../help/landing/governance-privacy-security/encryption.md)

## Próximas etapas {#next-steps}

Depois de preparar seus dados e ter todas as credenciais e esquemas em vigor, comece seguindo o [guia do usuário da IA de atribuição](./user-guide.md). Este guia aborda a criação de uma instância da IA de atribuição.
