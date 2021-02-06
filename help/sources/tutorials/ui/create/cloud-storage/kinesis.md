---
keywords: Experience Platform;lar;tópicos populares;Amazon Kinesis;amazon cinesis;Kinesis;cinesis
solution: Experience Platform
title: Criar uma conexão de origem Amazon Kinesis na interface do usuário
topic: overview
type: Tutorial
description: Saiba como criar uma conexão de origem Amazon Kinesis usando a interface do usuário Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: c7fb0d50761fa53c1fdf4dd70a63c62f2dcf6c85
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 1%

---


# Criar uma conexão de origem [!DNL Amazon Kinesis] na interface do usuário

>[!NOTE]
>
>O conector [!DNL Amazon Kinesis] está em beta. Consulte a [Visão geral das fontes](../../../../home.md#terms-and-conditions) para obter mais informações sobre o uso de conectores marcados com beta.

Os conectores de origem na Adobe Experience Platform fornecem a capacidade de assimilar dados de origem externa de forma programada. Este tutorial fornece etapas para autenticação de um [!DNL Amazon Kinesis] (a seguir denominado [!DNL "Kinesis"]) conector de origem usando a interface do usuário [!DNL Platform].

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): A estrutura padronizada pela qual  [!DNL Experience Platform] organiza os dados de experiência do cliente.
   - [Noções básicas da composição](../../../../../xdm/schema/composition.md) do schema: Saiba mais sobre os elementos básicos dos schemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   - [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md) do Editor de schemas: Saiba como criar schemas personalizados usando a interface do editor de Schemas.
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.

Se você já tiver uma conexão válida [!DNL Kinesis], poderá ignorar o restante desse documento e prosseguir para o tutorial em [configurar um fluxo de dados](../../dataflow/streaming/cloud-storage-streaming.md).

### Reunir credenciais obrigatórias

Para autenticar seu conector de origem [!DNL Kinesis], você deve fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| `accessKeyId` | A ID da chave de acesso para sua conta [!DNL Kinesis]. |
| `Secret access key` | A chave de acesso secreta para sua conta [!DNL Kinesis]. |
| `region` | A região do servidor AWS. |

Para obter mais informações sobre esses valores, consulte [this [!DNL Kinesis] documento](https://docs.aws.amazon.com/streams/latest/dev/getting-started.html).

## Conectar sua conta [!DNL Kinesis]

Depois de reunir as credenciais necessárias, siga as etapas abaixo para vincular sua conta [!DNL Kinesis] a [!DNL Platform].

Faça logon em [Adobe Experience Platform](https://platform.adobe.com) e selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar a área de trabalho **[!UICONTROL Fontes]**. A tela **[!UICONTROL Catalog]** exibe várias fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Na categoria **[!UICONTROL Armazenamento de nuvem]**, selecione **[!UICONTROL Amazon Kinesis]**. Se esta for a sua primeira vez usando este conector, selecione **[!UICONTROL Configurar]**. Caso contrário, selecione **[!UICONTROL Adicionar dados]** para criar um novo conector [!DNL Kinesis].

![](../../../../images/tutorials/create/kinesis/catalog.png)

A caixa de diálogo **[!UICONTROL Conectar-se ao Amazon Kinesis]** é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Nova conta

Se você estiver usando novas credenciais, selecione **[!UICONTROL Nova conta]**. No formulário de entrada exibido, forneça um nome, uma descrição opcional e suas credenciais [!DNL Kinesis]. Quando terminar, selecione **[!UICONTROL Connect]** e aguarde algum tempo para a nova conexão ser estabelecida.

![](../../../../images/tutorials/create/kinesis/new.png)

### Conta existente

Para conectar uma conta existente, selecione a conta [!DNL Kinesis] com a qual você deseja se conectar e selecione **[!UICONTROL Próximo]** para prosseguir.

![](../../../../images/tutorials/create/kinesis/existing.png)

## Próximas etapas

Ao seguir este tutorial, você se conectou à sua conta [!DNL Kinesis] a [!DNL Platform]. Agora você pode continuar para o próximo tutorial e [configurar um fluxo de dados para trazer dados do seu armazenamento em nuvem para [!DNL Platform]](../../dataflow/streaming/cloud-storage-streaming.md).