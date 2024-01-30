---
title: Exibir Insight SQL
description: Visualize o SQL por trás de seu perfil, público-alvo, destino e insights personalizados e execute a consulta sob demanda por meio do Editor de consultas.
source-git-commit: be90cf38970a54431f48799bf506fb0a20ec0166
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 0%

---

# Exibir insight SQL

Use o [!UICONTROL Exibir SQL] recurso para exibir o SQL por trás de seu Perfil, Público-alvo, Destino e insights personalizados e executar a consulta sob demanda por meio do Editor de consultas. Inspire-se no SQL de mais de 40 insights existentes para criar novas consultas que obtêm insights exclusivos dos dados da plataforma com base nas necessidades da empresa.

## Navegue até a visão geral do painel {#navigate-to-overview}

Para abrir o painel escolhido, selecione **[!UICONTROL Perfis]**, **[!UICONTROL Públicos-alvo]** ou **[!UICONTROL Destinos]** no painel de navegação esquerdo. Próxima seleção **[!UICONTROL Visão geral]** nas opções da guia, se o espaço de trabalho não for exibido automaticamente.

Como alternativa, selecione **[!UICONTROL Painéis]** na navegação à esquerda, seguido pelo nome do painel personalizado. A visão geral do painel definido pelo usuário é exibida.

![A interface do Experience Platform com [!UICONTROL Perfis], [!UICONTROL Públicos-alvo], [!UICONTROL Destinos], e [!UICONTROL Painéis] destacado.](./images/view-sql/dashboard-navigation.png)

## Alternância Exibir SQL {#toggle}

Um botão está disponível na visão geral do Perfil, Público-alvo, Destino e painéis definidos pelo usuário para ativar ou desativar o recurso.

>[!NOTE]
>
>Se você habilitar a opção [!UICONTROL Exibir SQL] você não pode alterar os filtros de nível global e de widget até desativar o recurso.

![A variável [!UICONTROL Exibir SQL] alternância realçada.](./images/view-sql/view-sql-toggle.png)

Ativar a alternância para exibição [!UICONTROL Exibir SQL] texto em cada insight individual.

![Um insight com [!UICONTROL Exibir SQL] destacado.](./images/view-sql/insight-view-sql.png)

Selecionar **[!UICONTROL Exibir SQL]** para abrir uma caixa de diálogo que contém o SQL do widget.

## Caixa de diálogo SQL {#sql-dialog}

Uma caixa de diálogo é exibida contendo o título do insight e do SQL que o gera.

>[!TIP]
>
>Você pode copiar toda a instrução SQL para a área de transferência selecionando o ícone copiar (![O ícone de cópia.](./images/view-sql/copy-icon.png)) na parte superior direita da caixa de diálogo.

![Uma caixa de diálogo de insight com a instrução SQL foi destacada.](./images/view-sql/sql-dialog.png)

Selecionar **[!UICONTROL Executar SQL]** para abrir o Editor de consultas com a consulta é pré-preenchida.

![Um diálogo de insight com o [!UICONTROL Executar SQL] destacado.](./images/view-sql/run-sql.png)

## Editar SQL existente {#edit-sql}

O Editor de consultas é exibido. Agora você pode editar a instrução e consultar os dados da plataforma de uma maneira que melhor atenda às suas necessidades de relatórios. Salve o novo modelo de consulta com um nome apropriado.

![O Editor de consultas com o SQL insight escolhido foi preenchido previamente.](./images/view-sql/edit-sql.png)

## Próximas etapas

Depois de ler este documento, agora você entende como acessar o SQL para qualquer insight nos painéis padrão ou em um painel definido pelo usuário. Se ainda não tiver feito isso, é recomendável que você leia a [Documento do modelo de dados do Real-time Customer Data Platform Insights](./cdp-insights-data-model.md). Esse documento contém insights sobre como personalizar modelos SQL para relatórios Real-Time CDP personalizados para suas necessidades de marketing e KPI.
