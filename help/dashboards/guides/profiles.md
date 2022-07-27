---
keywords: Experience Platform, perfil, perfil do cliente em tempo real, interface do usuário, interface do usuário, personalização, painel de perfil, painel
title: Painel de perfis
description: A Adobe Experience Platform fornece um painel pelo qual você pode visualizar informações importantes sobre os dados do Perfil do cliente em tempo real da sua organização.
type: Documentation
exl-id: 7b9752b2-460e-440b-a6f7-a1f1b9d22eeb
source-git-commit: bc1516d5453134ffb18fa682fd70b1f3581d5e18
workflow-type: tm+mt
source-wordcount: '3816'
ht-degree: 1%

---

# [!UICONTROL Perfis] painel

A interface do usuário do Adobe Experience Platform (UI) fornece um painel através do qual você pode visualizar informações importantes sobre sua [!DNL Real-time Customer Profile] dados, como capturados durante um instantâneo diário. Este guia descreve como acessar e trabalhar com a [!UICONTROL Perfis] painel na interface do usuário e fornece informações sobre as métricas exibidas no painel.

Para obter uma visão geral de todos os recursos de Perfil na interface do usuário do Experience Platform, visite o [Guia da interface do usuário do perfil do cliente em tempo real](../../profile/ui/user-guide.md).

## Dados do painel de perfis

O [!UICONTROL Perfis] O painel exibe um instantâneo dos dados de atributo (registro) que sua organização tem na Loja de perfis no Experience Platform. O instantâneo não inclui nenhum dado de evento (série de tempo).

Os dados do atributo no instantâneo mostram os dados exatamente como aparecem no momento específico em que o instantâneo foi tirado. Em outras palavras, o instantâneo não é uma aproximação ou amostra dos dados, e o painel de Perfil não está sendo atualizado em tempo real.

>[!NOTE]
>
>Quaisquer alterações ou atualizações feitas nos dados desde que o instantâneo foi tirado não serão refletidas no painel até que o próximo instantâneo seja tirado.

## Explorar o [!UICONTROL Perfis] painel

Para navegar até o [!UICONTROL Perfis] no painel da interface do usuário da plataforma, selecione **[!UICONTROL Perfis]** no painel à esquerda, selecione o **[!UICONTROL Visão geral]** para exibir o painel.

>[!NOTE]
>
>Se sua organização for nova na Plataforma e ainda não tiver conjuntos de dados ativos do Perfil ou políticas de mesclagem criadas, a variável [!UICONTROL Perfis] o painel não está visível. Em vez disso, a variável [!UICONTROL Visão geral] A guia exibe links e documentação para ajudar você a começar a usar o Perfil do cliente em tempo real.

![](../images/profiles/dashboard-overview.png)

### Modificação do [!UICONTROL Perfis] painel

Você pode modificar a aparência da variável [!UICONTROL Perfis] painel selecionando **[!UICONTROL Modificar painel]**. Isso permite mover, adicionar e remover widgets do painel, bem como acessar o **[!UICONTROL Biblioteca de widgets]** para explorar widgets disponíveis e criar widgets personalizados para sua organização.

Consulte a [modificação de painéis](../customize/modify.md) e [Visão geral da biblioteca de widgets](../customize/widget-library.md) documentação para saber mais.

## (Beta) Informações sobre a eficácia do perfil {#profile-efficacy-insights}

>[!IMPORTANT]
>
>A funcionalidade de insight da eficácia do perfil encontra-se atualmente em beta e não está disponível para todos os utilizadores. A documentação e a funcionalidade estão sujeitas a alterações.

O [!UICONTROL Eficácia] O guia fornece métricas sobre a qualidade e integridade dos dados do seu perfil através do uso de widgets de eficácia de perfil. Esses widgets ilustram rapidamente a composição de seus perfis, as tendências de integridade ao longo do tempo e as avaliações sobre a qualidade dos dados de seu perfil.

![O painel de eficácia do perfil.](../images/profiles/attributes-quality-assessment.png)

