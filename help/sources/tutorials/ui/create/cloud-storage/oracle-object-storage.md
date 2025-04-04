---
keywords: Experience Platform;home;tópicos populares;Oracle Object Storage;oracle object storage
solution: Experience Platform
title: Criar uma conexão Oracle Object Storage Source na interface do usuário
type: Tutorial
description: Saiba como criar uma conexão de origem do Oracle Object Storage usando a interface do usuário do Adobe Experience Platform.
exl-id: 32284163-5dde-4171-8977-f76ceeebcef2
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 1%

---

# Criar uma Conexão do Source [!DNL Oracle Object Storage] na interface

Este tutorial fornece etapas para criar uma conexão de origem [!DNL Oracle Object Storage] usando a interface do usuário do Adobe Experience Platform.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Fontes](../../../../home.md): o Experience Platform permite a assimilação de dados de várias fontes, ao mesmo tempo em que fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços do Experience Platform.
* [Sandboxes](../../../../../sandboxes/home.md): a Experience Platform fornece sandboxes virtuais que particionam uma única instância do Experience Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

### Coletar credenciais necessárias

Em para se conectar a [!DNL Oracle Object Storage], você deve fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| `serviceUrl` | O ponto de extremidade [!DNL Oracle Object Storage] necessário para autenticação. O formato do ponto de extremidade é: `https://{OBJECT_STORAGE_NAMESPACE}.compat.objectstorage.eu-frankfurt-1.oraclecloud.com` |
| `accessKey` | A ID da chave de acesso [!DNL Oracle Object Storage] é necessária para autenticação. |
| `secretKey` | A senha [!DNL Oracle Object Storage] é necessária para autenticação. |
| `bucketName` | O nome do bucket permitido é necessário se o usuário tiver acesso restrito. O nome do bucket deve ter entre três e 63 caracteres, deve começar e terminar com uma letra ou um número e pode conter apenas letras minúsculas, números ou hifens (`-`). O nome do bucket não pode ser formatado como um endereço IP. |
| `folderPath` | O caminho de pasta permitido é necessário caso o usuário tenha acesso restrito. |

Para obter mais informações sobre como obter esses valores, consulte o [guia de autenticação do Oracle Object Storage](https://docs.oracle.com/en-us/iaas/Content/Identity/Concepts/usercredentials.htm#User_Credentials).

Depois de obter as credenciais necessárias, siga as etapas abaixo para criar uma nova conta do Oracle Object Storage para se conectar ao Experience Platform.

## Conectar-se ao Oracle Object Storage

Na interface do Experience Platform, selecione **[!UICONTROL Fontes]** na navegação à esquerda para acessar o espaço de trabalho [!UICONTROL Fontes]. A tela [!UICONTROL Catálogo] exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a barra de pesquisa.

Na categoria [!UICONTROL Armazenamento na nuvem], selecione **[!UICONTROL Armazenamento de objetos do Oracle]** e **[!UICONTROL Adicionar dados]**.

![catálogo](../../../../images/tutorials/create/oracle-object-storage/catalog.png)

### Conta existente

Para usar uma conta existente, selecione a conta [!DNL Oracle Object Storage] com a qual deseja criar um novo fluxo de dados e clique em **[!UICONTROL Avançar]** para continuar.

![existente](../../../../images/tutorials/create/oracle-object-storage/existing.png)

### Nova conta

Se você estiver criando uma nova conta, selecione **[!UICONTROL Nova conta]** e forneça um nome, uma descrição opcional e suas credenciais do [!DNL Oracle Object Storage]. Quando terminar, selecione **[!UICONTROL Conectar à origem]** e aguarde algum tempo para que a nova conexão seja estabelecida.

![novo](../../../../images/tutorials/create/oracle-object-storage/new.png)

## Próximas etapas

Seguindo este tutorial, você estabeleceu uma conexão com sua conta do [!DNL Oracle Object Storage]. Agora você pode prosseguir para o próximo tutorial em [configurar um fluxo de dados para trazer dados do seu armazenamento na nuvem para o Experience Platform](../../dataflow/batch/cloud-storage.md).
