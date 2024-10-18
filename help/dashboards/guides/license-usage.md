---
keywords: Experience Platform;interface do usuário;UI;personalização;uso de licença painel;painel;uso de licença;direito;consumo
title: Painel de Uso da Licença
description: A Adobe Experience Platform fornece um painel por meio do qual você pode visualizar informações importantes sobre o uso de licença da sua organização.
type: Documentation
exl-id: 143d16bb-7dc3-47ab-9b93-9c16683b9f3f
source-git-commit: 80380fb1287d710460ad2c75d73ea5c2c38f5ebd
workflow-type: tm+mt
source-wordcount: '2855'
ht-degree: 15%

---

# Painel de uso da licença {#license-usage-dashboard}

>[!CONTEXTUALHELP]
>id="testy-mctestface"
>title="Caixa de diálogo de teste que não deve estar visível"
>abstract="O objeto {name} está sendo exibido em {date}."

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_core"
>title="Tabela de produtos principais"
>abstract="Os principais produtos listados na tabela têm suas próprias métricas, rastreamento de uso e exibições de detalhamento no nível da sandbox. Esses produtos principais fornecem as métricas principais para rastreamento e todos os complementos estão incluídos nessas métricas."

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseusage_addons"
>title="Tabela de complementos"
>abstract="A tabela Complementos lista produtos cujas quantidades de licença são combinadas com as métricas compatíveis com os produtos principais. Esses complementos não têm métricas separadas, mas aprimoram o rastreamento de uso dos produtos principais aos quais estão associados."

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseUsage"
>title="Painel de uso da licença"
>abstract="O painel de uso da licença oferece informações sobre os produtos da Adobe Experience Platform que você adquiriu. A visão geral do painel exibe as métricas principais de seus produtos, incluindo o uso de cada uma das métricas principais e o período de licença contratado. O espaço de trabalho de detalhes exibe um detalhamento das métricas para cada produto em sandboxes específicas."
>additional-url="https://experienceleague.adobe.com/pt-br/docs/experience-platform/data-lifecycle/ui/dataset-expiration" text="Expirações automatizadas de conjuntos de dados"
>additional-url="https://experienceleague.adobe.com/pt-br/docs/experience-platform/profile/pseudonymous-profiles" text="Expiração de dados de perfis pseudônimos"

>[!CONTEXTUALHELP]
>id="platform_licenseusage"
>title="Painel de uso da licença"
>abstract="O painel de uso da licença oferece informações sobre os produtos da Adobe Experience Platform que você adquiriu. A visão geral do painel exibe as métricas principais de seus produtos, incluindo o uso de cada uma das métricas principais e o período de licença contratado. O espaço de trabalho de detalhes exibe um detalhamento das métricas para cada produto em sandboxes específicas."
>additional-url="https://experienceleague.adobe.com/pt-br/docs/experience-platform/data-lifecycle/ui/dataset-expiration" text="Expirações automatizadas de conjuntos de dados"
>additional-url="https://experienceleague.adobe.com/pt-br/docs/experience-platform/profile/pseudonymous-profiles" text="Expiração de dados de perfis pseudônimos"

Você pode exibir informações importantes sobre o uso de licenças da sua organização no painel [!UICONTROL Uso de licenças] do Adobe Experience Platform. As informações exibidas aqui são capturadas durante um instantâneo diário da sua instância da Platform.

Os relatórios de uso de licença fornecem um alto grau de granularidade em relação às métricas de uso de licença. O painel fornece métricas de uso para cada produto comprado (e complementos associados), o uso consolidado de métricas em todas as sandboxes de produção ou desenvolvimento e a métrica de uso de uma sandbox específica. Os aplicativos de Experience Platform a seguir podem ser rastreados com métricas de uso: Real-time Customer Data Platform, Adobe Journey Optimizer e Customer Journey Analytics.

Este guia descreve como acessar e trabalhar com o painel de uso de licença na interface do usuário e fornece mais informações sobre as visualizações exibidas no painel.

Para obter uma visão geral da interface do usuário da Platform, consulte o [guia da interface do usuário do Experience Platform](../../landing/ui-guide.md).

## Dados do painel de [!UICONTROL uso da licença]

