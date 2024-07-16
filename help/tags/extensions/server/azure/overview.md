---
title: Visão geral da extensão do Microsoft Azure
description: Saiba mais sobre a extensão do Microsoft Azure para encaminhamento de eventos no Adobe Experience Platform.
exl-id: 2337d99d-861e-44e7-94ed-ba21ef28d815
last-substantial-update: 2022-11-23T00:00:00Z
source-git-commit: 1c417744518a7ac7cfb9c65d6af8219dcbc70d46
workflow-type: tm+mt
source-wordcount: '891'
ht-degree: 4%

---

# Visão geral da extensão do [!DNL Microsoft Azure]

>[!NOTE]
>
>O Adobe Experience Platform Launch foi reformulado como um conjunto de tecnologias de coleção de dados na Adobe Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](../../../term-updates.md) para obter uma referência consolidada das alterações de terminologia.

No [!DNL Microsoft Azure], o [[!DNL Event Hubs]](https://azure.microsoft.com/en-us/products/event-hubs/#overview) é um serviço de entrada de dados em tempo real altamente escalável que permite processar e analisar as grandes quantidades de dados produzidas pelos seus dispositivos e aplicativos conectados. Depois que os dados são coletados em um hub de eventos, eles podem ser transformados e armazenados usando qualquer provedor de análise em tempo real ou adaptadores de armazenamento/em lote.

A extensão [!DNL Microsoft Azure] [encaminhamento de eventos](../../../ui/event-forwarding/overview.md) aproveita [!DNL Event Hubs] para enviar eventos do Edge Network Adobe Experience Platform para [!DNL Azure] para processamento adicional. Este guia aborda como instalar a extensão e empregar seus recursos em uma regra de encaminhamento de eventos.

## Pré-requisitos

Para usar essa extensão, você deve ter uma conta válida do [!DNL Azure] com acesso ao [!DNL Event Hubs]. Você também deve [criar um hub de eventos usando o [!DNL Azure] portal](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create) antes de seguir as etapas abaixo.

## Instalar a extensão

Para instalar a extensão [!DNL Azure] do Microsoft, navegue até a interface da Coleção de dados ou a interface do Experience Platform e selecione **[!UICONTROL Encaminhamento de eventos]** na navegação à esquerda. Aqui, selecione uma propriedade à qual adicionar a extensão ou crie uma nova propriedade.

Depois de selecionar ou criar a propriedade desejada, selecione **[!UICONTROL Extensões]** na navegação à esquerda e selecione a guia **[!UICONTROL Catálogo]**. Procure o cartão [!UICONTROL Microsoft Azure] e selecione **[!UICONTROL Instalar]**.

![O botão [!UICONTROL Instalar] sendo selecionado para a extensão do [!UICONTROL Microsoft Azure] na interface da Coleção de Dados.](../../../images/extensions/server/azure/install.png)

Como a extensão não tem propriedades de configuração, ela é adicionada imediatamente à lista de extensões instaladas. Agora você pode começar a usar os tipos de ação [!DNL Event Hub] ao configurar as regras de encaminhamento de eventos.

## Configurar uma regra de encaminhamento de eventos {#rule}

Comece a criar uma nova regra de encaminhamento de eventos e configure as condições conforme desejado. Ao selecionar as ações para a regra, selecione **[!UICONTROL Microsoft Azure]** para a extensão e **[!UICONTROL Enviar Dados para os Hubs de Eventos]** para o tipo de ação.

![O tipo de ação [!UICONTROL Enviar Dados para os Hubs de Eventos] que está sendo selecionado para uma regra na Interface da Coleção de Dados.](../../../images/extensions/server/azure/select-action-type.png)

O painel direito atualiza para mostrar as opções de configuração de como os dados devem ser enviados. Você deve atribuir [elementos de dados](../../../ui/managing-resources/data-elements.md) às várias propriedades que representam sua configuração [!DNL Event Hub].

![As opções de configuração do tipo de ação [!UICONTROL Enviar Dados para os Hubs de Eventos] mostradas na interface do usuário.](../../../images/extensions/server/azure/event-hub-details.png)

**[!UICONTROL Detalhes do Hub de Eventos]**

| Entrada | Descrição |
| --- | --- |
| [!UICONTROL Namespace] | O nome do namespace [!DNL Event Hubs] que você criou ao [configurar o hub de eventos](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace). |
| [!UICONTROL Nome] | O nome do hub de eventos. |
| [!UICONTROL Nome da Regra de Autorização SAS] | O nome da regra de autorização de acesso compartilhado para todo o namespace [!DNL Event Hubs] ou a instância do hub de eventos específica para a qual você deseja enviar dados. Consulte a seção do apêndice sobre [obtenção de valores de autorização SAS](#sas) para obter mais informações. |
| [!UICONTROL Chave de Acesso SAS] | A chave primária da regra de autorização de acesso compartilhado para todo o namespace [!DNL Event Hubs] ou a instância do hub de eventos específico para a qual você deseja enviar dados. Consulte a seção do apêndice sobre [obtenção de valores de autorização SAS](#sas) para obter mais informações. |
| [!UICONTROL ID da Partição] | [!DNL Event Hubs] permite [enviar eventos diretamente para partições específicas](https://learn.microsoft.com/en-us/azure/architecture/reference-architectures/event-hubs/partitioning-in-event-hubs-and-kafka). Para aproveitar esse recurso, forneça a ID da partição que você deseja que receba os eventos. |

{style="table-layout:auto"}

**Dados**

| Entrada | Descrição |
| --- | --- |
| [!UICONTROL Carga] | Este campo contém os dados que serão encaminhados para o [!DNL Event Hubs]. Os dados podem ser um objeto JSON, uma string ou um elemento de dados. |

{style="table-layout:auto"}

Quando terminar, selecione **[!UICONTROL Manter alterações]** para adicionar a ação à configuração de regra. Quando estiver satisfeito com a regra, selecione **[!UICONTROL Salvar na biblioteca]**.

Finalmente, publique um novo encaminhamento de eventos [build](../../../ui/publishing/builds.md) para habilitar as alterações na biblioteca.

## Próximas etapas

Este guia abordou como enviar dados para [!DNL Event Hubs] usando a extensão de encaminhamento de eventos [!DNL Microsoft Azure]. Para obter mais informações sobre os recursos de encaminhamento de eventos do Experience Platform, consulte a [visão geral do encaminhamento de eventos](../../../ui/event-forwarding/overview.md).

## Apêndice: Obtenção de valores de autorização SAS {#sas}

Os aplicativos externos recebem acesso a [!DNL Event Hubs] por meio de [assinaturas de acesso compartilhado (SAS)](https://learn.microsoft.com/en-us/azure/event-hubs/authorize-access-shared-access-signature). Cada namespace e instância do hub de eventos [!DNL Event Hubs] tem uma regra de autorização SAS padrão automaticamente atribuída na criação, mas você também pode criar políticas adicionais para cada recurso, se desejar.

Ao [configurar uma regra de encaminhamento de eventos](#rule) usando a extensão [!DNL Azure], você deve fornecer o nome e a chave primária da regra de autorização que rege o namespace ou o hub de eventos específico para o qual deseja enviar dados. Para obter detalhes sobre como obter esses valores do portal [!DNL Azure], consulte as seguintes seções na documentação do [!DNL Azure]:

* [Obter valores SAS para um [!DNL Event Hubs] namespace](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-get-connection-string#connection-string-for-a-namespace)
* [Obter valores SAS para um hub de eventos específico em um namespace](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-get-connection-string#connection-string-for-a-specific-event-hub-in-a-namespace)

Depois de ter os valores necessários, o nome da regra de autorização pode ser fornecido diretamente como uma string na entrada de configuração ou você pode criar um elemento de dados do tipo string para referenciá-lo. No entanto, a chave primária deve primeiro estar contida dentro de um segredo de encaminhamento de eventos para que possa ser fornecida na configuração de regras para proteger sua segurança de dados.

Na interface do usuário do encaminhamento de eventos, [crie um novo segredo](../../../ui/event-forwarding/secrets.md) e selecione **[!UICONTROL Token]** como o tipo de segredo. Para o próprio valor do token, forneça a chave primária copiada anteriormente. Depois de criar o segredo, crie um elemento de dados do tipo **[!UICONTROL Segredo]** e selecione o segredo [!DNL Event Hubs] na lista. Depois que o elemento de dados secreto for configurado, você poderá referenciá-lo no campo **[!UICONTROL Chave de Acesso SAS]**.
