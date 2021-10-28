---
keywords: Experience Platform; home; tópicos populares; ingestão; dados de lote de assimilação; tutorial; ingestão em lote; tutorial; guia da interface do usuário;
solution: Experience Platform
title: Assimilar Dados No Experience Platform
topic-legacy: tutorial
type: Tutorial
description: O Adobe Experience Platform permite importar facilmente dados como arquivos em lote na forma de arquivos Parquet ou dados que estejam em conformidade com um esquema conhecido do Experience Data Model (XDM).
exl-id: a4a7358d-b117-4d81-8cb0-3dbbfeccdcbd
source-git-commit: e7fc8a168a48cc6fadda62efda9ee9eb3025ab51
workflow-type: tm+mt
source-wordcount: '1322'
ht-degree: 0%

---

# Assimilar dados na Adobe Experience Platform

O Adobe Experience Platform permite importar dados facilmente para o [!DNL Platform] como arquivos em lote. Os exemplos de dados a serem assimilados podem incluir dados de perfil de um arquivo simples em um sistema CRM (como um arquivo Parquet) ou dados que estejam em conformidade com um arquivo conhecido [!DNL Experience Data Model] (XDM) no Registro de Esquema.

## Introdução

Para concluir este tutorial, você deve ter acesso ao [!DNL Experience Platform]. Se você não tiver acesso a uma Organização IMS no [!DNL Experience Platform], fale com o administrador do sistema antes de continuar.

Se preferir assimilar dados usando APIs de assimilação de dados, comece lendo a variável [Guia do desenvolvedor de assimilação em lote](../batch-ingestion/api-overview.md).

## Espaço de trabalho Conjuntos de dados

O espaço de trabalho Conjuntos de dados em [!DNL Experience Platform] O permite visualizar e gerenciar todos os conjuntos de dados que sua organização IMS fez, bem como criar novos conjuntos.

Exibir o espaço de trabalho Conjuntos de dados clicando em **[!UICONTROL Conjuntos de dados]** na navegação à esquerda. A área de trabalho Conjuntos de dados contém uma lista de conjuntos de dados, incluindo colunas que mostram o nome, a data e a hora criadas, a origem, o esquema e o status do último lote, bem como a data e a hora em que o conjunto de dados foi atualizado pela última vez.

>[!NOTE]
>
>Clique no ícone de filtro ao lado da barra de pesquisa para usar os recursos de filtragem para exibir somente os conjuntos de dados habilitados para [!DNL Profile].

![Exibir todos os conjuntos de dados](../images/tutorials/ingest-batch-data/datasets-overview.png)

## Criar um conjunto de dados

Para criar um conjunto de dados, clique em **[!UICONTROL Criar conjunto de dados]** no canto superior direito do espaço de trabalho Conjuntos de dados.

![](../images/tutorials/ingest-batch-data/click-create-datasets.png)

No **[!UICONTROL Criar conjunto de dados]** selecione se deseja &quot;[!UICONTROL Criar conjunto de dados a partir do esquema]&quot; ou &quot;[!UICONTROL Criar conjunto de dados a partir do arquivo CSV]&quot;.

Para este tutorial, um esquema será usado para criar o conjunto de dados. Clique em **[!UICONTROL Criar conjunto de dados a partir do esquema]** para continuar.

![Selecionar fonte de dados](../images/tutorials/ingest-batch-data/create-dataset.png)

## Selecionar esquema do conjunto de dados

No **[!UICONTROL Selecionar esquema]** escolha um schema clicando no botão de opção ao lado do schema que deseja usar. Para este tutorial, o conjunto de dados será feito usando o schema Membros de fidelidade . Usar a barra de pesquisa para filtrar esquemas é uma maneira útil de encontrar o esquema exato que você está procurando.

Depois de selecionar o botão de opção ao lado do schema que deseja usar, clique em **[!UICONTROL Próximo]**.

![Selecionar esquema](../images/tutorials/ingest-batch-data/select-schema.png)

## Configurar conjunto de dados

No **[!UICONTROL Configurar conjunto de dados]** , será necessário fornecer um nome ao seu conjunto de dados e também pode fornecer uma descrição do conjunto de dados.

**Notas sobre os nomes dos conjuntos de dados:**

