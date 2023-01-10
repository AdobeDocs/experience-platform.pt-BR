---
keywords: Experience Platform, home, tópicos populares, Salesforce Service Cloud, salesforce service cloud
solution: Experience Platform
title: Criar uma conexão de origem da nuvem do Salesforce Service na interface do usuário
type: Tutorial
description: Saiba como criar uma conexão de origem do Salesforce Service Cloud usando a interface do usuário do Adobe Experience Platform.
exl-id: 38480a29-7852-46c6-bcea-5dc6bffdbd15
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 1%

---

# Crie um [!DNL Salesforce Service Cloud] conexão de origem na interface do usuário

Os conectores de origem no Adobe Experience Platform oferecem a capacidade de assimilar dados de origem externa de acordo com a programação. Este tutorial fornece etapas para criar um [!DNL Salesforce Service Cloud] Conector de fonte (a seguir designado &quot;SSC&quot;) usando o [!DNL Platform] interface do usuário.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): O quadro normalizado pelo qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas da composição do schema](../../../../../xdm/schema/composition.md): Saiba mais sobre os elementos básicos dos esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   * [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Fornece um perfil de consumidor unificado e em tempo real com base em dados agregados de várias fontes.

Se você já tiver uma conexão SSC válida, ignore o restante deste documento e prossiga para o tutorial em [configuração de um fluxo de dados](../../dataflow/customer-success.md)

### Obter credenciais necessárias

Para acessar sua conta do SSC em [!DNL Platform], você deve fornecer os seguintes valores:

| Credencial | Descrição |
| ---------- | ----------- |
| `username` | O nome de usuário da conta de usuário. |
| `password` | A senha da conta de usuário. |
| `securityToken` | O token de segurança da conta do usuário. |

Para obter mais informações sobre a introdução, consulte [this [!DNL Salesforce Service Cloud] documento](https://developer.salesforce.com/docs/atlas.en-us.api_iot.meta/api_iot/qs_auth_access_token.htm).

## Conecte seu [!DNL Salesforce Service Cloud] account

Depois de coletar suas credenciais necessárias, siga as etapas abaixo para vincular sua conta do SSC a [!DNL Platform].

Faça logon em [Adobe Experience Platform](https://platform.adobe.com) e depois selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar o **[!UICONTROL Fontes]** espaço de trabalho. O **[!UICONTROL Catálogo]** exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Em **[!UICONTROL Sucesso do cliente]** categoria , selecione **[!UICONTROL Salesforce Service Cloud]**. Se esta for a primeira vez que você usa esse conector, selecione **[!UICONTROL Configurar]**. Caso contrário, selecione **[!UICONTROL Adicionar dados]** para criar um novo conector SSC.

![catálogo](../../../../images/tutorials/create/ssc/catalog.png)

O **[!UICONTROL Conectar-se à Salesforce Service Cloud]** será exibida. Nesta página, você pode usar novas credenciais ou credenciais existentes.

### Nova conta

Se estiver usando novas credenciais, selecione **[!UICONTROL Nova conta]**. No formulário de entrada exibido, forneça um nome, uma descrição opcional e suas credenciais do SSC. Quando terminar, selecione **[!UICONTROL Connect]** e, em seguida, permitir que a nova conexão seja estabelecida.

![connect](../../../../images/tutorials/create/ssc/connect.png)

### Conta existente

Para conectar uma conta existente, selecione a conta do SSC à qual deseja se conectar e selecione **[!UICONTROL Próximo]** para continuar.

![existente](../../../../images/tutorials/create/ssc/existing.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com sua conta do SSC. Agora você pode continuar para o próximo tutorial e [configurar um fluxo de dados para trazer os dados de sucesso do cliente para [!DNL Platform]](../../dataflow/customer-success.md).
