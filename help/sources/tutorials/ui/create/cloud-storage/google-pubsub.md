---
title: Criar uma conexão Google PubSub-fonte na interface do usuário
description: Saiba como criar um conector Google PubSub-source usando a interface do usuário da plataforma.
exl-id: fb8411f2-ccae-4bb5-b1bf-52b1144534ed
source-git-commit: f56cdc2dc67f2d4820d80d8e5bdec8306d852891
workflow-type: tm+mt
source-wordcount: '612'
ht-degree: 1%

---

# Crie um [!DNL Google PubSub] conexão de origem na interface do usuário

Este tutorial fornece etapas para criar um [!DNL Google PubSub] (a seguir designado por &quot;[!DNL PubSub]&quot;) usando a interface do usuário da plataforma.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Fontes](../../../../home.md): O Experience Platform permite que os dados sejam assimilados de várias fontes, fornecendo a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma.
* [Sandboxes](../../../../../sandboxes/home.md): O Experience Platform fornece sandboxes virtuais que particionam uma única instância da Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

Se você já tiver um [!DNL PubSub] , você pode ignorar o restante deste documento e prosseguir para o tutorial em [configuração de um fluxo de dados](../../dataflow/batch/cloud-storage.md).

### Obter credenciais necessárias

Para se conectar [!DNL PubSub] para a Platform, você deve fornecer um valor válido para as seguintes credenciais:

| Credencial | Descrição |
| ---------- | ----------- |
| Projeto ID | A ID do projeto necessária para autenticação [!DNL PubSub]. |
| Credenciais | A ID da credencial ou da chave privada necessária para a autenticação [!DNL PubSub]. |
| ID do tópico | A ID da variável [!DNL PubSub] que representa um feed de mensagens. Você deve especificar uma ID de tópico se desejar fornecer acesso a um fluxo específico de dados no [!DNL Google PubSub] fonte. |

Para obter mais informações sobre esses valores, consulte o seguinte [Autenticação PubSub](https://cloud.google.com/pubsub/docs/authentication) documento. Se você estiver usando a autenticação baseada em conta de serviço, consulte o seguinte [PubSub guide](https://cloud.google.com/docs/authentication/production#create_service_account) para obter etapas sobre como gerar suas credenciais.

>[!TIP]
>
>Se estiver usando a autenticação baseada em conta de serviço, certifique-se de ter concedido acesso suficiente ao usuário à sua conta de serviço e de não haver espaços em branco adicionais no JSON, ao copiar e colar suas credenciais.

Depois de reunir suas credenciais necessárias, siga as etapas abaixo para vincular seus [!DNL PubSub] para a Platform.

## Conecte seu [!DNL PubSub] account

Na interface do usuário da plataforma, selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar o [!UICONTROL Fontes] espaço de trabalho. O [!UICONTROL Catálogo] exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Em [!UICONTROL armazenamento na nuvem] categoria , selecione **[!UICONTROL Google PubSub]** e selecione **[!UICONTROL Adicionar dados]**.

![catálogo](../../../../images/tutorials/create/google-pubsub/catalog.png)

O **[!UICONTROL Conectar-se ao Google PubSub]** será exibida. Nesta página, você pode usar novas credenciais ou credenciais existentes.

### Conta existente

Para usar uma conta existente, selecione a [!DNL PubSub] conta com a qual deseja criar um novo fluxo de dados e selecione **[!UICONTROL Próximo]** para continuar.

![existente](../../../../images/tutorials/create/google-pubsub/existing.png)

### Nova conta

Se estiver criando uma nova conta, selecione **[!UICONTROL Nova conta]** e forneça um nome, uma descrição opcional e [!DNL PubSub] credenciais de autenticação no formulário de entrada. Durante essa etapa, é possível definir os dados aos quais sua conta tem acesso fornecendo uma ID de tópico. Somente as subscrições associadas à ID de tópico estarão acessíveis.

>[!NOTE]
>
>Os principais (funções) atribuídos a um projeto público são herdados em todos os tópicos e subscrições criados dentro de um [!DNL PubSub] projeto. Se você quiser adicionar um principal (função) para ter acesso a um tópico específico, esse principal (função) também deverá ser adicionado à assinatura correspondente do tópico. Para obter mais informações, leia a [[!DNL PubSub] documentação sobre o controle de acesso](https://cloud.google.com/pubsub/docs/access-control).

Quando terminar, selecione **[!UICONTROL Conectar-se à origem]** e, em seguida, permitir que a nova conexão seja estabelecida.

![novo](../../../../images/tutorials/create/google-pubsub/new.png)

## Próximas etapas

Ao seguir este tutorial, você cria uma conexão entre [!DNL PubSub] conta e plataforma. Agora você pode continuar para o próximo tutorial e [configure um fluxo de dados para trazer dados de fluxo do armazenamento em nuvem para a plataforma](../../dataflow/streaming/cloud-storage-streaming.md).
