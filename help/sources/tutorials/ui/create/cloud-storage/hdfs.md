---
keywords: Experience Platform;página inicial;tópicos populares;Apache HDFS;HDFS;hdfs
solution: Experience Platform
title: Criar uma conexão Apache HDFS Source na interface
type: Tutorial
description: Saiba como criar uma conexão de origem do Apache Hadoop Distributed File System usando a interface do usuário do Adobe Experience Platform.
exl-id: 3b8bf210-13b6-44e6-9090-152998f67452
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 1%

---

# Criar uma conexão de origem HDFS [!DNL Apache] na interface

>[!NOTE]
>
>O conector HDFS [!DNL Apache] está na versão beta. Consulte a [Visão geral das fontes](../../../../home.md#terms-and-conditions) para obter mais informações sobre o uso de conectores rotulados com beta.

Os conectores do Source em [!DNL Adobe Experience Platform] fornecem a capacidade de assimilar dados obtidos externamente de forma programada. Este tutorial fornece etapas para autenticar um conector de origem do [!DNL Apache Hadoop Distributed File System] (doravante denominado &quot;HDFS&quot;) usando a interface do usuário [!DNL Platform].

## Introdução

Este tutorial requer entendimento prático dos seguintes componentes do [!DNL Platform]:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): a estrutura padronizada pela qual o [!DNL Experience Platform] organiza os dados de experiência do cliente.
   - [Noções básicas sobre a composição de esquema](../../../../../xdm/schema/composition.md): saiba mais sobre os blocos de construção básicos de esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição de esquema.
   - [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.

Se você já tiver uma conexão HDFS válida, ignore o restante deste documento e prossiga para o tutorial em [configurando um fluxo de dados](../../dataflow/batch/cloud-storage.md).

### Coletar credenciais necessárias

Para autenticar o conector de origem HDFS, você deve fornecer valores para a seguinte propriedade de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| `url` | A URL define parâmetros de autenticação necessários para a conexão com o HDFS anonimamente. Para obter mais informações sobre como obter esse valor, consulte o seguinte documento em [Autenticação HTTPS para HDFS](https://hadoop.apache.org/docs/r1.2.1/HttpAuthentication.html). |

## Conectar sua conta HDFS

Depois de obter as credenciais necessárias, siga as etapas abaixo para vincular sua conta HDFS a [!DNL Platform].

Faça logon em [Adobe Experience Platform](https://platform.adobe.com) e selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar o espaço de trabalho **[!UICONTROL Fontes]**. A tela **[!UICONTROL Catálogo]** exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Na categoria **[!UICONTROL Armazenamento na nuvem]**, selecione **[!UICONTROL Apache HDFS]**. Se esta for a primeira vez que você usa este conector, selecione **[!UICONTROL Configurar]**. Caso contrário, selecione **[!UICONTROL Adicionar dados]** para criar um novo conector HDFS.

![catálogo](../../../../images/tutorials/create/hdfs/catalog.png)

A página **[!UICONTROL Conectar-se ao HDFS]** é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Nova conta

Se você estiver usando novas credenciais, selecione **[!UICONTROL Nova conta]**. No formulário de entrada exibido, forneça um nome, uma descrição opcional e suas credenciais do HDFS. Quando terminar, selecione **[!UICONTROL Conectar à origem]** e aguarde algum tempo para que a nova conexão seja estabelecida.

![conectar](../../../../images/tutorials/create/hdfs/new.png)

### Conta existente

Para conectar uma conta existente, selecione a conta do HDFS com a qual deseja se conectar e selecione **[!UICONTROL Avançar]** para continuar.

![existente](../../../../images/tutorials/create/hdfs/existing.png)

## Próximas etapas

Seguindo este tutorial, você estabeleceu uma conexão com sua conta HDFS. Agora você pode seguir para o próximo tutorial e [configurar um fluxo de dados para trazer dados do seu armazenamento na nuvem para o  [!DNL Platform]](../../dataflow/batch/cloud-storage.md).
