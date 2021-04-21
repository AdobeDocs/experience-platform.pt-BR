---
keywords: Experience Platform, home, tópicos populares, ativar conjunto de dados, conjunto de dados, conjunto de dados
solution: Experience Platform
title: Guia da interface do usuário de conjuntos de dados
topic-legacy: datasets
description: Saiba como executar ações comuns ao trabalhar com conjuntos de dados na interface do usuário do Adobe Experience Platform.
exl-id: f0d59d4f-4ebd-42cb-bbc3-84f38c1bf973
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1083'
ht-degree: 0%

---

# Guia da interface do usuário de conjuntos de dados

Este guia do usuário fornece instruções sobre como executar ações comuns ao trabalhar com conjuntos de dados na interface do usuário do Adobe Experience Platform.

## Introdução

Este guia do usuário requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Conjuntos de dados](overview.md): A construção de armazenamento e gerenciamento para a persistência de dados no  [!DNL Experience Platform].
* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): A estrutura padronizada pela qual  [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas da composição](../../xdm/schema/composition.md) do schema: Saiba mais sobre os elementos básicos dos esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   * [Editor](../../xdm/tutorials/create-schema-ui.md) de esquema: Saiba como criar seus próprios esquemas XDM personalizados usando o  [!DNL Schema Editor] na interface do  [!DNL Platform] usuário do .
* [[!DNL Real-time Customer Profile]](../../profile/home.md): Fornece um perfil de consumidor unificado e em tempo real com base em dados agregados de várias fontes.
* [[!DNL Adobe Experience Platform Data Governance]](../../data-governance/home.md): Assegure a conformidade com regulamentos, restrições e políticas relacionadas ao uso de dados do cliente.

## Exibir conjuntos de dados

Na interface [!DNL Experience Platform], clique em **[!UICONTROL Datasets]** no painel de navegação esquerdo para abrir o painel **[!UICONTROL Datasets]**. O painel lista todos os conjuntos de dados disponíveis para sua organização. Os detalhes são exibidos para cada conjunto de dados listado, incluindo seu nome, o esquema ao qual o conjunto de dados adere e o status da execução de assimilação mais recente.

![](../images/datasets/user-guide/browse_datasets.png)

Clique no nome de um conjunto de dados para acessar a tela **[!UICONTROL Dataset activity]** e ver os detalhes do conjunto de dados selecionado. A guia activity inclui um gráfico que visualiza a taxa de mensagens que estão sendo consumidas, bem como uma lista de lotes bem-sucedidos e com falha.

![](../images/datasets/user-guide/dataset_activity_1.png)
![](../images/datasets/user-guide/dataset_activity_2.png)

## Visualizar um conjunto de dados

Na tela **[!UICONTROL Dataset activity]**, clique em **[!UICONTROL Preview dataset]** próximo ao canto superior direito da tela para visualizar até 100 linhas de dados. Se o conjunto de dados estiver vazio, o link de visualização será desativado e, em vez disso, dirá que a visualização não está disponível.

![](../images/datasets/user-guide/click_to_preview.png)

Na janela de pré-visualização, a exibição hierárquica do esquema do conjunto de dados é mostrada à direita.

![](../images/datasets/user-guide/preview_dataset.png)

Para métodos mais robustos de acesso aos seus dados, [!DNL Experience Platform] fornece serviços downstream como [!DNL Query Service] e [!DNL JupyterLab] para explorar e analisar dados. Consulte os seguintes documentos para obter mais informações:

* [Visão geral do Serviço de query](../../query-service/home.md)
* [Guia do usuário do JupyterLab](../../data-science-workspace/jupyterlab/overview.md)

## Criar um conjunto de dados {#create}

Para criar um novo conjunto de dados, comece clicando em **[!UICONTROL Create dataset]** no painel **[!UICONTROL Datasets]**.

![](../images/datasets/user-guide/click_to_create.png)

Na próxima tela, você verá as duas opções a seguir para criar um novo conjunto de dados:

