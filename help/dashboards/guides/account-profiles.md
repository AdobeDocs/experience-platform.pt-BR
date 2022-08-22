---
title: Guia do painel Perfis da conta
description: O Adobe Experience Platform fornece um painel pelo qual você pode visualizar informações importantes sobre os perfis da conta B2B de sua organização.
exl-id: c9a3d786-6240-4ba4-96c8-05f658e1150c
source-git-commit: 05e63064dc8eb3f070a383f508cc4a86d4f5e9cc
workflow-type: tm+mt
source-wordcount: '823'
ht-degree: 0%

---

# [!UICONTROL Perfis de conta] painel

A interface do usuário do Adobe Experience Platform (UI) fornece um painel através do qual você pode visualizar informações importantes sobre seus perfis de conta, conforme capturado durante um instantâneo diário. Este guia descreve como acessar e trabalhar com a [!UICONTROL Perfis de conta] painel na interface do usuário e fornece mais informações sobre as visualizações exibidas no painel.

Para obter uma visão geral de todos os recursos na interface do usuário do perfil da conta, visite o [guia da interface do usuário do perfil da conta](../../rtcdp/accounts/account-profile-ui-guide.md).

## Introdução

Você deve ter direito a [Real-time Customer Data Platform B2B Edition](../../rtcdp/b2b-overview.md) para ter acesso ao B2B [!UICONTROL Perfis de conta] painel.

## Dados de perfis de conta

O [!UICONTROL Perfis de conta] O painel exibe um instantâneo das informações de conta unificadas de várias fontes em seus canais de marketing e os diversos sistemas que sua organização usa atualmente para armazenar informações de conta do cliente.

Os dados do perfil no instantâneo mostram os dados exatamente como aparecem no ponto específico do tempo em que o instantâneo foi tirado. Por outras palavras, o instantâneo não é uma aproximação ou amostra dos dados, e o [!UICONTROL Perfis de conta] O painel não é atualizado em tempo real.

>[!NOTE]
>
>Quaisquer alterações ou atualizações feitas nos dados desde que o instantâneo foi tirado não serão refletidas no painel até que o próximo instantâneo seja tirado.

## Explore o [!UICONTROL Perfis de conta] painel

Para navegar até o [!UICONTROL Perfis de conta] no painel da interface do usuário da plataforma, selecione **[!UICONTROL Perfis]** under [!UICONTROL Contas] no painel de navegação esquerdo.

![A interface do usuário da plataforma com perfis de conta na navegação à esquerda é realçada e a guia de visão geral é exibida.](../images/account-profiles/account-profiles-dashboard.png)

No [!UICONTROL Perfis de conta] no painel você pode [navegue pelos perfis de conta assimilados em sua organização](#browse-account-profiles)ou [exibir todos os dados de perfil da conta imediatamente usando widgets](#standard-widgets) que visualizam aspectos dos dados.

## Procurar perfis de conta {#browse-account-profiles}

O [!UICONTROL Procurar] permite pesquisar e exibir os perfis de conta somente leitura assimilados em sua organização usando uma ID de conta de uma fonte corporativa conectada ou inserindo diretamente os detalhes da origem. Aqui você pode ver informações importantes pertencentes ao perfil da conta, incluindo o nome, o setor, a receita e o segmento, entre outros.

Selecione o [!UICONTROL ID do perfil] dos resultados exibidos na [!UICONTROL Procurar] para abrir o [!UICONTROL Detalhes] para o perfil da conta.

![Os Perfis de conta navegam na guia com os resultados exibidos e a ID de perfil é realçada.](../images/account-profiles/account-profiles-browse-tab.png)

As informações do perfil da conta exibidas no [!UICONTROL Detalhes] A guia foi unida de vários fragmentos de perfil para formar uma única visualização da conta individual. Consulte a documentação em [navegar pelos perfis da conta no Real-time Customer Data Platform](../../rtcdp/accounts/account-profile-ui-guide.md#browse-account-profiles) para saber mais sobre os recursos de visualização do perfil da conta na interface do usuário da plataforma.

## O [!UICONTROL Perfis de conta] [!UICONTROL Visão geral] {#overview}

O [!UICONTROL Visão geral] A guia é composta de widgets que fornecem métricas somente leitura para transmitir informações importantes sobre os perfis da sua conta. Selecionar **[!UICONTROL Modificar painel]** para alterar a aparência do [!UICONTROL Visão geral] movendo e redimensionando widgets.

![A guia Account Profiles overview com o painel Modificar é realçada.](../images/account-profiles/modify-dashboard.png)

Consulte o documento em [modificação de painéis](../customize/modify.md) e [Visão geral da biblioteca de widgets](../customize/widget-library.md) para saber mais.

## Widgets padrão {#standard-widgets}

O Adobe fornece widgets padrão que podem ser usados para visualizar métricas diferentes relacionadas aos perfis de sua conta.

Para saber mais sobre cada um dos widgets padrão disponíveis, selecione o nome de um widget na seguinte lista:

* [Total das contas por ramo de atividade](#total-accounts-by-industry)
* [Perfis de conta adicionados](#account-profiles-added)

### Total das contas por ramo de atividade {#total-accounts-by-industry}

Esse widget exibe o número total de contas em uma única métrica e usa um gráfico de rosca para ilustrar os tamanhos proporcionais de contagens para os setores que compõem o número geral. A chave fornece informações de codificação de cores para os diferentes setores que compõem o gráfico de rosca.

As contagens individuais para os diferentes setores são exibidas em uma caixa de diálogo quando o cursor passa o mouse sobre a respectiva seção do gráfico de rosca.

![O total de contas por widget do setor.](../images/account-profiles/total-accounts-by-industry-widget.png)

### Perfis de conta adicionados {#account-profiles-added}

Esse widget usa um gráfico de barras codificadas por cores para ilustrar a contagem de perfis adicionados a uma conta em um determinado período e a proporção de setores diferentes que constituem esses perfis adicionados. Os setores são codificados por cores e uma tecla fornece as informações de codificação por cores para os diferentes setores que compõem o gráfico de barras. O período de análise é selecionado no menu suspenso do widget. O gráfico de barras pode ser visualizado em um período de 30 dias, 90 dias e 12 meses.

>[!NOTE]
>
>Como os perfis são adicionados a uma conta e nunca são removidos, o número mais baixo possível de perfis adicionados durante um período é zero.

![Os perfis de conta adicionaram o widget.](../images/account-profiles/accounts-profiles-added-widget.png)

## Próximas etapas

Agora, ao seguir este documento, é possível localizar a variável [!UICONTROL Perfis de conta] painel. Você também deve entender as métricas exibidas nos widgets disponíveis. Para saber mais sobre como trabalhar com perfis de conta como parte dos dados B2B na interface do usuário do Experience Platform, consulte o [visão geral dos perfis da conta](../../rtcdp/accounts/account-profile-overview.md) para Adobe Real-Time CDP, B2B Edition.
