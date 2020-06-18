---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Criar um conector de origem da Salesforce Service Cloud na interface do usuário
topic: overview
translation-type: tm+mt
source-git-commit: cada7c7eff7597015caa7333559bef16a59eab65
workflow-type: tm+mt
source-wordcount: '543'
ht-degree: 0%

---


# Criar um conector de origem da Salesforce Service Cloud na interface do usuário

>[!NOTE]
>O conector da Salesforce Service Cloud está em beta. Consulte a visão geral [das](../../../../home.md#terms-and-conditions) Fontes para obter mais informações sobre o uso de conectores com rótulo beta.

Os conectores de origem no Adobe Experience Platform fornecem a capacidade de assimilar dados de origem externa de forma programada. Este tutorial fornece etapas para a criação de um conector de origem do Salesforce Service Cloud (a seguir denominado &quot;SSC&quot;) usando a interface do usuário do Platform.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Sistema](../../../../../xdm/home.md)do Experience Data Model (XDM): A estrutura padronizada pela qual o Experience Platform organiza os dados de experiência do cliente.
   * [Noções básicas da composição](../../../../../xdm/schema/composition.md)do schema: Saiba mais sobre os elementos básicos dos schemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   * [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md)do Editor de Schemas: Saiba como criar schemas personalizados usando a interface do editor de Schemas.
* [Perfil](../../../../../profile/home.md)do cliente em tempo real: Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.

Se você já tiver uma conexão SSC válida, poderá ignorar o restante deste documento e prosseguir para o tutorial sobre como [configurar um fluxo de dados](../../dataflow/customer-success.md)

### Reunir credenciais obrigatórias

Para acessar sua conta SSC no Platform, forneça os seguintes valores:

| Credencial | Descrição |
| ---------- | ----------- |
| `username` | O nome de usuário da conta de usuário. |
| `password` | A senha da conta de usuário. |
| `securityToken` | O token de segurança da conta de usuário. |

Para obter mais informações sobre a introdução, consulte [este documento](https://developer.salesforce.com/docs/atlas.en-us.api_iot.meta/api_iot/qs_auth_access_token.htm)da Salesforce Service Cloud.

## Conectar sua conta da Salesforce Service Cloud

Depois de reunir as credenciais necessárias, siga as etapas abaixo para criar uma nova conta SSC para se conectar ao Platform.

Faça logon no <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> e selecione **Fontes** na barra de navegação esquerda para acessar a área de trabalho *Fontes* . A tela *Catálogo* exibe várias fontes para as quais você pode criar uma conta de entrada, e cada fonte mostra o número de contas e fluxos de conjunto de dados existentes associados a elas.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Na categoria *Customer Success (Sucesso* do cliente), selecione **Salesforce Service Cloud** para exibir uma barra de informações no lado direito da tela. A barra de informações fornece uma breve descrição para a fonte selecionada, bem como opções para se conectar à fonte ou à sua documentação de visualização. Para criar uma nova conexão de entrada, selecione Origem **do** Connect.

![catálogo](../../../../images/tutorials/create/ssc/catalog.png)

A página *Conectar-se ao Salesforce Service Cloud* é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Nova conta

Se você estiver usando novas credenciais, selecione **Nova conta**. No formulário de entrada exibido, forneça à conexão um nome, uma descrição opcional e suas credenciais do SSC. Quando terminar, selecione **Connect** e aguarde algum tempo para a nova conta ser estabelecida.

![connect](../../../../images/tutorials/create/ssc/connect.png)

### Conta existente

Para conectar uma conta existente, selecione a conta SSC à qual deseja se conectar e, em seguida, selecione **Avançar** para continuar.

![existente](../../../../images/tutorials/create/ssc/existing.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com sua conta SSC. Agora você pode continuar para o próximo tutorial e [configurar um fluxo de dados para trazer os dados de sucesso do cliente para o Platform](../../dataflow/customer-success.md).