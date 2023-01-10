---
keywords: Experience Platform, home, tópicos populares, Phoenix, phonix
solution: Experience Platform
title: Criar uma conexão de origem Phoenix na interface do usuário
type: Tutorial
description: Saiba como criar uma conexão de origem Phoenix usando a interface do usuário do Adobe Experience Platform.
exl-id: 2ed469bc-1c72-4f04-a5f0-6a0bb519a6c2
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '520'
ht-degree: 0%

---

# Crie um [!DNL Phoenix] conexão de origem na interface do usuário

>[!NOTE]
>
> O [!DNL Phoenix] O conector está em beta. Consulte a [Visão geral das fontes](../../../../home.md#terms-and-conditions) para obter mais informações sobre o uso de conectores com rótulo beta.

Os conectores de origem no Adobe Experience Platform oferecem a capacidade de assimilar dados de origem externa de acordo com a programação. Este tutorial fornece etapas para criar um [!DNL Phoenix] conector de origem usando o [!DNL Platform] interface do usuário.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): O quadro normalizado pelo qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas da composição do schema](../../../../../xdm/schema/composition.md): Saiba mais sobre os elementos básicos dos esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   * [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Fornece um perfil de consumidor unificado e em tempo real com base em dados agregados de várias fontes.

Se você já tiver um [!DNL Phoenix] , você pode ignorar o restante deste documento e prosseguir para o tutorial em [configuração de um fluxo de dados](../../dataflow/databases.md)

### Obter credenciais necessárias

Para acessar o [!DNL Phoenix] conta em [!DNL Platform], você deve fornecer os seguintes valores:

| Credencial | Descrição |
| ---------- | ----------- |
| `host` | O endereço IP ou o nome do host do [!DNL Phoenix] servidor. |
| `port` | A porta TCP que [!DNL Phoenix] O servidor usa o para detectar as conexões do cliente. Se você se conectar a [!DNL Azure HDInsights], especifique a porta como 443. |
| `httpPath` | O URL parcial correspondente ao [!DNL Phoenix] servidor. Especifique /hbasephonix0 se estiver usando o [!DNL Azure HDInsights] cluster. |
| `username` | O nome de usuário usado para acessar o [!DNL Phoenix] servidor. |
| `password` | A senha que corresponde ao usuário. |
| `enableSsl` | Um botão que especifica se as conexões com o servidor são criptografadas usando SSL. |

Para obter mais informações sobre a introdução, consulte [this [!DNL Phoenix] documento](https://python-phoenixdb.readthedocs.io/en/latest/api.html).

## Conecte seu [!DNL Phoenix] account

Depois de reunir suas credenciais necessárias, siga as etapas abaixo para vincular seus [!DNL Phoenix] conta à qual se conectar [!DNL Platform].

Faça logon em [Adobe Experience Platform](https://platform.adobe.com) e depois selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar o **[!UICONTROL Fontes]** espaço de trabalho. O **[!UICONTROL Catálogo]** exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Em **[!UICONTROL Bancos de dados]** categoria , selecione **[!UICONTROL Phoenix]**. Se esta for a primeira vez que você usa esse conector, selecione **[!UICONTROL Configurar]**. Caso contrário, selecione **[!UICONTROL Adicionar dados]** para criar um novo [!DNL Phoenix] conta.

![catálogo](../../../../images/tutorials/create/phoenix/catalog.png)

O **[!UICONTROL Conecte-se a Phoenix]** será exibida. Nesta página, você pode usar novas credenciais ou credenciais existentes.

### Nova conta

Se estiver usando novas credenciais, selecione **[!UICONTROL Nova conta]**. No formulário de entrada exibido, forneça um nome, uma descrição opcional e [!DNL Phoenix] credenciais. Quando terminar, selecione **[!UICONTROL Connect]** e, em seguida, permitir que a nova conexão seja estabelecida.

![connect](../../../../images/tutorials/create/phoenix/new.png)

### Conta existente

Para conectar uma conta existente, selecione a [!DNL Phoenix] conta com a qual deseja se conectar e selecione **[!UICONTROL Próximo]** para continuar.

![existente](../../../../images/tutorials/create/phoenix/existing.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com seu [!DNL Phoenix] conta. Agora você pode continuar para o próximo tutorial e [configurar um fluxo de dados para trazer os dados para [!DNL Platform]](../../dataflow/databases.md).
