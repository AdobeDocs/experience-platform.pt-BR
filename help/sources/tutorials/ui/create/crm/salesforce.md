---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Criar um conector de origem do Salesforce na interface do usuário
topic: overview
translation-type: tm+mt
source-git-commit: 44c43afc653c147fa12e3e962904bfc79ee0fc64
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 1%

---


# Criar um conector de origem do Salesforce na interface do usuário

Os conectores de origem na plataforma Adobe Experience fornecem a capacidade de assimilar dados CRM de origem externa de forma programada. Este tutorial fornece etapas para a criação de um conector de origem do Salesforce usando a interface do usuário da plataforma.

## Introdução

Este tutorial requer uma compreensão prática dos seguintes componentes da Adobe Experience Platform:

* [Sistema](../../../../../xdm/home.md)do Experience Data Model (XDM): A estrutura padronizada pela qual a plataforma Experience organiza os dados da experiência do cliente.
   * [Noções básicas da composição](../../../../../xdm/schema/composition.md)do schema: Saiba mais sobre os elementos básicos dos schemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   * [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md)do Editor de Schemas: Saiba como criar schemas personalizados usando a interface do editor de Schemas.
* [Perfil](../../../../../profile/home.md)do cliente em tempo real: Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.

Se você já tiver uma conta Salesforce válida, poderá ignorar o restante deste documento e prosseguir para o tutorial sobre como [configurar um fluxo de dados](../../dataflow/crm.md).

### Reunir credenciais obrigatórias

| Credencial | Descrição |
| ---------- | ----------- |
| `environmentUrl` | O URL da instância de origem do Salesforce. |
| `username` | O nome de usuário da conta de usuário do Salesforce. |
| `password` | A senha da conta de usuário do Salesforce. |
| `securityToken` | O token de segurança da conta de usuário do Salesforce. |

Para obter mais informações sobre como começar, visite [este documento](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/intro_understanding_authentication.htm)do Salesforce.

## Conectar sua conta do Salesforce

Depois de reunir as credenciais necessárias, siga as etapas abaixo para criar uma nova conta do Salesforce para se conectar à Plataforma.

Faça logon na [Adobe Experience Platform](https://platform.adobe.com) e selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar a área de trabalho *[!UICONTROL Fontes]* . A tela *[!UICONTROL Catálogo]* exibe várias fontes nas quais você pode criar uma conta de entrada e cada fonte mostra o número de contas e fluxos de conjunto de dados associados a elas.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Na categoria *[!UICONTROL Bancos]* de dados, selecione **[!UICONTROL Salesforce]** click **no ícone + (+)** para criar um novo conector Salesforce.

![catálogo](../../../../images/tutorials/create/salesforce/catalog.png)

A página *[!UICONTROL Conectar-se ao Salesforce]* é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Nova conta

Se você estiver usando novas credenciais, selecione **[!UICONTROL Nova conta]**. No formulário de entrada exibido, forneça à conexão um nome, uma descrição opcional e suas credenciais do Salesforce. Quando terminar, selecione **[!UICONTROL Connect]** e aguarde algum tempo para a nova conta ser estabelecida.

![connect](../../../../images/tutorials/create/salesforce/new.png)

### Conta existente

Para conectar uma conta existente, selecione a conta do Salesforce com a qual deseja se conectar e, em seguida, selecione **[!UICONTROL Próximo]** no canto superior direito para prosseguir.

![existente](../../../../images/tutorials/create/salesforce/existing.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com sua conta Salesforce. Agora você pode continuar com o próximo tutorial e [configurar um fluxo de dados para trazer dados para a Plataforma](../../dataflow/crm.md).