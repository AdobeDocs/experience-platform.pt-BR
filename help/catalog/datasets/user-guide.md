---
keywords: Experience Platform;home;tópicos populares;habilitar conjunto de dados;conjunto de dados;conjunto de dados;;home;popular topics;enable dataset;Dataset;dataset
solution: Experience Platform
title: Guia da interface de conjuntos de dados
description: Saiba como executar ações comuns ao trabalhar com conjuntos de dados na interface do usuário do Adobe Experience Platform.
exl-id: f0d59d4f-4ebd-42cb-bbc3-84f38c1bf973
source-git-commit: 17825151f58548ab82d0ac44beacab06386f0a2d
workflow-type: tm+mt
source-wordcount: '4295'
ht-degree: 4%

---

# Guia da interface do usuário de conjuntos de dados

Este guia do usuário fornece instruções sobre como executar ações comuns ao trabalhar com conjuntos de dados na interface do usuário do Adobe Experience Platform.

## Introdução

Este guia do usuário requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Conjuntos de dados](overview.md): a construção de armazenamento e gerenciamento para a persistência de dados em [!DNL Experience Platform].
* [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): a estrutura padronizada pela qual o [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas sobre a composição de esquema](../../xdm/schema/composition.md): saiba mais sobre os blocos de construção básicos de esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição de esquema.
   * [Editor de esquemas](../../xdm/tutorials/create-schema-ui.md): saiba como criar seus próprios esquemas XDM personalizados usando o [!DNL Schema Editor] na interface do usuário do [!DNL Experience Platform].
* [[!DNL Real-Time Customer Profile]](../../profile/home.md): Fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.
* [[!DNL Adobe Experience Platform Data Governance]](../../data-governance/home.md): garanta a conformidade com regulamentos, restrições e políticas relativos ao uso de dados do cliente.

## Visualizar conjuntos de dados {#view-datasets}

>[!CONTEXTUALHELP]
>id="platform_datasets_negative_numbers"
>title="Números negativos na atividade do conjunto de dados"
>abstract="Números negativos em registros assimilados significam que um usuário excluiu determinados lotes em um intervalo de tempo selecionado."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_datasets_browse_daysRemaining"
>title="Expiração do conjunto de dados"
>abstract="Esta coluna indica o número de dias que o conjunto de dados de destino tem antes de expirar automaticamente."

>[!CONTEXTUALHELP]
>id="platform_datasets_browse_datalakeretention"
>title="Retenção de datalake"
>abstract="Exibe a política de retenção atual para cada conjunto de dados. Esse valor pode ser modificado nas configurações de retenção de cada conjunto de dados. Você só pode definir o tempo de retenção para o conjunto de dados ExperienceEvent."

>[!CONTEXTUALHELP]
>id="platform_datasets_browse_profileretention"
>title="Retenção de perfil"
>abstract="Exibe a política de retenção atual para cada conjunto de dados. Esse valor pode ser modificado nas configurações de retenção de cada conjunto de dados. Você só pode definir o tempo de retenção para um conjunto de dados ExperienceEvent."

>[!CONTEXTUALHELP]
>id="platform_datasets_datalakesettings_datasetretention"
>title="Retenção de conjunto de dados"
>abstract="A retenção do datalake define regras para o tempo em que os dados são armazenados e quando devem ser excluídos em diferentes serviços. Isso garante a conformidade com regulamentos, gerenciando os custos de armazenamento e mantendo a qualidade dos dados."

>[!CONTEXTUALHELP]
>id="platform_datasets_orchestratedCampaigns_toggle"
>title="Campanhas orquestradas"
>abstract="Ative essa opção para permitir que o conjunto de dados selecionado seja usado em campanhas do Adobe Journey Optimizer Orchestrated. O conjunto de dados deve usar um esquema relacional e somente um conjunto de dados pode ser criado por esquema."
>additional-url="https://experienceleague.adobe.com/en/docs/journey-optimizer/using/campaigns/orchestrated-campaigns/data-configuration/schemas-datasets/manual-schema#enable" text="Habilitar conjunto de dados para campanhas orquestradas"

>[!CONTEXTUALHELP]
>id="platform_datasets_enableforlookup_toggle"
>title="Habilitar para pesquisa"
>abstract="Habilite esse conjunto de dados para que a pesquisa use seus dados no Journey Optimizer para personalização, decisão e orquestração de jornadas."
>additional-url="https://experienceleague.adobe.com/en/docs/journey-optimizer/using/data-management/lookup-aep-data" text="Usar dados do Adobe Experience Platform no Journey Optimizer"

Na interface do usuário do [!DNL Experience Platform], selecione **[!UICONTROL Datasets]** no painel de navegação esquerdo para abrir o painel **[!UICONTROL Datasets]**. O painel lista todos os conjuntos de dados disponíveis para sua organização. Os detalhes são exibidos para cada conjunto de dados listado, incluindo o nome, o esquema ao qual o conjunto de dados pertence e o status da execução de assimilação mais recente.

![A interface do usuário do Experience Platform com o item Conjuntos de Dados realçado na barra de navegação à esquerda.](../images/datasets/user-guide/browse-datasets.png)

Selecione o nome de um conjunto de dados na guia [!UICONTROL Browse] para acessar sua tela **[!UICONTROL Dataset activity]** e ver detalhes do conjunto de dados selecionado. A guia Atividade inclui um gráfico que visualiza a taxa de mensagens que estão sendo consumidas, bem como uma lista de lotes bem-sucedidos e com falha.

