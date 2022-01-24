---
keywords: Experience Platform, home, tópicos populares, salesforce marketing cloud, Salesforce Marketing Cloud
solution: Experience Platform
title: Criar uma conexão de fonte de Marketing Cloud do Salesforce na interface do usuário
topic-legacy: overview
type: Tutorial
description: Saiba como criar uma conexão de origem do Marketing Cloud do Salesforce usando a interface do usuário do Adobe Experience Platform.
exl-id: 1d9bde60-31e0-489c-9c1c-b6471e0ea554
source-git-commit: 531d5619e0643b6195abaa53d1708e0368d45871
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 1%

---

# Crie um [!DNL Salesforce Marketing Cloud] conexão de origem na interface do usuário

>[!NOTE]
>
> O [!DNL Salesforce Marketing Cloud] A fonte está em beta. Consulte a [visão geral das fontes](../../../../home.md#terms-and-conditions) para obter mais informações sobre o uso de fontes com rótulo beta.

Os conectores de origem no Adobe Experience Platform oferecem a capacidade de assimilar dados de origem externa de acordo com a programação. Este tutorial fornece etapas para criar um [!DNL Salesforce Marketing Cloud] conector de origem usando a interface do usuário da plataforma.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): O quadro normalizado pelo qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas da composição do schema](../../../../../xdm/schema/composition.md): Saiba mais sobre os elementos básicos dos esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   * [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Fornece um perfil de consumidor unificado e em tempo real com base em dados agregados de várias fontes.

Se você já tiver uma [!DNL Salesforce Marketing Cloud] , você pode ignorar o restante deste documento e prosseguir para o tutorial em [configuração de um fluxo de dados](../../dataflow/marketing-automation.md).

### Obter credenciais necessárias

Para acessar o [!DNL Salesforce Marketing Cloud] na Platform, você deve fornecer os seguintes valores:

| Credencial | Descrição |
| ---------- | ----------- |
| `host` | O servidor host do seu aplicativo. Esse é frequentemente o seu subdomínio. **Observação:** Ao inserir sua `host` , é necessário especificar apenas o subdomínio e não o URL inteiro. Por exemplo, se o URL do host for `https://abcd-ab12c3d4e5fg6hijk7lmnop8qrst.auth.marketingcloudapis.com/`, então você só precisa inserir `abcd-ab12c3d4e5fg6hijk7lmnop8qrst` como seu valor de host. |
| `clientId` | A ID do cliente associada à [!DNL Salesforce Marketing Cloud] aplicativo. |
| `clientSecret` | O segredo do cliente associado ao seu [!DNL Salesforce Marketing Cloud] aplicativo. |

Para obter mais informações sobre a introdução, consulte esta seção [[!DNL Salesforce Marketing Cloud] documento](https://developer.salesforce.com/docs/atlas.en-us.mc-apis.meta/mc-apis/authentication.htm).

## Conecte seu [!DNL Salesforce Marketing Cloud] account

Depois de reunir suas credenciais necessárias, siga as etapas abaixo para vincular seus [!DNL Salesforce Marketing Cloud] para a Platform.

Na interface do usuário da plataforma, selecione **[!UICONTROL Fontes]** na navegação à esquerda para acessar o [!UICONTROL Fontes] espaço de trabalho. O [!UICONTROL Catálogo] exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Você também pode usar a barra de pesquisa para restringir os conectores exibidos.

Em [!UICONTROL Automação de marketing] categoria , selecione **[!UICONTROL Marketing Cloud Salesforce]** e depois selecione **[!UICONTROL Configurar]**.

![catálogo](../../../../images/tutorials/create/salesforce-marketing-cloud/catalog.png)

O **[!UICONTROL Conectar-se ao Marketing Cloud Salesforce]** será exibida. Nesta página, você pode usar novas credenciais ou credenciais existentes.

### Nova conta

Se estiver usando novas credenciais, selecione **[!UICONTROL Nova conta]**. No formulário de entrada exibido, forneça um nome, uma descrição opcional e [!DNL Salesforce Marketing Cloud] credenciais. Quando terminar, selecione **[!UICONTROL Connect]** e, em seguida, permitir que a nova conexão seja estabelecida.

![novo](../../../../images/tutorials/create/salesforce-marketing-cloud/new.png)

### Conta existente

Para conectar uma conta existente, selecione a [!DNL Salesforce Marketing Cloud] conta com a qual deseja se conectar e selecione **[!UICONTROL Próximo]** para continuar.

![existente](../../../../images/tutorials/create/salesforce-marketing-cloud/existing.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com seu [!DNL Salesforce Marketing Cloud] conta. Agora você pode continuar para o próximo tutorial e [configurar um fluxo de dados para trazer os dados do sistema de automação de marketing para a plataforma](../../dataflow/marketing-automation.md).