O painel de [!UICONTROL Uso da licença] exibe uma lista de todos os produtos do Experience Platform que você adquiriu e todos os complementos para esses produtos. Nesse painel, você pode encontrar um instantâneo dos dados de licença da sua organização para o Experience Platform em qualquer sandbox associada.

Os dados nesse painel são exibidos exatamente como são exibidos no momento específico em que o instantâneo foi tirado. Em outras palavras, o instantâneo não é uma aproximação ou amostra dos dados, e o painel não é atualizado em tempo real.

>[!NOTE]
>
>Quaisquer alterações ou atualizações feitas nos dados desde que o instantâneo foi tirado não serão refletidas no painel até que o próximo instantâneo seja tirado.

## Explorar o painel de uso de licença {#explore}

Para navegar até o painel de uso de licença na interface do usuário da Platform, selecione **[!UICONTROL Uso da licença]** no painel esquerdo. A guia [!UICONTROL Visão geral] é aberta, exibindo uma lista de produtos disponíveis.

>[!NOTE]
>
>O painel de uso de licença não está habilitado por padrão. Os usuários devem receber a permissão &quot;Exibir painel de uso da licença&quot; para poderem exibir o painel. Para obter etapas sobre como conceder permissões de acesso para exibir o painel de uso de licença, consulte o [guia de permissões do painel](../permissions.md).

![A guia Visão geral do painel de uso da licença, com o uso da licença realçado na barra lateral de navegação à esquerda.](../images/license-usage/dashboard-overview.png)

## Guia [!UICONTROL Visão geral] {#overview-tab}

O painel de [!UICONTROL Uso da Licença] exibe duas tabelas separadas: **Produtos principais** e **Complementos**.

- **[!UICONTROL Tabela de ] de produtos principais**: esta tabela lista os principais produtos da Adobe Experience Platform licenciados pela sua organização. Cada produto principal tem suas próprias métricas, rastreamento de uso e exibições de drill-through no nível da sandbox. Esses produtos principais fornecem as métricas principais para rastreamento e todos os complementos estão incluídos nessas métricas.

- **[!UICONTROL Tabela de complementos]**: esta tabela lista outros produtos cujos valores de licença são combinados com as métricas suportadas pelos produtos principais. Os complementos não têm métricas separadas, mas aprimoram o rastreamento de uso dos principais produtos aos quais estão associados.

| Nome da coluna | Descrição |
|---|---|
| **[!UICONTROL Produto]** | A solução Adobe licenciada pela sua organização. |
| **[!UICONTROL Métrica primária]** | A métrica principal usada para rastreamento nesse produto. |
| **[!UICONTROL Valor da Licença]** | O valor contratado para a quantidade máxima da Métrica primária, conforme acordado no contrato de licença do produto. |
| **[!UICONTROL Uso]** | A quantidade de sua métrica primária usada. Esse valor fornece o uso total dessa métrica em todas as sandboxes, seja de produção ou de desenvolvimento. |
| **[!UICONTROL Uso %]** | A porcentagem da métrica principal usada de acordo com o valor da licença. |
| **[!UICONTROL Uso de previsão]** | A porcentagem de uso prevista da sua métrica principal de acordo com o valor da licença. |

>[!NOTE]
>
>Os valores de licença para complementos estão incluídos no [!UICONTROL Valor de Licença] dos produtos principais. Por exemplo, se você comprar um pacote de cinco sandboxes como um complemento, a quantidade será adicionada ao do produto base. A tabela de complementos mostra um [!UICONTROL Valor de Licença] específico para o complemento, mas o uso real é rastreado por meio do produto base.

As tabelas indicam a métrica principal de cada produto, já que cada produto pode rastrear diversas métricas.

