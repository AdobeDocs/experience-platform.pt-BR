---
title: Grupo de campos de esquema de detalhes do Advertising
description: Saiba mais sobre o grupo de campos de esquema Detalhes do Advertising.
exl-id: 25de09bd-eedd-489c-9cd5-8acd0c52ddbe
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '992'
ht-degree: 27%

---

# [!UICONTROL Detalhes do Advertising] grupo de campos de esquema

[!UICONTROL Detalhes do Advertising] é um grupo de campos de esquema padrão para a [[!DNL XDM ExperienceEvent] classe](../../classes/experienceevent.md). O grupo de campos fornece um único objeto `advertising` para um esquema, que captura informações relacionadas a impressões de publicidade, click-throughs e atribuição.

![Estrutura do grupo de campos](../../images/field-groups/advertising-details/structure.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `adAssetReference` | Objeto | Registra informações de ativos sobre o anúncio. Consulte a [subseção abaixo](#adAssetReference) para obter mais informações sobre a estrutura desse objeto. |
| `adAssetViewDetails` | Objeto | Captura os detalhes de exibição para a reprodução de anúncio. Consulte a [subseção abaixo](#adAssetViewDetails) para obter mais informações sobre a estrutura desse objeto. |
| `adViewability` | Objeto | Registra o número de impressões vistas pelos usuários finais, como volume do player, versão da biblioteca, status da janela e dimensões do visor do anúncio. Consulte a [subseção abaixo](#adViewability) para obter mais informações sobre a estrutura desse objeto. |
| `clicks` | [[!UICONTROL Medida]](../../data-types/measure.md) | O número de ações de clique no anúncio. |
| `completes` | [[!UICONTROL Medida]](../../data-types/measure.md) | O número de vezes que um ativo de mídia cronometrado foi assistido até o fim. Isso não significa necessariamente que o usuário final assistiu ao vídeo inteiro, pois ele pode ter pulado. |
| `conversions` | [[!UICONTROL Medida]](../../data-types/measure.md) | O número de vezes que uma ação ou ações predefinidas acionaram um evento para avaliação de desempenho. |
| `federated` | [[!UICONTROL Medida]](../../data-types/measure.md) | Indica se um evento de experiência foi criado por meio de federação de dados, como compartilhamento de dados entre clientes. |
| `firstQuartiles` | [[!UICONTROL Medida]](../../data-types/measure.md) | O número de vezes que um anúncio de vídeo digital foi reproduzido até 25% de sua duração na velocidade normal. |
| `impressions` | [[!UICONTROL Medida]](../../data-types/measure.md) | O número de impressões de anúncios enviadas a um usuário final com potencial para serem visualizadas. |
| `midpoints` | [[!UICONTROL Medida]](../../data-types/measure.md) | O número de vezes que um anúncio de vídeo digital foi reproduzido até 50% de sua duração na velocidade normal. |
| `starts` | [[!UICONTROL Medida]](../../data-types/measure.md) | O número de vezes que um anúncio de vídeo digital iniciou a reprodução. |
| `thirdQuartiles` | [[!UICONTROL Medida]](../../data-types/measure.md) | O número de vezes que um anúncio de vídeo digital foi reproduzido até 75% de sua duração na velocidade normal. |
| `timePlayed` | [[!UICONTROL Medida]](../../data-types/measure.md) | A quantidade de tempo gasto por um usuário final em um ativo de mídia temporizado específico. |
| `downloadedPlayback` | Booleano | Quando definido como `true`, indica que a ocorrência é gerada devido à reprodução de uma sessão de anúncio baixado. |

{style="table-layout:auto"}

## `adAssetReference` {#adAssetReference}

O objeto `adAssetReference` captura informações de ativo sobre o anúncio.

![estrutura adAssetReference](../../images/field-groups/advertising-details/adAssetReference.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `_dc.title` | String | O nome amigável e legível do recurso do anúncio. |
| `_xmpDM.duration` | Número inteiro | O comprimento ou a duração do ativo em segundos. |
| `_id` | String | Um identificador exclusivo do ativo de anúncio, seguindo o [padrão de Ad-ID](https://datatracker.ietf.org/doc/html/rfc8107). |
| `advertiser` | String | A empresa ou marca cujo produto é apresentado no anúncio. |
| `campaign` | String | A ID da campanha publicitária. |
| `creativeID` | String | A ID do criativo do anúncio. |
| `creativeURL` | String | A URL do criativo do anúncio. |
| `placementID` | String | A ID de posicionamento do anúncio. |
| `siteID` | String | A ID do site do anúncio. |

{style="table-layout:auto"}

## `adAssetViewDetails` {#adAssetViewDetails}

O objeto `adAssetViewDetails` captura os detalhes de exibição da reprodução de anúncio.

![estrutura adAssetViewDetails](../../images/field-groups/advertising-details/adAssetViewDetails.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `adBreak` | [[!UICONTROL Intervalo comercial]](../../data-types/ad-break.md) | Descreve como um anúncio cronometrado é inserido na mídia cronometrada. |
| `index` | Número inteiro | O índice do anúncio dentro do ad break principal. Por exemplo, o primeiro anúncio tem índice `0` e o segundo anúncio tem índice `1`. |
| `playerName` | String | O nome do player responsável por renderizar o anúncio. |

{style="table-layout:auto"}

## `adViewability` {#adViewability}

O objeto `adViewability` captura o número de impressões vistas pelos usuários finais, como o volume do player, a versão da biblioteca, o status da janela e as dimensões do visor do anúncio.

![Estrutura adViewability](../../images/field-groups/advertising-details/adViewability.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `implementationDetails` | [[!UICONTROL Detalhes da implementação]](../../data-types/implementation-details.md) | O nome e a versão da biblioteca instrumentada para medir as métricas de visibilidade. |
| `measuredAdNotVisible` | [[!UICONTROL Medida]](../../data-types/measure.md) | Indica que o anúncio não está visível, conforme medido por uma biblioteca de visibilidade no momento da impressão. |
| `measuredMuted` | [[!UICONTROL Medida]](../../data-types/measure.md) | Indica que o anúncio está sem áudio, conforme medido por uma biblioteca de visibilidade no momento da impressão. |
| `unmeasurableIframe` | [[!UICONTROL Medida]](../../data-types/measure.md) | Indica que o anúncio é exibido em uma janela inativa medida por uma biblioteca de visibilidade no momento da impressão. |
| `unmeasurableOther` | [[!UICONTROL Medida]](../../data-types/measure.md) | Indica que a biblioteca de visibilidade não pode executar as medições corretamente porque o anúncio está sendo exibido dentro de um iframe. |
| `viewabilityEligibleImpressions` | [[!UICONTROL Medida]](../../data-types/measure.md) | Impressões de um anúncio para um usuário final com biblioteca de visibilidade instrumentada. |
| `viewabilityCompletes` | [[!UICONTROL Medida]](../../data-types/measure.md) | Conclusões de um anúncio para um usuário final considerado visível no momento da conclusão por uma biblioteca de visibilidade. |
| `viewableFirstQuartiles` | [[!UICONTROL Medida]](../../data-types/measure.md) | Primeiro quartil de um anúncio para um usuário final considerado visível no primeiro quartil de reprodução por uma biblioteca de visibilidade. |
| `viewableImpressions` | [[!UICONTROL Medida]](../../data-types/measure.md) | Impressões de um anúncio para um usuário final consideradas visíveis após dois segundos de reprodução por uma biblioteca de visibilidade. |
| `viewableMidpoints` | [[!UICONTROL Medida]](../../data-types/measure.md) | Pontos intermediários de um anúncio para um usuário final considerado visível no ponto intermediário de uma biblioteca de visibilidade. |
| `viewableThirdQuartiles` | [[!UICONTROL Medida]](../../data-types/measure.md) | Terceiro quartil de um anúncio para um usuário final considerado visível no terceiro quartil de reprodução por uma biblioteca de visibilidade. |
| `activeWindow` | Booleano | Indica se o anúncio foi mostrado na janela ativa do dispositivo do usuário. |
| `adHeight` | Número inteiro | O número de pixels verticais do player, medido em tempo de execução. Pode ser maior do que o tamanho do anúncio se o player tiver controles extras ou miniaturas. |
| `adUnitDepth` | Número inteiro | Os editores podem incorporar blocos de anúncios dentro de containers (iFrames) para limitar o acesso do anúncio apenas ao código da página. Esse valor descreve em quantos contêineres a unidade de anúncio é exibida. |
| `adWidth` | Número inteiro | O número de pixels horizontais do player, medido em tempo de execução. Pode ser maior do que o tamanho do anúncio se o player tiver controles extras ou miniaturas. |
| `measurementEligible` | Booleano | Se o anúncio era ou não qualificado para medição de visibilidade. Um anúncio é elegível se a unidade tiver um formato de criativo e tipo de tag compatíveis. |
| `percentViewable` | Número inteiro | A porcentagem de pixels no anúncio considerados visíveis no momento da medição. |
| `playerVolume` | Número inteiro | A porcentagem de volume do player, conforme medida em tempo de execução, em que `0` está sem áudio e `100` é o volume máximo. |
| `viewable` | Booleano | Indica se o anúncio estava visível no tempo de execução. Os anúncios gráficos são considerados visíveis quando pelo menos 50% do anúncio fica visível por pelo menos um segundo. Os anúncios de vídeo são considerados visíveis quando pelo menos 50% do anúncio fica visível enquanto o vídeo é reproduzido por pelo menos dois segundos consecutivos. |
| `viewportHeight` | Número inteiro | O tamanho vertical (em pixels) da janela em que a experiência foi exibida medido no tempo de execução. Para um evento de visualização da web, esse valor indica a altura da janela de visualização do navegador. |
| `viewportWidth` | Número inteiro | O tamanho horizontal (em pixels) da janela em que a experiência foi exibida medido no tempo de execução. Para um evento de visualização da web, esse valor indica a largura da janela de visualização do navegador. |

{style="table-layout:auto"}

Para obter mais detalhes sobre o grupo de campos, consulte o [repositório XDM público](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-advertising.schema.json).
