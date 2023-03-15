---
keywords: Experience Platform;início;tópicos populares;habilitar conjunto de dados;conjunto de dados;conjunto de dados;;home;popular topics;enable dataset;Dataset;dataset
solution: Experience Platform
title: Guia da interface de conjuntos de dados
description: Saiba como executar ações comuns ao trabalhar com conjuntos de dados na interface do usuário do Adobe Experience Platform.
exl-id: f0d59d4f-4ebd-42cb-bbc3-84f38c1bf973
source-git-commit: 74867f56ee13430cbfd9083a916b7167a9a24c01
workflow-type: tm+mt
source-wordcount: '1476'
ht-degree: 0%

---

# Guia da interface do usuário de conjuntos de dados

Este guia do usuário fornece instruções sobre como executar ações comuns ao trabalhar com conjuntos de dados na interface do usuário do Adobe Experience Platform.

## Introdução

Este guia do usuário requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Conjuntos de dados](overview.md): a construção de armazenamento e gerenciamento para a persistência de dados no [!DNL Experience Platform].
* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): o quadro normalizado pelo qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas da composição do esquema](../../xdm/schema/composition.md): saiba mais sobre os componentes básicos dos esquemas XDM, incluindo princípios fundamentais e práticas recomendadas na composição do esquema.
   * [Editor de esquema](../../xdm/tutorials/create-schema-ui.md): saiba como criar seus próprios esquemas XDM personalizados usando o [!DNL Schema Editor] no prazo de [!DNL Platform] interface do usuário.
* [[!DNL Real-Time Customer Profile]](../../profile/home.md): fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.
* [[!DNL Adobe Experience Platform Data Governance]](../../data-governance/home.md): garanta a conformidade com as regulamentações, as restrições e as políticas relacionadas ao uso dos dados do cliente.

## Exibir conjuntos de dados {#view-datasets}

>[!CONTEXTUALHELP]
>id="platform_datasets_negative_numbers"
>title="Números negativos na atividade do conjunto de dados"
>abstract="Números negativos em registros assimilados significa que um usuário excluiu determinados lotes em um intervalo de tempo selecionado."
>text="Learn more in documentation"

No [!DNL Experience Platform] Interface, selecione **[!UICONTROL Conjuntos de dados]** no painel de navegação esquerdo para abrir a **[!UICONTROL Conjuntos de dados]** painel. O painel lista todos os conjuntos de dados disponíveis para sua organização. Os detalhes são exibidos para cada conjunto de dados listado, incluindo o nome, o esquema ao qual o conjunto de dados pertence e o status da execução de assimilação mais recente.

![Uma imagem que destaca o item Conjuntos de dados na barra de navegação à esquerda.](../images/datasets/user-guide/browse-datasets.png)

Por padrão, somente os conjuntos de dados assimilados na são mostrados. Se quiser ver os conjuntos de dados gerados pelo sistema, ative a opção **[!UICONTROL Mostrar conjuntos de dados do sistema]** alternar. Os conjuntos de dados gerados pelo sistema são usados apenas para processar outros componentes. Por exemplo, o conjunto de dados de exportação de perfil gerado pelo sistema é usado para processar o painel de perfis.

![A opção que permite escolher se os conjuntos de dados do sistema devem ou não ser exibidos é realçada.](../images/datasets/user-guide/system-datasets.png)

Selecione o nome de um conjunto de dados para acessar seu **[!UICONTROL Atividade do conjunto de dados]** e veja detalhes do conjunto de dados selecionado. A guia Atividade inclui um gráfico que visualiza a taxa de mensagens que estão sendo consumidas, bem como uma lista de lotes bem-sucedidos e com falha.

![Os detalhes do conjunto de dados selecionado são destacados.](../images/datasets/user-guide/dataset-activity-1.png)
![Os lotes de amostra que pertencem ao conjunto de dados selecionado são destacados.](../images/datasets/user-guide/dataset-activity-2.png)

## Visualizar um conjunto de dados

No **[!UICONTROL Atividade do conjunto de dados]** , selecione **[!UICONTROL Visualizar conjunto de dados]** próximo ao canto superior direito da tela para visualizar até 100 linhas de dados. Se o conjunto de dados estiver vazio, o link de visualização será desativado e indicará que a visualização não está disponível.

![O botão Visualizar conjunto de dados é realçado.](../images/datasets/user-guide/select-preview.png)

Na janela de pré-visualização, a visualização hierárquica do esquema do conjunto de dados é mostrada à direita.

![Uma visualização do conjunto de dados é exibida. As informações sobre a estrutura, bem como valores de amostra, são mostradas.](../images/datasets/user-guide/preview-dataset.png)

Para obter métodos mais robustos para acessar seus dados, [!DNL Experience Platform] O fornece serviços downstream, como [!DNL Query Service] e [!DNL JupyterLab] para explorar e analisar dados. Consulte os seguintes documentos para obter mais informações:

