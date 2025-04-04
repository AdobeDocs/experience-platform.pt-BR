---
keywords: Experience Platform;página inicial;tópicos populares;Azure HDInsights;Apache Spark
solution: Experience Platform
title: Criar uma conexão do Apache Spark no Azure HDInsights Source na interface
type: Tutorial
description: Saiba como criar uma conexão de origem do Apache Spark no Azure HDInsights usando a interface do Adobe Experience Platform.
exl-id: 30d0b740-cec4-486f-9c9b-1579fd04f28b
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 1%

---

# Criar uma conexão de origem [!DNL Apache Spark] em [!DNL Azure HDInsights] na interface

>[!NOTE]
>
> O conector [!DNL Apache Spark] em [!DNL Azure HDInsights] está na versão beta. Consulte a [Visão geral das fontes](../../../../home.md#terms-and-conditions) para obter mais informações sobre o uso de conectores rotulados com beta.

Os conectores do Source no Adobe Experience Platform fornecem a capacidade de assimilar dados obtidos externamente de forma programada. Este tutorial fornece etapas para criar um [!DNL Apache Spark] no conector de origem [!DNL Azure HDInsights] usando a interface do usuário [!DNL Experience Platform].

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Sistema do Experience Data Model (XDM)](../../../../../xdm/home.md): a estrutura padronizada pela qual a Experience Platform organiza os dados de experiência do cliente.
   * [Noções básicas sobre a composição de esquema](../../../../../xdm/schema/composition.md): saiba mais sobre os blocos de construção básicos de esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição de esquema.
   * [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [Perfil de cliente em tempo real](../../../../../profile/home.md): fornece um perfil de cliente unificado em tempo real com base em dados agregados de várias fontes.

Se você já tiver uma conexão [!DNL Spark] válida, ignore o restante deste documento e prossiga para o tutorial em [configurando um fluxo de dados](../../dataflow/databases.md)

### Coletar credenciais necessárias

Para acessar sua conta do [!DNL Spark] em [!DNL Experience Platform], você deve fornecer os seguintes valores:

| Credencial | Descrição |
| ---------- | ----------- |
| `host` | O endereço IP ou o nome de host do servidor [!DNL Spark]. |
| `username` | O nome de usuário usado para acessar o servidor [!DNL Spark]. |
| `password` | A senha que corresponde ao usuário. |

Para obter mais informações sobre como começar, consulte [este documento do Spark](https://docs.microsoft.com/en-us/azure/hdinsight/spark/apache-spark-overview).

## Conectar sua conta do [!DNL Spark]

Depois de obter as credenciais necessárias, siga as etapas abaixo para vincular sua conta do [!DNL Spark] e conectar-se ao [!DNL Experience Platform].

Faça logon em [Adobe Experience Platform](https://platform.adobe.com) e selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar o espaço de trabalho **[!UICONTROL Fontes]**. A tela **[!UICONTROL Catálogo]** exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Na categoria **[!UICONTROL Databases]**, selecione **[!UICONTROL Spark]**. Se esta for a primeira vez que você usa este conector, selecione **[!UICONTROL Configurar]**. Caso contrário, selecione **[!UICONTROL Adicionar dados]** para criar um novo conector [!DNL Spark].

![catálogo](../../../../images/tutorials/create/spark/catalog.png)

A página **[!UICONTROL Conectar ao Spark]** é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Nova conta

Se você estiver usando novas credenciais, selecione **[!UICONTROL Nova conta]**. No formulário de entrada que aparece, forneça um nome, uma descrição opcional e suas credenciais do [!DNL Spark]. Quando terminar, selecione **[!UICONTROL Conectar]** e aguarde algum tempo para que a nova conexão seja estabelecida.

![novo](../../../../images/tutorials/create/spark/new.png)

### Conta existente

Para conectar uma conta existente, selecione a conta [!DNL Spark] com a qual deseja se conectar e clique em **[!UICONTROL Avançar]** para continuar.

![existente](../../../../images/tutorials/create/spark/existing.png)

## Próximas etapas

Seguindo este tutorial, você estabeleceu uma conexão com sua conta do [!DNL Spark]. Agora você pode seguir para o próximo tutorial e [configurar um fluxo de dados para trazer dados para o  [!DNL Experience Platform]](../../dataflow/databases.md).
