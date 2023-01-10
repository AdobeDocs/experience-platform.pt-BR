---
keywords: Experience Platform, home, tópicos populares, HP Vertica
solution: Experience Platform
title: Criar uma conexão de origem HP Vertica na interface do usuário
type: Tutorial
description: Saiba como criar uma conexão de origem HP Vertica usando a interface do usuário do Adobe Experience Platform.
exl-id: d7315ad4-9250-4e66-be33-016efabb512e
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '495'
ht-degree: 1%

---

# Criar uma HP [!DNL Vertica] conexão de origem na interface do usuário

>[!NOTE]
>
> A HP [!DNL Vertica] O conector está em beta. Consulte a [Visão geral das fontes](../../../../home.md#terms-and-conditions) para obter mais informações sobre o uso de conectores com rótulo beta.

Os conectores de origem no Adobe Experience Platform oferecem a capacidade de assimilar dados de origem externa de acordo com a programação. Este tutorial fornece etapas para a criação de uma HP [!DNL Vertica] conector de origem usando o [!DNL Platform] interface do usuário.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): O quadro normalizado pelo qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas da composição do schema](../../../../../xdm/schema/composition.md): Saiba mais sobre os elementos básicos dos esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   * [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Fornece um perfil de consumidor unificado e em tempo real com base em dados agregados de várias fontes.

Se você já tiver uma HP válida [!DNL Vertica] , você pode ignorar o restante deste documento e prosseguir para o tutorial em [configuração de um fluxo de dados](../../dataflow/databases.md).

### Obter credenciais necessárias

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito à HP [!DNL Vertica] usando o [!DNL Flow Service] API.

| Credencial | Descrição |
| ---------- | ----------- |
| `connectionString` | A string de conexão usada para se conectar à HP [!DNL Vertica] instância. O padrão da string de conexão para HP [!DNL Vertica] é `Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}` |

Para obter mais informações sobre a introdução, consulte [essa HP [!DNL Vertica] documento](https://www.vertica.com/docs/9.2.x/HTML/Content/Authoring/ConnectingToVertica/ClientJDBC/CreatingAndConfiguringAConnection.htm).

## Conecte sua HP [!DNL Vertica] account

Depois de reunir suas credenciais necessárias, você poderá seguir as etapas abaixo para vincular sua HP [!DNL Vertica] para [!DNL Platform].

Faça logon em [Adobe Experience Platform](https://platform.adobe.com) e depois selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar o **[!UICONTROL Fontes]** espaço de trabalho. O **[!UICONTROL Catálogo]** exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Em **[!UICONTROL Bancos de dados]** categoria , selecione **[!UICONTROL HP Vertica]**. Se esta for a primeira vez que você usa esse conector, selecione **[!UICONTROL Configurar]**. Caso contrário, selecione **[!UICONTROL Adicionar dados]** para criar uma nova HP [!DNL Vertica] conector.

![catálogo](../../../../images/tutorials/create/hp-vertica/catalog.png)

O **[!UICONTROL Conecte-se à HP Vertica]** será exibida. Nesta página, você pode usar novas credenciais ou credenciais existentes.

### Nova conta

Se estiver usando novas credenciais, selecione **[!UICONTROL Nova conta]**. No formulário de entrada exibido, forneça um nome, uma descrição opcional e sua HP [!DNL Vertica] credenciais. Quando terminar, selecione **[!UICONTROL Connect]** e, em seguida, permitir que a nova conexão seja estabelecida.

![connect](../../../../images/tutorials/create/hp-vertica/new.png)

### Conta existente

Para conectar uma conta existente, selecione a opção HP [!DNL Vertica] conta com a qual deseja se conectar e selecione **[!UICONTROL Próximo]** no canto superior direito para continuar.

![existente](../../../../images/tutorials/create/hp-vertica/existing.png)

## Próximas etapas

Seguindo este tutorial, você estabeleceu uma conexão com sua HP [!DNL Vertica] conta. Agora você pode continuar para o próximo tutorial e [configurar um fluxo de dados para trazer os dados para [!DNL Platform]](../../dataflow/databases.md).
