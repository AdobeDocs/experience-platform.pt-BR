---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Criar um conector de origem HP Vertica na interface do usuário
topic: overview
translation-type: tm+mt
source-git-commit: 5ad763d2167c68f3293a2813248efaee22230a52
workflow-type: tm+mt
source-wordcount: '512'
ht-degree: 0%

---


# Criar um conector de origem HP Vertica na interface do usuário

> [!NOTE]
> O conector HP Vertica está em beta. Consulte a visão geral [das](../../../../home.md#terms-and-conditions) Fontes para obter mais informações sobre o uso de conectores com rótulo beta.

Os conectores de origem no Adobe Experience Platform fornecem a capacidade de assimilar dados de origem externa de forma programada. Este tutorial fornece etapas para a criação de um conector de origem HP Vertica usando a interface do usuário Platform.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Sistema](../../../../../xdm/home.md)do Experience Data Model (XDM): A estrutura padronizada pela qual o Experience Platform organiza os dados de experiência do cliente.
   * [Noções básicas da composição](../../../../../xdm/schema/composition.md)do schema: Saiba mais sobre os elementos básicos dos schemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   * [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md)do Editor de Schemas: Saiba como criar schemas personalizados usando a interface do editor de Schemas.
* [Perfil](../../../../../profile/home.md)do cliente em tempo real: Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.

Se você já tiver uma conexão HP Vertica válida, poderá ignorar o restante desse documento e prosseguir para o tutorial sobre como [configurar um fluxo de dados](../../dataflow/databases.md).

### Reunir credenciais obrigatórias

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito à HP Vertica usando a API de Serviço de Fluxo.

| Credencial | Descrição |
| ---------- | ----------- |
| `connectionString` | A string de conexão usada para conectar-se à sua instância HP Vertica. O padrão da string de conexão para HP Vertica é `Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}` |

Para obter mais informações sobre como começar, consulte [este documento](https://www.vertica.com/docs/9.2.x/HTML/Content/Authoring/ConnectingToVertica/ClientJDBC/CreatingAndConfiguringAConnection.htm)HP Vertica.

## Conecte sua conta HP Vertica

Depois de reunir as credenciais necessárias, siga as etapas abaixo para criar uma nova conta HP Vertica para se conectar à Platform.

Faça logon no [Adobe Experience Platform](https://platform.adobe.com) e selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar a área de trabalho *[!UICONTROL Fontes]* . A tela *[!UICONTROL Catálogo]* exibe várias fontes nas quais você pode criar uma conta de entrada e cada fonte mostra o número de contas e fluxos de conjunto de dados associados a elas.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Na categoria *[!UICONTROL Bancos]* de dados, selecione **[!UICONTROL HP Vertica]** clique **no ícone + (+)** para criar um novo conector HP Vertica.

![catálogo](../../../../images/tutorials/create/hp-vertica/catalog.png)

A página *[!UICONTROL Conectar-se ao HP Vertica]* é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Nova conta

Se você estiver usando novas credenciais, selecione **[!UICONTROL Nova conta]**. No formulário de entrada exibido, forneça à conexão um nome, uma descrição opcional e suas credenciais HP Vertica. Quando terminar, selecione **[!UICONTROL Connect]** e aguarde algum tempo para a nova conta ser estabelecida.

![connect](../../../../images/tutorials/create/hp-vertica/new.png)

### Conta existente

Para conectar uma conta existente, selecione a conta HP Vertica à qual deseja se conectar e, em seguida, selecione **[!UICONTROL Avançar]** no canto superior direito para prosseguir.

![existente](../../../../images/tutorials/create/hp-vertica/existing.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com sua conta HP Vertica. Agora você pode continuar com o próximo tutorial e [configurar um fluxo de dados para trazer dados para o Platform](../../dataflow/databases.md).