* [Visão geral do Serviço de consulta](../../query-service/home.md)
* [Guia do usuário do JupyterLab](../../data-science-workspace/jupyterlab/overview.md)

## Criar um conjunto de dados {#create}

Para criar um novo conjunto de dados, comece selecionando **[!UICONTROL Criar conjunto de dados]** no **[!UICONTROL Conjuntos de dados]** painel.

![O botão Criar conjunto de dados é realçado.](../images/datasets/user-guide/select-create.png)

Na próxima tela, você verá as duas opções a seguir para criar um novo conjunto de dados:

* [Criar conjunto de dados a partir do esquema](#schema)
* [Criar conjunto de dados a partir de arquivo CSV](#csv)

### Criar um conjunto de dados com um esquema existente {#schema}

No **[!UICONTROL Criar conjunto de dados]** , selecione **[!UICONTROL Criar conjunto de dados a partir do esquema]** para criar um novo conjunto de dados vazio.

![O botão Criar conjunto de dados a partir do esquema é realçado.](../images/datasets/user-guide/create-dataset-schema.png)

A variável **[!UICONTROL Selecionar esquema]** é exibida. Navegue pela listagem de esquemas e selecione o esquema ao qual o conjunto de dados seguirá antes de selecionar **[!UICONTROL Próxima]**.

![Uma lista de schemas é exibida. O esquema que será usado para criar o conjunto de dados é realçado.](../images/datasets/user-guide/select-schema.png)

A variável **[!UICONTROL Configurar conjunto de dados]** é exibida. Forneça um nome e uma descrição opcional ao conjunto de dados e selecione **[!UICONTROL Concluir]** para criar o conjunto de dados.

![Os detalhes de configuração do conjunto de dados são inseridos. Isso inclui detalhes como o nome e a descrição do conjunto de dados.](../images/datasets/user-guide/configure-dataset-schema.png)

### Criar um conjunto de dados com um arquivo CSV {#csv}

Quando um conjunto de dados é criado usando um arquivo CSV, um esquema ad hoc é criado para fornecer ao conjunto de dados uma estrutura que corresponde ao arquivo CSV fornecido. No **[!UICONTROL Criar conjunto de dados]** , selecione **[!UICONTROL Criar conjunto de dados a partir de arquivo CSV]**.

![O botão Criar conjunto de dados a partir de arquivo CSV é realçado.](../images/datasets/user-guide/create-dataset-csv.png)

A variável **[!UICONTROL Configurar]** é exibida. Forneça um nome e uma descrição opcional ao conjunto de dados e selecione **[!UICONTROL Próxima]**.

![Os detalhes de configuração do conjunto de dados são inseridos. Isso inclui detalhes como o nome e a descrição do conjunto de dados.](../images/datasets/user-guide/configure-dataset-csv.png)

A variável **[!UICONTROL Adicionar dados]** é exibida. Carregue o arquivo CSV arrastando-o e soltando-o no centro da tela ou selecione **[!UICONTROL Procurar]** para explorar o diretório de arquivos. O arquivo pode ter até dez gigabytes. Depois que o arquivo CSV for carregado, selecione **[!UICONTROL Salvar]** para criar o conjunto de dados.

>[!NOTE]
>
>Os nomes das colunas CSV devem começar com caracteres alfanuméricos e podem conter apenas letras, números e sublinhados.

![A tela Adicionar dados é exibida. O local onde você pode fazer upload do arquivo CSV para o conjunto de dados é destacado.](../images/datasets/user-guide/add-csv-data.png)

## Ativar um conjunto de dados para o Perfil do cliente em tempo real {#enable-profile}

Cada conjunto de dados tem a capacidade de enriquecer os perfis do cliente com seus dados assimilados. Para fazer isso, o esquema que o conjunto de dados segue deve ser compatível para uso no [!DNL Real-Time Customer Profile]. Um esquema compatível satisfaz os seguintes requisitos:

* O esquema tem pelo menos um atributo especificado como uma propriedade de identidade.
* O esquema tem uma propriedade de identidade definida como a identidade principal.

Para obter mais informações sobre como ativar um esquema para [!DNL Profile], consulte o [Guia do usuário do Editor de esquema](../../xdm/tutorials/create-schema-ui.md).

Para habilitar um conjunto de dados para o Perfil, acesse seu **[!UICONTROL Atividade do conjunto de dados]** e selecione o **[!UICONTROL Perfil]** alternar dentro do **[!UICONTROL Propriedades]** coluna. Depois de ativados, os dados assimilados no conjunto de dados também serão usados para preencher perfis de clientes.

>[!NOTE]
>
>Se um conjunto de dados já contiver dados e estiver ativado para [!DNL Profile], os dados existentes não são consumidos automaticamente pelo [!DNL Profile]. Depois que um conjunto de dados é ativado para [!DNL Profile], é recomendável assimilar novamente todos os dados existentes para que eles contribuam com os perfis do cliente.

![A opção de Perfil é realçada na página de detalhes do conjunto de dados.](../images/datasets/user-guide/enable-dataset-profiles.png)

## Gerenciar e aplicar a governança de dados em um conjunto de dados

Os rótulos de uso de dados permitem categorizar conjuntos de dados e campos de acordo com as políticas de uso que se aplicam a esses dados. Consulte a [Visão geral da governança de dados](../../data-governance/home.md) para saber mais sobre rótulos ou consulte o [guia do usuário de rótulos de uso de dados](../../data-governance/labels/overview.md) para obter instruções sobre como aplicar rótulos a conjuntos de dados.

## Excluir um conjunto de dados {#delete}

É possível excluir um conjunto de dados acessando primeiro seu **[!UICONTROL Atividade do conjunto de dados]** tela. Em seguida, selecione **[!UICONTROL Excluir conjunto de dados]** para excluí-lo.

>[!NOTE]
>
>Conjuntos de dados criados e utilizados por aplicativos e serviços Adobe (como Adobe Analytics, Adobe Audience Manager ou [!DNL Offer Decisioning]) não pode ser excluída.

![O botão Excluir conjunto de dados é realçado na página de detalhes do conjunto de dados.](../images/datasets/user-guide/delete-dataset.png)

Uma caixa de confirmação é exibida. Selecionar **[!UICONTROL Excluir]** para confirmar a exclusão do conjunto de dados.

![A modal de confirmação para exclusão é exibida, com o botão Excluir realçado.](../images/datasets/user-guide/confirm-delete.png)

## Excluir um conjunto de dados habilitado para perfil

Se um conjunto de dados estiver ativado para o Perfil, a exclusão desse conjunto de dados por meio da interface do usuário o excluirá do data lake, do Serviço de identidade e do Armazenamento de perfis na Plataforma.

É possível excluir um conjunto de dados da variável [!DNL Profile] armazenar somente (deixando os dados no Data Lake) usando a API do Perfil do cliente em tempo real. Para obter mais informações, consulte [guia de ponto de extremidade da API de trabalhos do sistema de perfil](../../profile/api/profile-system-jobs.md).

## Monitorar assimilação de dados

No [!DNL Experience Platform] Interface, selecione **[!UICONTROL Monitoramento]** no painel de navegação esquerdo. A variável **[!UICONTROL Monitoramento]** O painel permite visualizar os status dos dados de entrada da assimilação em lote ou por transmissão. Para exibir os status de lotes individuais, selecione **[!UICONTROL Lote de ponta a ponta]** ou **[!UICONTROL Transmissão de ponta a ponta]**. Os painéis listam todas as execuções de assimilação em lote ou por transmissão, incluindo as que foram bem-sucedidas, falharam ou ainda estão em andamento. Cada lista fornece detalhes do lote, incluindo a ID do lote, o nome do conjunto de dados de destino e o número de registros assimilados. Se o conjunto de dados de destino estiver habilitado para [!DNL Profile], o número de registros de identidade e perfil assimilados também é exibido.

![A tela de monitoramento completa do lote é exibida. O monitoramento e a análise de lote a lote são destacados.](../images/datasets/user-guide/batch-listing.png)

Você pode selecionar um indivíduo **[!UICONTROL ID do lote]** para acessar o **[!UICONTROL Visão geral de lotes]** e consulte os detalhes do lote, incluindo logs de erros, caso o lote não seja assimilado.

![Os detalhes do lote selecionado são exibidos. Isso inclui o número de registros assimilados, o número de registros com falha, o status do lote, o tamanho do arquivo, as horas de início e término da assimilação, o conjunto de dados e as IDs do lote, a ID da organização, o nome do conjunto de dados e as informações de acesso.](../images/datasets/user-guide/batch-overview.png)

Se desejar excluir o lote, selecione **[!UICONTROL Excluir lote]** localizado próximo à parte superior direita do painel. Isso também removerá seus registros do conjunto de dados ao qual o lote foi originalmente assimilado.

![O botão Excluir lote é realçado na página de detalhes do conjunto de dados.](../images/datasets/user-guide/delete-batch.png)

## Próximas etapas

Este guia do usuário forneceu instruções para executar ações comuns ao trabalhar com conjuntos de dados na [!DNL Experience Platform] interface do usuário. Para obter as etapas sobre como executar tarefas [!DNL Platform] fluxos de trabalho envolvendo conjuntos de dados, consulte os seguintes tutoriais:

* [Criar um conjunto de dados usando APIs](create.md)
* [Consultar dados do conjunto de dados usando a API de acesso a dados](../../data-access/home.md)
* [Configurar um conjunto de dados para o Perfil do cliente em tempo real e o Serviço de identidade usando APIs](../../profile/tutorials/dataset-configuration.md)
