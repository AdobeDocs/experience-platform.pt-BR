---
keywords: email; Email; email; destinos de email; adobe campaign; campanha
title: Conexão Adobe Campaign
description: O Adobe Campaign é um conjunto de soluções que ajudam você a personalizar e entregar campanhas em todos os seus canais online e offline.
exl-id: 0de91738-8f56-41f5-8745-9b14b15db76a
source-git-commit: b4810dfef7b0d437744ca14a32bd4f5746e8d002
workflow-type: tm+mt
source-wordcount: '717'
ht-degree: 2%

---

# Conexão Adobe Campaign

## Visão geral {#overview}

O Adobe Campaign é um conjunto de soluções que ajudam você a personalizar e entregar campanhas em todos os seus canais online e offline. Consulte [Introdução ao Campaign Classic](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/starting-with-adobe-campaign/about-adobe-campaign-classic.html?lang=pt-BR) para obter mais informações.

Para enviar dados de segmento ao Adobe Campaign, primeiro você deve [conectar o destino](#connect-destination) no Adobe Experience Platform e, em seguida, [configurar uma importação de dados](#import-data-into-campaign) do local de armazenamento para o Adobe Campaign.

## Tipo de exportação {#export-type}

**Baseado em perfil** - estiver exportando todos os membros de um segmento, juntamente com os campos de esquema desejados (por exemplo: endereço de email, número de telefone, sobrenome), conforme escolhido na **[!UICONTROL Selecionar atributos]** da [fluxo de trabalho de ativação do público](../../ui/activate-batch-profile-destinations.md#select-attributes).

## LISTA DE PERMISSÕES de endereço IP {#allow-list}

Ao configurar destinos de marketing por email com o armazenamento SFTP, o Adobe recomenda adicionar determinados intervalos IP à lista de permissões.

Consulte [LISTA DE PERMISSÕES de endereço IP para destinos de armazenamento em nuvem](../cloud-storage/ip-address-allow-list.md) se você precisar adicionar IPs Adobe à lista de permissões.

## Conecte-se ao destino {#connect}

Para se conectar a esse destino, siga as etapas descritas na [tutorial de configuração de destino](../../ui/connect-destination.md).

O Adobe Campaign é compatível com os seguintes tipos de conexão:

* **[!UICONTROL Amazon S3]**
* **[!UICONTROL SFTP com senha]**
* **[!UICONTROL SFTP com chave SSH]**
* **[!UICONTROL Azure Blob]**

O método preferido para enviar dados para a Adobe Campaign é por [!DNL Amazon S3] ou [!DNL Azure Blob].

### Parâmetros de conexão {#parameters}

Ao [configuração](../../ui/connect-destination.md) nesse destino, você deve fornecer as seguintes informações:

* Para **[!UICONTROL Amazon S3]** , você deve fornecer [!UICONTROL ID da chave de acesso] e [!UICONTROL Chave de acesso secreta].
* Para **[!UICONTROL SFTP com senha]** conexões, você deve fornecer [!UICONTROL Domínio], [!UICONTROL Port], [!UICONTROL Nome do usuário]e [!UICONTROL Senha].
* Para **[!UICONTROL SFTP com chave SSH]** conexões, você deve fornecer [!UICONTROL Domínio], [!UICONTROL Port], [!UICONTROL Nome do usuário]e [!UICONTROL Chave SSH].
* Para **[!UICONTROL Azure Blob]** , você deve fornecer uma string de conexão.
* Como opção, você pode anexar sua chave pública formatada em RSA para adicionar criptografia com PGP/GPG aos arquivos exportados sob a variável **[!UICONTROL Chave]** seção. Sua chave pública deve ser escrita como uma [!DNL Base64] sequência de caracteres codificada.
* **[!UICONTROL Nome]**: Escolha um nome relevante para o seu destino.
* **[!UICONTROL Descrição]**: Insira uma descrição para o seu destino.
* **[!UICONTROL Nome do bucket]**: *Para conexões S3*. Insira o local do seu bucket S3, onde [!DNL Platform] O depositará seus dados de exportação como arquivos CSV.
* **[!UICONTROL Caminho da pasta]**: Forneça o caminho no local de armazenamento onde [!DNL Platform] O depositará seus dados de exportação como arquivos CSV.
* **[!UICONTROL Contêiner]**: *Para conexões Blob*. O contêiner que contém o Blob em que seu caminho de pasta está.
* **[!UICONTROL Formato de arquivo]**: **CSV** ou **TAB_DELIMITED**. Selecione o formato de arquivo a ser exportado para o local de armazenamento.

## Ativar segmentos para este destino {#activate}

Consulte [Ativar dados do público-alvo para destinos de exportação de perfil em lote](../../ui/activate-batch-profile-destinations.md) para obter instruções sobre como ativar segmentos de público-alvo para este destino.

### Atributos de destino {#destination-attributes}

Ao ativar segmentos para esse destino, o Adobe recomenda selecionar um identificador exclusivo de [schema de união](../../../profile/home.md#profile-fragments-and-union-schemas). Selecione o identificador exclusivo e quaisquer outros campos XDM que deseja exportar para o destino. Para obter mais informações, consulte [práticas recomendadas ao ativar públicos-alvo para destinos de marketing por email](overview.md#best-practices).

## Dados exportados {#exported-data}

Para [!DNL Adobe Campaign] destinos, [!DNL Platform] cria um `.csv` no local de armazenamento fornecido. Para obter mais informações sobre os arquivos, consulte [verificar ativação de segmento](../../ui/activate-batch-profile-destinations.md#verify) no tutorial de ativação de segmento.

## Configurar importação de dados no Adobe Campaign {#import-data-into-campaign}

>[!IMPORTANT]
>
>* Lembre-se [!DNL SFTP] limites de armazenamento, limites de armazenamento de banco de dados e limites de perfil ativo de acordo com seu contrato da Adobe Campaign ao executar essa integração.
>* Você precisa agendar, importar e mapear os segmentos exportados no Adobe Campaign usando [!DNL Campaign] fluxos de trabalho. Consulte [Configuração de uma importação recorrente](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/use-cases/data-management/recurring-import-workflow.html) na documentação do Adobe Campaign Classic e [Sobre as atividades de gestão de dados](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/data-management-activities/about-data-management-activities.html) na documentação do Adobe Campaign Standard.
>* O método preferido para enviar dados para a Adobe Campaign é por [!DNL Amazon S3] ou [!DNL Azure Blob].


Depois de conectar [!DNL Platform] para [!DNL Amazon S3] ou [!DNL Azure Blob] , é necessário configurar a importação de dados do local de armazenamento para o Adobe Campaign. Para saber como fazer isso, consulte as seguintes páginas de documentação do Adobe Campaign:
* [Introdução à importação e exportação de dados](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/importing-and-exporting-data/get-started-data-import-export.html?lang=pt-BR) e [Carregamento de dados (arquivo)](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/action-activities/data-loading--file-.html) na documentação do Adobe Campaign Classic.
* [Introdução a processos e gerenciamento de dados](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/get-started-workflows.html) e [Carregar arquivo](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/data-management-activities/load-file.html) na documentação do Adobe Campaign Standard.
