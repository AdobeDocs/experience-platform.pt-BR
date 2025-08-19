---
title: Conectar o Armazenamento Azure Blob ao Experience Platform na interface
description: Saiba como conectar sua conta de Armazenamento de Blobs do Azure à Experience Platform usando o espaço de trabalho de origens na interface do usuário.
exl-id: 0e54569b-7305-4065-981e-951623717648
source-git-commit: 7acdc090c020de31ee1a010d71a2969ec9e5bbe1
workflow-type: tm+mt
source-wordcount: '595'
ht-degree: 1%

---

# Conectar o [!DNL Azure Blob Storage] ao Experience Platform usando a interface

Leia este guia para saber como conectar sua instância do [!DNL Azure Blob Storage] ao Adobe Experience Platform usando o espaço de trabalho de origens na interface do usuário do Experience Platform.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): a estrutura padronizada para organização de dados de experiência do cliente no Experience Platform.
   * [Noções básicas sobre a composição de esquema](../../../../../xdm/schema/composition.md): saiba mais sobre os blocos de construção básicos de esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição de esquema.
   * [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.

Se você já tiver uma conexão [!DNL Azure Blob Storage] válida, ignore o restante deste documento e prossiga para o tutorial em [configurando um fluxo de dados](../../dataflow/batch/cloud-storage.md).

### Formatos de arquivo compatíveis

O Experience Platform oferece suporte aos seguintes formatos de arquivo para serem assimilados de armazenamentos externos:

* Valores separados por delimitadores (DSV): você pode usar qualquer delimitador de coluna única, como tabulação, vírgula, barra vertical, ponto e vírgula ou hash, para coletar arquivos simples em qualquer formato.
* Notação de objeto do JavaScript (JSON): os arquivos de dados formatados em JSON devem ser compatíveis com XDM.
* Apache Parquet: os arquivos de dados formatados com Parquet devem ser compatíveis com XDM.

### Coletar credenciais necessárias

Leia a [[!DNL Azure Blob Storage] visão geral](../../../../connectors/cloud-storage/blob.md#authentication) para obter informações sobre autenticação.

## Navegar pelo catálogo de origens

Na interface do Experience Platform, selecione **[!UICONTROL Fontes]** na navegação à esquerda para acessar o espaço de trabalho *[!UICONTROL Fontes]*. Escolha uma categoria ou use a barra de pesquisa para localizar sua fonte.

Para se conectar ao [!DNL Azure Blob Storage], vá para a categoria *[!UICONTROL Armazenamento na nuvem]*, selecione o cartão de origem **[!UICONTROL Armazenamento de Blobs do Azure]** e selecione **[!UICONTROL Configurar]**.

>[!TIP]
>
>As fontes mostram **[!UICONTROL Configurar]** para novas conexões e **[!UICONTROL Adicionar dados]** se uma conta já existir.

![O catálogo de origens com a origem de Armazenamento de Blob do Azure selecionada.](../../../../images/tutorials/create/blob/catalog.png)

## Usar uma conta existente

Para usar uma conta existente, selecione **[!UICONTROL Conta existente]** e depois selecione a conta [!DNL Azure Blob Storage] que deseja usar.

![A interface de origem existente para o Armazenamento Azure Blob.](../../../../images/tutorials/create/blob/existing.png)

## Criar uma nova conta

Para criar uma nova conta, selecione **[!UICONTROL Nova conta]** e forneça um nome e, opcionalmente, adicione uma descrição para sua conta. Você pode conectar sua conta do [!DNL Azure Blob Storage] à Experience Platform usando estes tipos de autenticação:

* **Autenticação da chave da conta**: usa a chave de acesso da conta de armazenamento para autenticar e conectar-se à sua conta do [!DNL Azure Blob Storage].
* **Assinatura de acesso compartilhado (SAS)**: usa um URI SAS para fornecer acesso delegado e limitado por tempo aos recursos da sua conta [!DNL Azure Blob Storage].
* **Autenticação baseada na entidade de serviço**: usa uma entidade de serviço do Azure Ative Diretory (AAD) (ID de cliente e segredo) para autenticar com segurança em sua conta de Armazenamento de Blobs do Azure.

>[!BEGINTABS]

>[!TAB Autenticação da chave da conta]

Selecione a **[!UICONTROL Autenticação da chave da conta]** e forneça suas `connectionString`, `container` e `folderPath`. Em seguida, selecione **[!UICONTROL Conectar à origem]** e aguarde alguns momentos para estabelecer a conexão.

![A opção de autenticação de chave de conta na etapa de criação da nova conta.](../../../../images/tutorials/create/blob/account-key.png)

>[!TAB Assinatura de acesso compartilhado]

Selecione **[!UICONTROL Assinatura de acesso compartilhado]** e forneça seu `sasUri`, `container` e `folderPath`. Em seguida, selecione **[!UICONTROL Conectar à origem]** e aguarde alguns momentos para estabelecer a conexão.

![A opção de autenticação de assinatura de acesso compartilhado na etapa de criação da nova conta.](../../../../images/tutorials/create/blob/sas.png)

>[!TAB Autenticação baseada na entidade de serviço]

Selecione a **[!UICONTROL Autenticação baseada na entidade de serviço]** e forneça suas `serviceEndpoint`, `servicePrincipalId`, `servicePrincipalKey`, `accountKind`, `tenant`, `container` e `folderPath`. Em seguida, selecione **[!UICONTROL Conectar à origem]** e aguarde alguns momentos para estabelecer a conexão.

![A opção de autenticação baseada na entidade de serviço na etapa de criação da nova conta.](../../../../images/tutorials/create/blob/service-principal.png)

>[!ENDTABS]

## Próximas etapas

Seguindo este tutorial, você estabeleceu uma conexão com sua conta do [!DNL Azure Blob Storage]. Agora você pode seguir para o próximo tutorial e [configurar um fluxo de dados para trazer dados do seu armazenamento em nuvem para o Experience Platform](../../dataflow/batch/cloud-storage.md).