### Uso previsto {#predicted-usage}

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseUsage_prediction"
>title="Uso previsto"
>abstract="As previsões são baseadas no uso durante os últimos 6 a 7 meses e são geradas no dia 15 de cada mês. Observe que as previsões de uso de licença são aproximações baseadas no uso anterior. Você é responsável por entender o uso real da sua organização e garantir que ele não ultrapasse o escopo da licença da organização na Adobe. Para reduzir o uso, defina expirações de conjuntos de dados ou dados de perfis pseudônimos para sandboxes e conjuntos de dados."
>additional-url="https://experienceleague.adobe.com/pt-br/docs/experience-platform/data-lifecycle/ui/dataset-expiration" text="Expirações automatizadas de conjuntos de dados"
>additional-url="https://experienceleague.adobe.com/pt-br/docs/experience-platform/profile/pseudonymous-profiles" text="Expiração de dados de perfis pseudônimos"

>[!CONTEXTUALHELP]
>id="platform_licenseusage_prediction"
>title="Uso previsto"
>abstract="As previsões são baseadas no uso durante os últimos 6 a 7 meses e são geradas no dia 15 de cada mês. Observe que as previsões de uso de licença são aproximações baseadas no uso anterior. Você é responsável por entender o uso real da sua organização e garantir que ele não ultrapasse o escopo da licença da organização na Adobe. Para reduzir o uso, defina expirações de conjuntos de dados ou dados de perfis pseudônimos para sandboxes e conjuntos de dados."
>additional-url="https://experienceleague.adobe.com/pt-br/docs/experience-platform/data-lifecycle/ui/dataset-expiration" text="Expirações automatizadas de conjuntos de dados"
>additional-url="https://experienceleague.adobe.com/pt-br/docs/experience-platform/profile/pseudonymous-profiles" text="Expiração de dados de perfis pseudônimos"

Gerencie e otimize proativamente seus recursos de licenciamento com base em previsões de uso relevantes. A coluna [!UICONTROL Uso previsto] prevê com precisão o uso futuro de licenças no nível da sandbox, em todas as sandboxes de produção e desenvolvimento, para todos os produtos adquiridos. Esse recurso de alerta fornece uma previsão do uso de licenças por seis semanas no futuro, com base no seu uso até o dia 15 deste mês. As previsões são fornecidas com um limite inferior e superior.

>[!IMPORTANT]
>
>As previsões são atualizadas mensalmente. A data de atualização está incluída em um ícone de informações (![Este ícone de informações.](../images/license-usage/info-icon.png)) acima do título da coluna.

Para ver um resumo do uso de direitos de um produto, selecione um produto na tabela [!UICONTROL Produtos principais].

![O [!UICONTROL Uso da licença] [!UICONTROL Visão geral] com um produto e a coluna de uso previsto realçada.](../images/license-usage/product-predicted-usage.png)

A guia Summary (Resumo) é exibida. Você pode usar as previsões granulares disponíveis nas guias [!UICONTROL Resumo] e [!UICONTROL Detalhes] para garantir uma tomada de decisão informada para o uso eficiente da licença.

>[!NOTE]
>
>Observe que as previsões de uso de licença são aproximações baseadas no uso anterior. Você é responsável por entender o uso real da sua organização e garantir que o uso não vá além do escopo da licença da sua organização com o Adobe.

![O modo de exibição de resumo de um Produto da Plataforma com a coluna de uso previsto está realçado.](../images/license-usage/summary-predicted-usage.png)

A porcentagem de uso previsto é determinada da seguinte maneira:

- Se os limites inferior e superior forem significativamente diferentes, eles serão exibidos como um intervalo (por exemplo, 32% - 35%).
- Se os limites inferior e superior forem quase idênticos e não forem zero, serão exibidos como um valor aproximado (por exemplo, ~34%).
- Se os limites inferior e superior forem quase idênticos e zero, serão exibidos como exatamente 0%.

>[!NOTE]
>
>&quot;Quase idêntico&quot; neste contexto significa que os valores são estatisticamente significativos para duas casas decimais (por exemplo, um limite inferior de 0,342 e um limite superior de 0,344 são arredondados para 34%).

O recurso de uso previsto é compatível com as seguintes métricas:

- [!UICONTROL Público-alvo endereçável]
- [!UICONTROL Horas de computação]
- [!UICONTROL Número de linhas do Público-alvo de Jornada do cliente]
- [!UICONTROL Volume de Dados Total]

## Guia [!UICONTROL Resumo] {#summary-tab}

