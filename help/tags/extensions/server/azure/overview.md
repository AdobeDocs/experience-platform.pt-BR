---
title: Visão geral da extensão do Microsoft Azure
description: Saiba mais sobre a extensão do Microsoft Azure para encaminhamento de eventos no Adobe Experience Platform.
exl-id: 2337d99d-861e-44e7-94ed-ba21ef28d815
last-substantial-update: 2022-11-23T00:00:00Z
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '794'
ht-degree: 0%

---

# Visão geral da extensão do [!DNL Microsoft Azure]

No [!DNL Microsoft Azure], o [[!DNL Event Hubs]](https://azure.microsoft.com/en-us/products/event-hubs/#overview) é um serviço de entrada de dados em tempo real altamente escalável que permite processar e analisar as grandes quantidades de dados produzidas pelos seus dispositivos e aplicativos conectados. Depois que os dados são coletados em um hub de eventos, eles podem ser transformados e armazenados usando qualquer provedor de análise em tempo real ou adaptadores de armazenamento/em lote.

A extensão [!DNL Microsoft Azure] [encaminhamento de eventos](../../../ui/event-forwarding/overview.md) aproveita o [!DNL Event Hubs] para enviar eventos do Adobe Experience Platform Edge Network para o [!DNL Azure] para processamento adicional. Este guia aborda como instalar a extensão e empregar seus recursos em uma regra de encaminhamento de eventos.

## Pré-requisitos

Para usar essa extensão, você deve ter uma conta válida do [!DNL Azure] com acesso ao [!DNL Event Hubs]. Você também deve [criar um hub de eventos usando o [!DNL Azure] portal](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create) antes de seguir as etapas abaixo.

## Instalar a extensão

Para instalar a extensão [!DNL Azure] do Microsoft, navegue até a interface da Coleção de dados ou a interface do usuário do Experience Platform e selecione **[!UICONTROL Event Forwarding]** na navegação à esquerda. Aqui, selecione uma propriedade à qual adicionar a extensão ou crie uma nova propriedade.

Depois de selecionar ou criar a propriedade desejada, selecione **[!UICONTROL Extensions]** na navegação à esquerda e, em seguida, selecione a guia **[!UICONTROL Catalog]**. Procure o cartão [!UICONTROL Microsoft Azure] e selecione **[!UICONTROL Install]**.

![O botão [!UICONTROL Install] que está sendo selecionado para a extensão [!UICONTROL Microsoft Azure] na interface da Coleção de Dados.](../../../images/extensions/server/azure/install.png)

Como a extensão não tem propriedades de configuração, ela é adicionada imediatamente à lista de extensões instaladas. Agora você pode começar a usar os tipos de ação [!DNL Event Hub] ao configurar as regras de encaminhamento de eventos.

## Configurar uma regra de encaminhamento de eventos {#rule}

Comece a criar uma nova regra de encaminhamento de eventos e configure as condições conforme desejado. Ao selecionar as ações para a regra, selecione **[!UICONTROL Microsoft Azure]** para a extensão e **[!UICONTROL Send Data to Event Hubs]** para o tipo de ação.

![O tipo de ação [!UICONTROL Send Data to Event Hubs] que está sendo selecionado para uma regra na interface da Coleção de Dados.](../../../images/extensions/server/azure/select-action-type.png)

O painel direito atualiza para mostrar as opções de configuração de como os dados devem ser enviados. Você deve atribuir [elementos de dados](../../../ui/managing-resources/data-elements.md) às várias propriedades que representam sua configuração [!DNL Event Hub].

![As opções de configuração para o tipo de ação [!UICONTROL Send Data to Event Hubs] mostradas na interface do usuário.](../../../images/extensions/server/azure/event-hub-details.png)

**[!UICONTROL Event Hub Details]**

| Entrada | Descrição |
| --- | --- |
| [!UICONTROL Namespace] | O nome do namespace [!DNL Event Hubs] que você criou ao [configurar o hub de eventos](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace). |
| [!UICONTROL Name] | O nome do hub de eventos. |
| [!UICONTROL SAS Authorization Rule Name] | O nome da regra de autorização de acesso compartilhado para todo o namespace [!DNL Event Hubs] ou a instância do hub de eventos específica para a qual você deseja enviar dados. Consulte a seção do apêndice sobre [obtenção de valores de autorização SAS](#sas) para obter mais informações. |
| [!UICONTROL SAS Access Key] | A chave primária da regra de autorização de acesso compartilhado para todo o namespace [!DNL Event Hubs] ou a instância do hub de eventos específico para a qual você deseja enviar dados. Consulte a seção do apêndice sobre [obtenção de valores de autorização SAS](#sas) para obter mais informações. |
| [!UICONTROL Partition ID] | [!DNL Event Hubs] permite [enviar eventos diretamente para partições específicas](https://learn.microsoft.com/en-us/azure/architecture/reference-architectures/event-hubs/partitioning-in-event-hubs-and-kafka). Para aproveitar esse recurso, forneça a ID da partição que você deseja que receba os eventos. |

{style="table-layout:auto"}

**Dados**

| Entrada | Descrição |
| --- | --- |
| [!UICONTROL Payload] | Este campo contém os dados que serão encaminhados para o [!DNL Event Hubs]. Os dados podem ser um objeto JSON, uma string ou um elemento de dados. |

{style="table-layout:auto"}

Quando terminar, selecione **[!UICONTROL Keep Changes]** para adicionar a ação à configuração de regra. Quando estiver satisfeito com a regra, selecione **[!UICONTROL Save to Library]**.

Finalmente, publique um novo encaminhamento de eventos [build](../../../ui/publishing/builds.md) para habilitar as alterações na biblioteca.

## Próximas etapas

Este guia abordou como enviar dados para [!DNL Event Hubs] usando a extensão de encaminhamento de eventos [!DNL Microsoft Azure]. Para obter mais informações sobre os recursos de encaminhamento de eventos do Experience Platform, consulte a [visão geral do encaminhamento de eventos](../../../ui/event-forwarding/overview.md).

## Apêndice: Obtenção de valores de autorização SAS {#sas}

Os aplicativos externos recebem acesso a [!DNL Event Hubs] por meio de [assinaturas de acesso compartilhado (SAS)](https://learn.microsoft.com/en-us/azure/event-hubs/authorize-access-shared-access-signature). Cada namespace e instância do hub de eventos [!DNL Event Hubs] tem uma regra de autorização SAS padrão automaticamente atribuída na criação, mas você também pode criar políticas adicionais para cada recurso, se desejar.

Ao [configurar uma regra de encaminhamento de eventos](#rule) usando a extensão [!DNL Azure], você deve fornecer o nome e a chave primária da regra de autorização que rege o namespace ou o hub de eventos específico para o qual deseja enviar dados. Para obter detalhes sobre como obter esses valores do portal [!DNL Azure], consulte as seguintes seções na documentação do [!DNL Azure]:

* [Obter valores SAS para um [!DNL Event Hubs] namespace](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-get-connection-string#connection-string-for-a-namespace)
* [Obter valores SAS para um hub de eventos específico em um namespace](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-get-connection-string#connection-string-for-a-specific-event-hub-in-a-namespace)

Depois de ter os valores necessários, o nome da regra de autorização pode ser fornecido diretamente como uma string na entrada de configuração ou você pode criar um elemento de dados do tipo string para referenciá-lo. No entanto, a chave primária deve primeiro estar contida dentro de um segredo de encaminhamento de eventos para que possa ser fornecida na configuração de regras para proteger sua segurança de dados.

Na interface do usuário do encaminhamento de eventos, [crie um novo segredo](../../../ui/event-forwarding/secrets.md) e selecione **[!UICONTROL Token]** como o tipo de segredo. Para o próprio valor do token, forneça a chave primária copiada anteriormente. Depois de criar o segredo, crie um elemento de dados com o tipo **[!UICONTROL Secret]** e selecione o segredo [!DNL Event Hubs] na lista. Após configurar o elemento de dados secreto, você poderá referenciá-lo no campo **[!UICONTROL SAS Access Key]**.
