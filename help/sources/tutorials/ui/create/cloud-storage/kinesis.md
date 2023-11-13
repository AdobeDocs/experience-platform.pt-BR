---
title: Criar uma conexão de origem do Amazon Kinesis na interface
description: Saiba como criar uma conexão de origem do Amazon Kinesis usando a interface do usuário do Adobe Experience Platform.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 4152e48b-bec7-4b05-a172-eea71c9d9880
source-git-commit: 9a8139c26b5bb5ff937a51986967b57db58aab6c
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 1%

---

# Criar um [!DNL Amazon Kinesis] conexão de origem na interface

>[!IMPORTANT]
>
>A variável [!DNL Amazon Kinesis] origem está disponível no catálogo de origens para usuários que compraram o Real-time Customer Data Platform Ultimate.

Os conectores de origem no Adobe Experience Platform fornecem a capacidade de assimilar dados originados externamente de forma programada. Este tutorial fornece etapas para autenticar um [!DNL Amazon Kinesis] (a seguir designado [!DNL "Kinesis"]) de origem usando o [!DNL Platform] interface do usuário.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): o quadro normalizado pelo qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
   - [Noções básicas da composição do esquema](../../../../../xdm/schema/composition.md): saiba mais sobre os componentes básicos dos esquemas XDM, incluindo princípios fundamentais e práticas recomendadas na composição do esquema.
   - [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.

Se você já tiver um [!DNL Kinesis] conexão, você pode ignorar o restante deste documento e prosseguir para o tutorial em [configuração de um fluxo de dados](../../dataflow/streaming/cloud-storage-streaming.md).

### Coletar credenciais necessárias

Para autenticar seu [!DNL Kinesis] conector de origem, você deve fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| `accessKeyId` | A ID da chave de acesso do [!DNL Kinesis] conta. |
| `Secret access key` | A chave de acesso secreta para seu [!DNL Kinesis] conta. |
| `region` | A região do servidor do AWS. |

Para obter mais informações sobre esses valores, consulte [este [!DNL Kinesis] documento](https://docs.aws.amazon.com/streams/latest/dev/getting-started.html).

## Conecte seu [!DNL Kinesis] account

Depois de obter as credenciais necessárias, siga as etapas abaixo para vincular [!DNL Kinesis] conta para [!DNL Platform].

Efetue logon no [Adobe Experience Platform](https://platform.adobe.com) e selecione **[!UICONTROL Origens]** na barra de navegação esquerda, para acessar a **[!UICONTROL Origens]** espaço de trabalho. A variável **[!UICONTROL Catálogo]** A tela exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

No **[!UICONTROL Armazenamento na nuvem]** categoria, selecione **[!UICONTROL Amazon Kinesis]**. Se esta for a primeira vez que você usa este conector, selecione **[!UICONTROL Configurar]**. Caso contrário, selecione **[!UICONTROL Adicionar dados]** para criar um novo [!DNL Kinesis] conector.

![](../../../../images/tutorials/create/kinesis/catalog.png)

A variável **[!UICONTROL Conectar-se ao Amazon Kinesis]** será exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Nova conta

Se estiver usando novas credenciais, selecione **[!UICONTROL Nova conta]**. No formulário de entrada que aparece, forneça um nome, uma descrição opcional e [!DNL Kinesis] credenciais. Quando terminar, selecione **[!UICONTROL Conectar]** e aguarde algum tempo para estabelecer a nova conexão.

![](../../../../images/tutorials/create/kinesis/new.png)

### Conta existente

Para conectar uma conta existente, selecione a [!DNL Kinesis] conta à qual deseja se conectar e selecione **[!UICONTROL Próxima]** para continuar.

![](../../../../images/tutorials/create/kinesis/existing.png)

## Próximas etapas

Ao seguir este tutorial, você se conectou ao seu [!DNL Kinesis] conta para [!DNL Platform]. Agora você pode seguir para o próximo tutorial e [configure um fluxo de dados para trazer dados do armazenamento em nuvem para [!DNL Platform]](../../dataflow/streaming/cloud-storage-streaming.md).