Para exibir mais métricas e insights detalhados sobre o uso da licença do seu produto, selecione um nome de produto na lista. A exibição [!UICONTROL Resumo] desse produto é exibida. Todas as métricas disponíveis são exibidas na guia [!UICONTROL Resumo]. As métricas disponíveis dependem do produto licenciado. Esta exibição fornece **uma exibição consolidada de todas as métricas em todas as sandboxes de produção ou desenvolvimento**. O mesmo nível de análise é fornecido para sandboxes de produção e desenvolvimento.

![O modo de exibição de resumo de um Produto da Plataforma que mostra todas as métricas disponíveis para esse produto.](../images/license-usage/summary-tab.png)

Na guia de resumo, a tabela inclui a coluna [!UICONTROL Métrica]. Essas descrições em formato legível por humanos indicam todas as métricas usadas para esse tipo de sandbox.

### Selecionar uma sandbox {#select-sandbox}

Para alterar a exibição entre tipos de sandbox de produção e desenvolvimento, selecione [!UICONTROL sandboxes de produção] ou [!UICONTROL sandboxes de desenvolvimento]. O tipo de sandbox selecionado é indicado pelo botão de opção ao lado do nome da sandbox.

O relatório de consumo de sandboxes é cumulativo para todas as sandboxes do mesmo tipo. Em outras palavras, selecionar [!UICONTROL Produção] ou [!UICONTROL Desenvolvimento] fornece relatórios de consumo para todas as sandboxes de produção ou desenvolvimento, respectivamente.

![A exibição de resumo de um Produto de plataforma com sandboxes de produção e sandboxes de desenvolvimento realçadas.](../images/license-usage/summary-tab-sandboxes.png)

>[!WARNING]
>
>A permissão para exibir o painel de uso de licença deve ser especificada em nível de sandbox. Adicione permissões a cada sandbox individual para visualizá-las no painel. Essa limitação será abordada em uma versão futura. Enquanto isso, a seguinte solução alternativa está disponível:
>
>1. Crie um perfil de produto no Adobe Admin Console.
>2. Em Permissão na categoria Sandbox, adicione todas as sandboxes que deseja visualizar no painel de uso de licença.
>3. Na categoria Permissão do painel do usuário, adicione a permissão &quot;Exibir painel de uso da licença&quot;.

## Guia [!UICONTROL Detalhes] {#details-tab}

Para ver **uma métrica de uso específica de uma sandbox específica**, navegue até a guia [!UICONTROL Detalhes]. A guia [!UICONTROL Detalhes] mostra todas as sandboxes disponíveis nas sandboxes de Produção ou Desenvolvimento.

![A guia Detalhes do painel de uso da Licença.](../images/license-usage/details-tab.png)

Nesta exibição, você pode selecionar ![O ícone Inspecionar.](/help/images/icons/inspect.png) ao lado de um nome de sandbox para exibir a visualização dessa métrica. Uma caixa de diálogo é aberta com uma visualização para essa métrica.

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

![A caixa de diálogo de visualização com a lista suspensa de intervalo de datas está realçada.](../images/license-usage/date-range.png)

Você também pode selecionar **[!UICONTROL Data personalizada]** para escolher o período de tempo mostrado.

![A guia Visão Geral do painel de uso da licença com as opções de intervalo de datas personalizado realçadas.](../images/license-usage/custom-date-range.png)

## Métricas disponíveis {#available-metrics}

>[!IMPORTANT]
>
>A partir de 20 de agosto, os clientes com direitos para &#39;[!UICONTROL Riqueza Média de Perfil]&#39; e &#39;[!UICONTROL Armazenamento Total]&#39; viram &#39;[!UICONTROL Volume Total de Dados]&#39; no Painel de Uso de Licenças. Não houve alteração nos direitos do cliente, apenas uma simplificação das métricas de rastreamento. [!UICONTROL Volume de Dados Total] representa os dados disponíveis no Serviço de Perfil da Adobe Experience Platform para os fluxos de trabalho de envolvimento e personalização. Essa métrica simplificada melhorou o gerenciamento e a medição do uso do Serviço de perfil. Os clientes foram incentivados a entrar em contato com o representante da Adobe para obter mais esclarecimentos sobre essa alteração.

