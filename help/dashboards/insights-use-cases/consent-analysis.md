---
title: Rastreamento e análise de consentimento
description: Saiba como criar um painel de análise de consentimento para rastrear a tendência do consentimento do usuário ao longo do tempo.
source-git-commit: 4c45492157f0fe1a82187faf73439d6206cb0dc9
workflow-type: tm+mt
source-wordcount: '1921'
ht-degree: 0%

---

# Rastreamento e análise de consentimento

No cenário de marketing de hoje, você precisa entender e respeitar as preferências de consentimento do cliente. O Adobe Real-time Customer Data Platform oferece a capacidade de os profissionais de marketing analisarem o consentimento do cliente para criar confiança, cumprir as regulamentações de privacidade e fornecer experiências mais personalizadas.

Este documento detalha como criar um painel de consentimento para vários casos de uso de marketing para dados do Real-Time CDP. Especificamente, ele se concentra em como criar um público-alvo com os atributos apropriados para suas necessidades comerciais e, em seguida, consumir os insights por meio do uso de widgets pré-configurados na interface do usuário do Adobe Experience Platform. Um método alternativo de criar seu próprio widget personalizado com o recurso de painéis definido pelo usuário também é apresentado.

## Casos de uso {#use-cases}

Os casos de uso abordados neste guia são tendência de consentimento e sobreposição de consentimento.

- **Tendência de consentimento** rastreia a tendência do consentimento do usuário ao longo do tempo. A análise das alterações de preferência de consentimento ajuda os profissionais de marketing a planejar e executar campanhas que se adaptam a essas alterações de preferência do usuário. Por exemplo, você pode querer executar campanhas educacionais direcionadas, campanhas de transparência e confiança ou campanhas de incentivo para impulsionar opções de consentimento. Você também pode correlacionar campanhas que podem ter um impacto negativo no consentimento para reduzir proativamente a frequência dessas campanhas.
- **Sobreposição de consentimento** O usa a sobreposição entre canais de consentimento para fornecer mensagens personalizadas consistentes em vários canais para seus clientes que consentiram com vários canais. Os profissionais de marketing podem priorizar e alocar recursos para determinados canais em que um grau mais alto de consentimento e mensagens personalizadas podem repercutir nos clientes e gerar taxas de resposta mais altas.

<!-- ## Build a consent dashboard {#build-a-consent-dashboard} -->

## Criar públicos-alvo com consentimento {#create-consent-audiences}

Para criar um painel de consentimento, primeiro crie um público-alvo de todos os perfis que consentiram em entrar em contato com o. Para navegar até o Construtor de segmentos do Real-time Customer Data Platform, selecione **[!UICONTROL Públicos-alvo]** na navegação à esquerda da interface do usuário da Platform. No menu [!UICONTROL Cliente] guia do [!UICONTROL Públicos-alvo] painel, selecione **[!UICONTROL Criar público]** na parte superior direita da exibição, depois **[!UICONTROL Criar regras]**.

<!-- Update screenshot below to include Create audience -->s

![A variável [!UICONTROL Públicos-alvo] painel com [!UICONTROL Cliente], [!UICONTROL Públicos-alvo], e [!UICONTROL Criar segmento] destacado.](../images/insights-use-cases/consent-analysis/create-audience.png)

