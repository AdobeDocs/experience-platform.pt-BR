---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Criar um conector de origem IBM DB2 na interface do usuário
topic: overview
translation-type: tm+mt
source-git-commit: ec2d0a33e0ae92a3153b7bdcad29734e487a0439
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 0%

---



# Criar um conector de origem IBM DB2 na interface do usuário

>[!NOTE]
> O conector IBM DB2 está em beta. Consulte a visão geral [das](../../../../home.md#terms-and-conditions) Fontes para obter mais informações sobre o uso de conectores com rótulo beta.

Os conectores de origem na Adobe Experience Platform fornecem a capacidade de assimilar dados de origem externa de forma programada. Este tutorial fornece etapas para a criação de um conector de origem IBM DB2 (a seguir denominado &quot;DB2&quot;) usando a interface do [!DNL Platform] usuário.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Experience Data Model] (XDM) Sistema](../../../../../xdm/home.md): A estrutura padronizada pela qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas da composição](../../../../../xdm/schema/composition.md)do schema: Saiba mais sobre os elementos básicos dos schemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   * [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md)do Editor de schemas: Saiba como criar schemas personalizados usando a interface do editor de Schemas.
* [[!DNL Perfil do cliente em tempo real]](../../../../../profile/home.md): Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.

Se você já tiver uma conexão DB2 válida, poderá ignorar o restante desse documento e prosseguir para o tutorial sobre como [configurar um fluxo de dados](../../dataflow/databases.md).

### Reunir credenciais obrigatórias

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito ao DB2 usando a [!DNL Flow Service] API.

| Credencial | Descrição |
| ---------- | ----------- |
| `server` | O nome do servidor DB2. Você pode especificar o número da porta após o nome do servidor delimitado por dois pontos. Por exemplo: server:port. |
| `database` | O nome do banco de dados DB2. |
| `username` | O nome de usuário usado para conexão com o banco de dados DB2. |
| `password` | A senha da conta de usuário especificada para o nome de usuário. |

Para obter mais informações sobre a introdução, consulte [este documento](https://www.ibm.com/support/knowledgecenter/SSFMBX/com.ibm.swg.im.dashdb.doc/connecting/connect_credentials.html)DB2.

## Conecte sua conta IBM DB2

Depois de reunir as credenciais necessárias, siga as etapas abaixo para vincular sua conta DB2 a [!DNL Platform].

Faça logon no [Adobe Experience Platform](https://platform.adobe.com) e selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar a área de trabalho **[!UICONTROL Fontes]** . A tela **[!UICONTROL Catálogo]** exibe várias fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Na categoria **[!UICONTROL Bancos]** de Dados, selecione **[!UICONTROL IBM DB2]**. Se esta for a sua primeira vez usando este conector, selecione **[!UICONTROL Configurar]**. Caso contrário, selecione **[!UICONTROL Adicionar dados]** para criar um novo conector DB2.

![catálogo](../../../../images/tutorials/create/ibm-db2/catalog.png)

A página **[!UICONTROL Conectar-se ao IBM DB2]** é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Nova conta

Se você estiver usando novas credenciais, selecione **[!UICONTROL Nova conta]**. No formulário de entrada exibido, forneça um nome, uma descrição opcional e suas credenciais do DB2. Quando terminar, selecione **[!UICONTROL Connect]** e aguarde algum tempo para a nova conexão ser estabelecida.

![connect](../../../../images/tutorials/create/ibm-db2/new.png)

### Conta existente

Para conectar uma conta existente, selecione a conta DB2 com a qual deseja se conectar e, em seguida, selecione **[!UICONTROL Próximo]** para prosseguir.

![existente](../../../../images/tutorials/create/ibm-db2/existing.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com sua conta DB2. Agora você pode continuar para o próximo tutorial e [configurar um fluxo de dados para trazer [!DNL Platform]](../../dataflow/databases.md)os dados para o