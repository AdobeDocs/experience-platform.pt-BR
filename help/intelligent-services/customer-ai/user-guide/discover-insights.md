---
keywords: Experience Platform;insights;customer ai;popular topics;customer ai insights
solution: Experience Platform, Intelligent Services, Real-time Customer Data Platform
title: Descobrindo insights com a IA do cliente
topic: Discovering insights
description: Este documento serve como um guia para interagir com as informações da instância do serviço na interface do usuário da API do cliente do Intelligent Services.
translation-type: tm+mt
source-git-commit: de16ebddd8734f082f908f5b6016a1d3eadff04c
workflow-type: tm+mt
source-wordcount: '1389'
ht-degree: 1%

---


# Descobrindo insights com a IA do cliente

A IA do cliente, como parte dos Serviços inteligentes, fornece aos comerciantes o poder de aproveitar a Adobe Sensei para antecipar qual será a próxima ação dos clientes. o Customer AI é usado para gerar pontuações de propensão personalizadas, como churn e conversão para perfis individuais em escala. Isso é feito sem precisar transformar as necessidades de negócios em um problema de aprendizado em máquina, escolher um algoritmo, treinamento ou implantação.

Este documento serve como um guia para interagir com as informações da instância do serviço na interface do usuário da API do cliente do Intelligent Services.

## Introdução

Para utilizar insights para a IA do cliente, é necessário ter uma instância de serviço com um status de execução bem-sucedida disponível. Para criar uma nova instância de serviço, visite [Configuração de uma instância](./configure.md)do AI do cliente. Se você criou recentemente uma instância de serviço e ela ainda está treinando e marcando, aguarde 24 horas para que ela termine de ser executada.

## Visão geral da instância do serviço

Na [!DNL Adobe Experience Platform] interface do usuário, clique em **[!UICONTROL Serviços]** na navegação à esquerda. O navegador *Serviços* é exibido e exibe os Serviços inteligentes disponíveis. No container para API do cliente, clique em **[!UICONTROL Abrir]**.

![Acessar sua instância](../images/insights/navigate-to-service.png)

A página Serviço de IA do cliente é exibida. Esta página lista as instâncias de serviço da API do cliente e exibe informações sobre elas, incluindo o nome da instância, o tipo de propensão, a frequência de execução da instância e o status da última atualização.

>[!NOTE]
>
>Somente as instâncias de serviço que concluíram execuções de pontuação bem-sucedidas têm insights.

![Criar instância](../images/insights/dashboard.png)

Clique no nome de uma instância de serviço para começar.

![Criar instância](../images/insights/click-the-name.png)

Em seguida, a página de insights para essa instância de serviço será exibida, onde você receberá visualizações dos seus dados. As visualizações e o que você pode fazer com os dados são explicados com mais detalhes neste guia.

![página de configuração](../images/insights/landing-page.png)


### Detalhes da instância de serviço

Há duas maneiras de visualização detalhes da instância do serviço: do painel ou dentro da instância do serviço.

Para visualização de uma visão geral dos detalhes da instância do serviço no painel, selecione um container de instância do serviço, evitando o hiperlink anexado ao nome. Isso abre um painel direito que fornece detalhes adicionais. Os controles contêm o seguinte:

- **[!UICONTROL Editar]**: Selecionar **[!UICONTROL Editar]** permite modificar uma instância de serviço existente. Você pode editar o nome, a descrição e a frequência de pontuação da instância.
- **[!UICONTROL Clonar]**: Selecionar **[!UICONTROL Clonar]** copia a configuração da instância de serviço atualmente selecionada. Em seguida, você pode modificar o fluxo de trabalho para fazer ajustes secundários e renomeá-lo como uma nova instância.
- **[!UICONTROL Excluir]**: Você pode excluir uma instância de serviço, incluindo quaisquer execuções históricas.
- **[!UICONTROL Fonte]** de dados: Um link para o conjunto de dados usado por esta instância.
- **[!UICONTROL Frequência]** de execução: Com que frequência uma execução de pontuação ocorre e quando.
- **[!UICONTROL Definição]** da pontuação: Uma visão geral rápida da meta configurada para esta instância.

