---
title: Grupo de campos do esquema Detalhes da publicidade
description: Este documento fornece uma visão geral do grupo de campos Detalhes de publicidade .
source-git-commit: 77fb3e348c2298fc5c325fcf2d3408da084b2b19
workflow-type: tm+mt
source-wordcount: '1016'
ht-degree: 11%

---

# [!UICONTROL Detalhes da publicidade] grupo de campos de esquema

[!UICONTROL Detalhes da publicidade] é um grupo de campos de esquema padrão para a variável [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md). O grupo de campos fornece um único `advertising` objeto de um esquema, que captura informações relacionadas a impressões de anúncios, cliques e atribuição.

![Estrutura do grupo de campos](../../images/field-groups/advertising-details/structure.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `adAssetReference` | Objeto | Captura informações do ativo sobre o anúncio. Consulte a [subseção abaixo](#adAssetReference) para obter mais informações sobre a estrutura deste objeto. |
| `adAssetViewDetails` | Objeto | Captura detalhes de exibição para a reprodução do anúncio. Consulte a [subseção abaixo](#adAssetViewDetails) para obter mais informações sobre a estrutura deste objeto. |
| `adViewability` | Objeto | Captura o número de impressões vistas por usuários finais, como volume do reprodutor, versão da biblioteca, status da janela e dimensões do visor de anúncio. Consulte a [subseção abaixo](#adViewability) para obter mais informações sobre a estrutura deste objeto. |
| `clicks` | [[!UICONTROL Medição]](../../data-types/measure.md) | O número de ações de clique no anúncio. |
| `completes` | [[!UICONTROL Medição]](../../data-types/measure.md) | O número de vezes que um ativo de mídia cronometrado foi observado até a conclusão. Isso não significa necessariamente que o usuário final assistiu a todo o vídeo, pois ele pode ter avançado. |
| `conversions` | [[!UICONTROL Medição]](../../data-types/measure.md) | O número de vezes que uma ação (ou ações) predefinida acionou um evento para avaliação de desempenho. |
| `federated` | [[!UICONTROL Medição]](../../data-types/measure.md) | Indica se um evento de experiência foi criado por meio da federação de dados, como o compartilhamento de dados entre clientes. |
| `firstQuartiles` | [[!UICONTROL Medição]](../../data-types/measure.md) | O número de vezes que um anúncio de vídeo digital foi reproduzido em 25% de sua duração em velocidade normal. |
| `impressions` | [[!UICONTROL Medição]](../../data-types/measure.md) | O número de impressões de anúncios enviadas a um usuário final com o potencial de serem visualizadas. |
| `midpoints` | [[!UICONTROL Medição]](../../data-types/measure.md) | O número de vezes que um anúncio de vídeo digital foi reproduzido em 50% de sua duração em velocidade normal. |
| `starts` | [[!UICONTROL Medição]](../../data-types/measure.md) | O número de vezes que um anúncio de vídeo digital foi reproduzido. |
| `thirdQuartiles` | [[!UICONTROL Medição]](../../data-types/measure.md) | O número de vezes que um anúncio de vídeo digital foi reproduzido em 75% de sua duração em velocidade normal. |
| `timePlayed` | [[!UICONTROL Medição]](../../data-types/measure.md) | O tempo gasto por um usuário final em um ativo de mídia programado específico. |
| `downloadedPlayback` | Booleano | Quando definido como `true`, indica que a ocorrência foi gerada devido à reprodução de uma sessão de anúncio baixada. |

{style=&quot;table-layout:auto&quot;}

## `adAssetReference` {#adAssetReference}

O `adAssetReference` captura informações do ativo sobre o anúncio.

![Estrutura adAssetReference](../../images/field-groups/advertising-details/adAssetReference.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `_dc.title` | String | O nome amigável e legível do ativo de anúncio. |
| `_xmpDM.duration` | Número inteiro | A duração do ativo em segundos. |
| `_id` | String | Um identificador exclusivo do ativo de anúncio, seguindo a [Padrão de ID do anúncio](https://datatracker.ietf.org/doc/html/rfc8107). |
| `advertiser` | String | A empresa ou marca cujo produto aparece no anúncio. |
| `campaign` | String | A ID da campanha publicitária. |
| `creativeID` | String | A ID de criação do anúncio. |
| `creativeURL` | String | O URL da arte do anúncio. |
| `placementID` | String | A ID de posicionamento do anúncio. |
| `siteID` | String | A ID do site do anúncio. |

{style=&quot;table-layout:auto&quot;}

## `adAssetViewDetails` {#adAssetViewDetails}

O `adAssetViewDetails` captura os detalhes da exibição para a reprodução do anúncio.

![estrutura adAssetViewDetails](../../images/field-groups/advertising-details/adAssetViewDetails.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `adBreak` | [[!UICONTROL Pausa do anúncio]](../../data-types/ad-break.md) | Descreve como um anúncio programado é inserido em mídia programada. |
| `index` | Número inteiro | O índice do anúncio dentro do ad break principal. Por exemplo, o primeiro anúncio tem índice `0` e o segundo anúncio tem índice `1`. |
| `playerName` | String | O nome do reprodutor responsável pela renderização do anúncio. |

{style=&quot;table-layout:auto&quot;}

## `adViewability` {#adViewability}

O `adViewability` captura o número de impressões vistas por usuários finais, como volume do reprodutor, versão da biblioteca, status da janela e dimensões do visor de anúncio.

![Estrutura de adViewability](../../images/field-groups/advertising-details/adViewability.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `implementationDetails` | [[!UICONTROL Detalhes da implementação]](../../data-types/implementation-details.md) | O nome e a versão da biblioteca instrumentada para medir métricas de visualização. |
| `measuredAdNotVisible` | [[!UICONTROL Medição]](../../data-types/measure.md) | Indica que o anúncio não está visível, conforme medido por uma biblioteca de visualização no momento da impressão. |
| `measuredMuted` | [[!UICONTROL Medição]](../../data-types/measure.md) | Indica que o anúncio está emudecido, medido por uma biblioteca de visualização no momento da impressão. |
| `unmeasurableIframe` | [[!UICONTROL Medição]](../../data-types/measure.md) | Indica que o anúncio é exibido em uma janela inativa, medida por uma biblioteca de visualização no momento da impressão. |
| `unmeasurableOther` | [[!UICONTROL Medição]](../../data-types/measure.md) | Indica que a biblioteca de visualização não é capaz de executar corretamente as medidas devido ao anúncio ser exibido dentro de um iframe. |
| `viewabilityEligibleImpressions` | [[!UICONTROL Medição]](../../data-types/measure.md) | Impressão(ões) de um anúncio para um usuário final com biblioteca de visibilidade instrumentada. |
| `viewabilityCompletes` | [[!UICONTROL Medição]](../../data-types/measure.md) | Conclusão(ões) de um anúncio para um usuário final considerado visível no momento da conclusão por uma biblioteca de visualização. |
| `viewableFirstQuartiles` | [[!UICONTROL Medição]](../../data-types/measure.md) | Primeiro(s) quartil(s) de um anúncio para um usuário final considerado visível no primeiro quartil de reprodução por uma biblioteca de visualização. |
| `viewableImpressions` | [[!UICONTROL Medição]](../../data-types/measure.md) | Impressões de um anúncio para um usuário final consideradas visualizáveis após dois segundos de reprodução por uma biblioteca de visualização. |
| `viewableMidpoints` | [[!UICONTROL Medição]](../../data-types/measure.md) | Ponto(s) médio(is) de um anúncio para um usuário final considerado(s) visível(s) no meio de uma biblioteca de visualização. |
| `viewableThirdQuartiles` | [[!UICONTROL Medição]](../../data-types/measure.md) | Terceiro(s) quartil(s) de um anúncio para um usuário final considerado visível em um terceiro quartil de reprodução por uma biblioteca de visualização. |
| `activeWindow` | Booleano | Indica se o anúncio foi exibido na janela ativa do dispositivo do usuário. |
| `adHeight` | Número inteiro | O número de pixels verticais do reprodutor, medidos no tempo de execução. Isso pode ser maior que o tamanho do anúncio se o reprodutor tiver controles ou miniaturas adicionais. |
| `adUnitDepth` | Número inteiro | Os editores podem incorporar unidades de anúncio em contêineres (iFrames) para limitar o acesso do anúncio apenas ao código da página. Este valor descreve quantos contêineres a unidade de anúncio é exibida no. |
| `adWidth` | Número inteiro | O número de pixels horizontais do reprodutor, medidos no tempo de execução. Isso pode ser maior que o tamanho do anúncio se o reprodutor tiver controles ou miniaturas adicionais. |
| `measurementEligible` | Booleano | Se o anúncio estava ou não qualificado para a avaliação da capacidade de visualização. Um anúncio é elegível se a unidade tiver um formato criativo e tipo de tag aceitos. |
| `percentViewable` | Número inteiro | A porcentagem de pixels no anúncio considerado visível no momento da medição. |
| `playerVolume` | Número inteiro | A porcentagem do volume do reprodutor conforme medido no tempo de execução, em que `0` é mudo e `100` é o volume máximo. |
| `viewable` | Booleano | Indica se o anúncio estava visível no tempo de execução. Anúncios são considerados visualizáveis quando pelo menos 50% do anúncio estiver visível por pelo menos um segundo. Anúncios de vídeo são considerados visualizáveis quando pelo menos 50% do anúncio estiver visível enquanto o vídeo estiver sendo reproduzido por pelo menos dois segundos consecutivos. |
| `viewportHeight` | Número inteiro | O tamanho vertical (em pixels) da janela em que a experiência foi exibida foi medida no tempo de execução. Para um evento de exibição da Web, esse valor indica a altura da janela de visualização do navegador. |
| `viewportWidth` | Número inteiro | O tamanho horizontal (em pixels) da janela em que a experiência foi exibida foi medida no tempo de execução. Para um evento de exibição da Web, esse valor indica a largura da janela de visualização do navegador. |

{style=&quot;table-layout:auto&quot;}

Para obter mais detalhes sobre o grupo de campos, consulte [repositório XDM público](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-advertising.schema.json).
