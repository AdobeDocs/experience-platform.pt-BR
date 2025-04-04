---
keywords: Experience Platform;home;tópicos populares;origens;conectores;oracle;
title: (Beta) Criar uma conexão de origem do Oracle Responsys usando a interface do usuário do Experience Platform
description: Saiba como conectar o Adobe Experience Platform ao Oracle Responsys usando a interface do usuário do Experience Platform.
hide: true
hidefromtoc: true
exl-id: 9ec5e1c2-3d9e-4729-be81-89a85d5ea782
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 2%

---

# (Beta) Criar uma conexão de origem [!DNL Oracle Responsys] usando a interface do usuário do Experience Platform

>[!NOTE]
>
>A origem [!DNL Oracle Responsys] está na versão beta. Consulte a [Visão geral das fontes](../../../../home.md#terms-and-conditions) para obter mais informações sobre o uso de conectores rotulados com beta.

Este tutorial fornece etapas para criar uma conexão de origem [[!DNL Oracle Responsys]](../../../../connectors/marketing-automation/oracle-responsys.md) usando a interface do usuário do Adobe Experience Platform.

## Introdução

Este guia requer uma compreensão funcional dos seguintes componentes do Experience Platform:

* [Fontes](../../../../home.md): o Experience Platform permite a assimilação de dados de várias fontes, ao mesmo tempo em que fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços do Experience Platform.
* [Sandboxes](../../../../../sandboxes/home.md): a Experience Platform fornece sandboxes virtuais que particionam uma única instância do Experience Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

Se você já tiver uma conta autenticada do [!DNL Oracle Responsys] no Experience Platform, ignore o restante deste documento e prossiga para o tutorial em [criação de um fluxo de dados para trazer dados de automação de marketing para o Experience Platform](../../dataflow/marketing-automation.md).

### Coletar credenciais necessárias

Para conectar [!DNL Oracle Responsys] ao Experience Platform, você deve fornecer valores para as seguintes propriedades de autenticação:

| Credencial | Descrição |
| --- | --- |
| Endpoint | A URL do ponto de extremidade de autenticação REST da instância [!DNL Oracle Responsys]. |
| ID de cliente | A ID do cliente da sua instância [!DNL Oracle Responsys]. |
| Segredo do cliente | O segredo do cliente da sua instância [!DNL Oracle Responsys]. |

Para obter mais informações sobre credenciais de autenticação para [!DNL Oracle Responsys], consulte o [[!DNL Oracle Responsys] guia sobre autenticação](https://docs.oracle.com/en/cloud/saas/marketing/responsys-develop/API/GetStarted/authentication.htm).

Depois de obter as credenciais necessárias, siga as etapas abaixo para vincular sua conta do [!DNL Oracle Responsys] à Experience Platform.

## Conectar sua conta do [!DNL Oracle Responsys]

Na interface do Experience Platform, selecione **[!UICONTROL Fontes]** na navegação à esquerda para acessar o espaço de trabalho [!UICONTROL Fontes]. A tela [!UICONTROL Catálogo] exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Na categoria [!UICONTROL Automação de marketing], selecione **[!UICONTROL Oracle Responsys]** e **[!UICONTROL Adicionar dados]**.

![O catálogo de fontes do Adobe Experience Platform com a origem do Oracle Responsys foi realçado.](../../../../images/tutorials/create/oracle-responsys/catalog.png)

A página **[!UICONTROL Conectar conta do Oracle Responsys]** é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Conta existente

Para usar uma conta existente, selecione a conta [!DNL Oracle Responsys] com a qual deseja criar um novo fluxo de dados e clique em **[!UICONTROL Avançar]** para continuar.

![A tela de autenticação de conta existente para o Oracle Responsys.](../../../../images/tutorials/create/oracle-responsys/existing.png)

### Nova conta

Para criar uma nova conta, selecione **[!UICONTROL Nova conta]** e forneça um nome, uma descrição opcional e os valores apropriados para suas credenciais do [!DNL Oracle Responsys]. Quando terminar, selecione **[!UICONTROL Conectar à origem]** e aguarde algum tempo para que a nova conexão seja estabelecida.

![A nova tela de autenticação de conta do Oracle Responsys.](../../../../images/tutorials/create/oracle-eloqua/new.png)

## Próximas etapas

Seguindo este tutorial, você autenticou e criou uma conexão de origem entre sua conta do [!DNL Oracle Responsys] e a Experience Platform. Agora você pode seguir para o próximo tutorial e [criar um fluxo de dados para trazer os dados de automação de marketing para o Experience Platform](../../dataflow/marketing-automation.md).
