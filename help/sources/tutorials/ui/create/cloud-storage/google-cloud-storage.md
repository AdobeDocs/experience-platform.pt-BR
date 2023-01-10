---
keywords: Experience Platform, home, tópicos populares, Google Cloud Storage, armazenamento em nuvem do google, GCS, gcs
solution: Experience Platform
title: Criar uma conexão da fonte de armazenamento da Google Cloud na interface do usuário
type: Tutorial
description: Saiba como criar uma conexão de origem de armazenamento do Google Cloud usando a interface do usuário do Adobe Experience Platform.
exl-id: 3258ccd7-757c-4c4a-b7bb-0e8c9de3b50a
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '594'
ht-degree: 1%

---

# Crie um [!DNL Google Cloud Storage] conexão de origem na interface do usuário

Os conectores de origem no Adobe Experience Platform oferecem a capacidade de assimilar dados de origem externa de acordo com a programação. Este tutorial fornece etapas para criar um [!DNL Google Cloud Storage] Conector de fonte (a seguir denominado &quot;GCS&quot;) usando o [!DNL Platform] interface do usuário.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): A estrutura padronizada pela qual o Experience Platform organiza os dados de experiência do cliente.
   * [Noções básicas da composição do schema](../../../../../xdm/schema/composition.md): Saiba mais sobre os elementos básicos dos esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   * [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Fornece um perfil de consumidor unificado e em tempo real com base em dados agregados de várias fontes.

Se você já tiver uma conexão GCS válida, ignore o restante deste documento e prossiga para o tutorial em [configuração de um fluxo de dados](../../dataflow/batch/cloud-storage.md).

### Formatos de arquivo não compatíveis

[!DNL Experience Platform] O suporta os seguintes formatos de arquivo a serem assimilados de armazenamentos externos:

* Valores separados por delimitador (DSV): No momento, o suporte para arquivos de dados formatados em DSV está limitado a valores separados por vírgula. O valor dos cabeçalhos de campo em arquivos formatados em DSV deve consistir apenas em caracteres alfanuméricos e sublinhados. O suporte para arquivos DSV gerais será fornecido no futuro.
* Notação de objeto JavaScript (JSON): Os arquivos de dados formatados JSON devem ser compatíveis com XDM.
* Parqueta Apache: Os arquivos de dados formatados do parâmetro devem ser compatíveis com XDM.

### Obter credenciais necessárias

Para acessar os dados do GCS em [!DNL Platform], você deve fornecer os seguintes valores:

| Credencial | Descrição |
| ---------- | ----------- |
| ID da chave de acesso | Uma sequência de 61 caracteres alfanuméricos usada para autenticar o [!DNL Google Cloud Storage] para a Platform. |
| Chave de acesso secreta | Uma string codificada em 40 caracteres, base e 64, usada para autenticar seu [!DNL Google Cloud Storage] para a Platform. |

Para obter mais informações sobre esses valores, consulte o [Chaves HMAC do Google Cloud Storage](https://cloud.google.com/storage/docs/authentication/hmackeys#overview) guia. Para obter etapas sobre como gerar sua própria ID de chave de acesso e chave de acesso secreta, consulte [[!DNL Google Cloud Storage] visão geral](../../../../connectors/cloud-storage/google-cloud-storage.md).

## Conecte seu [!DNL Google Cloud Storage] account

Depois de coletar suas credenciais necessárias, siga as etapas abaixo para vincular sua conta GCS a [!DNL Platform].

Faça logon em [Adobe Experience Platform](https://platform.adobe.com) e depois selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar o **[!UICONTROL Fontes]** espaço de trabalho. O **[!UICONTROL Catálogo]** exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Em **[!UICONTROL Bancos de dados]** categoria , selecione **[!UICONTROL Armazenamento em nuvem Google]**. Se esta for a primeira vez que você usa esse conector, selecione **[!UICONTROL Configurar]**. Caso contrário, selecione **[!UICONTROL Adicionar dados]** para criar um novo conector GCS.

![catálogo](../../../../images/tutorials/create/google-cloud-storage/catalog.png)

O **[!UICONTROL Conectar-se ao Google Cloud Storage]** será exibida. Nesta página, você pode usar novas credenciais ou credenciais existentes.

### Nova conta

Se estiver usando novas credenciais, selecione **[!UICONTROL Nova conta]**. No formulário de entrada exibido, forneça um nome, uma descrição opcional e suas credenciais do GCS. Quando terminar, selecione **[!UICONTROL Connect]** e, em seguida, permitir que a nova conexão seja estabelecida.

![connect](../../../../images/tutorials/create/google-cloud-storage/connect.png)

### Conta existente

Para conectar uma conta existente, selecione a conta GCS à qual deseja se conectar e selecione **[!UICONTROL Próximo]** para continuar.

![existente](../../../../images/tutorials/create/google-cloud-storage/existing.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com sua conta GCS. Agora você pode continuar para o próximo tutorial e [configure um fluxo de dados para trazer dados do armazenamento na nuvem para [!DNL Platform]](../../dataflow/batch/cloud-storage.md).
