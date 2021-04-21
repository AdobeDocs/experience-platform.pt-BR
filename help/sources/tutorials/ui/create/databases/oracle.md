---
keywords: Experience Platform, home, tópicos populares, Oracle DB, oracle db
solution: Experience Platform
title: Criar uma conexão de origem de banco de dados do Oracle na interface do usuário
topic-legacy: overview
type: Tutorial
description: Saiba como criar uma conexão de origem de banco de dados do Oracle usando a interface do usuário do Adobe Experience Platform.
exl-id: 4ca6ecc6-0382-4cee-acc5-1dec7eeb9443
translation-type: tm+mt
source-git-commit: b2384bfe26fa3d111c342062b2d9bb37c4226857
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 1%

---

# Criar uma conexão de origem [!DNL Oracle DB] na interface do usuário

Os conectores de origem no Adobe Experience Platform oferecem a capacidade de assimilar dados de origem externa de acordo com a programação. Este tutorial fornece etapas para criar um conector de origem [!DNL Oracle DB] usando a interface do usuário [!DNL Platform].

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): A estrutura padronizada pela qual  [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas da composição](../../../../../xdm/schema/composition.md) do schema: Saiba mais sobre os elementos básicos dos esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   * [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md) do Editor de esquema: Saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Fornece um perfil de consumidor unificado e em tempo real com base em dados agregados de várias fontes.

Se você já tiver uma conexão válida [!DNL Oracle DB], poderá ignorar o restante deste documento e prosseguir para o tutorial em [configurar um fluxo de dados](../../dataflow/databases.md).

### Obter credenciais necessárias

Para acessar sua conta [!DNL Oracle DB] em [!DNL Platform], você deve fornecer os seguintes valores:

| Credencial | Descrição |
| ---------- | ----------- |
| `connectionString` | A cadeia de conexão usada para se conectar a [!DNL Oracle DB]. O padrão da string de conexão [!DNL Oracle DB] é: `Host={HOST};Port={PORT};Sid={SID};User Id={USERNAME};Password={PASSWORD}`. |
| `connectionSpec.id` | O identificador exclusivo necessário para criar uma conexão. A ID de especificação de conexão para [!DNL Oracle DB] é `d6b52d86-f0f8-475f-89d4-ce54c8527328`. |

Para obter mais informações sobre a introdução, consulte [este documento do Oracle](https://docs.oracle.com/database/121/ODPNT/featConnecting.htm#ODPNT199).

## Conecte sua conta [!DNL Oracle DB]

Depois de coletar suas credenciais necessárias, siga as etapas abaixo para vincular sua conta [!DNL Oracle DB] para se conectar a [!DNL Platform].

Faça logon em [Adobe Experience Platform](https://platform.adobe.com) e selecione **[!UICONTROL Sources]** na barra de navegação esquerda para acessar o espaço de trabalho **[!UICONTROL Sources]**. A tela **[!UICONTROL Catalog]** exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Na categoria **[!UICONTROL Databases]**, selecione **[!UICONTROL Oracle DB]**. Se esta for a primeira vez que você usa esse conector, selecione **[!UICONTROL Configure]**. Caso contrário, selecione **[!UICONTROL Add data]** para criar um novo conector [!DNL Oracle DB].

![catálogo](../../../../images/tutorials/create/oracle/catalog.png)

A página **[!UICONTROL Connect to Oracle DB]** é exibida. Nesta página, você pode usar novas credenciais ou credenciais existentes.

### Nova conta

Se estiver usando novas credenciais, selecione **[!UICONTROL New account]**. No formulário de entrada exibido, forneça um nome, uma descrição opcional e suas credenciais [!DNL Oracle DB]. Quando terminar, selecione **[!UICONTROL Connect]** e aguarde algum tempo para que a nova conexão seja estabelecida.

![connect](../../../../images/tutorials/create/oracle/new.png)

### Conta existente

Para conectar uma conta existente, selecione a conta [!DNL Oracle DB] com a qual deseja se conectar e selecione **[!UICONTROL Next]** para prosseguir.

![existente](../../../../images/tutorials/create/oracle/existing.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com sua conta [!DNL Oracle DB]. Agora você pode continuar para o próximo tutorial e [configurar um fluxo de dados para trazer dados para [!DNL Platform]](../../dataflow/databases.md).
