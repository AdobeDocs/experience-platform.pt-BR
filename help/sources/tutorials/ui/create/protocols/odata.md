---
keywords: Experience Platform, home, tópicos populares, OData, odata, Generic Open Data Protocol
solution: Experience Platform
title: Criar uma conexão de fonte OData genérica na interface do usuário
topic-legacy: overview
type: Tutorial
description: Saiba como criar uma conexão de fonte Genérica de Protocolo de Dados Abertos usando a interface do usuário do Adobe Experience Platform.
exl-id: aad6b6f7-622c-4ab6-bf6d-1221fe1132d1
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 1%

---

# Criar uma conexão de origem [!DNL Generic OData] na interface do usuário

>[!NOTE]
>
> O conector [!DNL Generic OData] está em beta. Consulte a [Visão geral das Fontes](../../../../home.md#terms-and-conditions) para obter mais informações sobre o uso de conectores com marca beta.

Os conectores de origem no Adobe Experience Platform oferecem a capacidade de assimilar dados de origem externa de acordo com a programação. Este tutorial fornece etapas para criar um conector de origem [!DNL Generic Open Data Protocol] (a seguir chamado &quot;[!DNL OData]&quot;) usando a interface do usuário [!DNL Platform].

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): A estrutura padronizada pela qual  [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas da composição](../../../../../xdm/schema/composition.md) do schema: Saiba mais sobre os elementos básicos dos esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   * [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md) do Editor de esquema: Saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Fornece um perfil de consumidor unificado e em tempo real com base em dados agregados de várias fontes.

Se você já tiver uma conexão válida [!DNL OData], poderá ignorar o restante deste documento e prosseguir para o tutorial em [configurar um fluxo de dados](../../dataflow/protocols.md)

### Obter credenciais necessárias

Para acessar sua conta [!DNL OData] em [!DNL Platform], você deve fornecer os seguintes valores:

| Credencial | Descrição |
| ---------- | ----------- |
| `url` | O URL raiz do serviço [!DNL OData]. |

Para obter mais informações sobre a introdução, consulte [this [!DNL OData] document](https://www.odata.org/getting-started/basic-tutorial/).

## Conecte sua conta [!DNL OData]

Depois de coletar suas credenciais necessárias, siga as etapas abaixo para vincular sua conta [!DNL OData] a [!DNL Platform].

Faça logon em [Adobe Experience Platform](https://platform.adobe.com) e selecione **[!UICONTROL Sources]** na barra de navegação esquerda para acessar o espaço de trabalho **[!UICONTROL Sources]**. A tela **[!UICONTROL Catalog]** exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Na categoria **[!UICONTROL Protocols]**, selecione **[!UICONTROL Generic OData]**. Se esta for a primeira vez que você usa esse conector, selecione **[!UICONTROL Configure]**. Caso contrário, selecione **[!UICONTROL Add data]** para criar um novo conector [!DNL OData].

![catálogo](../../../../images/tutorials/create/odata/catalog.png)

A página **[!UICONTROL Connect to Generic OData]** é exibida. Nesta página, você pode usar novas credenciais ou credenciais existentes.

### Nova conta

Se estiver usando novas credenciais, selecione **[!UICONTROL New account]**. No formulário de entrada exibido, forneça a conexão com um nome, uma descrição opcional e suas credenciais [!DNL OData]. Quando terminar, selecione **[!UICONTROL Connect]** e aguarde algum tempo para que a nova conexão seja estabelecida.

![connect](../../../../images/tutorials/create/odata/connect.png)

### Conta existente

Para conectar uma conta existente, selecione a conta [!DNL OData] com a qual deseja se conectar e selecione **[!UICONTROL Next]** para prosseguir.

![existente](../../../../images/tutorials/create/odata/existing.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com sua conta [!DNL OData]. Agora você pode continuar para o próximo tutorial e [configurar um fluxo de dados para trazer dados de protocolos para [!DNL Platform]](../../dataflow/protocols.md).
