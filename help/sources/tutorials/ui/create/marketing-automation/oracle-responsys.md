---
keywords: Experience Platform; home; tópicos populares; fontes; conectores; oracle;
title: (Beta) Criar uma conexão de origem do Responsys do Oracle usando a interface do usuário da plataforma
description: Saiba como conectar o Adobe Experience Platform ao Oracle Responsys usando a interface do usuário da plataforma.
hide: true
hidefromtoc: true
exl-id: 9ec5e1c2-3d9e-4729-be81-89a85d5ea782
source-git-commit: 784ec5f799c591185620e8376a6980b4930d914a
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 1%

---

# (Beta) Criar um [!DNL Oracle Responsys] conexão de origem usando a interface do usuário da plataforma

>[!NOTE]
>
>O [!DNL Oracle Responsys] A fonte está em beta. Consulte a [Visão geral das fontes](../../../../home.md#terms-and-conditions) para obter mais informações sobre o uso de conectores com rótulo beta.

Este tutorial fornece etapas para criar um [[!DNL Oracle Responsys]](../../../../connectors/marketing-automation/oracle-responsys.md) conexão de origem usando a interface do usuário do Adobe Experience Platform.

## Introdução

Este guia requer uma compreensão funcional dos seguintes componentes da Platform:

* [Fontes](../../../../home.md): A Platform permite que os dados sejam assimilados de várias fontes, além de fornecer a você a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma.
* [Sandboxes](../../../../../sandboxes/home.md): A Platform fornece sandboxes virtuais que particionam uma única instância da Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

Se você já tiver um [!DNL Oracle Responsys] na Platform, você pode ignorar o restante deste documento e prosseguir para o tutorial em [criação de um fluxo de dados para trazer dados de automação de marketing para a Platform](../../dataflow/marketing-automation.md).

### Obter credenciais necessárias

Para se conectar [!DNL Oracle Responsys] para o Platform, você deve fornecer valores para as seguintes propriedades de autenticação:

| Credencial | Descrição |
| --- | --- |
| Endpoint | O URL do ponto de extremidade de autenticação REST de sua [!DNL Oracle Responsys] instância. |
| ID do cliente | A ID de cliente do [!DNL Oracle Responsys] instância. |
| Segredo do cliente | O segredo do cliente de seu [!DNL Oracle Responsys] instância. |

Para obter mais informações sobre credenciais de autenticação para [!DNL Oracle Responsys], consulte o [[!DNL Oracle Responsys] guia de autenticação](https://docs.oracle.com/en/cloud/saas/marketing/responsys-develop/API/GetStarted/authentication.htm).

Depois de reunir suas credenciais necessárias, siga as etapas abaixo para vincular seus [!DNL Oracle Responsys] para a Platform.

## Conecte seu [!DNL Oracle Responsys] account

Na interface do usuário da plataforma, selecione **[!UICONTROL Fontes]** na navegação à esquerda para acessar o [!UICONTROL Fontes] espaço de trabalho. O [!UICONTROL Catálogo] exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Em [!UICONTROL Automação de marketing] categoria , selecione **[!UICONTROL Oracle Responsys]** e selecione **[!UICONTROL Adicionar dados]**.

![O catálogo Adobe Experience Platform sources com a fonte do Responsys do Oracle foi realçado.](../../../../images/tutorials/create/oracle-responsys/catalog.png)

O **[!UICONTROL Conta do Oracle Responsys do Connect]** será exibida. Nesta página, você pode usar novas credenciais ou credenciais existentes.

### Conta existente

Para usar uma conta existente, selecione a [!DNL Oracle Responsys] conta com a qual deseja criar um novo fluxo de dados e selecione **[!UICONTROL Próximo]** para continuar.

![A tela de autenticação de conta existente para o Oracle Responsys.](../../../../images/tutorials/create/oracle-responsys/existing.png)

### Nova conta

Para criar uma nova conta, selecione **[!UICONTROL Nova conta]** e forneça um nome, uma descrição opcional e os valores apropriados para sua [!DNL Oracle Responsys] credenciais. Quando terminar, selecione **[!UICONTROL Conectar-se à origem]** e, em seguida, permitir que a nova conexão seja estabelecida.

![A nova tela de autenticação de conta do Oracle Responsys.](../../../../images/tutorials/create/oracle-eloqua/new.png)

## Próximas etapas

Ao seguir este tutorial, você autenticou e criou uma conexão de origem entre os [!DNL Oracle Responsys] conta e plataforma. Agora você pode continuar para o próximo tutorial e [criar um fluxo de dados para trazer os dados de automação de marketing para a Platform](../../dataflow/marketing-automation.md).
