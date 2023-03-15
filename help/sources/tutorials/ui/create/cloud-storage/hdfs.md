---
keywords: Experience Platform;página inicial;tópicos populares;Apache HDFS;HDFS;hdfs
solution: Experience Platform
title: Criar uma conexão de origem Apache HDFS na interface
type: Tutorial
description: Saiba como criar uma conexão de origem do Apache Hadoop Distributed File System usando a interface do usuário do Adobe Experience Platform.
exl-id: 3b8bf210-13b6-44e6-9090-152998f67452
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 1%

---

# Criar um [!DNL Apache] Conexão de origem HDFS na interface

>[!NOTE]
>
>A variável [!DNL Apache] O conector HDFS está na versão beta. Consulte a [Visão geral das fontes](../../../../home.md#terms-and-conditions) para obter mais informações sobre o uso de conectores rotulados com beta.

Conectores de origem em [!DNL Adobe Experience Platform] fornecer a capacidade de assimilar dados obtidos externamente de forma programada. Este tutorial fornece etapas para autenticar um [!DNL Apache Hadoop Distributed File System] (a seguir denominado &quot;HDFS&quot;) utilizando o conector de origem [!DNL Platform] interface do usuário.

## Introdução

Este tutorial requer um entendimento prático dos seguintes componentes do [!DNL Platform]:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): o quadro normalizado pelo qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
   - [Noções básicas da composição do esquema](../../../../../xdm/schema/composition.md): saiba mais sobre os componentes básicos dos esquemas XDM, incluindo princípios fundamentais e práticas recomendadas na composição do esquema.
   - [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.

Se você já tiver uma conexão HDFS válida, ignore o restante deste documento e prossiga para o tutorial em [configuração de um fluxo de dados](../../dataflow/batch/cloud-storage.md).

### Coletar credenciais necessárias

Para autenticar o conector de origem HDFS, você deve fornecer valores para a seguinte propriedade de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| `url` | A URL define parâmetros de autenticação necessários para a conexão com o HDFS anonimamente. Para obter mais informações sobre como obter esse valor, consulte o seguinte documento em [Autenticação HTTPS para HDFS](https://hadoop.apache.org/docs/r1.2.1/HttpAuthentication.html). |

## Conectar sua conta HDFS

Depois de obter as credenciais necessárias, siga as etapas abaixo para vincular sua conta HDFS a [!DNL Platform].

Efetue logon no [Adobe Experience Platform](https://platform.adobe.com) e selecione **[!UICONTROL Origens]** na barra de navegação esquerda, para acessar a **[!UICONTROL Origens]** espaço de trabalho. A variável **[!UICONTROL Catálogo]** A tela exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

No **[!UICONTROL armazenamento na nuvem]** categoria, selecione **[!UICONTROL Apache HDFS]**. Se esta for a primeira vez que você usa este conector, selecione **[!UICONTROL Configurar]**. Caso contrário, selecione **[!UICONTROL Adicionar dados]** para criar um novo conector HDFS.

![catálogo](../../../../images/tutorials/create/hdfs/catalog.png)

A variável **[!UICONTROL Conectar-se ao HDFS]** é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Nova conta

Se estiver usando novas credenciais, selecione **[!UICONTROL Nova conta]**. No formulário de entrada exibido, forneça um nome, uma descrição opcional e suas credenciais do HDFS. Quando terminar, selecione **[!UICONTROL Conectar à origem]** e aguarde algum tempo para estabelecer a nova conexão.

![conectar](../../../../images/tutorials/create/hdfs/new.png)

### Conta existente

Para conectar uma conta existente, selecione a conta do HDFS à qual deseja se conectar e selecione **[!UICONTROL Próxima]** para continuar.

![existente](../../../../images/tutorials/create/hdfs/existing.png)

## Próximas etapas

Seguindo este tutorial, você estabeleceu uma conexão com sua conta HDFS. Agora você pode seguir para o próximo tutorial e [configure um fluxo de dados para trazer dados do armazenamento em nuvem para [!DNL Platform]](../../dataflow/batch/cloud-storage.md).
