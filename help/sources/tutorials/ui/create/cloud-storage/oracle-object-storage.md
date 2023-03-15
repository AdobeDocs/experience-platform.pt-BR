---
keywords: Experience Platform;página inicial;tópicos populares;Armazenamento de objetos do Oracle;armazenamento de objetos do oracle
solution: Experience Platform
title: Criar uma Conexão de Origem de Armazenamento do Objeto do Oracle na Interface do Usuário
type: Tutorial
description: Saiba como criar uma conexão de origem do Oracle Object Storage usando a interface do usuário do Adobe Experience Platform.
exl-id: 32284163-5dde-4171-8977-f76ceeebcef2
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 1%

---

# Criar um [!DNL Oracle Object Storage] Conexão de origem na interface

Este tutorial fornece etapas para a criação de um [!DNL Oracle Object Storage] conexão de origem usando a interface do Adobe Experience Platform.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Origens](../../../../home.md): o Experience Platform permite que os dados sejam assimilados de várias fontes e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma.
* [Sandboxes](../../../../../sandboxes/home.md): o Experience Platform fornece sandboxes virtuais que particionam uma única instância da Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

### Coletar credenciais necessárias

Em para se conectar a [!DNL Oracle Object Storage], você deve fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| `serviceUrl` | A variável [!DNL Oracle Object Storage] endpoint necessário para autenticação. O formato do endpoint é: `https://{OBJECT_STORAGE_NAMESPACE}.compat.objectstorage.eu-frankfurt-1.oraclecloud.com` |
| `accessKey` | A variável [!DNL Oracle Object Storage] ID da chave de acesso necessária para autenticação. |
| `secretKey` | A variável [!DNL Oracle Object Storage] senha necessária para autenticação. |
| `bucketName` | O nome do bucket permitido é necessário se o usuário tiver acesso restrito. O nome do bucket deve ter entre três e 63 caracteres, deve começar e terminar com uma letra ou um número e pode conter apenas letras minúsculas, números ou hifens (`-`). O nome do bucket não pode ser formatado como um endereço IP. |
| `folderPath` | O caminho de pasta permitido é necessário caso o usuário tenha acesso restrito. |

Para obter mais informações sobre como obter esses valores, consulte a [Guia de autenticação do Oracle Object Storage](https://docs.oracle.com/en-us/iaas/Content/Identity/Concepts/usercredentials.htm#User_Credentials).

Depois de obter as credenciais necessárias, você pode seguir as etapas abaixo para criar uma nova conta do Armazenamento de objetos do Oracle para se conectar à Platform.

## Conectar-se ao Armazenamento de Objetos do Oracle

Na interface do usuário da Platform, selecione **[!UICONTROL Origens]** na navegação à esquerda, para acessar a [!UICONTROL Origens] espaço de trabalho. A variável [!UICONTROL Catálogo] exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a barra de pesquisa.

No [!UICONTROL armazenamento na nuvem] categoria, selecione **[!UICONTROL Armazenamento de objetos de oracle]** e selecione **[!UICONTROL Adicionar dados]**.

![catálogo](../../../../images/tutorials/create/oracle-object-storage/catalog.png)

### Conta existente

Para usar uma conta existente, selecione a variável [!DNL Oracle Object Storage] conta com a qual deseja criar um novo fluxo de dados e selecione **[!UICONTROL Próxima]** para continuar.

![existente](../../../../images/tutorials/create/oracle-object-storage/existing.png)

### Nova conta

Se estiver criando uma nova conta, selecione **[!UICONTROL Nova conta]** e forneça um nome, uma descrição opcional e suas [!DNL Oracle Object Storage] credenciais. Quando terminar, selecione **[!UICONTROL Conectar à origem]** e aguarde algum tempo para estabelecer a nova conexão.

![novo](../../../../images/tutorials/create/oracle-object-storage/new.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com o seu [!DNL Oracle Object Storage] conta. Agora você pode prosseguir para o próximo tutorial em [configurar um fluxo de dados para trazer dados do armazenamento em nuvem para a Platform](../../dataflow/batch/cloud-storage.md).
