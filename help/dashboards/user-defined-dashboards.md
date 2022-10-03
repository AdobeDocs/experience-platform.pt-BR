---
title: Painéis definidos pelo usuário
description: Saiba como criar e gerenciar painéis personalizados, onde você pode criar, adicionar e editar widgets de contexto para visualizar métricas principais.
exl-id: a9ab83f7-b68d-4dbf-9dc6-ef253df5c82c
source-git-commit: d874fed681449c6f5114196cface157c8c406d69
workflow-type: tm+mt
source-wordcount: '938'
ht-degree: 0%

---

# Painéis definidos pelo usuário

Os painéis do Adobe Experience Platform ajudam a agilizar insights e personalizar a visualização por meio do recurso de painéis definidos pelo usuário. Esse recurso permite criar e gerenciar painéis personalizados, onde você pode criar, adicionar e editar widgets de sobreposição para visualizar métricas principais relevantes para a sua organização.

>[!IMPORTANT]
>
>Para garantir que cada query de um painel do Real-time Customer Data Platform Insights tenha recursos suficientes para ser executada com eficiência, a API rastreia o uso dos recursos atribuindo slots de simultaneidade a cada query. O sistema pode processar até quatro queries simultâneos e, portanto, quatro slots de query simultâneos estão disponíveis em um determinado momento. As consultas são colocadas em uma fila com base em slots de simultaneidade e, em seguida, aguardam na fila até que haja slots de simultaneidade suficientes disponíveis.


<!-- Getting started / permissions section commented out for Beta. This will be necessary after GA only

## Getting started

