---
title: Rastreamento e análise de consentimento
description: Saiba como criar um painel de análise de consentimento para rastrear a tendência do consentimento do usuário ao longo do tempo.
exl-id: 34accae5-8b4f-4281-8333-187a91db8199
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '1910'
ht-degree: 0%

---

# Rastreamento e análise de consentimento

No cenário de marketing de hoje, você precisa entender e respeitar as preferências de consentimento do cliente. O Adobe Real-Time Customer Data Platform oferece a capacidade de os profissionais de marketing analisarem o consentimento do cliente para criar confiança, cumprir as regulamentações de privacidade e fornecer experiências mais personalizadas.

Este documento detalha como criar um painel de consentimento para vários casos de uso de marketing para dados do Real-Time CDP. Especificamente, ele se concentra em como criar um público-alvo com os atributos apropriados para suas necessidades comerciais e, em seguida, consumir os insights por meio do uso de widgets pré-configurados na interface do usuário do Adobe Experience Platform. Um método alternativo de criar seu próprio widget personalizado com o recurso de painéis definido pelo usuário também é apresentado.

## Casos de uso {#use-cases}

Os casos de uso abordados neste guia são tendência de consentimento e sobreposição de consentimento.

- **Tendência de consentimento** rastreia a tendência do consentimento do usuário ao longo do tempo. A análise das alterações de preferência de consentimento ajuda os profissionais de marketing a planejar e executar campanhas que se adaptam a essas alterações de preferência do usuário. Por exemplo, você pode querer executar campanhas educacionais direcionadas, campanhas de transparência e confiança ou campanhas de incentivo para impulsionar opções de consentimento. Você também pode correlacionar campanhas que podem ter um impacto negativo no consentimento para reduzir proativamente a frequência dessas campanhas.
- **Sobreposição de consentimento** usa a sobreposição entre canais de consentimento para fornecer mensagens personalizadas consistentes em vários canais para seus clientes que consentiram com vários canais. Os profissionais de marketing podem priorizar e alocar recursos para determinados canais em que um grau mais alto de consentimento e mensagens personalizadas podem repercutir nos clientes e gerar taxas de resposta mais altas.

## Criar públicos-alvo com consentimento {#create-consent-audiences}

Para criar um painel de consentimento, primeiro crie um público-alvo de todos os perfis que consentiram em entrar em contato com o. Para navegar até o Construtor de segmentos do Real-Time Customer Data Platform, selecione **[!UICONTROL Públicos-alvo]** na navegação à esquerda da interface do usuário do Experience Platform. Na guia [!UICONTROL Cliente] do painel [!UICONTROL Públicos-alvo], selecione **[!UICONTROL Criar público-alvo]** na parte superior direita da exibição e **[!UICONTROL Regras de compilação]**.

![O painel [!UICONTROL Públicos-alvo] com [!UICONTROL Cliente], [!UICONTROL Públicos-alvo] e [!UICONTROL Criar segmento] foi realçado.](../images/insights-use-cases/consent-analysis/create-audience.png)

