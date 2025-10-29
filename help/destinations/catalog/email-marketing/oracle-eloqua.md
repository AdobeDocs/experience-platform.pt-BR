---
keywords: email;Email;e-mail;destinos de e-mail;oracle eloqua;oracle
title: (Arquivos) Conexão Oracle Eloqua
description: O Oracle Eloqua é uma plataforma de software as a service (SaaS) para automação de marketing oferecida pela Oracle, que tem como objetivo ajudar profissionais e organizações B2B a gerenciar campanhas de marketing e a geração de leads de vendas.
exl-id: 6eaa79ff-8874-423b-bdff-aa04f6101a53
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '671'
ht-degree: 2%

---

# [!DNL (Files) Oracle Eloqua] conexão

[[!DNL Oracle Eloqua]](https://www.oracle.com/cx/marketing/automation/) é uma plataforma SaaS (software as a service) para automação de marketing oferecida por [!DNL Oracle] que tem como objetivo ajudar profissionais e organizações B2B a gerenciar campanhas de marketing e a geração de leads de vendas.

Para enviar dados de público-alvo para [!DNL Oracle Eloqua], primeiro [conecte o destino](#connect-destination) no Adobe Experience Platform e [configure uma importação de dados](#import-data-into-eloqua) do local de armazenamento para [!DNL Oracle Eloqua].

## Públicos-alvo compatíveis {#supported-audiences}

Esta seção descreve quais tipos de públicos-alvo você pode exportar para esse destino.

| Origem do público | Suportado | Descrição |
|---------|----------|----------|
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

## LISTA DE PERMISSÕES de endereço IP {#allow-list}

Ao configurar destinos de marketing por email com armazenamento SFTP, a Adobe recomenda adicionar determinados intervalos IP à lista de permissões.

Consulte a [lista de permissões de endereço IP para destinos SFTP](../cloud-storage/ip-address-allow-list.md) se precisar adicionar IPs da Adobe à sua lista de permissões.

## Conectar ao destino {#connect}

>[!IMPORTANT]
> 
>Para se conectar ao destino, você precisa da **[!UICONTROL Manage Destinations]** [permissão de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias

Para se conectar a este destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md).

Esse destino oferece suporte aos seguintes tipos de conexão:

* **[!UICONTROL SFTP with Password]**
* **[!UICONTROL SFTP with SSH Key]**

### Parâmetros de conexão {#parameters}

Ao [configurar](../../ui/connect-destination.md) este destino, você deve fornecer as seguintes informações:

* Para **[!UICONTROL SFTP with Password]** conexões, você deve fornecer:
   * [!UICONTROL Domain]
   * [!UICONTROL Port]
   * [!UICONTROL Username]
   * [!UICONTROL Password]
* Para **[!UICONTROL SFTP with SSH Key]** conexões, você deve fornecer:
   * [!UICONTROL Domain]
   * [!UICONTROL Port]
   * [!UICONTROL Username]
   * [!UICONTROL SSH Key]

* Como opção, você pode anexar sua chave pública formatada em RSA para adicionar criptografia com PGP/GPG aos arquivos exportados na seção **[!UICONTROL Key]**. Sua chave pública deve ser gravada como uma cadeia de caracteres codificada [!DNL Base64].
* **[!UICONTROL Name]**: Escolha um nome relevante para seu destino.
* **[!UICONTROL Description]**: insira uma descrição para o seu destino.
* **[!UICONTROL Folder Path]**: forneça o caminho no local de armazenamento onde a Experience Platform depositará seus dados de exportação como arquivos CSV.
* **[!UICONTROL File Format]**: Selecione **CSV** para exportar arquivos CSV para o local de armazenamento.

<!--

Commenting out Amazon S3 bucket part for now until support is clarified

- **[!UICONTROL Bucket name]**: Your Amazon S3 bucket, where Experience Platform will deposit the data export. Your input must be between 3 and 63 characters long. Must begin and end with a letter or number. Must contain only lowercase letters, numbers, or hyphens ( - ). Must not be formatted as an IP address (for example, 192.100.1.1).

-->

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

Para destinos [!DNL Oracle Eloqua], o Experience Platform cria um arquivo `.csv` no local de armazenamento fornecido. Para obter mais informações sobre os arquivos, consulte [verificar ativação de público-alvo](../../ui/activate-batch-profile-destinations.md#verify) no tutorial de ativação de público-alvo.

## Configurar importação de dados para [!DNL Oracle Eloqua] {#import-data-into-eloqua}

Depois de conectar [!DNL Experience Platform] ao armazenamento do [!DNL SFTP], você deve configurar a importação de dados do local de armazenamento para o [!DNL Oracle Eloqua]. Para saber como fazer isso, consulte [Importando contatos ou contas](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCAA/Help/DataImportExport/Tasks/ImportingContactsOrAccounts.htm) em [!DNL Oracle Eloqua Help Center].
