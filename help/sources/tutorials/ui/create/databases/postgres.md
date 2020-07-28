---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Criar um conector de origem PostgreSQL na interface do usuário
topic: overview
translation-type: tm+mt
source-git-commit: 4f7d7e2bf255afe1588dbe7cfb2ec055f2dcbf75
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 1%

---


# Criar um conector [!DNL PostgreSQL] de origem na interface do usuário

>[!NOTE]
> O [!DNL PostgreSQL] conector está em beta. Consulte a visão geral [das](../../../../home.md#terms-and-conditions) Fontes para obter mais informações sobre o uso de conectores com rótulo beta.

Os conectores de origem no Adobe Experience Platform fornecem a capacidade de assimilar dados de origem externa de forma programada. Este tutorial fornece etapas para a criação de um conector de origem [!DNL PostgreSQL] (a seguir denominado &quot;PSQL&quot;) usando a interface do [!DNL Platform] usuário.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Sistema](../../../../../xdm/home.md)do Experience Data Model (XDM): A estrutura padronizada pela qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas da composição](../../../../../xdm/schema/composition.md)do schema: Saiba mais sobre os elementos básicos dos schemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   * [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md)do Editor de Schemas: Saiba como criar schemas personalizados usando a interface do editor de Schemas.
* [Perfil](../../../../../profile/home.md)do cliente em tempo real: Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.

Se você já tiver uma conexão básica PSQL, poderá ignorar o restante desse documento e prosseguir para o tutorial sobre como [configurar um fluxo de dados](../../dataflow/databases.md).

### Reunir credenciais obrigatórias

Para acessar sua conta PSQL em [!DNL Platform], forneça o seguinte valor:

| Credencial | Descrição |
| ---------- | ----------- |
| `connectionString` | A cadeia de conexão associada à sua conta PSQL. O padrão da cadeia de conexão PSQL é: `Server={SERVER};Database={DATABASE};Port={PORT};UID={USERNAME};Password={PASSWORD}`. |

Para obter mais informações sobre a introdução, consulte este documento [](https://www.postgresql.org/docs/9.2/app-psql.html)PSQL.

## Conectar sua conta PSQL

Depois de coletar as credenciais necessárias, você pode seguir as etapas abaixo para criar uma nova conexão básica de entrada para vincular sua conta PSQL à [!DNL Platform].

Faça logon no <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> e selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar a área de trabalho *[!UICONTROL Fontes]* . A tela *[!UICONTROL Catálogo]* exibe várias fontes com as quais você pode criar conexões base de entrada e cada fonte mostra o número de conexões base existentes associadas a elas.

Na categoria *[!UICONTROL Bancos]* de Dados, selecione **[!UICONTROL PostgreSQL DB]** para expor uma barra de informações no lado direito da tela. A barra de informações fornece uma breve descrição para a fonte selecionada, bem como opções para se conectar à fonte ou à sua documentação de visualização. Para criar uma nova conexão básica de entrada, selecione **[!UICONTROL Fonte]** do Connect.

![](../../../../images/tutorials/create/psql/catalog.png)

A página *[!UICONTROL Conectar-se ao PSQL]* é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Nova conta

Se você estiver usando novas credenciais, selecione **[!UICONTROL Nova conta]**. No formulário de entrada exibido, forneça um nome, uma descrição opcional e suas credenciais PSQL à conexão básica. Quando terminar, selecione **[!UICONTROL Connect]** e aguarde algum tempo para a nova conexão básica ser estabelecida.

![](../../../../images/tutorials/create/psql/connect.png)

### Conta existente

Para conectar uma conta existente, selecione a conta PSQL com a qual deseja se conectar e, em seguida, selecione **[!UICONTROL Próximo]** para prosseguir.

![](../../../../images/tutorials/create/psql/existing.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão básica com sua conta PSQL. Agora você pode continuar com o próximo tutorial e [configurar um fluxo de dados para trazer dados para o Platform](../../dataflow/databases.md).