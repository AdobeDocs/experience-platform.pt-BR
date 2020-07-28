---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Criar um conector de origem Amazon Kinesis na interface do usuário
topic: overview
translation-type: tm+mt
source-git-commit: d3c725c4760acb3857a67d0d30b24732c963a030
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 1%

---


# Criar um conector [!DNL Amazon Kinesis] de origem na interface do usuário

>[!NOTE]
>O [!DNL Amazon Kinesis] conector está em beta. Consulte a visão geral [das](../../../../home.md#terms-and-conditions) Fontes para obter mais informações sobre o uso de conectores com rótulo beta.

Os conectores de origem no Adobe Experience Platform fornecem a capacidade de assimilar dados de origem externa de forma programada. Este tutorial fornece etapas para autenticação de um conector de origem [!DNL Amazon Kinesis] (a seguir denominado [!DNL "Kinesis"]) usando a interface do [!DNL Platform] usuário.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

- [Sistema](../../../../../xdm/home.md)do Experience Data Model (XDM): A estrutura padronizada pela qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
   - [Noções básicas da composição](../../../../../xdm/schema/composition.md)do schema: Saiba mais sobre os elementos básicos dos schemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   - [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md)do Editor de Schemas: Saiba como criar schemas personalizados usando a interface do editor de Schemas.
- [Perfil](../../../../../profile/home.md)do cliente em tempo real: Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.

Se você já tiver uma [!DNL Kinesis] conta, poderá ignorar o restante desse documento e prosseguir para o tutorial sobre como [configurar um fluxo de dados](../../dataflow/streaming/cloud-storage.md).

### Reunir credenciais obrigatórias

Para autenticar seu conector [!DNL Kinesis] de origem, é necessário fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| `accessKeyId` | A ID da chave de acesso da sua [!DNL Kinesis] conta. |
| `Secret access key` | A chave de acesso secreta da sua [!DNL Kinesis] conta. |
| `region` | A região do servidor AWS. |

Para obter mais informações sobre esses valores, consulte [este documento](https://docs.aws.amazon.com/streams/latest/dev/getting-started.html)Kinesis.

## Conectar sua [!DNL Kinesis] conta

Depois de reunir as credenciais necessárias, siga as etapas abaixo para vincular sua [!DNL Kinesis] conta a [!DNL Platform].

Faça logon no [Adobe Experience Platform](https://platform.adobe.com) e selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar a área de trabalho *Fontes* . A guia *Catálogo* exibe várias fontes às quais é possível se conectar [!DNL Platform]. Cada fonte mostra o número de contas existentes associadas a elas.

Na categoria do Armazenamento *[!UICONTROL da]* Cloud, selecione **[!UICONTROL Amazon Kinesis]** e clique **no ícone + (+)** para criar um novo [!DNL Kinesis] conector.

![](../../../../images/tutorials/create/kinesis/catalog.png)

A caixa de diálogo *[!UICONTROL Conectar-se ao Amazon Kinesis]* é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Nova conta

Se você estiver usando novas credenciais, selecione **[!UICONTROL Nova conta]**. No formulário de entrada exibido, forneça um nome, uma descrição opcional e suas [!DNL Kinesis] credenciais. Quando terminar, selecione **[!UICONTROL Connect]** e aguarde algum tempo para a nova conexão ser estabelecida.

![](../../../../images/tutorials/create/kinesis/new.png)

### Conta existente

Para conectar uma conta existente, selecione a [!DNL Kinesis] conta à qual deseja se conectar e, em seguida, selecione **[!UICONTROL Avançar]** para continuar.

![](../../../../images/tutorials/create/kinesis/existing.png)

## Próximas etapas

Ao seguir este tutorial, você se conectou à sua [!DNL Kinesis] conta [!DNL Platform]. Agora você pode continuar para o próximo tutorial e [configurar um fluxo de dados para trazer dados do seu armazenamento em nuvem para o Platform](../../dataflow/streaming/cloud-storage.md).