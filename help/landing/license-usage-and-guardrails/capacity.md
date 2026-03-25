---
title: Uso e capacidade da licença
description: Saiba mais sobre o uso de sua licença e os limites de capacidade no Adobe Experience Platform.
exl-id: 38dad2f1-bd0f-4cc3-a3a6-5105ea866ea4
source-git-commit: 1a7a074a455542bb1438b2cbf199d79229142389
workflow-type: tm+mt
source-wordcount: '2072'
ht-degree: 4%

---


# Uso e capacidades da licença

>[!AVAILABILITY]
>
>Para usar esse recurso, você deve ter as seguintes permissões:
>
>- **Exibir Painel de Uso de Licenças**
>   - Esta permissão possibilita **visualizar** a capacidade inicial.
>- **Gerenciar Sandboxes**
>   - Essa permissão permite **editar** suas alocações de capacidade.
>   - Além disso, você **deve** ter acesso a todas as sandboxes para editar a capacidade da sandbox **qualquer**.
>
>Mais informações sobre permissões no Experience Platform podem ser encontradas na [visão geral do controle de acesso](/help/access-control/home.md#permissions)
>
>Além disso, se você adquiriu a Segmentação de transmissão de alta taxa de transferência, você **não** poderá alocar suas capacidades usando a Capacidade. Para atualizar suas capacidades, entre em contato com o Atendimento ao cliente da Adobe.

No Adobe Experience Platform, as capacidades informam se sua organização excedeu qualquer uma de suas medidas de proteção e fornecem informações sobre como corrigir esses problemas.

Para obter mais informações sobre medidas de proteção no Experience Platform, leia a [visão geral das medidas de proteção do Real-Time CDP](../../rtcdp/guardrails/overview.md).

## Comportamento de capacidade {#behavior}

>[!CONTEXTUALHELP]
>id="platform_capacity_streamingthroughput"
>title="Taxa de transferência de transmissão"
>abstract="O valor da taxa de transferência de transmissão mede o pico combinado de eventos de entrada por segundo para a assimilação de streaming no Perfil, em suas sandboxes de produção e desenvolvimento."

>[!CONTEXTUALHELP]
>id="platform_capacity_streamingaudiences"
>title="Contagem de público-alvo de transmissão"
>abstract="O número máximo de públicos-alvo de transmissão por sandbox. Esse número inclui o número de públicos-alvo de borda que você tem na sandbox."

>[!CONTEXTUALHELP]
>id="platform_capacity_edgeaudiences"
>title="Públicos-alvo de borda"
>abstract="O número máximo de públicos-alvo de borda por sandbox."

Atualmente, o Capacity oferece suporte aos seguintes serviços:

- Segmentação de transmissão
- Assimilação por transmissão
- Segmentação de borda

Nesses serviços, as seguintes medidas de proteção são rastreadas:

- O número máximo de públicos-alvo de transmissão é 500
- O número máximo de públicos-alvo de borda é 150
- A taxa de transferência inicial combinada para assimilação por transmissão é de 1500 registros por segundo (rps)
   - Essa taxa de transferência de transmissão combinada mede o pico combinado de eventos de entrada por segundo para a assimilação de transmissão no Perfil do cliente em tempo real em suas sandboxes de produção e desenvolvimento.
   - Você pode adquirir suporte adicional para segmentação por transmissão de até 13.500 registros por segundo. Mais informações sobre a compra de direitos adicionais podem ser encontradas na [descrição do produto Real-Time CDP](https://helpx.adobe.com/br/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html).
- A taxa de transferência combinada para a segmentação de borda é de 1500 registros por segundo (rps)

A capacidade de público-alvo está no nível de **sandbox**. Isso significa que, para cada sandbox que você tem em sua organização, você pode ter 500 públicos-alvo de transmissão, dos quais 150 podem ser públicos-alvo de borda.

A capacidade de taxa de transferência de transmissão está em um nível de **organização** e pode ser distribuída para suas sandboxes individuais. Por exemplo, com a taxa de transferência de assimilação de 1500 rps para streaming, é possível definir a sandbox de produção como 1300 rps e a sandbox de desenvolvimento como 200 rps.

O Experience Platform calcula a taxa de transferência da sandbox em intervalos contínuos de 15 minutos. Essa taxa de transferência é medida em tempo real, com os dados sendo atualizados a cada 60 segundos.

Se o uso atingir 80% e 90% da capacidade licenciada, a Experience Platform emitirá um alerta, notificando que você está atingindo o máximo da capacidade especificada. Você pode modificar as configurações para personalizar a porcentagem de capacidade para receber o alerta ou remover o alerta totalmente.

Se o uso ultrapassar 100% da capacidade licenciada, você será considerado em violação da capacidade. Se você violar sua capacidade, as seguintes limitações serão aplicadas:

>[!NOTE]
>
>Se você tiver acesso ao Adobe Journey Optimizer, as seguintes limitações **não** serão aplicadas.

- Os dados do evento **podem** ser removidos da personalização de streaming se a fila de processamento de eventos exceder 12 horas
- Os dados removidos do evento **não** serão assimilados no Perfil
   - Você poderá ver quando os eventos foram removidos
   - Os eventos estarão disponíveis no data lake, de acordo com seus direitos
   - Você *pode* usar o Serviço de consulta para assimilar os dados novamente diretamente, se necessário

## Acesso {#access}

Para acessar a visão geral de Capacidade, selecione **[!UICONTROL License usage]** seguido por **[!UICONTROL Capacity]**.

![O método para acessar a seção Capacidade está realçado.](/help/landing/images/capacity/access-capacity.png)

A página Visão geral da capacidade é exibida, mostrando informações, incluindo um histórico de alertas, bem como detalhes sobre as capacidades de sua organização.

![A página Visão geral da Capacidade é exibida, mostrando o histórico de alertas e as seções de detalhes da capacidade.](/help/landing/images/capacity/capacity-overview.png) {zoomable="yes" width="80%"}

### Histórico de alertas {#alert-history}

A seção **[!UICONTROL Alert history]** exibe uma lista das violações de capacidade mais recentes em sua organização.

![A seção Histórico de alertas é exibida.](/help/landing/images/capacity/alert-history.png)

| Nome da coluna | Descrição |
| ----------- | ----------- |
| Sandbox | O nome da sandbox onde ocorreu a violação de capacidade. |
| Alerta | A capacidade que foi violada na sandbox. |
| Carimbo de data e hora | Os dados e a hora em que a violação ocorreu. |

Para exibir um histórico completo dos alertas da sua organização, selecione o ![ícone de três pontos](/help/images/icons/more.png), seguido de **[!UICONTROL View all]**.

![O histórico completo de alertas é exibido para uma organização.](/help/landing/images/capacity/full-alert-history.png)

### Capacidades de transmissão {#streaming-capacities}

A seção Capacidades de transmissão descreve as informações sobre as capacidades de transmissão da organização. Especificamente, esta seção exibe informações de capacidade sobre a taxa de transferência da transmissão e os públicos-alvo da transmissão. Você pode filtrar essas informações por sandbox e alterar o período de pesquisa.

![O seletor de sandbox e o seletor de datas para o período de pesquisa estão realçados.](/help/landing/images/capacity/filter-sandbox-and-date.png)

#### Taxa de transferência de transmissão {#streaming-throughput}

A seção **[!UICONTROL Streaming throughput]** exibe informações sobre a taxa de transferência da transmissão nas sandboxes da organização. O valor da taxa de transferência de transmissão mede o pico combinado de eventos de entrada por segundo para a assimilação de streaming no Perfil.

![A seção de taxa de transferência de streaming na página de detalhes de capacidade é exibida.](/help/landing/images/capacity/streaming-throughput-section.png)

| Nome da coluna | Descrição |
| ----------- | ----------- |
| Sandbox | O nome da sandbox. |
| Serviços | O serviço usado pela sandbox. No momento, o único valor compatível é Perfil. |
| Uso (Pico) | O pico de taxa de transferência de transmissão de dados na sandbox dentro do período de pesquisa selecionado. |
| Capacidade | A taxa de transferência máxima de transmissão para a sandbox. |
| Violação | Se uma violação tiver ocorrido, o tipo de violação para a taxa de transferência de transmissão. |
| Ações recomendadas | Uma coluna que descreve a ação recomendada para atenuar a violação. |

Você pode selecionar a sandbox individual para ver uma visualização mais detalhada da taxa de transferência de transmissão da sandbox.

![Uma sandbox está realçada na seção de taxa de transferência de streaming.](/help/landing/images/capacity/select-sandbox.png)

A página de detalhes da Taxa de transferência de transmissão é exibida. Você pode ver um gráfico que exibe a taxa de transferência da solicitação comparada ao limite de capacidade, uma lista das sandboxes e suas taxas de transferência, bem como um botão para alocar as capacidades de sua organização.

![A página de taxa de transferência de streaming é exibida, mostrando informações detalhadas sobre a taxa de transferência de streaming da sandbox selecionada.](/help/landing/images/capacity/streaming-capacity-allocation.png)

Para atualizar as capacidades de taxa de transferência de streaming da organização, selecione **[!UICONTROL Allocate capacities]**.

![O botão Alocar capacidades está realçado na página de detalhes da taxa de transferência de streaming.](/help/landing/images/capacity/select-allocate.png)

A página de alocação é exibida. Nesta página, você pode definir suas capacidades para diferentes sandboxes. A soma de todas as capacidades **deve** ser igual ao total de capacidade da organização.

![A página de alocação de capacidade é exibida.](/help/landing/images/capacity/allocate-capacity.png)

>[!NOTE]
>
>Você só pode definir a nova capacidade nas ordens de **100**. Por exemplo, você pode definir o valor da nova capacidade da sandbox como 300 ou 500, mas **não pode** definir esse valor como 450.
>
>Se o valor não for da ordem de 100, ele será arredondado para cima ou para baixo de acordo.

Depois de atualizar as alocações de capacidade, selecione **[!UICONTROL Save]** para concluir as atualizações. Observe que pode levar até 10 minutos para que as alterações sejam refletidas em sua organização.

#### Contagem de público-alvo de transmissão {#streaming-audience-count}

A seção **[!UICONTROL Streaming audience count]** exibe o número de públicos de transmissão dentro da sandbox, bem como o número máximo de públicos de transmissão permitidos dentro da sandbox.

![As seções de Contagem de público-alvo são exibidas.](/help/landing/images/capacity/audience-count.png)

| Nome da coluna | Descrição |
| ----------- | ----------- |
| Sandbox | O nome da sandbox. |
| Serviços | O serviço que está em uso para a sandbox. |
| Uso | O número de públicos-alvo de transmissão que estão na sandbox. |
| Capacidade | O número máximo de públicos-alvo de transmissão permitidos na sandbox. |

### Capacidades do Edge {#edge-capacities}

A seção **[!UICONTROL Edge capacities]** descreve as informações sobre as capacidades de borda da sua organização. Especificamente, esta seção exibe informações de capacidade sobre a taxa de transferência da segmentação de borda e os públicos-alvo de borda. Você pode alterar o período de lookback para as capacidades de borda da organização.

![A seção Capacidades do Edge é exibida. Isso descreve informações, incluindo a taxa de transferência de segmentação de borda e o contagem de público-alvo de borda.](/help/landing/images/capacity/edge-capacities.png)

#### Taxa de transferência de segmentação de borda {#edge-streaming-throughput}

A seção **[!UICONTROL Edge segmentation throughput]** exibe informações sobre a taxa de transferência da segmentação de borda nas sandboxes da sua organização e da organização. O valor da taxa de transferência de segmentação de borda mede o pico combinado de eventos de entrada por segundo para a assimilação de borda no Perfil.

![A seção Taxa de transferência da segmentação do Edge é exibida. Isso mostra informações sobre a taxa de transferência da segmentação de borda em sua organização e suas sandboxes.](/help/landing/images/capacity/edge-segmentation-throughput.png)

| Nome da coluna | Descrição |
| ----------- | ----------- |
| Organização | O nome da organização. As sandboxes disponíveis para a organização estão listadas no nome da organização. |
| Uso do RPS (Pico) | A taxa de transferência máxima de dados na sandbox dentro do período de pesquisa selecionado. |
| RPS de capacidade | A taxa de transferência máxima da organização. |
| Violação | Se uma violação tiver ocorrido, o tipo de violação para a taxa de transferência de segmentação de borda. |
| Ações recomendadas | Uma coluna que descreve a ação recomendada para atenuar a violação. |

É possível selecionar a organização para ver uma visualização mais detalhada da taxa de transferência da segmentação de borda da organização.

![A organização está realçada.](/help/landing/images/capacity/select-organization.png)

A página **[!UICONTROL Edge Segmentation Throughput]** é exibida. Você pode ver um gráfico que exibe a taxa de transferência da solicitação comparada ao limite de capacidade. Nessa página, é possível ajustar o período de lookback para o gráfico exibido.

![A página Taxa de transferência da segmentação do Edge é exibida. Isso mostra um gráfico detalhando a taxa de transferência comparada ao limite de capacidade.](/help/landing/images/capacity/edge-segmentation-throughput-details.png)

#### Contagem de públicos-alvo na borda {#edge-audience-count}

A seção **[!UICONTROL Edge audience count]** exibe o número de públicos-alvo de borda em cada sandbox, bem como o número máximo de públicos-alvo de borda permitidos na sandbox.

![A seção contagem de público-alvo do Edge é exibida. Isso mostra informações relacionadas ao contagem de público-alvo de borda.](/help/landing/images/capacity/edge-audience-count.png)

| Nome da coluna | Descrição |
| ----------- | ----------- |
| Sandbox | O nome da sandbox. |
| Serviços | O serviço que está em uso para a sandbox. |
| Uso | O número de públicos do tipo listado que estão na sandbox. |
| Capacidade | O número máximo de públicos-alvo do tipo listado que são permitidos na sandbox. |

## Práticas recomendadas de taxa de transferência de transmissão {#streaming-throughput-suggestions}

Você pode resolver as violações de taxa de transferência adotando uma das seguintes recomendações:

1. Aumente a capacidade alocada para a sandbox.
2. Identifique fluxos de dados de alta taxa de transferência no [painel de monitoramento](/help/dataflows/ui/monitor-streaming-profile.md) e aplique limitação ou filtragem a esses fluxos de dados, se necessário.
3. Otimize sua assimilação usando a assimilação em lote para casos de uso de latência mais baixa.

Além disso, você pode examinar seus fluxos de dados e ver se pode otimizar sua estratégia de dados.

| Fator de contribuição | O que é | Impacto nos casos de uso | Práticas recomendadas |
| --- | --- | --- | --- |
| Conversão em lote para fluxo contínuo | As cargas de trabalho em lote convertidas em fluxo podem aumentar significativamente a taxa de transferência, afetando o desempenho e a alocação de recursos. Por exemplo, executar uma atualização de perfil em massa após um evento sem limites de taxa. | As estratégias de transmissão são desnecessárias para casos de uso em lote quando o processamento de baixa latência não é necessário. | Avaliar os requisitos de caso de uso. Para marketing de saída em lote, considere usar a [assimilação em lote](/help/ingestion/batch-ingestion/overview.md) em vez da transmissão para gerenciar a assimilação de dados com mais eficiência. |
| Assimilação desnecessária de dados | A ingestão de dados não é necessária para personalização e aumenta a taxa de transferência sem adicionar valor, desperdiçando recursos. Por exemplo, assimilar todo o tráfego de análises em perfis, independentemente da relevância. | O excesso de dados não relevantes cria ruído, dificultando a identificação de pontos de dados impactantes. Também pode causar atrito ao definir e gerenciar públicos e perfis. | Assimile somente dados necessários para seus casos de uso. Filtre os dados desnecessários.<ul><li>**Adobe Analytics**: use a [filtragem em nível de linha](/help/sources/tutorials/ui/create/adobe-applications/analytics.md#filtering-for-real-time-customer-profile) para otimizar a entrada de dados.</li><li>**Fontes**: Use a [[!DNL Flow Service] API para filtrar dados de nível de linha](/help/sources/tutorials/api/filter.md) de fontes com suporte, como [!DNL Snowflake] e [!DNL Google BigQuery].</li></li>**Sequência de dados do Edge**: configure [sequências de dados dinâmicas](/help/datastreams/configure-dynamic-datastream.md) para executar a filtragem em nível de linha do tráfego proveniente do SDK da Web.</li></ul> |

## Práticas recomendadas de taxa de transferência de segmentação do Edge {#edge-best-practices}

Você pode resolver as violações de taxa de transferência de segmentação de borda adotando uma das seguintes recomendações:

1. Identifique sequências de dados de alta taxa de transferência no [painel de monitoramento](/help/dataflows/ui/monitor-edge.md) e aplique limitação ou filtragem a essas sequências de dados, se necessário.
2. Otimize sua assimilação usando a assimilação em lote para casos de uso de latência mais baixa.
3. Entre em contato com o representante do Atendimento ao cliente da Adobe se os problemas persistirem.

## Visão geral do vídeo {#video}

O vídeo a seguir fornece uma visão geral da Capacidade.

>[!VIDEO](https://video.tv.adobe.com/v/3475272/?learn=on&enablevpops)

## Perguntas frequentes {#faq}

A seção a seguir descreve as perguntas mais frequentes sobre os recursos da capacidade.

### Posso ter um limite máximo de rendimento combinado que soma até menos do que o máximo do meu público-alvo?

+++ Resposta

Não. O limite máximo de produtividade combinada **deve** somar até a proteção de sua organização.

+++

### O que acontece se eu exceder minhas capacidades máximas?

+++ Resposta

Isso depende de qual capacidade é excedida.

Atualmente, se você exceder o número máximo de públicos-alvo permitidos, seu número excessivo de públicos-alvo não será afetado. No entanto, a capacidade de criar novos públicos-alvo pode ser restrita no futuro.

Se você exceder a taxa de transferência de transmissão, haverá latência de desempenho na assimilação e segmentação.

+++

### Por que devo aderir às minhas capacidades máximas?

+++ Resposta

Trabalhar com o máximo de suas capacidades garante que seus dados permaneçam consistentes e mantenha a integridade dos dados intacta.

Você garante um desempenho consistente durante os eventos de pico, evitando problemas técnicos que poderiam afetar negativamente o desempenho do sistema e afetar suas experiências de clientes downstream, melhorando, em última análise, a higiene dos dados e o desempenho geral do sistema.

+++

### Quais são as práticas recomendadas para gerenciar a taxa de transferência de assimilação por transmissão?

+++ Resposta

Para gerenciar melhor a taxa de transferência de assimilação de streaming, você deve avaliar seus conjuntos de dados para garantir que eles estejam priorizando os dados necessários para personalização.


Se o processamento em tempo real não for necessário, você deverá usar a assimilação em lote em vez da assimilação por transmissão.

+++
