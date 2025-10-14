---
title: Conexão com o Salesforce Marketing Cloud
description: O Salesforce Marketing Cloud é uma suíte de marketing digital conhecida anteriormente como ExactTarget que permite criar e personalizar jornadas para visitantes e clientes personalizarem suas experiências.
exl-id: e85049a7-eaed-4f8a-b670-9999d56928f8
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '801'
ht-degree: 2%

---

# [!DNL (Files) Salesforce Marketing Cloud] conexão

## Visão geral {#overview}

[[!DNL Salesforce Marketing Cloud]](https://www.salesforce.com/products/marketing-cloud/email-marketing/) é um conjunto de marketing digital conhecido anteriormente como ExactTarget que permite a você criar e personalizar jornadas para visitantes e clientes para personalizar sua experiência.

Para enviar dados de público-alvo para [!DNL Salesforce Marketing Cloud], primeiro [conecte-se ao destino](#connect-destination) no Experience Platform e [configure uma importação de dados](#import-data-into-salesforce) do local de armazenamento para [!DNL Salesforce Marketing Cloud].

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
---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Baseado em perfil]** | Você está exportando todos os membros de um segmento, juntamente com os campos de esquema desejados (por exemplo: endereço de email, número de telefone, sobrenome), conforme escolhido na tela selecionar atributos de perfil do [fluxo de trabalho de ativação de destino](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Frequência de exportação | **[!UICONTROL Lote]** | Os destinos em lote exportam arquivos para plataformas downstream em incrementos de três, seis, oito, doze ou vinte e quatro horas. Leia mais sobre [destinos com base em arquivo de lote](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## INCLUIR NA LISTA DE PERMISSÕES endereço IP {#allow-list}

Ao configurar destinos de marketing por email com armazenamento SFTP, a Adobe recomenda adicionar determinados intervalos IP ao seu incluo na lista de permissões.

Consulte [inclui na lista de permissões de endereço IP para destinos SFTP](../cloud-storage/ip-address-allow-list.md) se precisar adicionar IPs Adobe incluir na lista de permissões ao seu arquivo de pesquisa.

## Conectar ao destino {#connect}

>[!IMPORTANT]
> 
>Para se conectar ao destino, você precisa de **[!UICONTROL Exibir Destinos]** e **[!UICONTROL Gerenciar Destinos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.

Para se conectar a este destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md).

Esse destino oferece suporte aos seguintes tipos de conexão:

* **[!UICONTROL SFTP com senha]**
* **[!UICONTROL SFTP com chave SSH]**

### Parâmetros de conexão {#parameters}

Ao [configurar](../../ui/connect-destination.md) este destino, você deve fornecer as seguintes informações:

* Para conexões de **[!UICONTROL SFTP com Senha]**, você deve fornecer:
   * **[!UICONTROL Domínio]**: o endereço IP ou o nome de domínio da sua conta SFTP;
   * **[!UICONTROL Porta]**: a porta usada pelo local de armazenamento SFTP;
   * **[!UICONTROL Nome de usuário]**: o nome de usuário para fazer logon no local de armazenamento SFTP;
   * **[!UICONTROL Senha]**: a senha para fazer logon no local de armazenamento SFTP.
* Para conexões **[!UICONTROL SFTP com Chave SSH]**, você deve fornecer:
   * **[!UICONTROL Domínio]**: o endereço IP ou o nome de domínio da sua conta SFTP;
   * **[!UICONTROL Porta]**: a porta usada pelo local de armazenamento SFTP;
   * **[!UICONTROL Nome de usuário]**: o nome de usuário para fazer logon no local de armazenamento SFTP;
   * **[!UICONTROL Chave SSH]**: a chave SSH privada usada para fazer logon no local de armazenamento SFTP. A chave privada deve ser formatada como uma cadeia de caracteres codificada em Base64 e não deve ser protegida por senha.

* Como opção, você pode anexar sua chave pública formatada em RSA para adicionar criptografia com PGP/GPG aos arquivos exportados na seção **[!UICONTROL Chave]**. Sua chave pública deve ser gravada como uma cadeia de caracteres codificada [!DNL Base64].
* **[!UICONTROL Nome]**: escolha um nome relevante para o seu destino.
* **[!UICONTROL Descrição]**: insira uma descrição para o seu destino.
* **[!UICONTROL Caminho da pasta]**: forneça o caminho no local de armazenamento onde a Experience Platform depositará seus dados de exportação como arquivos CSV.
* **[!UICONTROL Formato de arquivo]**: selecione **CSV** para exportar arquivos CSV para o local de armazenamento.

<!--

Commenting out Amazon S3 bucket part for now until support is clarified

- **[!UICONTROL Bucket name]**: Your Amazon S3 bucket, where Experience Platform will deposit the data export. Your input must be between 3 and 63 characters long. Must begin and end with a letter or number. Must contain only lowercase letters, numbers, or hyphens ( - ). Must not be formatted as an IP address (for example, 192.100.1.1).

-->

### Ativar alertas {#enable-alerts}

Você pode ativar os alertas para receber notificações sobre o status do fluxo de dados para o seu destino. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o manual sobre [assinatura de alertas de destinos usando a interface](../../ui/alerts.md).

Quando terminar de fornecer detalhes da conexão de destino, selecione **[!UICONTROL Avançar]**.

## Ativar públicos-alvo para esse destino {#activate}

>[!IMPORTANT]
> 
>* Para ativar dados, você precisa de **[!UICONTROL Exibir Destinos]**, **[!UICONTROL Ativar Destinos]**, **[!UICONTROL Exibir Perfis]** e **[!UICONTROL Exibir Segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.
>* Para exportar *identidades*, você precisa da **[!UICONTROL permissão Exibir Gráfico de Identidade]** [controle de acesso](/help/access-control/home.md#permissions). <br> ![Selecione o namespace de identidade realçado no fluxo de trabalho para ativar as audiências para os destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Selecione o namespace de identidade realçado no fluxo de trabalho para ativar as audiências para os destinos."){width="100" zoomable="yes"}

Consulte [Ativar dados do público-alvo para destinos de exportação de perfil em lote](../../ui/activate-batch-profile-destinations.md) para obter instruções sobre como ativar públicos-alvo para esse destino.

### Atributos de destino {#destination-attributes}

Ao ativar públicos para esse destino, a Adobe recomenda que você selecione um identificador exclusivo do seu [esquema de união](../../../profile/home.md#profile-fragments-and-union-schemas). Selecione o identificador exclusivo e quaisquer outros campos XDM que você deseja exportar para o destino. Para obter mais informações, consulte as [práticas recomendadas ao ativar públicos para destinos de marketing por email](overview.md#best-practices).

## Dados exportados {#exported-data}

Para destinos [!DNL Salesforce Marketing Cloud], o Experience Platform cria um arquivo `.csv` no local de armazenamento fornecido. Para obter mais informações sobre os arquivos, consulte [verificar ativação de público-alvo](../../ui/activate-batch-profile-destinations.md#verify) no tutorial de ativação de público-alvo.

## Configurar importação de dados para [!DNL Salesforce Marketing Cloud] {#import-data-into-salesforce}

Depois de conectar [!DNL Experience Platform] ao armazenamento do [!DNL SFTP], você deve configurar a importação de dados do local de armazenamento para o [!DNL Salesforce Marketing Cloud]. Para saber como fazer isso, consulte [Importando Assinantes para o Marketing Cloud de um Arquivo](https://help.salesforce.com/articleView?id=mc_es_import_subscribers_from_file.htm&type=5) em [!DNL Salesforce Help Center].
