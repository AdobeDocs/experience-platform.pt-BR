---
title: Visão geral do painel de monitoramento
description: Saiba como usar o painel de monitoramento na interface do usuário do Adobe Experience Platform
exl-id: 06ea5380-d66e-45ae-aa02-c8060667da4e
source-git-commit: 710fa6930b27f95d34539a18881c0f9d23e1debd
workflow-type: tm+mt
source-wordcount: '1031'
ht-degree: 0%

---

# Visão geral do painel de monitoramento

Use o painel de monitoramento na interface do usuário do Adobe Experience Platform para exibir a jornada dos dados, da assimilação à ativação. Com o painel de monitoramento, é possível:

* Monitore a jornada de seus dados de Fontes, Serviço de identidade, Perfil do cliente em tempo real, Públicos-alvo e, finalmente, em Destinos.
* Visualize métricas e status diferentes dependendo do estágio em que seus dados estão.
* Filtre sua visualização de monitoramento de dados por tipo de dados.

O painel de monitoramento é compatível com a exibição de vários tipos de dados diferentes:

* **Cliente e Conta**: os dados do cliente referem-se aos dados usados no [Real-time Customer Data Platform](../../rtcdp/home.md), enquanto os dados da conta referem-se aos [dados de perfis de conta](../../rtcdp/accounts/account-profile-overview.md) que podem ser acessados quando se inscreveu no [Real-Time CDP, B2B Edition](../../rtcdp/b2b-overview.md). Se sua licença do Real-Time CDP não incluir o Real-Time CDP, B2B Edition, você só poderá usar o painel de monitoramento para monitorar os dados do cliente.
* **Prospecto**: [Os perfis de prospecto](../../profile/ui/prospect-profile.md) são usados para representar pessoas que ainda não se envolveram com a sua empresa, mas que você deseja contatar. Com perfis de prospecto, você pode complementar seus perfis de clientes com atributos de parceiros de terceiros confiáveis. Você deve estar licenciado com o Real-Time CDP (App Service), Adobe Experience Platform Ativation, Real-Time CDP, Real-Time CDP Prime, Real-Time CDP Ultimate para ver o tipo de dados do cliente potencial.
* **Enriquecimento do perfil de conta**: os perfis de conta permitem unificar as informações de conta de várias fontes. Você deve ter uma licença do Real-Time CDP, B2B Edition para monitorar os dados de enriquecimento do perfil da conta.

Leia este documento para saber como usar o painel de monitoramento para monitorar a jornada de seus dados em diferentes serviços de Experience Platform.

## Introdução

Este documento requer uma compreensão funcional dos seguintes componentes do Experience Platform:

* [Fluxos de dados](../home.md): Fluxos de dados são representações de trabalhos de dados que movem dados pelo Experience Platform. Você pode usar o espaço de trabalho de origens para criar fluxos de dados que assimilam dados de uma determinada origem para o Experience Platform.
* [Fontes](../../sources/home.md): use fontes no Experience Platform para assimilar dados de um aplicativo Adobe ou de uma fonte de dados de terceiros.
* [Serviço de identidade](../../identity-service/home.md): obtenha uma melhor visão dos clientes individuais e de seu comportamento unindo as identidades de vários dispositivos e sistemas.
* [Perfil de cliente em tempo real](../../profile/home.md): fornece um perfil de cliente unificado em tempo real com base em dados agregados de várias fontes.
* [Segmentação](../../segmentation/home.md): use o Serviço de segmentação para criar segmentos e públicos a partir dos dados do Perfil do cliente em tempo real.
* [Destinos](../../destinations/home.md): os destinos são integrações pré-criadas com aplicativos usados com frequência que permitem a ativação contínua de dados da Platform para campanhas de marketing entre canais, campanhas de email, publicidade direcionada e muitos outros casos de uso.

## Guia do painel de monitoramento

Na interface do usuário do Experience Platform, selecione **[!UICONTROL Monitoramento]** em [!UICONTROL Gerenciamento de dados] na navegação à esquerda.

![O painel de monitoramento na interface do Experience Platform.](../assets/ui/monitor-overview/monitoring.png)

Selecione **[!UICONTROL Tipo de Dados]** e use o menu suspenso para selecionar o tipo de dados que deseja exibir. Os tipos de dados são definidos pelas classes de esquema do Experience Data Model (XDM) para garantir que seus dados sigam um formato padrão quando assimilados no Experience Platform. Para obter mais informações, consulte a seguinte documentação:

* [Tipo de dados da conta B2B](../../rtcdp/b2b-tutorial.md)
* [Tipo de dados de cliente potencial](../../rtcdp/partner-data/prospecting.md)

Você pode filtrar sua visualização com base nos seguintes tipos de dados:

>[!BEGINTABS]

>[!TAB Tudo]

Selecione **[!UICONTROL Todos]** para atualizar seu painel e exibir métricas em todos os dados assimilados no Experience Platform durante um determinado período.

![O tipo de dados de monitoramento foi definido como &quot;Todos&quot;.](../assets/ui/monitor-overview/all.png)

>[!TAB Cliente e conta]