- Os nomes dos conjuntos de dados devem ser curtos e descritivos para que o conjunto de dados possa ser facilmente encontrado na biblioteca posteriormente.
- Os nomes do conjunto de dados devem ser exclusivos, o que significa que também devem ser específicos o suficiente para que não sejam reutilizados no futuro.
- É uma prática recomendada fornecer informações adicionais sobre o conjunto de dados usando o campo de descrição, pois pode ajudar outros usuários a diferenciar os conjuntos de dados no futuro.

Depois que o conjunto de dados tiver um nome e uma descrição, clique em **[!UICONTROL Concluir]**.

![Configurar conjunto de dados](../images/tutorials/ingest-batch-data/configure-dataset.png)

## Atividade do conjunto de dados

Um conjunto de dados vazio foi criado e você foi retornado para o **[!UICONTROL Atividade do conjunto de dados]** na área de trabalho Conjuntos de dados . Você deve ver o nome do conjunto de dados no canto superior esquerdo do espaço de trabalho, juntamente com uma notificação de que &quot;Nenhum lote foi adicionado&quot;. Isso é esperado, pois você ainda não adicionou nenhum lote a esse conjunto de dados.

No lado direito do espaço de trabalho Conjuntos de dados, você verá a variável **[!UICONTROL Informações]** guia que contém informações relacionadas ao novo conjunto de dados, como ID do conjunto de dados, nome, descrição, nome da tabela, esquema, transmissão e origem. A guia Informações também inclui informações sobre quando o conjunto de dados foi criado e sua última data de modificação.

Também na guia Informações há uma  **[!UICONTROL Perfil]** alternar usado para habilitar seu conjunto de dados para uso com [!DNL Real-time Customer Profile]. Usar essa alternância e [!DNL Real-time Customer Profile], serão explicadas com mais detalhes na seção a seguir.

![Atividade do conjunto de dados](../images/tutorials/ingest-batch-data/sample-dataset.png)

## Ativar conjunto de dados para [!DNL Real-time Customer Profile]

Os conjuntos de dados são usados para assimilar dados no [!DNL Experience Platform]e que os dados são usados para identificar indivíduos e unir informações provenientes de várias fontes. Essa informação unida é chamada de [!DNL Real-Time Customer Profile]. Para [!DNL Platform] para saber quais informações devem ser incluídas no [!DNL Real-Time Profile], os conjuntos de dados podem ser marcados para inclusão usando o **[!UICONTROL Perfil]** alternar.

Por padrão, essa alternância está desativada. Se você optar por ativar [!DNL Profile], todos os dados assimilados no conjunto de dados serão usados para ajudar a identificar um indivíduo e unir seus dados [!DNL Real-Time Profile].

Para saber mais sobre [!DNL Real-time Customer Profile] e trabalhando com identidades, reveja o [Serviço de identidade](../../identity-service/home.md) documentação.

Para ativar o conjunto de dados para [!DNL Real-time Customer Profile], clique no botão **[!UICONTROL Perfil]** alternar no **[!UICONTROL Informações]** guia .

![Ativar/desativar perfil](../images/tutorials/ingest-batch-data/dataset-profile-toggle.png)

Uma caixa de diálogo será exibida solicitando que você confirme que deseja ativar o conjunto de dados para o [!DNL Real-time Customer Profile].

![Caixa de diálogo Ativar perfil](../images/tutorials/ingest-batch-data/enable-dataset-for-profile.png)

Clique em **[!UICONTROL Habilitar]** e o botão ficará azul, indicando que está ligado.

![Ativado para Perfil](../images/tutorials/ingest-batch-data/profile-enabled-dataset.png)

## Adicionar dados ao conjunto de dados

Os dados podem ser adicionados a um conjunto de dados de várias maneiras diferentes. Você poderia optar por usar [!DNL Data Ingestion] APIs ou um parceiro de ETL, como [!DNL Unifi] ou [!DNL Informatica]. Para este tutorial, os dados serão adicionados ao conjunto de dados usando o **[!UICONTROL Adicionar dados]** na interface do usuário.

Para começar a adicionar dados ao conjunto de dados, clique no botão **[!UICONTROL Adicionar dados]** guia . Agora você pode arrastar e soltar arquivos ou procurar no computador os arquivos que deseja adicionar.

