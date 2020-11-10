---
keywords: Experience Platform;home;popular topics;Apache HDFS;HDFS;hdfs
solution: Experience Platform
title: Criar um conector de origem HDFS Apache na interface do usuário
topic: overview
type: Tutorial
description: Este tutorial fornece etapas para autenticação de um conector de origem do Apache Hadoop Distributed File System (a seguir denominado "HDFS") usando a interface do usuário da plataforma.
translation-type: tm+mt
source-git-commit: f86f7483e7e78edf106ddd34dc825389dadae26a
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 1%

---


# Criar um conector de origem [!DNL Apache] HDFS na interface do usuário

>[!NOTE]
>
>O conector [!DNL Apache] HDFS está em beta. Consulte a visão geral [das](../../../../home.md#terms-and-conditions) Fontes para obter mais informações sobre o uso de conectores com rótulo beta.

Os conectores de origem fornecem [!DNL Adobe Experience Platform] a capacidade de assimilar dados de origem externa de forma programada. Este tutorial fornece etapas para autenticação de um conector de origem [!DNL Apache Hadoop Distributed File System] (a seguir denominado &quot;HDFS&quot;) usando a interface do [!DNL Platform] usuário.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do [!DNL Platform]:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): A estrutura padronizada pela qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
   - [Noções básicas da composição](../../../../../xdm/schema/composition.md)do schema: Saiba mais sobre os elementos básicos dos schemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   - [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md)do Editor de schemas: Saiba como criar schemas personalizados usando a interface do editor de Schemas.
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.

Se você já tiver uma conexão HDFS válida, poderá ignorar o restante deste documento e prosseguir para o tutorial sobre como [configurar um fluxo de dados](../../dataflow/batch/cloud-storage.md).

### Reunir credenciais obrigatórias

Para autenticar seu conector de origem HDFS, você deve fornecer valores para a seguinte propriedade de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| `url` | O URL define os parâmetros de autenticação necessários para a conexão anônima com o HDFS. Para obter mais informações sobre como obter este valor, consulte o seguinte documento sobre autenticação [HTTPS para HDFS](https://hadoop.apache.org/docs/r1.2.1/HttpAuthentication.html). |

## Ligar a sua conta HDFS

Depois de reunir as credenciais necessárias, siga os passos abaixo para ligar a sua conta HDFS à [!DNL Platform].

Faça logon no [Adobe Experience Platform](https://platform.adobe.com) e selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar a área de trabalho **[!UICONTROL Fontes]** . A tela **[!UICONTROL Catálogo]** exibe várias fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Na categoria do armazenamento **[!UICONTROL da]** nuvem, selecione **[!UICONTROL Apache HDFS]**. Se esta for a sua primeira vez usando este conector, selecione **[!UICONTROL Configurar]**. Caso contrário, selecione **[!UICONTROL Adicionar dados]** para criar um novo conector HDFS.

![catálogo](../../../../images/tutorials/create/hdfs/catalog.png)

A página **[!UICONTROL Conectar-se ao HDFS]** é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Nova conta

Se você estiver usando novas credenciais, selecione **[!UICONTROL Nova conta]**. No formulário de entrada exibido, forneça um nome, uma descrição opcional e suas credenciais do HDFS. Quando terminar, selecione **[!UICONTROL Conectar-se à fonte]** e aguarde algum tempo para a nova conexão ser estabelecida.

![connect](../../../../images/tutorials/create/hdfs/new.png)

### Conta existente

Para ligar uma conta existente, selecione a conta HDFS com a qual pretende ligar e, em seguida, selecione **[!UICONTROL Seguinte]** para continuar.

![existente](../../../../images/tutorials/create/hdfs/existing.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com sua conta HDFS. Agora você pode continuar para o próximo tutorial e [configurar um fluxo de dados para trazer dados do seu armazenamento em nuvem para [!DNL Platform]](../../dataflow/batch/cloud-storage.md)dentro.