Consulte a [seção de widgets de eficácia do perfil](#profile-efficacy-widgets) para obter mais informações sobre os widgets atualmente disponíveis.

O layout deste painel também pode ser personalizado ao selecionar [**[!UICONTROL Modificar painel]**](../customize/modify.md) do [!UICONTROL Visão geral] guia .

## Procurar perfis {#browse-profiles}

O [!UICONTROL Procurar] permite pesquisar e exibir os perfis somente leitura assimilados na organização IMS. Desse ponto, você pode ver informações importantes pertencentes ao perfil, relacionadas às preferências, aos eventos passados, às interações e aos segmentos

Para saber mais sobre os recursos de visualização de perfil fornecidos na interface do usuário da plataforma, consulte a documentação em [navegar pelos perfis no Real-time Customer Data Platform](../../rtcdp/profile/profile-browse.md).

## Mesclar políticas {#merge-policies}

As métricas exibidas no [!UICONTROL Perfis] O painel é baseado nas políticas de mesclagem aplicadas aos dados do Perfil do cliente em tempo real. Quando os dados são reunidos de várias fontes para criar o perfil do cliente, os dados podem conter valores conflitantes. Por exemplo, um conjunto de dados pode listar um cliente como &quot;único&quot;, enquanto outro conjunto de dados pode listá-lo como &quot;casado&quot;. É tarefa da política de mesclagem determinar quais dados priorizar e exibir como parte do perfil.

Para obter mais informações sobre políticas de mesclagem, incluindo como criar, editar e declarar uma política de mesclagem padrão para sua organização, comece lendo a variável [visão geral das políticas de mesclagem](../../profile/merge-policies/overview.md).

O painel selecionará automaticamente uma política de mesclagem para usar. A política de mesclagem aplicada pode ser alterada usando o menu suspenso ao lado do nome da política de mesclagem.

>[!NOTE]
>
>O menu suspenso mostra apenas as políticas de mesclagem relacionadas à Classe de Perfil Individual XDM. No entanto, se sua organização criou várias políticas de mesclagem, pode significar que será necessário rolar a página para visualizar a lista completa de políticas de mesclagem disponíveis.

![](../images/profiles/select-merge-policy.png)

## Schemas da União

O [!UICONTROL Esquema de união] O painel exibe o esquema de união para uma classe XDM específica. Ao selecionar a variável **[!UICONTROL Classe]** na lista suspensa, é possível exibir os esquemas de união para diferentes classes XDM.

Os esquemas de união são compostos de vários esquemas que compartilham a mesma classe e foram habilitados para o Perfil. Eles permitem que você veja em uma única visualização, uma combinação de cada campo contido em cada schema que compartilha a mesma classe.

Consulte o guia da interface do usuário do schema de união para saber mais sobre [visualizar esquemas de união na interface do usuário da plataforma](../../profile/ui/union-schema.md#view-union-schemas).

## Widgets e métricas

O painel é composto de widgets, que são métricas somente leitura, fornecendo informações importantes sobre os dados do perfil.

A data e a hora da &quot;última atualização&quot; em um widget mostram quando o último instantâneo dos dados foi tirado. A data e a hora do instantâneo são fornecidas em UTC; não está no fuso horário do usuário individual ou da Organização IMS.

## Widgets padrão

O Adobe fornece vários widgets padrão que podem ser usados para visualizar métricas diferentes relacionadas aos dados do seu perfil. Você também pode criar widgets personalizados para serem compartilhados com sua organização usando o [!UICONTROL Biblioteca de widgets]. Para saber mais sobre a criação de widgets personalizados, comece lendo o [Visão geral da biblioteca de widgets](../customize/widget-library.md).

Para saber mais sobre cada um dos widgets padrão disponíveis, selecione o nome de um widget na seguinte lista:

* [[!UICONTROL Contagem de perfis]](#profile-count)
* [[!UICONTROL Perfis adicionados]](#profiles-added)
* [[!UICONTROL Tendência de adição de perfis]](#profiles-added-trend)
* [[!UICONTROL Perfis por identidade]](#profiles-by-identity)
* [[!UICONTROL Sobreposição de identidade]](#identity-overlap)
* [[!UICONTROL Perfis de identidade única]](#single-identity-profiles)
* [[!UICONTROL Perfis não segmentados]](#unsegmented-profiles)
* [[!UICONTROL Tendência de perfis não segmentados]](#unsegmented-profiles-trend)
* [[!UICONTROL Perfis não segmentados por identidade]](#unsegmented-profiles-by-identity)
* [[!UICONTROL Públicos-alvo]](#audiences)
* [[!UICONTROL Públicos-alvo mapeados para o status de destino]](#audiences-mapped-to-destination-status)
* [[!UICONTROL Tamanho dos públicos-alvo]](#audiences-size)
* [[!UICONTROL Tendência da contagem de perfis]](#profile-count-trend)
* [[!UICONTROL Perfis de identidade únicos por identidade]](#single-identity-profiles-by-identity)
* [[!UICONTROL Sobreposição de público-alvo por política de mesclagem]](#audience-overlap-by-merge-policy)
* [[!UICONTROL Tendência de alteração de contagem de perfis por identidade]](#profiles-count-change-trend-by-identity)

### [!UICONTROL Contagem de perfis] {#profile-count}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_profilecount"
>title="Contagem de perfis"
>abstract="Este widget exibe o número total de perfis mesclados na Loja de perfis no momento em que o instantâneo foi tirado. O número depende da política de mesclagem selecionada que está sendo aplicada aos dados do perfil."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/dashboards/guides/profiles.html#profile-count" text="Saiba mais pela documentação"

O **[!UICONTROL Contagem de perfis]** O widget exibe o número total de perfis mesclados na Loja de perfis no momento em que o instantâneo foi tirado. Esse número é o resultado da política de mesclagem selecionada ser aplicada aos dados do Perfil para unir fragmentos de perfil para formar um único perfil para cada indivíduo.

Consulte a [seção sobre políticas de mesclagem no início deste documento](#merge-policies) para saber mais.

>[!NOTE]
>
>O [!UICONTROL Contagem de perfis] o widget pode mostrar um número diferente da contagem de perfis exibida no [!UICONTROL Procurar] na guia no [!UICONTROL Perfis] da interface do usuário por vários motivos. A razão mais comum para isso é porque a variável [!UICONTROL Procurar] guia faz referência ao número total de perfis mesclados com base na política de mesclagem padrão da organização, enquanto a variável [!UICONTROL Contagem de perfis] O widget faz referência ao número total de perfis mesclados com base na política de mesclagem que você selecionou para exibir no painel.
>
>Outra razão comum é devido às diferenças entre o momento em que o instantâneo do painel é tirado e o momento em que o trabalho de amostra é executado para o [!UICONTROL Procurar] guia . Você pode ver quando a variável [!UICONTROL Contagem de perfis] O widget foi atualizado pela última vez, observando o carimbo de data e hora no widget e para saber mais sobre como o trabalho de amostra é acionado no [!UICONTROL Procurar] consulte a guia [seção contagem de perfis no guia da interface do usuário de perfil do cliente em tempo real](https://experienceleague.adobe.com/docs/experience-platform/profile/ui/user-guide.html?lang=en#profile-count).

![](../images/profiles/profile-count.png)

### [!UICONTROL Perfis adicionados] {#profiles-added}

<!-- This CONTEXTUALHELP was commented out because this widget name will change. Details in https://jira.corp.adobe.com/browse/PLAT-120313  -->

<!-- >[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_profilesadded"
>title="Profiles added"
>abstract="This widget displays the total number of merged profiles **added** to the Profile Store at the time of the last snapshot. The number depends on the selected merge policy being applied to your Profile data."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/dashboards/guides/profiles.html#profiles-added" text="Learn more from documentation" -->

O **[!UICONTROL Perfis adicionados]** O widget exibe o número total de perfis mesclados adicionados à Loja de perfis no momento do último instantâneo. Esse número é o resultado da política de mesclagem selecionada ser aplicada aos dados do Perfil para unir fragmentos de perfil para formar um único perfil para cada indivíduo. Você pode usar o seletor suspenso para exibir os perfis adicionados nos últimos 30 dias, 90 dias ou 12 meses.

>[!NOTE]
>
>O [!UICONTROL Perfis adicionados] O widget reflete o número de perfis adicionados **after** a assimilação de perfil inicial e a configuração da Loja de perfis. Em outras palavras, se sua organização configurar a Loja de perfis e assimilar 4.000.000 no Dia 1, em 24 horas o painel estará disponível, no entanto, a variável [!UICONTROL Perfis adicionados] o widget seria definido como 0. Isso é feito para evitar um pico associado à assimilação inicial de perfis no sistema. Nos próximos 30 dias, sua organização assimilará mais 1.000.000 perfis na Loja de perfis. Depois que o próximo instantâneo for tirado, o [!UICONTROL Perfis adicionados] o widget mostraria um total de 1.000.000 perfis adicionados, enquanto o [!UICONTROL Contagem de perfis] O widget exibiria 5.000.000 perfis totais.

![](../images/profiles/profiles-added.png)

### [!UICONTROL Tendência de adição de perfis] {#profiles-added-trend}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_profilesaddedtrend"
>title="Tendência de adição de perfis"
>abstract="Este widget exibe o número total de perfis mesclados que foram adicionados à Loja de perfis diariamente nos últimos 30 dias, 90 dias ou 12 meses. O número também depende da política de mesclagem selecionada ser aplicada aos dados do perfil."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/dashboards/guides/profiles.html#profiles-count-trend" text="Saiba mais pela documentação"

O **[!UICONTROL Tendência de adição de perfis]** O widget exibe o número total de perfis mesclados que foram adicionados à Loja de perfis diariamente nos últimos 30 dias, 90 dias ou 12 meses. Esse número é atualizado todos os dias quando o instantâneo é tirado. Portanto, se você assimilasse perfis na Platform, o número de perfis não seria refletido até que o próximo instantâneo fosse tirado. A contagem de perfis adicionada é o resultado da política de mesclagem selecionada ser aplicada aos dados do perfil para unir fragmentos de perfil para formar um único perfil para cada indivíduo.

Consulte a [seção sobre políticas de mesclagem no início deste documento](#merge-policies) para saber mais.

O **[!UICONTROL Tendência de adição de perfis]** o widget exibe um botão &quot;legendas&quot; na parte superior direita do widget. Selecionar **[!UICONTROL Legendas]** para abrir a caixa de diálogo de legendas automáticas.

![A guia Visão geral do perfil que exibe o widget de tendência Perfis adicionada com o botão de legendas realçado.](../images/profiles/profiles-added-trend-captions.png)

Um modelo de aprendizado de máquina gera automaticamente legendas para descrever as tendências principais e eventos importantes ao analisar o gráfico e os dados.

![A caixa de diálogo de legendas automáticas do widget de tendência Perfis adicionada.](../images/profiles/profiles-added-trends-automatic-captions-dialog.png)

### [!UICONTROL Perfis por identidade] {#profiles-by-identity}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_profilesbyidentity"
>title="Perfis por identidade"
>abstract="Este widget exibe o detalhamento de todos os perfis mesclados na Loja de perfis por identidades."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/dashboards/guides/profiles.html#profiles-by-identity" text="Saiba mais pela documentação"

O **[!UICONTROL Perfis por identidade]** O widget exibe o detalhamento das identidades em todos os perfis mesclados na Loja de perfis. O número total de perfis por identidade (em outras palavras, adicionar os valores mostrados para cada namespace) pode ser maior que o número total de perfis mesclados, pois um perfil pode ter vários namespaces associados a ele. Por exemplo, se um cliente interagir com sua marca em mais de um canal, vários namespaces serão associados a esse cliente individual.

Consulte a [seção sobre políticas de mesclagem no início deste documento](#merge-policies) para saber mais.

![O painel de visão geral Perfis com o widget Perfis por identidade é destacado.](../images/profiles/profiles-by-identity.png)

Selecionar **[!UICONTROL Legendas]** para abrir a caixa de diálogo de legendas automáticas.

![A caixa de diálogo perfis por legendas de identidade.](../images/profiles/profiles-by-identity-captions.png)

Um modelo de aprendizado de máquina gera automaticamente insights de dados ao analisar a distribuição geral e as principais dimensões dos dados.

Para saber mais sobre identidades, visite o [Documentação do Adobe Experience Platform Identity Service](../../identity-service/home.md).

### [!UICONTROL Sobreposição de identidade] {#identity-overlap}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_identityoverlap"
>title="Sobreposição de identidade"
>abstract="Esse widget usa um diagrama Venn para exibir a sobreposição de perfis na Loja de perfis que contém as duas identidades selecionadas."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/dashboards/guides/profiles.html#identity-overlap" text="Saiba mais pela documentação"

O **[!UICONTROL Sobreposição de identidade]** O widget usa um diagrama Venn ou um diagrama de conjunto para exibir a sobreposição de perfis na Loja de perfis que contém as duas identidades selecionadas.

Use os menus suspensos do widget para selecionar as identidades que deseja comparar. Os círculos exibem a contagem total relativa de perfis que contêm cada identidade. O número de perfis que contém ambas as identidades é representado pelo tamanho da sobreposição entre os círculos. Se um cliente interagir com sua marca em mais de um canal, várias identidades serão associadas a esse cliente individual, portanto, é provável que sua organização tenha vários perfis contendo fragmentos de mais de uma identidade.

Para obter mais informações sobre fragmentos de perfil, comece lendo a seção em [fragmentos de perfil vs. perfis mesclados](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html?lang=en#profile-fragments-vs-merged-profiles) na visão geral do Perfil do cliente em tempo real.

Para saber mais sobre identidades, visite o [Documentação do Adobe Experience Platform Identity Service](../../identity-service/home.md).

![](../images/profiles/identity-overlap.png)

### [!UICONTROL Perfis de identidade única] {#single-identity-profiles}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_singleidentityprofiles"
>title="Perfis de identidade única"
>abstract="Esse widget fornece uma contagem dos perfis de sua organização que têm apenas um tipo de ID que cria sua identidade. Esse tipo de ID pode ser um email ou uma ECID."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/dashboards/guides/profiles.html#single-identity-profiles" text="Saiba mais pela documentação"

O [!UICONTROL Perfis de identidade única] O widget fornece uma contagem dos perfis de sua organização que têm apenas um tipo de ID que cria sua identidade. Esse tipo de ID pode ser um email ou uma ECID. A contagem de perfis é gerada a partir dos dados contidos no instantâneo mais recente.

![Dispositivo Perfis de identidade única.](../images/profiles/single-identity-profiles.png)

### [!UICONTROL Perfis não segmentados] {#unsegmented-profiles}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_unsegmentedprofiles"
>title="Perfis não segmentados"
>abstract="Este widget fornece o número total de perfis não anexados a nenhum segmento e representa a oportunidade para a ativação de perfil em sua organização."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/dashboards/guides/profiles.html#unsegmented-profiles" text="Saiba mais pela documentação"

O [!UICONTROL Perfis não segmentados] O widget fornece o número total de perfis não anexados a nenhum segmento. O número gerado é preciso a partir do último instantâneo e representa a oportunidade para a ativação do perfil em toda a organização. Também indica a oportunidade de explorar perfis que não fornecem ROI adequado.

![O widget Perfis não segmentados.](../images/profiles/unsegmented-profiles.png)

### [!UICONTROL Tendência de perfis não segmentados] {#unsegmented-profiles-trend}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_unsegmentedprofilestrend"
>title="Tendência de perfis não segmentados"
>abstract="Este widget fornece uma ilustração de gráfico de linhas para o número de perfis que não estão anexados a nenhum segmento em um determinado período de tempo. A tendência dos perfis não anexados a nenhum segmento pode ser visualizada ao longo de períodos de 30 dias, 90 dias e 12 meses."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/dashboards/guides/profiles.html#unsegmented-profiles-trend" text="Saiba mais pela documentação"

O [!UICONTROL Tendência de perfis não segmentados] O widget fornece uma ilustração de gráfico de linhas para o número de perfis que não estão anexados a nenhum segmento em um determinado período. A tendência dos perfis não anexados a nenhum segmento pode ser visualizada ao longo de períodos de 30 dias, 90 dias e 12 meses. O período é escolhido em um menu suspenso no widget. A contagem de perfis é refletida no eixo y e no tempo no eixo x.

![O widget Tendência de perfis não segmentados.](../images/profiles/unsegmented-profiles-trend.png)

### [!UICONTROL Perfis não segmentados por identidade] {#unsegmented-profiles-by-identity}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_unsegmentedprofilesbyidentity"
>title="Perfis não segmentados por identidade"
>abstract="Esse widget categoriza o número total de perfis não segmentados por seu identificador exclusivo."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/dashboards/guides/profiles.html#unsegmented-profiles-by-identity" text="Saiba mais pela documentação"

O [!UICONTROL Perfis não segmentados por identidade] O widget categoriza o número total de perfis não segmentados por seu identificador exclusivo. Os dados são visualizados em um gráfico de barras para facilitar a comparação.

![O widget Perfis não segmentados por identidade.](../images/profiles/unsegmented-profiles-by-identity.png)

### [!UICONTROL Públicos-alvo] {#audiences}

Este widget fornece o número total de segmentos prontos para serem ativados, de acordo com a política de mesclagem escolhida aplicada aos dados do seu perfil.

Selecionar **[!UICONTROL Públicos-alvo]** para navegar até o [!UICONTROL Segmentos] painel [!UICONTROL Procurar] guia . A partir daí, você pode ver uma lista de todas as definições de segmentos para sua organização.

![O widget Públicos-alvo .](../images/profiles/audiences.png)

<!-- https://jira.corp.adobe.com/browse/PLAT-115291 -->

<!-- * [[!UICONTROL Audiences change trend]](#audiences-change-trend) -->
<!-- ### [!UICONTROL Audiences change trend] {#audiences-change-trend}

This line graph widget visualizes the change in the total number of audiences each day, trending over time. The change in the number of audiences is dependent on the selected merge policy being applied to your profile data. The period of analysis is selected from the widget dropdown menu. The bar chart can be visualized over 30 days, 90 days, and 12-month periods.  

The visualization allows you to monitor the overall health of audiences within Adobe Experience Platform by understanding trends in the growth or decline of the total number of audiences. -->

<!-- ![The Audiences change trend widget.]() -->

<!-- * [[!UICONTROL Audience overlap report]](#audience-overlap-report) -->
<!-- ### [!UICONTROL Audience overlap report] {#audience-overlap-report} -->

<!-- View an ordered list of audiences by highest or lowest overlap percentages by selected merge policy. -->
<!-- ![The Audiences overlap report widget.]() -->
<!-- https://jira.corp.adobe.com/browse/PLAT-126851 -->

### [!UICONTROL Públicos-alvo mapeados para o status de destino] {#audiences-mapped-to-destination-status}

O [!UICONTROL Públicos-alvo mapeados para o status de destino] O widget exibe o número total de públicos-alvo mapeados e não mapeados em uma única métrica e usa um gráfico de rosca para ilustrar a diferença proporcional entre seus totais. Os números calculados dependem da política de mesclagem escolhida.

As contagens individuais de públicos-alvo mapeados ou não são exibidas em uma caixa de diálogo quando o cursor passa o mouse sobre a respectiva seção do gráfico de rosca.

![Os públicos-alvo mapeados para o widget de status de destino.](../images/profiles/audiences-mapped-to-destination-status.png)

### [!UICONTROL Tamanho dos públicos-alvo] {#audiences-size}

O [!UICONTROL Tamanho dos públicos-alvo] O widget fornece uma tabela de duas colunas que lista até 20 segmentos e o número total de públicos-alvo contidos em cada segmento. A lista é solicitada de alto para baixo de acordo com o número total de públicos-alvo. O número total de tamanho do público-alvo depende da política de mesclagem aplicada.

![O widget de tamanho Públicos-alvo.](../images/profiles/audiences-size.png)

Para ver informações abrangentes sobre um segmento, selecione um nome de segmento na lista fornecida para navegar até a [!UICONTROL Segmentos] [!UICONTROL Detalhe] página. Além disso, selecionando **[!UICONTROL Exibir todos os segmentos]** a partir do fim do widget, você pode navegar até o [!UICONTROL Segmentos] [!UICONTROL Procurar] para localizar qualquer segmento existente.

![O widget de tamanho de Públicos-alvo com um nome de segmento e o texto de todos os segmentos destacado.](../images/profiles/audiences-size-view-all-segments.png)

Consulte a documentação para obter mais informações sobre o [[!UICONTROL Segmentos] [!UICONTROL  Procurar] guia](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/overview.html#browse).

### [!UICONTROL Tendência da contagem de perfis] {#profile-count-trend}

O [!UICONTROL Tendência da contagem de perfis] O widget usa um gráfico de linhas para ilustrar a tendência no número total de perfis contidos no sistema ao longo do tempo. Esse número total inclui todos os perfis importados para o sistema desde o último instantâneo diário. Os dados podem ser visualizados por períodos de 30 dias, 90 dias e 12 meses. O período é escolhido em um menu suspenso no widget.

![O widget de tendência de contagem de perfis.](../images/profiles/profile-count-trend.png)

### [!UICONTROL Perfis de identidade únicos por identidade] {#single-identity-profiles-by-identity}

Esse widget usa um gráfico de barras para ilustrar o número total de perfis identificados com apenas um único identificador exclusivo. O widget suporta até cinco das identidades mais comuns.

Passe o mouse sobre barras individuais para ver uma caixa de diálogo que detalha a contagem total de perfis de uma identidade.

![Os perfis de identidade única por widget de identidade.](../images/profiles/single-identity-profiles-by-identity.png)

### [!UICONTROL Sobreposição de público-alvo por política de mesclagem] {#audience-overlap-by-merge-policy}

Esse widget usa um diagrama Venn para exibir a sobreposição de dois segmentos selecionados. A política de mesclagem é escolhida na lista suspensa de visão geral na parte superior da página e os segmentos para análise são selecionados em dois menus suspensos no widget. O número total de perfis contidos na definição de segmento relevante pode ser visualizado ao passar o mouse sobre um círculo ou a interseção.

À medida que o widget exibe a cruz visual das definições de segmento, você pode otimizar sua estratégia de segmentação estudando semelhanças entre as definições de segmento.

![O painel Perfis da interface do usuário da plataforma com a lista suspensa de política de mesclagem e os menus suspensos do segmento de widget são realçados.](../images/profiles/audience-overlap-by-merge-policy.png)

### [!UICONTROL Tendência de alteração de contagem de perfis por identidade] {#profiles-count-change-trend-by-identity}

<!-- This widget uses a line graph to illustrate the change in number of profiles filtered by a chosen source identity and merge policy. -->

Esse widget filtra a contagem de perfis com base na identidade de origem selecionada e na política de mesclagem, e ilustra a alteração no número para uma variedade de períodos usando um gráfico de linhas. A política de mesclagem é selecionada na lista suspensa visão geral na parte superior da página, a identidade de origem e o período de tempo são selecionados nos menus suspensos do widget. A tendência pode ser visualizada por períodos de 30 dias, 90 dias e 12 meses.

Este widget ajuda você a gerenciar suas necessidades de ativação de destino demonstrando o padrão de crescimento de perfis filtrados por uma identidade necessária.

![Os Perfis contam a tendência de alteração por widget de identidade.](../images/profiles/profiles-count-change-trend-by-identity.png)


## (Beta) Widgets de eficácia do perfil {#profile-efficacy-widgets}

>[!IMPORTANT]
>
>Os widgets de eficácia do perfil estão atualmente em Beta e não estão disponíveis para todos os usuários. A documentação e a funcionalidade estão sujeitas a alterações.

O Adobe fornece vários widgets para avaliar a integridade dos perfis assimilados disponíveis para a análise de dados. Cada um dos widgets de eficácia do perfil pode ser filtrado pela política de mesclagem. Para alterar o filtro de política de mesclagem, selecione o[!UICONTROL Perfis usando política de mesclagem] e escolha a política apropriada na lista disponível.

Para saber mais sobre cada um dos widgets de eficácia de perfil, selecione o nome de um widget na seguinte lista:

* [[!UICONTROL Avaliação da qualidade dos atributos]](#attributes-quality-assessment)
* [[!UICONTROL Perfis por integridade]](#profiles-by-completeness)
* [[!UICONTROL Tendência de integridade de perfis]](#profiles-completeness-trend)

### (Beta) [!UICONTROL Atributos da avaliação da qualidade] {#attributes-quality-assessment}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_attributesqualityassessment"
>title="Atributos da avaliação da qualidade"
>abstract="Este widget mostra a integridade e cardinalidade de todos os perfis de acordo com seus atributos. Cada linha descreve um atributo. O **Perfis** fornece o número de perfis que têm esse atributo e são preenchidos com valores não nulos. O **Integridade** a porcentagem é determinada pelo número total de perfis que têm esse atributo e são preenchidos com valores não nulos dividido pelo número total de valores não vazios nos perfis desse atributo. **Cardinalidade** O fornece o número total de valores não nulos exclusivos desse atributo em todos os atributos."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/dashboards/guides/profiles.html#attributes-quality-assessment" text="Saiba mais pela documentação"

O [!UICONTROL Avaliação da qualidade dos atributos] O widget mostra a integridade e cardinalidade de todos os perfis de acordo com seus atributos. Os dados são precisos para a data do último processamento. Essas informações são apresentadas como uma tabela com quatro colunas, onde cada linha na tabela representa um único atributo.

| Coluna | Descrição |
|---|---|
| Atributo | O nome do atributo. |
| Perfis | O número de perfis que têm esse atributo e são preenchidos com valores não nulos. |
| Integridade | Essa porcentagem é determinada pelo número total de perfis que têm esse atributo e são preenchidos com valores não nulos. O número é calculado dividindo o número total de perfis pelo número total de valores que não estão vazios nos perfis desse atributo. |
| Cardinalidade | O número total de **único** valores não nulos deste atributo. Ele é medido em todos os perfis. |

![O widget de avaliação da qualidade dos atributos](../images/profiles/attributes-quality-assessment.png)

### (Beta) [!UICONTROL Perfis por integridade] {#profiles-by-completeness}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_profilesbycompleteness"
>title="Perfis por integridade"
>abstract="O gráfico de rosca exibe a porcentagem de atributos de perfil preenchidos com valores não nulos entre todos os atributos observados. Ele ilustra a proporção de perfis que são de alta, média ou baixa integridade. Perfis de alta integridade têm mais de 70% de seus atributos preenchidos. Os perfis de integridade média têm entre 30% e 70% de seus atributos preenchidos. Os perfis de baixa integridade têm menos de 30% dos atributos preenchidos."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/dashboards/guides/profiles.html#profile-completeness" text="Saiba mais pela documentação"

O [!UICONTROL Perfis por integridade] o widget cria um gráfico de rosca de integridade de perfil desde a última data de processamento. A integridade de um perfil é medida pela porcentagem de atributos preenchidos com valores não nulos entre todos os atributos observados.

Este widget mostra a proporção de perfis que são de alta, média ou baixa integridade. Por padrão, há três níveis de integridade configurados:

* Alta integridade: Os perfis têm mais de 70% dos atributos preenchidos.
* Integridade média: Perfis têm entre 30% e 70% de seus atributos preenchidos.
* Baixa integridade: Os perfis têm menos de 30% dos atributos preenchidos.

![Os perfis por widget de integridade](../images/profiles/profiles-by-completeness.png)

### (Beta) [!UICONTROL Tendência de integridade de perfis] {#profiles-completeness-trend}

>[!CONTEXTUALHELP]
>id="platform_dashboards_profiles_profilescompletenesstrend"
>title="Tendência de integridade de perfis"
>abstract="Este widget cria um gráfico de área empilhada para descrever a tendência da integridade do perfil ao longo do tempo. A integridade é medida pela porcentagem de atributos que são preenchidos com valores não nulos entre todos os atributos observados."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/dashboards/guides/profiles.html#profile-completeness-trend" text="Saiba mais pela documentação"

Este widget cria um gráfico de área empilhada para descrever a tendência da integridade do perfil ao longo do tempo. A integralidade é medida pela porcentagem de atributos preenchidos com valores não nulos entre todos os atributos observados. Ele classifica a integridade do perfil como alta, média ou baixa desde a última data de processamento.

O eixo x representa o tempo, o eixo y representa o número de perfis e as cores representam os três níveis de integridade do perfil.

Os três níveis de integridade são:

* Alta integridade: Os perfis têm mais de 70% dos atributos preenchidos.
* Integridade média: Os perfis têm menos de 70% e mais de 30% dos atributos preenchidos.
* Baixa integridade: Os perfis têm menos de 30% dos atributos preenchidos.

![O widget de tendência de integridade de perfis](../images/profiles/profiles-completeness-trend.png)

## Próximas etapas

Agora, ao seguir este documento, você pode localizar o painel Perfis e entender as métricas exibidas nos widgets disponíveis. Para saber mais sobre como trabalhar com a [!DNL Profile] na interface do usuário do Experience Platform, consulte o [Guia da interface do usuário do perfil do cliente em tempo real](../../profile/ui/user-guide.md).
