---
keywords: destino de armazenamento na nuvem; armazenamento na nuvem
title: Criar um destino de armazenamento em nuvem
type: Tutorial
description: Instruções para conectar-se aos locais de armazenamento na nuvem
seo-description: Instruções para conectar-se aos locais de armazenamento na nuvem
translation-type: tm+mt
source-git-commit: 632003773100ec8ef0389840695a1c75a1aa663d
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 0%

---


# Criar um destino de armazenamento em nuvem

## Visão geral {#overview}

Esta página explica como você pode se conectar a locais de armazenamento em nuvem no Adobe Experience Platform.

Em **[!UICONTROL Connections]** > **[!UICONTROL Destinations]**, selecione o destino de armazenamento de nuvem preferencial e selecione **[!UICONTROL Configure]**.

![Conectar-se ao destino de armazenamento em nuvem](../../assets/catalog/cloud-storage/workflow/connect.png)

>[!NOTE]
>
>Se uma conexão com esse destino já existir, você poderá ver um botão **[!UICONTROL Activate]** no cartão de destino. Para obter mais informações sobre a diferença entre **[!UICONTROL Activate]** e **[!UICONTROL Configure]**, consulte a seção [Catálogo](../../ui/destinations-workspace.md#catalog) da documentação do espaço de trabalho de destino.

## Etapa da conta {#account}

Na etapa **[!UICONTROL Account]**, se você tiver configurado anteriormente uma conexão com o destino de armazenamento na nuvem, selecione **[!UICONTROL Existing Account]** e selecione a conexão existente. Ou você pode selecionar **[!UICONTROL New Account]** para configurar uma nova conexão com o destino de armazenamento na nuvem. Preencha as credenciais de autenticação da conta e selecione **[!UICONTROL Connect to destination]**. Opcionalmente, é possível anexar sua chave pública formatada em RSA para adicionar criptografia aos arquivos exportados. Sua chave pública deve ser gravada como uma sequência de caracteres [!DNL Base64] codificada.

Consulte [destino Amazon S3](./amazon-s3.md), [[!DNL Amazon Kinesis]](./amazon-kinesis.md) destino, [[!DNL Azure Event Hubs]](./azure-event-hubs.md) destino e [destino SFTP](./sftp.md) para obter detalhes sobre a entrada de credenciais na etapa **Autenticação**.

>[!NOTE]
>
>A Platform oferece suporte à validação de credenciais no processo de autenticação e exibe uma mensagem de erro se você inserir credenciais incorretas no local de armazenamento da nuvem. Isso garante que você não conclua o fluxo de trabalho com credenciais incorretas.

![Conectar-se ao destino de armazenamento na nuvem - etapa de autenticação](../../assets/catalog/cloud-storage/workflow/destination-account.png)

## Etapa de autenticação {#authentication}

Na etapa **[!UICONTROL Authentication]** , digite um **[!UICONTROL Name]** e um **[!UICONTROL Description]** para o fluxo de ativação.

Nesta etapa, você também pode selecionar qualquer **[!UICONTROL Marketing action]** que deve se aplicar a esse destino. As ações de marketing indicam a intenção para a qual os dados serão exportados para o destino. Você pode selecionar ações de marketing definidas pelo Adobe ou criar sua própria ação de marketing. Para obter mais informações sobre ações de marketing, consulte a [Visão geral das políticas de uso de dados](../../../data-governance/policies/overview.md).

Para destinos Amazon S3, insira o **[!UICONTROL Bucket name]** e o **[!UICONTROL Folder path]** no destino de armazenamento na nuvem onde os arquivos serão entregues. Selecione **[!UICONTROL Create Destination]** depois de preencher os campos acima.

![Conectar-se ao destino de armazenamento na nuvem do Amazon S3 - etapa de autenticação](../../assets/catalog/cloud-storage/workflow/amazon-s3-setup.png)

Para destinos SFTP, insira o **[!UICONTROL Folder path]** onde os arquivos serão entregues. Selecione **[!UICONTROL Create Destination]** depois de preencher os campos acima.

![Conectar-se ao destino de armazenamento em nuvem SFTP - etapa de autenticação](../../assets/catalog/cloud-storage/workflow/sftp-setup.png)

Para destinos [!DNL Amazon Kinesis] , forneça o nome do fluxo de dados existente na conta [!DNL Amazon Kinesis] . A Platform exportará dados para esse fluxo. Selecione **[!UICONTROL Create Destination]** depois de preencher os campos acima.

![Conectar-se ao destino de armazenamento na nuvem da Kinesis - etapa de autenticação](../../assets/catalog/cloud-storage/workflow/kinesis-setup.png)

Para destinos [!DNL Azure Event Hubs] , forneça o nome do fluxo de dados existente na conta [!DNL Amazon Event Hubs] . A Platform exportará dados para esse fluxo. Selecione **[!UICONTROL Create Destination]** depois de preencher os campos acima.

![Conectar-se ao destino de armazenamento em nuvem de Hubs de Eventos - etapa de autenticação](../../assets/catalog/cloud-storage/workflow/event-hubs-setup.png)

Seu destino foi criado. Você pode selecionar **[!UICONTROL Save & Exit]** se desejar ativar segmentos posteriormente ou selecionar **[!UICONTROL Next]** para continuar o fluxo de trabalho e selecionar segmentos para ativar. Em ambos os casos, consulte a próxima seção, [Ativate segments](#activate-segments), para que o restante do workflow exporte dados.

## Ativar segmentos {#activate-segments}

Consulte [Ativar perfis e segmentos para um destino](../../ui/activate-destinations.md) para obter informações sobre o fluxo de trabalho de ativação de segmentos.