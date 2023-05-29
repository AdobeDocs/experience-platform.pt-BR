---
keywords: Experience Platform;página inicial;tópicos populares;DB2;db2;IBM DB2;ibm db2
solution: Experience Platform
title: Criar uma conexão de origem do IBM DB2 na interface
type: Tutorial
description: Saiba como criar uma conexão de origem do IBM DB2 usando a interface do usuário do Adobe Experience Platform.
exl-id: 69c99f94-9cb9-43ff-9315-ce166ab35a60
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 0%

---

# Criar uma conexão de origem do IBM DB2 na interface

>[!NOTE]
>
> O conector IBM DB2 está na versão beta. Consulte a [Visão geral das fontes](../../../../home.md#terms-and-conditions) para obter mais informações sobre o uso de conectores rotulados com beta.

Os conectores de origem no Adobe Experience Platform fornecem a capacidade de assimilar dados originados externamente de forma programada. Este tutorial fornece etapas para a criação de um conector de origem do IBM DB2 (doravante chamado de &quot;DB2&quot;) usando o [!DNL Platform] interface do usuário.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): o quadro normalizado pelo qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas da composição do esquema](../../../../../xdm/schema/composition.md): saiba mais sobre os componentes básicos dos esquemas XDM, incluindo princípios fundamentais e práticas recomendadas na composição do esquema.
   * [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.

Se você já tiver uma conexão DB2 válida, ignore o restante deste documento e prossiga para o tutorial em [configuração de um fluxo de dados](../../dataflow/databases.md).

### Coletar credenciais necessárias

As seções a seguir fornecem informações adicionais que você precisará saber para se conectar com êxito ao DB2 usando o [!DNL Flow Service] API.

| Credencial | Descrição |
| ---------- | ----------- |
| `server` | O nome do servidor DB2. Você pode especificar o número da porta após o nome do servidor delimitado por dois pontos. Por exemplo: servidor:porta. |
| `database` | O nome do banco de dados DB2. |
| `username` | O nome de usuário usado para conexão com o banco de dados DB2. |
| `password` | A senha da conta de usuário especificada para o nome de usuário. |

Para obter mais informações sobre a introdução, consulte [este documento DB2](https://www.ibm.com/support/knowledgecenter/SSFMBX/com.ibm.swg.im.dashdb.doc/connecting/connect_credentials.html).

## Conectar sua conta do IBM DB2

Depois de obter as credenciais necessárias, siga as etapas abaixo para vincular sua conta DB2 ao [!DNL Platform].

Efetue logon no [Adobe Experience Platform](https://platform.adobe.com) e selecione **[!UICONTROL Origens]** na barra de navegação esquerda, para acessar a **[!UICONTROL Origens]** espaço de trabalho. A variável **[!UICONTROL Catálogo]** A tela exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

No **[!UICONTROL Bancos de dados]** categoria, selecione **[!UICONTROL IBM DB2]**. Se esta for a primeira vez que você usa este conector, selecione **[!UICONTROL Configurar]**. Caso contrário, selecione **[!UICONTROL Adicionar dados]** para criar um novo conector DB2.

![catálogo](../../../../images/tutorials/create/ibm-db2/catalog.png)

A variável **[!UICONTROL Conectar-se ao IBM DB2]** é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Nova conta

Se estiver usando novas credenciais, selecione **[!UICONTROL Nova conta]**. No formulário de entrada que é exibido, forneça um nome, uma descrição opcional e suas credenciais do DB2. Quando terminar, selecione **[!UICONTROL Conectar]** e aguarde algum tempo para estabelecer a nova conexão.

![conectar](../../../../images/tutorials/create/ibm-db2/new.png)

### Conta existente

Para conectar uma conta existente, selecione a conta do DB2 com a qual deseja se conectar e selecione **[!UICONTROL Próxima]** para continuar.

![existente](../../../../images/tutorials/create/ibm-db2/existing.png)

## Próximas etapas

Seguindo este tutorial, você estabeleceu uma conexão com sua conta DB2. Agora você pode seguir para o próximo tutorial e [configurar um fluxo de dados para trazer dados para o [!DNL Platform]](../../dataflow/databases.md).
