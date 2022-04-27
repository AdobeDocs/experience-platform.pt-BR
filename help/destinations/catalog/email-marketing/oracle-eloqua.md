---
keywords: email; Email; email; destinos de email; oracle eloqua; oracle
title: Conexão Eloqua do Oracle
description: O Oracle Eloqua é uma plataforma de software como serviço (SaaS) para automação de marketing oferecida pelo Oracle, que tem como objetivo ajudar profissionais de marketing B2B e organizações a gerenciar campanhas de marketing e geração de líderes de vendas.
exl-id: 6eaa79ff-8874-423b-bdff-aa04f6101a53
source-git-commit: 0006c498cd33d9deb66f1d052b4771ec7504457d
workflow-type: tm+mt
source-wordcount: '599'
ht-degree: 1%

---

# [!DNL Oracle Eloqua] conexão

[[!DNL Oracle Eloqua]](https://www.oracle.com/cx/marketing/automation/) é uma plataforma de software como um serviço (SaaS) para automação de marketing oferecida por [!DNL Oracle] que tem como objetivo ajudar profissionais de marketing e organizações B2B a gerenciar campanhas de marketing e geração de leads de vendas.

Para enviar dados de segmento para [!DNL Oracle Eloqua], você deve primeiro [conectar o destino](#connect-destination) no Adobe Experience Platform e, em seguida, [configurar uma importação de dados](#import-data-into-eloqua) do local de armazenamento para [!DNL Oracle Eloqua].

## Tipo e frequência de exportação {#export-type-frequency}

Consulte a tabela abaixo para obter informações sobre o tipo e a frequência da exportação de destino.

| Item | Tipo | Notas |
---------|----------|---------|
| Tipo de exportação | **[!UICONTROL Baseado em perfil]** | Você está exportando todos os membros de um segmento, junto com os campos de esquema desejados (por exemplo: endereço de email, número de telefone, sobrenome), conforme escolhido na tela selecionar atributos de perfil do [fluxo de trabalho de ativação de destino](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Frequência de exportação | **[!UICONTROL Em lote]** | Destinos em lote exportam arquivos para plataformas downstream em incrementos de três, seis, oito, doze ou vinte e quatro horas. Leia mais sobre [destinos com base em arquivo em lote](/help/destinations/destination-types.md#file-based). |

{style=&quot;table-layout:auto&quot;}

## LISTA DE PERMISSÕES de endereço IP {#allow-list}

Ao configurar destinos de marketing por email com o armazenamento SFTP, o Adobe recomenda adicionar determinados intervalos IP à lista de permissões.

Consulte [LISTA DE PERMISSÕES de endereço IP para destinos de armazenamento em nuvem](../cloud-storage/ip-address-allow-list.md) se você precisar adicionar IPs Adobe à lista de permissões.

## Conecte-se ao destino {#connect}

>[!IMPORTANT]
> 
>Para se conectar ao destino, é necessário **[!UICONTROL Gerenciar destinos]** [permissão de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias

Para se conectar a esse destino, siga as etapas descritas na [tutorial de configuração de destino](../../ui/connect-destination.md).

Esse destino oferece suporte aos seguintes tipos de conexão:

* **[!UICONTROL SFTP com senha]**
* **[!UICONTROL SFTP com chave SSH]**

### Parâmetros de conexão {#parameters}

Ao [configuração](../../ui/connect-destination.md) nesse destino, você deve fornecer as seguintes informações:

* Para **[!UICONTROL SFTP com senha]** , você deve fornecer:
   * [!UICONTROL Domínio]
   * [!UICONTROL Porta ]
   * [!UICONTROL Nome do usuário]
   * [!UICONTROL Senha]
* Para **[!UICONTROL SFTP com chave SSH]** , você deve fornecer:
   * [!UICONTROL Domínio]
   * [!UICONTROL Porta ]
   * [!UICONTROL Nome do usuário]
   * [!UICONTROL Chave SSH]

* Como opção, você pode anexar sua chave pública formatada em RSA para adicionar criptografia com PGP/GPG aos arquivos exportados sob a variável **[!UICONTROL Chave]** seção. Sua chave pública deve ser escrita como uma [!DNL Base64] sequência de caracteres codificada.
* **[!UICONTROL Nome]**: Escolha um nome relevante para o seu destino.
* **[!UICONTROL Descrição]**: Insira uma descrição para o seu destino.
* **[!UICONTROL Caminho da pasta]**: Forneça o caminho no local de armazenamento onde a Platform depositará seus dados de exportação como arquivos CSV.
* **[!UICONTROL Formato de arquivo]**: Selecionar **CSV** para exportar arquivos CSV para o local de armazenamento.

<!--

Commenting out Amazon S3 bucket part for now until support is clarified

- **[!UICONTROL Bucket name]**: Your Amazon S3 bucket, where Platform will deposit the data export. Your input must be between 3 and 63 characters long. Must begin and end with a letter or number. Must contain only lowercase letters, numbers, or hyphens ( - ). Must not be formatted as an IP address (for example, 192.100.1.1).

-->

## Ativar segmentos para este destino {#activate}

>[!IMPORTANT]
> 
>Para ativar os dados, é necessário **[!UICONTROL Gerenciar destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]** e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

Consulte [Ativar dados do público-alvo para destinos de exportação de perfil em lote](../../ui/activate-batch-profile-destinations.md) para obter instruções sobre como ativar segmentos de público-alvo para este destino.

### Atributos de destino {#destination-attributes}

Ao ativar segmentos para esse destino, o Adobe recomenda selecionar um identificador exclusivo de [schema de união](../../../profile/home.md#profile-fragments-and-union-schemas). Selecione o identificador exclusivo e quaisquer outros campos XDM que deseja exportar para o destino. Para obter mais informações, consulte [práticas recomendadas ao ativar públicos-alvo para destinos de marketing por email](overview.md#best-practices).

## Dados exportados {#exported-data}

Para [!DNL Oracle Eloqua] destinos, a Platform cria uma `.csv` no local de armazenamento fornecido. Para obter mais informações sobre os arquivos, consulte [verificar ativação de segmento](../../ui/activate-batch-profile-destinations.md#verify) no tutorial de ativação de segmento.

## Configurar a importação de dados no [!DNL Oracle Eloqua] {#import-data-into-eloqua}

Depois de conectar [!DNL Platform] para [!DNL SFTP] você deve configurar a importação de dados do seu local de armazenamento para [!DNL Oracle Eloqua]. Para saber como fazer isso, consulte [Importação de contatos ou contas](https://docs.oracle.com/cloud/latest/marketingcs_gs/OMCAA/Help/DataImportExport/Tasks/ImportingContactsOrAccounts.htm) no [!DNL Oracle Eloqua Help Center].
