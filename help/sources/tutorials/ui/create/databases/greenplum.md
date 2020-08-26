---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Criar um conector de origem GreenPlum na interface do usuário
topic: overview
translation-type: tm+mt
source-git-commit: 690ddbd92f0a2e4e06b988e761dabff399cd2367
workflow-type: tm+mt
source-wordcount: '465'
ht-degree: 1%

---


# Criar um conector [!DNL GreenPlum] de origem na interface do usuário

>[!NOTE]
>
> O [!DNL GreenPlum] conector está em beta. Consulte a visão geral [das](../../../../home.md#terms-and-conditions) Fontes para obter mais informações sobre o uso de conectores com rótulo beta.

Os conectores de origem na Adobe Experience Platform fornecem a capacidade de assimilar dados de origem externa de forma programada. Este tutorial fornece etapas para criar um conector de [!DNL GreenPlum] origem usando a interface do [!DNL Platform] usuário.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Experience Data Model] (XDM) Sistema](../../../../../xdm/home.md): A estrutura padronizada pela qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas da composição](../../../../../xdm/schema/composition.md)do schema: Saiba mais sobre os elementos básicos dos schemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   * [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md)do Editor de schemas: Saiba como criar schemas personalizados usando a interface do editor de Schemas.
* [[!DNL Perfil do cliente em tempo real]](../../../../../profile/home.md): Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.

Se você já tiver uma [!DNL GreenPlum] conexão válida, poderá ignorar o restante desse documento e prosseguir para o tutorial sobre como [configurar um fluxo de dados](../../dataflow/databases.md).

### Reunir credenciais obrigatórias

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito [!DNL GreenPlum] usando a [!DNL Flow Service] API.

| Credencial | Descrição |
| ---------- | ----------- |
| `connectionString` | A cadeia de conexão usada para se conectar à sua [!DNL GreenPlum] instância. O padrão da string de conexão para [!DNL GreenPlum] é `Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}` |

Para obter mais informações sobre a introdução, consulte [este documento](https://gpdb.docs.pivotal.io/580/security-guide/topics/Authenticate.html#topic_fzv_wb2_jr__config_ssl_client_conn)GreenPlum.

## Conectar sua [!DNL GreenPlum] conta

Depois de reunir as credenciais necessárias, siga as etapas abaixo para vincular sua [!DNL GreenPlum] conta a [!DNL Platform].

Faça logon no [Adobe Experience Platform](https://platform.adobe.com) e selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar a área de trabalho **[!UICONTROL Fontes]** . A tela **[!UICONTROL Catálogo]** exibe várias fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Na categoria **[!UICONTROL Bancos]** de dados, selecione **[!UICONTROL GreenPlum]**. Se esta for a sua primeira vez usando este conector, selecione **[!UICONTROL Configurar]**. Caso contrário, selecione **[!UICONTROL Adicionar dados]** para criar um novo [!DNL GreenPlum] conector.

![catálogo](../../../../images/tutorials/create/greenplum/catalog.png)

A página **[!UICONTROL Conectar-se ao GreenPlum]** é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Nova conta

Se você estiver usando novas credenciais, selecione **[!UICONTROL Nova conta]**. No formulário de entrada exibido, forneça um nome, uma descrição opcional e suas [!DNL GreenPlum] credenciais. Quando terminar, selecione **[!UICONTROL Connect]** e aguarde algum tempo para a nova conexão ser estabelecida.

![connect](../../../../images/tutorials/create/greenplum/new.png)

### Conta existente

Para conectar uma conta existente, selecione a [!DNL GreenPlum] conta à qual deseja se conectar e, em seguida, selecione **[!UICONTROL Próximo]** no canto superior direito para continuar.

![existente](../../../../images/tutorials/create/greenplum/existing.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com sua [!DNL GreenPlum] conta. Agora você pode continuar para o próximo tutorial e [configurar um fluxo de dados para trazer [!DNL Platform]](../../dataflow/databases.md)os dados para o