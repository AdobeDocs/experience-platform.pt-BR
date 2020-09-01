---
keywords: Experience Platform;home;popular topics;Maria DB;maria db
solution: Experience Platform
title: Criar um conector de origem MariaDB na interface do usuário
topic: overview
description: Este tutorial fornece etapas para a criação de um conector de origem Maria DB usando a interface de usuário da plataforma.
translation-type: tm+mt
source-git-commit: f82dfee2c75a0b8b2ec1615266780b309152ead4
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 1%

---


# Criar um conector [!DNL MariaDB] de origem na interface do usuário

>[!NOTE]
>
> O [!DNL MariaDB] conector está em beta. Consulte a visão geral [das](../../../../home.md#terms-and-conditions) Fontes para obter mais informações sobre o uso de conectores com rótulo beta.

Os conectores de origem na Adobe Experience Platform fornecem a capacidade de assimilar dados de origem externa de forma programada. Este tutorial fornece etapas para a criação de um conector de origem Maria DB usando a interface do [!DNL Platform] usuário.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Experience Data Model] (XDM) Sistema](../../../../../xdm/home.md): A estrutura padronizada pela qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas da composição](../../../../../xdm/schema/composition.md)do schema: Saiba mais sobre os elementos básicos dos schemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   * [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md)do Editor de schemas: Saiba como criar schemas personalizados usando a interface do editor de Schemas.
* [Perfil](../../../../../profile/home.md)do cliente em tempo real: Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.

Se você já tiver uma [!DNL MariaDB] conexão, poderá ignorar o restante desse documento e prosseguir para o tutorial sobre como [configurar um fluxo de dados](../../dataflow/databases.md).

### Reunir credenciais obrigatórias

Para acessar sua [!DNL MariaDB] conta em [!DNL Platform], forneça o seguinte valor:

| Credencial | Descrição |
| ---------- | ----------- |
| `connectionString` | A cadeia de conexão associada à autenticação MariaDB. O padrão da string de [!DNL MariaDB] conexão é: `Server={HOST};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}`. |

Para obter mais informações sobre a introdução, consulte este [[!DNL MariaDB] documento](https://mariadb.com/kb/en/about-mariadb-connector-odbc/).

## Conectar sua [!DNL Maria DB] conta

Depois de reunir as credenciais necessárias, siga as etapas abaixo para vincular sua [!DNL Maria DB] conta a [!DNL Platform].

Faça logon no [Adobe Experience Platform](https://platform.adobe.com) e selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar a área de trabalho **[!UICONTROL Fontes]** . A tela **[!UICONTROL Catálogo]** exibe várias fontes com as quais você pode criar uma conta.

Na categoria **[!UICONTROL Bancos]** de Dados, selecione **[!UICONTROL Maria DB]**. Se esta for a sua primeira vez usando este conector, selecione **[!UICONTROL Configurar]**. Caso contrário, selecione **[!UICONTROL Adicionar dados]** para criar um novo [!DNL Maria DB] conector.

![](../../../../images/tutorials/create/maria-db/catalog.png)

A página **[!UICONTROL Conectar-se a Maria DB]** é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Nova conta

Se você estiver usando novas credenciais, selecione **[!UICONTROL Nova conta]**. No formulário de entrada exibido, forneça um nome, uma descrição opcional e suas [!DNL MariaDB] credenciais. Quando terminar, selecione **[!UICONTROL Connect]** e aguarde algum tempo para a nova conexão ser estabelecida.

![](../../../../images/tutorials/create/maria-db/new.png)

### Conta existente

Para conectar uma conta existente, selecione a [!DNL MariaDB] conta à qual deseja se conectar e, em seguida, selecione **[!UICONTROL Avançar]** para continuar.

![](../../../../images/tutorials/create/maria-db/existing.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com sua [!DNL MariaDB] conta. Agora você pode continuar para o próximo tutorial e [configurar um fluxo de dados para trazer [!DNL Platform]](../../dataflow/databases.md)os dados para o