---
title: Criar uma conexão de origem Google PubSub na interface
description: Saiba como criar um conector de origem Google PubSub usando a interface do usuário da Platform.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: fb8411f2-ccae-4bb5-b1bf-52b1144534ed
source-git-commit: b157b9147d8ea8100bcaedca272b303a3c04e71a
workflow-type: tm+mt
source-wordcount: '1043'
ht-degree: 1%

---

# Criar um [!DNL Google PubSub] conexão de origem na interface

>[!IMPORTANT]
>
>A variável [!DNL Google PubSub] origem está disponível no catálogo de origens para usuários que compraram o Real-time Customer Data Platform Ultimate.

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
| Credenciais | A credencial necessária para autenticar [!DNL PubSub]. Certifique-se de colocar o arquivo JSON completo após remover os espaços em branco de suas credenciais. |
| Nome do tópico | O nome do seu [!DNL PubSub] assinatura. Entrada [!DNL PubSub], assinaturas permitem que você receba mensagens inscrevendo-se no tópico no qual as mensagens foram publicadas. **Nota**: Uma única [!DNL PubSub] a assinatura só pode ser usada para um fluxo de dados. Para fazer vários fluxos de dados, você deve ter várias assinaturas. |
| Nome da assinatura | O nome do seu [!DNL PubSub] assinatura. Entrada [!DNL PubSub], assinaturas permitem que você receba mensagens inscrevendo-se no tópico no qual as mensagens foram publicadas. |

