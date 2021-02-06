---
keywords: Experience Platform;home;popular topics;conector de origem do gerenciador de Audiências;Audience Manager;conector do gerenciador de audiências;home;popular topics;conector de origem do gerenciador de ;;manager
solution: Experience Platform
title: Criar uma conexão de origem Adobe Audience Manager na interface do usuário
topic: overview
type: Tutorial
description: Este tutorial o orienta pelas etapas para criar conectores de origem para a Adobe Audience Manager trazer os dados do Evento da Experiência do consumidor para a Plataforma usando a interface do usuário.
translation-type: tm+mt
source-git-commit: c7fb0d50761fa53c1fdf4dd70a63c62f2dcf6c85
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 0%

---


# Criar uma conexão de origem Adobe Audience Manager na interface do usuário

Este tutorial o orienta pelas etapas para criar um conector de origem para a Adobe Audience Manager, que traz os dados do Evento de experiência do consumidor para a Plataforma usando a interface do usuário.

## Criar uma conexão de origem com o Adobe Audience Manager

Faça logon em [Adobe Experience Platform](https://platform.adobe.com) e selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar a área de trabalho [!UICONTROL Fontes]. A tela [!UICONTROL Catalog] exibe várias fontes com as quais você pode criar uma conta.

Na categoria [!UICONTROL Applications] Adobe, selecione **[!UICONTROL Adobe Audience Manager]** e selecione **[!UICONTROL Configurar]**.

![catálogo](../../../../images/tutorials/create/aam/catalog.png)

A etapa [!UICONTROL Selecionar características e segmentos] é exibida, fornecendo uma interface interativa para explorar e selecionar suas características, segmentos e dados.

* O painel esquerdo da interface contém as opções [!UICONTROL Selecionar características e segmentos], bem como um diretório hierárquico de todos os segmentos disponíveis para você.
* A metade direita da interface permite interagir com segmentos selecionados e selecionar dados específicos que você deseja usar.

![add-data](../../../../images/tutorials/create/aam/add-data.png)

Para navegar pelos segmentos disponíveis, selecione a pasta que deseja acessar no painel [!UICONTROL Todos os segmentos]. Selecionar uma pasta permite que você percorra a hierarquia de uma pasta e fornece uma lista de segmentos para filtrar.

![segment-folder](../../../../images/tutorials/create/aam/segment-folder.png)

Depois de identificar e selecionar os segmentos que deseja usar, um novo painel aparecerá à direita, exibindo sua lista de itens selecionados. Você pode continuar a acessar pastas diferentes e selecionar segmentos diferentes para sua conexão. Selecionar mais segmentos atualiza o painel à direita.

![select-data](../../../../images/tutorials/create/aam/select-data.png)

Como alternativa, você pode selecionar as caixas **[!UICONTROL Selecionar todos os segmentos]** e **[!UICONTROL Selecionar todas as características]**. A seleção de todos os segmentos trará os segmentos de Audience Manager para a Plataforma, enquanto a seleção de todas as características permite que todas as características principais sejam incluídas no Audience Manager.

Quando terminar, selecione **[!UICONTROL Próximo]**

![todos os segmentos](../../../../images/tutorials/create/aam/all-segments.png)

A etapa [!UICONTROL Revisar] é exibida, permitindo que você analise suas características e segmentos selecionados antes que eles estejam conectados à Plataforma. Os detalhes são agrupados nas seguintes categorias:

* **[!UICONTROL Conexão]**: Mostra a plataforma de origem e o status da conexão.
* **[!UICONTROL Dados]** selecionados: Mostra o número de segmentos selecionados e características ativadas.

![revisão](../../../../images/tutorials/create/aam/review.png)

Depois de revisar seu fluxo de dados, selecione **[!UICONTROL Finalizar]** e aguarde algum tempo para que o fluxo de dados seja criado.

## Próximas etapas

Enquanto um fluxo de dados Audience Manager está ativo, os dados recebidos são automaticamente assimilados aos Perfis do cliente em tempo real. Agora você pode utilizar esses dados de entrada e criar segmentos de audiência usando o Serviço de segmentação de plataforma. Consulte os seguintes documentos para obter mais detalhes:

* [Visão geral do Perfil do cliente em tempo real](../../../../../profile/home.md)
* [Visão geral do Serviço de segmentação](../../../../../segmentation/home.md)