![As métricas e visualizações do conjunto de dados selecionado estão destacadas.](../images/datasets/user-guide/dataset-activity-1.png)
![Os lotes de amostra relacionados ao conjunto de dados selecionado estão destacados.](../images/datasets/user-guide/dataset-activity-2.png)

## Mais ações {#more-actions}

Você pode [!UICONTROL Delete] ou [!UICONTROL Enable a dataset for Profile] da exibição de detalhes de [!UICONTROL Dataset]. Para ver as ações disponíveis, selecione **[!UICONTROL ... More]** na parte superior direita da interface. O menu suspenso é exibido.

![O espaço de trabalho de Conjuntos de Dados com o menu suspenso [!UICONTROL ... More] realçado.](../images/datasets/user-guide/more-actions.png)

Se você selecionar **[!UICONTROL Enable a dataset for Profile]**, uma caixa de diálogo de confirmação será exibida. Selecione **[!UICONTROL Enable]** para confirmar sua escolha.

>[!NOTE]
>
>Para habilitar um conjunto de dados para o Perfil, o esquema que o conjunto de dados segue deve ser compatível para uso no Perfil do cliente em tempo real. Consulte a seção [Habilitar conjunto de dados para perfil](#enable-profile) para obter mais informações.

![A caixa de diálogo de confirmação Habilitar conjunto de dados.](../images/datasets/user-guide/profile-enable-confirmation-dialog.png)

Se você selecionar **[!UICONTROL Delete]**, a caixa de diálogo de confirmação [!UICONTROL Delete dataset] será exibida. Selecione **[!UICONTROL Delete]** para confirmar sua escolha.

>[!NOTE]
>
>Não é possível excluir conjuntos de dados do sistema.

Você também pode excluir ou adicionar um conjunto de dados para uso com o Perfil de Cliente em Tempo Real a partir das ações embutidas encontradas na guia [!UICONTROL Browse]. Consulte a [seção de ações embutidas](#inline-actions) para obter mais informações.

![A caixa de diálogo de confirmação Excluir conjunto de dados.](../images/datasets/user-guide/delete-confirmation-dialog.png)

## Ações embutidas do conjunto de dados {#inline-actions}

A interface dos conjuntos de dados agora oferece uma coleção de ações em linha para cada conjunto de dados disponível. Selecione as reticências (...) de um conjunto de dados que você deseja gerenciar para ver as opções disponíveis em um menu pop-up. As ações disponíveis incluem:

* [[!UICONTROL Preview dataset]](#preview)
* [[!UICONTROL Manage data and access labels]](#manage-and-enforce-data-governance)
* [[!UICONTROL Enable unified profile]](#enable-profile)
* [[!UICONTROL Manage tags]](#manage-tags)
* [[!UICONTROL Set data retention policy]](#data-retention-policy)
* [[!UICONTROL Move to folders]](#move-to-folders)
* [[!UICONTROL Delete]](#delete).

Mais informações sobre essas ações disponíveis podem ser encontradas nas respectivas seções. Para saber como gerenciar grandes números de conjuntos de dados simultaneamente, consulte a seção [ações em massa](#bulk-actions).

### Visualizar um conjunto de dados {#preview}

Você pode visualizar até 100 linhas de dados de amostra para qualquer conjunto de dados, seja das opções em linha na guia [!UICONTROL Browse] ou da exibição [!UICONTROL Dataset activity].

Na guia [!UICONTROL Browse], selecione as reticências (...) ao lado do nome do conjunto de dados e escolha [!UICONTROL Preview dataset]. Se o conjunto de dados estiver vazio, a opção de visualização será desativada. Como alternativa, na tela **[!UICONTROL Dataset activity]**, selecione **[!UICONTROL Preview dataset]** próximo ao canto superior direito da tela.

![A guia Procurar do espaço de trabalho Conjuntos de Dados com a opção de conjunto de dados reticências e Visualização realçada para o conjunto de dados escolhido.](../images/datasets/user-guide/preview-dataset-option.png)

Isso abre a janela de pré-visualização, onde a visualização hierárquica do esquema do conjunto de dados aparece à esquerda.

>[!NOTE]
>
>O diagrama do esquema à esquerda exibe apenas os campos que contêm dados. Os campos sem dados são ocultos automaticamente para simplificar a interface do usuário e se concentrar em informações relevantes.

![A caixa de diálogo de visualização do conjunto de dados com informações sobre a estrutura, bem como valores de exemplo, para o conjunto de dados são mostrados.](../images/datasets/user-guide/preview-dataset.png)

Como alternativa, na tela **[!UICONTROL Dataset activity]**, selecione **[!UICONTROL Preview dataset]** para abrir a janela de visualização e revisar uma amostra da estrutura e dos valores do seu conjunto de dados.

![O botão Visualizar conjunto de dados está realçado.](../images/datasets/user-guide/select-preview.png)

A janela de visualização do conjunto de dados fornece uma maneira rápida de explorar e validar a estrutura e os dados do seu conjunto de dados.


#### Janela de visualização do conjunto de dados {#dataset-preview-window}

A animação a seguir mostra a janela de visualização do conjunto de dados com seus recursos de navegação e exploração de dados:

![Gravação de tela mostrando a janela de visualização do conjunto de dados. A gravação destaca a barra lateral do navegador de objetos, os indicadores de tipo de dados, a exibição de consulta SQL e a tabela de dados formatada.](../images/datasets/user-guide/dataset-preview-demo.gif)

A janela de visualização do conjunto de dados inclui:

* Uma barra lateral do navegador de objetos à esquerda para navegar e filtrar campos do conjunto de dados.
* Indicadores de tipo de dados ao lado de cada nome de coluna para o insight na estrutura do conjunto de dados.
* Uma consulta SQL é exibida na parte superior da janela, mostrando a consulta usada para gerar o conjunto de dados.
* Uma exibição de tabela formatada de até 100 linhas para uma análise eficiente dos dados.

Esses recursos ajudam você a navegar, entender detalhes do esquema e validar dados de amostra com eficiência.

#### Atalho do Editor de consultas avançado {#query-editor-shortcut}

Se sua organização tiver uma licença do Data Distiller, você poderá acessar o [!UICONTROL Advanced Query Editor] diretamente da janela de visualização do conjunto de dados. Use esse atalho para mover facilmente da visualização de dados de amostra para a execução e refinamento de consultas no Serviço de consulta.

>[!AVAILABILITY]
>
>O acesso ao [!UICONTROL Advanced Query Editor] é limitado a organizações com uma licença do Data Distiller SKU. Se sua organização não tiver a licença necessária, essa opção não aparecerá na janela de visualização do conjunto de dados.

Selecione [!UICONTROL Advanced Query Editor] no canto superior direito da janela de visualização para abrir o Serviço de consulta com sua consulta SQL atual pré-carregada e executada. Você pode continuar analisando ou modificando o SQL sem inserir a consulta novamente.

![Janela de visualização do conjunto de dados mostrando o botão Editor de Consulta Avançado no canto superior direito.](../images/datasets/user-guide/dataset-preview-advanced-query-editor.png)

Para análise adicional, use serviços downstream como [!DNL Query Service] e [!DNL JupyterLab]. Consulte os seguintes documentos para obter mais informações:

* [Visão geral do Serviço de consulta](../../query-service/home.md)
* [Guia do usuário do JupyterLab](../../data-science-workspace/jupyterlab/overview.md)

### Gerenciar e aplicar a governança de dados em um conjunto de dados {#manage-and-enforce-data-governance}

Você pode gerenciar os rótulos de governança de dados para um conjunto de dados selecionando as opções em linha da guia [!UICONTROL Browse]. Selecione as reticências (...) ao lado do nome do conjunto de dados que você deseja gerenciar, seguido por **[!UICONTROL Manage data and access labels]** no menu suspenso.

Os rótulos de uso de dados, aplicados no nível do esquema, permitem categorizar conjuntos de dados e campos de acordo com as políticas de uso que se aplicam a esses dados. Consulte a [visão geral da Governança de dados](../../data-governance/home.md) para saber mais sobre rótulos ou consulte o [guia do usuário de rótulos de uso de dados](../../data-governance/labels/overview.md) para obter instruções sobre como aplicar rótulos a esquemas para propagação para conjuntos de dados.

## Ativar um conjunto de dados para o Perfil do cliente em tempo real {#enable-profile}

Cada conjunto de dados tem a capacidade de enriquecer os perfis do cliente com seus dados assimilados. Para fazer isso, o esquema que o conjunto de dados segue deve ser compatível para uso em [!DNL Real-Time Customer Profile]. Um esquema compatível satisfaz os seguintes requisitos:

* O esquema tem pelo menos um atributo especificado como uma propriedade de identidade.
* O esquema tem uma propriedade de identidade definida como a identidade principal.

Para obter mais informações sobre como habilitar um esquema para [!DNL Profile], consulte o [guia do usuário do Editor de Esquemas](../../xdm/tutorials/create-schema-ui.md).

Você pode habilitar um conjunto de dados para o Perfil nas opções embutidas da guia [!UICONTROL Browse] e também na exibição [!UICONTROL Dataset activity]. Na guia [!UICONTROL Browse] do espaço de trabalho [!UICONTROL Datasets], selecione as reticências de um conjunto de dados que você deseja habilitar para o Perfil. Uma lista de opções de menu é exibida. Em seguida, selecione **[!UICONTROL Enable unified profile]** na lista de opções disponíveis.

![A guia Procurar do espaço de trabalho Conjuntos de Dados com as reticências e Habilitar perfil unificado foi realçada.](../images/datasets/user-guide/enable-for-profile.png)

Como alternativa, na tela **[!UICONTROL Dataset activity]** do conjunto de dados, selecione a opção **[!UICONTROL Profile]** na coluna **[!UICONTROL Properties]**. Depois de ativados, os dados assimilados no conjunto de dados também serão usados para preencher perfis de clientes.

>[!NOTE]
>
>Se um conjunto de dados já contiver dados e estiver habilitado para [!DNL Profile], os dados existentes não serão consumidos automaticamente por [!DNL Profile]. Depois que um conjunto de dados for habilitado para [!DNL Profile], é recomendável assimilar novamente todos os dados existentes para que ele contribua com os perfis do cliente.

![A opção Perfil é realçada na página de detalhes do conjunto de dados.](../images/datasets/user-guide/enable-dataset-profiles.png)

Os conjuntos de dados que foram ativados para o Perfil também podem ser filtrados com esse critério. Consulte a seção sobre como [filtrar conjuntos de dados habilitados por perfil](#filter-profile-enabled-datasets) para obter mais informações.

### Gerenciar tags do conjunto de dados {#manage-tags}

Adicione tags criadas personalizadas para organizar conjuntos de dados e melhorar os recursos de pesquisa, filtragem e classificação. Na guia [!UICONTROL Browse] do espaço de trabalho [!UICONTROL Datasets], selecione as reticências de um conjunto de dados que você deseja gerenciar, seguidas por **[!UICONTROL Manage tags]** no menu suspenso.

![A guia Procurar do espaço de trabalho Conjuntos de Dados com a opção de reticências e Gerenciar marcas foi realçada para o conjunto de dados escolhido.](../images/datasets/user-guide/manage-tags.png)

A caixa de diálogo [!UICONTROL Manage tags] é exibida. Insira uma breve descrição para criar uma tag personalizada ou escolha em uma tag pré-existente para rotular seu conjunto de dados. Selecione **[!UICONTROL Save]** para confirmar suas configurações.

![A caixa de diálogo Gerenciar marcas com marcas personalizadas foi realçada.](../images/datasets/user-guide/manage-tags-dialog.png)

A caixa de diálogo [!UICONTROL Manage tags] também pode remover marcas existentes de um conjunto de dados. Basta selecionar o &#39;x&#39; ao lado da tag que deseja remover e selecionar **[!UICONTROL Save]**.

Depois que uma tag é adicionada a um conjunto de dados, os conjuntos de dados podem ser filtrados com base na tag correspondente. Consulte a seção sobre como [filtrar conjuntos de dados por marcas](#enable-profile) para obter mais informações.

Para obter mais informações sobre como classificar objetos comerciais para facilitar a descoberta e a categorização, consulte o manual em [gerenciando taxonomias de metadados](../../administrative-tags/ui/managing-tags.md). Este guia explica como os usuários com as permissões certas podem criar tags predefinidas, atribuí-las a categorias e gerenciar todas as operações CRUD relacionadas na interface do usuário do Experience Platform.

### Definir política de retenção de dados {#data-retention-policy}

Gerencie as configurações de expiração e retenção do conjunto de dados usando o menu de ação em linha da guia [!UICONTROL Browse] do espaço de trabalho [!UICONTROL Datasets]. Você pode usar esse recurso para configurar por quanto tempo os dados são retidos no data lake e no armazenamento de perfis. A data de expiração se baseia em quando os dados foram assimilados na Experience Platform e no período de retenção configurado.

>[!IMPORTANT]
>
>Para aplicar ou atualizar regras de retenção para um conjunto de dados ExperienceEvent, sua função de usuário deve incluir a permissão **[!UICONTROL Manage datasets]**. Esse controle de acesso baseado em função garante que somente usuários autorizados possam modificar as configurações de retenção do conjunto de dados.
>
>Consulte a [Visão geral do controle de acesso](../../access-control/home.md#platform-permissions) para obter mais informações sobre a atribuição de permissões no Adobe Experience Platform.

>[!TIP]
>
>O data lake armazena dados brutos e não processados, como logs de eventos, dados de sequência de cliques e registros assimilados em massa, para análise e processamento. A Loja de perfis contém dados identificáveis pelo cliente, incluindo eventos compilados por identidade e informações de atributos, para oferecer suporte à personalização e ativação em tempo real.

Para configurar o período de retenção, selecione as reticências ao lado do conjunto de dados seguido por **[!UICONTROL Set data retention policy]** no menu suspenso.

![A guia Procurar do espaço de trabalho Conjuntos de Dados com as reticências e a opção Definir política de retenção de dados realçada.](../images/datasets/user-guide/set-data-retention-policy-dropdown.png)

A caixa de diálogo [!UICONTROL Set dataset retention] é exibida. A caixa de diálogo exibe métricas de uso de licença em nível de sandbox, detalhes em nível de conjunto de dados e configurações atuais de retenção de dados. Essas métricas mostram sua utilização em comparação aos seus direitos e ajudam a avaliar as configurações de armazenamento e retenção específicas do conjunto de dados. As métricas incluem o nome do conjunto de dados, o tipo, o status de ativação do perfil e o uso do data lake e do armazenamento de perfil.

>[!NOTE]
>
>As métricas de armazenamento de data lake licenciadas no nível de sandbox ainda estão em desenvolvimento e podem não aparecer. Um detalhamento completo das métricas de uso de licença pode ser encontrado no painel Uso da licença. Consulte a documentação para obter descrições dessas métricas.
<!-- replace this screenshot with a dataset that enabled unified profile so user can see the Profile TTL settings -->
![A caixa de diálogo Definir retenção do conjunto de dados.](../images/datasets/user-guide/set-data-retention-dialog.png)

Configure seu período de retenção preferido na caixa de diálogo de configurações de retenção de dados. Insira um número e selecione uma unidade de tempo (dias, meses ou anos) no menu suspenso. Você pode definir configurações de retenção separadas para o data lake e o Serviço de perfil.

>[!NOTE]
> 
>O período mínimo de retenção para o data lake é de 30 dias. O período mínimo de retenção do Serviço de perfil é de um dia.
>
>Além disso, você só pode atualizar o período de retenção do Serviço de perfil uma vez a cada 30 dias.

Para oferecer suporte à transparência e ao monitoramento, os carimbos de data e hora são fornecidos para as execuções de trabalho de retenção de dados **last** e **next**. Os carimbos de data e hora ajudam a entender quando ocorreu a última limpeza de dados e quando a próxima está programada.

#### Insights de impacto do armazenamento {#storage-impact-insights}

Para abrir uma previsão visual do impacto de armazenamento de diferentes políticas de retenção, selecione **[!UICONTROL View Experience Event Data distribution]**.

O gráfico exibe a distribuição de eventos de experiência em vários períodos de retenção para o conjunto de dados selecionado no momento. Passe o mouse sobre cada barra para ver o número exato de registros que serão removidos se o período de retenção selecionado for aplicado.

Você pode usar a previsão visual para avaliar o impacto de diferentes períodos de retenção e tomar decisões comerciais informadas. Por exemplo, se você selecionar um período de retenção de 30 dias e o gráfico mostrar que 60% dos dados serão excluídos, será possível optar por estender a retenção para preservar mais dados para análise.

>[!NOTE]
>
>O gráfico de distribuição do Evento de experiência é específico para o conjunto de dados selecionado e reflete apenas seus dados. Ela se aplica exclusivamente aos dados armazenados no data lake.

![A caixa de diálogo Definir retenção de dados com o gráfico de distribuição Evento de Experiência foi exibida.](../images/datasets/user-guide/visual-forecast.png)

Quando estiver satisfeito com sua configuração, selecione **[!UICONTROL Save]** para confirmar suas configurações.

>[!IMPORTANT]
>
>Quando as regras de retenção de dados forem aplicadas, todos os dados anteriores ao número de dias definido pelo valor de expiração serão excluídos permanentemente e não poderão ser recuperados.

Depois de definir as configurações de retenção, use a interface de monitoramento para confirmar se as alterações foram executadas pelo sistema. A interface de monitoramento fornece uma exibição centralizada da atividade de retenção de dados em todos os conjuntos de dados. A partir daí, você pode rastrear a execução do trabalho, revisar quantos dados foram excluídos e garantir que suas políticas de retenção estejam funcionando como esperado.

Para explorar como as políticas de retenção se aplicam a diferentes serviços, consulte os guias dedicados em [Retenção do conjunto de dados do evento de experiência no perfil](../../profile/event-expirations.md) e [Retenção do conjunto de dados do evento de experiência no Data Lake](./experience-event-dataset-retention-ttl-guide.md). Essa visibilidade apoia o controle, a conformidade e o gerenciamento eficiente do ciclo de vida dos dados.

Para saber como usar o painel de monitoramento para rastrear fluxos de dados de origem na interface do usuário do Experience Platform, consulte a documentação [Monitorar fluxos de dados de origens na interface do usuário](../../dataflows/ui/monitor-sources.md).

<!-- Improve the link above. I cannot link to a 100% appropriate document yet. -->

Para obter mais informações sobre as regras que definem intervalos de datas de expiração do conjunto de dados e práticas recomendadas para configurar sua política de retenção de dados, consulte a [página de perguntas frequentes](../catalog-faq.md).

#### Maior visibilidade dos períodos de retenção e das métricas de armazenamento {#retention-and-storage-metrics}

Quatro novas colunas oferecem maior visibilidade ao gerenciamento de dados: **[!UICONTROL Data Lake Storage]**, **[!UICONTROL Data Lake Retention]**, **[!UICONTROL Profile Storage]** e **[!UICONTROL Profile Retention]**. Essas métricas mostram quanto armazenamento seus dados consomem e o período de retenção no data lake e no serviço de perfil.

Essa maior visibilidade permite que você tome decisões conscientes e gerencie os custos de armazenamento com mais eficiência. Classifique os conjuntos de dados por tamanho de armazenamento para identificar os maiores na sandbox atual. Esses insights oferecem suporte às práticas recomendadas de gerenciamento de dados e ajudam a garantir a conformidade com seus direitos licenciados.

![A guia Procurar do espaço de trabalho Conjuntos de Dados com as quatro novas colunas de armazenamento e retenção realçadas.](../images/datasets/user-guide/storage-and-retention-columns.png)

A tabela a seguir fornece uma visão geral das novas métricas de retenção e armazenamento. Ela detalha a finalidade de cada coluna e como ela oferece suporte ao gerenciamento da retenção e do armazenamento de dados.

| Título da coluna | Descrição |
|---|---|
| [!UICONTROL Data Lake Retention] | O período de retenção atual para cada conjunto de dados no data lake. Esse valor é configurável e determina por quanto tempo os dados são retidos antes da exclusão. |
| [!UICONTROL Data Lake Storage] | O uso de armazenamento atual para cada conjunto de dados no data lake. Use essa métrica para gerenciar limites de armazenamento e otimizar o uso. |
| [!UICONTROL Profile Storage] | O uso de armazenamento atual para cada conjunto de dados no Serviço de perfil. Ajuda a monitorar o consumo de armazenamento e a apoiar as decisões de gerenciamento de dados. |
| [!UICONTROL Profile Retention] | O período de retenção atual para conjuntos de dados de Perfil. Você pode atualizar esse valor para controlar por quanto tempo os dados do perfil são retidos. |

{style="table-layout:auto"}

Para agir com base nos insights das métricas de armazenamento e retenção, consulte o [guia de práticas recomendadas de direito de licença de gerenciamento de dados](../../landing/license-usage-and-guardrails/data-management-best-practices.md). Use-a para gerenciar quais dados você assimila e retém, aplicar filtros e regras de expiração e controlar o crescimento dos dados para permanecer dentro dos limites de uso licenciados.

### Mover para pastas {#move-to-folders}

Você pode colocar conjuntos de dados em pastas para melhorar o gerenciamento do conjunto de dados. Para mover um conjunto de dados para uma pasta, selecione as reticências (...) ao lado do nome do conjunto de dados que você deseja gerenciar, seguido por **[!UICONTROL Move to folder]** no menu suspenso.

![O painel [!UICONTROL Datasets] com as reticências e [!UICONTROL Move to folder] realçado.](../images/datasets/user-guide/move-to-folder.png)

A caixa de diálogo [!UICONTROL Move] conjunto de dados para pasta é exibida. Selecione a pasta para onde deseja mover o público-alvo e selecione **[!UICONTROL Move]**. Uma notificação pop-up informa que a movimentação do conjunto de dados foi bem-sucedida.

![A caixa de diálogo do conjunto de dados [!UICONTROL Move] com [!UICONTROL Move] está realçada.](../images/datasets/user-guide/move-dialog.png)

>[!TIP]
>
>Você também pode criar pastas diretamente na caixa de diálogo Mover conjunto de dados. Para criar uma pasta, selecione o ícone criar pasta (![O ícone criar pasta.](/help/images/icons/folder-add.png)) na parte superior direita da caixa de diálogo.
>
>![A caixa de diálogo do conjunto de dados [!UICONTROL Move] com o ícone de criação de pasta está realçada.](/help/catalog/images/datasets/user-guide/create-folder.png)

Quando o conjunto de dados estiver em uma pasta, você poderá optar por exibir somente os conjuntos de dados que pertencem a uma pasta específica. Para abrir a estrutura de pastas, selecione o ícone mostrar pastas (![O ícone mostrar pastas](/help/images/icons/rail-left.png)). Em seguida, selecione a pasta escolhida para ver todos os conjuntos de dados associados.

![Os painéis [!UICONTROL Datasets] com a estrutura de pastas dos conjuntos de dados exibida, o ícone mostrar pastas e uma pasta selecionada realçada.](../images/datasets/user-guide/folder-structure.png)

### Excluir um conjunto de dados {#delete}

Você pode excluir um conjunto de dados das ações embutidas do conjunto de dados na guia [!UICONTROL Browse] ou na parte superior direita da exibição [!UICONTROL Dataset activity]. Na exibição [!UICONTROL Browse], selecione as reticências (...) ao lado do nome do conjunto de dados que deseja excluir. Uma lista de opções de menu é exibida. Em seguida, selecione **[!UICONTROL Delete]** no menu suspenso.

![A guia Procurar do espaço de trabalho Conjuntos de Dados com as reticências e a opção Excluir realçada para o conjunto de dados escolhido.](../images/datasets/user-guide/inline-delete-dataset.png)

Uma caixa de diálogo de confirmação é exibida. Selecione **[!UICONTROL Delete]** para confirmar.

Como alternativa, selecione **[!UICONTROL Delete dataset]** na tela **[!UICONTROL Dataset activity]**.

>[!NOTE]
>
>Conjuntos de dados criados e utilizados por aplicativos e serviços da Adobe (como Adobe Analytics, Adobe Audience Manager ou [!DNL Offer Decisioning]) não podem ser excluídos.

![O botão Excluir conjunto de dados está realçado na página de detalhes do conjunto de dados.](../images/datasets/user-guide/delete-dataset.png)

Uma caixa de confirmação é exibida. Selecione **[!UICONTROL Delete]** para confirmar a exclusão do conjunto de dados.

![O modal de confirmação para exclusão é exibido, com o botão Excluir realçado.](../images/datasets/user-guide/confirm-delete.png)

### Excluir um conjunto de dados habilitado para perfil

Se um conjunto de dados estiver ativado para o Perfil, a exclusão desse conjunto de dados por meio da interface do usuário o excluirá do data lake, do Serviço de identidade e também de quaisquer dados de perfil associados a esse conjunto de dados no Armazenamento de perfis.

Você pode excluir dados de perfil associados a um conjunto de dados do armazenamento [!DNL Profile] (deixando os dados no data lake) usando a API de Perfil de Cliente em Tempo Real. Para obter mais informações, consulte o [manual de ponto de extremidade da API de trabalhos do sistema de perfil](../../profile/api/profile-system-jobs.md).

## Pesquisar e filtrar conjuntos de dados {#search-and-filter}

Para pesquisar ou filtrar a lista de conjuntos de dados disponíveis, selecione o ícone de filtro (![O ícone de filtro.](/help/images/icons/filter.png)) na parte superior esquerda do espaço de trabalho. Um conjunto de opções de filtro no painel esquerdo é exibido. Há vários métodos para filtrar seus conjuntos de dados disponíveis. Isso inclui: [[!UICONTROL Show System Datasets]](#show-system-datasets), [[!UICONTROL Included in profile]](#filter-profile-enabled-datasets), [[!UICONTROL Tags]](#filter-by-tag), [[!UICONTROL Creation date]](#filter-by-creation-date), [[!UICONTROL Modified date], [!UICONTROL Created by]](#filter-by-creation-date) e [[!UICONTROL Schema]](#filter-by-schema).

A lista de filtros aplicados é exibida acima dos resultados filtrados.

![A guia Procurar do espaço de trabalho Conjuntos de Dados com a lista de filtros aplicados realçada.](../images/datasets/user-guide/applied-filters.png)

### Mostrar conjuntos de dados do sistema {#show-system-datasets}

Por padrão, somente os conjuntos de dados que você assimilou no são mostrados. Se quiser ver os conjuntos de dados gerados pelo sistema, marque a caixa de seleção **[!UICONTROL Yes]** na seção [!UICONTROL Show system datasets]. Os conjuntos de dados gerados pelo sistema são usados apenas para processar outros componentes. Por exemplo, o conjunto de dados de exportação de perfil gerado pelo sistema é usado para processar o painel de perfis.

![As opções de filtro do espaço de trabalho de Conjuntos de Dados com a seção [!UICONTROL Show system datasets] realçada.](../images/datasets/user-guide/show-system-datasets.png)

### Filtrar conjuntos de dados habilitados para o perfil {#filter-profile-enabled-datasets}

Os conjuntos de dados que foram habilitados para dados de Perfil são usados para preencher perfis de clientes após a assimilação de dados. Consulte a seção sobre [habilitação de conjuntos de dados para o Perfil](#enable-profile) para saber mais.

Para filtrar seu conjunto de dados com base no fato de terem sido habilitados para o Perfil, marque a caixa de seleção [!UICONTROL Yes] nas opções de filtro.

![As opções de filtro do espaço de trabalho de Conjuntos de Dados com a seção [!UICONTROL Included in Profile] realçada.](../images/datasets/user-guide/included-in-profile.png)

### Filtrar conjuntos de dados por tag {#filter-by-tag}

Insira seu nome de tag personalizado na entrada [!UICONTROL Tags] e selecione sua tag na lista de opções disponíveis para pesquisar e filtrar conjuntos de dados que correspondam a essa tag.

![As opções de filtro do espaço de trabalho Conjuntos de Dados com o ícone de filtro e entrada [!UICONTROL Tags] realçado.](../images/datasets/user-guide/filter-tags.png)

### Filtrar conjuntos de dados por data de criação {#filter-by-creation-date}

Os conjuntos de dados podem ser filtrados pela data de criação em um período personalizado. Isso pode ser usado para excluir dados históricos ou gerar insights de dados cronológicos e relatórios específicos. Escolha uma [!UICONTROL Start date] e uma [!UICONTROL End date] selecionando o ícone de calendário de cada campo. Depois disso, somente os conjuntos de dados que estão em conformidade com esses critérios aparecerão na guia Procurar.

### Filtrar conjuntos de dados por data de modificação {#filter-by-modified-date}

Semelhante ao filtro para data de criação, é possível filtrar seus conjuntos de dados com base na data em que foram modificados pela última vez. Na seção [!UICONTROL Modified date], escolha um [!UICONTROL Start date] e um [!UICONTROL End date] selecionando o ícone de calendário de cada campo. Depois disso, somente os conjuntos de dados modificados durante esse período aparecerão na guia Procurar.

### Filtrar por esquema {#filter-by-schema}

Você pode filtrar conjuntos de dados com base no esquema que define sua estrutura. Selecione o ícone suspenso ou insira o nome do schema no campo de texto. Uma lista de correspondências em potencial é exibida. Selecione o schema apropriado na lista.

## Ações em massa {#bulk-actions}

Use ações em massa para aprimorar a eficiência operacional e execute várias ações em vários conjuntos de dados simultaneamente. Você pode economizar tempo e manter uma estrutura de dados organizada com ações em massa, como [Mover para pasta](#move-to-folders), [Editar tags](#manage-tags) e [Excluir](#delete) conjuntos de dados.

Para atuar em mais de um conjunto de dados por vez, selecione conjuntos de dados individuais com a caixa de seleção em cada linha ou selecione uma página inteira com a caixa de seleção do cabeçalho da coluna. Depois de selecionada, a barra de ação em massa é exibida.

![A guia Procurar Conjuntos de Dados com vários conjuntos de dados selecionados e a barra de ação em massa realçada.](../images/datasets/user-guide/bulk-actions.png)

Quando você aplica ações em massa a conjuntos de dados, as seguintes condições se aplicam:

* É possível selecionar conjuntos de dados de diferentes páginas da interface do usuário.
* Se você selecionar um filtro, os conjuntos de dados selecionados serão redefinidos.

## Classificar conjuntos de dados por data de criação {#sort}

Os conjuntos de dados na guia [!UICONTROL Browse] podem ser classificados por datas crescentes ou decrescentes. Selecione os cabeçalhos de coluna [!UICONTROL Created] ou [!UICONTROL Last updated] para alternar entre ordem crescente e decrescente. Depois de selecionada, a coluna indica isso com uma seta para cima ou para baixo ao lado do cabeçalho da coluna.

![A guia Procurar do espaço de trabalho Conjuntos de Dados com a coluna Criado e Última atualização realçada.](../images/datasets/user-guide/ascending-descending-columns.png)

## Criar um conjunto de dados {#create}

Para criar um novo conjunto de dados, comece selecionando **[!UICONTROL Create dataset]** no painel **[!UICONTROL Datasets]**.

![O botão Criar conjunto de dados está realçado.](../images/datasets/user-guide/select-create.png)

Na próxima tela, você verá as duas opções a seguir para criar um novo conjunto de dados:

* [Criar conjunto de dados a partir de esquema](#schema)
* [Criar conjunto de dados a partir de arquivo CSV](#csv)

### Criar um conjunto de dados com um esquema existente {#schema}

Na tela **[!UICONTROL Create dataset]**, selecione **[!UICONTROL Create dataset from schema]** para criar um novo conjunto de dados vazio.

![O botão Criar conjunto de dados a partir do esquema está realçado.](../images/datasets/user-guide/create-dataset-schema.png)

A etapa **[!UICONTROL Select schema]** é exibida. Procure a lista de esquemas e selecione o esquema ao qual o conjunto de dados seguirá antes de selecionar **[!UICONTROL Next]**.

![Uma lista de esquemas é exibida. O esquema que será usado para criar o conjunto de dados está realçado.](../images/datasets/user-guide/select-schema.png)

A etapa **[!UICONTROL Configure dataset]** é exibida. Forneça um nome e uma descrição opcional ao conjunto de dados e selecione **[!UICONTROL Finish]** para criar o conjunto de dados.

![Os detalhes de configuração do conjunto de dados foram inseridos. Isso inclui detalhes como nome e descrição do conjunto de dados.](../images/datasets/user-guide/configure-dataset-schema.png)

Os conjuntos de dados podem ser filtrados da lista de conjuntos de dados disponíveis na interface do usuário com o filtro de esquema. Consulte a seção sobre como [filtrar conjuntos de dados por esquema](#filter-by-schema) para obter mais informações.

### Criar um conjunto de dados com um arquivo CSV {#csv}

Quando um conjunto de dados é criado usando um arquivo CSV, um esquema ad hoc é criado para fornecer ao conjunto de dados uma estrutura que corresponde ao arquivo CSV fornecido. Na tela **[!UICONTROL Create dataset]**, selecione **[!UICONTROL Create dataset from CSV file]**.

![O botão Criar conjunto de dados a partir de arquivo CSV está realçado.](../images/datasets/user-guide/create-dataset-csv.png)

A etapa **[!UICONTROL Configure]** é exibida. Forneça um nome e uma descrição opcional ao conjunto de dados e selecione **[!UICONTROL Next]**.

![Os detalhes de configuração do conjunto de dados foram inseridos. Isso inclui detalhes como nome e descrição do conjunto de dados.](../images/datasets/user-guide/configure-dataset-csv.png)

A etapa **[!UICONTROL Add data]** é exibida. Carregue o arquivo CSV arrastando-o e soltando-o no centro da tela ou selecione **[!UICONTROL Browse]** para explorar o diretório do arquivo. O arquivo pode ter até dez gigabytes. Após carregar o arquivo CSV, selecione **[!UICONTROL Save]** para criar o conjunto de dados.

>[!NOTE]
>
>Os nomes das colunas CSV devem começar com caracteres alfanuméricos e podem conter apenas letras, números e sublinhados.

![A tela Adicionar dados é exibida. O local onde você pode carregar o arquivo CSV para o conjunto de dados está realçado.](../images/datasets/user-guide/add-csv-data.png)

## Monitorar assimilação de dados

Na interface do usuário do [!DNL Experience Platform], selecione **[!UICONTROL Monitoring]** no menu de navegação esquerdo. O painel **[!UICONTROL Monitoring]** permite a visualização dos status dos dados de entrada a partir da assimilação em lote ou por transmissão. Para exibir os status de lotes individuais, selecione **[!UICONTROL Batch end-to-end]** ou **[!UICONTROL Streaming end-to-end]**. Os painéis listam todas as execuções de assimilação em lote ou por transmissão, incluindo as que foram bem-sucedidas, falharam ou ainda estão em andamento. Cada lista fornece detalhes do lote, incluindo a ID do lote, o nome do conjunto de dados de destino e o número de registros assimilados. Se o conjunto de dados de destino estiver habilitado para [!DNL Profile], o número de registros de identidade e perfil assimilados também será exibido.

![A tela inteira do lote de monitoramento é mostrada. Tanto o monitoramento quanto o lote a lote estão destacados.](../images/datasets/user-guide/batch-listing.png)

Você pode selecionar um **[!UICONTROL Batch ID]** individual para acessar o painel **[!UICONTROL Batch overview]** e ver os detalhes do lote, incluindo logs de erros caso o lote não seja assimilado.

![Detalhes do lote selecionado são exibidos. Isso inclui o número de registros assimilados, o número de registros com falha, o status do lote, o tamanho do arquivo, as horas inicial e final da assimilação, o conjunto de dados e as IDs do lote, a ID da organização, o nome do conjunto de dados e as informações de acesso.](../images/datasets/user-guide/batch-overview.png)

Se desejar excluir o lote, selecione **[!UICONTROL Delete batch]** próximo à parte superior direita do painel. A exclusão de um lote também remove seus registros do conjunto de dados ao qual o lote foi originalmente assimilado.

>[!NOTE]
>
>Se os dados assimilados tiverem sido ativados para Perfil e processados, a exclusão de um lote não excluirá esses dados do armazenamento de Perfil.

![O botão Excluir lote está realçado na página de detalhes do conjunto de dados.](../images/datasets/user-guide/delete-batch.png)

## Próximas etapas

Este guia do usuário forneceu instruções para executar ações comuns ao trabalhar com conjuntos de dados na interface do usuário do [!DNL Experience Platform]. Para obter as etapas sobre como executar fluxos de trabalho [!DNL Experience Platform] comuns envolvendo conjuntos de dados, consulte os seguintes tutoriais:

* [Criar um conjunto de dados usando APIs](create.md)
* [Consultar dados do conjunto de dados usando a API de acesso a dados](../../data-access/home.md)
* [Configurar um conjunto de dados para o Perfil do cliente em tempo real e o Serviço de identidade usando APIs](../../profile/tutorials/dataset-configuration.md)