To view dashboards in Adobe Experience Platform you must have the appropriate permissions enabled. Please read the [dashboards permissions documentation](./permissions.md#available-permissions) to learn how to grant users the ability to view, edit, and update Experience Platform dashboards using Adobe Admin Console. If you do not have administrator privileges for your organization, contact your product administrator to obtain the required permissions. -->

## Criar painéis personalizados

Para criar um painel personalizado, primeiro navegue até o inventário do painel. Selecionar **[!UICONTROL Painéis]** na navegação à esquerda da interface do usuário da plataforma, seguida por **[!UICONTROL Criar painel]**.

![O inventário do painel com Painéis na navegação à esquerda e &quot;Criar painel&quot; realçado.](./images/user-defined-dashboards/create-dashboard.png)

Antes de adicionar um painel personalizado, o inventário de painéis fica vazio e exibe &quot;Nenhum painel encontrado&quot;. mensagem. Depois de criados, todos os painéis definidos pelo usuário são listados no inventário do painel.

O [!UICONTROL Criar painel] será exibida. Insira um nome descritivo e amigável para a coleção de widgets que você pretende criar e selecione **[!UICONTROL Salvar]**.

![A caixa de diálogo Criar painel .](./images/user-defined-dashboards/create-dashboard-dialog.png)

O painel em branco recém-criado é exibido com o nome escolhido no canto superior esquerdo da exibição.

## Criar um widget {#create-widget}

>[!CONTEXTUALHELP]
>id="platform_dashboards_udd_maxwidgets"
>title="Número máximo de widgets"
>abstract="Painéis definidos pelo usuário suportam até dez widgets. Depois de adicionar dez widgets ao painel, a [!UICONTROL Adicionar novo widget] está desativada e é exibida em cinza."

Na nova exibição do painel, selecione **[!UICONTROL Adicionar novo widget]** para iniciar o processo de criação de widgets.

>[!IMPORTANT]
>
>Painéis definidos pelo usuário suportam até dez widgets. Depois de adicionar dez widgets ao painel, a [!UICONTROL Adicionar novo widget] está desativada e é exibida em cinza.

![O novo painel vazio com Adicionar novo widget destacado.](./images/user-defined-dashboards/add-new-widget.png)

### Compositor de widget

A área de trabalho do compositor de widgets é exibida. Em seguida, selecione **[!UICONTROL Selecionar dados]** para escolher o modelo de dados do qual adicionar atributos aos seus widgets.

![A área de trabalho do compositor de widgets.](./images/user-defined-dashboards/widget-composer.png)

O [!UICONTROL Selecionar dados] será exibida. Selecione um modelo de dados na coluna esquerda para exibir uma lista de visualização de todas as tabelas disponíveis.

>[!NOTE]
>
>Atualmente, os painéis definidos pelo usuário são compatíveis apenas com o modelo de dados de perfil. Mais opções serão suportadas.

![A caixa de diálogo Selecionar dados.](./images/user-defined-dashboards/select-data-dialog.png)

A lista de visualização fornece detalhes sobre as tabelas contidas no modelo de dados. A tabela abaixo fornece descrições dos campos de coluna e seus valores em potencial.

| Campo de coluna | Descrição |
|---|---|
| [!UICONTROL Title] | O nome da tabela. |
| [!UICONTROL Tipo de tabela] | O tipo de tabela. Os tipos potenciais incluem: `fact`, `dimension`e `none`. |
| [!UICONTROL Pesquisas] | O número de tabelas unidas à tabela escolhida. |

Selecionar **[!UICONTROL Próximo]** para confirmar a escolha do modelo de dados. A próxima exibição exibe uma lista das tabelas disponíveis no painel à esquerda. Selecione uma tabela para ver um detalhamento abrangente dos dados contidos na tabela selecionada.

O [!UICONTROL Visualizar] painel contém guias para [!UICONTROL Registros de amostra] e [!UICONTROL Atributos]. O [!UICONTROL Registros de amostra] A guia fornece um subconjunto dos registros da tabela selecionada em uma exibição tabulada. O [!UICONTROL Atributos] A guia fornece o nome do atributo, o tipo de dados e a tabela de origem para cada atributo associado à tabela selecionada.

Selecione uma tabela na lista disponível no painel esquerdo para fornecer dados para o widget e selecione **[!UICONTROL Selecionar]** para retornar ao compositor de widget.

![A caixa de diálogo selecionar dados com selecionado destacado.](./images/user-defined-dashboards/select-a-table.png)

O compositor de widget agora é preenchido com dados da tabela escolhida.

O modelo de dados e a tabela selecionada no momento são exibidos na parte superior do painel à esquerda, e os atributos disponíveis para criar seu widget são listados na coluna de atributos.

![Um widget preenchido com dados no compositor de widget.](./images/user-defined-dashboards/populated-widget-composer.png)

>[!TIP]
>
>Você pode alterar o modelo de dados escolhido selecionando o ícone de lápis (![Ícone Lápis .](./images/user-defined-dashboards/edit-icon.png)) no painel esquerdo.

Selecione o ícone adicionar (./images/user-defined-dashboards/add-icon.png) ao lado de um nome de atributo para adicionar um atributo ao eixo X ou Y.

![O compositor de widget com a lista suspensa adicionar ícone , destacado para adicionar atributos ao eixo do widget.](./images/user-defined-dashboards/attributes-dropdown.png)

Em seguida, selecione o tipo de gráfico ou tabela no [!UICONTROL Marcas] lista suspensa para gerar uma visualização das configurações atuais do widget. No [!UICONTROL Propriedades] no painel à direita da tela, digite um nome para o widget no [!UICONTROL Título do widget] campo de texto.

![O compositor de widget com o campo de texto suspenso Marcas e título do widget destacado.](./images/user-defined-dashboards/marks-dropdown-widget-title.png)

Quando estiver satisfeito com seu widget, selecione **[!UICONTROL Salvar]**. Um ícone de marca de verificação sob o nome do widget indica que ele foi salvo.

>[!NOTE]
>
>Salvar no compositor de widget salva o widget localmente em seu painel. Se você sair do editor de painel sem salvar o painel, o widget não será salvo no painel.

![Confirmação de salvamento de novo widget.](./images/user-defined-dashboards/save-confirmation.png)

Selecionar **[!UICONTROL Cancelar]** para retornar ao painel personalizado.

![O compositor de widget com um exemplo de widget criado.](./images/user-defined-dashboards/composed-widget.png)

>[!TIP]
>
>Selecione o ícone de configuração ao lado do nome do painel para ver detalhes sobre a criação. Você pode alterar o nome do seu painel na caixa de diálogo exibida.

Os widgets podem ser reorganizados e redimensionados enquanto estiverem nesse espaço de trabalho. Selecionar **[!UICONTROL Salvar]** para preservar o nome do painel e o layout configurado.

![O painel definido pelo usuário com um widget personalizado e o botão Salvar realçado.](./images/user-defined-dashboards/user-defined-dashboard.png)

## Próximas etapas

Ao ler este documento, você tem uma melhor compreensão de como criar um painel personalizado e como criar, editar e atualizar widgets personalizados para esse painel.

Para descobrir as métricas e visualizações pré-configuradas disponíveis para o [perfis](./guides/profiles.md#standard-widgets), [segmentos](./guides/segments.md#standard-widgets)e [destinos](./guides/destinations.md#standard-widgets) painéis, consulte a lista de widgets padrão em sua respectiva documentação.
