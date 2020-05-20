---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Criar um conector de origem GreenPlum na interface do usuário
topic: overview
translation-type: tm+mt
source-git-commit: a015d2612bc5a72004e15dc5706c7718617a0af4
workflow-type: tm+mt
source-wordcount: '495'
ht-degree: 1%

---


# Criar um conector de origem GreenPlum na interface do usuário

> [!NOTE]
> O conector GreenPlum está em beta. Os recursos e a documentação estão sujeitos a alterações.

Os conectores de origem na Adobe Experience Platform fornecem a capacidade de assimilar dados de origem externa de forma programada. Este tutorial fornece etapas para a criação de um conector de origem GreenPlum usando a interface do usuário da plataforma.

## Introdução

Este tutorial requer uma compreensão prática dos seguintes componentes da Adobe Experience Platform:

* [Sistema](../../../../../xdm/home.md)do Experience Data Model (XDM): A estrutura padronizada pela qual a plataforma Experience organiza os dados da experiência do cliente.
   * [Noções básicas da composição](../../../../../xdm/schema/composition.md)do schema: Saiba mais sobre os elementos básicos dos schemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   * [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md)do Editor de Schemas: Saiba como criar schemas personalizados usando a interface do editor de Schemas.
* [Perfil](../../../../../profile/home.md)do cliente em tempo real: Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.

Se você já tiver uma conexão GreenPlum válida, poderá ignorar o restante desse documento e prosseguir para o tutorial sobre como [configurar um fluxo de dados](../../dataflow/databases.md).

### Reunir credenciais obrigatórias

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito ao GreenPlum usando a API de Serviço de Fluxo.

| Credencial | Descrição |
| ---------- | ----------- |
| `connectionString` | A cadeia de conexão usada para se conectar à sua instância GreenPlum. O padrão da string de conexão para GreenPlum é `HOST=<server>;PORT=<port>;DB=<database>;UID=<user name>;PWD=<password>` |

Para obter mais informações sobre como começar, consulte [este documento](https://gpdb.docs.pivotal.io/580/security-guide/topics/Authenticate.html#topic_fzv_wb2_jr__config_ssl_client_conn)GreenPlum.

## Conecte sua conta do GreenPlum

Depois de reunir as credenciais necessárias, siga as etapas abaixo para criar uma nova conta do GreenPlum para se conectar à Plataforma.

Faça logon na [Adobe Experience Platform](https://platform.adobe.com) e selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar a área de trabalho *[!UICONTROL Fontes]* . A tela *[!UICONTROL Catálogo]* exibe várias fontes nas quais você pode criar uma conta de entrada e cada fonte mostra o número de contas e fluxos de conjunto de dados associados a elas.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Na categoria *[!UICONTROL Bancos]* de dados, selecione **[!UICONTROL GreenPlum]** clique **no ícone + (+)** para criar um novo conector GreenPlum.

![catálogo](../../../../images/tutorials/create/greenplum/catalog.png)

A página *[!UICONTROL Conectar-se ao GreenPlum]* é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Nova conta

Se você estiver usando novas credenciais, selecione **[!UICONTROL Nova conta]**. No formulário de entrada exibido, forneça à conexão um nome, uma descrição opcional e suas credenciais do GreenPlum. Quando terminar, selecione **[!UICONTROL Connect]** e aguarde algum tempo para a nova conta ser estabelecida.

![connect](../../../../images/tutorials/create/greenplum/new.png)

### Conta existente

Para conectar uma conta existente, selecione a conta GreenPlum com a qual deseja se conectar e, em seguida, selecione **[!UICONTROL Avançar]** no canto superior direito para prosseguir.

![existente](../../../../images/tutorials/create/greenplum/existing.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com sua conta do GreenPlum. Agora você pode continuar com o próximo tutorial e [configurar um fluxo de dados para trazer dados para a Plataforma](../../dataflow/databases.md).