---
keywords: Experience Platform;página inicial;tópicos populares;Azure Data Explorer;azure data explorer;explorador de dados;Data Explorer
solution: Experience Platform
title: Criar uma conexão de origem do Azure Data Explorer na interface
type: Tutorial
description: Saiba como criar uma conexão de origem do Azure Data Explorer usando a interface do Adobe Experience Platform.
exl-id: 561bf948-fc92-4401-8631-e2a408667507
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 1%

---

# Criar um [!DNL Azure Data Explorer] conexão de origem na interface

Os conectores de origem no Adobe Experience Platform fornecem a capacidade de assimilar dados originados externamente de forma programada. Este tutorial fornece etapas para a criação de um [!DNL Azure Data Explorer] (a seguir designado por &quot;[!DNL Data Explorer]&quot;) conector de origem usando o [!DNL Platform] interface do usuário.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): o quadro normalizado pelo qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas da composição do esquema](../../../../../xdm/schema/composition.md): saiba mais sobre os componentes básicos dos esquemas XDM, incluindo princípios fundamentais e práticas recomendadas na composição do esquema.
   * [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.

Se você já tiver um [!DNL Data Explorer] conexão, você pode ignorar o restante deste documento e prosseguir para o tutorial em [configuração de um fluxo de dados](../../dataflow/databases.md).

### Coletar credenciais necessárias

Para acessar seu [!DNL Data Explorer] conta em [!DNL Platform], você deve fornecer os seguintes valores:

| Credencial | Descrição |
| ---------- | ----------- |
| `endpoint` | O endpoint do [!DNL Data Explorer] servidor. |
| `database` | O nome do [!DNL Data Explorer] banco de dados. |
| `tenant` | A ID de locatário exclusiva usada para se conectar à [!DNL Data Explorer] banco de dados. |
| `servicePrincipalId` | A ID da entidade de serviço exclusiva usada para se conectar ao [!DNL Data Explorer] banco de dados. |
| `servicePrincipalKey` | A chave principal de serviço exclusiva usada para se conectar ao [!DNL Data Explorer] banco de dados. |

Para obter mais informações sobre a introdução, consulte [este [!DNL Data Explorer] documento](https://docs.microsoft.com/en-us/azure/data-explorer/kusto/management/access-control/how-to-authenticate-with-aad).

## Conecte seu [!DNL Azure Data Explorer] account

Depois de obter as credenciais necessárias, siga as etapas abaixo para vincular [!DNL Data Explorer] conta para [!DNL Platform].

Efetue logon no [Adobe Experience Platform](https://platform.adobe.com) e selecione **[!UICONTROL Origens]** na barra de navegação esquerda, para acessar a **[!UICONTROL Origens]** espaço de trabalho. A variável **[!UICONTROL Catálogo]** exibe uma variedade de fontes para as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

No **[!UICONTROL Bancos de dados]** categoria, selecione **[!UICONTROL Data Explorer do Azure]**. Se esta for a primeira vez que você usa este conector, selecione **[!UICONTROL Configurar]**. Caso contrário, selecione **[!UICONTROL Adicionar dados]** para criar um novo conector do Data Explorer.

![catálogo](../../../../images/tutorials/create/data-explorer/catalog.png)

A variável **[!UICONTROL Conectar-se ao Azure Data Explorer]** é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Nova conta

Se estiver usando novas credenciais, selecione **[!UICONTROL Nova conta]**. No formulário de entrada que aparece, forneça um nome, uma descrição opcional e [!DNL Data Explorer] credenciais. Quando terminar, selecione **[!UICONTROL Conectar]** e aguarde algum tempo para estabelecer a nova conexão.

![conectar](../../../../images/tutorials/create/data-explorer/new.png)

### Conta existente

Para conectar uma conta existente, selecione a [!DNL Data Explorer] conta à qual deseja se conectar e selecione **[!UICONTROL Próxima]** para continuar.

![existente](../../../../images/tutorials/create/data-explorer/existing.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com o seu [!DNL Data Explorer] conta. Agora você pode seguir para o próximo tutorial e [configurar um fluxo de dados para trazer dados para o [!DNL Platform]](../../dataflow/databases.md).
