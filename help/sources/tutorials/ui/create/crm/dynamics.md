---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Criar um conector de origem do Microsoft Dynamics na interface do usuário
topic: overview
translation-type: tm+mt
source-git-commit: 44c43afc653c147fa12e3e962904bfc79ee0fc64
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 1%

---


# Criar um conector de origem do Microsoft Dynamics na interface do usuário

Os conectores de origem na plataforma Adobe Experience fornecem a capacidade de assimilar dados CRM de origem externa de forma programada. Este tutorial fornece etapas para a criação de um conector de origem do Microsoft Dynamics (a seguir denominado &quot;Dinâmico&quot;) usando a interface do usuário da Plataforma.

## Introdução

Este tutorial requer uma compreensão prática dos seguintes componentes da Adobe Experience Platform:

* [Sistema](../../../../../xdm/home.md)do Experience Data Model (XDM): A estrutura padronizada pela qual a plataforma Experience organiza os dados da experiência do cliente.
   * [Noções básicas da composição](../../../../../xdm/schema/composition.md)do schema: Saiba mais sobre os elementos básicos dos schemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   * [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md)do Editor de Schemas: Saiba como criar schemas personalizados usando a interface do editor de Schemas.
* [Perfil](../../../../../profile/home.md)do cliente em tempo real: Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.

Se você já tiver uma conta dinâmica válida, poderá ignorar o restante deste documento e prosseguir para o tutorial sobre como [configurar um fluxo de dados](../../dataflow/crm.md).

### Reunir credenciais obrigatórias

| Credencial | Descrição |
| ---------- | ----------- |
| `serviceUri` | O URL de serviço da sua instância do Dynamics. |
| `username` | O nome de usuário da sua conta de usuário do Dynamics. |
| `password` | A senha da sua conta do Dynamics. |

Para obter mais informações sobre a introdução, visite [este documento](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth)do Dynamics.

## Conectar sua conta do Dynamics

Depois de coletar as credenciais necessárias, siga as etapas abaixo para criar uma nova conta do Dynamics para conectar-se ao Platform.

Faça logon na [Adobe Experience Platform](https://platform.adobe.com) e selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar a área de trabalho *[!UICONTROL Fontes]* . A tela *[!UICONTROL Catálogo]* exibe várias fontes nas quais você pode criar uma conta de entrada e cada fonte mostra o número de contas e fluxos de conjunto de dados associados a elas.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Na categoria *[!UICONTROL Bancos]* de Dados, selecione **[!UICONTROL Dinâmicas]** , clique **no ícone + (+)** para criar um novo conector Dinâmico.

![catálogo](../../../../images/tutorials/create/ms-dynamics/catalog.png)

A página *[!UICONTROL Conectar-se ao Dynamics]* é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Nova conta

Se você estiver usando novas credenciais, selecione **[!UICONTROL Nova conta]**. No formulário de entrada exibido, forneça à conexão um nome, uma descrição opcional e suas credenciais do Dynamics. Quando terminar, selecione **[!UICONTROL Connect]** e aguarde algum tempo para a nova conta ser estabelecida.

![connect](../../../../images/tutorials/create/ms-dynamics/new.png)

### Conta existente

Para conectar uma conta existente, selecione a conta Dinâmica com a qual deseja se conectar e, em seguida, selecione **[!UICONTROL Próximo]** no canto superior direito para continuar.

![existente](../../../../images/tutorials/create/ms-dynamics/existing.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com sua conta do Dynamics. Agora você pode continuar com o próximo tutorial e [configurar um fluxo de dados para trazer dados para a Plataforma](../../dataflow/crm.md).