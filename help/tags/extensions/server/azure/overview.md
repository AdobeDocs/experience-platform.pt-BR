---
title: Visão geral da extensão do Microsoft Azure
description: Saiba mais sobre a extensão do Microsoft Azure para encaminhamento de eventos no Adobe Experience Platform.
exl-id: 2337d99d-861e-44e7-94ed-ba21ef28d815
source-git-commit: f6c11fadc0d8019044fbdd2923af00ce18ce39e1
workflow-type: tm+mt
source-wordcount: '931'
ht-degree: 3%

---

# [!DNL Microsoft Azure] visão geral da extensão

>[!NOTE]
>
>O Adobe Experience Platform Launch foi reformulado como um conjunto de tecnologias de coleção de dados na Adobe Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](../../../term-updates.md) para obter uma referência consolidada das alterações de terminologia.

Entrada [!DNL Microsoft Azure], [[!DNL Event Hubs]](https://azure.microsoft.com/en-us/products/event-hubs/#overview) O é um serviço de entrada de dados em tempo real altamente escalável que permite processar e analisar as grandes quantidades de dados produzidas pelos dispositivos e aplicativos conectados. Depois que os dados são coletados em um hub de eventos, eles podem ser transformados e armazenados usando qualquer provedor de análise em tempo real ou adaptadores de armazenamento/em lote.

A variável [!DNL Microsoft Azure] [encaminhamento de eventos](../../../ui/event-forwarding/overview.md) aproveitamentos de extensão [!DNL Event Hubs] para enviar eventos da Rede de borda da Adobe Experience Platform para [!DNL Azure] para processamento posterior. Este guia aborda como instalar a extensão e empregar seus recursos em uma regra de encaminhamento de eventos.

## Pré-requisitos

Para usar essa extensão, você deve ter uma [!DNL Azure] conta com acesso a [!DNL Event Hubs]. Você também deve [criar um hub de eventos usando o [!DNL Azure] portal](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create) antes de seguir as etapas abaixo.

## Instalar a extensão

Para instalar o Microsoft [!DNL Azure] , navegue até a interface da Coleção de dados ou a interface do Experience Platform e selecione **[!UICONTROL Encaminhamento de evento]** no painel de navegação esquerdo. Aqui, selecione uma propriedade à qual adicionar a extensão ou crie uma nova propriedade.

Depois de selecionar ou criar a propriedade desejada, selecione **[!UICONTROL Extensões]** na navegação à esquerda, selecione o **[!UICONTROL Catálogo]** guia. Procure por [!UICONTROL Microsoft Azure] e selecione **[!UICONTROL Instalar]**.

![A variável [!UICONTROL Instalar] botão que está sendo selecionado para o [!UICONTROL Microsoft Azure] na interface da Coleção de dados.](../../../images/extensions/server/azure/install.png)

Como a extensão não tem propriedades de configuração, ela é adicionada imediatamente à lista de extensões instaladas. Agora você pode começar a usar o [!DNL Event Hub] tipos de ação ao configurar regras de encaminhamento de eventos.

## Configurar uma regra de encaminhamento de eventos {#rule}

Comece a criar uma nova regra de encaminhamento de eventos e configure as condições conforme desejado. Ao selecionar as ações para a regra, selecione **[!UICONTROL Microsoft Azure]** para a extensão e selecione **[!UICONTROL Enviar dados para os Hubs de eventos]** para o tipo de ação.

![A variável [!UICONTROL Enviar dados para os Hubs de eventos] tipo de ação que está sendo selecionado para uma regra na interface da Coleção de dados.](../../../images/extensions/server/azure/select-action-type.png)

O painel direito atualiza para mostrar as opções de configuração de como os dados devem ser enviados. Você deve atribuir [elementos de dados](../../../ui/managing-resources/data-elements.md) para as várias propriedades que representam a [!DNL Event Hub] configuração.

![As opções de configuração para a variável [!UICONTROL Enviar dados para os Hubs de eventos] tipo de ação mostrado na interface do usuário.](../../../images/extensions/server/azure/event-hub-details.png)

**[!UICONTROL Detalhes do Hub de Eventos]**

| Entrada | Descrição |
| --- | --- |
| [!UICONTROL Namespace] | O nome do [!DNL Event Hubs] namespace que você criou quando [configuração do hub de eventos](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace). |
| [!UICONTROL Nome] | O nome do hub de eventos. |
| [!UICONTROL Nome da Regra de Autorização SAS] | O nome da regra de autorização de acesso compartilhado para todo o [!DNL Event Hubs] ou a instância do hub de eventos específico para a qual você deseja enviar dados. Consulte a seção do apêndice sobre [obtenção de valores de autorização SAS](#sas) para obter mais informações. |
| [!UICONTROL Chave de Acesso SAS] | A chave primária da regra de autorização de acesso compartilhado para todo o [!DNL Event Hubs] ou a instância do hub de eventos específico para a qual você deseja enviar dados. Consulte a seção do apêndice sobre [obtenção de valores de autorização SAS](#sas) para obter mais informações. |
| [!UICONTROL ID da Partição] | [!DNL Event Hubs] permite que você [enviar eventos diretamente para partições específicas](https://learn.microsoft.com/en-us/azure/architecture/reference-architectures/event-hubs/partitioning-in-event-hubs-and-kafka). Para aproveitar esse recurso, forneça a ID da partição que você deseja que receba os eventos. |

{style="table-layout:auto"}

**Dados**

| Entrada | Descrição |
| --- | --- |
| [!UICONTROL Carga] | Este campo contém os dados que serão encaminhados para a [!DNL Event Hubs]. Os dados podem ser um objeto JSON, uma string ou um elemento de dados. |

{style="table-layout:auto"}

Quando terminar, selecione **[!UICONTROL Manter alterações]** para adicionar a ação à configuração de regra. Quando estiver satisfeito com a regra, selecione **[!UICONTROL Salvar na biblioteca]**.

Por fim, publique um novo encaminhamento de eventos [build](../../../ui/publishing/builds.md) para ativar as alterações na biblioteca.

## Próximas etapas

Este guia abordou como enviar dados para o [!DNL Event Hubs] usando o [!DNL Microsoft Azure] extensão de encaminhamento de eventos. Para obter mais informações sobre os recursos de encaminhamento de eventos no Experience Platform, consulte [visão geral do encaminhamento de eventos](../../../ui/event-forwarding/overview.md).

## Apêndice: Obtenção de valores de autorização SAS {#sas}

Os aplicativos externos recebem acesso ao [!DNL Event Hubs] até [assinaturas de acesso compartilhado (SAS)](https://learn.microsoft.com/en-us/azure/event-hubs/authorize-access-shared-access-signature). Each [!DNL Event Hubs] A instância do hub de eventos e namespaces tem uma regra de autorização SAS padrão atribuída automaticamente na criação, mas você também pode criar políticas adicionais para cada recurso, se desejar.

Quando [configurar uma regra de encaminhamento de eventos](#rule) usando o [!DNL Azure] , você deve fornecer o nome e a chave primária para a regra de autorização que rege o namespace ou hub de eventos específico para o qual deseja enviar dados. Para obter detalhes sobre como obter esses valores do [!DNL Azure] portal, consulte as seguintes seções no [!DNL Azure] documentação:

* [Obter valores SAS para um [!DNL Event Hubs] namespace](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-get-connection-string#connection-string-for-a-namespace)
* [Obter valores SAS para um hub de eventos específico em um namespace](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-get-connection-string#connection-string-for-a-specific-event-hub-in-a-namespace)

Depois de ter os valores necessários, o nome da regra de autorização pode ser fornecido diretamente como uma string na entrada de configuração ou você pode criar um elemento de dados do tipo string para referenciá-lo. No entanto, a chave primária deve primeiro estar contida dentro de um segredo de encaminhamento de eventos para que possa ser fornecida na configuração de regras para proteger sua segurança de dados.

Na interface do usuário do encaminhamento de eventos, [criar um novo segredo](../../../ui/event-forwarding/secrets.md) e selecione **[!UICONTROL Token]** como o tipo secreto. Para o próprio valor do token, forneça a chave primária copiada anteriormente. Depois de criar o segredo, crie um elemento de dados com o tipo **[!UICONTROL Segredo]** e selecione o [!DNL Event Hubs] segredo da lista. Após configurar o elemento de dados secreto, você poderá referenciá-lo na variável **[!UICONTROL Chave de Acesso SAS]** campo.
