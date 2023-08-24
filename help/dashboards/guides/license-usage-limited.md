---
keywords: Experience Platform;interface do usuário;UI;personalização;uso de licença painel;painel;uso de licença;direito;consumo
title: Guia do Painel de Uso da Licença
description: A Adobe Experience Platform fornece um painel por meio do qual você pode visualizar informações importantes sobre o uso de licença da sua organização.
type: Documentation
hide: true
hidefromtoc: true
source-git-commit: 25f57b1bfbcb2ec95f88afb69386a10deb600125
workflow-type: tm+mt
source-wordcount: '1495'
ht-degree: 1%

---

# Painel de uso da licença (versão limitada) {#license-usage-dashboard-limited-release}

>[!IMPORTANT]
>
>A atualização [!UICONTROL Uso da licença] o painel está disponível atualmente em um **somente versão limitada** e não está disponível para todos os clientes.

Você pode exibir informações importantes sobre o uso de licenças da sua organização por meio da Adobe Experience Platform [!UICONTROL Uso da licença] painel. As informações exibidas aqui são capturadas durante um instantâneo diário da sua instância da Platform.

Os relatórios de uso de licença fornecem um alto grau de granularidade em relação às métricas de uso de licença. O painel fornece métricas de uso para cada produto comprado, o uso consolidado de métricas em todas as sandboxes de produção ou desenvolvimento e a métrica de uso de uma sandbox específica. Os aplicativos de Experience Platform a seguir podem ser rastreados com métricas de uso: Perfil de dados do cliente em tempo real, Adobe Journey Optimizer e Customer Journey Analytics.

Este guia descreve como acessar e trabalhar com o painel de uso de licença na interface do usuário e fornece mais informações sobre as visualizações exibidas no painel.

Para obter uma visão geral da interface do usuário da Platform, consulte o [Guia da interface de usuário do Experience Platform](../../landing/ui-guide.md).

## [!UICONTROL Uso da licença] dados do painel

A variável [!UICONTROL Uso da licença] painel exibe uma lista de todos os produtos Experience Platform que você adquiriu. Nessa lista, você pode encontrar um instantâneo dos dados de licença da sua organização para o Experience Platform em qualquer sandbox associada.

Os dados nesse painel são exibidos exatamente como são exibidos no momento específico em que o instantâneo foi tirado. Em outras palavras, o instantâneo não é uma aproximação ou amostra dos dados, e o painel não é atualizado em tempo real.

>[!NOTE]
>
>Quaisquer alterações ou atualizações feitas nos dados desde que o instantâneo foi tirado não serão refletidas no painel até que o próximo instantâneo seja tirado.

## Explorar o painel de uso de licença {#explore}

Para navegar até o painel de uso de licença na interface do Platform, selecione **[!UICONTROL Uso da licença]** no painel esquerdo. A variável [!UICONTROL Visão geral] é aberta, exibindo uma lista de produtos disponíveis.

>[!NOTE]
>
>O painel de uso de licença não está habilitado por padrão. Os usuários devem ser concedidos &quot;[!UICONTROL Exibir Painel de Uso da Licença]&quot; para poder visualizar o painel. Para obter etapas sobre como conceder permissões de acesso para exibir o painel de uso da licença, consulte o [guia de permissões do painel](../permissions.md).

![A guia Visão geral do painel de uso da licença, com o uso da licença realçado na barra lateral de navegação à esquerda.](../images/license-usage/dashboard-overview.png)

## [!UICONTROL Guia Visão geral] {#overview-tab}

Esse painel exibe todos os produtos licenciados da Adobe Experience Platform, incluindo complementos, em formato de tabela. A tabela fornece as principais informações sobre o uso de licença em todos os perfis disponíveis.

| Nome da coluna | Descrição |
|---|---|
| **[!UICONTROL Produto]** | A solução Adobe licenciada pela sua organização. |
| **[!UICONTROL Métrica primária]** | A métrica principal usada para rastrear o desse produto no. |
| **[!UICONTROL Valor da licença]** | O valor contratado para a quantidade máxima da Métrica primária, conforme acordado no contrato de licença do produto. |
| **[!UICONTROL Uso]** | A quantidade de sua métrica primária usada. Esse valor fornece o uso total dessa métrica em todas as sandboxes, seja de produção ou de desenvolvimento. |
| **[!UICONTROL Uso %]** | A porcentagem da métrica principal usada de acordo com o valor da licença. |

