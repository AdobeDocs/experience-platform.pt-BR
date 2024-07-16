---
keywords: Experience Platform;página inicial;tópicos populares;assimilação;assimilar dados em lote;tutorial;assimilação em lote;tutorial;guia da interface do usuário;
solution: Experience Platform
title: Assimilar Dados No Experience Platform
type: Tutorial
description: O Adobe Experience Platform permite importar dados facilmente como arquivos em lote na forma de arquivos do Parquet ou dados que estejam em conformidade com um esquema conhecido do Experience Data Model (XDM).
exl-id: a4a7358d-b117-4d81-8cb0-3dbbfeccdcbd
source-git-commit: 8351f6907a0dc4a4bba01c7f6e9dec7c376c8575
workflow-type: tm+mt
source-wordcount: '1321'
ht-degree: 0%

---

# Assimilar dados na Adobe Experience Platform

O Adobe Experience Platform permite importar dados facilmente para o [!DNL Platform] como arquivos em lote. Exemplos de dados a serem assimilados podem incluir dados de perfil de um arquivo simples em um sistema CRM (como um arquivo Parquet) ou dados que estejam em conformidade com um esquema [!DNL Experience Data Model] (XDM) conhecido no Registro de Esquemas.

## Introdução

Para concluir este tutorial, você deve ter acesso a [!DNL Experience Platform]. Se você não tiver acesso a uma organização no [!DNL Experience Platform], fale com o administrador do sistema antes de continuar.

Se você preferir assimilar dados usando as APIs de assimilação de dados, comece lendo o [Guia do desenvolvedor de assimilação em lote](../batch-ingestion/api-overview.md).

## Espaço de trabalho de conjuntos de dados

O espaço de trabalho Conjuntos de Dados no [!DNL Experience Platform] permite que você exiba e gerencie todos os conjuntos de dados criados por sua organização, bem como criar novos conjuntos.

Exiba o espaço de trabalho Conjuntos de dados clicando em **[!UICONTROL Conjuntos de dados]** na navegação à esquerda. O espaço de trabalho Conjuntos de dados contém uma lista de conjuntos de dados, incluindo colunas mostrando nome, criado (data e hora), origem, esquema e status do último lote, bem como a data e a hora em que o conjunto de dados foi atualizado pela última vez.

>[!NOTE]
>
>Clique no ícone de filtro ao lado da barra de Pesquisa para usar os recursos de filtragem para exibir apenas os conjuntos de dados habilitados para [!DNL Profile].

![Exibir todos os conjuntos de dados](../images/tutorials/ingest-batch-data/datasets-overview.png)

## Criar um conjunto de dados

Para criar um conjunto de dados, clique em **[!UICONTROL Criar conjunto de dados]** no canto superior direito do espaço de trabalho Conjuntos de dados.

![](../images/tutorials/ingest-batch-data/click-create-datasets.png)

Na tela **[!UICONTROL Criar Conjunto de Dados]**, selecione se deseja &quot;[!UICONTROL Criar Conjunto de Dados do Esquema]&quot; ou &quot;[!UICONTROL Criar Conjunto de Dados do Arquivo CSV]&quot;.

Neste tutorial, um esquema será usado para criar o conjunto de dados. Clique em **[!UICONTROL Criar Conjunto de Dados do Esquema]** para continuar.

![Selecionar fonte de dados](../images/tutorials/ingest-batch-data/create-dataset.png)

## Selecionar esquema do conjunto de dados

Na tela **[!UICONTROL Selecionar esquema]**, escolha um esquema clicando no botão de opção ao lado do esquema que deseja usar. Para este tutorial, o conjunto de dados será criado usando o esquema Membros de fidelidade. Usar a barra de pesquisa para filtrar esquemas é uma maneira útil de encontrar o esquema exato que você está procurando.

Depois de selecionar o botão de opção ao lado do esquema que deseja usar, clique em **[!UICONTROL Avançar]**.

![Selecionar esquema](../images/tutorials/ingest-batch-data/select-schema.png)

## Configurar conjunto de dados

Na tela **[!UICONTROL Configurar Conjunto de Dados]**, você deverá dar um nome ao conjunto de dados e também poderá fornecer uma descrição do conjunto de dados.

**Notas sobre Nomes de Conjuntos de Dados:**

