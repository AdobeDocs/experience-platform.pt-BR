---
title: Visão geral da extensão do AWS
description: Saiba mais sobre a extensão AWS para encaminhamento de eventos no Adobe Experience Platform.
exl-id: 826a96aa-2d64-4a8b-88cf-34a0b6c26df5
last-substantial-update: 2022-11-23T00:00:00Z
source-git-commit: 1c417744518a7ac7cfb9c65d6af8219dcbc70d46
workflow-type: tm+mt
source-wordcount: '841'
ht-degree: 4%

---

# [!DNL AWS] visão geral da extensão

>[!NOTE]
>
>A Adobe Experience Platform Launch foi reformulada como um conjunto de tecnologias de coleta de dados no Adobe Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](../../../term-updates.md) para obter uma referência consolidada das alterações de terminologia.

[[!DNL Amazon Web Services] ([!DNL AWS])](https://aws.amazon.com/) é uma plataforma de computação em nuvem que oferece uma grande variedade de serviços, como computação distribuída, armazenamento de banco de dados, entrega de conteúdo e serviços de integração de software como um serviço (SaaS) para gerenciamento de relacionamento com o cliente (CRM) e ERP (Enterprise Resource Planning, planejamento de recursos corporativos).

O [!DNL AWS] [encaminhamento de eventos](../../../ui/event-forwarding/overview.md) aproveitadores de extensão [[!DNL Amazon Kinesis Data Streams]](https://docs.aws.amazon.com/streams/latest/dev/introduction.html) para enviar eventos da rede de borda da Adobe Experience Platform para o [!DNL AWS] para transformação subsequente. Este guia aborda como instalar a extensão e empregar seus recursos em uma regra de encaminhamento de eventos.

## Pré-requisitos

Você deve ter um [!DNL AWS] com uma conta existente [!DNL Kinesis] fluxo de dados para usar essa extensão. Se você não tiver um fluxo de dados pré-existente, consulte o [!DNL AWS] documentação sobre [criar um novo fluxo de dados usando o [!DNL AWS] Console de gerenciamento](https://docs.aws.amazon.com/streams/latest/dev/how-do-i-create-a-stream.html).

## Instalar a extensão {#install}

Para instalar o [!DNL AWS] , navegue até a interface do usuário da coleta de dados ou a interface do usuário do Experience Platform e selecione **[!UICONTROL Encaminhamento de evento]** no painel de navegação esquerdo. Aqui, selecione uma propriedade para adicionar a extensão ou crie uma nova propriedade.

Após selecionar ou criar a propriedade desejada, selecione **[!UICONTROL Extensões]** na navegação à esquerda, selecione o **[!UICONTROL Catálogo]** guia . Procure a variável [!UICONTROL AWS] cartão e, em seguida, selecione **[!UICONTROL Instalar]**.

![O [!UICONTROL Instalar] botão que está sendo selecionado para o [!UICONTROL AWS] na interface do usuário da Coleta de dados.](../../../images/extensions/server/aws/install.png)

Na próxima tela, você deve fornecer as credenciais de conexão para [!DNL AWS] conta. Especificamente, você deve fornecer seu [!DNL AWS] a ID da chave de acesso e a chave de acesso secreta. Se não souber esses valores, consulte a [!DNL AWS] documentação sobre [como obter a ID da chave de acesso e a chave de acesso secreta](https://docs.aws.amazon.com/powershell/latest/userguide/pstools-appendix-sign-up.html).

![A ID da chave de acesso e a chave de acesso secreta adicionadas na exibição de configuração da extensão.](../../../images/extensions/server/aws/credentials.png)

>[!IMPORTANT]
>
>É necessário anexar uma política de acesso à [!DNL AWS] conta usada para gerar as credenciais de acesso. Essa política deve ser configurada para conceder direitos de acesso para enviar dados para o [!DNL Kinesis] fluxo de dados. Consulte **Exemplo 2** no [!DNL AWS] documento em [políticas de exemplo para [!DNL Kinesis Data Streams]](https://docs.aws.amazon.com/streams/latest/dev/controlling-access.html#kinesis-using-iam-examples) para ver como a política deve ser definida.

Quando terminar, selecione **[!UICONTROL Salvar]** e a extensão é instalada.

## Configurar uma regra de encaminhamento de eventos {#rule}

Depois de instalar a extensão, crie um novo encaminhamento de evento [regra](../../../ui/managing-resources/rules.md) e configure as condições conforme desejado. Ao configurar as ações para a regra, selecione o **[!UICONTROL AWS]** e selecione **[!UICONTROL Enviar dados para o fluxo de dados do Kinesis]** para o tipo de ação.

![O [!UICONTROL Enviar dados para o fluxo de dados do Kinesis] tipo de ação sendo selecionado para uma regra na interface do usuário da Coleta de dados.](../../../images/extensions/server/aws/select-action-type.png)

O painel direito é atualizado para mostrar as opções de configuração de como os dados devem ser enviados. Especificamente, você deve atribuir [elementos de dados](../../../ui/managing-resources/data-elements.md) para as várias propriedades que representam as [!DNL Event Hub] configuração.

![As opções de configuração do [!UICONTROL Enviar dados para o fluxo de dados do Kinesis] tipo de ação mostrado na interface do usuário.](../../../images/extensions/server/aws/data-stream-details.png)

**[!UICONTROL Detalhes do fluxo de dados do Kinesis]**

| Entrada | Descrição |
| --- | --- |
| [!UICONTROL Nome do fluxo] | O nome do fluxo para o qual essa regra de encaminhamento de eventos enviará registros de dados. |
| [!UICONTROL AWS Region] | O [!DNL AWS] região em que [!DNL Kinesis] fluxo de dados é criado. |
| [!UICONTROL Chave de Partição] | O [chave de partição](https://docs.aws.amazon.com/streams/latest/dev/key-concepts.html#partition-key) que a extensão usará ao enviar dados para o fluxo de dados.<br><br>[!DNL Kinesis Data Streams] segrega os registros de dados pertencentes a um fluxo em vários fragmentos. Ele usa a chave de partição enviada com cada registro de dados para determinar a qual compartilhamento um determinado registro de dados pertence.<br><br>Uma boa chave de partição para distribuir clientes pode ser o número do cliente, já que é diferente para cada cliente. Uma chave de partição ruim pode ter o CEP, pois todos podem viver na mesma área próxima. Em geral, você deve escolher uma chave de partição que tenha o maior intervalo de valores em potencial diferentes. Consulte a [!DNL AWS] artigo sobre [dimensionamento de [!DNL Kinesis] fluxos de dados](https://aws.amazon.com/blogs/big-data/under-the-hood-scaling-your-kinesis-data-streams/) para obter as práticas recomendadas de gerenciamento de chaves de partição. |

{style="table-layout:auto"}

**[!UICONTROL Dados]**

| Entrada | Descrição |
| --- | --- |
| [!UICONTROL Carga] | Esse campo contém os dados que serão encaminhados para a variável [!DNL Kinesis] fluxo de dados, no formato JSON.<br><br>Em **[!UICONTROL Bruto]** , você pode colar o objeto JSON diretamente no campo de texto fornecido ou pode selecionar o ícone do elemento de dados (![Ícone do conjunto de dados](../../../images/extensions/server/aws/data-element-icon.png)) para selecionar de uma lista de elementos de dados existentes para representar a carga útil.<br><br>Também é possível usar a variável **[!UICONTROL Editor de pares de valores-chave JSON]** para adicionar manualmente cada par de valores chave por meio de um editor de interface. Cada valor pode ser representado por uma entrada bruta, ou um elemento de dados pode ser selecionado. |

{style="table-layout:auto"}

Quando terminar, selecione **[!UICONTROL Manter alterações]** para adicionar a ação à configuração da regra. Quando estiver satisfeito com a regra, selecione **[!UICONTROL Salvar na biblioteca]**.

Finalmente, publique um novo encaminhamento de evento [build](../../../ui/publishing/builds.md) para ativar as alterações na biblioteca.

## Próximas etapas

Este guia cobriu como enviar dados para o [!DNL Kinesis Data Streams] usando o [!DNL AWS] extensão de encaminhamento de evento. Para obter mais informações sobre os recursos de encaminhamento de eventos no Experience Platform, consulte o [visão geral do encaminhamento de eventos](../../../ui/event-forwarding/overview.md).
