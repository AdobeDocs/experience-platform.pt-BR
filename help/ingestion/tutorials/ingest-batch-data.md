---
keywords: Experience Platform;home;popular topics;ingest batch data;tutorial;ingestão em lote;tutorial;utorial;guia ui;
solution: Experience Platform
title: Ingressar dados no Adobe Experience Platform
topic: tutorial
type: Tutorial
description: A Adobe Experience Platform permite importar facilmente dados como arquivos em lote na forma de arquivos ou dados do Parquet que estejam em conformidade com um schema conhecido do Experience Data Model (XDM).
translation-type: tm+mt
source-git-commit: 2940f030aa21d70cceeedc7806a148695f68739e
workflow-type: tm+mt
source-wordcount: '1323'
ht-degree: 0%

---


# Ingressar dados no Adobe Experience Platform

A Adobe Experience Platform permite importar facilmente dados para [!DNL Platform] como arquivos em lote. Exemplos de dados a serem ingeridos podem incluir dados de perfil de um arquivo simples em um sistema CRM (como um arquivo Parquet) ou dados que estejam em conformidade com um schema conhecido [!DNL Experience Data Model] (XDM) no Registro do Schema.

## Introdução

Para concluir este tutorial, é necessário ter acesso a [!DNL Experience Platform]. Se você não tiver acesso a uma Organização IMS em [!DNL Experience Platform], fale com o administrador do sistema antes de continuar.

Se preferir assimilar dados usando as APIs de ingestão de dados, comece lendo o [guia do desenvolvedor de ingestão em lote](../batch-ingestion/api-overview.md).

## Área de trabalho de conjuntos de dados

A área de trabalho de conjuntos de dados em [!DNL Experience Platform] permite que você visualização e gerencie todos os conjuntos de dados criados pela organização do IMS, bem como criar novos.

Visualização a área de trabalho Conjuntos de dados clicando em **[!UICONTROL Conjuntos de dados]** na navegação à esquerda. A área de trabalho Conjuntos de dados contém uma lista de conjuntos de dados, incluindo colunas que mostram o nome, a data e a hora, a origem, o schema e o status do último lote, bem como a data e a hora em que o conjunto de dados foi atualizado pela última vez.

>[!NOTE]
>
>Clique no ícone de filtro ao lado da barra Pesquisar para usar os recursos de filtragem para visualização somente dos conjuntos de dados habilitados para [!DNL Profile].

![Visualização de todos os conjuntos de dados](../images/tutorials/ingest-batch-data/datasets-overview.png)

## Criar um conjunto de dados

Para criar um conjunto de dados, clique em **[!UICONTROL Criar conjunto de dados]** no canto superior direito da área de trabalho Conjuntos de dados.

![](../images/tutorials/ingest-batch-data/click-create-datasets.png)

Na tela **[!UICONTROL Criar conjunto de dados]**, selecione se deseja &quot;[!UICONTROL Criar conjunto de dados do Schema]&quot; ou &quot;[!UICONTROL Criar conjunto de dados do arquivo CSV]&quot;.

Para este tutorial, um schema será usado para criar o conjunto de dados. Clique em **[!UICONTROL Criar conjunto de dados do Schema]** para continuar.

![Selecionar fonte de dados](../images/tutorials/ingest-batch-data/create-dataset.png)

## Selecionar schema de conjunto de dados

Na tela **[!UICONTROL Selecionar Schema]**, escolha um schema clicando no botão de opção ao lado do schema que deseja usar. Para este tutorial, o conjunto de dados será feito usando o schema Membros de Fidelidade. Usar a barra de pesquisa para filtrar schemas é uma maneira útil de encontrar o schema exato que você está procurando.

Depois de selecionar o botão de opção ao lado do schema que deseja usar, clique em **[!UICONTROL Avançar]**.

![Selecionar schema](../images/tutorials/ingest-batch-data/select-schema.png)

## Configurar conjunto de dados

Na tela **[!UICONTROL Configurar conjunto de dados]**, você deverá fornecer um nome ao conjunto de dados e também poderá fornecer uma descrição do conjunto de dados.

**Notas sobre os nomes dos conjuntos de dados:**

