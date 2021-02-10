---
keywords: destino do armazenamento em nuvem;armazenamento em nuvem
title: Criar um destino de armazenamento em nuvem
type: Tutorial
description: Instruções para conectar-se aos locais dos armazenamentos na nuvem
seo-description: Instruções para conectar-se aos locais dos armazenamentos na nuvem
translation-type: tm+mt
source-git-commit: e13a19640208697665b0a7e0106def33fd1e456d
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 0%

---


# Criar um destino de armazenamento em nuvem

Esta página explica como você pode se conectar aos locais do armazenamento em nuvem no Adobe Experience Platform.

Em **[!UICONTROL Conexões]** > **[!UICONTROL Destinos]**, selecione o destino preferencial do armazenamento em nuvem e, em seguida, selecione **[!UICONTROL Configurar]**.

![Conectar-se ao destino do armazenamento na nuvem](../../assets/catalog/cloud-storage/workflow/connect.png)

>[!NOTE]
>
>Se já existir uma conexão com esse destino, você poderá ver um botão **[!UICONTROL Ativar]** no cartão de destino. Para obter mais informações sobre a diferença entre **[!UICONTROL Ativate]** e **[!UICONTROL Configure]**, consulte a seção [Catalog](../../ui/destinations-workspace.md#catalog) da documentação da área de trabalho de destino.

Na etapa **[!UICONTROL Authentication]**, se você já tiver configurado uma conexão com o destino do armazenamento na nuvem, selecione **[!UICONTROL Conta existente]** e selecione a conexão existente. Ou você pode selecionar **[!UICONTROL Nova conta]** para configurar uma nova conexão com o destino do armazenamento na nuvem. Preencha as credenciais de autenticação da sua conta e selecione **[!UICONTROL Ligar ao destino]**. Opcionalmente, você pode anexar sua chave pública formatada pelo RSA para adicionar criptografia aos arquivos exportados. Observe que essa chave pública **deve** ser gravada como uma string codificada em Base64.

Consulte [destino Amazon S3](./amazon-s3.md), [[!DNL Amazon Kinesis]](./amazon-kinesis.md) destino, [[!DNL Azure Event Hubs]](./azure-event-hubs.md) destino e [destino SFTP](./sftp.md) para obter detalhes sobre as credenciais inseridas na etapa **Authentication**.

>[!NOTE]
>
>A plataforma oferece suporte à validação de credenciais no processo de autenticação e exibe uma mensagem de erro se você inserir credenciais incorretas no local do armazenamento na nuvem. Isso garante que você não conclua o fluxo de trabalho com credenciais incorretas.

![Conectar ao destino do armazenamento na nuvem - etapa de autenticação](../../assets/catalog/cloud-storage/workflow/destination-account.png)

Na etapa **[!UICONTROL Setup]**, digite um **[!UICONTROL Name]** e um **[!UICONTROL Description]** para o fluxo de ativação.

Também nesta etapa, você pode selecionar qualquer **[!UICONTROL caso de uso de marketing]** que deve se aplicar a este destino. Os casos de uso de marketing indicam a intenção para a qual os dados serão exportados para o destino. Você pode selecionar de casos de uso de marketing definidos pelo Adobe ou criar seu próprio caso de uso de marketing. Para obter mais informações sobre casos de uso de marketing, consulte [Visão geral das políticas de uso de dados](../../../data-governance/policies/overview.md).

Para destinos do Amazon S3, insira **[!UICONTROL Nome do compartimento]** e **[!UICONTROL Caminho da pasta]** no destino do armazenamento da nuvem onde os arquivos serão entregues. Selecione **[!UICONTROL Criar destino]** depois de preencher os campos acima.

![Conectar-se ao destino do armazenamento na nuvem do Amazon S3 - etapa de autenticação](../../assets/catalog/cloud-storage/workflow/amazon-s3-setup.png)

Para destinos SFTP, insira o **[!UICONTROL caminho da pasta]** onde os arquivos serão entregues. Selecione **[!UICONTROL Criar destino]** depois de preencher os campos acima.

![Conectar-se ao destino do armazenamento na nuvem SFTP - etapa de autenticação](../../assets/catalog/cloud-storage/workflow/sftp-setup.png)

Para destinos [!DNL Amazon Kinesis], forneça o nome do seu fluxo de dados existente em sua conta [!DNL Amazon Kinesis]. A plataforma exportará dados para esse fluxo. Selecione **[!UICONTROL Criar destino]** depois de preencher os campos acima.

![Conectar-se ao destino do armazenamento na nuvem do Kinesis - etapa de autenticação](../../assets/catalog/cloud-storage/workflow/kinesis-setup.png)

Para destinos [!DNL Azure Event Hubs], forneça o nome do seu fluxo de dados existente em sua conta [!DNL Amazon Event Hubs]. A plataforma exportará dados para esse fluxo. Selecione **[!UICONTROL Criar destino]** depois de preencher os campos acima.

![Conectar-se ao destino do armazenamento na nuvem do Hubs do Evento - etapa de autenticação](../../assets/catalog/cloud-storage/workflow/event-hubs-setup.png)

Seu destino agora é criado. Você pode selecionar **[!UICONTROL Salvar e Sair]** se quiser ativar segmentos posteriormente ou selecionar **[!UICONTROL Próximo]** para continuar o fluxo de trabalho e selecionar segmentos para ativação. Em ambos os casos, consulte a próxima seção, [Ativar segmentos](#activate-segments), para que o restante do fluxo de trabalho exporte dados.

## Ativar segmentos {#activate-segments}

Consulte [Ativar perfis e segmentos em um destino](../../ui/activate-destinations.md) para obter informações sobre o fluxo de trabalho da ativação de segmentos.