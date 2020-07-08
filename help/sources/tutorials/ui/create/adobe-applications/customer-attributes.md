---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Criar um conector de origem de atributos do cliente na interface do usuário
topic: overview
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 7%

---


# Criar um conector de origem de atributos do cliente na interface do usuário

Este tutorial fornece etapas para criar um conector de origem na interface do usuário para coletar dados de perfil de atributos do cliente no Adobe Experience Platform. Para obter mais informações sobre atributos do cliente, consulte o documento [de](https://docs.adobe.com/content/help/pt-BR/core-services/interface/customer-attributes/attributes.html)visão geral.

## Criar uma conexão de origem

Faça logon no <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> e selecione **Fontes** na barra de navegação esquerda para acessar a área de trabalho de fontes. A tela *Catálogo* exibe as fontes disponíveis para criar conexões de entrada e cada fonte mostra o número de conexões existentes associadas a elas. Selecione a opção Atributos **do** cliente e clique em Origem **do** Connect. Aguarde até que a conexão seja estabelecida, você será redirecionado se uma conexão for estabelecida com êxito.

>[!NOTE]
>
>Se você já tiver estabelecido um conector de origem para dados de perfil de atributos do cliente, a opção de conexão com a fonte será desativada.

![](../../../../images/tutorials/create/customer-attributes/CA-sources_catalog.png)

A tela atividade *de origem lista todas as conexões estabelecidas anteriormente para os dados de perfil dos atributos do cliente. Você pode criar uma nova conexão clicando em* Selecionar dados ****.

>[!NOTE]
>
>Várias conexões de entrada para uma fonte podem ser feitas para inserir dados diferentes.

![](../../../../images/tutorials/create/customer-attributes/CA-source_activity.png)

Na lista de conjuntos de dados de perfil de atributos do cliente disponíveis, selecione aquele que deseja trazer para o Platform e clique em **Avançar**.

>[!NOTE]
>
>Somente um conjunto de dados pode ser selecionado por conexão de origem de atributos do cliente.

![](../../../../images/tutorials/create/customer-attributes/CA-select_data.png)

A etapa *Revisar* é exibida, permitindo que você revise sua nova conexão de entrada antes de ela ser criada. Os detalhes da conexão são agrupados por categorias, incluindo:

* *Detalhes* da fonte: Mostra o tipo da conexão de origem e os dados de origem selecionados.
* *Detalhes* do Público alvo: Ao criar outros conectores de origem, esse container mostra em qual conjunto de dados os dados de origem estão assimilando, incluindo o schema ao qual o conjunto de dados está aderindo. Os dados do perfil dos atributos do cliente são mapeados e assimilados automaticamente nos Perfis do cliente em tempo real.

![](../../../../images/tutorials/create/customer-attributes/CA-review.png)

## Próximas etapas

Depois que a conexão é criada, um esquema de público-alvo e um conjunto de dados são criados automaticamente para conter os dados recebidos. Quando a ingestão inicial for concluída, os dados do perfil dos atributos do cliente poderão ser usados pelos serviços Platform de downstream, como Perfil do cliente em tempo real e Serviço de segmentação. Consulte os seguintes documentos para obter mais detalhes:

* [Visão geral do Perfil do cliente em tempo real](../../../../../profile/home.md)
* [Visão geral do Serviço de segmentação](../../../../../segmentation/home.md)
