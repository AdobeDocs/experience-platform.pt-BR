---
title: Criar uma conexão de origem Google PubSub na interface
description: Saiba como criar um conector de origem Google PubSub usando a interface do usuário da Platform.
exl-id: fb8411f2-ccae-4bb5-b1bf-52b1144534ed
source-git-commit: 2b72d384e8edd91c662364dfac31ce4edff79172
workflow-type: tm+mt
source-wordcount: '658'
ht-degree: 1%

---

# Criar um [!DNL Google PubSub] conexão de origem na interface

Este tutorial fornece etapas para a criação de um [!DNL Google PubSub] (a seguir designado por &quot;[!DNL PubSub]&quot;) usando a interface do usuário da Platform.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Origens](../../../../home.md): o Experience Platform permite que os dados sejam assimilados de várias fontes e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma.
* [Sandboxes](../../../../../sandboxes/home.md): o Experience Platform fornece sandboxes virtuais que particionam uma única instância da Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

Se você já tiver um [!DNL PubSub] conexão, você pode ignorar o restante deste documento e prosseguir para o tutorial em [configuração de um fluxo de dados](../../dataflow/batch/cloud-storage.md).

### Coletar credenciais necessárias

Para se conectar [!DNL PubSub] Para o Platform, você deve fornecer um valor válido para as seguintes credenciais:

| Credencial | Descrição |
| ---------- | ----------- |
| Projeto  ID | A ID do projeto necessária para a autenticação [!DNL PubSub]. |
| Credenciais | A ID da chave privada ou credencial necessária para autenticar [!DNL PubSub]. |
| ID do tópico | A ID para o [!DNL PubSub] recurso que representa um feed de mensagens. Você deve especificar uma ID de tópico se quiser fornecer acesso a um fluxo específico de dados em seu [!DNL Google PubSub] origem. |
| ID de assinatura | A ID do seu [!DNL PubSub] assinatura. Entrada [!DNL PubSub], assinaturas permitem que você receba mensagens inscrevendo-se no tópico no qual as mensagens foram publicadas. |

Para obter mais informações sobre esses valores, consulte o seguinte [Autenticação PubSub](https://cloud.google.com/pubsub/docs/authentication) documento. Se você estiver usando autenticação baseada em conta de serviço, consulte o seguinte [Guia PubSub](https://cloud.google.com/docs/authentication/production#create_service_account) para obter etapas sobre como gerar suas credenciais.

>[!TIP]
>
>Se estiver usando autenticação baseada em conta de serviço, verifique se você concedeu acesso de usuário suficiente à conta de serviço e se não há espaços em branco adicionais no JSON ao copiar e colar suas credenciais.

Depois de obter as credenciais necessárias, siga as etapas abaixo para vincular [!DNL PubSub] para a Platform.

## Conecte seu [!DNL PubSub] account

Na interface do usuário da Platform, selecione **[!UICONTROL Origens]** na barra de navegação esquerda, para acessar a [!UICONTROL Origens] espaço de trabalho. A variável [!UICONTROL Catálogo] exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

No [!UICONTROL armazenamento na nuvem] categoria, selecione **[!UICONTROL Google PubSub]** e selecione **[!UICONTROL Adicionar dados]**.

![O catálogo de fontes na interface do usuário do Experience Platform.](../../../../images/tutorials/create/google-pubsub/catalog.png)

A variável **[!UICONTROL Conectar-se ao Google PubSub]** é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Conta existente

Para usar uma conta existente, selecione a variável [!DNL PubSub] conta com a qual deseja criar um novo fluxo de dados e selecione **[!UICONTROL Próxima]** para continuar.

![A seleção de conta existente no fluxo de trabalho de códigos-fonte.](../../../../images/tutorials/create/google-pubsub/existing.png)

### Nova conta

Se estiver criando uma nova conta, selecione **[!UICONTROL Nova conta]** e forneça um nome, uma descrição opcional e suas [!DNL PubSub] credenciais de autenticação no formulário de entrada. Durante essa etapa, é possível definir os dados aos quais sua conta tem acesso fornecendo uma ID do tópico. Somente as assinaturas associadas a essa ID de tópico estarão acessíveis.

>[!NOTE]
>
>O Principal (funções) atribuído a um subprojeto Publish é herdado em todos os tópicos e assinaturas criadas dentro de um [!DNL PubSub] projeto. Se você quiser adicionar um principal (função) para ter acesso a um tópico específico, esse principal (função) também deverá ser adicionado à assinatura correspondente do tópico. Para obter mais informações, leia a [[!DNL PubSub] documentação sobre o controle de acesso](https://cloud.google.com/pubsub/docs/access-control).

Quando terminar, selecione **[!UICONTROL Conectar à origem]** e aguarde algum tempo para estabelecer a nova conexão.

![A nova interface de conta no workflow de origens.](../../../../images/tutorials/create/google-pubsub/new.png)

## Próximas etapas

Ao seguir este tutorial, você criará uma conexão entre suas [!DNL PubSub] conta e plataforma. Agora você pode seguir para o próximo tutorial e [configure um fluxo de dados para trazer dados de transmissão do armazenamento em nuvem para a Platform](../../dataflow/streaming/cloud-storage-streaming.md).
