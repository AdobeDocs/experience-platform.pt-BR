---
keywords: Experience Platform, home, tópicos populares, Apache Hive, Azure HDInsights, azure hdinsights
solution: Experience Platform
title: Criar um Apache Hive na Conexão de Origem do Azure HDInsights na interface do usuário
type: Tutorial
description: Saiba como criar um Apache Hive na conexão de origem do Azure HDInsights usando a interface do usuário do Adobe Experience Platform.
exl-id: 3eb3cb02-9867-451a-b847-ab895310eedf
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 1%

---

# Crie um [!DNL Apache Hive] on [!DNL Azure HDInsights] conexão de origem na interface do usuário

>[!NOTE]
>
> O [!DNL Apache Hive] on [!DNL Azure HDInsights] O conector está em beta. Consulte a [Visão geral das fontes](../../../../home.md#terms-and-conditions) para obter mais informações sobre o uso de conectores com rótulo beta.

Os conectores de origem no Adobe Experience Platform oferecem a capacidade de assimilar dados de origem externa de acordo com a programação. Este tutorial fornece etapas para criar um [!DNL Apache Hive] on [!DNL Azure HDInsights] conector de origem usando o [!DNL Platform] interface do usuário.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): O quadro normalizado pelo qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas da composição do schema](../../../../../xdm/schema/composition.md): Saiba mais sobre os elementos básicos dos esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   * [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Fornece um perfil de consumidor unificado e em tempo real com base em dados agregados de várias fontes.

Se você já tiver um [!DNL Hive] , você pode ignorar o restante deste documento e prosseguir para o tutorial em [configuração de um fluxo de dados](../../dataflow/databases.md)

### Obter credenciais necessárias

Para acessar o [!DNL Hive] conta em [!DNL Platform], você deve fornecer os seguintes valores:

| Credencial | Descrição |
| ---------- | ----------- |
| `host` | O endereço IP ou o nome do host do [!DNL Hive] servidor. |
| `username` | O nome de usuário usado para acessar o [!DNL Hive] servidor. |
| `password` | A senha que corresponde ao usuário. |

Para obter mais informações sobre a introdução, consulte [this [!DNL Hive] documento](https://cwiki.apache.org/confluence/display/Hive/Tutorial#Tutorial-GettingStarted).

## Conecte seu [!DNL Hive] account

Depois de reunir suas credenciais necessárias, siga as etapas abaixo para vincular seus [!DNL Hive] para [!DNL Platform].

Faça logon em [Adobe Experience Platform](https://platform.adobe.com) e depois selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar o **[!UICONTROL Fontes]** espaço de trabalho. O **[!UICONTROL Catálogo]** exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Em **[!UICONTROL Bancos de dados]** categoria , selecione **[!UICONTROL Hive]**. Se esta for a primeira vez que você usa esse conector, selecione **[!UICONTROL Configurar]**. Caso contrário, selecione **[!UICONTROL Adicionar dados]** para criar um novo [!DNL Hive] conector.

![catálogo](../../../../images/tutorials/create/hive/catalog.png)

O **[!UICONTROL Conectar-se ao Hive]** será exibida. Nesta página, você pode usar novas credenciais ou credenciais existentes.

### Nova conta

Se estiver usando novas credenciais, selecione **[!UICONTROL Nova conta]**. No formulário de entrada exibido, forneça um nome, uma descrição opcional e [!DNL Hive] credenciais. Quando terminar, selecione **[!UICONTROL Connect]** e, em seguida, permitir que a nova conexão seja estabelecida.

![connect](../../../../images/tutorials/create/hive/new.png)

### Conta existente

Para conectar uma conta existente, selecione a [!DNL Hive] conta com a qual deseja se conectar e selecione **[!UICONTROL Próximo]** para continuar.

![existente](../../../../images/tutorials/create/hive/existing.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com seu [!DNL Hive] conta. Agora você pode continuar para o próximo tutorial e [configurar um fluxo de dados para trazer os dados para [!DNL Platform]](../../dataflow/databases.md).
