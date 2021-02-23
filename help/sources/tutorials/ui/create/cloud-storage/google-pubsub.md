---
keywords: Experience Platform;home;popular topics;Google PubSub;google pubsub
solution: Experience Platform
title: Criar uma conexão de subfonte do Google na interface do usuário
topic: visão geral
type: Tutorial
description: Saiba como criar um conector do Google PubSub-source usando a interface do usuário da plataforma.
translation-type: tm+mt
source-git-commit: 0af90253f04377149986aedf2e9d3012ca06d4f8
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 1%

---


# Criar uma conexão de origem [!DNL Google PubSub] na interface do usuário

>[!NOTE]
>
> O conector [!DNL Google PubSub] está em beta. Consulte a [Visão geral das fontes](../../../../home.md#terms-and-conditions) para obter mais informações sobre o uso de conectores marcados com beta.

Este tutorial fornece etapas para criar um [!DNL Google PubSub] (a seguir denominado &quot;[!DNL PubSub]&quot;) usando a interface do usuário da plataforma.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Fontes](../../../../home.md): O Experience Platform permite que os dados sejam assimilados de várias fontes, ao mesmo tempo em que lhe fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma.
* [Caixas de proteção](../../../../../sandboxes/home.md): O Experience Platform fornece caixas de proteção virtuais que particionam uma única instância da Plataforma em ambientes virtuais separados para ajudar a desenvolver e desenvolver aplicativos de experiência digital.

Se você já tiver uma conexão válida [!DNL PubSub], poderá ignorar o restante desse documento e prosseguir para o tutorial em [configurar um fluxo de dados](../../dataflow/batch/cloud-storage.md).

### Reunir credenciais obrigatórias

Para conectar [!DNL PubSub] à Plataforma, é necessário fornecer um valor válido para a seguinte credencial:

| Credencial | Descrição |
| ---------- | ----------- |
| `projectId` | A ID do projeto necessária para autenticar [!DNL PubSub]. |
| `credentials` | A credencial ou chave necessária para autenticar [!DNL PubSub]. |

Para obter mais informações sobre esses valores, consulte o seguinte documento [PubSub authentication](https://cloud.google.com/pubsub/docs/authentication).

Depois de reunir as credenciais necessárias, siga as etapas abaixo para vincular sua conta [!DNL Blob] à Plataforma.

## Conectar sua conta [!DNL PubSub]

Na [Interface do usuário da plataforma](https://platform.adobe.com), selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar a área de trabalho [!UICONTROL Fontes]. A tela [!UICONTROL Catalog] exibe várias fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a barra de pesquisa.

Na categoria [!UICONTROL armazenamento em nuvem], selecione **[!UICONTROL Google PubSub]** e selecione **[!UICONTROL Adicionar dados]**.

![catálogo](../../../../images/tutorials/create/google-pubsub/catalog.png)

A página **[!UICONTROL Conectar-se ao Google PubSub]** é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Conta existente

Para usar uma conta existente, selecione a conta [!DNL PubSub] com a qual deseja criar um novo fluxo de dados e selecione **[!UICONTROL Próximo]** para continuar.

![existente](../../../../images/tutorials/create/google-pubsub/existing.png)

### Nova conta

Se estiver criando uma nova conta, selecione **[!UICONTROL Nova conta]** e forneça um nome, uma descrição opcional e suas credenciais de autenticação [!DNL PubSub] no formulário de entrada. Quando terminar, selecione **[!UICONTROL Ligar à origem]** e, em seguida, aguarde algum tempo para que a nova ligação seja estabelecida.

![new](../../../../images/tutorials/create/google-pubsub/new.png)

## Próximas etapas

Ao seguir este tutorial, você cria uma conexão entre sua conta [!DNL PubSub] e a Plataforma. Agora você pode continuar para o próximo tutorial e [configurar um fluxo de dados para trazer dados de fluxo contínuo do seu armazenamento em nuvem para a Plataforma](../../dataflow/streaming/cloud-storage-streaming.md).
