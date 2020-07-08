---
keywords: Experience Platform;insights;attribution ai;popular topics
solution: Experience Platform
title: Descobrindo insights no AI de Atribuição
topic: Attribution AI insights
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '1164'
ht-degree: 1%

---


# Descobrindo insights no AI de Atribuição

As instâncias do serviço de IA de atribuição fornecem informações que podem ser usadas para auxiliar na tomada e medição de decisões de marketing relacionadas ao desempenho de marketing e retorno sobre o investimento. A seleção de uma instância de serviço fornece visualizações e filtros para ajudá-lo a entender o impacto de cada interação do cliente em cada fase da jornada do cliente.

Este documento serve como um guia para interagir com insights de instância de serviço na interface do usuário do Adobe Intelligent Services.

## Introdução

Para utilizar insights para a Atribuição AI, é necessário ter uma instância de serviço com um status de execução bem-sucedida disponível. Para criar uma nova instância do serviço, visite o guia [da interface do usuário da](./user-guide.md)Atribuição AI. Se você criou recentemente uma instância de serviço e ela ainda está treinando e marcando, aguarde 24 horas para terminar a execução.

## Visão geral dos insights da instância de serviço

Na [!DNL Adobe Experience Platform] interface do usuário, clique em **Serviços** na navegação à esquerda. O navegador *Serviços* é exibido e exibe os Serviços inteligentes da Adobe disponíveis. No container para Atribuição AI, clique em **Abrir**.

![Acessar sua instância](./images/insights/open_Attribution_ai.png)

A página do serviço AI de atribuição é exibida. Esta página lista as instâncias de serviço da Atribuição AI e exibe informações sobre elas, incluindo o nome da instância, os eventos de conversão, a frequência de execução da instância e o status da última atualização. Clique no nome de uma instância de serviço para começar.

>[!NOTE]
>
>Somente as instâncias de serviço que concluíram execuções de pontuação bem-sucedidas podem ser selecionadas.

![Criar instância](./images/insights/select-service-instance.png)

Em seguida, a página de insights para essa instância de serviço é exibida, onde você recebe visualizações e vários filtros para interagir com seus dados. As visualizações e os filtros são explicados com mais detalhes neste guia.

![página de configuração](./images/insights/landing-page.png)

### Detalhes da instância de serviço

Para visualização de detalhes adicionais para uma instância de serviço, clique em **Mostrar mais** no canto superior direito.

![mostrar mais](./images/insights/show-more.png)

Uma lista detalhada é exibida. Para obter mais informações sobre qualquer uma das propriedades listadas, visite o guia [do usuário da](./user-guide.md)Atribuição AI.

![mostrar detalhes](./images/insights/advanced-details.png)

### Editar uma instância

Para editar uma instância, clique em *Editar* na navegação superior direita.
![clique no botão editar](./images/insights/edit-button.png)

A caixa de diálogo Editar é exibida, permitindo que você edite a descrição e a frequência de pontuação da instância. Para confirmar suas alterações e fechar a caixa de diálogo, clique em *Editar* no canto inferior direito.

![editar fornecedor](./images/insights/edit-popover.png)

### Mais ações {#more-actions}

O botão *Mais ações* está localizado na navegação superior direita ao lado de *Editar*. Clicar em **Mais ações** abre uma lista suspensa que permite selecionar uma das seguintes operações:

- **Excluir**: Exclui a instância.
- **Baixar dados** de resumo: Faz o download de um arquivo CSV que contém os dados de resumo.
- **Pontuações** de acesso: Clicar em Pontuações *de* acesso o redireciona para as Pontuações de [acesso do tutorial](./download-scores.md)AI de atribuição.
- **Histórico** de execução da Visualização: Um provedor que contém uma lista de todas as execuções de pontuação associadas à instância do serviço é exibido.

![mais ações](./images/insights/more-actions.png)

## Filtrar seus dados

Os insights da AI de atribuição permitem filtrar seus dados e atualizar automaticamente os visuais da interface com base nos filtros selecionados.

>[!NOTE]
>
>Por padrão, cada filtro é definido como &quot;Todos&quot;, exceto o filtro do modelo *de* Atribuição, que é definido como &quot;Conversões atribuídas incrementais e influenciadas&quot;.

### evento de conversão

Quando você cria uma nova instância na Atribuição AI, um dos campos obrigatórios é &quot;eventos de conversão&quot;. Os eventos de conversão são objetivos de negócios que identificam o impacto das atividades de marketing, como pedidos de comércio eletrônico, compras na loja e visitas ao site.

Na instância, a lista suspensa eventos *de* conversão permite selecionar qualquer um dos eventos definidos para sua instância para filtrar seus dados. A seleção de eventos específicos altera as visualizações da interface para preencher somente as conversões pertencentes a esses eventos.

