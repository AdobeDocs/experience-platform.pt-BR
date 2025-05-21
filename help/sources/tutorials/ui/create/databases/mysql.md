---
title: Conectar o MySQL ao Experience Platform usando a interface
description: Saiba como conectar seu banco de dados MySQL ao Experience Platform usando a interface do usuário.
exl-id: 75e74bde-6199-4970-93d2-f95ec3a59aa5
source-git-commit: f4200ca71479126e585ac76dd399af4092fdf683
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 0%

---

# Conectar o [!DNL MySQL] ao Experience Platform usando a interface

Leia este guia para saber como conectar seu banco de dados do [!DNL MySQL] ao Adobe Experience Platform usando o espaço de trabalho de origens na interface do usuário do Experience Platform.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): a estrutura padronizada pela qual o Experience Platform organiza os dados de experiência do cliente.
   * [Noções básicas sobre a composição de esquema](../../../../../xdm/schema/composition.md): saiba mais sobre os blocos de construção básicos de esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição de esquema.
   * [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.

Se você já tiver uma conexão [!DNL MySQL], ignore o restante deste documento e prossiga para o tutorial em [configurando um fluxo de dados](../../dataflow/databases.md).

### Coletar credenciais necessárias

Leia a [[!DNL MySQL] visão geral](../../../../connectors/databases/mysql.md#prerequisites) para obter informações sobre autenticação.

## Navegar pelo catálogo de origens

Na interface do Experience Platform, selecione **[!UICONTROL Fontes]** na navegação à esquerda para acessar o espaço de trabalho *[!UICONTROL Fontes]*. Escolha uma categoria ou use a barra de pesquisa para localizar sua fonte.

Para se conectar a [!DNL MySQL], vá para a categoria *[!UICONTROL Bancos de Dados]*, selecione o cartão de origem **[!UICONTROL MySQL]** e selecione **[!UICONTROL Configurar]**.

>[!TIP]
>
>As origens no catálogo de origens exibem a opção **[!UICONTROL Configurar]** quando uma determinada origem ainda não tem uma conta autenticada. Após a criação de uma conta autenticada, esta opção será alterada para **[!UICONTROL Adicionar dados]**.

![O catálogo de origens com o cartão de origem MySQL selecionado.](../../../../images/tutorials/create/my-sql/catalog.png)

## Usar uma conta existente {#existing}

Para usar uma conta existente, selecione **[!UICONTROL Conta existente]** e depois selecione a conta [!DNL MySQL] que deseja usar.

![A interface de contas existentes no fluxo de trabalho de origem com a opção &quot;Conta existente&quot; selecionada.](../../../../images/tutorials/create/my-sql/existing.png)

## Criar uma nova conta {#new}

Para criar uma nova conta, selecione **[!UICONTROL Nova conta]** e forneça um nome e, opcionalmente, adicione uma descrição para sua conta.

![A nova interface de conta no fluxo de trabalho de origem com um nome de conta e uma descrição opcional fornecidos.](../../../../images/tutorials/create/my-sql/new.png)

### Conectar-se ao Experience Platform no Azure {#azure}

Você pode conectar seu banco de dados do [!DNL MySQL] ao Experience Platform no Azure usando a chave da conta ou a autenticação básica.

>[!BEGINTABS]

>[!TAB Autenticação da chave da conta]

Para usar a autenticação de chave de conta, selecione **[!UICONTROL Autenticação de chave de conta]**, forneça sua [cadeia de conexão](../../../../connectors/databases/mysql.md#azure) e selecione **[!UICONTROL Conectar à origem]**.

![A nova interface de conta no fluxo de trabalho de origens com a opção &quot;Autenticação de chave de conta&quot; selecionada.](../../../../images/tutorials/create/my-sql/account-key.png)

>[!TAB Autenticação básica]

Para usar a autenticação básica, selecione **[!UICONTROL Autenticação básica]**, forneça valores para suas [credenciais de autenticação](../../../../connectors/databases/mysql.md#azure) e selecione **[!UICONTROL Conectar à origem]**.

![A nova interface de conta no fluxo de trabalho de origens com &quot;Autenticação básica&quot; selecionada.](../../../../images/tutorials/create/my-sql/basic-auth.png)

>[!ENDTABS]

### Conectar-se ao Experience Platform no Amazon Web Services (AWS) {#aws}

>[!AVAILABILITY]
>
>Esta seção se aplica às implementações do Experience Platform em execução no Amazon Web Services (AWS). O Experience Platform em execução no AWS está disponível atualmente para um número limitado de clientes. Para saber mais sobre a infraestrutura do Experience Platform compatível, consulte a [visão geral da nuvem múltipla do Experience Platform](../../../../../landing/multi-cloud.md).

Para criar uma nova conta do [!DNL MySQL] e conectar-se ao Experience Platform no AWS, verifique se você está em uma sandbox VA6 e forneça as [credenciais necessárias para autenticação](../../../../connectors/databases/mysql.md#aws).

![A nova interface de conta no fluxo de trabalho de origens para se conectar ao AWS.](../../../../images/tutorials/create/my-sql/aws.png)

## Criar um fluxo de dados para dados de [!DNL MySQL]

Agora que você conectou com êxito o banco de dados [!DNL MySQL], agora é possível [criar um fluxo de dados e assimilar dados do banco de dados na Experience Platform](../../dataflow/databases.md).
