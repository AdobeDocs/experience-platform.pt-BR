---
keywords: Experience Platform;home;popular topics;OData;odata;Generic Open Data Protocol
solution: Experience Platform
title: Criar um conector de origem OData genérico na interface do usuário
topic: overview
description: Este tutorial fornece etapas para a criação de um conector de origem Genérico Open Data Protocol (a seguir denominado "OData") usando a interface de usuário da Plataforma.
translation-type: tm+mt
source-git-commit: f82dfee2c75a0b8b2ec1615266780b309152ead4
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 1%

---


# Criar um conector [!DNL Generic OData] de origem na interface do usuário

>[!NOTE]
>
> O [!DNL Generic OData] conector está em beta. Consulte a visão geral [das](../../../../home.md#terms-and-conditions) Fontes para obter mais informações sobre o uso de conectores com rótulo beta.

Os conectores de origem na Adobe Experience Platform fornecem a capacidade de assimilar dados de origem externa de forma programada. Este tutorial fornece etapas para a criação de um conector de origem [!DNL Generic Open Data Protocol] (a seguir denominado &quot;[!DNL OData]&quot;) usando a interface do [!DNL Platform] usuário.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Experience Data Model] (XDM) Sistema](../../../../../xdm/home.md): A estrutura padronizada pela qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas da composição](../../../../../xdm/schema/composition.md)do schema: Saiba mais sobre os elementos básicos dos schemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   * [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md)do Editor de schemas: Saiba como criar schemas personalizados usando a interface do editor de Schemas.
* [[!DNL Perfil do cliente em tempo real]](../../../../../profile/home.md): Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.

Se você já tiver uma [!DNL OData] conexão válida, poderá ignorar o restante desse documento e prosseguir para o tutorial sobre como [configurar um fluxo de dados](../../dataflow/protocols.md)

### Reunir credenciais obrigatórias

Para acessar sua [!DNL OData] conta em [!DNL Platform], forneça os seguintes valores:

| Credencial | Descrição |
| ---------- | ----------- |
| `url` | O URL raiz do [!DNL OData] serviço. |

Para obter mais informações sobre como começar, consulte [ [!DNL OData] este documento](https://www.odata.org/getting-started/basic-tutorial/).

## Conectar sua [!DNL OData] conta

Depois de reunir as credenciais necessárias, siga as etapas abaixo para vincular sua [!DNL OData] conta a [!DNL Platform].

Faça logon no [Adobe Experience Platform](https://platform.adobe.com) e selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar a área de trabalho **[!UICONTROL Fontes]** . A tela **[!UICONTROL Catálogo]** exibe várias fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Em categoria de **[!UICONTROL protocolos]** , selecione OData **[!UICONTROL genérico]**. Se esta for a sua primeira vez usando este conector, selecione **[!UICONTROL Configurar]**. Caso contrário, selecione **[!UICONTROL Adicionar dados]** para criar um novo [!DNL OData] conector.

![catálogo](../../../../images/tutorials/create/odata/catalog.png)

A página **[!UICONTROL Conectar-se a OData]** genérica é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Nova conta

Se você estiver usando novas credenciais, selecione **[!UICONTROL Nova conta]**. No formulário de entrada exibido, forneça à conexão um nome, uma descrição opcional e suas [!DNL OData] credenciais. Quando terminar, selecione **[!UICONTROL Connect]** e aguarde algum tempo para a nova conexão ser estabelecida.

![connect](../../../../images/tutorials/create/odata/connect.png)

### Conta existente

Para conectar uma conta existente, selecione a [!DNL OData] conta à qual deseja se conectar e, em seguida, selecione **[!UICONTROL Avançar]** para continuar.

![existente](../../../../images/tutorials/create/odata/existing.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com sua [!DNL OData] conta. Agora, você pode continuar para o próximo tutorial e [configurar um fluxo de dados para trazer dados de protocolos para [!DNL Platform]](../../dataflow/protocols.md)ele.