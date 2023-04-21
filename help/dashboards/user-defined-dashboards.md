---
title: Painéis definidos pelo usuário
description: Saiba como criar e gerenciar painéis personalizados, onde você pode criar, adicionar e editar widgets de contexto para visualizar métricas principais.
exl-id: a9ab83f7-b68d-4dbf-9dc6-ef253df5c82c
source-git-commit: a0be2f8625ca60f9c8f355c1230a889002436d6d
workflow-type: tm+mt
source-wordcount: '1307'
ht-degree: 4%

---

# Painéis definidos pelo usuário

Os painéis do Adobe Experience Platform ajudam a agilizar insights e personalizar a visualização por meio do recurso de painéis definidos pelo usuário. Esse recurso permite criar e gerenciar painéis personalizados, onde você pode criar, adicionar e editar widgets de sobreposição para visualizar métricas principais relevantes para a sua organização.

<!-- Getting started / permissions section commented out for Beta. This will be necessary after GA only

## Getting started

To view dashboards in Adobe Experience Platform you must have the appropriate permissions enabled. Please read the [dashboards permissions documentation](./permissions.md#available-permissions) to learn how to grant users the ability to view, edit, and update Experience Platform dashboards using Adobe Admin Console. If you do not have administrator privileges for your organization, contact your product administrator to obtain the required permissions. -->

## Criar um painel personalizado

Para criar um painel personalizado, primeiro navegue até o inventário do painel. Selecionar **[!UICONTROL Painéis]** na navegação à esquerda da interface do usuário da plataforma, seguida por **[!UICONTROL Criar painel]**.

![O inventário do painel com Painéis na navegação à esquerda e &quot;Criar painel&quot; realçado.](./images/user-defined-dashboards/create-dashboard.png)

Antes de adicionar um painel personalizado, o inventário de painéis fica vazio e exibe &quot;Nenhum painel encontrado&quot;. mensagem. Depois de criados, todos os painéis definidos pelo usuário são listados no inventário do painel.

>[!NOTE]
>
>Para editar um painel existente, selecione o nome do painel na lista de inventário seguido pelo ícone de lápis (![Um ícone de lápis.](./images/user-defined-dashboards/edit-icon.png))

O [!UICONTROL Criar painel] será exibida. Insira um nome descritivo e amigável para a coleção de widgets que você pretende criar e selecione **[!UICONTROL Salvar]**.

![A caixa de diálogo Criar painel .](./images/user-defined-dashboards/create-dashboard-dialog.png)

O painel em branco recém-criado é exibido com o nome escolhido no canto superior esquerdo da exibição.

## Criar um widget {#create-widget}

>[!CONTEXTUALHELP]
>id="platform_dashboards_udd_maxwidgets"
>title="Número máximo de widgets"
>abstract="Painéis definidos pelo usuário comportam até dez widgets. Depois de adicionar dez widgets ao painel, a opção [!UICONTROL Adicionar novo widget] fica desativada e é exibida em cinza."

Na nova exibição do painel, selecione **[!UICONTROL Adicionar novo widget]** para iniciar o processo de criação de widgets.

>[!IMPORTANT]
>
>Painéis definidos pelo usuário comportam até dez widgets. Depois de adicionar dez widgets ao painel, a opção [!UICONTROL Adicionar novo widget] fica desativada e é exibida em cinza.

![O novo painel vazio com Adicionar novo widget destacado.](./images/user-defined-dashboards/add-new-widget.png)

### Compositor de widget

A área de trabalho do compositor de widgets é exibida. Em seguida, selecione **[!UICONTROL Selecionar dados]** para escolher o modelo de dados do qual adicionar atributos aos seus widgets.

![A área de trabalho do compositor de widgets.](./images/user-defined-dashboards/widget-composer.png)

#### Selecionar modelo de dados {#select-data-model}

O [!UICONTROL Selecionar modelo de dados] será exibida. Selecione um modelo de dados na coluna esquerda para exibir uma lista de visualização de todas as tabelas disponíveis. O modelo de dados pré-configurado para Real-time Customer Data Platform é nomeado [!UICONTROL CDPInsights].

>[!TIP]
>
>Selecione o ícone de informações (![Um ícone de informações.](./images/user-defined-dashboards/info-icon.png)) para ver o nome completo do modelo de dados se for muito longo para ser exibido no painel de dados.

![A caixa de diálogo Selecionar dados.](./images/user-defined-dashboards/select-data-model-dialog.png)

A lista de visualização fornece detalhes sobre as tabelas contidas no modelo de dados. A tabela abaixo fornece descrições dos campos de coluna e seus valores em potencial.

| Campo de coluna | Descrição |
|---|---|
| [!UICONTROL Title] | O nome da tabela. |
| [!UICONTROL Tipo de tabela] | O tipo de tabela. Os tipos potenciais incluem: `fact`, `dimension`e `none`. |
| [!UICONTROL Registros] | O número de registros associados à tabela escolhida. |
| [!UICONTROL Pesquisas] | O número de tabelas unidas à tabela escolhida. |
| [!UICONTROL Atributos] | O número de atributos para a tabela escolhida. |

Selecionar **[!UICONTROL Próximo]** para confirmar a escolha do modelo de dados. A próxima exibição exibe uma lista das tabelas disponíveis no painel à esquerda. Selecione uma tabela para ver um detalhamento abrangente dos dados contidos na tabela selecionada.

### Preencher widget {#populate-widget}

O [!UICONTROL Visualizar] painel contém guias para [!UICONTROL Registros de amostra] e [!UICONTROL Atributos]. O [!UICONTROL Registros de amostra] A guia fornece um subconjunto dos registros da tabela selecionada em uma exibição tabulada. O [!UICONTROL Atributos] A guia fornece o nome do atributo, o tipo de dados e a tabela de origem para cada atributo associado à tabela selecionada.

Selecione uma tabela na lista disponível no painel esquerdo para fornecer dados para o widget e selecione **[!UICONTROL Selecionar]** para retornar ao compositor de widget.

![A caixa de diálogo selecionar dados com selecionado destacado.](./images/user-defined-dashboards/select-a-table.png)

O compositor de widget agora é preenchido com dados da tabela escolhida.

O modelo de dados e a tabela selecionada no momento são exibidos na parte superior do painel à esquerda, e os atributos disponíveis para criar seu widget são listados na [!UICONTROL Atributos] coluna. Use a barra de pesquisa para procurar atributos em vez de rolar a lista ou alterar o modelo de dados escolhido selecionando o ícone de lápis (![Ícone Lápis .](./images/user-defined-dashboards/edit-icon.png)) no painel esquerdo.

![Um widget preenchido com dados no compositor de widget.](./images/user-defined-dashboards/populated-widget-composer.png)

#### Adicionar e filtrar atributos {#add-and-filter-attributes}

Selecione o ícone adicionar (![Um ícone de adição.](./images/user-defined-dashboards/add-icon.png)) ao lado de um nome de atributo para adicionar um atributo ao seu widget. O menu suspenso que aparece permite adicionar um atributo como o eixo X, o eixo Y, uma cor ou um filtro para o widget. O [!UICONTROL Cor] permite diferenciar os resultados das marcas dos eixos X e Y com base na cor. Ele faz isso dividindo os resultados em cores diferentes com base em sua composição de um terceiro atributo.

>[!TIP]
>
>Se quiser inverter a disposição dos eixos X e Y, selecione o ícone de seta para cima e para baixo (![O ícone de seta para cima e para baixo.](./images/user-defined-dashboards/switch-axis-icon.png)) para alterar sua organização.

![O compositor de widget com o menu suspenso de adição destacado.](./images/user-defined-dashboards/attributes-dropdown.png)

Para alterar o tipo de gráfico ou gráfico do seu widget, selecione a variável [!UICONTROL Marcas] e escolha entre as opções disponíveis. As opções incluem barras, pontos, tiques, linhas ou área. Uma vez selecionada, uma visualização das configurações atuais do seu widget é gerada.

![O compositor de widget com a lista suspensa Marcas realçada.](./images/user-defined-dashboards/marks-dropdown.png)

Ao adicionar um atributo como filtro, é possível selecionar quais valores incluir ou excluir do widget. Depois de adicionar um filtro da lista de atributos, a variável [!UICONTROL Filtro] é exibida onde é possível selecionar ou desmarcar valores usando a caixa de seleção.

![A caixa de diálogo de filtro para filtrar valores do seu widget.](./images/user-defined-dashboards/filter-dialog.png)

### Propriedades do widget

Selecione o ícone de propriedades (![O ícone de propriedades.](./images/user-defined-dashboards/properties-icon.png)) no painel direito para abrir o painel de propriedades. No [!UICONTROL Propriedades] , digite um nome para o widget no painel [!UICONTROL Título do widget] campo de texto.

![O painel de propriedades com o ícone de propriedades e o campo Título do widget realçado.](./images/user-defined-dashboards/properties-panel.png)

No painel de propriedades do widget, é possível editar vários aspectos do widget. Você tem controle total para editar o local da legenda do widget. Para mover a legenda, selecione o [!UICONTROL Inserção de legenda] e escolha o local desejado na lista de opções disponíveis. Você também pode renomear o rótulo associado à legenda e o eixo X ou Y inserindo um novo nome na variável [!UICONTROL Título da legenda] campo de texto ou [!UICONTROL Rótulo do eixo] campo de texto, respectivamente.

#### Salvar o widget {#save-widget}

Salvar no compositor de widget salva o widget localmente em seu painel. Para salvar seu trabalho e retomar posteriormente, selecione **[!UICONTROL Salvar]**. Um ícone de marca de verificação sob o nome do widget indica que ele foi salvo. Como alternativa, quando estiver satisfeito com seu widget, selecione **[!UICONTROL Salvar e fechar]** para disponibilizar o widget para todos os outros usuários com acesso ao painel. Selecionar **[!UICONTROL Cancelar]** para abandonar seu trabalho e retornar ao painel personalizado.

![Confirmação de salvamento de novo widget.](./images/user-defined-dashboards/save-confirmation.png)

>[!TIP]
>
>Selecione o ícone de propriedades (![O ícone de propriedades.](./images/user-defined-dashboards/properties-icon.png)) ao lado do nome do painel para ver detalhes sobre a criação. Você pode alterar o nome do seu painel na caixa de diálogo exibida.

Os widgets podem ser reorganizados e redimensionados enquanto estiverem nesse espaço de trabalho. Selecionar **[!UICONTROL Salvar]** para preservar o nome do painel e o layout configurado.

![O painel definido pelo usuário com um widget personalizado e o botão Salvar realçado.](./images/user-defined-dashboards/user-defined-dashboard.png)

Para garantir que cada query de um painel do Adobe Real-time Customer Data Platform Insights tenha recursos suficientes para ser executada com eficiência, a API rastreia o uso dos recursos atribuindo slots de simultaneidade a cada query. O sistema pode processar até quatro queries simultâneos e, portanto, quatro slots de query simultâneos estão disponíveis em um determinado momento. As consultas são colocadas em uma fila com base em slots de simultaneidade e, em seguida, aguardam na fila até que haja slots de simultaneidade suficientes disponíveis.

## Próximas etapas e recursos adicionais

Ao ler este documento, você tem uma melhor compreensão de como criar um painel personalizado e como criar, editar e atualizar widgets personalizados para esse painel.

Para descobrir as métricas e visualizações pré-configuradas disponíveis para o [perfis](./guides/profiles.md#standard-widgets), [segmentos](./guides/segments.md#standard-widgets)e [destinos](./guides/destinations.md#standard-widgets) painéis, consulte a lista de widgets padrão em sua respectiva documentação.

Para reforçar sua compreensão dos painéis definidos pelo usuário no Experience Platform, assista ao seguinte vídeo:

>[!VIDEO](https://video.tv.adobe.com/v/3409637?quality=12&learn=on)