>[!NOTE]
>
>Adições à [!UICONTROL Valor da licença] como resultado de complementos, são adicionados além do [!UICONTROL Valor da licença] para os produtos básicos, como Perfil de dados do cliente em tempo real, Adobe Journey Optimizer e Customer Journey Analytics. O uso dessa quantidade licenciada (após os complementos) é rastreado pelos produtos básicos. Por exemplo, se você comprar um pacote de cinco sandboxes, a quantidade de cinco será adicionada à do produto base. Nesse caso, o complemento mostra uma [!UICONTROL Valor da licença] de um, e o uso desse complemento fica &quot;em branco&quot; à medida que o uso é rastreado pelo produto base.

A tabela indica a métrica principal de cada produto, pois cada produto pode rastrear várias métricas. Para exibir mais métricas e insights detalhados sobre o uso da licença do seu produto, selecione um nome de produto na lista. A variável [!UICONTROL Resumo] para esse produto.

## [!UICONTROL Resumo] guia {#summary-tab}

Todas as métricas disponíveis são exibidas na [!UICONTROL Resumo] guia. As métricas disponíveis dependem do produto licenciado. Essa visualização fornece **uma exibição consolidada de todas as métricas em todas as sandboxes de produção ou desenvolvimento**. O mesmo nível de análise é fornecido para sandboxes de produção e desenvolvimento.

![A visualização resumida de um Produto da plataforma que mostra todas as métricas disponíveis para esse produto.](../images/license-usage/summary-tab.png)

Na guia resumo, a tabela inclui a variável [!UICONTROL Métrica] coluna. Essas descrições em formato legível por humanos indicam todas as métricas usadas para esse tipo de sandbox.

### Selecionar uma sandbox {#select-sandbox}

Para alterar a exibição entre tipos de sandbox de produção e desenvolvimento, selecione [!UICONTROL Sandboxes de produção] ou [!UICONTROL Sandboxes de desenvolvimento]. O tipo de sandbox selecionado é indicado pelo botão de opção ao lado do nome da sandbox.

O relatório de consumo de sandboxes é cumulativo para todas as sandboxes do mesmo tipo. Em outras palavras, selecionar [!UICONTROL Produção] ou [!UICONTROL Desenvolvimento] O fornece relatórios de consumo para todas as sandboxes de produção ou desenvolvimento, respectivamente.

![A exibição de resumo de um Produto de plataforma com sandboxes de produção e sandboxes de desenvolvimento foi destacada.](../images/license-usage/summary-tab-sandboxes.png)

>[!WARNING]
>
>A permissão para exibir o painel de uso de licença deve ser especificada em nível de sandbox. Você deve adicionar permissões a cada sandbox individual para visualizá-las no painel. Essa limitação será abordada em uma versão futura. Enquanto isso, a seguinte solução alternativa está disponível:
>
>1. Crie um perfil de produto no Adobe Admin Console.
>2. Em Permissão na categoria Sandbox, adicione todas as sandboxes que deseja visualizar no painel de uso de licença.
>3. Na categoria de Permissão do painel do usuário, adicione a permissão &quot;Exibir painel de uso da licença&quot;.

## A variável [!UICONTROL Detalhes] guia {#details-tab}

Para ver **uma métrica de uso específica de uma sandbox específica**, navegue até o [!UICONTROL Detalhes] guia. A variável [!UICONTROL Detalhes] A guia mostra todas as sandboxes disponíveis nas sandboxes de Produção ou Desenvolvimento.

![A guia Details do painel de uso da licença.](../images/license-usage/details-tab.png)

Nessa visualização, é possível selecionar ![O ícone Inspect.](../images/license-usage/inspect-icon.png) ao lado do nome de uma sandbox para exibir a visualização dessa métrica. Uma caixa de diálogo é aberta com uma visualização para essa métrica.

### Visualizações {#visualizations}

Cada widget de visualização inclui os seguintes aspectos:

- Um gráfico de linhas que rastreia a alteração da métrica ao longo do tempo
- Uma chave para o gráfico de linhas
- O nome da sandbox
- Um menu suspenso para ajustar o período de tempo do gráfico de linhas

Os gráficos de linha comparam os números de uso da organização com o total disponível com o licenciamento da organização e fornecem uma porcentagem do uso total.

![A visualização de uma métrica.](../images/license-usage/visualization.png)

O período de análise da pesquisa pode ser ajustado no menu suspenso. O valor padrão dos últimos 30 dias

