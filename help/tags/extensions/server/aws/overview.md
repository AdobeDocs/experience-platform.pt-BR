---
title: Visão geral da extensão do AWS
description: Saiba mais sobre a extensão do AWS para encaminhamento de eventos no Adobe Experience Platform.
exl-id: 826a96aa-2d64-4a8b-88cf-34a0b6c26df5
source-git-commit: b4ff3dbc9c62dceefdf2b842cafa65132dde41fc
workflow-type: tm+mt
source-wordcount: '841'
ht-degree: 4%

---

# [!DNL AWS] visão geral da extensão

>[!NOTE]
>
>O Adobe Experience Platform Launch foi reformulado como um conjunto de tecnologias de coleção de dados na Adobe Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](../../../term-updates.md) para obter uma referência consolidada das alterações de terminologia.

[[!DNL Amazon Web Services] ([!DNL AWS])](https://aws.amazon.com/) O é uma plataforma de computação em nuvem que oferece uma grande variedade de serviços, como computação distribuída, armazenamento de banco de dados, entrega de conteúdo e serviços de integração de software como um serviço (SaaS) para gerenciamento de relacionamento com o cliente (CRM) e planejamento de recursos corporativos (ERP).

A variável [!DNL AWS] [encaminhamento de eventos](../../../ui/event-forwarding/overview.md) aproveitamentos de extensão [[!DNL Amazon Kinesis Data Streams]](https://docs.aws.amazon.com/streams/latest/dev/introduction.html) para enviar eventos da Rede de borda da Adobe Experience Platform para [!DNL AWS] para processamento posterior. Este guia aborda como instalar a extensão e empregar seus recursos em uma regra de encaminhamento de eventos.

## Pré-requisitos

Você deve ter um [!DNL AWS] conta com um existente [!DNL Kinesis] fluxo de dados para usar essa extensão. Se você não tiver um fluxo de dados pré-existente, consulte a [!DNL AWS] documentação sobre [criação de um novo fluxo de dados usando o [!DNL AWS] Console de gerenciamento](https://docs.aws.amazon.com/streams/latest/dev/how-do-i-create-a-stream.html).

## Instalar a extensão {#install}

Para instalar o [!DNL AWS] , navegue até a interface da Coleção de dados ou a interface do Experience Platform e selecione **[!UICONTROL Encaminhamento de evento]** no painel de navegação esquerdo. Aqui, selecione uma propriedade à qual adicionar a extensão ou crie uma nova propriedade.

Depois de selecionar ou criar a propriedade desejada, selecione **[!UICONTROL Extensões]** na navegação à esquerda, selecione o **[!UICONTROL Catálogo]** guia. Procure por [!UICONTROL AWS] e selecione **[!UICONTROL Instalar]**.

![A variável [!UICONTROL Instalar] botão que está sendo selecionado para o [!UICONTROL AWS] na interface da Coleção de dados.](../../../images/extensions/server/aws/install.png)

Na próxima tela, você deve fornecer as credenciais de conexão para o [!DNL AWS] conta. Você deve fornecer suas [!DNL AWS] ID e chave de acesso secreta. Se você não souber esses valores, consulte a [!DNL AWS] documentação sobre [como obter a ID da chave de acesso e a chave de acesso secreta](https://docs.aws.amazon.com/powershell/latest/userguide/pstools-appendix-sign-up.html).

![A ID da chave de acesso e a chave de acesso secreta foram adicionadas na visualização de configuração da extensão.](../../../images/extensions/server/aws/credentials.png)

>[!IMPORTANT]
>
>É necessário anexar uma política de acesso ao [!DNL AWS] conta usada para gerar as credenciais de acesso. Essa política deve ser configurada para conceder direitos de acesso para enviar dados ao [!DNL Kinesis] fluxo de dados. Consulte **Exemplo 2** no [!DNL AWS] documento ativado [exemplo de políticas para [!DNL Kinesis Data Streams]](https://docs.aws.amazon.com/streams/latest/dev/controlling-access.html#kinesis-using-iam-examples) para ver como a política deve ser definida.

Quando terminar, selecione **[!UICONTROL Salvar]** e a extensão estiver instalada.

## Configurar uma regra de encaminhamento de eventos {#rule}

Depois de instalar a extensão, crie um novo encaminhamento de eventos [regra](../../../ui/managing-resources/rules.md) e configure suas condições conforme desejado. Ao configurar as ações para a regra, selecione a variável **[!UICONTROL AWS]** e selecione **[!UICONTROL Enviar dados para o fluxo de dados do Kinesis]** para o tipo de ação.

![A variável [!UICONTROL Enviar dados para o fluxo de dados do Kinesis] tipo de ação que está sendo selecionado para uma regra na interface da Coleção de dados.](../../../images/extensions/server/aws/select-action-type.png)

O painel direito atualiza para mostrar as opções de configuração de como os dados devem ser enviados. Você deve atribuir [elementos de dados](../../../ui/managing-resources/data-elements.md) para as várias propriedades que representam a [!DNL Event Hub] configuração.

![As opções de configuração para a variável [!UICONTROL Enviar dados para o fluxo de dados do Kinesis] tipo de ação mostrado na interface do usuário.](../../../images/extensions/server/aws/data-stream-details.png)

**[!UICONTROL Detalhes do fluxo de dados do Kinesis]**

| Entrada | Descrição |
| --- | --- |
| [!UICONTROL Nome do fluxo] | O nome do fluxo para o qual esta regra de encaminhamento de eventos enviará registros de dados. |
| [!UICONTROL AWS Region] | A variável [!DNL AWS] região em que o [!DNL Kinesis] fluxo de dados é criado. |
| [!UICONTROL Chave de Partição] | A variável [chave de partição](https://docs.aws.amazon.com/streams/latest/dev/key-concepts.html#partition-key) que a extensão usará ao enviar dados para o fluxo de dados.<br><br>[!DNL Kinesis Data Streams] separa os registros de dados pertencentes a um fluxo em vários fragmentos. Ele usa a chave de partição enviada com cada registro de dados para determinar a qual fragmento um determinado registro de dados pertence.<br><br>Uma boa chave de partição para distribuir clientes pode ser o número do cliente, já que é diferente para cada cliente. Uma chave de partição ruim pode ter o código postal porque todos eles podem viver na mesma área nas proximidades. Em geral, você deve escolher uma chave de partição que tenha o intervalo mais alto de diferentes valores em potencial. Consulte a [!DNL AWS] artigo sobre [dimensionamento do [!DNL Kinesis] fluxos de dados](https://aws.amazon.com/blogs/big-data/under-the-hood-scaling-your-kinesis-data-streams/) para obter as práticas recomendadas sobre o gerenciamento de chaves de partição. |

{style="table-layout:auto"}

**[!UICONTROL Dados]**

| Entrada | Descrição |
| --- | --- |
| [!UICONTROL Carga] | Este campo contém os dados que serão encaminhados para a [!DNL Kinesis] fluxo de dados, no formato JSON.<br><br>No **[!UICONTROL Brutos]** , você pode colar o objeto JSON diretamente no campo de texto fornecido ou selecionar o ícone de elemento de dados (![Ícone de conjunto de dados](../../../images/extensions/server/aws/data-element-icon.png)) para selecionar de uma lista de elementos de dados existentes para representar a carga.<br><br>Você também pode usar a variável **[!UICONTROL Editor de pares de valor-chave JSON]** opção para adicionar manualmente cada par de valor-chave por meio de um editor de interface do usuário. Cada valor pode ser representado por uma entrada bruta, ou um elemento de dados pode ser selecionado. |

{style="table-layout:auto"}

Quando terminar, selecione **[!UICONTROL Manter alterações]** para adicionar a ação à configuração de regra. Quando estiver satisfeito com a regra, selecione **[!UICONTROL Salvar na biblioteca]**.

Por fim, publique um novo encaminhamento de eventos [build](../../../ui/publishing/builds.md) para ativar as alterações na biblioteca.

## Próximas etapas

Este guia abordou como enviar dados para o [!DNL Kinesis Data Streams] usando o [!DNL AWS] extensão de encaminhamento de eventos. Para obter mais informações sobre os recursos de encaminhamento de eventos no Experience Platform, consulte [visão geral do encaminhamento de eventos](../../../ui/event-forwarding/overview.md).