Selecione **[!UICONTROL Cliente e conta]** para atualizar seu painel e exibir as métricas nos dados do Cliente e conta que foram assimilados no Experience Platform durante um determinado período.

![O tipo de dados de monitoramento definido como &quot;Cliente e Conta&quot;.](../assets/ui/monitor-overview/customer-account.png)

>[!TAB Prospecto]

Selecione **[!UICONTROL Prospecto]** para atualizar seu painel e exibir métricas em dados de prospecção que foram assimilados no Experience Platform durante um determinado período. **Observação**: você só poderá exibir atividades de tipos de dados de prospecto se estiver [qualificado para dados de prospecto](../../rtcdp/partner-data/prospecting.md).

![O tipo de dados de monitoramento definido como &quot;Prospecto&quot;.](../assets/ui/monitor-overview/prospect.png)

>[!TAB Enriquecimento do perfil da conta]

Selecione **[!UICONTROL Enriquecimento do perfil da conta]** para atualizar seu painel e exibir as métricas nos dados de enriquecimento do perfil. **Observação**: você só poderá exibir métricas de enriquecimento do perfil da conta se tiver direito a [dados B2B](../../rtcdp/b2b-tutorial.md).

![O tipo de dados de monitoramento definido como &quot;Enriquecimento do perfil da conta&quot;.](../assets/ui/monitor-overview/account-profile-enrichment.png)

>[!ENDTABS]

Use o cabeçalho superior do painel para obter uma experiência de monitoramento entre serviços. É possível filtrar a visualização de métricas e gráficos ao selecionar o cartão de recurso de sua escolha no cabeçalho da categoria de dados.

>[!BEGINTABS]

>[!TAB Fontes]

Selecione **[!UICONTROL Fontes]** para exibir as métricas sobre a taxa de assimilação das fontes. Leia o guia em [dados de fontes de monitoramento](monitor-sources.md) para obter mais informações.

![O painel de monitoramento na interface do usuário com o cartão de origens selecionado.](../assets/ui/monitor-overview/sources.png)

>[!TAB Identidades]

Selecione **[!UICONTROL Identidades]** para exibir a taxa de êxito do processamento de seus dados de identidade. Leia o guia em [dados de identidade de monitoramento](monitor-identities.md) para obter mais informações.

![O painel de monitoramento na interface do usuário com o cartão de identidades selecionado.](../assets/ui/monitor-overview/identities.png)

>[!TAB Perfis]

Selecione **[!UICONTROL Perfis]** para exibir a taxa de sucesso do processamento dos dados do seu perfil. Leia o guia em [dados do perfil de monitoramento](monitor-profiles.md) para obter mais informações.

![O painel de monitoramento na interface do usuário com o cartão de perfis selecionado.](../assets/ui/monitor-overview/profiles.png)

>[!TAB Públicos-alvo]

Selecione **[!UICONTROL Públicos-alvo]** para exibir métricas sobre seus públicos-alvo e trabalhos de segmentação. Leia o manual sobre [monitoramento de dados de público-alvo](monitor-audiences.md) para obter mais informações.

![O painel de monitoramento na interface do usuário com o cartão de públicos selecionado.](../assets/ui/monitor-overview/audiences.png)

>[!TAB Destinos]

Selecione **[!UICONTROL Destinos]** para exibir métricas em sua [!UICONTROL Taxa de ativação de streaming] e [!UICONTROL Execuções de fluxo de dados com falha em lote]. Leia o manual sobre [dados de destinos de monitoramento](monitor-destinations.md) para obter mais informações.

![O painel de monitoramento na interface do usuário com o cartão de destinos selecionado.](../assets/ui/monitor-overview/destinations.png)

>[!ENDTABS]

### Configurar intervalo de tempo de monitoramento {#configure-monitoring-time-frame}

Por padrão, o painel de monitoramento exibe métricas sobre dados assimilados nas últimas 24 horas. Para atualizar o período, selecione **[!UICONTROL Últimas 24 horas]**.

![O painel de monitoramento na interface do usuário com a configuração de hora selecionada.](../assets/ui/monitor-overview/select-time.png)

Você pode configurar um novo intervalo de tempo para a visualização de monitoramento de dados na caixa de diálogo exibida. Você tem a opção de criar um intervalo de tempo personalizado ou selecionar na lista de opções pré-configuradas:

* [!UICONTROL Últimas 24 horas]
* [!UICONTROL Últimos 7 dias]
* [!UICONTROL Últimos 30 dias]

Quando terminar, selecione **[!UICONTROL Aplicar]**.

![A janela pop-up de configuração de intervalo de tempo no painel de monitoramento.](../assets/ui/monitor-overview/update-time.png)

## Próximas etapas

Agora, ao ler este documento, você pode navegar pelo painel de monitoramento na interface do usuário do. Para obter informações sobre como monitorar dados para um serviço Experience Platform específico, leia a documentação abaixo:

* [Monitorar dados de fontes](monitor-sources.md).
* [Monitorar dados de identidade](monitor-identities.md).
* [Monitorar dados de perfil](monitor-profiles.md).
* [Monitorar dados de público-alvo](monitor-audiences.md).
* [Monitorar dados de destinos](monitor-destinations.md).
