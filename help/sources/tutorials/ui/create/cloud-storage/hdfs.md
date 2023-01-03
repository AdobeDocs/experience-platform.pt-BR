---
keywords: Experience Platform, home, tópicos populares, Apache HDFS, HDFS, hdfs
solution: Experience Platform
title: Criar uma conexão de origem Apache HDFS na interface do usuário
topic-legacy: overview
type: Tutorial
description: Saiba como criar uma conexão de origem do Sistema de Arquivos Distribuído do Apache Hadoop usando a interface do usuário do Adobe Experience Platform.
exl-id: 3b8bf210-13b6-44e6-9090-152998f67452
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 1%

---

# Crie um [!DNL Apache] Conexão de origem HDFS na interface do usuário

>[!NOTE]
>
>O [!DNL Apache] O conector HDFS está em beta. Consulte a [Visão geral das fontes](../../../../home.md#terms-and-conditions) para obter mais informações sobre o uso de conectores com rótulo beta.

Conectores de origem em [!DNL Adobe Experience Platform] fornecer a capacidade de assimilar dados provenientes do exterior de forma programada. Este tutorial fornece etapas para a autenticação de um [!DNL Apache Hadoop Distributed File System] (a seguir designado por conector de origem &quot;HDFS&quot;) utilizando o [!DNL Platform] interface do usuário.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do [!DNL Platform]:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): O quadro normalizado pelo qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
   - [Noções básicas da composição do schema](../../../../../xdm/schema/composition.md): Saiba mais sobre os elementos básicos dos esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   - [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Fornece um perfil de consumidor unificado e em tempo real com base em dados agregados de várias fontes.

Se já tiver uma conexão HDFS válida, ignore o restante deste documento e prossiga para o tutorial em [configuração de um fluxo de dados](../../dataflow/batch/cloud-storage.md).

### Obter credenciais necessárias

Para autenticar seu conector de origem HDFS, você deve fornecer valores para a seguinte propriedade de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| `url` | O URL define os parâmetros de autenticação necessários para a conexão com o HDFS anonimamente. Para obter mais informações sobre como obter esse valor, consulte o seguinte documento em [Autenticação HTTPS para HDFS](https://hadoop.apache.org/docs/r1.2.1/HttpAuthentication.html). |

## Ligar a sua conta HDFS

Depois de reunir as credenciais necessárias, siga as etapas abaixo para vincular sua conta do HDFS a [!DNL Platform].

Faça logon em [Adobe Experience Platform](https://platform.adobe.com) e depois selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar o **[!UICONTROL Fontes]** espaço de trabalho. O **[!UICONTROL Catálogo]** exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Em **[!UICONTROL armazenamento na nuvem]** categoria , selecione **[!UICONTROL Apache HDFS]**. Se esta for a primeira vez que você usa esse conector, selecione **[!UICONTROL Configurar]**. Caso contrário, selecione **[!UICONTROL Adicionar dados]** para criar um novo conector HDFS.

![catálogo](../../../../images/tutorials/create/hdfs/catalog.png)

O **[!UICONTROL Ligar ao HDFS]** será exibida. Nesta página, você pode usar novas credenciais ou credenciais existentes.

### Nova conta

Se estiver usando novas credenciais, selecione **[!UICONTROL Nova conta]**. No formulário de entrada exibido, forneça um nome, uma descrição opcional e suas credenciais do HDFS. Quando terminar, selecione **[!UICONTROL Conectar-se à origem]** e, em seguida, permitir que a nova conexão seja estabelecida.

![connect](../../../../images/tutorials/create/hdfs/new.png)

### Conta existente

Para ligar uma conta existente, selecione a conta HDFS à qual pretende ligar e selecione **[!UICONTROL Próximo]** para continuar.

![existente](../../../../images/tutorials/create/hdfs/existing.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com sua conta HDFS. Agora você pode continuar para o próximo tutorial e [configure um fluxo de dados para trazer dados do armazenamento na nuvem para [!DNL Platform]](../../dataflow/batch/cloud-storage.md).
