---
title: Visão geral da extensão do Microsoft Azure
description: Saiba mais sobre a extensão do Microsoft Azure para encaminhamento de eventos no Adobe Experience Platform.
exl-id: 2337d99d-861e-44e7-94ed-ba21ef28d815
last-substantial-update: 2022-11-23T00:00:00Z
source-git-commit: 1c417744518a7ac7cfb9c65d6af8219dcbc70d46
workflow-type: tm+mt
source-wordcount: '931'
ht-degree: 3%

---

# [!DNL Microsoft Azure] visão geral da extensão

>[!NOTE]
>
>A Adobe Experience Platform Launch foi reformulada como um conjunto de tecnologias de coleta de dados no Adobe Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](../../../term-updates.md) para obter uma referência consolidada das alterações de terminologia.

Em [!DNL Microsoft Azure], [[!DNL Event Hubs]](https://azure.microsoft.com/en-us/products/event-hubs/#overview) O é um serviço de entrada de dados altamente escalável e em tempo real que permite processar e analisar a grande quantidade de dados produzidos pelos seus dispositivos e aplicativos conectados. Depois que os dados são coletados em um hub de eventos, eles podem ser transformados e armazenados usando qualquer provedor de análise em tempo real ou adaptadores de armazenamento/agrupamento.

O [!DNL Microsoft Azure] [encaminhamento de eventos](../../../ui/event-forwarding/overview.md) aproveitadores de extensão [!DNL Event Hubs] para enviar eventos da rede de borda da Adobe Experience Platform para o [!DNL Azure] para transformação subsequente. Este guia aborda como instalar a extensão e empregar seus recursos em uma regra de encaminhamento de eventos.

## Pré-requisitos

Para usar essa extensão, você deve ter um [!DNL Azure] com acesso a [!DNL Event Hubs]. Você também deve [crie um hub de eventos usando o [!DNL Azure] portal](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create) antes de seguir as etapas abaixo.

## Instalar a extensão

Para instalar o Microsoft [!DNL Azure] , navegue até a interface do usuário da coleta de dados ou a interface do usuário do Experience Platform e selecione **[!UICONTROL Encaminhamento de evento]** no painel de navegação esquerdo. Aqui, selecione uma propriedade para adicionar a extensão ou crie uma nova propriedade.

Após selecionar ou criar a propriedade desejada, selecione **[!UICONTROL Extensões]** na navegação à esquerda, selecione o **[!UICONTROL Catálogo]** guia . Procure a variável [!UICONTROL Microsoft Azure] cartão e, em seguida, selecione **[!UICONTROL Instalar]**.

![O [!UICONTROL Instalar] botão que está sendo selecionado para o [!UICONTROL Microsoft Azure] na interface do usuário da Coleta de dados.](../../../images/extensions/server/azure/install.png)

Como a extensão não tem propriedades de configuração, ela é adicionada imediatamente à lista de extensões instaladas. Agora você pode começar a usar [!DNL Event Hub] tipos de ação ao configurar regras de encaminhamento de eventos.

## Configurar uma regra de encaminhamento de eventos {#rule}

Comece criando uma nova regra de encaminhamento de eventos e configure suas condições conforme desejado. Ao selecionar as ações para a regra, selecione **[!UICONTROL Microsoft Azure]** para a extensão e selecione **[!UICONTROL Enviar dados para Hubs de evento]** para o tipo de ação .

![O [!UICONTROL Enviar dados para Hubs de evento] tipo de ação sendo selecionado para uma regra na interface do usuário da Coleta de dados.](../../../images/extensions/server/azure/select-action-type.png)

O painel direito é atualizado para mostrar as opções de configuração de como os dados devem ser enviados. Especificamente, você deve atribuir [elementos de dados](../../../ui/managing-resources/data-elements.md) para as várias propriedades que representam as [!DNL Event Hub] configuração.

![As opções de configuração do [!UICONTROL Enviar dados para Hubs de evento] tipo de ação mostrado na interface do usuário.](../../../images/extensions/server/azure/event-hub-details.png)

**[!UICONTROL Detalhes do Hub de eventos]**

| Entrada | Descrição |
| --- | --- |
| [!UICONTROL Namespace] | O nome do [!DNL Event Hubs] namespace criado ao [configurar o hub de eventos](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-create#create-an-event-hubs-namespace). |
| [!UICONTROL Nome] | O nome do hub de eventos. |
| [!UICONTROL Nome da Regra de Autorização SAS] | O nome da regra de autorização de acesso compartilhado para todo o [!DNL Event Hubs] namespace ou a instância do hub de evento específico para a qual você deseja enviar dados. Consulte a seção do apêndice em [obtendo valores de autorização SAS](#sas) para obter mais informações. |
| [!UICONTROL Chave de acesso SAS] | A chave primária da regra de autorização de acesso compartilhado para todo o [!DNL Event Hubs] namespace ou a instância do hub de evento específico para a qual você deseja enviar dados. Consulte a seção do apêndice em [obtendo valores de autorização SAS](#sas) para obter mais informações. |
| [!UICONTROL ID da partição] | [!DNL Event Hubs] permite [enviar eventos diretamente para partições específicas](https://learn.microsoft.com/en-us/azure/architecture/reference-architectures/event-hubs/partitioning-in-event-hubs-and-kafka). Para aproveitar esse recurso, forneça a ID da partição que você deseja que receba os eventos. |

{style="table-layout:auto"}

**Dados**

| Entrada | Descrição |
| --- | --- |
| [!UICONTROL Carga] | Esse campo contém os dados que serão encaminhados para a variável [!DNL Event Hubs]. Os dados podem ser um objeto JSON, uma string ou um elemento de dados. |

{style="table-layout:auto"}

Quando terminar, selecione **[!UICONTROL Manter alterações]** para adicionar a ação à configuração da regra. Quando estiver satisfeito com a regra, selecione **[!UICONTROL Salvar na biblioteca]**.

Finalmente, publique um novo encaminhamento de evento [build](../../../ui/publishing/builds.md) para ativar as alterações na biblioteca.

## Próximas etapas

Este guia cobriu como enviar dados para o [!DNL Event Hubs] usando o [!DNL Microsoft Azure] extensão de encaminhamento de evento. Para obter mais informações sobre os recursos de encaminhamento de eventos no Experience Platform, consulte o [visão geral do encaminhamento de eventos](../../../ui/event-forwarding/overview.md).

## Apêndice: Obter valores de autorização SAS {#sas}

Os pedidos externos recebem acesso a [!DNL Event Hubs] through [assinaturas de acesso compartilhado (SAS)](https://learn.microsoft.com/en-us/azure/event-hubs/authorize-access-shared-access-signature). Cada [!DNL Event Hubs] o namespace e a instância do hub de eventos têm uma regra de autorização SAS padrão atribuída automaticamente na criação, mas você também pode criar políticas adicionais para cada recurso, se desejar.

When [configuração de uma regra de encaminhamento de eventos](#rule) usando o [!DNL Azure] , você deve fornecer o nome e a chave primária para a regra de autorização que rege o namespace ou o hub de evento específico para o qual deseja enviar dados. Para obter detalhes sobre como obter esses valores da variável [!DNL Azure] , consulte as seguintes seções na [!DNL Azure] documentação:

* [Obter valores SAS para um [!DNL Event Hubs] namespace](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-get-connection-string#connection-string-for-a-namespace)
* [Obter valores SAS para um hub de evento específico em um namespace](https://learn.microsoft.com/en-us/azure/event-hubs/event-hubs-get-connection-string#connection-string-for-a-specific-event-hub-in-a-namespace)

Depois de ter os valores obrigatórios, o nome da regra de autorização pode ser fornecido diretamente como uma string na entrada de configuração ou você pode criar um elemento de dados do tipo string para referenciá-la. A chave primária, no entanto, deve primeiro estar contida em um segredo de encaminhamento de evento antes de ser fornecida na configuração da regra para proteger sua segurança de dados.

Na interface do usuário de encaminhamento do evento, [criar um novo segredo](../../../ui/event-forwarding/secrets.md) e selecione **[!UICONTROL Token]** como o tipo secreto. Para o próprio valor do token, forneça a chave primária copiada anteriormente. Depois de criar o segredo, crie um elemento de dados com o tipo **[!UICONTROL Segredo]** e selecione o [!DNL Event Hubs] segredo da lista. Depois que o elemento de dados secreto for configurado, você poderá fazer referência a esse elemento de dados no **[!UICONTROL Chave de acesso SAS]** campo.
