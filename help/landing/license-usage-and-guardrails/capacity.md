---
title: Uso e capacidade da licença
description: Saiba mais sobre o uso de sua licença e os limites de capacidade no Adobe Experience Platform.
exl-id: 38dad2f1-bd0f-4cc3-a3a6-5105ea866ea4
source-git-commit: 5520e449b4cbe45eb9664ce3c913dd5d544e088c
workflow-type: tm+mt
source-wordcount: '1603'
ht-degree: 6%

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
>abstract="O valor da taxa de transferência de transmissão mede o pico combinado de eventos de entrada por segundo para ingestão de transmissão no serviço de perfil, em suas sandboxes de produção e desenvolvimento."

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

Nesses serviços, as seguintes medidas de proteção são rastreadas:

- O número máximo de públicos-alvo de transmissão é 500
   - Desses 500 públicos-alvo de transmissão, o número máximo de públicos-alvo de borda é 150
- A taxa de transferência inicial combinada para assimilação por transmissão é de 1500 registros por segundo (rps)
   - Essa taxa de transferência de transmissão combinada mede o pico combinado de eventos de entrada por segundo para a assimilação de transmissão no Perfil do cliente em tempo real em suas sandboxes de produção e desenvolvimento.
   - Você pode adquirir suporte adicional para segmentação por transmissão de até 13.500 registros por segundo. Mais informações sobre a compra de direitos adicionais podem ser encontradas na [descrição do produto Real-Time CDP](https://helpx.adobe.com/br/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html).

A capacidade de público-alvo está no nível de **sandbox**. Isso significa que, para cada sandbox que você tem em sua organização, você pode ter 500 públicos-alvo de transmissão, dos quais 150 podem ser públicos-alvo de borda.

A capacidade de taxa de transferência de transmissão está em um nível de **organização** e pode ser distribuída para suas sandboxes individuais. Por exemplo, com a taxa de transferência de assimilação de 1500 rps para streaming, é possível definir a sandbox de produção como 1300 rps e a sandbox de desenvolvimento como 200 rps.

O Experience Platform calcula a taxa de transferência da sandbox em intervalos contínuos de 15 minutos. Essa taxa de transferência é medida em tempo real, com os dados sendo atualizados a cada 60 segundos.

Se o uso atingir 80% e 90% da capacidade licenciada, a Experience Platform emitirá um alerta, notificando que você está atingindo o máximo da capacidade especificada. Você pode modificar as configurações para personalizar a porcentagem de capacidade para receber o alerta ou remover o alerta totalmente.

Se o uso ultrapassar 100% da capacidade licenciada, você será considerado em violação da capacidade. Neste ponto, haverá latência de desempenho, e seus destinos de nível de serviço (SLTs) **não** serão garantidos.

## Acesso {#access}

Para acessar a visão geral de Capacidade, selecione **[!UICONTROL License usage]** seguido por **[!UICONTROL Capacity]**.

![O método para acessar a seção Capacidade está realçado.](/help/landing/images/capacity/access-capacity.png)

A página Visão geral da capacidade é exibida, mostrando informações, incluindo um histórico de alertas, bem como detalhes sobre as capacidades de sua organização.

![A página Visão geral da capacidade é exibida na íntegra, mostrando o histórico de alertas e as seções de detalhes da capacidade.](/help/landing/images/capacity/capacity-overview.png) {zoomable="yes" width="80%"}

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

### Detalhes da capacidade {#capacity-details}

A seção Detalhes da capacidade descreve as informações sobre as capacidades da organização. Nesta seção, você pode filtrar por sandbox e alterar o período de pesquisa.

![O seletor de sandbox e o seletor de datas para o período de pesquisa estão realçados.](/help/landing/images/capacity/filter-sandbox-and-date.png)

Atualmente, exibe informações de capacidade sobre taxa de transferência de transmissão, públicos-alvo de transmissão e públicos-alvo de borda.

#### Taxa de transferência de transmissão {#streaming-throughput}

A seção taxa de transferência de transmissão exibe informações sobre a taxa de transferência de transmissão nas sandboxes da organização. O valor da taxa de transferência de transmissão mede o pico combinado de eventos de entrada por segundo para a assimilação de transmissão no serviço de perfil.

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

#### Contagem de público-alvo {#audience-count}

As seções **[!UICONTROL Streaming audience count]** e **[!UICONTROL Edge audience count]** exibem o número de públicos de streaming e borda na sandbox, bem como o número máximo de públicos de streaming e borda permitidos na sandbox.

![As seções de contagem de público-alvo são exibidas.](/help/landing/images/capacity/audience-count.png)

| Nome da coluna | Descrição |
| ----------- | ----------- |
| Sandbox | O nome da sandbox. |
| Serviços | O serviço que está em uso para a sandbox. |
| Uso | O número de públicos do tipo listado que estão na sandbox. |
| Capacidade | O número máximo de públicos-alvo do tipo listado que são permitidos na sandbox. |

## Práticas recomendadas de taxa de transferência de transmissão {#suggestions}

Você pode resolver as violações da taxa de transferência de transmissão adotando uma das seguintes recomendações:

1. Aumente a capacidade alocada para a sandbox.
2. Identifique fluxos de dados de alta taxa de transferência no [painel de monitoramento](/help/dataflows/ui/monitor-streaming-profile.md) e aplique limitação ou filtragem a esses fluxos de dados, se necessário.
3. Otimize sua assimilação usando a assimilação em lote para casos de uso de latência mais baixa.

Além disso, você pode examinar seus fluxos de dados e ver se pode otimizar sua estratégia de dados.

| Fator de contribuição | O que é | Impacto nos casos de uso | Práticas recomendadas |
| --- | --- | --- | --- |
| Conversão em lote para fluxo contínuo | As cargas de trabalho em lote convertidas em fluxo podem aumentar significativamente a taxa de transferência, afetando o desempenho e a alocação de recursos. Por exemplo, executar uma atualização de perfil em massa após um evento sem limites de taxa. | As estratégias de transmissão são desnecessárias para casos de uso em lote quando o processamento de baixa latência não é necessário. | Avaliar os requisitos de caso de uso. Para marketing de saída em lote, considere usar a [assimilação em lote](/help/ingestion/batch-ingestion/overview.md) em vez da transmissão para gerenciar a assimilação de dados com mais eficiência. |
| Assimilação desnecessária de dados | A ingestão de dados não é necessária para personalização e aumenta a taxa de transferência sem adicionar valor, desperdiçando recursos. Por exemplo, assimilar todo o tráfego de análises em perfis, independentemente da relevância. | O excesso de dados não relevantes cria ruído, dificultando a identificação de pontos de dados impactantes. Também pode causar atrito ao definir e gerenciar públicos e perfis. | Assimile somente dados necessários para seus casos de uso. Filtre os dados desnecessários.<ul><li>**Adobe Analytics**: use a [filtragem em nível de linha](/help/sources/tutorials/ui/create/adobe-applications/analytics.md#filtering-for-real-time-customer-profile) para otimizar a entrada de dados.</li><li>**Fontes**: Use a [[!DNL Flow Service] API para filtrar dados de nível de linha](/help/sources/tutorials/api/filter.md) de fontes com suporte, como [!DNL Snowflake] e [!DNL Google BigQuery].</li></li>**Sequência de dados do Edge**: configure [sequências de dados dinâmicas](/help/datastreams/configure-dynamic-datastream.md) para executar a filtragem em nível de linha do tráfego proveniente do SDK da Web.</li></ul> |

## Visão geral do vídeo {#video}

O vídeo a seguir fornece uma visão geral da Capacidade.

>[!VIDEO](https://video.tv.adobe.com/v/3475278/?captions=por_br&learn=on&enablevpops)

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