![](../images/user-guide/service-instance-panel.png)

>[!NOTE]
>
>No evento de que uma execução de pontuação falhe, uma mensagem de erro é fornecida. A mensagem de erro é listada em Detalhes **da** última execução no painel direito, que está visível apenas para execução com falha.

![falha ao executar mensagem](../images/insights/failed-run.png)

A segunda maneira de visualização de detalhes adicionais para uma instância de serviço está localizada na página de insights. Você pode clicar em **[!UICONTROL Mostrar mais]** no canto superior direito para preencher uma lista suspensa. Os detalhes são listados como a definição da pontuação, quando ela foi criada e o tipo de propensão. Para obter mais informações sobre qualquer uma das propriedades listadas, visite [Configuração de uma instância](./configure.md)do AI do cliente.

![mostrar mais](../images/insights/landing-show-more.png)

![mostrar mais](../images/insights/show-more.png)

### Editar uma instância

Para editar uma instância, clique em **[!UICONTROL Editar]** na navegação superior direita.

![clique no botão editar](../images/insights/edit-button.png)

A caixa de diálogo de edição é exibida, permitindo que você edite o nome, a descrição, o status e a frequência de pontuação da instância. Para confirmar suas alterações e fechar a caixa de diálogo, selecione **[!UICONTROL Salvar]** no canto inferior direito.

![editar fornecedor](../images/insights/edit-instance.png)

### Mais ações

O botão **[!UICONTROL Mais ações]** está localizado na navegação superior direita ao lado de **[!UICONTROL Editar]**. Clicar em **[!UICONTROL Mais ações]** abre uma lista suspensa que permite selecionar uma das seguintes operações:

- **[!UICONTROL Clonar]**: Selecionar **[!UICONTROL Clonar]** copia a instância de serviço configurada. Em seguida, você pode modificar o fluxo de trabalho para fazer ajustes secundários e renomeá-lo como uma nova instância.
- **[!UICONTROL Excluir]**: Exclui a instância.
- **[!UICONTROL Pontuações]** de acesso: Selecionar pontuações **[!UICONTROL de]** acesso abre uma caixa de diálogo que fornece um link para as pontuações de [download do tutorial de IA](./download-scores.md) do cliente, a caixa de diálogo também fornece a ID do conjunto de dados necessária para fazer chamadas de API.
- **[!UICONTROL Histórico]** de execução da visualização: Uma caixa de diálogo contendo uma lista de todas as execuções de pontuação associadas à instância do serviço é exibida.

![mais ações](../images/insights/more-actions.png)

## Resumo da pontuação {#scoring-summary}

O resumo de pontuação exibe o número total de perfis pontuados e os categoriza em compartimentos que contêm alta, média e baixa propensão. Os compartimentos de propensão são determinados com base no intervalo de pontuação, baixa é menor que 24, média é de 25 a 74 e alta é acima de 74. Cada bucket tem uma cor correspondente à legenda.

>[!NOTE]
>
>Se for uma pontuação de propensão de conversão, as pontuações altas serão exibidas em verde e as pontuações baixas em vermelho. Se você está predizendo que a propensão de churn é invertida, as altas pontuações estão em vermelho e as baixas pontuações são verdes. O bucket médio permanece amarelo independentemente do tipo de propensão escolhido.

![resumo da pontuação](../images/insights/scoring-summary.png)

É possível passar o mouse sobre qualquer cor do anel para obter informações adicionais de visualização, como uma porcentagem e o número total de perfis pertencentes a um bucket.

![](../images/insights/scoring-ring.png)

## Distribuição das pontuações

O cartão de **[!UICONTROL distribuição de pontuações]** fornece um resumo visual da população com base na pontuação. As cores que você vê no cartão [!UICONTROL Distribuição de pontuações] representam o tipo de pontuação de propensão gerada. Passar o mouse sobre qualquer distribuição de pontuação fornece a contagem exata pertencente a essa distribuição.

