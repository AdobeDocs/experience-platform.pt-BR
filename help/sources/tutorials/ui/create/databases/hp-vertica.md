---
keywords: Experience Platform;home;popular topics;HP Vertica
solution: Experience Platform
title: Criar um conector de origem HP Vertica na interface do usuário
topic: overview
description: Este tutorial fornece etapas para a criação de um conector de origem HP Vertica usando a interface do usuário da plataforma.
translation-type: tm+mt
source-git-commit: 6934bfeee84f542558894bbd4ba5759891cd17f3
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 1%

---


# Criar um conector de origem HP [!DNL Vertica] na interface do usuário

>[!NOTE]
>
> O conector HP [!DNL Vertica] está em beta. Consulte a visão geral [das](../../../../home.md#terms-and-conditions) Fontes para obter mais informações sobre o uso de conectores com rótulo beta.

Os conectores de origem na Adobe Experience Platform fornecem a capacidade de assimilar dados de origem externa de forma programada. Este tutorial fornece etapas para a criação de um conector de origem HP [!DNL Vertica] usando a interface do [!DNL Platform] usuário.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Experience Data Model] (XDM) Sistema](../../../../../xdm/home.md): A estrutura padronizada pela qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas da composição](../../../../../xdm/schema/composition.md)do schema: Saiba mais sobre os elementos básicos dos schemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   * [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md)do Editor de schemas: Saiba como criar schemas personalizados usando a interface do editor de Schemas.
* [[!DNL Perfil do cliente em tempo real]](../../../../../profile/home.md): Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.

Se você já tiver uma conexão HP válida, ignore o restante deste documento e prossiga para o tutorial sobre como [!DNL Vertica] configurar um fluxo de dados [](../../dataflow/databases.md).

### Reunir credenciais obrigatórias

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito à HP [!DNL Vertica] usando a [!DNL Flow Service] API.

| Credencial | Descrição |
| ---------- | ----------- |
| `connectionString` | A cadeia de conexão usada para conectar-se à sua instância HP [!DNL Vertica] . O padrão da string de conexão para HP [!DNL Vertica] é `Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}` |

Para obter mais informações sobre a introdução, consulte [este documento [!DNL Vertica] da](https://www.vertica.com/docs/9.2.x/HTML/Content/Authoring/ConnectingToVertica/ClientJDBC/CreatingAndConfiguringAConnection.htm)HP.

## Conecte sua conta HP [!DNL Vertica]

Depois de reunir as credenciais necessárias, siga as etapas abaixo para vincular sua conta da HP [!DNL Vertica] a [!DNL Platform].

Faça logon no [Adobe Experience Platform](https://platform.adobe.com) e selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar a área de trabalho **[!UICONTROL Fontes]** . A tela **[!UICONTROL Catálogo]** exibe várias fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Na categoria **[!UICONTROL Bancos]** de dados, selecione **[!UICONTROL HP Vertica]**. Se esta for a sua primeira vez usando este conector, selecione **[!UICONTROL Configurar]**. Caso contrário, selecione **[!UICONTROL Adicionar dados]** para criar um novo conector HP [!DNL Vertica] .

![catálogo](../../../../images/tutorials/create/hp-vertica/catalog.png)

A página **[!UICONTROL Conectar-se ao HP Vertica]** é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Nova conta

Se você estiver usando novas credenciais, selecione **[!UICONTROL Nova conta]**. No formulário de entrada exibido, forneça um nome, uma descrição opcional e suas [!DNL Vertica] credenciais da HP. Quando terminar, selecione **[!UICONTROL Connect]** e aguarde algum tempo para a nova conexão ser estabelecida.

![connect](../../../../images/tutorials/create/hp-vertica/new.png)

### Conta existente

Para conectar uma conta existente, selecione a conta HP com a qual você deseja se conectar e, em seguida, selecione [!DNL Vertica] Avançar **** no canto superior direito para continuar.

![existente](../../../../images/tutorials/create/hp-vertica/existing.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com sua conta da HP [!DNL Vertica] . Agora você pode continuar para o próximo tutorial e [configurar um fluxo de dados para trazer [!DNL Platform]](../../dataflow/databases.md)os dados para o