- Os nomes dos conjuntos de dados devem ser curtos e descritivos para que possam ser facilmente encontrados na biblioteca posteriormente.
- Os nomes dos conjuntos de dados devem ser exclusivos, o que significa que eles também devem ser específicos o suficiente para não serem reutilizados no futuro.
- É uma prática recomendada fornecer informações adicionais sobre o conjunto de dados usando o campo de descrição, pois pode ajudar outros usuários a diferenciar entre conjuntos de dados no futuro.

Depois que o conjunto de dados tiver um nome e uma descrição, clique em **[!UICONTROL Concluir]**.

![Configurar conjunto de dados](../images/tutorials/ingest-batch-data/configure-dataset.png)

## Atividade do conjunto de dados

Um conjunto de dados vazio foi criado e você retornou à guia **[!UICONTROL Atividade do conjunto de dados]** no espaço de trabalho Conjuntos de Dados. Você deve ver o nome do conjunto de dados no canto superior esquerdo do espaço de trabalho, juntamente com uma notificação de que &quot;Nenhum lote foi adicionado&quot;. Isso é esperado, pois você ainda não adicionou lotes a esse conjunto de dados.

No lado direito do espaço de trabalho Conjuntos de Dados, você verá a guia **[!UICONTROL Informações]** que contém informações relacionadas ao seu novo conjunto de dados, como ID do conjunto de dados, nome, descrição, nome da tabela, esquema, fluxo e origem. A guia Informações também inclui informações sobre quando o conjunto de dados foi criado e sua última data de modificação.

Na guia Informações também há um botão de alternância **[!UICONTROL Perfil]**, usado para habilitar seu conjunto de dados para uso com o [!DNL Real-Time Customer Profile]. O uso desta opção, e [!DNL Real-Time Customer Profile], será explicado com mais detalhes na seção a seguir.

![Atividade do conjunto de dados](../images/tutorials/ingest-batch-data/sample-dataset.png)

## Habilitar conjunto de dados para [!DNL Real-Time Customer Profile]

Conjuntos de dados são usados para assimilar dados no [!DNL Experience Platform], e esses dados são usados para identificar indivíduos e unir informações provenientes de várias fontes. Essas informações agrupadas são chamadas de [!DNL Real-Time Customer Profile]. Para que [!DNL Platform] saiba quais informações devem ser incluídas em [!DNL Real-Time Profile], os conjuntos de dados podem ser marcados para inclusão usando a opção **[!UICONTROL Perfil]**.

Por padrão, esse botão de alternância está desativado. Se você optar por ativar ou desativar o [!DNL Profile], todos os dados assimilados no conjunto de dados serão usados para ajudar a identificar um indivíduo e compilar seus [!DNL Real-Time Profile].

Para saber mais sobre [!DNL Real-Time Customer Profile] e como trabalhar com identidades, reveja a documentação do [Serviço de Identidade](../../identity-service/home.md).

Para habilitar o conjunto de dados para [!DNL Real-Time Customer Profile], clique no botão de alternância **[!UICONTROL Perfil]** na guia **[!UICONTROL Informações]**.

![Alternância de perfil](../images/tutorials/ingest-batch-data/dataset-profile-toggle.png)

Uma caixa de diálogo será exibida solicitando que você confirme se deseja habilitar o conjunto de dados para [!DNL Real-Time Customer Profile].

![Habilitar caixa de diálogo Perfil](../images/tutorials/ingest-batch-data/enable-dataset-for-profile.png)

Clique em **[!UICONTROL Habilitar]** e o botão de alternância ficará azul, indicando que está ligado.

![Habilitado para Perfil](../images/tutorials/ingest-batch-data/profile-enabled-dataset.png)

## Adicionar dados ao conjunto de dados

Os dados podem ser adicionados a um conjunto de dados de várias maneiras diferentes. Você pode optar por usar [!DNL Data Ingestion] APIs ou um parceiro de ETL, como [!DNL Unifi] ou [!DNL Informatica]. Para este tutorial, dados serão adicionados ao conjunto de dados usando a guia **[!UICONTROL Adicionar dados]** na interface.

Para começar a adicionar dados ao conjunto de dados, clique na guia **[!UICONTROL Adicionar dados]**. Agora você pode arrastar e soltar arquivos ou procurar no computador os arquivos que deseja adicionar.