![distribuição das pontuações](../images/insights/distribution-of-scores.png)

## Fatores influentes

Para cada grupo de pontuação, é gerado um cartão que mostra os 10 fatores influentes principais para esse grupo. Os fatores influentes fornecem detalhes adicionais sobre por que seus clientes pertencem a vários grupos de pontuação.

![Fatores influentes](../images/insights/influential-factors.png)

### Derivados de fatores influentes

Passar o mouse sobre qualquer um dos principais fatores influentes desagrega ainda mais os dados. Você recebe uma visão geral sobre por que certos perfis pertencem a um grupo de propensão. Dependendo do fator, você pode receber valores numéricos, categóricos ou booleanos. O exemplo abaixo exibe valores categóricos por região.

![captura de tela de detalhamento](../images/insights/drilldown.png)

Além disso, usando detalhamentos, você pode comparar um fator de distribuição se ele ocorrer em dois ou mais compartimentos de propensão e criar segmentos mais específicos com esses valores. O exemplo a seguir ilustra o primeiro caso de uso:

![](../images/insights/drilldown-compare.png)

Você pode ver que perfis com baixa propensão para conversão têm menos probabilidade de ter feito uma visita recente às páginas da Web adobe.com. O fator &quot;Dias desde a última visita à web&quot; tem apenas 8% de cobertura em comparação com 26% em perfis de propensão média. Usando esses números, você pode comparar a distribuição dentro de cada grupo para o fator. Essas informações podem ser usadas para inferir que a recenticidade na visita da Web não é tão influente no balde de baixa propensão, como no balde de propensão média.

### Criar um segmento

Selecionar o botão **[!UICONTROL Criar segmento]** em qualquer um dos compartimentos para propensão baixa, média e alta redireciona você para o construtor de segmentos.

>[!NOTE]
>
>O botão **[!UICONTROL Criar segmento]** só estará disponível se o Perfil do cliente em tempo real estiver ativado para o conjunto de dados. Para obter mais informações sobre como ativar o Perfil do cliente em tempo real, visite a visão geral [do Perfil do cliente em tempo](../../../rtcdp/overview.md)real.

![Clique em criar segmento](../images/insights/influential-factors-create-segment.png)

![Criar um segmento](../images/insights/create-segment.png)

O construtor de segmentos é usado para definir um segmento. Ao selecionar **[!UICONTROL Criar segmento]** na página Insights, a API do cliente adiciona automaticamente as informações dos buckets selecionados ao segmento. Para concluir a criação do segmento, basta preencher os container *Nome* e *Descrição* localizados no painel direito da interface do usuário do construtor de segmentos. Depois de fornecer um nome e uma descrição ao segmento, clique em **[!UICONTROL Salvar]** no canto superior direito.

>[!NOTE]
>
>Como as pontuações de propensão são gravadas no perfil individual, elas estão disponíveis no Construtor de segmentos, como qualquer outro atributo do perfil. Ao navegar até o construtor de segmentos para criar novos segmentos, você pode ver todas as várias pontuações de propensão em sua IA do cliente de namespace.

![Preenchimento do segmento em](../images/insights/segment-saving.png)

Para visualização do novo segmento na interface do usuário da plataforma, clique em **[!UICONTROL Segmentos]** no painel de navegação esquerdo. A página **[!UICONTROL Procurar]** é exibida e exibe todos os segmentos disponíveis.

![Todos os seus segmentos](../images/insights/Segments-dashboard.png)

## Próximas etapas

Este documento descreveu os insights fornecidos por uma instância de serviço de IA do cliente. Agora você pode continuar com o tutorial sobre como [baixar pontuações no AI](./download-scores.md) do cliente ou navegar pelos outros guias de Serviços [inteligentes do](../../home.md) Adobe que são oferecidos.

## Recursos adicionais

O vídeo a seguir descreve como usar a IA do cliente para ver a saída dos modelos e fatores influentes.

>[!VIDEO](https://video.tv.adobe.com/v/32666?learn=on&quality=12)