---
keywords: Experience Platform;home;popular topics;Couchbase;couchbase
solution: Experience Platform
title: Criar um conector de origem Couchbase na interface do usuário
topic: overview
description: Este tutorial fornece etapas para a criação de um conector de origem Couchbase usando a interface do usuário da plataforma.
translation-type: tm+mt
source-git-commit: f82dfee2c75a0b8b2ec1615266780b309152ead4
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 1%

---


# Criar um conector [!DNL Couchbase] de origem na interface do usuário

>[!NOTE]
>
> O [!DNL Couchbase] conector está em beta. Consulte a visão geral [das](../../../../home.md#terms-and-conditions) Fontes para obter mais informações sobre o uso de conectores com rótulo beta.

Os conectores de origem fornecem [!DNL Adobe Experience Platform] a capacidade de assimilar dados de origem externa de forma programada. Este tutorial fornece etapas para criar um conector de [!DNL Couchbase] origem usando a interface do [!DNL Platform] usuário.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do [!DNL Platform]:

* [[!DNL Experience Data Model] (XDM) Sistema](../../../../../xdm/home.md): A estrutura padronizada pela qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas da composição](../../../../../xdm/schema/composition.md)do schema: Saiba mais sobre os elementos básicos dos schemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   * [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md)do Editor de schemas: Saiba como criar schemas personalizados usando a interface do editor de Schemas.
* [[!DNL Perfil do cliente em tempo real]](../../../../../profile/home.md): Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.

Se você já tiver uma [!DNL Couchbase] conexão válida, poderá ignorar o restante desse documento e prosseguir para o tutorial sobre como [configurar um fluxo de dados](../../dataflow/databases.md).

### Reunir credenciais obrigatórias

Para autenticar seu conector [!DNL Couchbase] de origem, é necessário fornecer valores para a seguinte propriedade de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| `connectionString` | A cadeia de conexão usada para se conectar à sua [!DNL Couchbase] instância. O padrão da string de conexão para [!DNL Couchbase] é `Server={SERVER}; Port={PORT};AuthMech=1;CredString=[{\"user\": \"{USER}\", \"pass\":\"{PASS}\"}];`. Para obter mais informações sobre como adquirir uma string de conexão, consulte a documentação sobre a [[!DNL Couchbase] conexão](https://docs.Couchbase.com/c-sdk/2.10/client-settings.html#configuring-overview). |

## Conectar sua [!DNL Couchbase] conta

Depois de reunir as credenciais necessárias, siga as etapas abaixo para vincular sua [!DNL Couchbase] conta a [!DNL Platform].

Faça logon no [Adobe Experience Platform](https://platform.adobe.com) e selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar a área de trabalho **[!UICONTROL Fontes]** . A tela **[!UICONTROL Catálogo]** exibe várias fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Na categoria **[!UICONTROL Bancos]** de dados, selecione **[!UICONTROL Couchbase]**. Se esta for a sua primeira vez usando este conector, selecione **[!UICONTROL Configurar]**. Caso contrário, selecione **[!UICONTROL Adicionar dados]** para criar um novo [!DNL Couchbase] conector.

![catálogo](../../../../images/tutorials/create/couchbase/catalog.png)

A página **[!UICONTROL Conectar-se ao Couchbase]** é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Nova conta

Se você estiver usando novas credenciais, selecione **[!UICONTROL Nova conta]**. No formulário de entrada exibido, forneça um nome, uma descrição opcional e suas [!DNL Couchbase] credenciais. Quando terminar, selecione **[!UICONTROL Conectar-se à fonte]** e aguarde algum tempo para a nova conexão ser estabelecida.

![connect](../../../../images/tutorials/create/couchbase/new.png)

### Conta existente

Para conectar uma conta existente, selecione a [!DNL Couchbase] conta à qual deseja se conectar e, em seguida, selecione **[!UICONTROL Próximo]** no canto superior direito para continuar.

![existente](../../../../images/tutorials/create/couchbase/existing.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com sua [!DNL Couchbase] conta. Agora você pode continuar para o próximo tutorial e [configurar um fluxo de dados para trazer [!DNL Platform]](../../dataflow/databases.md)os dados para o