>[!NOTE]
>
>A plataforma oferece suporte a dois tipos de arquivos para assimilação de dados, Parquet ou JSON. Você pode adicionar até cinco arquivos de cada vez, com o tamanho máximo de arquivo de cada arquivo de 1 GB.

![Guia Adicionar dados](../images/tutorials/ingest-batch-data/drag-and-drop.png)

## Carregar um arquivo

Depois de arrastar e soltar (ou procurar e selecionar) um arquivo Parquet ou JSON que você deseja fazer upload, [!DNL Platform] começará imediatamente a processar o arquivo e um **[!UICONTROL Upload]** será exibida no **[!UICONTROL Adicionar dados]** guia mostrando o progresso do upload do arquivo.

![Caixa de diálogo de upload](../images/tutorials/ingest-batch-data/uploading-file.png)

## Métricas do conjunto de dados

Após a conclusão do upload do arquivo, a variável **[!UICONTROL Atividade do conjunto de dados]** A guia não mostra mais que &quot;Nenhum lote foi adicionado.&quot; Em vez disso, a variável **[!UICONTROL Atividade do conjunto de dados]** agora mostra métricas do conjunto de dados. Todas as métricas mostrarão &quot;0&quot; neste estágio, pois o lote ainda não foi carregado.

Na parte inferior da guia há uma lista que mostra a variável **[!UICONTROL ID em lote]** dos dados que foram assimilados por meio da variável [&quot;Adicionar dados ao conjunto de dados&quot;](#add-data-to-dataset) processo. Também inclui informações relacionadas ao lote, incluindo data assimilada, número de registros assimilados e o status atual do lote.

![Métricas do conjunto de dados](../images/tutorials/ingest-batch-data/batch-id.png)

## Detalhes do lote

Clique no botão **[!UICONTROL ID em lote]** para visualizar uma **[!UICONTROL Visão geral do lote]**, mostrando detalhes adicionais sobre o lote. Quando o lote terminar de carregar, as informações sobre o lote serão atualizadas para mostrar o número de registros assimilados e o tamanho do arquivo. O status também será alterado para &quot;Sucesso&quot; ou &quot;Falha&quot;. Se o lote falhar, o **[!UICONTROL Código de erro]** A seção conterá detalhes sobre quaisquer erros durante a assimilação.

Para obter mais informações e perguntas frequentes sobre a ingestão em lote, consulte o [Guia de solução de problemas de assimilação em lote](../batch-ingestion/troubleshooting.md).

Para retornar ao **[!UICONTROL Atividade do conjunto de dados]** , clique no nome do conjunto de dados (**[!UICONTROL Detalhes da Fidelidade]**) na navegação estrutural.

![Visão geral do lote](../images/tutorials/ingest-batch-data/batch-details.png)

## Visualizar conjunto de dados

Quando o conjunto de dados estiver pronto, será possível **[!UICONTROL Visualizar conjunto de dados]** aparece na parte superior do **[!UICONTROL Atividade do conjunto de dados]** guia .

Clique em **[!UICONTROL Visualizar conjunto de dados]** para abrir uma caixa de diálogo mostrando dados de amostra no conjunto de dados. Se o conjunto de dados foi criado usando um esquema, os detalhes do esquema do conjunto de dados serão exibidos no lado esquerdo da visualização. É possível expandir o schema usando as setas para ver a estrutura do schema. Cada cabeçalho de coluna nos dados de visualização representa um campo no conjunto de dados.

![Detalhes do conjunto de dados](../images/tutorials/ingest-batch-data/dataset-preview.png)

## Próximas etapas e recursos adicionais

Agora que você criou um conjunto de dados e assimilou dados com êxito no [!DNL Experience Platform], você pode repetir essas etapas para criar um novo conjunto de dados ou assimilar mais dados no conjunto de dados existente.

Para saber mais sobre a ingestão em lote, leia o [Visão geral da Assimilação em lote](../batch-ingestion/overview.md) e complemente seu aprendizado assistindo ao vídeo abaixo.

>[!WARNING]
>
>O [!DNL Platform] A interface do usuário exibida no vídeo a seguir está desatualizada. Consulte a documentação acima para obter as capturas de tela e a funcionalidade mais recentes da interface do usuário.

>[!VIDEO](https://video.tv.adobe.com/v/27269?quality=12&learn=on)
