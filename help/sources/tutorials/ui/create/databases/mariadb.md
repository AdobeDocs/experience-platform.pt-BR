---
title: Conectar o MariaDB ao Experience Platform usando a interface
description: Saiba como conectar sua conta MariaDB ao Experience Platform usando o espaço de trabalho de origens na interface do usuário do Experience Platform.
exl-id: 259ca112-01f1-414a-bf9f-d94caf4c69df
source-git-commit: bca4f40d452f0a5e70a388872a65640d1fd58533
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 0%

---

# Conectar o [!DNL MariaDB] ao Experience Platform usando a interface

Leia este guia para saber como conectar sua conta do [!DNL MariaDB] à Adobe Experience Platform usando o espaço de trabalho de fontes na interface do usuário do Experience Platform.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): a estrutura padronizada pela qual o Experience Platform organiza os dados de experiência do cliente.
   * [Noções básicas sobre a composição de esquema](../../../../../xdm/schema/composition.md): saiba mais sobre os blocos de construção básicos de esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição de esquema.
   * [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [Perfil de cliente em tempo real](../../../../../profile/home.md): fornece um perfil de cliente unificado em tempo real com base em dados agregados de várias fontes.

Se você já tiver uma conexão [!DNL MariaDB], ignore o restante deste documento e prossiga para o tutorial em [configurando um fluxo de dados](../../dataflow/databases.md).

### Coletar credenciais necessárias

Leia a [[!DNL MariaDB] visão geral](../../../../connectors/databases/mariadb.md#prerequisites) para obter informações sobre autenticação.

## Navegar pelo catálogo de origens

Na interface do Experience Platform, selecione **[!UICONTROL Fontes]** na navegação à esquerda para acessar o espaço de trabalho *[!UICONTROL Fontes]*. Selecione a categoria apropriada no painel *[!UICONTROL Categorias]* Como alternativa, use a barra de pesquisa para navegar até a fonte específica que deseja usar.

Para usar [!DNL MariaDB], selecione o cartão de origem **[!UICONTROL MariaDB]** em *[!UICONTROL Bancos de dados]* e selecione **[!UICONTROL Configurar]**.

>[!TIP]
>
>As origens no catálogo de origens exibem a opção **[!UICONTROL Configurar]** quando uma determinada origem ainda não tem uma conta autenticada. Após a criação de uma conta autenticada, esta opção será alterada para **[!UICONTROL Adicionar dados]**.

![O catálogo de fontes na interface do usuário com o cartão MariaDB selecionado.](../../../../images/tutorials/create/maria-db/catalog.png)

## Usar uma conta existente {#existing}

Para usar uma conta existente, selecione **[!UICONTROL Conta existente]** e depois selecione a conta [!DNL MariaDB] que deseja usar.

![A interface de contas existentes no fluxo de trabalho de origem com a opção &quot;Conta existente&quot; selecionada.](../../../../images/tutorials/create/maria-db/existing.png)

## Criar uma nova conta {#create}

Se você não tiver uma conta existente, deverá criar uma nova conta fornecendo as credenciais de autenticação necessárias que correspondam à sua origem.

Para criar uma nova conta, selecione **[!UICONTROL Nova conta]** e forneça um nome e, opcionalmente, adicione uma descrição para sua conta.

![A nova interface de conta no fluxo de trabalho de origem com um nome de conta e uma descrição opcional fornecidos.](../../../../images/tutorials/create/maria-db/new.png)

### Conectar-se ao Experience Platform

Você pode conectar sua conta do [!DNL MariaDB] à Experience Platform usando a chave da conta ou a autenticação básica.

>[!BEGINTABS]

>[!TAB Autenticação da chave da conta]

Para usar a autenticação de chave de conta, selecione **[!UICONTROL Autenticação de chave de conta]**, forneça sua [cadeia de conexão](../../../../connectors/databases/mariadb.md#azure) e selecione **[!UICONTROL Conectar à origem]**.

![A nova interface de conta no fluxo de trabalho de origens com a opção &quot;Autenticação de chave de conta&quot; selecionada.](../../../../images/tutorials/create/maria-db/account-key.png)

>[!TAB Autenticação básica]

Para usar a autenticação básica, selecione **[!UICONTROL Autenticação básica]**, forneça valores para suas [credenciais de autenticação](../../../../connectors/databases/mariadb.md#azure) e selecione **[!UICONTROL Conectar à origem]**.

![A nova interface de conta no fluxo de trabalho de origens com &quot;Autenticação básica&quot; selecionada.](../../../../images/tutorials/create/maria-db/basic-auth.png)

>[!ENDTABS]

Seguindo este tutorial, você estabeleceu uma conexão com sua conta do [!DNL MariaDB]. Agora você pode seguir para o próximo tutorial e [configurar um fluxo de dados para trazer dados para a Experience Platform](../../dataflow/databases.md).
