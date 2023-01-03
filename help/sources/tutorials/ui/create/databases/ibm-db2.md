---
keywords: Experience Platform, home, tópicos populares, DB2, db2, IBM DB2, ibm db2
solution: Experience Platform
title: Criar uma conexão de origem IBM DB2 na interface do usuário
topic-legacy: overview
type: Tutorial
description: Saiba como criar uma conexão de origem IBM DB2 usando a interface do usuário do Adobe Experience Platform.
exl-id: 69c99f94-9cb9-43ff-9315-ce166ab35a60
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 0%

---

# Criar uma conexão de origem IBM DB2 na interface do usuário

>[!NOTE]
>
> O conector IBM DB2 está em beta. Consulte a [Visão geral das fontes](../../../../home.md#terms-and-conditions) para obter mais informações sobre o uso de conectores com rótulo beta.

Os conectores de origem no Adobe Experience Platform oferecem a capacidade de assimilar dados de origem externa de acordo com a programação. Este tutorial fornece etapas para a criação de um conector de origem IBM DB2 (a seguir denominado &quot;DB2&quot;) usando o [!DNL Platform] interface do usuário.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): O quadro normalizado pelo qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas da composição do schema](../../../../../xdm/schema/composition.md): Saiba mais sobre os elementos básicos dos esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   * [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Fornece um perfil de consumidor unificado e em tempo real com base em dados agregados de várias fontes.

Se você já tiver uma conexão válida do DB2, poderá ignorar o restante deste documento e prosseguir para o tutorial em [configuração de um fluxo de dados](../../dataflow/databases.md).

### Obter credenciais necessárias

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito ao DB2 usando o [!DNL Flow Service] API.

| Credencial | Descrição |
| ---------- | ----------- |
| `server` | O nome do servidor DB2. Você pode especificar o número da porta seguindo o nome do servidor delimitado por dois pontos. Por exemplo: server:port. |
| `database` | O nome do banco de dados DB2. |
| `username` | O nome de usuário usado para se conectar ao banco de dados DB2. |
| `password` | A senha da conta de usuário especificada para o nome de usuário. |

Para obter mais informações sobre a introdução, consulte [este documento DB2](https://www.ibm.com/support/knowledgecenter/SSFMBX/com.ibm.swg.im.dashdb.doc/connecting/connect_credentials.html).

## Conecte sua conta IBM DB2

Depois de coletar suas credenciais necessárias, siga as etapas abaixo para vincular sua conta do DB2 a [!DNL Platform].

Faça logon em [Adobe Experience Platform](https://platform.adobe.com) e depois selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar o **[!UICONTROL Fontes]** espaço de trabalho. O **[!UICONTROL Catálogo]** exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Em **[!UICONTROL Bancos de dados]** categoria , selecione **[!UICONTROL IBM DB2]**. Se esta for a primeira vez que você usa esse conector, selecione **[!UICONTROL Configurar]**. Caso contrário, selecione **[!UICONTROL Adicionar dados]** para criar um novo conector DB2.

![catálogo](../../../../images/tutorials/create/ibm-db2/catalog.png)

O **[!UICONTROL Conectar-se ao IBM DB2]** será exibida. Nesta página, você pode usar novas credenciais ou credenciais existentes.

### Nova conta

Se estiver usando novas credenciais, selecione **[!UICONTROL Nova conta]**. No formulário de entrada exibido, forneça um nome, uma descrição opcional e suas credenciais do DB2. Quando terminar, selecione **[!UICONTROL Connect]** e, em seguida, permitir que a nova conexão seja estabelecida.

![connect](../../../../images/tutorials/create/ibm-db2/new.png)

### Conta existente

Para conectar uma conta existente, selecione a conta DB2 à qual deseja se conectar e selecione **[!UICONTROL Próximo]** para continuar.

![existente](../../../../images/tutorials/create/ibm-db2/existing.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com sua conta DB2. Agora você pode continuar para o próximo tutorial e [configurar um fluxo de dados para trazer os dados para [!DNL Platform]](../../dataflow/databases.md).
