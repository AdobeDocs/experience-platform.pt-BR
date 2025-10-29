---
keywords: Experience Platform;insights;ia de atribuição;tópicos populares;insights de ia de atribuição
feature: Attribution AI
title: Descubra insights no Attribution AI
description: Este documento serve como um guia para interagir com insights da instância do serviço na interface do usuário dos Serviços inteligentes da Adobe.
exl-id: 6b8e51e7-1b56-4f4e-94cf-96672b426c88
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1583'
ht-degree: 0%

---

# Descubra insights na IA de atribuição

As instâncias de serviço da IA de atribuição fornecem insights que podem ser usados para ajudar a tomar e medir decisões de marketing relacionadas ao desempenho de marketing e ao retorno sobre o investimento. A seleção de uma instância de serviço fornece visualizações e filtros para ajudá-lo a entender o impacto de cada interação com o cliente em cada fase da jornada do cliente.

Este documento serve como um guia para interagir com insights da instância do serviço na interface do usuário dos Serviços inteligentes da Adobe.

## Introdução

Para utilizar insights para a IA de atribuição, é necessário ter uma instância de serviço com um status de execução bem-sucedida disponível. Para criar uma nova instância de serviço, visite o [guia da interface do usuário da IA de atribuição](./user-guide.md). Se você criou recentemente uma instância de serviço e ela ainda está sendo treinada e pontuada, aguarde 24 horas para que ela seja concluída.

## Visão geral dos insights da instância de serviço

Na interface do usuário do [!DNL Adobe Experience Platform], selecione **[!UICONTROL Services]** na navegação à esquerda. O navegador **[!UICONTROL Services]** é exibido e exibe os Serviços Inteligentes da Adobe disponíveis. No contêiner da IA de atribuição, selecione **[!UICONTROL Open]**.

![Acessando sua instância](./images/insights/open_Attribution_ai.png)

A página do serviço IA de atribuição é exibida. Esta página lista as instâncias de serviço da IA de atribuição e exibe informações sobre elas, incluindo o nome da instância, eventos de conversão, a frequência com que a instância é executada e o status da última atualização. Selecione um nome de instância de serviço para começar.

>[!NOTE]
>
>Somente as instâncias de serviço que concluíram execuções de pontuação bem-sucedidas podem ser selecionadas.

![Criar instância](./images/insights/select-service-instance.png)

Em seguida, a página de insights para essa instância do serviço é exibida, onde você recebe visualizações e vários filtros para interagir com seus dados. As visualizações e os filtros são explicados com mais detalhes neste guia.

![página de configuração](./images/insights/landing-page.png)

### Detalhes da instância do serviço

Para exibir detalhes adicionais de uma instância de serviço, selecione **[!UICONTROL Show more]** no canto superior direito.

![mostrar mais](./images/insights/show-more.png)

Uma lista detalhada é exibida. Para obter mais informações sobre qualquer uma das propriedades listadas, visite o [guia do usuário da IA de atribuição](./user-guide.md).

![mostrar detalhes](./images/insights/advanced-details.png)

### Editar uma instância

Para editar uma instância, selecione **[!UICONTROL Edit]** na navegação superior direita.
![clique no botão editar](./images/insights/edit-button.png)

A caixa de diálogo de edição é exibida, permitindo editar o nome, a descrição e a frequência de pontuação da instância. Se o status da instância estiver desativado, a frequência de pontuação não poderá ser editada. Para confirmar as alterações e fechar a caixa de diálogo, selecione **[!UICONTROL Save]** no canto inferior direito.

![editar popover](./images/insights/edit-popover.png)

### Mais ações {#more-actions}

O botão **[!UICONTROL More actions]** está localizado na navegação superior direita ao lado de **[!UICONTROL Edit]**. Selecionar **[!UICONTROL More actions]** abre uma lista suspensa que permite selecionar uma das seguintes operações:

- **[!UICONTROL Clone]**: clona a instância.
- **[!UICONTROL Delete]**: exclui a instância.
- **[!UICONTROL Download summary data]**: baixa um arquivo CSV contendo os dados de resumo.
- **[!UICONTROL Access scores]**: Ao selecionar **[!UICONTROL Access scores]**, você será redirecionado para o [tutorial de pontuações de acesso para a IA de atribuição](./download-scores.md).
- **[!UICONTROL View run history]**: um popover contendo uma lista de todas as execuções de pontuação associadas à instância do serviço é exibido.

![mais ações](./images/insights/more-actions.png)

## Filtrar seus dados