![evento de conversão](./images/insights/conversion-event.png)

### Modelo de atribuição

Clicar no modelo *de* Atribuição abre uma lista suspensa com todos os diferentes modelos de atribuição disponíveis. Você pode selecionar vários modelos para comparar resultados. Para obter mais informações sobre os diferentes modelos de atribuição e como eles funcionam, visite a visão geral do AI [de](./overview.md) atribuição que contém uma tabela com informações sobre cada modelo.

![modelo de atribuição](./images/insights/attribution-model.png)

### Produto

O filtro *Produto* permite selecionar entre quaisquer produtos que foram inicialmente ingeridos na criação da sua instância. Clique na lista suspensa e use o recurso de pesquisa para selecionar rapidamente todos os produtos que deseja comparar.

![filtro de produtos](./images/insights/product-filter.png)

### Geografia

O filtro *Geografia* preenche códigos de países com base em modelos baseados em região. Dependendo dos seus dados, este filtro pode ou não estar presente.

>[!NOTE]
>
>Os códigos de país têm dois caracteres. Uma lista completa pode ser encontrada aqui [ISO 3166-1 alfa-2](https://datahub.io/core/country-list).

### Região

>[!NOTE]
>
>Esse filtro só estará presente se você tiver realizado a modelagem [opcional baseada na](./user-guide.md#region-based-modeling-optional) região da etapa no guia da interface do usuário do AI de atribuição ao criar a instância do serviço.

Esse filtro permite que você selecione quaisquer regiões configuradas no processo de criação de instâncias.

### Channel

Clicar no filtro *Canal* revela uma lista suspensa que contém todos os canais de marketing disponíveis. Você pode selecionar vários canais para compará-los.

![Channel](./images/insights/channel.png)

### Date Range

Clique no ícone de calendário para abrir o intervalo de datas. As datas de início e término do evento de conversão determinam a quantidade de dados preenchidos na interface do usuário. Você pode escolher restringir ou ampliar o intervalo de datas para focar ou expandir a quantidade de dados preenchidos.

![intervalo de datas](./images/insights/display-date-range.png)

## Visão geral de seus dados

O cartão *Visão geral* mostra o total de conversões por modelo de atribuição. O número total muda com base no quão específico você faz sua pesquisa usando os filtros descritos anteriormente neste documento. Selecionar mais modelos adiciona círculos adicionais à Visão geral, cada um com sua própria cor correspondente à legenda.

![visão geral](./images/insights/Overview.png)

## Tendências semanais

O cartão de tendências ** semanais detalha sua conversão total pelo intervalo de datas definido durante o processo de filtragem.

![tendências](./images/insights/weekly-trends.png)

Clicar nas elipses na parte superior direita do cartão de tendências ** semanais exibe uma lista suspensa que permite selecionar tendências diárias, semanais ou mensais.

Passar o mouse sobre a linha de dados de um modelo de atribuição específico cria um provedor que mostra o número total de conversões para essa data.

![tendências de flutuação](./images/insights/weekly-trend-hover.png)

## Detalhamento por canal

A *Análise por placa de canal* é usada para determinar o número total de conversões em relação a cada canal. Este cartão pode ser utilizado para ajudar a tomar decisões sobre a eficácia de cada canal e o retorno do investimento.

![canal detalhado](./images/insights/channel-breakdown.png)

Clicar nas elipses na parte superior direita do cartão *Detalhamento por canal* abre uma lista suspensa que permite preencher dados com base em pontos de contato.

![pontos de contato](./images/insights/breakdown-by-touchpoints.png)

## Principais campanhas

A placa *Top campanha* exibe uma visão geral das campanhas e o desempenho da campanha em cada canal. Este cartão pode ajudar a informar sua equipe sobre a eficácia de uma campanha específica para um determinado canal e fornecer informações sobre onde investir mais.

![campanhas principais](./images/insights/top-campaigns.png)

## Próximas etapas

Depois que você terminar de filtrar os dados e puder exibir as informações apropriadas, terá a opção de acessar as pontuações. Para obter um guia detalhado sobre como acessar suas pontuações, visite as pontuações de [acesso no tutorial do AI](./download-scores.md) de atribuição. Além disso, você também pode baixar seus dados de resumo conforme indicado em [mais ações](#more-actions). Selecionar &quot;Baixar dados de resumo&quot; faz o download dos dados de resumo agregados por datas.

## Recursos adicionais

O vídeo a seguir foi criado para ajudar a aprender como usar a página de insights da Atribuição AI para entender o ROI de canais e campanhas de marketing.

>[!VIDEO](https://video.tv.adobe.com/v/32669?learn=on&quality=12)