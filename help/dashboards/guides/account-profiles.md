---
title: Painel de perfis de conta
description: A Adobe Experience Platform fornece um painel por meio do qual você pode visualizar informações importantes sobre os perfis de conta B2B da sua organização.
exl-id: c9a3d786-6240-4ba4-96c8-05f658e1150c
source-git-commit: 4f67df5d3667218c79504535534de57f871b0650
workflow-type: tm+mt
source-wordcount: '1675'
ht-degree: 1%

---

# [!UICONTROL Perfis de conta] painel

A interface do usuário (UI) do Adobe Experience Platform fornece um painel por meio do qual você pode visualizar informações importantes sobre os perfis de conta, conforme capturados durante um instantâneo diário. Este guia descreve como acessar e trabalhar com a [!UICONTROL Perfis de conta] painel na interface do usuário e fornece mais informações sobre as visualizações exibidas no painel.

Este documento fornece uma visão geral dos recursos da [!UICONTROL Perfis de conta] e detalha os insights padrão disponíveis. Consulte a [[!UICONTROL Perfis de conta] Guia da interface do usuário](../../rtcdp/accounts/account-profile-ui-guide.md) para obter detalhes abrangentes sobre os recursos disponíveis.

## Introdução

Você deve ter direito a [Adobe Real-time Customer Data Platform B2B Edition](../../rtcdp/b2b-overview.md) para acessar o B2B [!UICONTROL Perfis de conta] painel.

## Dados de perfis de conta {#data}

A variável [!UICONTROL Perfis de conta] O painel exibe um instantâneo das informações unificadas da conta. Essas informações de conta vêm de várias fontes em seus canais de marketing e dos diversos sistemas que sua organização usa atualmente para armazenar informações de conta do cliente.

Os dados do perfil no instantâneo mostram os dados exatamente como aparecem no momento específico em que o instantâneo foi tirado. Em outras palavras, o instantâneo não é uma aproximação ou uma amostra dos dados, e o [!UICONTROL Perfis de conta] O painel do não é atualizado em tempo real.

>[!NOTE]
>
>Quaisquer alterações ou atualizações feitas nos dados desde que o instantâneo foi tirado não serão refletidas no painel até que o próximo instantâneo seja tirado.

## Explore o [!UICONTROL Perfis de conta] painel {#explore}

Para navegar até o [!UICONTROL Perfis de conta] no painel da interface do Platform, selecione **[!UICONTROL Perfis]** em [!UICONTROL Contas] no painel de navegação esquerdo.

![A interface do usuário da Platform com Perfis de conta na navegação à esquerda é realçada e a guia Visão geral é exibida.](../images/account-profiles/account-profiles-dashboard.png)

