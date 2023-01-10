---
keywords: Experience Platform, home, tópicos populares, Data Explorer do Azure, explorador de dados do azure, explorador de dados, Data Explorer
solution: Experience Platform
title: Criar uma conexão de origem de Data Explorer do Azure na interface do usuário
type: Tutorial
description: Saiba como criar uma conexão de origem do Azure Data Explorer usando a interface do usuário do Adobe Experience Platform.
exl-id: 561bf948-fc92-4401-8631-e2a408667507
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 1%

---

# Crie um [!DNL Azure Data Explorer] conexão de origem na interface do usuário

Os conectores de origem no Adobe Experience Platform oferecem a capacidade de assimilar dados de origem externa de acordo com a programação. Este tutorial fornece etapas para criar um [!DNL Azure Data Explorer] (a seguir designado por &quot;[!DNL Data Explorer]&quot;) conector de origem usando o [!DNL Platform] interface do usuário.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): O quadro normalizado pelo qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas da composição do schema](../../../../../xdm/schema/composition.md): Saiba mais sobre os elementos básicos dos esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   * [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Fornece um perfil de consumidor unificado e em tempo real com base em dados agregados de várias fontes.

Se você já tiver um [!DNL Data Explorer] , você pode ignorar o restante deste documento e prosseguir para o tutorial em [configuração de um fluxo de dados](../../dataflow/databases.md).

### Obter credenciais necessárias

Para acessar o [!DNL Data Explorer] conta em [!DNL Platform], você deve fornecer os seguintes valores:

| Credencial | Descrição |
| ---------- | ----------- |
| `endpoint` | O terminal da [!DNL Data Explorer] servidor. |
| `database` | O nome do [!DNL Data Explorer] banco de dados. |
| `tenant` | A ID de locatário exclusiva usada para se conectar ao [!DNL Data Explorer] banco de dados. |
| `servicePrincipalId` | A ID da entidade de serviço exclusiva usada para se conectar ao [!DNL Data Explorer] banco de dados. |
| `servicePrincipalKey` | A chave principal de serviço exclusiva usada para se conectar ao [!DNL Data Explorer] banco de dados. |

Para obter mais informações sobre a introdução, consulte [this [!DNL Data Explorer] documento](https://docs.microsoft.com/en-us/azure/data-explorer/kusto/management/access-control/how-to-authenticate-with-aad).

## Conecte seu [!DNL Azure Data Explorer] account

Depois de reunir suas credenciais necessárias, siga as etapas abaixo para vincular seus [!DNL Data Explorer] para [!DNL Platform].

Faça logon em [Adobe Experience Platform](https://platform.adobe.com) e depois selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar o **[!UICONTROL Fontes]** espaço de trabalho. O **[!UICONTROL Catálogo]** exibe uma variedade de fontes para as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Em **[!UICONTROL Bancos de dados]** categoria , selecione **[!UICONTROL Data Explorer do Azure]**. Se esta for a primeira vez que você usa esse conector, selecione **[!UICONTROL Configurar]**. Caso contrário, selecione **[!UICONTROL Adicionar dados]** para criar um novo conector do Data Explorer.

![catálogo](../../../../images/tutorials/create/data-explorer/catalog.png)

O **[!UICONTROL Conectar-se ao Azure Data Explorer]** será exibida. Nesta página, você pode usar novas credenciais ou credenciais existentes.

### Nova conta

Se estiver usando novas credenciais, selecione **[!UICONTROL Nova conta]**. No formulário de entrada exibido, forneça um nome, uma descrição opcional e [!DNL Data Explorer] credenciais. Quando terminar, selecione **[!UICONTROL Connect]** e, em seguida, permitir que a nova conexão seja estabelecida.

![connect](../../../../images/tutorials/create/data-explorer/new.png)

### Conta existente

Para conectar uma conta existente, selecione a [!DNL Data Explorer] conta com a qual deseja se conectar e selecione **[!UICONTROL Próximo]** para continuar.

![existente](../../../../images/tutorials/create/data-explorer/existing.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com seu [!DNL Data Explorer] conta. Agora você pode continuar para o próximo tutorial e [configurar um fluxo de dados para trazer os dados para [!DNL Platform]](../../dataflow/databases.md).
