---
keywords: Experience Platform;home;popular topics;Salesforce;salesforce
solution: Experience Platform
title: Criar um conector de origem do Salesforce na interface do usuário
topic: overview
description: Este tutorial fornece etapas para a criação de um conector de origem do Salesforce usando a interface do usuário da plataforma.
translation-type: tm+mt
source-git-commit: f82dfee2c75a0b8b2ec1615266780b309152ead4
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 1%

---


# Criar um conector [!DNL Salesforce] de origem na interface do usuário

Os conectores de origem na Adobe Experience Platform fornecem a capacidade de assimilar dados CRM de origem externa de forma programada. Este tutorial fornece etapas para criar um conector de [!DNL Salesforce] origem usando a interface do [!DNL Platform] usuário.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Experience Data Model] (XDM) Sistema](../../../../../xdm/home.md): A estrutura padronizada pela qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas da composição](../../../../../xdm/schema/composition.md)do schema: Saiba mais sobre os elementos básicos dos schemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   * [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md)do Editor de schemas: Saiba como criar schemas personalizados usando a interface do editor de Schemas.
* [[!DNL Perfil do cliente em tempo real]](../../../../../profile/home.md): Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.

Se você já tiver uma [!DNL Salesforce] conta válida, poderá ignorar o restante deste documento e prosseguir para o tutorial sobre como [configurar um fluxo de dados](../../dataflow/crm.md).

### Reunir credenciais obrigatórias

| Credencial | Descrição |
| ---------- | ----------- |
| `environmentUrl` | O URL da instância de [!DNL Salesforce] origem. |
| `username` | O nome de usuário da conta de [!DNL Salesforce] usuário. |
| `password` | A senha da conta de [!DNL Salesforce] usuário. |
| `securityToken` | O token de segurança da conta de [!DNL Salesforce] usuário. |

Para obter mais informações sobre a introdução, consulte [este documento](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/intro_understanding_authentication.htm)do Salesforce.

## Conectar sua [!DNL Salesforce] conta

Depois de reunir as credenciais necessárias, siga as etapas abaixo para vincular sua [!DNL Salesforce] conta a [!DNL Platform].

Faça logon no [Adobe Experience Platform](https://platform.adobe.com) e selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar a área de trabalho **[!UICONTROL Fontes]** . A tela **[!UICONTROL Catálogo]** exibe várias fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Na categoria **[!UICONTROL Bancos]** de dados, selecione **[!UICONTROL Salesforce]**. Se esta for a sua primeira vez usando este conector, selecione **[!UICONTROL Configurar]**. Caso contrário, selecione **[!UICONTROL Adicionar dados]** para criar um novo conector Salesforce.

![catálogo](../../../../images/tutorials/create/salesforce/catalog.png)

A página **[!UICONTROL Conectar-se ao Salesforce]** é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Nova conta

Se você estiver usando novas credenciais, selecione **[!UICONTROL Nova conta]**. No formulário de entrada exibido, forneça um nome, uma descrição opcional e suas [!DNL Salesforce] credenciais. Quando terminar, selecione **[!UICONTROL Connect]** e aguarde algum tempo para a nova conexão ser estabelecida.

![connect](../../../../images/tutorials/create/salesforce/new.png)

### Conta existente

Para conectar uma conta existente, selecione a [!DNL Salesforce] conta à qual deseja se conectar e, em seguida, selecione **[!UICONTROL Próximo]** no canto superior direito para continuar.

![existente](../../../../images/tutorials/create/salesforce/existing.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com sua [!DNL Salesforce] conta. Agora você pode continuar para o próximo tutorial e [configurar um fluxo de dados para trazer [!DNL Platform]](../../dataflow/crm.md)os dados para o