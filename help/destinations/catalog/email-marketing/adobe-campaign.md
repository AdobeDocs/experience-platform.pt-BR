---
keywords: email;Email;e-mail;destinos de e-mail;adobe campaign;campanha
title: Conexão com o Adobe Campaign
description: O Adobe Campaign é um conjunto de soluções que ajudam você a personalizar e entregar campanhas em todos os seus canais online e offline.
exl-id: 0de91738-8f56-41f5-8745-9b14b15db76a
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '841'
ht-degree: 5%

---

# Conexão com o Adobe Campaign

## Visão geral {#overview}

O Adobe Campaign é um conjunto de soluções que ajudam você a personalizar e entregar campanhas em todos os seus canais online e offline. Consulte [Introdução ao Campaign Classic](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/starting-with-adobe-campaign/about-adobe-campaign-classic.html) para obter mais informações.

Para enviar dados de público-alvo para o Adobe Campaign, primeiro [conecte o destino](#connect-destination) no Adobe Experience Platform e [configure uma importação de dados](#import-data-into-campaign) do local de armazenamento para o Adobe Campaign.

## Públicos-alvo compatíveis {#supported-audiences}

Esta seção descreve quais tipos de públicos-alvo você pode exportar para esse destino.

| Origem do público | Suportado | Descrição |
| ---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Públicos-alvo gerados pelo [Serviço de Segmentação](../../../segmentation/home.md) da Experience Platform. |
| Uploads personalizados | ✓ | Públicos [importados](../../../segmentation/ui/audience-portal.md#import-audience) para o Experience Platform de arquivos CSV. |

{style="table-layout:auto"}

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
|---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Profile-based]** | Você está exportando todos os membros de um segmento, juntamente com os campos de esquema desejados (por exemplo: endereço de email, número de telefone, sobrenome), conforme escolhido na tela selecionar atributos de perfil do [fluxo de trabalho de ativação de destino](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Frequência de exportação | **[!UICONTROL Batch]** | Os destinos em lote exportam arquivos para plataformas downstream em incrementos de três, seis, oito, doze ou vinte e quatro horas. Leia mais sobre [destinos com base em arquivo de lote](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## INCLUO NA LISTA DE PERMISSÕES de endereços IP {#allow-list}

Ao configurar destinos de marketing por email com armazenamento SFTP, a Adobe recomenda adicionar determinados intervalos IP ao incluo na lista de permissões.

Consulte [incluo na lista de permissões de endereços IP para destinos SFTP](../cloud-storage/ip-address-allow-list.md) se precisar adicionar IPs da Adobe ao seu incluo na lista de permissões.

## Conectar ao destino {#connect}

>[!IMPORTANT]
> 
>Para se conectar ao destino, você precisa da **[!UICONTROL Manage Destinations]** [permissão de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias

Para se conectar a este destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md).

O Adobe Campaign é compatível com os seguintes tipos de conexão:

* **[!UICONTROL Amazon S3]**
* **[!UICONTROL SFTP with Password]**
* **[!UICONTROL SFTP with SSH Key]**
* **[!UICONTROL Azure Blob]**

O método preferido para enviar dados para o Adobe Campaign é por meio de [!DNL Amazon S3] ou [!DNL Azure Blob].

### Parâmetros de conexão {#parameters}

Ao [configurar](../../ui/connect-destination.md) este destino, você deve fornecer as seguintes informações:

* Para conexões **[!UICONTROL Amazon S3]**, você deve fornecer o [!UICONTROL Access Key ID] e o [!UICONTROL Secret Access Key].
* Para conexões **[!UICONTROL SFTP with Password]**, você deve fornecer [!UICONTROL Domain], [!UICONTROL Port], [!UICONTROL Username] e [!UICONTROL Password].
* Para conexões **[!UICONTROL SFTP with SSH Key]**, você deve fornecer [!UICONTROL Domain], [!UICONTROL Port], [!UICONTROL Username] e [!UICONTROL SSH Key].
* Para conexões **[!UICONTROL Azure Blob]**, você deve fornecer uma cadeia de conexão.
* Como opção, você pode anexar sua chave pública formatada em RSA para adicionar criptografia com PGP/GPG aos arquivos exportados na seção **[!UICONTROL Key]**. Sua chave pública deve ser gravada como uma cadeia de caracteres codificada [!DNL Base64].
* **[!UICONTROL Name]**: Escolha um nome relevante para seu destino.
* **[!UICONTROL Description]**: insira uma descrição para o seu destino.
* **[!UICONTROL Bucket Name]**: *Para conexões S3*. Digite o local do bucket do S3 no qual o [!DNL Experience Platform] depositará seus dados de exportação como arquivos CSV.
* **[!UICONTROL Folder Path]**: forneça o caminho no local de armazenamento onde [!DNL Experience Platform] depositará seus dados de exportação como arquivos CSV.
* **[!UICONTROL Container]**: *Para conexões Blob*. O container que contém o Blob em que o caminho da pasta está.
* **[!UICONTROL File Format]**: Selecione **CSV** para exportar arquivos CSV para o local de armazenamento.

### Ativar alertas {#enable-alerts}

Você pode ativar os alertas para receber notificações sobre o status do fluxo de dados para o seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o manual sobre [assinatura de alertas de destinos usando a interface](../../ui/alerts.md).

Quando terminar de fornecer detalhes da conexão de destino, selecione **[!UICONTROL Next]**.

## Ativar públicos-alvo para esse destino {#activate}

>[!IMPORTANT]
> 
>* Para ativar dados, você precisa das **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** e **[!UICONTROL View Segments]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.
>* Para exportar *identidades*, você precisa da **[!UICONTROL View Identity Graph]** [permissão de controle de acesso](/help/access-control/home.md#permissions). <br> ![Selecione o namespace de identidade realçado no fluxo de trabalho para ativar as audiências para os destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Selecione o namespace de identidade realçado no fluxo de trabalho para ativar as audiências para os destinos."){width="100" zoomable="yes"}


Consulte [Ativar dados do público-alvo para destinos de exportação de perfil em lote](../../ui/activate-batch-profile-destinations.md) para obter instruções sobre como ativar públicos-alvo para esse destino.

### Atributos de destino {#destination-attributes}

Ao ativar públicos para esse destino, a Adobe recomenda que você selecione um identificador exclusivo do seu [esquema de união](../../../profile/home.md#profile-fragments-and-union-schemas). Selecione o identificador exclusivo e quaisquer outros campos XDM que você deseja exportar para o destino. Para obter mais informações, consulte as [práticas recomendadas ao ativar públicos para destinos de marketing por email](overview.md#best-practices).

## Dados exportados {#exported-data}

Para destinos [!DNL Adobe Campaign], o [!DNL Experience Platform] cria um arquivo `.csv` no local de armazenamento fornecido. Para obter mais informações sobre os arquivos, consulte a seção [verificar ativação de público-alvo](../../ui/activate-batch-profile-destinations.md#verify) no tutorial de ativação de público-alvo.

## Configurar importação de dados para o Adobe Campaign {#import-data-into-campaign}

>[!IMPORTANT]
>
>* Lembre-se dos limites de armazenamento do [!DNL SFTP], do armazenamento do banco de dados e do perfil ativo conforme o contrato do Adobe Campaign ao realizar essa integração.
>* Você precisa agendar, importar e mapear os segmentos exportados no Adobe Campaign usando fluxos de trabalho do [!DNL Campaign]. Consulte [Configuração de uma importação recorrente](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/use-cases/data-management/recurring-import-workflow.html) na documentação do Adobe Campaign Classic e [Sobre atividades de gerenciamento de dados](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/data-management-activities/about-data-management-activities.html) na documentação do Adobe Campaign Standard.
>* O método preferido para enviar dados para o Adobe Campaign é por meio de [!DNL Amazon S3] ou [!DNL Azure Blob].

Depois de conectar o [!DNL Experience Platform] ao armazenamento do [!DNL Amazon S3] ou do [!DNL Azure Blob], você deve configurar a importação de dados do local de armazenamento para o Adobe Campaign. Para saber como fazer isso, consulte as seguintes páginas de documentação do Adobe Campaign:

* [Introdução à importação e exportação de dados](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/importing-and-exporting-data/get-started-data-import-export.html?lang=pt-BR) e [ao carregamento de dados (arquivo)](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/action-activities/data-loading--file-.html) na documentação do Adobe Campaign Classic.
* [Introdução a processos e gerenciamento de dados](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/get-started-workflows.html) e [Carregar arquivo](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/data-management-activities/load-file.html) na documentação do Adobe Campaign Standard.
