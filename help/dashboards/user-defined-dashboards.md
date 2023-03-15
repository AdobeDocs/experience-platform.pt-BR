---
title: Painéis definidos pelo usuário
description: Saiba como criar e gerenciar painéis personalizados onde você pode criar, adicionar e editar widgets personalizados para visualizar as métricas principais.
exl-id: a9ab83f7-b68d-4dbf-9dc6-ef253df5c82c
source-git-commit: cde7c99291ec34be811ecf3c85d12fad09bcc373
workflow-type: tm+mt
source-wordcount: '956'
ht-degree: 0%

---

# Painéis definidos pelo usuário

Os Painéis do Adobe Experience Platform ajudam você a acelerar insights e personalizar a visualização por meio do recurso de painéis definido pelo usuário. Este recurso permite que você crie e gerencie painéis personalizados onde é possível criar, adicionar e editar widgets personalizados para visualizar as métricas principais relevantes para sua organização.

<!-- Getting started / permissions section commented out for Beta. This will be necessary after GA only

## Getting started

To view dashboards in Adobe Experience Platform you must have the appropriate permissions enabled. Please read the [dashboards permissions documentation](./permissions.md#available-permissions) to learn how to grant users the ability to view, edit, and update Experience Platform dashboards using Adobe Admin Console. If you do not have administrator privileges for your organization, contact your product administrator to obtain the required permissions. -->

## Criar painéis personalizados

Para criar um painel personalizado, primeiro, navegue até o inventário do painel. Selecionar **[!UICONTROL Painéis]** da navegação à esquerda da interface do usuário do Platform, seguida por **[!UICONTROL Criar painel]**.

![O inventário do painel com Painéis na navegação à esquerda e &quot;Criar painel&quot; destacados.](./images/user-defined-dashboards/create-dashboard.png)

Antes de adicionar um painel personalizado, o inventário de painéis está vazio e exibe &quot;Nenhum painel encontrado&quot;. mensagem. Depois de criado, todos os painéis definidos pelo usuário são listados no inventário de painéis.

A variável [!UICONTROL Criar painel] será exibida. Insira um nome descritivo amigável para a coleção de dispositivos que você deseja criar e selecione **[!UICONTROL Salvar]**.

![A caixa de diálogo Criar painel.](./images/user-defined-dashboards/create-dashboard-dialog.png)

O painel em branco recém-criado é exibido com o nome escolhido no canto superior esquerdo da exibição.

## Criar um widget {#create-widget}

>[!CONTEXTUALHELP]
>id="platform_dashboards_udd_maxwidgets"
>title="Número máximo de widgets"
>abstract="Os painéis definidos pelo usuário suportam até dez widgets. Depois de adicionar dez widgets ao painel, a variável [!UICONTROL Adicionar novo widget] está desativada e aparece em cinza."

Na nova visualização de painel, selecione **[!UICONTROL Adicionar novo widget]** para iniciar o processo de criação do widget.

>[!IMPORTANT]
>
>Os painéis definidos pelo usuário suportam até dez widgets. Depois de adicionar dez widgets ao painel, a variável [!UICONTROL Adicionar novo widget] está desativada e aparece em cinza.

![O novo painel vazio com Adicionar novo widget realçado.](./images/user-defined-dashboards/add-new-widget.png)

### Widget composer

A área de trabalho do compositor de widgets é exibida. Em seguida, selecione **[!UICONTROL Selecionar dados]** para escolher o modelo de dados a partir do qual adicionar atributos aos seus widgets.

![O espaço de trabalho do compositor de widgets.](./images/user-defined-dashboards/widget-composer.png)

A variável [!UICONTROL Selecionar dados] será exibida. Selecione um modelo de dados na coluna à esquerda para exibir uma lista de visualização de todas as tabelas disponíveis.

>[!NOTE]
>
>Atualmente, os painéis definidos pelo usuário são compatíveis apenas com o modelo de dados do perfil. Mais opções serão compatíveis.

![A janela para Selecionar os dados.](./images/user-defined-dashboards/select-data-dialog.png)

A lista de visualização fornece detalhes sobre as tabelas contidas no modelo de dados. A tabela abaixo fornece descrições dos campos de coluna e seus valores em potencial.

| Campo Coluna | Descrição |
|---|---|
| [!UICONTROL Title] | O nome da tabela. |
| [!UICONTROL Tipo de tabela] | O tipo de tabela. Os tipos possíveis incluem: `fact`, `dimension`, e `none`. |
| [!UICONTROL Pesquisas] | O número de tabelas unidas à tabela escolhida. |

Selecionar **[!UICONTROL Próxima]** para confirmar sua escolha de modelo de dados. A próxima exibição exibe uma lista das tabelas disponíveis no painel esquerdo. Selecione uma tabela para ver um detalhamento abrangente dos dados contidos na tabela selecionada.

A variável [!UICONTROL Visualizar] painel contém guias para [!UICONTROL Registros de amostra] e [!UICONTROL Atributos]. A variável [!UICONTROL Registros de amostra] A guia fornece um subconjunto dos registros da tabela selecionada em uma exibição tabulada. A variável [!UICONTROL Atributos] A guia fornece o nome do atributo, o tipo de dados e a tabela de origem para cada atributo associado à tabela selecionada.

Selecione uma tabela na lista disponível no painel à esquerda para fornecer dados para o widget e selecione **[!UICONTROL Selecionar]** para retornar ao widget composer.

![A caixa de diálogo Selecionar dados com a seleção realçada.](./images/user-defined-dashboards/select-a-table.png)

O widget composer agora é preenchido com dados da tabela escolhida.

O modelo de dados e a tabela selecionada no momento são exibidos na parte superior do painel à esquerda, e os atributos disponíveis para criar seu widget são listados na coluna atributos.

![Um widget preenchido com dados dentro do compositor de widgets.](./images/user-defined-dashboards/populated-widget-composer.png)

>[!TIP]
>
>Você pode alterar o modelo de dados escolhido selecionando o ícone de lápis (![Ícone de lápis.](./images/user-defined-dashboards/edit-icon.png)) no painel esquerdo.

Selecione o ícone de adição (./images/user-defined-dashboards/add-icon.png) ao lado de um nome de atributo para adicionar um atributo ao eixo X ou Y.

![O compositor de widgets com o menu suspenso de ícones adicionar é realçado para adicionar atributos a um eixo de widget.](./images/user-defined-dashboards/attributes-dropdown.png)

Em seguida, selecione o tipo de gráfico na [!UICONTROL Marcas] para gerar uma visualização prévia das configurações atuais do seu widget. No [!UICONTROL Propriedades] no lado direito da tela, digite um nome para o widget na caixa [!UICONTROL Título do widget] campo de texto.

![O compositor de widgets com a lista suspensa Marcas e o campo de texto do título do widget realçado.](./images/user-defined-dashboards/marks-dropdown-widget-title.png)

Quando estiver satisfeito com a seleção do widget **[!UICONTROL Salvar]**. Um ícone de marca de verificação abaixo do nome do widget indica que o widget foi salvo.

>[!NOTE]
>
>Salvar no widget composer salva o widget localmente no painel. Se você sair do editor de painel sem salvar o painel, o widget não será salvo no painel.

![Confirmação de salvamento do novo widget.](./images/user-defined-dashboards/save-confirmation.png)

Selecionar **[!UICONTROL Cancelar]** para retornar ao painel personalizado.

![O compositor de widgets com um widget de exemplo criado.](./images/user-defined-dashboards/composed-widget.png)

>[!TIP]
>
>Selecione o ícone de configuração ao lado do nome do painel para ver detalhes sobre a criação. Você pode alterar o nome do painel na caixa de diálogo exibida.

Os widgets podem ser reorganizados e redimensionados enquanto estiverem neste espaço de trabalho. Selecionar **[!UICONTROL Salvar]** para preservar o nome do painel e o layout configurado.

![O painel definido pelo usuário com um widget personalizado e o botão Salvar realçado.](./images/user-defined-dashboards/user-defined-dashboard.png)

Para garantir que cada consulta de um painel de insights do Adobe Real-time Customer Data Platform tenha recursos suficientes para ser executada com eficiência, a API rastreia o uso de recursos atribuindo slots de simultaneidade a cada consulta. O sistema pode processar até quatro queries simultâneas e, portanto, quatro slots de query simultâneos estarão disponíveis a qualquer momento. As consultas são colocadas em uma fila com base em slots de simultaneidade e, em seguida, aguardam na fila até que slots de simultaneidade suficientes estejam disponíveis.

## Próximas etapas e recursos adicionais

Ao ler este documento, você tem uma melhor compreensão de como criar um painel personalizado e como criar, editar e atualizar widgets personalizados para esse painel.

Para descobrir as métricas e visualizações pré-configuradas disponíveis para o [perfis](./guides/profiles.md#standard-widgets), [segmentos](./guides/segments.md#standard-widgets), e [destinos](./guides/destinations.md#standard-widgets) painéis, consulte a lista de widgets padrão em sua respectiva documentação.

Para reforçar sua compreensão dos painéis definidos pelo usuário no Experience Platform, assista ao vídeo a seguir:

>[!VIDEO](https://video.tv.adobe.com/v/3409637?quality=12&learn=on)
