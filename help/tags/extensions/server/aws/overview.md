---
title: Visão geral da extensão do AWS
description: Saiba mais sobre a extensão do AWS para encaminhamento de eventos no Adobe Experience Platform.
exl-id: 826a96aa-2d64-4a8b-88cf-34a0b6c26df5
last-substantial-update: 2022-11-23T00:00:00Z
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 0%

---

# Visão geral da extensão do [!DNL AWS]

[[!DNL Amazon Web Services] ([!DNL AWS])](https://aws.amazon.com/) é uma plataforma de computação em nuvem que oferece uma grande variedade de serviços, como computação distribuída, armazenamento de banco de dados, entrega de conteúdo e serviços de integração de software como um serviço (SaaS) para CRM (gerenciamento de relacionamento com o cliente) e ERP (planejamento de recursos da empresa).

A extensão [!DNL AWS] [encaminhamento de eventos](../../../ui/event-forwarding/overview.md) aproveita [[!DNL Amazon Kinesis Data Streams]](https://docs.aws.amazon.com/streams/latest/dev/introduction.html) para enviar eventos do Adobe Experience Platform Edge Network para [!DNL AWS] para processamento adicional. Este guia aborda como instalar a extensão e empregar seus recursos em uma regra de encaminhamento de eventos.

## Pré-requisitos

Você deve ter uma conta [!DNL AWS] com um fluxo de dados [!DNL Kinesis] existente para usar esta extensão. Se você não tiver um fluxo de dados pré-existente, consulte a documentação do [!DNL AWS] sobre [criação de um novo fluxo de dados usando o [!DNL AWS] Console de Gerenciamento](https://docs.aws.amazon.com/streams/latest/dev/how-do-i-create-a-stream.html).

## Instalar a extensão {#install}

Para instalar a extensão [!DNL AWS], navegue até a interface da Coleção de Dados ou a interface do Experience Platform e selecione **[!UICONTROL Event Forwarding]** na navegação à esquerda. Aqui, selecione uma propriedade à qual adicionar a extensão ou crie uma nova propriedade.

Depois de selecionar ou criar a propriedade desejada, selecione **[!UICONTROL Extensions]** na navegação à esquerda e, em seguida, selecione a guia **[!UICONTROL Catalog]**. Procure o cartão [!UICONTROL AWS] e selecione **[!UICONTROL Install]**.

![O botão [!UICONTROL Install] que está sendo selecionado para a extensão [!UICONTROL AWS] na interface da Coleção de Dados.](../../../images/extensions/server/aws/install.png)

Na próxima tela, você deve fornecer as credenciais de conexão para sua conta do [!DNL AWS]. Você deve fornecer sua ID de chave de acesso e chave de acesso secreta do [!DNL AWS]. Se você não souber esses valores, consulte a documentação do [!DNL AWS] sobre [como obter a ID da chave de acesso e a chave de acesso secreta](https://docs.aws.amazon.com/powershell/latest/userguide/pstools-appendix-sign-up.html).

![A ID da chave de acesso e a chave de acesso secreta adicionadas na exibição de configuração da extensão.](../../../images/extensions/server/aws/credentials.png)

>[!IMPORTANT]
>
>É necessário anexar uma política de acesso à conta [!DNL AWS] usada para gerar as credenciais de acesso. Esta política deve ser configurada para conceder direitos de acesso para enviar dados ao fluxo de dados [!DNL Kinesis]. Consulte **Exemplo 2** no documento [!DNL AWS] sobre [políticas de exemplo para [!DNL Kinesis Data Streams]](https://docs.aws.amazon.com/streams/latest/dev/controlling-access.html#kinesis-using-iam-examples) para ver como a política deve ser definida.

Quando terminar, selecione **[!UICONTROL Save]** e a extensão será instalada.

## Configurar uma regra de encaminhamento de eventos {#rule}

Após instalar a extensão, crie uma nova [regra](../../../ui/managing-resources/rules.md) para o encaminhamento de eventos e configure suas condições conforme desejado. Ao configurar as ações para a regra, selecione a extensão **[!UICONTROL AWS]** e selecione **[!UICONTROL Send Data to Kinesis Data Stream]** para o tipo de ação.

![O tipo de ação [!UICONTROL Send Data to Kinesis Data Stream] que está sendo selecionado para uma regra na interface da Coleção de Dados.](../../../images/extensions/server/aws/select-action-type.png)

O painel direito atualiza para mostrar as opções de configuração de como os dados devem ser enviados. Você deve atribuir [elementos de dados](../../../ui/managing-resources/data-elements.md) às várias propriedades que representam sua configuração [!DNL Event Hub].

![As opções de configuração para o tipo de ação [!UICONTROL Send Data to Kinesis Data Stream] mostradas na interface do usuário.](../../../images/extensions/server/aws/data-stream-details.png)

**[!UICONTROL Kinesis Data Stream Details]**

| Entrada | Descrição |
| --- | --- |
| [!UICONTROL Stream Name] | O nome do fluxo para o qual esta regra de encaminhamento de eventos enviará registros de dados. |
| [!UICONTROL AWS Region] | A região [!DNL AWS] onde o fluxo de dados [!DNL Kinesis] é criado. |
| [!UICONTROL Partition Key] | A [chave de partição](https://docs.aws.amazon.com/streams/latest/dev/key-concepts.html#partition-key) que a extensão usará ao enviar dados para o fluxo de dados.<br><br>[!DNL Kinesis Data Streams] separa os registros de dados pertencentes a um fluxo em vários fragmentos. Ele usa a chave de partição enviada com cada registro de dados para determinar a qual fragmento um determinado registro de dados pertence.<br><br>Uma boa chave de partição para distribuir clientes pode ser o número do cliente, pois ele é diferente para cada cliente. Uma chave de partição ruim pode ter o código postal porque todos eles podem viver na mesma área nas proximidades. Em geral, você deve escolher uma chave de partição que tenha o intervalo mais alto de diferentes valores em potencial. Consulte o artigo [!DNL AWS] sobre [dimensionamento de  [!DNL Kinesis] fluxos de dados](https://aws.amazon.com/blogs/big-data/under-the-hood-scaling-your-kinesis-data-streams/) para obter as práticas recomendadas sobre o gerenciamento de chaves de partição. |

{style="table-layout:auto"}

**[!UICONTROL Data]**

| Entrada | Descrição |
| --- | --- |
| [!UICONTROL Payload] | Este campo contém os dados que serão encaminhados para o fluxo de dados [!DNL Kinesis], no formato JSON.<br><br>Na opção **[!UICONTROL Raw]**, você pode colar o objeto JSON diretamente no campo de texto fornecido ou selecionar o ícone de elemento de dados (![ícone de Conjunto de Dados](/help/images/icons/database.png)) para selecionar de uma lista de elementos de dados existentes para representar a carga.<br><br>Você também pode usar a opção **[!UICONTROL JSON Key-Value Pairs Editor]** para adicionar manualmente cada par de valor-chave por meio de um editor de interface. Cada valor pode ser representado por uma entrada bruta, ou um elemento de dados pode ser selecionado. |

{style="table-layout:auto"}

Quando terminar, selecione **[!UICONTROL Keep Changes]** para adicionar a ação à configuração de regra. Quando estiver satisfeito com a regra, selecione **[!UICONTROL Save to Library]**.

Finalmente, publique um novo encaminhamento de eventos [build](../../../ui/publishing/builds.md) para habilitar as alterações na biblioteca.

## Próximas etapas

Este guia abordou como enviar dados para [!DNL Kinesis Data Streams] usando a extensão de encaminhamento de eventos [!DNL AWS]. Para obter mais informações sobre os recursos de encaminhamento de eventos do Experience Platform, consulte a [visão geral do encaminhamento de eventos](../../../ui/event-forwarding/overview.md).