O painel de uso da licença relata várias métricas exclusivas que são aplicáveis a vários produtos na organização. As métricas disponíveis são:

| Métrica | Descrição |
|---|---|
| [!UICONTROL Tamanho do Audience Activation] | O tamanho total dos perfis ativados para qualquer destino baseado em arquivo em um ano. Observação: isso não inclui perfis enviados por meio de destinos de streaming. |
| [!UICONTROL Público-alvo endereçável] | A soma do direito de público-alvo comercial e do direito de público-alvo consumidor. Um público-alvo do consumidor é definido como o número de perfis de pessoas identificados como um &quot;Público-alvo do consumidor&quot; na ordem de venda. Um público-alvo comercial é definido como o número de perfis empresariais identificados como o &quot;Público-alvo comercial&quot; na ordem de venda. |
| [!UICONTROL Pacotes de Usuários do Serviço de Consulta Adhoc] | Um complemento para aumentar o direito dos Usuários do Serviço de Consulta simultâneos autorizados em cinco usuários adicionais do Serviço de Consulta simultâneos e uma consulta ad hoc adicional em execução simultânea por pacote. É possível que vários pacotes adicionais de usuários de Ad Hoc Query sejam licenciados. |
| [!UICONTROL Riqueza média de perfil] | **Obsoleto** - A soma de todos os dados de produção armazenados no Serviço de Perfil de Hub em qualquer momento, dividida por cinco vezes o número de perfis empresariais autorizados. [!UICONTROL A riqueza média do perfil] é um recurso compartilhado. |
| [!UICONTROL Linhas do CJA Disponíveis] | A média diária de linhas de dados disponíveis para análise no Customer Journey Analytics. |
| [!UICONTROL Atributos computados] | A contagem total de dados comportamentais agregados de perfis. Os dados comportamentais agregados do perfil são baseados em eventos de experiência convertidos em um atributo de perfil e podem ser incluídos em um perfil de pessoa ou perfil de pessoa de negócios. |
| [!UICONTROL Público-alvo] | O número de perfis de pessoas identificados como &quot;Público-alvo do consumidor&quot; na ordem de venda. |
| [!UICONTROL Tamanho da Exportação de Dados] | A quantidade de dados enviados por meio de ativações de conjuntos de dados em um ano. |
| [!UICONTROL Exportações de dados] | O tamanho total dos conjuntos de dados que podem ser exportados para qualquer solução não Adobe (direta ou indiretamente) em um ano. |
| [!UICONTROL Armazenamento Data Lake] | A quantidade usada do armazenamento de dados analíticos no Adobe Experience Platform. |
| [!UICONTROL Público-alvo envolvente] | Essa métrica se refere ao público-alvo de perfis utilizáveis. Um perfil envolvível é um registro de informações que representam um indivíduo e é representado no Serviço de perfil. Esses registros são perfis que você tentou utilizar com os recursos de criação, decisão, entrega, experimentação ou orquestração do Journey Optimizer nos últimos 12 meses. |
| [!UICONTROL Públicos-alvo semelhantes] | A contagem de públicos-alvo gerada pela modelagem de um público-alvo de consumidor existente para identificar perfis de pessoas semelhantes ao público-alvo de consumidor existente. |
| [!UICONTROL Número de Modelos AMM] | Uma contagem do modelo de aprendizado de máquina (Adobe Mix Modeler interno) usada para medir e/ou prever um resultado especificado com base em seus investimentos. |
| [!UICONTROL Número de Sandboxes] | A contagem de separações lógicas na instância de qualquer Adobe On-demand Service que acesse dados e operações de isolamento do Adobe Experience Platform. |
| [!UICONTROL Número de Pacotes de Riqueza de Perfis] | Um aumento no Volume total de dados autorizado de 25 KB por perfil para cada pacote adicional de Riqueza de perfil. |
| [!UICONTROL Horas de Computação do Serviço de Consulta] | Uma medida do tempo gasto pelos mecanismos de Serviço de consulta para ler, processar e gravar dados de volta no data lake quando uma consulta em lote é executada. |
| [!UICONTROL Número de pacotes de segmentação de streaming] | Os pacotes atualizam a associação de segmento para um perfil de pessoa à medida que novos dados entram no Serviço de segmentação por meio de um fluxo de transmissão. A associação do segmento é avaliada com base nos atributos atuais do perfil da pessoa e no valor do evento atual, sem levar em conta o comportamento histórico. A segmentação de transmissão é um recurso compartilhado. |
| [!UICONTROL Volume de Dados Total] | A quantidade total de dados disponíveis para o Serviço de perfil da Adobe Experience Platform usar em fluxos de trabalho de envolvimento. |