- Os nomes dos conjuntos de dados devem ser curtos e descritivos para que o conjunto de dados possa ser facilmente encontrado na biblioteca posteriormente.
- Os nomes dos conjuntos de dados devem ser exclusivos, o que significa que também devem ser específicos o suficiente para que não sejam reutilizados no futuro.
- É prática recomendada fornecer informações adicionais sobre o conjunto de dados usando o campo de descrição, pois pode ajudar outros usuários a diferenciarem entre conjuntos de dados no futuro.

Depois que o conjunto de dados tiver um nome e uma descrição, clique em **[!UICONTROL Concluir]**.

![Configurar conjunto de dados](../images/tutorials/ingest-batch-data/configure-dataset.png)

## Atividade do conjunto de dados

Um conjunto de dados vazio foi criado e você foi retornado para a guia **[!UICONTROL Atividade de conjunto de dados]** na área de trabalho Conjuntos de dados. Você deve ver o nome do conjunto de dados no canto superior esquerdo do espaço de trabalho, juntamente com uma notificação de que &quot;Nenhum lote foi adicionado.&quot; Isso é esperado, pois você ainda não adicionou nenhum lote a esse conjunto de dados.

No lado direito da área de trabalho dos conjuntos de dados, você verá a guia **[!UICONTROL Info]** contendo informações relacionadas ao seu novo conjunto de dados, como ID do conjunto de dados, nome, descrição, nome da tabela, schema, transmissão e origem. A guia Informações também inclui informações sobre quando o conjunto de dados foi criado e sua última data de modificação.

Também na guia Informações há uma alternância **[!UICONTROL Perfil]** usada para habilitar seu conjunto de dados para uso com [!DNL Real-time Customer Profile]. O uso dessa alternância e [!DNL Real-time Customer Profile] serão explicados com mais detalhes na seção a seguir.

![Atividade do conjunto de dados](../images/tutorials/ingest-batch-data/sample-dataset.png)

## Habilitar conjunto de dados para [!DNL Real-time Customer Profile]

Os conjuntos de dados são usados para assimilar dados em [!DNL Experience Platform], e esses dados são usados para identificar indivíduos e unir informações provenientes de várias fontes. Essas informações agrupadas são chamadas de [!DNL Real-Time Customer Profile]. Para que [!DNL Platform] saiba quais informações devem ser incluídas em [!DNL Real-Time Profile], os conjuntos de dados podem ser marcados para inclusão usando a alternância **[!UICONTROL Perfil]**.

Por padrão, essa alternância está desativada. Se você optar por alternar em [!DNL Profile], todos os dados ingeridos no conjunto de dados serão usados para ajudar a identificar um indivíduo e unir seus [!DNL Real-Time Profile].

Para saber mais sobre [!DNL Real-time Customer Profile] e trabalhar com identidades, consulte a documentação do [Serviço de Identidade](../../identity-service/home.md).

Para habilitar o conjunto de dados para [!DNL Real-time Customer Profile], clique na alternância **[!UICONTROL Perfil]** na guia **[!UICONTROL Info]**.

![Alternar perfil](../images/tutorials/ingest-batch-data/dataset-profile-toggle.png)

Será exibida uma caixa de diálogo solicitando que você confirme que deseja ativar o conjunto de dados para [!DNL Real-time Customer Profile].

![Habilitar caixa de diálogo Perfil](../images/tutorials/ingest-batch-data/enable-dataset-for-profile.png)

Clique em **[!UICONTROL Ativar]** e a alternância ficará azul, indicando que está ativada.

![Ativado para Perfil](../images/tutorials/ingest-batch-data/profile-enabled-dataset.png)

## Adicionar dados ao conjunto de dados

Os dados podem ser adicionados a um conjunto de dados de várias maneiras diferentes. Você poderia optar por usar [!DNL Data Ingestion] APIs ou um parceiro ETL, como [!DNL Unifi] ou [!DNL Informatica]. Para este tutorial, os dados serão adicionados ao conjunto de dados usando a guia **[!UICONTROL Adicionar dados]** na interface do usuário.

Para começar a adicionar dados ao conjunto de dados, clique na guia **[!UICONTROL Adicionar dados]**. Agora você pode arrastar e soltar arquivos ou procurar no computador os arquivos que deseja adicionar.

