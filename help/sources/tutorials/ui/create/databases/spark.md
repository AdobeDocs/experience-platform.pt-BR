---
keywords: Experience Platform;página inicial;tópicos populares;Azure HDInsights;Apache Spark
solution: Experience Platform
title: Criar uma conexão de origem do Apache Spark no Azure HDInsights na interface
type: Tutorial
description: Saiba como criar uma conexão de origem do Apache Spark no Azure HDInsights usando a interface do Adobe Experience Platform.
exl-id: 30d0b740-cec4-486f-9c9b-1579fd04f28b
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 1%

---

# Criar um [!DNL Apache Spark] em [!DNL Azure HDInsights] conexão de origem na interface

>[!NOTE]
>
> A variável [!DNL Apache Spark] em [!DNL Azure HDInsights] o conector está na versão beta. Consulte a [Visão geral das fontes](../../../../home.md#terms-and-conditions) para obter mais informações sobre o uso de conectores rotulados com beta.

Os conectores de origem no Adobe Experience Platform fornecem a capacidade de assimilar dados originados externamente de forma programada. Este tutorial fornece etapas para a criação de um [!DNL Apache Spark] em [!DNL Azure HDInsights] conector de origem usando o [!DNL Platform] interface do usuário.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Sistema do Experience Data Model (XDM)](../../../../../xdm/home.md): a estrutura padronizada pela qual o Experience Platform organiza os dados de experiência do cliente.
   * [Noções básicas da composição do esquema](../../../../../xdm/schema/composition.md): saiba mais sobre os componentes básicos dos esquemas XDM, incluindo princípios fundamentais e práticas recomendadas na composição do esquema.
   * [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [Perfil do cliente em tempo real](../../../../../profile/home.md): fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.

Se você já tiver um [!DNL Spark] conexão, você pode ignorar o restante deste documento e prosseguir para o tutorial em [configuração de um fluxo de dados](../../dataflow/databases.md)

### Coletar credenciais necessárias

Para acessar seu [!DNL Spark] conta em [!DNL Platform], você deve fornecer os seguintes valores:

| Credencial | Descrição |
| ---------- | ----------- |
| `host` | O endereço IP ou o nome de host do [!DNL Spark] servidor. |
| `username` | O nome de usuário que você usa para acessar o [!DNL Spark] servidor. |
| `password` | A senha que corresponde ao usuário. |

Para obter mais informações sobre a introdução, consulte [este documento do Spark](https://docs.microsoft.com/en-us/azure/hdinsight/spark/apache-spark-overview).

## Conecte seu [!DNL Spark] account

Depois de obter as credenciais necessárias, siga as etapas abaixo para vincular [!DNL Spark] conta à qual se conectar [!DNL Platform].

Efetue logon no [Adobe Experience Platform](https://platform.adobe.com) e selecione **[!UICONTROL Origens]** na barra de navegação esquerda, para acessar a **[!UICONTROL Origens]** espaço de trabalho. A variável **[!UICONTROL Catálogo]** A tela exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

No **[!UICONTROL Bancos de dados]** categoria, selecione **[!UICONTROL Spark]**. Se esta for a primeira vez que você usa este conector, selecione **[!UICONTROL Configurar]**. Caso contrário, selecione **[!UICONTROL Adicionar dados]** para criar um novo [!DNL Spark] conector.

![catálogo](../../../../images/tutorials/create/spark/catalog.png)

A variável **[!UICONTROL Conectar ao Spark]** é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Nova conta

Se estiver usando novas credenciais, selecione **[!UICONTROL Nova conta]**. No formulário de entrada que aparece, forneça um nome, uma descrição opcional e [!DNL Spark] credenciais. Quando terminar, selecione **[!UICONTROL Conectar]** e aguarde algum tempo para estabelecer a nova conexão.

![novo](../../../../images/tutorials/create/spark/new.png)

### Conta existente

Para conectar uma conta existente, selecione a [!DNL Spark] conta à qual deseja se conectar e selecione **[!UICONTROL Próxima]** para continuar.

![existente](../../../../images/tutorials/create/spark/existing.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com o seu [!DNL Spark] conta. Agora você pode seguir para o próximo tutorial e [configurar um fluxo de dados para trazer dados para o [!DNL Platform]](../../dataflow/databases.md).