<!-- |  [!UICONTROL Sandbox No of Packs] |  A logical separation within your instance of any Adobe On-demand Service that accesses Adobe Experience Platform isolating data and operations | -->

>[!TIP]
>
>Você pode verificar seus direitos de licença em seu Pedido de vendas para calcular métricas como sua &quot;Permissão de armazenamento&quot;.<br>Por exemplo,<ul><li>Abatimento de armazenamento = o número de &quot;perfis autorizados&quot; em seu contrato X Perfil médio Riqueza</li></ul>

A disponibilidade dessas métricas e a definição específica de cada uma delas variam de acordo com o licenciamento adquirido pela sua organização. Para obter definições detalhadas de cada métrica, consulte a documentação apropriada Descrição do produto:

| Licença | Descrição do produto |
| --- | --- |
| <ul><li>ADOBE EXPERIENCE PLATFORM:OD LITE</li><li>ADOBE EXPERIENCE PLATFORM:PADRÃO OD</li><li>ADOBE EXPERIENCE PLATFORM:MUITO PESADO</li></ul> | [Adobe Experience Platform](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform.html) |
| <ul><li>ADOBE EXPERIENCE PLATFORM:OD</li></ul> | [Experience Platform, Serviços de Aplicativos e Serviços Inteligentes](https://helpx.adobe.com/legal/product-descriptions/exp-platform-app-svcs.html) |
| <ul><li>PLATAFORMA DE DADOS DO CLIENTE DE RT:OD</li><li>PLATAFORMA DE DADOS DO CLIENTE DE RT:OD PRFL PARA 10M</li><li>PLATAFORMA DE DADOS DO CLIENTE DE RT:OD PRFL PARA 50M</li></ul> | [Adobe Real-time Customer Data Platform](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html?lang=pt-BR) |
| <ul><li>AEP:ATIVAÇÃO OD</li><li>AEP:OD ATIVATION PRFL PARA 10M</li><li>AEP:OD ATIVATION PRFL ATÉ 50 M</li></ul> | [Ativação do Adobe Experience Platform](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform0.html) |
| <ul><li>AEP:INTELIGÊNCIA OD</li></ul> | [Adobe Experience Platform Intelligence](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform-intelligence---product-description.html) |
| <ul><li>JOURNEY OPTIMIZER SELECT:OD</li><li>JOURNEY OPTIMIZER PRIME:OD</li><li>JOURNEY OPTIMIZER ULTIMATE:OD</li><li>UNP AJO PRIME STARTER:OD</li><li>UNP AJO ULTIMATE STARTER:OD</li><li>UNP Real-Time CDP:ORQUESTRAÇÃO DE PERFIL OD</li></ul> | [Adobe Journey Optimizer](https://helpx.adobe.com/br/legal/product-descriptions/adobe-journey-optimizer.html) |

>[!WARNING]
>
>O painel de uso de licença relata apenas a licença mais recente que foi provisionada para sua organização. Se a licença mais recente provisionada para sua organização não aparecer na tabela acima, o painel de uso da licença pode não ser exibido corretamente. O suporte para licenças adicionais e várias licenças em uma única organização está planejado para uma versão futura.

## Próximas etapas

Depois de ler este documento, você pode localizar o painel de uso da licença e exibir as métricas de uso para cada produto comprado, para todas as sandboxes de produção ou desenvolvimento e para uma sandbox específica. Você pode encontrar mais informações sobre métricas disponíveis para sua organização, com base no licenciamento que sua organização adquiriu.

Para saber mais sobre outros recursos disponíveis na interface do usuário do Experience Platform, consulte o [guia da interface do usuário da plataforma](../../landing/ui-guide.md).