O Construtor de segmentos é exibido. Em seguida, selecione **[!UICONTROL Perfil individual XDM]** nas opções disponíveis. Consulte a documentação para obter mais informações sobre o [tela do construtor de regras](../../segmentation/ui/segment-builder.md#rule-builder-canvas).

![O Construtor de segmentos com a [!UICONTROL Perfil individual XDM] Pasta de atributo realçada.](../images/insights-use-cases/consent-analysis/xdm-individual-profile.png)

Localize seus atributos de consentimento nas opções disponíveis. Selecionar **[!UICONTROL Consentimentos e preferências]**.

>[!NOTE]
>
>Se você tiver mantido o consentimento do usuário em um atributo diferente do grupo de campos recomendado Adobe, deverá selecionar esses atributos em vez dos mostrados abaixo.

Mais informações podem ser encontradas no [tratamento do consentimento na segmentação](../../segmentation/consents.md#handling-consent-in-segmentation) documentação.

![O Construtor de segmentos com a [!UICONTROL Consentimento e preferências] Pasta de atributo realçada.](../images/insights-use-cases/consent-analysis/consent-and-preferences.png)

As várias opções de consentimento e preferência são exibidas. Como essa demonstração se concentra no consentimento para entrar em contato por vários canais de marketing, selecione **[!UICONTROL Preferências de marketing]**.

![O Construtor de segmentos com a [!UICONTROL Preferências de marketing] pasta realçada.](../images/insights-use-cases/consent-analysis/marketing-preferences.png)

A lista de preferências de marketing é exibida. Embora esse exemplo de caso de uso se concentre em email, SMS e chamadas, também é possível criar insights para qualquer outra combinação ou para a totalidade das opções. Para cada um dos canais, execute as etapas abaixo para criar um público-alvo.

Para começar a configurar um público-alvo, selecione **[!UICONTROL Receber SMS]** / **[!UICONTROL Receber email]** / **[!UICONTROL Receber chamadas]**.

![Os canais de contato disponíveis para marketing são destacados no construtor de público-alvo.](../images/insights-use-cases/consent-analysis/channels.png)

A variável [!UICONTROL Assinaturas] é exibida. Nas opções disponíveis, selecione e arraste o botão **[!UICONTROL Valor de escolha]** para o painel central e selecione o valor desejado no menu suspenso. Nesse caso, selecione **Sim (aceitar)**. Em seguida, nomeie o público-alvo de acordo com suas necessidades comerciais e forneça uma descrição simples.

>[!NOTE]
>
>Há um limite flexível no número de públicos que você é recomendado criar. Mais informações podem ser encontradas no [documentação das medidas de proteção de segmentação](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=en#segmentation-guardrails).

![A variável [!UICONTROL Valor de escolha] atributo com o [!UICONTROL Sim (aceitação)] valor destacado no construtor de segmentos. O nome e a descrição do público-alvo também são destacados.](../images/insights-use-cases/consent-analysis/choice-value.png)

Após criar os públicos-alvo necessários, eles são listados na [!UICONTROL Públicos-alvo] [!UICONTROL Procurar] guia.

>[!NOTE]
>
>Ao criar um público-alvo, é necessário aguardar a conclusão do trabalho de segmentação em lote antes que os dados estejam disponíveis para começar a criar seu painel de consentimento. A segmentação em lote descreve o processo de mover todos os dados de perfil de uma só vez pelas definições de segmento para produzir os públicos correspondentes. Depois de criado, esse público-alvo é salvo e armazenado para que você o exporte e use. Os segmentos em lote são avaliados automaticamente a cada 24 horas.

## Consumir insights {#consume-insights}

O Adobe criou vários insights que estão automaticamente disponíveis para você nos painéis Perfis, Públicos-alvo e Destinos. Qualquer público-alvo criado é automaticamente utilizável com esses insights pré-configurados. Consulte a documentação do widget padrão para obter uma lista dos insights disponíveis no [Perfis](../guides/profiles.md#standard-widgets), [Públicos-alvo](../guides/audiences.md#standard-widgets), e [Destinos](../guides/destinations.md) painéis.

## Sobreposição de público {#audience-overlap}

Para revisar a sobreposição entre dois públicos-alvo de consentimento, adicione o [!UICONTROL Sobreposição de público por política de mesclagem] ao painel Perfis e selecione os públicos-alvo desejados nos menus suspensos. Consulte a documentação para obter instruções sobre como adicionar um widget ao seu painel no [*Sobreposição de público por política de mesclagem*](../guides/profiles.md#audience-overlap-by-merge-policy) para obter mais informações sobre o insight.

<!-- Image needs updating to night mode -->

![O painel Perfis com o widget Sobreposição de público por política de mesclagem é realçado. O widget visualiza as sobreposições entre dois públicos-alvo de consentimento.](../images/insights-use-cases/consent-analysis/audience-overlap-by-merge-policy.png)

É possível visualizar a sobreposição de todos os públicos-alvo nos quais os usuários consentiram em receber chamadas em todos os outros públicos-alvo, com o relatório de sobreposição de público-alvo no painel Públicos-alvo. Para exibir a sobreposição de públicos-alvo de consentimento, navegue primeiro para a [!UICONTROL Públicos-alvo] [!UICONTROL Visão geral] guia. A partir daí, você pode adicionar a variável [!UICONTROL Relatório de sobreposição de público] para o painel Públicos-alvo. Depois que o widget tiver sido criado, selecione o **[!UICONTROL Usuário consentiu com chamadas]** público-alvo no menu suspenso visão geral do público-alvo na parte superior da página. Em seguida, selecione **[!UICONTROL Exibir mais]** no widget Relatório de sobreposição de público-alvo para ver até 50 das sobreposições principais e até 50 das sobreposições mínimas em relação ao segmento selecionado.

<!-- Image needs updating to night mode -->

![O painel Públicos-alvo com o widget de relatório de sobreposição de público-alvo é exibido. O usuário consentiu em chamar o público-alvo como um público-alvo de comparação, e o link Exibir mais está destacado.](../images/insights-use-cases/consent-analysis/audience-overlap-report-user-consent-to-calls.png)

A caixa de diálogo Relatório de sobreposição de público-alvo é expandida para mostrar dados adicionais de sobreposição de público-alvo.

<!-- Image needs updating to night mode -->

![O relatório Audience overlap, com os Usuários consentidos com o público-alvo de email destacado.](../images/insights-use-cases/consent-analysis/additional-audience-overlap-reports.png)

## Tendências de tamanho do público {#audience-size-trends}

Ao criar um público-alvo com base em consentimento, ele é direcionado automaticamente para até 12 meses a partir da data de criação do público-alvo. Para ter uma tendência totalmente funcional do consentimento do cliente, adicione os seguintes widgets à [!UICONTROL Segmentos] [!UICONTROL Visão geral] página. Esses insights oferecem um meio poderoso de rastrear como o seu consentimento está mudando com o tempo. Eles até se correlacionam com qualquer campanha que você execute em paralelo e que possa afetar o consentimento de forma positiva ou negativa. As descrições oferecidas para esses widgets se aplicam a um caso de uso de consentimento.

- [Tendência de tamanho do público](../guides/audiences.md#audience-size-trend): este widget oferece uma maneira de rastrear como seu respectivo consentimento mudou com o tempo.
- [Tendência de alteração de tamanho do público](../guides/audiences.md#audience-size-change-trend): este widget rastreia diariamente como o consentimento do cliente foi alterado. Por exemplo, se a contagem do consentimento do cliente cair em 100.000, você poderá ver como essa alteração ocorreu diariamente.
- [Tendência de tamanho do público por identidade](../guides/audiences.md#audience-size-trend-by-identity): com esse widget, você pode rastrear como seu respectivo consentimento foi alterado ao longo do tempo, mas filtrado ainda mais por uma identidade específica, como um email.

<!-- Image needs updating to night mode -->

![O painel Públicos-alvo com o widget Tendência de tamanho do público-alvo, Tendência de tamanho do público-alvo por identidade e Tendência de alteração de tamanho do público-alvo exibido. A página Usuários consentidos com o público-alvo de email é destacada.](../images/insights-use-cases/consent-analysis/three-audience-trend-widgets.png)

## Painel de visão geral do Audiences {#audiences-overview-dashboard}

Depois de criar um público-alvo relacionado ao consentimento, como &quot;Usuários consentidos com SMS&quot;, você pode exibir as principais informações de consentimento personalizadas sobre o público-alvo adicionando os widgets apropriados ao painel Visão geral do público-alvo. Navegue até a [!UICONTROL Públicos-alvo] [!UICONTROL Visão geral] e adicione os widgets escolhidos da biblioteca de widgets. Qualquer widget adicionado à sua visualização do painel pode ser redimensionado e movido usando o [!UICONTROL Modificar painel] recurso. Sua visualização personalizada pode conter insights, como a tendência ao longo do tempo (até 12 meses), as sobreposições com outros públicos-alvo e a composição de identidade do público-alvo. Um exemplo de exibição é mostrado abaixo.

![O painel de públicos-alvo com os Usuários consentidos com o público-alvo do SMS destacado no menu suspenso de público-alvo global.](../images/insights-use-cases/consent-analysis/audience-dashboard-user-consent-to-sms.png)

## Painéis definidos pelo usuário {#usr-defined-dashboards}

Você também pode criar seus próprios widgets com painéis definidos pelo usuário. Criar seu próprio widget fornece controle total sobre o tipo de widget, além de flexibilidade para adicionar filtros e muito mais, diretamente no Adobe Real-Time CDP.

Por exemplo, se você quiser direcionar vários públicos-alvo de consentimento no mesmo gráfico, para que possa ver ao longo do tempo como cada uma de suas preferências de consentimento foi alterada. Esse tipo de visualização é possível com painéis definidos pelo usuário em etapas mínimas e uma configuração única. Primeiro, selecione **[!UICONTROL Painéis]** no painel de navegação esquerdo. A variável [!UICONTROL Painéis] espaço de trabalho é exibido. Em seguida, selecione **[!UICONTROL Criar painel]**. Instruções completas sobre como [criar um painel e um widget personalizado](../user-defined-dashboards.md) podem ser encontradas no guia de painéis definido pelo usuário.

![A área de trabalho de painéis com Painéis e Criar painel realçados.](../images/user-defined-dashboards/create-dashboard.png)

Quando você [selecionar seu modelo de dados](../user-defined-dashboards.md#select-data-model) no widget composer, selecione `CDPInsights` seguido por **[!UICONTROL Próxima]**. A variável [!UICONTROL Selecionar tabela] será exibida.

![A caixa de diálogo Selecionar modelo de dados com o modelo CDPInsights está realçada.](../images/user-defined-dashboards/select-data-model-dialog.png)

A próxima exibição exibe uma lista das tabelas disponíveis no painel esquerdo. Selecione o `adwh_fact_profile_by_segment_and_namespace_trendlines`.

![A caixa de diálogo Selecionar tabela com a tabela &#39;adwh_fact_profile_by_segment_and_namespace_trendlines&#39; foi realçada.](../images/insights-use-cases/consent-analysis/select-table.png)

Depois que o widget composer for preenchido com dados da tabela escolhida, execute as etapas abaixo:

- [Pesquisar [!UICONTROL Atributos]](../user-defined-dashboards.md#add-filter-attributes) para `[!UICONTROL date]`, use o ícone + para adicionar o `[!UICONTROL date]` para o eixo X no menu suspenso.
  ![O compositor de widgets com o ícone de adição e o menu suspenso realçados.](../images/user-defined-dashboards/attributes-dropdown.png)
- Pesquisar [!UICONTROL Atributos] para `[!UICONTROL count_of_profiles]`, use o ícone + para adicionar o `[!UICONTROL count_of_profiles]` para o eixo Y no menu suspenso.
- Selecione o `...` (reticências) no campo [!UICONTROL Eixo Y] e selecione o [!UICONTROL SOMA] agregar função no menu suspenso.
  ![O widget Composição de widget Tendências de consentimento com o modelo de dados, a tabela, o menu suspenso do eixo Y e o recurso SOMA destacados. ](../images/insights-use-cases/consent-analysis/y-axis-sum-function.png)
- Selecione o [!UICONTROL Marcas] e altere o tipo de gráfico para [!UICONTROL Linha].
- Pesquisar [!UICONTROL Atributos] para o `[!UICONTROL segment_name]`, use o ícone + para adicionar o `segment_name` as a [!UICONTROL Filtro] no menu suspenso. A variável [!UICONTROL Filtro: Segment_name] será exibida. Selecione os públicos-alvo criados anteriormente que estão relacionados ao consentimento. Para este exemplo, selecione **[!UICONTROL Usuários consentidos com chamadas]**, **[!UICONTROL Usuários consentidos com o SMS]**, e **[!UICONTROL Usuários consentidos com o email]**, seguido por **[!UICONTROL Aplicar]**.
- Pesquisar [!UICONTROL Atributos] para `[!UICONTROL segment_name]`, em seguida, selecione o ícone + para adicionar `segment_name` as a [!UICONTROL Cor] no menu suspenso.
- Abertura [o [!UICONTROL Propriedades] painel](../user-defined-dashboards.md#widget-properties) e fornecer uma [!UICONTROL Título do widget] e [!UICONTROL Rótulo do eixo].
  ![O compositor de widgets com o ícone de propriedades e o Título do widget realçados.](../images/user-defined-dashboards/properties-panel.png)
- Selecionar **[!UICONTROL Salvar e fechar]** para confirmar as configurações.

>[!TIP]
>
>Agora é possível redimensionar ou mover o widget para o tamanho e a posição desejados antes de salvar o painel.


A imagem abaixo demonstra como o widget concluído é exibido e outros insights personalizados em potencial. Para obter mais detalhes sobre os tipos de widgets que podem ser criados, consulte o [documentação do modelo de dados](../cdp-insights-data-model.md).

<!-- The diagram shows straight lines due to a lack of data, however in your environment the trends will reflect the actual changes over time. -->

![O widget personalizado Tendências de consentimento concluído.](../images/insights-use-cases/consent-analysis/consent-trends-widget.png)

## Rastreamento de políticas de consentimento {#consent-policies}

Os painéis de consentimento criados capturam o **somente distribuição de atributos de consentimento e preferência**.

>[!NOTE]
>
>Para clientes do **Adobe Healthcare Shield** ou **Proteção de segurança e privacidade do Adobe**, estes painéis **não** refletir qualquer rastreamento de políticas de consentimento. O rastreamento disponível inclui o número de políticas criadas, ativadas e o impacto na associação do público-alvo.

## Próximas etapas

Ao ler este documento, você aprendeu a criar painéis para obter uma visualização abrangente das preferências de consentimento do cliente usando os insights do Real-Time CDP. Este documento demonstra como o Real-Time CDP fornece uma solução robusta para o cenário atual de privacidade focada, em que a coleta, a segmentação, a análise e as campanhas de marketing personalizadas com base em dados de consentimento são cruciais para os profissionais de marketing.