O Construtor de segmentos é exibido. Em seguida, selecione **[!UICONTROL Perfil individual XDM]** nas opções disponíveis. Consulte a documentação para obter mais informações sobre a [tela do construtor de regras](../../segmentation/ui/segment-builder.md#rule-builder-canvas).

![O Construtor de segmentos com a [!UICONTROL pasta de atributo Perfil Individual XDM] foi realçada.](../images/insights-use-cases/consent-analysis/xdm-individual-profile.png)

Localize seus atributos de consentimento nas opções disponíveis. Selecione **[!UICONTROL Consentimentos e Preferências]**.

>[!NOTE]
>
>Se você tiver mantido o consentimento do usuário em um atributo diferente do grupo de campos recomendado do Adobe, deverá selecionar esses atributos em vez dos mostrados abaixo.

Mais informações podem ser encontradas no [tratamento do consentimento na documentação de segmentação](../../segmentation/tutorials/consents.md#handling-consent-in-segmentation).

![O Construtor de Segmentos com a pasta de atributos [!UICONTROL Consentimento e Preferências] está realçada.](../images/insights-use-cases/consent-analysis/consent-and-preferences.png)

As várias opções de consentimento e preferência são exibidas. Como esta demonstração foca no consentimento para contato em vários canais de marketing, selecione **[!UICONTROL Preferências de marketing]**.

![O Construtor de Segmentos com a pasta [!UICONTROL Preferências de Marketing] está realçado.](../images/insights-use-cases/consent-analysis/marketing-preferences.png)

A lista de preferências de marketing é exibida. Embora esse exemplo de caso de uso se concentre em email, SMS e chamadas, também é possível criar insights para qualquer outra combinação ou para a totalidade das opções. Para cada um dos canais, execute as etapas abaixo para criar um público-alvo.

Para começar a configurar um público, selecione **[!UICONTROL Receber SMS]** / **[!UICONTROL Receber email]** / **[!UICONTROL Receber chamadas]**.

![Os canais de contato disponíveis para marketing estão destacados no construtor de público-alvo.](../images/insights-use-cases/consent-analysis/channels.png)

A pasta [!UICONTROL Assinaturas] é exibida. Nas opções disponíveis, selecione e arraste o atributo **[!UICONTROL Valor da opção]** para o painel central e selecione o valor desejado no menu suspenso. Nesse caso, selecione **Sim (aceitar)**. Em seguida, nomeie o público-alvo de acordo com suas necessidades comerciais e forneça uma descrição simples.

>[!NOTE]
>
>Há um limite flexível no número de públicos que você é recomendado criar. Mais informações podem ser encontradas na [documentação de medidas de proteção de segmentação](../../profile/guardrails.md#segmentation-guardrails).

![O atributo [!UICONTROL Valor de Escolha] com o valor [!UICONTROL Sim (aceitação)] realçado no construtor de segmentos. O nome e a descrição do público-alvo também são destacados.](../images/insights-use-cases/consent-analysis/choice-value.png)

Após criar os públicos necessários, eles serão listados na guia [!UICONTROL Públicos-alvo] [!UICONTROL Procurar].

>[!NOTE]
>
>Ao criar um público-alvo, é necessário aguardar a conclusão do trabalho de segmentação em lote antes que os dados estejam disponíveis para começar a criar seu painel de consentimento. A segmentação em lote descreve o processo de mover todos os dados de perfil de uma só vez pelas definições de segmento para produzir os públicos correspondentes. Depois de criado, esse público-alvo é salvo e armazenado para que você o exporte e use. Os segmentos em lote são avaliados automaticamente a cada 24 horas.

## Consumir insights {#consume-insights}

O Adobe criou vários insights que estão automaticamente disponíveis para você nos painéis Perfis, Públicos-alvo e Destinos. Qualquer público-alvo criado é automaticamente utilizável com esses insights pré-configurados. Consulte a documentação do widget padrão para obter uma lista dos insights disponíveis nos painéis [Perfis](../guides/profiles.md#standard-widgets), [Públicos-alvo](../guides/audiences.md#standard-widgets) e [Destinos](../guides/destinations.md).

## Sobreposição de público {#audience-overlap}

Para revisar a sobreposição entre dois públicos-alvo de consentimento, adicione a [!UICONTROL Política de sobreposição de público-alvo por mesclagem] ao painel Perfis e selecione os públicos-alvo desejados nos menus suspensos. Consulte a documentação para obter instruções sobre como adicionar um widget ao seu painel na [*Política de sobreposição de público-alvo por mesclagem*](../guides/profiles.md#audience-overlap-by-merge-policy) para obter mais informações sobre a insight.

<!-- Image needs updating to night mode -->

![O painel Perfis com o widget Sobreposição de público por política de mesclagem está realçado. O widget visualiza sobreposições entre dois públicos-alvo de consentimento.](../images/insights-use-cases/consent-analysis/audience-overlap-by-merge-policy.png)

É possível visualizar a sobreposição de todos os públicos-alvo nos quais os usuários consentiram em receber chamadas em todos os outros públicos-alvo, com o relatório de sobreposição de público-alvo no painel Públicos-alvo. Para exibir a sobreposição de públicos-alvo de consentimento, navegue primeiro para a guia [!UICONTROL Públicos-alvo] [!UICONTROL Visão geral]. A partir daí, você pode adicionar o widget [!UICONTROL Relatório de sobreposição de público] ao painel Públicos. Após a criação do widget, selecione o público-alvo **[!UICONTROL Usuário consentiu com chamadas]** na visão geral do menu suspenso de público-alvo na parte superior da página. Em seguida, selecione **[!UICONTROL Exibir mais]** no widget de relatório de sobreposição de público-alvo para ver até 50 das sobreposições principais e até 50 das sobreposições mínimas relacionadas ao segmento selecionado.

<!-- Image needs updating to night mode -->

![O painel de Públicos-alvo com o widget de relatório de sobreposição de Público-alvo exibido. O Usuário consentiu em chamar o público-alvo como um público-alvo de comparação, e o link Exibir mais estão destacados.](../images/insights-use-cases/consent-analysis/audience-overlap-report-user-consent-to-calls.png)

A caixa de diálogo Relatório de sobreposição de público-alvo é expandida para mostrar dados adicionais de sobreposição de público-alvo.

<!-- Image needs updating to night mode -->

![O relatório de sobreposição de Público-alvo, com os Usuários consentidos destacando o público-alvo por email.](../images/insights-use-cases/consent-analysis/additional-audience-overlap-reports.png)

## Tendências de tamanho do público-alvo {#audience-size-trends}

Ao criar um público-alvo com base em consentimento, ele é direcionado automaticamente para até 12 meses a partir da data de criação do público-alvo. Para ter uma tendência totalmente funcional do consentimento do cliente, adicione os seguintes widgets à página [!UICONTROL Segmentos] [!UICONTROL Visão geral]. Esses insights oferecem um meio poderoso de rastrear como o seu consentimento está mudando com o tempo. Eles até se correlacionam com qualquer campanha que você execute em paralelo e que possa afetar o consentimento de forma positiva ou negativa. As descrições oferecidas para esses widgets se aplicam a um caso de uso de consentimento.

- [Tendência de tamanho do público-alvo](../guides/audiences.md#audience-size-trend): esse widget oferece uma maneira de acompanhar como seu respectivo consentimento foi alterado ao longo do tempo.
- [Tendência de alteração no tamanho do público-alvo](../guides/audiences.md#audience-size-change-trend): esse widget acompanha o modo como o consentimento do cliente é alterado diariamente. Por exemplo, se a contagem do consentimento do cliente cair em 100.000, você poderá ver como essa alteração ocorreu diariamente.
- [Tendência de tamanho do público por identidade](../guides/audiences.md#audience-size-trend-by-identity): com este widget, você pode acompanhar como seu respectivo consentimento mudou com o tempo, mas foi filtrado ainda mais por uma identidade específica, como um email.

<!-- Image needs updating to night mode -->

![O painel de Públicos-alvo com a tendência de tamanho do Público-alvo, tendência de tamanho do Público-alvo por identidade e widget de tendência de alteração de tamanho do Público-alvo exibido. O campo Usuários consentidos com o email do público é destacado.](../images/insights-use-cases/consent-analysis/three-audience-trend-widgets.png)

## Painel de visão geral do Audiences {#audiences-overview-dashboard}

Depois de criar um público-alvo relacionado ao consentimento, como &quot;Usuários consentidos com SMS&quot;, você pode exibir as principais informações de consentimento personalizadas sobre o público-alvo adicionando os widgets apropriados ao painel Visão geral do público-alvo. Navegue até [!UICONTROL Públicos-alvo] [!UICONTROL Visão geral] e adicione os widgets escolhidos da biblioteca de widgets. Qualquer widget adicionado à sua exibição do painel pode ser redimensionado e movido usando o recurso [!UICONTROL Modificar painel]. Sua visualização personalizada pode conter insights, como a tendência ao longo do tempo (até 12 meses), as sobreposições com outros públicos-alvo e a composição de identidade do público-alvo. Um exemplo de exibição é mostrado abaixo.

![O painel de públicos-alvo com os Usuários consentidos com o público-alvo do SMS destacado no menu suspenso de público-alvo global.](../images/insights-use-cases/consent-analysis/audience-dashboard-user-consent-to-sms.png)

## Painéis definidos pelo usuário {#usr-defined-dashboards}

Você também pode criar seus próprios widgets com painéis definidos pelo usuário. Criar seu próprio widget fornece controle total sobre o tipo de widget, além de flexibilidade para adicionar filtros e muito mais, diretamente no Adobe Real-Time CDP.

Por exemplo, se você quiser direcionar vários públicos-alvo de consentimento no mesmo gráfico, para que possa ver ao longo do tempo como cada uma de suas preferências de consentimento foi alterada. Esse tipo de visualização é possível com painéis definidos pelo usuário em etapas mínimas e uma configuração única. Primeiro, selecione **[!UICONTROL Painéis]** na navegação à esquerda. O espaço de trabalho [!UICONTROL Painéis] é exibido. Em seguida, selecione **[!UICONTROL Criar painel]**. Instruções completas sobre como [criar um painel e um widget personalizado](../standard-dashboards.md) podem ser encontradas no guia de painéis definido pelo usuário.

![O espaço de trabalho de painéis com Painéis e Criar painel realçados.](../images/standard-dashboards/create-dashboard.png)

Quando você [selecionar seu modelo de dados](../standard-dashboards.md#select-data-model) no widget composer, selecione `CDPInsights` seguido de **[!UICONTROL Próximo]**. A caixa de diálogo [!UICONTROL Selecionar tabela] é exibida.

![A caixa de diálogo Selecionar modelo de dados com o modelo CDPInsights está realçada.](../images/standard-dashboards/select-data-model-dialog.png)

A próxima exibição exibe uma lista das tabelas disponíveis no painel esquerdo. Selecione o `adwh_fact_profile_by_segment_and_namespace_trendlines`.

![A caixa de diálogo Selecionar tabela com a tabela &#39;adwh_fact_profile_by_segment_and_namespace_trendlines&#39; foi realçada.](../images/insights-use-cases/consent-analysis/select-table.png)

Depois que o widget composer for preenchido com dados da tabela escolhida, execute as etapas abaixo:

- [Pesquise [!UICONTROL Atributos]](../standard-dashboards.md#add-filter-attributes) para `[!UICONTROL date]` e use o ícone + para adicionar o atributo `[!UICONTROL date]` ao eixo X do menu suspenso.
  ![O widget composer com o ícone de adição e menu suspenso realçado.](../images/standard-dashboards/attributes-dropdown.png)
- Pesquise [!UICONTROL Atributos] para `[!UICONTROL count_of_profiles]`, em seguida, use o ícone + para adicionar o atributo `[!UICONTROL count_of_profiles]` ao eixo Y do menu suspenso.
- Selecione o ícone `...` (elipses) no campo [!UICONTROL Eixo Y] e selecione a função de agregação [!UICONTROL SUM] no menu suspenso.
  ![Widget de Tendências de consentimento do widget com o modelo de dados, a tabela, o menu suspenso do eixo Y e o recurso SOMA destacados. &#x200B;](../images/insights-use-cases/consent-analysis/y-axis-sum-function.png)
- Selecione o menu suspenso [!UICONTROL Marcas] e altere o tipo de gráfico para [!UICONTROL Linha].
- Pesquise [!UICONTROL Atributos] para `[!UICONTROL segment_name]`, em seguida, use o ícone + para adicionar o `segment_name` como um [!UICONTROL Filtro] no menu suspenso. A caixa de diálogo [!UICONTROL Filtro: Nome_do_Segmento] é exibida. Selecione os públicos-alvo criados anteriormente que estão relacionados ao consentimento. Para este exemplo, selecione **[!UICONTROL Usuários Consentidos em Chamadas]**, **[!UICONTROL Usuários Consentidos em SMS]** e **[!UICONTROL Usuários Consentidos em Email]**, seguido de **[!UICONTROL Aplicar]**.
- Pesquise [!UICONTROL Atributos] para `[!UICONTROL segment_name]` e selecione o ícone + para adicionar `segment_name` como [!UICONTROL Cor] no menu suspenso.
- Abra [o painel [!UICONTROL Propriedades]](../standard-dashboards.md#widget-properties) e forneça um [!UICONTROL Título do widget] e um [!UICONTROL Rótulo do eixo] apropriados.
  ![O widget composer com o ícone de propriedades e o título do Widget destacados.](../images/standard-dashboards/properties-panel.png)
- Selecione **[!UICONTROL Salvar e fechar]** para confirmar suas configurações.

>[!TIP]
>
>Agora é possível redimensionar ou mover o widget para o tamanho e a posição desejados antes de salvar o painel.


A imagem abaixo demonstra como o widget concluído é exibido e outros insights personalizados em potencial. Para obter mais detalhes sobre os tipos de widgets que podem ser criados, consulte a [documentação sobre modelo de dados](../data-models/cdp-insights-data-model-b2c.md).

<!-- The diagram shows straight lines due to a lack of data, however in your environment the trends will reflect the actual changes over time. -->

![Widget de Tendências de consentimento personalizado concluído.](../images/insights-use-cases/consent-analysis/consent-trends-widget.png)

## Rastreamento de políticas de consentimento {#consent-policies}

Os painéis de consentimento criados capturam apenas a **distribuição de atributos de consentimento e preferência**.

>[!NOTE]
>
>Para clientes do **Adobe Healthcare Shield** ou do **Adobe Privacy &amp; Security Shield**, esses painéis **não** refletem qualquer rastreamento de políticas de consentimento. O rastreamento disponível inclui o número de políticas criadas, ativadas e o impacto na associação do público-alvo.

## Próximas etapas

Ao ler este documento, você aprendeu a criar painéis para obter uma visualização abrangente das preferências de consentimento do cliente usando os insights do Real-Time CDP. Este documento demonstra como o Real-Time CDP fornece uma solução robusta para o cenário atual de privacidade focada, em que a coleta, a segmentação, a análise e as campanhas de marketing personalizadas com base em dados de consentimento são cruciais para os profissionais de marketing.
