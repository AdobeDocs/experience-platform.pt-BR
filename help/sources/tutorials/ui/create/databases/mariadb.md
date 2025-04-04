---
keywords: Experience Platform;página inicial;tópicos populares;Maria DB;maria db
solution: Experience Platform
title: Criar uma conexão MariaDB Source na interface
type: Tutorial
description: Saiba como criar uma conexão de origem Maria DB usando a interface do usuário do Adobe Experience Platform.
exl-id: 259ca112-01f1-414a-bf9f-d94caf4c69df
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 2%

---

# Criar uma conexão de origem [!DNL MariaDB] na interface

Os conectores do Source no Adobe Experience Platform fornecem a capacidade de assimilar dados obtidos externamente de forma programada. Este tutorial fornece etapas para a criação de um conector de origem Maria DB usando a interface do usuário [!DNL Experience Platform].

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): a estrutura padronizada pela qual o [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas sobre a composição de esquema](../../../../../xdm/schema/composition.md): saiba mais sobre os blocos de construção básicos de esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição de esquema.
   * [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [Perfil de cliente em tempo real](../../../../../profile/home.md): fornece um perfil de cliente unificado em tempo real com base em dados agregados de várias fontes.

Se você já tiver uma conexão [!DNL MariaDB], ignore o restante deste documento e prossiga para o tutorial em [configurando um fluxo de dados](../../dataflow/databases.md).

### Coletar credenciais necessárias

Para acessar sua conta do [!DNL MariaDB] em [!DNL Experience Platform], você deve fornecer o seguinte valor:

| Credencial | Descrição |
| ---------- | ----------- |
| `connectionString` | A cadeia de conexão associada à autenticação MariaDB. O padrão da cadeia de conexão [!DNL MariaDB] é: `Server={HOST};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}`. |

Para obter mais informações sobre a introdução, consulte este [[!DNL MariaDB] documento](https://mariadb.com/kb/en/about-mariadb-connector-odbc/).

## Conectar sua conta do [!DNL Maria DB]

Depois de obter as credenciais necessárias, siga as etapas abaixo para vincular sua conta do [!DNL Maria DB] ao [!DNL Experience Platform].

Faça logon em [Adobe Experience Platform](https://platform.adobe.com) e selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar o espaço de trabalho **[!UICONTROL Fontes]**. A tela **[!UICONTROL Catálogo]** exibe uma variedade de fontes com as quais você pode criar uma conta.

Na categoria **[!UICONTROL Bancos de dados]**, selecione **[!UICONTROL Maria DB]**. Se esta for a primeira vez que você usa este conector, selecione **[!UICONTROL Configurar]**. Caso contrário, selecione **[!UICONTROL Adicionar dados]** para criar um novo conector [!DNL Maria DB].

![](../../../../images/tutorials/create/maria-db/catalog.png)

A página **[!UICONTROL Conectar-se ao Maria DB]** é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Nova conta

Se você estiver usando novas credenciais, selecione **[!UICONTROL Nova conta]**. No formulário de entrada que aparece, forneça um nome, uma descrição opcional e suas credenciais do [!DNL MariaDB]. Quando terminar, selecione **[!UICONTROL Conectar]** e aguarde algum tempo para que a nova conexão seja estabelecida.

![](../../../../images/tutorials/create/maria-db/new.png)

### Conta existente

Para conectar uma conta existente, selecione a conta [!DNL MariaDB] com a qual deseja se conectar e clique em **[!UICONTROL Avançar]** para continuar.

![](../../../../images/tutorials/create/maria-db/existing.png)

## Próximas etapas

Seguindo este tutorial, você estabeleceu uma conexão com sua conta do [!DNL MariaDB]. Agora você pode seguir para o próximo tutorial e [configurar um fluxo de dados para trazer dados para o  [!DNL Experience Platform]](../../dataflow/databases.md).
