---
keywords: Experience Platform, home, tópicos populares, Google PubSub, google pubsub
solution: Experience Platform
title: Criar uma conexão do Google PubSub-Source na interface do usuário
topic: overview
type: Tutorial
description: Saiba como criar um conector de origem Google PubSub usando a interface do usuário da plataforma.
translation-type: tm+mt
source-git-commit: b5358ce206888c413035b46fe751520fd9aefb14
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 1%

---


# Criar uma conexão de origem [!DNL Google PubSub] na interface do usuário

>[!NOTE]
>
> O conector [!DNL Google PubSub] está em beta. Consulte a [Visão geral das Fontes](../../../../home.md#terms-and-conditions) para obter mais informações sobre o uso de conectores com marca beta.

Este tutorial fornece etapas para criar um [!DNL Google PubSub] (a seguir chamado &quot;[!DNL PubSub]&quot;) usando a interface do usuário da plataforma.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Fontes](../../../../home.md): O Experience Platform permite que os dados sejam assimilados de várias fontes, fornecendo a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma.
* [Sandboxes](../../../../../sandboxes/home.md): O Experience Platform fornece sandboxes virtuais que particionam uma única instância da Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

Se você já tiver uma conexão válida [!DNL PubSub], poderá ignorar o restante deste documento e prosseguir para o tutorial em [configurar um fluxo de dados](../../dataflow/batch/cloud-storage.md).

### Obter credenciais necessárias

Para se conectar [!DNL PubSub] à Plataforma, você deve fornecer um valor válido para as seguintes credenciais:

| Credencial | Descrição |
| ---------- | ----------- |
| `projectId` | A ID do projeto necessária para autenticar [!DNL PubSub]. |
| `credentials` | A ID da credencial ou da chave privada necessária para autenticar [!DNL PubSub]. |

Para obter mais informações sobre esses valores, consulte o seguinte documento [PubSub authentication](https://cloud.google.com/pubsub/docs/authentication). Se você estiver usando a autenticação baseada em conta de serviço, consulte o [PubSub guide](https://cloud.google.com/docs/authentication/production#create_service_account) a seguir para obter as etapas sobre como gerar suas credenciais.

>[!TIP]
>
>Se estiver usando a autenticação baseada em conta de serviço, certifique-se de ter concedido acesso suficiente ao usuário à sua conta de serviço e de não haver espaços em branco adicionais no JSON, ao copiar e colar suas credenciais.

Depois de reunir suas credenciais necessárias, siga as etapas abaixo para vincular sua conta [!DNL PubSub] à Platform.

## Conecte sua conta [!DNL PubSub]

Na [Interface do usuário da plataforma](https://platform.adobe.com), selecione **[!UICONTROL Sources]** na barra de navegação esquerda para acessar o espaço de trabalho [!UICONTROL Sources]. A tela [!UICONTROL Catalog] exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a barra de pesquisa.

Na categoria [!UICONTROL Cloud storage], selecione **[!UICONTROL Google PubSub]** e selecione **[!UICONTROL Add data]**.

![catálogo](../../../../images/tutorials/create/google-pubsub/catalog.png)

A página **[!UICONTROL Connect to Google PubSub]** é exibida. Nesta página, você pode usar novas credenciais ou credenciais existentes.

### Conta existente

Para usar uma conta existente, selecione a conta [!DNL PubSub] com a qual deseja criar um novo fluxo de dados e selecione **[!UICONTROL Next]** para prosseguir.

![existente](../../../../images/tutorials/create/google-pubsub/existing.png)

### Nova conta

Se estiver criando uma nova conta, selecione **[!UICONTROL New account]** e forneça um nome, uma descrição opcional e suas credenciais de autenticação [!DNL PubSub] no formulário de entrada. Quando terminar, selecione **[!UICONTROL Connect to source]** e aguarde algum tempo para que a nova conexão seja estabelecida.

![novo](../../../../images/tutorials/create/google-pubsub/new.png)

## Próximas etapas

Ao seguir este tutorial, você cria uma conexão entre sua conta [!DNL PubSub] e a Plataforma. Agora você pode continuar para o próximo tutorial e [configurar um fluxo de dados para trazer dados de fluxo do armazenamento em nuvem para a Platform](../../dataflow/streaming/cloud-storage-streaming.md).