Os insights da IA de atribuição permitem filtrar seus dados e atualizar automaticamente os visuais da interface com base nos filtros selecionados.

### Evento de conversão

Ao criar uma nova instância na IA de atribuição, um dos campos obrigatórios é &quot;Eventos de conversão&quot;. Eventos de conversão são Objetivos de negócios que identificam o impacto de atividades de marketing, como pedidos, compras na loja e visitas a sites.

Na instância, a lista suspensa **[!UICONTROL Conversion events]** permite selecionar qualquer um dos eventos definidos para sua instância para filtrar seus dados. Selecionar eventos específicos altera as visualizações da interface do usuário para preencher somente as conversões pertencentes a esses eventos.

![evento de conversão](./images/insights/conversion-event.png)

### Modelo de atribuição

Selecionar **[!UICONTROL Attribution Model]** abre uma lista suspensa com todos os diferentes modelos de atribuição disponíveis. É possível selecionar vários modelos para comparar os resultados. Para obter mais informações sobre os diferentes modelos de atribuição e como eles funcionam, visite a visão geral da [IA de atribuição](./overview.md) que contém uma tabela com informações sobre cada modelo.

![modelo de atribuição](./images/insights/attribution-model.png)

### Região

>[!NOTE]
>
>Este filtro só estará presente se você tiver executado a etapa opcional [modelagem baseada em região](./user-guide.md#region-based-modeling-optional) no guia da interface do usuário da IA de atribuição ao criar sua instância de serviço.

Esse filtro permite selecionar qualquer região configurada no processo de criação de instância.

### Adicionar filtros

Você pode adicionar mais filtros selecionando o ícone **filtro** para abrir o popover **[!UICONTROL Add filters]**. O popover **[!UICONTROL Add filters]** permite filtrar por Canal, Geografia, Tipo de mídia e Produto. Somente os filtros aplicáveis para uma instância de serviço são preenchidos pelo popover. Por exemplo, se você não forneceu dados geográficos ou um tipo de mídia, esses atributos de filtro não estarão disponíveis para sua instância.

![filtros extras](./images/insights/additional-filters.png)

![popover de filtro](./images/insights/filter-popover.png)

- **[!UICONTROL Channel]:** A seleção do atributo de canal permite filtrar qualquer um dos canais de marketing disponíveis. Você pode selecionar vários canais para compará-los.
- **[!UICONTROL Geography]:** A seleção do atributo de geografia permite filtrar códigos de país com base em modelos baseados em região. Dependendo dos seus dados, esse filtro pode ou não estar presente. Os códigos de país têm dois caracteres. Veja a lista completa de códigos de país [aqui](https://datahub.io/core/country-list).
- **[!UICONTROL Media type]:** A seleção do atributo de tipo de mídia permite filtrar qualquer um dos tipos de mídia definidos.
- **[!UICONTROL Product]:** A seleção do atributo de produto permite filtrar por todos os produtos que foram inicialmente assimilados na criação da sua instância.

### Date Range

Selecione o ícone de calendário para abrir o popover de intervalo de datas. As datas de evento de conversão inicial e final determinam a quantidade de dados preenchidos na interface do usuário. É possível optar por restringir ou ampliar o intervalo de datas para focalizar ou expandir a quantidade de dados preenchidos.

![intervalo de datas](./images/insights/display-date-range.png)

## Visão geral dos seus dados

O cartão **[!UICONTROL Overview]** mostra o total de conversões por modelo de atribuição. O número total muda com base em quão específica você faz sua pesquisa usando os filtros descritos anteriormente neste documento. Selecionar mais modelos adiciona círculos adicionais à Visão geral, cada um com sua própria cor correspondente à legenda.

![visão geral](./images/insights/Overview.png)

## Tendências semanais

O cartão **[!UICONTROL Weekly trends]** detalha sua conversão total pelo intervalo de datas definido durante o processo de filtragem.

Selecionar as reticências no canto superior direito do cartão **Tendências semanais** exibe uma lista suspensa que permite selecionar tendências diárias, semanais ou mensais.

Passar o mouse sobre a linha de dados de um modelo de atribuição específico cria um popover que mostra o número total de conversões dessa data.

![tendências](./images/insights/weekly-trends.png)

## Detalhamento por canal

O cartão **[!UICONTROL Breakdown by channel]** é usado para determinar o número total de conversões em relação a cada canal. Essa placa pode ser usada para ajudar a tomar decisões sobre a eficácia de cada canal e o retorno sobre o investimento.

Selecionar as reticências no canto superior direito do cartão **[!UICONTROL Breakdown by channel]** abre uma lista suspensa que permite preencher dados com base em pontos de contato.

![canal de detalhamento](./images/insights/channel-breakdown.png)

## Principais campanhas

O cartão **[!UICONTROL Top campaigns]** exibe uma visão geral de suas campanhas e como a campanha está se saindo em cada canal. Este cartão pode ajudar a informar sua equipe sobre a eficácia de uma campanha específica para um determinado canal e fornecer insights, como em quais campanhas você deve investir ainda mais.

![campanhas principais](./images/insights/top-campaigns.png)

## Detalhamento por posição de ponto de contato

Selecionar a guia **[!UICONTROL Path Analysis]** carrega os gráficos **[!UICONTROL Breakdown by touchpoint position]** e **[!UICONTROL Top conversion paths]**.

O gráfico **[!UICONTROL Breakdown by touchpoint position]** é um detalhamento das conversões atribuídas por posição do ponto de contato comparado em todos os caminhos de conversão. Este gráfico ajuda você a entender quais pontos de contato são mais eficazes em diferentes estágios do caminho de conversão. Os estágios são inicial, reprodutor e final.

- **Início:** indica que o ponto de contato foi o primeiro contato em um caminho de conversão.
- **Player:** indica que o ponto de contato não foi o primeiro ou o último contato que levou a uma conversão.
- **Mais Próximo:** Indica que o ponto de contato foi o último contato antes de uma conversão.

>[!NOTE]
>
>A soma da contribuição percentual para um modelo de atribuição em todos os pontos de contato e posições deve ser igual a 100.

![ponto de contato de detalhamento de caminho de usuário](./images/insights/user-paths.png)

## Principais caminhos de conversão

O gráfico **[!UICONTROL Top conversion paths]** mostra as pontuações influenciadas e algorítmicas nos principais caminhos de conversão nas regiões selecionadas. Este gráfico permite visualizar quais pontos de contato contribuem para conversões e qual é a pontuação de atribuição para cada ponto de contato. É possível usar essas informações para exibir os caminhos mais frequentes em uma determinada região e ver se algum padrão surge entre os diferentes conjuntos de pontos de contato.

![Caminhos de usuário mais comuns](./images/insights/Touchpoint-paths.png)

## Eficácia do ponto de contato

Selecionar a guia **[!UICONTROL Touchpoint Effectiveness]** carrega o cartão **[!UICONTROL Touchpoint effectiveness]**. Esse cartão usa a distribuição de dados da IA de atribuição para exibir informações para cada ponto de contato. Os dados desta tabela são gerados apenas por períodos específicos, conforme indicado pela data **[!UICONTROL As of]** no canto superior direito do cartão.

![seleção da eficácia do ponto de contato](./images/insights/Touchpoint-effectiveness.png)

Você pode usar as informações do cartão **[!UICONTROL Touchpoint effectiveness]** para entender como um ponto de contato contribui para uma conversão. Você também pode ver a eficiência de cada ponto de contato com as seguintes métricas de desempenho:

**Caminhos tocados**: essa métrica exibe uma porcentagem de caminhos que atingem/não atingem a conversão para o ponto de contato. Você verá conversões atribuídas mais altas se a proporção de caminhos (porcentagem) que alcançam a conversão para caminhos que não alcançam a conversão for alta.

![Métrica de caminhos tocados](./images/insights/Touchpoint-metrics.png)

**Medida de eficiência**: essa métrica exibe estrelas em uma escala de um a cinco. A escala indica a importância relativa de um ponto de contato para fazer uma conversão.

>[!NOTE]
>
>Um maior volume de pontos de contato não garante uma medida de eficiência mais alta.

**Volume total**: o número agregado de vezes que um ponto de contato foi tocado por um usuário. Isso inclui os pontos de contato que aparecem em um caminho que alcança a conversão, bem como caminhos que não resultam em uma conversão.

## Próximas etapas

Quando terminar de filtrar os dados e puder exibir as informações apropriadas, você terá a opção de acessar as pontuações. Para obter um guia detalhado sobre como acessar suas pontuações, visite o [tutorial de pontuações de acesso na IA de atribuição](./download-scores.md). Além disso, você também pode baixar os dados de resumo conforme indicado em [mais ações](#more-actions). Selecionar &quot;Baixar dados de resumo&quot; baixa os dados de resumo agregados por datas.

## Recursos adicionais

O vídeo a seguir foi projetado para ajudar a saber como usar a página de insights do Attribution AI para entender o ROI de canais e campanhas de marketing.

>[!VIDEO](https://video.tv.adobe.com/v/32669?learn=on&quality=12)