>[!NOTE]
>
>A Platform oferece suporte a dois tipos de arquivos para assimilação de dados: Parquet ou JSON. Você pode adicionar até cinco arquivos de cada vez, com o tamanho máximo de cada arquivo de 1 GB.

![Guia Adicionar Dados](../images/tutorials/ingest-batch-data/drag-and-drop.png)

## Carregar um arquivo {#upload-file}

Depois de arrastar e soltar (ou navegar e selecionar) um arquivo Parquet ou JSON que você deseja carregar, o [!DNL Platform] começará imediatamente a processar o arquivo e uma caixa de diálogo **[!UICONTROL Carregamento]** será exibida na guia **[!UICONTROL Adicionar Dados]** mostrando o progresso do carregamento do arquivo.

![Carregando caixa de diálogo](../images/tutorials/ingest-batch-data/uploading-file.png)

## Métricas de conjunto de dados

Após concluir o carregamento do arquivo, a guia **[!UICONTROL Atividade do conjunto de dados]** não mostra mais que &quot;Nenhum lote foi adicionado&quot;. Em vez disso, a guia **[!UICONTROL Atividade do conjunto de dados]** agora mostra métricas do conjunto de dados. Todas as métricas mostrarão &quot;0&quot; neste estágio, pois o lote ainda não foi carregado.

Na parte inferior da guia há uma lista mostrando a **[!UICONTROL ID do Lote]** dos dados que acabaram de ser assimilados pelo processo [&quot;Adicionar dados ao conjunto de dados&quot;](#add-data-to-dataset). Também estão incluídas informações relacionadas ao lote, incluindo a data de assimilação, o número de registros assimilados e o status atual do lote.

![Métricas do conjunto de dados](../images/tutorials/ingest-batch-data/batch-id.png)

## Detalhes do lote

Clique no **[!UICONTROL ID do Lote]** para exibir uma **[!UICONTROL Visão Geral do Lote]**, mostrando detalhes adicionais sobre o lote. Quando o carregamento do lote for concluído, as informações sobre o lote serão atualizadas para mostrar o número de registros assimilados e o tamanho do arquivo. O status também será alterado para &quot;Sucesso&quot; ou &quot;Falha&quot;. Se o lote falhar, a seção **[!UICONTROL Código de erro]** conterá detalhes sobre quaisquer erros durante a assimilação.

Para obter mais informações e perguntas frequentes sobre a assimilação em lote, consulte o [Guia de solução de problemas de assimilação em lote](../batch-ingestion/troubleshooting.md).

Para retornar à tela **[!UICONTROL Atividade do Conjunto de Dados]**, clique no nome do conjunto de dados (**[!UICONTROL Detalhes de Fidelidade]**) na navegação estrutural.

![Visão geral de lotes](../images/tutorials/ingest-batch-data/batch-details.png)

## Visualizar conjunto de dados

Quando o conjunto de dados estiver pronto, uma opção para **[!UICONTROL Visualizar Conjunto de Dados]** aparecerá na parte superior da guia **[!UICONTROL Atividade do Conjunto de Dados]**.

Clique em **[!UICONTROL Visualizar Conjunto de Dados]** para abrir uma caixa de diálogo mostrando dados de exemplo do conjunto de dados. Se o conjunto de dados foi criado usando um esquema, os detalhes do esquema do conjunto de dados aparecerão no lado esquerdo da visualização. É possível expandir o schema usando as setas para ver a estrutura do schema. Cada cabeçalho de coluna nos dados de visualização representa um campo no conjunto de dados.

![Detalhes do conjunto de dados](../images/tutorials/ingest-batch-data/dataset-preview.png)

## Próximas etapas e recursos adicionais

Agora que você criou um conjunto de dados e assimilou os dados com êxito no [!DNL Experience Platform], é possível repetir essas etapas para criar um novo conjunto de dados ou assimilar mais dados no conjunto de dados existente.

Para saber mais sobre a assimilação em lote, leia a [Visão geral de assimilação em lote](../batch-ingestion/overview.md) e complemente seu aprendizado assistindo ao vídeo abaixo.

>[!WARNING]
>
>A interface do usuário [!DNL Platform] mostrada no vídeo a seguir está desatualizada. Consulte a documentação acima para obter as capturas de tela e a funcionalidade mais recentes da interface.

>[!VIDEO](https://video.tv.adobe.com/v/27269?quality=12&learn=on)