Para selecionar um intervalo de datas, você pode usar a lista suspensa de intervalo de datas para selecionar o período a ser exibido no painel. Há várias opções disponíveis, incluindo o valor padrão dos últimos 30 dias.

![A caixa de diálogo de visualização com o menu suspenso de intervalo de datas está realçada.](../images/license-usage/date-range.png)

Também é possível selecionar **[!UICONTROL Data personalizada]** para escolher o período mostrado.

![A guia Visão geral do painel de uso da licença com as opções de intervalo de datas personalizado destacadas.](../images/license-usage/custom-date-range.png)

## Métricas disponíveis

O painel de uso da licença relata várias métricas exclusivas que são aplicáveis a vários produtos na organização. As métricas disponíveis são:

- [!UICONTROL Número de sandboxes]
- [!UICONTROL Público-alvo endereçável]
- [!UICONTROL Riqueza média do perfil]
- [!UICONTROL Principais horas]
- [!UICONTROL Armazenamento de data lake]
- [!UICONTROL Dados digitalizados por taxa de segmentação]
- [!UICONTROL Público envolvente]
- [!UICONTROL Armazenamento total consumido]
- [!UICONTROL Armazenamento total]
- [!UICONTROL Horas calculadas do serviço de consulta]

A disponibilidade dessas métricas e a definição específica de cada uma delas variam de acordo com o licenciamento adquirido pela sua organização. Para obter definições detalhadas de cada métrica, consulte a documentação apropriada Descrição do produto:

| Licença | Descrição do produto |
|---|---|
| <ul><li>ADOBE EXPERIENCE PLATFORM:OD LITE</li><li>ADOBE EXPERIENCE PLATFORM:PADRÃO OD</li><li>ADOBE EXPERIENCE PLATFORM:MUITO PESADO</li></ul> | [Adobe Experience Platform](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform.html) |
| <ul><li>ADOBE EXPERIENCE PLATFORM:OD</li></ul> | [Experience Platform, serviços de aplicativos e serviços inteligentes](https://helpx.adobe.com/legal/product-descriptions/exp-platform-app-svcs.html) |
| <ul><li>PLATAFORMA DE DADOS DO CLIENTE DE RT:OD</li><li>PLATAFORMA DE DADOS DO CLIENTE DE RT:OD PRFL PARA 10M</li><li>PLATAFORMA DE DADOS DO CLIENTE DE RT:OD PRFL PARA 50M</li></ul> | [Adobe Real-time Customer Data Platform](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html?lang=pt-BR) |
| <ul><li>AEP:ATIVAÇÃO OD</li><li>AEP:OD ATIVATION PRFL PARA 10M</li><li>AEP:OD ATIVATION PRFL ATÉ 50 M</li></ul> | [Ativação do Adobe Experience Platform](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform0.html) |
| <ul><li>AEP:INTELIGÊNCIA OD</li></ul> | [Adobe Experience Platform Intelligence](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform-intelligence---product-description.html) |
| <ul><li>JOURNEY OPTIMIZER SELECT:OD</li><li>JOURNEY OPTIMIZER PRIME:OD</li><li>JOURNEY OPTIMIZER ULTIMATE:OD</li><li>UNP AJO PRIME STARTER:OD</li><li>UNP AJO ULTIMATE STARTER:OD</li><li>UNP Real-Time CDP:ORQUESTRAÇÃO DE PERFIL OD</li></ul> | [Adobe Journey Optimizer](https://helpx.adobe.com/br/legal/product-descriptions/adobe-journey-optimizer.html) |

>[!WARNING]
>
>O painel de uso de licença relata apenas a licença mais recente que foi provisionada para sua organização. Se a licença mais recente provisionada para sua organização não aparecer na tabela acima, o painel de uso da licença pode não ser exibido corretamente. O suporte para licenças adicionais e várias licenças em uma única organização está planejado para uma versão futura.

## Próximas etapas

Depois de ler este documento, você pode localizar o painel de uso da licença e exibir as métricas de uso para cada produto comprado, para todas as sandboxes de produção ou desenvolvimento e para uma sandbox específica. Você pode encontrar mais informações sobre métricas disponíveis para sua organização, com base no licenciamento que sua organização adquiriu.

Para saber mais sobre outros recursos disponíveis na interface do usuário do Experience Platform, consulte [Guia da interface do usuário da Platform](../../landing/ui-guide.md).
