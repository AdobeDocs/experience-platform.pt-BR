---
keywords: Experience Platform;home;popular topics;Oracle Object Armazenamento;oracle object armazenamento
solution: Experience Platform
title: Criar uma conexão de origem de Armazenamento de objeto Oracle na interface do usuário
topic: overview
type: Tutorial
description: Saiba como criar uma conexão de origem de Armazenamento Object usando a interface do usuário do Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: c1453a9f0be42f834d35af871051324df8dadf80
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 1%

---


# Criar uma conexão de origem [!DNL Oracle Object Storage] na interface do usuário

Este tutorial fornece etapas para criar uma conexão de origem [!DNL Oracle Object Storage] usando a interface do usuário do Adobe Experience Platform.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Fontes](../../../../home.md): O Experience Platform permite que os dados sejam assimilados de várias fontes, ao mesmo tempo em que lhe fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma.
* [Caixas de proteção](../../../../../sandboxes/home.md): O Experience Platform fornece caixas de proteção virtuais que particionam uma única instância da Plataforma em ambientes virtuais separados para ajudar a desenvolver e desenvolver aplicativos de experiência digital.

### Reunir credenciais obrigatórias

Para se conectar a [!DNL Oracle Object Storage], é necessário fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| `serviceUrl` | O terminal [!DNL Oracle Object Storage] necessário para autenticação. O formato do ponto de extremidade é: `https://{OBJECT_STORAGE_NAMESPACE}.compat.objectstorage.eu-frankfurt-1.oraclecloud.com` |
| `accessKey` | A ID da chave de acesso [!DNL Oracle Object Storage] necessária para autenticação. |
| `secretKey` | A senha [!DNL Oracle Object Storage] necessária para autenticação. |
| `bucketName` | O nome do bucket permitido é necessário se o usuário tiver acesso restrito. O nome do bucket deve ter entre três e 63 caracteres, deve começar e terminar com uma letra ou um número e só pode conter letras minúsculas, números ou hífens (`-`). O nome do bucket não pode ser formatado como um endereço IP. |
| `folderPath` | O caminho de pasta permitido é necessário se o usuário tiver acesso restrito. |

Para obter mais informações sobre como obter esses valores, consulte o [guia de autenticação do Armazenamento de objeto de Oracle](https://docs.oracle.com/en-us/iaas/Content/Identity/Concepts/usercredentials.htm#User_Credentials).

Depois de reunir as credenciais necessárias, siga as etapas abaixo para criar uma nova conta de Oracle Object Armazenamento para se conectar à Plataforma.

## Conectar-se ao Armazenamento de objeto Oracle

Na interface do usuário da plataforma, selecione **[!UICONTROL Fontes]** no painel de navegação esquerdo para acessar a área de trabalho [!UICONTROL Fontes]. A tela [!UICONTROL Catálogo] exibe várias fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a barra de pesquisa.

Na categoria [!UICONTROL armazenamento de nuvem], selecione **[!UICONTROL Armazenamento Object]** e selecione **[!UICONTROL Adicionar dados]**.

![catálogo](../../../../images/tutorials/create/oracle-object-storage/catalog.png)

### Conta existente

Para usar uma conta existente, selecione a conta [!DNL Oracle Object Storage] com a qual deseja criar um novo fluxo de dados e selecione **[!UICONTROL Próximo]** para continuar.

![existente](../../../../images/tutorials/create/oracle-object-storage/existing.png)

### Nova conta

Se estiver criando uma nova conta, selecione **[!UICONTROL Nova conta]** e forneça um nome, uma descrição opcional e suas credenciais [!DNL Oracle Object Storage]. Quando terminar, selecione **[!UICONTROL Ligar à origem]** e, em seguida, aguarde algum tempo para que a nova ligação seja estabelecida.

![new](../../../../images/tutorials/create/oracle-object-storage/new.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com sua conta [!DNL Oracle Object Storage]. Agora você pode continuar com o próximo tutorial em [configurar um fluxo de dados para trazer dados do armazenamento em nuvem para a Plataforma](../../dataflow/batch/cloud-storage.md).