>[!NOTE]
>
>A plataforma suporta dois tipos de arquivos para a ingestão de dados, Parquet ou JSON. Você pode adicionar até cinco arquivos de cada vez, com o tamanho máximo de cada arquivo de 10 GB.

![Guia Adicionar dados](../images/tutorials/ingest-batch-data/drag-and-drop.png)

## Carregar um arquivo

Depois que você arrastar e soltar (ou navegar e selecionar) um arquivo Parquet ou JSON que deseja carregar, [!DNL Platform] começará imediatamente a processar o arquivo e uma caixa de diálogo **[!UICONTROL Carregando]** aparecerá na guia **[!UICONTROL Adicionar dados]** mostrando o progresso do upload do arquivo.

![Caixa de diálogo de upload](../images/tutorials/ingest-batch-data/uploading-file.png)

## Métricas do conjunto de dados

Após a conclusão do upload do arquivo, a guia **[!UICONTROL Atividade do conjunto de dados]** não mostra mais que &quot;Nenhum lote foi adicionado.&quot; Em vez disso, a guia **[!UICONTROL Atividade do conjunto de dados]** agora mostra as métricas do conjunto de dados. Todas as métricas mostrarão &quot;0&quot; neste estágio, pois o lote ainda não foi carregado.

Na parte inferior da guia, há uma lista que mostra a **[!UICONTROL ID do lote]** dos dados que foram ingeridos pelo processo [&quot;Adicionar dados ao conjunto de dados&quot;](#add-data-to-dataset). Também estão incluídas as informações relacionadas ao lote, incluindo a data de assimilação, o número de registros ingeridos e o status atual do lote.

![Métricas do conjunto de dados](../images/tutorials/ingest-batch-data/batch-id.png)

## Detalhes do lote

Clique em **[!UICONTROL ID do lote]** para visualização de **[!UICONTROL Visão geral do lote]**, mostrando detalhes adicionais sobre o lote. Depois que o lote terminar de carregar, as informações sobre o lote serão atualizadas para mostrar o número de registros ingeridos e o tamanho do arquivo. O status também será alterado para &quot;Êxito&quot; ou &quot;Falha&quot;. Se o lote falhar, a seção **[!UICONTROL Código de Erro]** conterá detalhes sobre quaisquer erros durante a ingestão.

Para obter mais informações e perguntas frequentes sobre a ingestão em lote, consulte o [guia de solução de problemas de ingestão em lote](../batch-ingestion/troubleshooting.md).

Para retornar à tela **[!UICONTROL Atividade de conjunto de dados]**, clique no nome do conjunto de dados (**[!UICONTROL Detalhes de fidelidade]**) na navegação estrutural.

![Visão geral do lote](../images/tutorials/ingest-batch-data/batch-details.png)

## Conjunto de dados de pré-visualização

Quando o conjunto de dados estiver pronto, uma opção para **[!UICONTROL Conjunto de dados de Pré-visualização]** será exibida na parte superior da guia **[!UICONTROL Atividade do conjunto de dados]**.

Clique em **[!UICONTROL Conjunto de Dados de Pré-visualização]** para abrir uma caixa de diálogo mostrando dados de amostra do conjunto de dados. Se o conjunto de dados tiver sido criado usando um schema, os detalhes do schema do conjunto de dados aparecerão no lado esquerdo da pré-visualização. Você pode expandir o schema usando as setas para ver a estrutura do schema. Cada cabeçalho de coluna nos dados de pré-visualização representa um campo no conjunto de dados.

![Detalhes do conjunto de dados](../images/tutorials/ingest-batch-data/dataset-preview.png)

## Próximos passos e recursos adicionais

Agora que você criou um conjunto de dados e assimilou dados com êxito em [!DNL Experience Platform], pode repetir essas etapas para criar um novo conjunto de dados ou assimilar mais dados no conjunto de dados existente.

Para saber mais sobre a ingestão em lote, leia a [visão geral da ingestão em lote](../batch-ingestion/overview.md) e complete sua aprendizagem assistindo ao vídeo abaixo.

>[!WARNING]
>
>A interface do usuário [!DNL Platform] mostrada no vídeo a seguir está desatualizada. Consulte a documentação acima para obter as capturas de tela e a funcionalidade mais recentes da interface do usuário.

>[!VIDEO](https://video.tv.adobe.com/v/27269?quality=12&learn=on)