* [Criar conjunto de dados a partir do esquema](#schema)
* [Criar conjunto de dados a partir do arquivo CSV](#csv)

### Criar um conjunto de dados com um esquema existente {#schema}

Na tela **[!UICONTROL Create dataset]**, clique em **[!UICONTROL Create dataset from schema]** para criar um novo conjunto de dados vazio.

![](../images/datasets/user-guide/create_dataset_schema.png)

A etapa **[!UICONTROL Select schema]** é exibida. Navegue pela lista de esquema e selecione o esquema que o conjunto de dados seguirá antes de clicar em **[!UICONTROL Next]**.

![](../images/datasets/user-guide/select_schema.png)

A etapa **[!UICONTROL Configure dataset]** é exibida. Forneça um nome e uma descrição opcional ao conjunto de dados, em seguida, clique em **[!UICONTROL Finish]** para criar o conjunto de dados.

![](../images/datasets/user-guide/configure_dataset_schema.png)

### Criar um conjunto de dados com um arquivo CSV {#csv}

Quando um conjunto de dados é criado usando um arquivo CSV, um esquema ad hoc é criado para fornecer ao conjunto de dados uma estrutura que corresponda ao arquivo CSV fornecido. Na tela **[!UICONTROL Create dataset]**, clique na caixa que diz **[!UICONTROL Create dataset from CSV file]**.

![](../images/datasets/user-guide/create_dataset_csv.png)

A etapa **[!UICONTROL Configure]** é exibida. Forneça um nome e uma descrição opcional ao conjunto de dados, em seguida, clique em **[!UICONTROL Next]**.

![](../images/datasets/user-guide/configure_dataset_csv.png)

A etapa **[!UICONTROL Add data]** é exibida. Faça upload do arquivo CSV arrastando-o e soltando-o no centro da tela ou clique em **[!UICONTROL Browse]** para explorar seu diretório de arquivos. O arquivo pode ter até dez gigabytes de tamanho. Depois que o arquivo CSV for carregado, clique em **[!UICONTROL Save]** para criar o conjunto de dados.

>[!NOTE]
>
>Os nomes das colunas CSV devem começar com caracteres alfanuméricos e podem conter somente letras, números e sublinhados.

![](../images/datasets/user-guide/add_csv_data.png)

## Ativar um conjunto de dados para o Perfil do cliente em tempo real {#enable-profile}

Cada conjunto de dados tem a capacidade de enriquecer perfis de clientes com seus dados assimilados. Para fazer isso, o esquema que o conjunto de dados adere deve ser compatível para uso em [!DNL Real-time Customer Profile]. Um schema compatível satisfaz os seguintes requisitos:

* O esquema tem pelo menos um atributo especificado como uma propriedade de identidade.
* O esquema tem uma propriedade de identidade definida como a identidade primária.

Para obter mais informações sobre como ativar um schema para [!DNL Profile], consulte o [Guia do usuário do Editor de Esquema](../../xdm/tutorials/create-schema-ui.md).

Para ativar um conjunto de dados para o Perfil, acesse a tela **[!UICONTROL Dataset activity]** e clique no botão **[!UICONTROL Profile]** na coluna **[!UICONTROL Properties]**. Depois de habilitado, os dados assimilados no conjunto de dados também serão usados para preencher perfis do cliente.

>[!NOTE]
>
>Se um conjunto de dados já contiver dados e estiver ativado para [!DNL Profile], os dados existentes não serão consumidos automaticamente por [!DNL Profile]. Depois que um conjunto de dados for ativado para [!DNL Profile], é recomendável assimilar novamente todos os dados existentes para contribuir com os perfis do cliente.

![](../images/datasets/user-guide/enable_dataset_profiles.png)

## Gerenciar e aplicar o controle de dados em um conjunto de dados

Os rótulos de uso de dados permitem categorizar os conjuntos de dados e campos de acordo com as políticas de uso que se aplicam a esses dados. Consulte a [Visão geral da Governança de dados](../../data-governance/home.md) para saber mais sobre rótulos, ou consulte o [guia do usuário de rótulos de uso de dados](../../data-governance/labels/overview.md) para obter instruções sobre como aplicar rótulos a conjuntos de dados.

## Excluir um conjunto de dados

Você pode excluir um conjunto de dados acessando primeiro sua tela **[!UICONTROL Dataset activity]**. Em seguida, clique em **[!UICONTROL Delete dataset]** para excluí-lo.

>[!NOTE]
>
>Os conjuntos de dados criados e utilizados por aplicativos e serviços do Adobe (como Adobe Analytics, Adobe Audience Manager ou [!DNL Offer Decisioning]) não podem ser excluídos.

![](../images/datasets/user-guide/delete_dataset.png)

Uma caixa de confirmação é exibida. Clique em **[!UICONTROL Delete]** para confirmar a exclusão do conjunto de dados.

![](../images/datasets/user-guide/confirm_delete.png)

## Excluir um conjunto de dados habilitado para perfil

Se um conjunto de dados estiver ativado para [!DNL Profile], a exclusão desse conjunto de dados pela interface do usuário o excluirá do Data Lake e do armazenamento de Perfil na Platform.

Você pode excluir um conjunto de dados somente do armazenamento [!DNL Profile] (deixando os dados no Data Lake) usando a API de Perfil do cliente em tempo real. Para obter mais informações, consulte o [guia do ponto de extremidade da API de tarefas do sistema de perfil](../../profile/api/profile-system-jobs.md).

## Monitorar assimilação de dados

Na interface do usuário [!DNL Experience Platform], clique em **[!UICONTROL Monitoring]** na navegação à esquerda. O painel **[!UICONTROL Monitoring]** permite visualizar os status dos dados de entrada da assimilação em lote ou streaming. Para exibir os status de lotes individuais, clique em **[!UICONTROL Batch end-to-end]** ou **[!UICONTROL Streaming end-to-end]**. Os painéis listam todas as execuções de assimilação em lote ou streaming, incluindo aquelas que foram bem-sucedidas, falharam ou ainda estão em andamento. Cada listagem fornece detalhes do lote, incluindo a ID do lote, o nome do conjunto de dados de destino e o número de registros assimilados. Se o conjunto de dados de destino estiver ativado para [!DNL Profile], o número de registros de identidade e perfil assimilados também será exibido.

![](../images/datasets/user-guide/batch_listing.png)

Você pode clicar em um **[!UICONTROL Batch ID]** individual para acessar o painel **[!UICONTROL Batch overview]** e ver detalhes do lote, incluindo registros de erros caso o lote não seja assimilado.

![](../images/datasets/user-guide/batch_overview.png)

Se quiser excluir o lote, faça isso clicando em **[!UICONTROL Delete batch]** localizado próximo à parte superior direita do painel. Isso também removerá seus registros do conjunto de dados ao qual o lote foi originalmente assimilado.

![](../images/datasets/user-guide/delete_batch.png)

## Próximas etapas

Este guia do usuário forneceu instruções para executar ações comuns ao trabalhar com conjuntos de dados na interface do usuário [!DNL Experience Platform]. Para obter etapas sobre como executar workflows comuns [!DNL Platform] envolvendo conjuntos de dados, consulte os seguintes tutoriais:

* [Criar um conjunto de dados usando APIs](create.md)
* [Consultar dados do conjunto de dados usando a API de acesso a dados](../../data-access/home.md)
* [Configurar um conjunto de dados para o Perfil do cliente em tempo real e o Serviço de identidade usando APIs](../../profile/tutorials/dataset-configuration.md)
