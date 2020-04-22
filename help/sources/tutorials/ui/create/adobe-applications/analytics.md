---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Criar um conector de origem do Adobe Analytics na interface do usuário
topic: overview
translation-type: tm+mt
source-git-commit: ac1e5dbe435d9e85e8ce3ad90c60dd31ba9248ff

---


# Criar um conector de origem do Adobe Analytics na interface do usuário

Este tutorial fornece etapas para a criação de um conector de origem do Adobe Analytics na interface do usuário, a fim de trazer os dados do consumidor para a plataforma Adobe Experience.

## Criar uma conexão de origem com o Adobe Analytics

Faça logon na <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> e selecione **Fontes** na barra de navegação esquerda para acessar a área de trabalho de fontes. A tela *Catálogo* exibe as fontes disponíveis para criar conexões de entrada e cada fonte mostra o número de conexões existentes associadas a elas. Selecione a opção para o **Adobe Analytics** e clique em Fonte **de** Visualização para ver todas as conexões estabelecidas em vínculo a ela.

![](../../../../images/tutorials/create/analytics/AA-sources_catalog.png)

A tela atividade *de origem lista todas as conexões estabelecidas anteriormente com o Adobe Analytics. Para criar uma nova conexão, clique em* Selecionar dados ****.

>[!NOTE] Várias conexões de entrada para uma fonte podem ser feitas para inserir dados diferentes.

![](/help/sources/images/tutorials/create/analytics/AA-source_activity.png)

Na lista dos conjuntos de relatórios disponíveis, selecione o que deseja trazer para a Plataforma e clique em **Avançar**.

>[!NOTE] Somente um conjunto de relatórios pode ser selecionado por conexão de origem do Analytics. Além disso, apenas um conjunto de relatórios pode existir em uma caixa de proteção.

![](../../../../images/tutorials/create/analytics/AA-select_data.png)

A etapa *Revisar* é exibida, permitindo que você reveja sua nova conexão vinculada ao Analytics antes de ela ser criada. Os detalhes da conexão são agrupados por categorias, incluindo:

* *Detalhes* da fonte: Mostra o tipo da conexão de origem e o conjunto de relatórios selecionado.
* *Detalhes* do Público alvo: Ao criar outros conectores de origem, esse container mostra em qual conjunto de dados os dados de origem estão assimilando, incluindo o schema ao qual o conjunto de dados está aderindo. Os dados do Analytics são mapeados e assimilados automaticamente em Perfis do cliente em tempo real.

![](../../../../images/tutorials/create/analytics/AA-review.png)

## Próximas etapas

Depois que a conexão é criada, um schema de público alvo e um conjunto de dados são criados automaticamente para conter os dados recebidos. Além disso, ocorre o preenchimento retroativo de dados e ingere até 13 meses de dados históricos. Quando a ingestão inicial for concluída, os dados do Analytics e serão usados pelos serviços de plataforma downstream, como o Perfil do cliente em tempo real e o Serviço de segmentação. Consulte os seguintes documentos para obter mais detalhes:

* [Visão geral do Perfil do cliente em tempo real](../../../../../profile/home.md)
* [Visão geral do Serviço de segmentação](../../../../../segmentation/home.md)
* [Visão geral da Análise do espaço de trabalho da Data Science](../../../../../data-science-workspace/home.md)
* [Visão geral do Serviço de Query](../../../../../query-service/home.md)

