---
keywords: Experience Platform, home, tópicos populares, Armazenamento de objetos do Oracle, Armazenamento de objetos do oracle
solution: Experience Platform
title: Criar uma conexão de origem de armazenamento do objeto de Oracle na interface do usuário
type: Tutorial
description: Saiba como criar uma conexão de origem do Armazenamento de objetos do Oracle usando a interface do usuário do Adobe Experience Platform.
exl-id: 32284163-5dde-4171-8977-f76ceeebcef2
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 1%

---

# Crie um [!DNL Oracle Object Storage] Conexão de origem na interface do usuário

Este tutorial fornece etapas para criar um [!DNL Oracle Object Storage] conexão de origem usando a interface do usuário do Adobe Experience Platform.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Fontes](../../../../home.md): O Experience Platform permite que os dados sejam assimilados de várias fontes, fornecendo a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma.
* [Sandboxes](../../../../../sandboxes/home.md): O Experience Platform fornece sandboxes virtuais que particionam uma única instância da Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

### Obter credenciais necessárias

Em para se conectar ao [!DNL Oracle Object Storage], você deve fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| `serviceUrl` | O [!DNL Oracle Object Storage] endpoint necessário para autenticação. O formato do ponto de extremidade é: `https://{OBJECT_STORAGE_NAMESPACE}.compat.objectstorage.eu-frankfurt-1.oraclecloud.com` |
| `accessKey` | O [!DNL Oracle Object Storage] a ID da chave de acesso é necessária para autenticação. |
| `secretKey` | O [!DNL Oracle Object Storage] senha necessária para autenticação. |
| `bucketName` | O nome do bucket permitido é necessário se o usuário tiver acesso restrito. O nome do bucket deve ter entre três e 63 caracteres, deve começar e terminar com uma letra ou um número e pode conter somente letras minúsculas, números ou hífens (`-`). O nome do bucket não pode ser formatado como um endereço IP. |
| `folderPath` | O caminho de pasta permitido é necessário se o usuário tiver acesso restrito. |

Para obter mais informações sobre como obter esses valores, consulte [Guia de autenticação do Armazenamento de objetos do Oracle](https://docs.oracle.com/en-us/iaas/Content/Identity/Concepts/usercredentials.htm#User_Credentials).

Depois de coletar suas credenciais necessárias, siga as etapas abaixo para criar uma nova conta de Armazenamento de objetos do Oracle para se conectar à Platform.

## Conectar-se ao Armazenamento de Objeto do Oracle

Na interface do usuário da plataforma, selecione **[!UICONTROL Fontes]** na navegação à esquerda para acessar o [!UICONTROL Fontes] espaço de trabalho. O [!UICONTROL Catálogo] exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a barra de pesquisa.

Em [!UICONTROL armazenamento na nuvem] categoria , selecione **[!UICONTROL Armazenamento de objetos de oracle]** e depois selecione **[!UICONTROL Adicionar dados]**.

![catálogo](../../../../images/tutorials/create/oracle-object-storage/catalog.png)

### Conta existente

Para usar uma conta existente, selecione a [!DNL Oracle Object Storage] conta com a qual deseja criar um novo fluxo de dados e selecione **[!UICONTROL Próximo]** para continuar.

![existente](../../../../images/tutorials/create/oracle-object-storage/existing.png)

### Nova conta

Se estiver criando uma nova conta, selecione **[!UICONTROL Nova conta]** e forneça um nome, uma descrição opcional e [!DNL Oracle Object Storage] credenciais. Quando terminar, selecione **[!UICONTROL Conectar-se à origem]** e, em seguida, permitir que a nova conexão seja estabelecida.

![novo](../../../../images/tutorials/create/oracle-object-storage/new.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com seu [!DNL Oracle Object Storage] conta. Agora você pode prosseguir para o próximo tutorial em [configuração de um fluxo de dados para trazer dados do armazenamento em nuvem para o Platform](../../dataflow/batch/cloud-storage.md).