No [!UICONTROL Perfis de conta] painel de controle, você pode [procure os perfis de conta assimilados em sua organização](#browse-account-profiles)ou [visualizar todos os dados do perfil da sua conta rapidamente usando widgets](#standard-widgets).

### Filtro de data {#date-filter}

A variável [!UICONTROL Visão geral] A guia é composta de widgets que fornecem métricas somente leitura para transmitir informações importantes sobre os perfis da sua conta. Selecione o ícone ou as datas do calendário para alterar o filtro de datas global dos seus widgets.

>[!IMPORTANT]
>
>O intervalo de datas selecionado no calendário suspenso afeta todos os insights, exceto os dois widgets de pontuação preditiva ([distribuição](#predictive-scoring-distribution) e [principais fatores influentes](#predictive-scoring-top-influential-factors)).

![A guia de visão geral Perfis de conta com o seletor de datas e o ícone de filtro destacados.](../images/account-profiles/date-filter.png)

### Configurar o cliente potencial para o serviço de correspondência de contas {#lead-to-account-matching-service}

Selecionar **[!UICONTROL Configurações]** para configurar o cliente em potencial para o serviço de correspondência de contas no [!UICONTROL Configurações da conta] diálogo. Para obter detalhes completos sobre como configurar seu lead para correspondência de contas, consulte a [Guia da interface do usuário](../../rtcdp/accounts/account-profile-ui-guide.md#configure-lead-to-account-matching). Para saber mais sobre correspondência entre lead e conta, consulte a [levar à correspondência de contas na documentação B2B do Real-Time CDP](../../rtcdp/b2b-ai-ml-services/lead-to-account-matching.md).

![O painel Perfis de conta com Configurações realçadas.](../images/account-profiles/settings.png)

## Procurar perfis de conta {#browse-account-profiles}

No [!UICONTROL Procurar] você pode pesquisar e visualizar os perfis de conta somente leitura assimilados em sua organização. Use uma ID de conta de uma fonte corporativa conectada ou insira os detalhes da fonte diretamente. Nesse espaço de trabalho, você pode ver informações importantes pertencentes ao perfil da conta, incluindo nome, setor, receita e público-alvo, entre outros.

Selecione o [!UICONTROL ID do perfil] a partir dos resultados exibidos no [!UICONTROL Procurar] para abrir a guia [!UICONTROL Detalhes] para o perfil da conta.

![A guia de navegação Perfis de conta com os resultados exibidos e a ID do perfil destacada.](../images/account-profiles/account-profiles-browse-tab.png)

As informações de perfil da conta exibidas na variável [!UICONTROL Detalhes] A guia foi mesclada de vários fragmentos de perfil para formar uma única visualização da conta individual. Consulte a documentação em [procurar perfis de conta no Adobe Real-time Customer Data Platform](../../rtcdp/accounts/account-profile-ui-guide.md#browse-account-profiles) para saber mais sobre os recursos de visualização de perfil da conta na interface do usuário da plataforma.

## Widgets padrão {#standard-widgets}

O Adobe fornece widgets padrão que você pode usar para visualizar métricas diferentes relacionadas aos seus perfis de conta.

>[!IMPORTANT]
>
>Se você não fornecer um filtro de datas, o comportamento padrão dos insights analisará os dados adicionados do ano anterior até hoje.

Para saber mais sobre cada um dos widgets padrão disponíveis, selecione o nome de um widget na lista a seguir:

* [Perfis de conta adicionados](#account-profiles-added)
* [Novas contas por setor](#accounts-by-industry)
* [Novas contas por tipo](#accounts-by-type)
* [Novas oportunidades por função de pessoa](#opportunities-by-person-role)
* [Novas oportunidades por receita](#opportunities-by-revenue)
* [Novas oportunidades por status e estágio](#opportunities-by-status-&-stage)
* [Novas oportunidades conquistadas](#opportunities-won)
* [Oportunidades adicionadas](#opportunities-added)
* [Distribuição de pontuação preditiva](#predictive-scoring-distribution)
* [Principais fatores influentes da pontuação preditiva](#predictive-scoring-top-influential-factors)

### Perfis de conta adicionados {#account-profiles-added}

A variável [!UICONTROL Perfis de conta adicionados] O widget usa um gráfico de linhas para exibir o número de perfis de conta adicionados a cada dia durante um período. Use o filtro de data global localizado na parte superior do painel para determinar o período de análise. Se nenhum filtro de data for fornecido, o comportamento padrão listará os perfis de conta adicionados para o ano anterior a hoje. Os resultados podem ser usados para inferir uma tendência no número de perfis de conta adicionados.

![O widget Perfis de conta foram adicionados.](../images/account-profiles/account-profiles-added.png)

### Novas contas por setor {#accounts-by-industry}

A variável [!UICONTROL Novas contas por setor] exibe o número total de contas em uma única métrica dentro de um gráfico de rosca. O gráfico de rosca ilustra a composição relativa de diferentes setores que compõem esse total. Uma chave codificada por cores fornece um detalhamento de todos os setores incluídos. As contagens individuais de cada setor são exibidas em uma caixa de diálogo quando o cursor passa o mouse sobre a respectiva seção do gráfico de rosca.

![O widget Novas contas por setor.](../images/account-profiles/new-accounts-by-industry.png)

### Novas contas por tipo {#accounts-by-type}

A variável [!UICONTROL Novas contas por tipo] exibe o número total de contas em uma única métrica dentro de um gráfico de rosca. O gráfico de rosca ilustra a composição relativa de diferentes tipos de conta que compõem esse total. Uma chave com código de cores fornece um detalhamento de todos os tipos de conta incluídos. As contagens individuais de cada tipo de conta são exibidas em uma caixa de diálogo quando o cursor passa o mouse sobre a respectiva seção do gráfico de rosca.

![O widget Novas contas por tipo.](../images/account-profiles/new-accounts-by-type.png)

### Novas oportunidades por função de pessoa {#opportunities-by-person-role}

A variável [!UICONTROL Novas oportunidades por função de pessoa] O widget exibe o número total de suas oportunidades em uma única métrica dentro de um gráfico de rosca. O gráfico de rosca ilustra a composição relativa de funções que compõem esse número total de oportunidades. Uma chave codificada por cores fornece um detalhamento de todas as funções incluídas. As contagens individuais de cada função são exibidas em uma caixa de diálogo quando o cursor passa o mouse sobre a respectiva seção do gráfico de rosca.

>[!NOTE]
>
>A variável [!UICONTROL Nenhum dado encontrado] ou [!UICONTROL Não foi possível carregar] O erro é causado quando a tabela de ponte &quot;Oportunidade-Pessoa&quot; não é usada no esquema. Se o seu insight exibir um desses erros, verifique o esquema de união e verifique se o grupo de campos &quot;Oportunidade-Pessoa&quot; está assimilando dados.

![O widget Novas oportunidades por função de pessoa.](../images/account-profiles/new-opportunities-by-person-role.png)

### Novas oportunidades por receita {#opportunities-by-revenue}

A variável [!UICONTROL Novas oportunidades por receita] O widget usa um gráfico de barras para ilustrar a quantidade total estimada de receita gerada por suas oportunidades. O widget suporta até seis oportunidades.

Para ver uma caixa de diálogo que contém o total de receita específico de uma oportunidade, use o cursor para passar o mouse sobre barras individuais.

![O widget Novas oportunidades por receita.](../images/account-profiles/new-opportunities-by-revenue.png)

### Novas oportunidades por status e estágio {#opportunities-by-status-&-stage}

Esse widget usa um gráfico de barras para ilustrar o número de oportunidades que estão abertas ou fechadas em todos os estágios do funil de marketing/vendas. O widget usa cores para diferenciar o estágio das oportunidades. Uma chave codificada por cores indica os estágios disponíveis para oportunidades.

![O widget Novas oportunidades por status e estágio.](../images/account-profiles/new-opportunities-by-status-&-stage.png)

### Novas oportunidades conquistadas {#opportunities-won}

A variável [!UICONTROL Novas oportunidades conquistadas] O widget exibe o número total de oportunidades que foram finalizadas com êxito em uma única métrica dentro de um gráfico de rosca. O gráfico de rosca ilustra a composição relativa de oportunidades que são ganhas ou não. Uma chave codificada por cores distingue entre oportunidades ganhas e não ganhas. As contagens individuais de cada função são exibidas em uma caixa de diálogo quando o cursor passa o mouse sobre a respectiva seção do gráfico de rosca.

![Widget de Novas oportunidades ganhas.](../images/account-profiles/new-opportunities-won.png)

### Oportunidades adicionadas {#opportunities-added}

A variável [!UICONTROL Oportunidades adicionadas] O widget usa um gráfico de linhas para exibir o número de oportunidades adicionadas a cada dia durante um período. Use o filtro de data global localizado na parte superior do painel para determinar o período de análise. Se nenhum filtro de data for fornecido, o comportamento padrão listará as oportunidades adicionadas para o ano anterior a hoje. Os resultados podem ser usados para inferir uma tendência no número de oportunidades adicionadas.

<!-- Link to date filter documentation from Annamalai -->

![O widget Oportunidades adicionadas.](../images/account-profiles/opportunities-added.png)

### Distribuição de pontuação preditiva {#predictive-scoring-distribution}

A variável [!UICONTROL Distribuição de pontuação preditiva] O widget mostra a distribuição de pontuação de todos os perfis de conta para ajudar você a entender rapidamente a integridade do pipeline de vendas. Os dados de pontuação são transmitidos por um gráfico de rosca e um gráfico de coluna.

O gráfico de rosca ilustra a proporção do total de perfis de conta em cada um dos segmentos de alta, média e baixa propensão para compra. A tecla fornece mais detalhes sobre as seções codificadas por cores, incluindo os intervalos do intervalo de classificação de pontuação e o número de perfis de conta nesse intervalo.

O gráfico de colunas fornece um detalhamento de pontuação mais granular. Cada coluna mostra o número de perfis de conta em cada um dos 20 intervalos de incremento de cinco pontos.

O menu suspenso no widget permite selecionar o modelo de pontuação da conta.

>[!NOTE]
>
>Os filtros de intervalo de datas global não se aplicam aos insights de pontuação preditiva. Os widgets de pontuação preditiva analisam dados com base no modelo de pontuação de conta selecionado na lista suspensa.

![O widget de distribuição Pontuação preditiva.](../images/account-profiles/predictive-scoring-distribution.png)

### Principais fatores influentes da pontuação preditiva {#predictive-scoring-top-influential-factors}

A variável [!UICONTROL Principais fatores influentes da pontuação preditiva] O widget ajuda você a entender os fatores mais significativos que determinam as pontuações para cada intervalo de propensão.

Este widget mostra os principais fatores influentes para cada um dos intervalos de alta, média e baixa propensão. Uma barra para cada fator influente indica a porcentagem dos perfis de conta nesse intervalo de propensão que contém o fator influente específico.

O menu suspenso no widget permite selecionar o modelo de pontuação da conta.

>[!NOTE]
>
>Os filtros de intervalo de datas global não se aplicam aos insights de pontuação preditiva. Os widgets de pontuação preditiva analisam dados com base no modelo de pontuação de conta selecionado na lista suspensa.

![O widget Principais fatores influentes da pontuação preditiva.](../images/account-profiles/predictive-scoring-top-influential-factors.png)

## Próximas etapas

Ao seguir este documento, agora você deve saber como localizar o [!UICONTROL Perfis de conta] e também entendem as métricas exibidas nos widgets disponíveis. Para saber mais sobre como trabalhar com perfis de conta como parte de seus dados B2B na interface do usuário do Experience Platform, consulte o [visão geral dos perfis de conta](../../rtcdp/accounts/account-profile-overview.md) para o Adobe Real-Time CDP, B2B Edition.
