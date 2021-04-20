---
keywords: Experience Platform, home, tópicos populares, Armazenamento no Google Cloud, armazenamento na nuvem do google, GCS, gcs
solution: Experience Platform
title: Criar uma conexão de origem de armazenamento do Google Cloud na interface do usuário
topic: overview
type: Tutorial
description: Saiba como criar uma conexão de origem de armazenamento do Google Cloud usando a interface do usuário do Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: f6a63ca1e21b3c3f6a55574f31fdf04038b7e5c4
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 1%

---


# Criar uma conexão de origem [!DNL Google Cloud Storage] na interface do usuário

Os conectores de origem no Adobe Experience Platform oferecem a capacidade de assimilar dados de origem externa de acordo com a programação. Este tutorial fornece etapas para criar um conector de origem [!DNL Google Cloud Storage] (a seguir chamado &quot;GCS&quot;) usando a interface do usuário [!DNL Platform].

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): A estrutura padronizada pela qual o Experience Platform organiza os dados de experiência do cliente.
   * [Noções básicas da composição](../../../../../xdm/schema/composition.md) do schema: Saiba mais sobre os elementos básicos dos esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   * [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md) do Editor de esquema: Saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Fornece um perfil de consumidor unificado e em tempo real com base em dados agregados de várias fontes.

Se você já tiver uma conexão GCS válida, poderá ignorar o restante deste documento e prosseguir para o tutorial em [configurar um fluxo de dados](../../dataflow/batch/cloud-storage.md).

### Formatos de arquivo não suportados

[!DNL Experience Platform] O suporta os seguintes formatos de arquivo a serem assimilados de armazenamentos externos:

* Valores separados por delimitador (DSV): No momento, o suporte para arquivos de dados formatados em DSV está limitado a valores separados por vírgula. O valor dos cabeçalhos de campo em arquivos formatados em DSV deve consistir apenas em caracteres alfanuméricos e sublinhados. O suporte para arquivos DSV gerais será fornecido no futuro.
* Notação de objeto JavaScript (JSON): Os arquivos de dados formatados JSON devem ser compatíveis com XDM.
* Parqueta Apache: Os arquivos de dados formatados do parâmetro devem ser compatíveis com XDM.

### Obter credenciais necessárias

Para acessar seus dados do GCS em [!DNL Platform], você deve fornecer os seguintes valores:

| Credencial | Descrição |
| ---------- | ----------- |
| ID da chave de acesso | Uma sequência de 61 caracteres alfanuméricos usada para autenticar sua conta [!DNL Google Cloud Storage] para a Platform. |
| Chave de acesso secreta | Uma sequência de 40 caracteres codificados na base de 64 caracteres usada para autenticar sua conta [!DNL Google Cloud Storage] para a Platform. |

Para obter mais informações sobre esses valores, consulte o guia [Google Cloud Storage HMAC keys](https://cloud.google.com/storage/docs/authentication/hmackeys#overview) . Para obter etapas sobre como gerar sua própria ID de chave de acesso e chave de acesso secreta, consulte a [[!DNL Google Cloud Storage] visão geral](../../../../connectors/cloud-storage/google-cloud-storage.md).

## Conecte sua conta [!DNL Google Cloud Storage]

Depois de coletar suas credenciais necessárias, siga as etapas abaixo para vincular sua conta GCS a [!DNL Platform].

Faça logon em [Adobe Experience Platform](https://platform.adobe.com) e selecione **[!UICONTROL Sources]** na barra de navegação esquerda para acessar o espaço de trabalho **[!UICONTROL Sources]**. A tela **[!UICONTROL Catalog]** exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Na categoria **[!UICONTROL Databases]**, selecione **[!UICONTROL Google Cloud Storage]**. Se esta for a primeira vez que você usa esse conector, selecione **[!UICONTROL Configure]**. Caso contrário, selecione **[!UICONTROL Add data]** para criar um novo conector GCS.

![catálogo](../../../../images/tutorials/create/google-cloud-storage/catalog.png)

A página **[!UICONTROL Connect to Google Cloud Storage]** é exibida. Nesta página, você pode usar novas credenciais ou credenciais existentes.

### Nova conta

Se estiver usando novas credenciais, selecione **[!UICONTROL New account]**. No formulário de entrada exibido, forneça um nome, uma descrição opcional e suas credenciais do GCS. Quando terminar, selecione **[!UICONTROL Connect]** e aguarde algum tempo para que a nova conexão seja estabelecida.

![connect](../../../../images/tutorials/create/google-cloud-storage/connect.png)

### Conta existente

Para conectar uma conta existente, selecione a conta GCS à qual deseja se conectar e selecione **[!UICONTROL Next]** para prosseguir.

![existente](../../../../images/tutorials/create/google-cloud-storage/existing.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com sua conta GCS. Agora você pode continuar para o próximo tutorial e [configurar um fluxo de dados para trazer dados do armazenamento de nuvem para [!DNL Platform]](../../dataflow/batch/cloud-storage.md).