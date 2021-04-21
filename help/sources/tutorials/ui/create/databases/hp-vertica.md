---
keywords: Experience Platform, home, tópicos populares, HP Vertica
solution: Experience Platform
title: Criar uma conexão de origem HP Vertica na interface do usuário
topic-legacy: overview
type: Tutorial
description: Saiba como criar uma conexão de origem HP Vertica usando a interface do usuário do Adobe Experience Platform.
exl-id: d7315ad4-9250-4e66-be33-016efabb512e
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 1%

---

# Criar uma conexão de origem HP [!DNL Vertica] na interface do usuário

>[!NOTE]
>
> O conector HP [!DNL Vertica] está em beta. Consulte a [Visão geral das Fontes](../../../../home.md#terms-and-conditions) para obter mais informações sobre o uso de conectores com marca beta.

Os conectores de origem no Adobe Experience Platform oferecem a capacidade de assimilar dados de origem externa de acordo com a programação. Este tutorial fornece etapas para criar um conector de origem HP [!DNL Vertica] usando a interface do usuário [!DNL Platform].

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): A estrutura padronizada pela qual  [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas da composição](../../../../../xdm/schema/composition.md) do schema: Saiba mais sobre os elementos básicos dos esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   * [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md) do Editor de esquema: Saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Fornece um perfil de consumidor unificado e em tempo real com base em dados agregados de várias fontes.

Se você já tiver uma conexão HP válida [!DNL Vertica], poderá ignorar o restante deste documento e prosseguir para o tutorial em [configurar um fluxo de dados](../../dataflow/databases.md).

### Obter credenciais necessárias

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito à HP [!DNL Vertica] usando a API [!DNL Flow Service].

| Credencial | Descrição |
| ---------- | ----------- |
| `connectionString` | A string de conexão usada para se conectar à instância HP [!DNL Vertica]. O padrão da string de conexão para HP [!DNL Vertica] é `Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}` |

Para obter mais informações sobre a introdução, consulte [este documento HP [!DNL Vertica] document](https://www.vertica.com/docs/9.2.x/HTML/Content/Authoring/ConnectingToVertica/ClientJDBC/CreatingAndConfiguringAConnection.htm).

## Conecte sua conta HP [!DNL Vertica]

Depois de coletar suas credenciais necessárias, siga as etapas abaixo para vincular sua conta HP [!DNL Vertica] a [!DNL Platform].

Faça logon em [Adobe Experience Platform](https://platform.adobe.com) e selecione **[!UICONTROL Sources]** na barra de navegação esquerda para acessar o espaço de trabalho **[!UICONTROL Sources]**. A tela **[!UICONTROL Catalog]** exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Na categoria **[!UICONTROL Databases]**, selecione **[!UICONTROL HP Vertica]**. Se esta for a primeira vez que você usa esse conector, selecione **[!UICONTROL Configure]**. Caso contrário, selecione **[!UICONTROL Add data]** para criar um novo conector HP [!DNL Vertica].

![catálogo](../../../../images/tutorials/create/hp-vertica/catalog.png)

A página **[!UICONTROL Connect to HP Vertica]** é exibida. Nesta página, você pode usar novas credenciais ou credenciais existentes.

### Nova conta

Se estiver usando novas credenciais, selecione **[!UICONTROL New account]**. No formulário de entrada exibido, forneça um nome, uma descrição opcional e suas credenciais HP [!DNL Vertica]. Quando terminar, selecione **[!UICONTROL Connect]** e aguarde algum tempo para que a nova conexão seja estabelecida.

![connect](../../../../images/tutorials/create/hp-vertica/new.png)

### Conta existente

Para conectar uma conta existente, selecione a conta HP [!DNL Vertica] com a qual deseja se conectar e selecione **[!UICONTROL Next]** no canto superior direito para prosseguir.

![existente](../../../../images/tutorials/create/hp-vertica/existing.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com sua conta HP [!DNL Vertica]. Agora você pode continuar para o próximo tutorial e [configurar um fluxo de dados para trazer dados para [!DNL Platform]](../../dataflow/databases.md).
