---
keywords: Experience Platform, home, tópicos populares, Amazon Kinesis, amazon cinesis, Kinesis, cinesis
solution: Experience Platform
title: Criar uma conexão de origem Kinesis do Amazon na interface do usuário
type: Tutorial
description: Saiba como criar uma conexão de origem do Amazon Kinesis usando a interface do usuário do Adobe Experience Platform.
exl-id: 4152e48b-bec7-4b05-a172-eea71c9d9880
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 1%

---

# Crie um [!DNL Amazon Kinesis] conexão de origem na interface do usuário

Os conectores de origem no Adobe Experience Platform oferecem a capacidade de assimilar dados de origem externa de acordo com a programação. Este tutorial fornece etapas para a autenticação de um [!DNL Amazon Kinesis] (a seguir designada [!DNL "Kinesis"]) conector de origem usando o [!DNL Platform] interface do usuário.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): O quadro normalizado pelo qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
   - [Noções básicas da composição do schema](../../../../../xdm/schema/composition.md): Saiba mais sobre os elementos básicos dos esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   - [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Fornece um perfil de consumidor unificado e em tempo real com base em dados agregados de várias fontes.

Se você já tiver um [!DNL Kinesis] , você pode ignorar o restante deste documento e prosseguir para o tutorial em [configuração de um fluxo de dados](../../dataflow/streaming/cloud-storage-streaming.md).

### Obter credenciais necessárias

Para autenticar seu [!DNL Kinesis] conector de origem, você deve fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| `accessKeyId` | A ID da chave de acesso para sua [!DNL Kinesis] conta. |
| `Secret access key` | A chave de acesso secreta para sua [!DNL Kinesis] conta. |
| `region` | A região do seu servidor AWS. |

Para obter mais informações sobre esses valores, consulte [this [!DNL Kinesis] documento](https://docs.aws.amazon.com/streams/latest/dev/getting-started.html).

## Conecte seu [!DNL Kinesis] account

Depois de reunir suas credenciais necessárias, siga as etapas abaixo para vincular seus [!DNL Kinesis] para [!DNL Platform].

Faça logon em [Adobe Experience Platform](https://platform.adobe.com) e depois selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar o **[!UICONTROL Fontes]** espaço de trabalho. O **[!UICONTROL Catálogo]** exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Em **[!UICONTROL Armazenamento na nuvem]** categoria , selecione **[!UICONTROL Amazon Kinesis]**. Se esta for a primeira vez que você usa esse conector, selecione **[!UICONTROL Configurar]**. Caso contrário, selecione **[!UICONTROL Adicionar dados]** para criar um novo [!DNL Kinesis] conector.

![](../../../../images/tutorials/create/kinesis/catalog.png)

O **[!UICONTROL Conectar-se ao Amazon Kinesis]** será exibida. Nesta página, você pode usar novas credenciais ou credenciais existentes.

### Nova conta

Se estiver usando novas credenciais, selecione **[!UICONTROL Nova conta]**. No formulário de entrada exibido, forneça um nome, uma descrição opcional e [!DNL Kinesis] credenciais. Quando terminar, selecione **[!UICONTROL Connect]** e, em seguida, permitir que a nova conexão seja estabelecida.

![](../../../../images/tutorials/create/kinesis/new.png)

### Conta existente

Para conectar uma conta existente, selecione a [!DNL Kinesis] conta com a qual deseja se conectar e selecione **[!UICONTROL Próximo]** para continuar.

![](../../../../images/tutorials/create/kinesis/existing.png)

## Próximas etapas

Ao seguir este tutorial, você se conectou ao [!DNL Kinesis] para [!DNL Platform]. Agora você pode continuar para o próximo tutorial e [configure um fluxo de dados para trazer dados do armazenamento na nuvem para [!DNL Platform]](../../dataflow/streaming/cloud-storage-streaming.md).
