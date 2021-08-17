---
keywords: conectar destino, conexão de destino, como conectar destino
title: Criar uma nova conexão de destino
type: Tutorial
description: Este tutorial lista as etapas para se conectar a um destino no Adobe Experience Platform
exl-id: 56d7799a-d1da-4727-ae79-fb2c775fe5a5
source-git-commit: 1c67d9eb1b7762ecfcad5b0b7db5c317621f144e
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 0%

---

# Criar uma nova conexão de destino

## Visão geral {#overview}

Antes de enviar dados do público-alvo para um destino, você deve configurar uma conexão com a plataforma de destino. Este artigo mostra como configurar um novo destino usando a interface do usuário do Adobe Experience Platform.

## Criar uma nova conexão de destino {#setup}

### Selecionar destino {#select-destination}

1. Vá para **[!UICONTROL Connections]** > **[!UICONTROL Destinations]** e selecione a guia **[!UICONTROL Catalog]**.

   ![Página do catálogo](../assets/ui/connect-destinations/catalog.png)

1. Dependendo de você ter uma conexão existente com seu destino, poderá ver um botão **[!UICONTROL Configurar]** ou **[!UICONTROL Ativar]** no cartão de destino. Para obter mais informações sobre a diferença entre **[!UICONTROL Ativate]** e **[!UICONTROL Configure]**, consulte a seção [Catalog](../ui/destinations-workspace.md#catalog) da documentação do espaço de trabalho de destino. Selecione **[!UICONTROL Configurar]** ou **[!UICONTROL Ativar]**, dependendo do botão que estiver disponível.

   ![Página do catálogo](../assets/ui/connect-destinations/set-up.png)

   ![Ativar segmentos](../assets/ui/connect-destinations/activate-segments.png)

<!-- 1. If you selected **[!UICONTROL Set up]**, skip this step. If you selected **[!UICONTROL Activate segments]**, you can now see a list of the existing destination connections. Select **[!UICONTROL Configure new destination]**.

   ![Configure new destination](../assets/ui/connect-destinations/configure-new-destination.png) -->

### Etapa da conta {#account}

Selecione **[!UICONTROL New Account]** para configurar uma nova conexão com seu destino. Ou, se você tiver configurado anteriormente uma conexão com seu destino, selecione **[!UICONTROL Conta existente]** e selecione a conexão existente.

As credenciais que você deve inserir na etapa da conta variam de acordo com o destino e o tipo de autenticação.

* Para destinos de armazenamento em nuvem, é necessário fornecer credenciais para o Experience Platform se conectar ao local de armazenamento.

   ![Selecione o tipo de conta para destinos de armazenamento em nuvem](../assets/ui/connect-destinations/new-account-cloud-storage.png)

* Para o Facebook e vários outros destinos sociais e publicitários, selecione **[!UICONTROL New account]** e selecione **[!UICONTROL Connect to destination]**. Isso o levará à página de logon de destino, para que você possa conectar o Experience Platform ao seu destino.

   ![Selecione o tipo de conta para destinos sociais](../assets/ui/connect-destinations/new-account.png)

>[!IMPORTANT]
>
>Consulte a seção **[!UICONTROL Connection parameters]** em cada página do catálogo de destino para obter informações detalhadas sobre os parâmetros necessários nesta etapa (por exemplo, [Azure Blob](../catalog/cloud-storage/azure-blob.md#parameters) requer uma cadeia de conexão).

### Etapa de autenticação {#authentication}

Insira os detalhes de conexão da plataforma de destino e selecione **[!UICONTROL Criar destino]**.

1. Selecione as ações de marketing aplicáveis aos dados que você deseja exportar para o destino. As ações de marketing indicam a intenção para a qual os dados serão exportados para o destino. Você pode selecionar ações de marketing definidas pelo Adobe ou criar sua própria ação de marketing. Para obter mais informações sobre ações de marketing, consulte a página [visão geral das políticas de uso de dados](../../data-governance/policies/overview.md) .

   >[!IMPORTANT]
   >
   >A imagem abaixo é usada somente para fins ilustrativos. Os detalhes da conexão de destino variam entre destinos. Para obter informações detalhadas sobre os detalhes da conexão com seu destino, consulte a seção **[!UICONTROL Connection parameters]** em cada página [destination catalog](../catalog/overview.md) (por exemplo, [Google Customer Match](../catalog/advertising/google-customer-match.md#parameters)).

   ![Ligar ao destino](../assets/ui/connect-destinations/connect-destination.png)

1. Selecione **[!UICONTROL Salvar e sair]** para salvar a configuração de destino, ou selecione **[!UICONTROL Próximo]** para prosseguir para os dados de público-alvo [fluxo de ativação](activate-destinations.md).