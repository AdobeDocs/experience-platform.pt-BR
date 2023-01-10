---
keywords: Experience Platform, home, tópicos populares, OData, odata, Generic Open Data Protocol
solution: Experience Platform
title: Criar uma conexão de fonte OData genérica na interface do usuário
type: Tutorial
description: Saiba como criar uma conexão de fonte Genérica de Protocolo de Dados Abertos usando a interface do usuário do Adobe Experience Platform.
exl-id: aad6b6f7-622c-4ab6-bf6d-1221fe1132d1
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 1%

---

# Crie um [!DNL Generic OData] conexão de origem na interface do usuário

Os conectores de origem no Adobe Experience Platform oferecem a capacidade de assimilar dados de origem externa de acordo com a programação. Este tutorial fornece etapas para criar um [!DNL Generic Open Data Protocol] (a seguir designado por &quot;[!DNL OData]&quot;) conector de origem usando o [!DNL Platform] interface do usuário.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): O quadro normalizado pelo qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas da composição do schema](../../../../../xdm/schema/composition.md): Saiba mais sobre os elementos básicos dos esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   * [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Fornece um perfil de consumidor unificado e em tempo real com base em dados agregados de várias fontes.

Se você já tiver um [!DNL OData] , você pode ignorar o restante deste documento e prosseguir para o tutorial em [configuração de um fluxo de dados](../../dataflow/protocols.md)

### Obter credenciais necessárias

Para acessar o [!DNL OData] conta em [!DNL Platform], você deve fornecer os seguintes valores:

| Credencial | Descrição |
| ---------- | ----------- |
| `url` | O URL raiz da variável [!DNL OData] serviço. |

Para obter mais informações sobre a introdução, consulte [this [!DNL OData] documento](https://www.odata.org/getting-started/basic-tutorial/).

## Conecte seu [!DNL OData] account

Depois de reunir suas credenciais necessárias, siga as etapas abaixo para vincular seus [!DNL OData] para [!DNL Platform].

Faça logon em [Adobe Experience Platform](https://platform.adobe.com) e depois selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar o **[!UICONTROL Fontes]** espaço de trabalho. O **[!UICONTROL Catálogo]** exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Em **[!UICONTROL Protocolos]** categoria , selecione **[!UICONTROL OData genérico]**. Se esta for a primeira vez que você usa esse conector, selecione **[!UICONTROL Configurar]**. Caso contrário, selecione **[!UICONTROL Adicionar dados]** para criar um novo [!DNL OData] conector.

![catálogo](../../../../images/tutorials/create/odata/catalog.png)

O **[!UICONTROL Conectar-se ao OData genérico]** será exibida. Nesta página, você pode usar novas credenciais ou credenciais existentes.

### Nova conta

Se estiver usando novas credenciais, selecione **[!UICONTROL Nova conta]**. No formulário de entrada exibido, forneça à conexão um nome, uma descrição opcional e [!DNL OData] credenciais. Quando terminar, selecione **[!UICONTROL Connect]** e, em seguida, permitir que a nova conexão seja estabelecida.

![connect](../../../../images/tutorials/create/odata/connect.png)

### Conta existente

Para conectar uma conta existente, selecione a [!DNL OData] conta com a qual deseja se conectar e selecione **[!UICONTROL Próximo]** para continuar.

![existente](../../../../images/tutorials/create/odata/existing.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com seu [!DNL OData] conta. Agora você pode continuar para o próximo tutorial e [configurar um fluxo de dados para trazer os dados de protocolos para [!DNL Platform]](../../dataflow/protocols.md).