Para obter mais informações sobre esses valores, consulte o seguinte [Autenticação PubSub](https://cloud.google.com/pubsub/docs/authentication) documento. Se você estiver usando autenticação baseada em conta de serviço, consulte o seguinte [Guia PubSub](https://cloud.google.com/docs/authentication/production#create_service_account) para obter etapas sobre como gerar suas credenciais.

>[!TIP]
>
>Se estiver usando autenticação baseada em conta de serviço, verifique se você concedeu acesso de usuário suficiente à conta de serviço e se não há espaços em branco adicionais no JSON ao copiar e colar suas credenciais.

Depois de obter as credenciais necessárias, siga as etapas abaixo para vincular [!DNL PubSub] para a Platform.

## Conecte seu [!DNL PubSub] account

Na interface do usuário da Platform, selecione **[!UICONTROL Origens]** na navegação à esquerda, para acessar a [!UICONTROL Origens] espaço de trabalho. A variável [!UICONTROL Catálogo] exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

No [!UICONTROL armazenamento na nuvem] categoria, selecione **[!UICONTROL Google PubSub]** e selecione **[!UICONTROL Adicionar dados]**.

![O catálogo de fontes na interface do usuário do Experience Platform.](../../../../images/tutorials/create/google-pubsub/catalog.png)

A variável **[!UICONTROL Conectar-se ao Google PubSub]** é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Conta existente

Para usar uma conta existente, selecione a variável [!DNL PubSub] conta com a qual deseja criar um novo fluxo de dados e selecione **[!UICONTROL Próxima]** para continuar.

![A seleção de conta existente no fluxo de trabalho de códigos-fonte.](../../../../images/tutorials/create/google-pubsub/existing.png)

### Nova conta

>[!TIP]
>
>Ao criar uma conta com acesso restrito, você deve fornecer pelo menos um dos nomes do tópico ou da assinatura. A autenticação falhará se ambos os valores estiverem ausentes.

Se estiver criando uma nova conta, selecione **[!UICONTROL Nova conta]** e forneça um nome e uma descrição opcional para o novo [!DNL PubSub] conta.

![A nova interface de conta para a origem Google PubSub no fluxo de trabalho de origens](../../../../images/tutorials/create/google-pubsub/new.png)

A variável [!DNL PubSub] source permite especificar o tipo de acesso que você deseja permitir durante a autenticação. Você pode configurar sua conta para ter autenticação baseada em projeto ou autenticação baseada em tópico e assinatura. A autenticação baseada em projeto permite conceder acesso ao projeto de nível raiz em sua conta, enquanto a autenticação baseada em tópico e assinatura permite restringir o acesso a um específico [!DNL PubSub] tópico e assinatura.

>[!BEGINTABS]

>[!TAB Autenticação baseada em projeto]

Para criar uma conta com acesso à raiz [!DNL PubSub] pasta do projeto. Selecionar **[!UICONTROL Credenciais de autenticação do Google PubSub]** como tipo de autenticação e forneça a ID do projeto e as credenciais. Quando terminar, selecione **[!UICONTROL Conectar à origem]** e aguarde algum tempo para estabelecer a nova conexão.

![A nova interface de conta para a origem Google PubSub com acesso raiz selecionado.](../../../../images/tutorials/create/google-pubsub/root.png)

>[!TAB Tópico e autenticação por assinatura]

Para criar uma conta com acesso restrito apenas a um [!DNL PubSub] tópico e assinatura, selecione **[!UICONTROL Credenciais de autenticação do Google PubSub Scoped]** e forneça suas credenciais, nome do tópico e/ou nome da assinatura. Quando terminar, selecione **[!UICONTROL Conectar à origem]** e aguarde algum tempo para estabelecer a nova conexão.

![A nova interface de conta para a origem Google PubSub com acesso com escopo selecionado.](../../../../images/tutorials/create/google-pubsub/scoped.png)

>[!ENDTABS]

>[!NOTE]
>
>Principal (funções) atribuído a um [!DNL PubSub] projetos são herdados em todos os tópicos e assinaturas criadas dentro de um [!DNL PubSub] projeto. Se você quiser que um principal (função) tenha acesso a um tópico específico, esse principal (função) também deverá ser adicionado à assinatura correspondente do tópico. Para obter mais informações, leia a [[!DNL PubSub] documentação sobre o controle de acesso](<https://cloud.google.com/pubsub/docs/access-control>).

## Selecionar dados

Uma autenticação bem-sucedida leva você ao [!UICONTROL Selecionar dados] etapa, onde você pode navegar pelos seus [!DNL PubSub] hierarquia de dados e selecione os dados que deseja trazer para o Experience Platform.

>[!BEGINTABS]

>[!TAB Autenticação baseada em projeto]

Se você tiver autenticado com acesso baseado em projeto, a variável [!UICONTROL Selecionar dados] A interface do exibirá todas as assinaturas do projeto que tenham um tópico anexado a elas.

![A etapa de seleção de dados do fluxo de trabalho de fontes com autenticação baseada em projeto.](../../../../images/tutorials/create/google-pubsub/root-folders.png)

>[!TAB Tópico e autenticação por assinatura]

Se você tiver autenticado com um tópico e acesso baseado em assinatura, a variável [!UICONTROL Selecionar dados] A exibição da interface do pode variar dependendo das informações fornecidas.

* Se você fornecer apenas o nome do tópico, a interface exibirá todos os pares de assinatura de tópico que correspondem ao tópico fornecido.
* Se você fornecer apenas o nome da subscrição, a interface exibirá todos os pares de topic-subscription que correspondem ao nome da subscrição fornecido.
* Se os nomes do tópico e da assinatura forem fornecidos, a interface exibirá o par topic-subscription que corresponde a ambos os valores fornecidos.

![A etapa de seleção de dados do fluxo de trabalho de fontes com autenticação baseada em tópico e assinatura.](../../../../images/tutorials/create/google-pubsub/scoped-folders.png)

>[!ENDTABS]

## Próximas etapas

Ao seguir este tutorial, você criou uma conexão entre suas [!DNL PubSub] conta e plataforma. Agora você pode seguir para o próximo tutorial e [configure um fluxo de dados para trazer dados de transmissão do armazenamento em nuvem para a Platform](../../dataflow/streaming/cloud-storage-streaming.md).
