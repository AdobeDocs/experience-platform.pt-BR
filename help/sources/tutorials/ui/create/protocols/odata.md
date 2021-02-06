---
keywords: Experience Platform;home;popular topics;OData;odata;Generic Open Data Protocol
solution: Experience Platform
title: Criar uma conexão de fonte OData genérica na interface do usuário
topic: overview
type: Tutorial
description: Saiba como criar uma conexão de fonte Genérica Open Data Protocol usando a interface do usuário do Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: c7fb0d50761fa53c1fdf4dd70a63c62f2dcf6c85
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 1%

---


# Criar uma conexão de origem [!DNL Generic OData] na interface do usuário

>[!NOTE]
>
> O conector [!DNL Generic OData] está em beta. Consulte a [Visão geral das fontes](../../../../home.md#terms-and-conditions) para obter mais informações sobre o uso de conectores marcados com beta.

Os conectores de origem na Adobe Experience Platform fornecem a capacidade de assimilar dados de origem externa de forma programada. Este tutorial fornece etapas para a criação de um conector de origem [!DNL Generic Open Data Protocol] (a seguir denominado &quot;[!DNL OData]&quot;) usando a interface do usuário [!DNL Platform].

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): A estrutura padronizada pela qual  [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas da composição](../../../../../xdm/schema/composition.md) do schema: Saiba mais sobre os elementos básicos dos schemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   * [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md) do Editor de schemas: Saiba como criar schemas personalizados usando a interface do editor de Schemas.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.

Se você já tiver uma conexão válida [!DNL OData], poderá ignorar o restante desse documento e prosseguir para o tutorial em [configurar um fluxo de dados](../../dataflow/protocols.md)

### Reunir credenciais obrigatórias

Para acessar sua conta [!DNL OData] em [!DNL Platform], forneça os seguintes valores:

| Credencial | Descrição |
| ---------- | ----------- |
| `url` | O URL raiz do serviço [!DNL OData]. |

Para obter mais informações sobre a introdução, consulte [this [!DNL OData] documento](https://www.odata.org/getting-started/basic-tutorial/).

## Conectar sua conta [!DNL OData]

Depois de reunir as credenciais necessárias, siga as etapas abaixo para vincular sua conta [!DNL OData] a [!DNL Platform].

Faça logon em [Adobe Experience Platform](https://platform.adobe.com) e selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar a área de trabalho **[!UICONTROL Fontes]**. A tela **[!UICONTROL Catalog]** exibe várias fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Na categoria **[!UICONTROL Protocols]**, selecione **[!UICONTROL OData genérico]**. Se esta for a sua primeira vez usando este conector, selecione **[!UICONTROL Configurar]**. Caso contrário, selecione **[!UICONTROL Adicionar dados]** para criar um novo conector [!DNL OData].

![catálogo](../../../../images/tutorials/create/odata/catalog.png)

A página **[!UICONTROL Conectar-se a OData]** genérica é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Nova conta

Se você estiver usando novas credenciais, selecione **[!UICONTROL Nova conta]**. No formulário de entrada exibido, forneça à conexão um nome, uma descrição opcional e suas credenciais [!DNL OData]. Quando terminar, selecione **[!UICONTROL Connect]** e aguarde algum tempo para a nova conexão ser estabelecida.

![connect](../../../../images/tutorials/create/odata/connect.png)

### Conta existente

Para conectar uma conta existente, selecione a conta [!DNL OData] com a qual você deseja se conectar e selecione **[!UICONTROL Próximo]** para prosseguir.

![existente](../../../../images/tutorials/create/odata/existing.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com sua conta [!DNL OData]. Agora você pode continuar para o próximo tutorial e [configurar um fluxo de dados para trazer dados de protocolos para  [!DNL Platform]](../../dataflow/protocols.md).