---
title: Visão geral do Azure Data Lake Storage Gen2 Source Connector
description: Saiba como conectar o Azure Data Lake Storage Gen2 à Adobe Experience Platform usando APIs ou a interface do usuário.
exl-id: 424d7278-44d9-4653-82c0-eb21cbb9b623
source-git-commit: 06b2108715ce368ff4ecf5c6c7dd3a327d9f61b1
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 0%

---

# Conector Gen2 do Azure Data Lake Storage

O Adobe Experience Platform fornece conectividade nativa para provedores de nuvem, como o AWS, o [!DNL Google Cloud Platform] e o [!DNL Azure], permitindo que você traga seus dados desses sistemas.

As fontes de armazenamento na nuvem podem trazer seus próprios dados para a Experience Platform sem a necessidade de baixar, formatar ou carregar. Os dados assimilados podem ser formatados como XDM JSON, XDM Parquet ou delimitados. Cada etapa do processo é integrada ao fluxo de trabalho Origens. O Experience Platform permite trazer dados de [!DNL Azure Data Lake Storage Gen2] (ADLS Gen2) por meio de lotes.

## INCLUO NA LISTA DE PERMISSÕES de endereços IP

Você deve adicionar endereços IP específicos da região ao incluo na lista de permissões antes de conectar suas fontes à Experience Platform. Para obter mais informações, leia o guia sobre [como ler os endereços IP de incluir na lista de permissões para se conectar ao Experience Platform](../../ip-address-allow-list.md) para obter mais informações.

>[!IMPORTANT]
>
>A origem [!DNL Azure Data Lake Storage Gen2] não dá suporte à conectividade da mesma região com o Experience Platform. Se a instância do [!DNL Azure] estiver usando a mesma região de rede que o Experience Platform, não será possível estabelecer uma conexão com as origens do Experience Platform. Atualmente, somente a conectividade entre regiões é compatível.

## Restrições de nomenclatura para arquivos e diretórios

Veja a seguir uma lista de restrições que você deve considerar ao nomear seu arquivo ou diretório de armazenamento em nuvem.

- Os nomes dos componentes de diretório e arquivo não podem exceder 255 caracteres.
- Nomes de diretório e arquivo não podem terminar com uma barra (`/`). Se fornecido, ele será removido automaticamente.
- Os seguintes caracteres de URL reservados devem ter um escape adequado: `! ' ( ) ; @ & = + $ , % # [ ]`
- Os seguintes caracteres não são permitidos: `" \ / : | < > * ?`.
- Caracteres de caminho de URL inválidos não permitidos. Pontos de código como `\uE000`, embora válidos em nomes de arquivo NTFS, não são caracteres Unicode válidos. Além disso, alguns caracteres ASCII ou Unicode, como caracteres de controle (0x00 a 0x1F, \u0081 etc.), também não são permitidos. Para regras que regem cadeias de caracteres Unicode em HTTP/1.1, consulte [RFC 2616, Seção 2.2: Regras Básicas](https://www.ietf.org/rfc/rfc2616.txt) e [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Os seguintes nomes de arquivo não são permitidos: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, caractere de ponto (.) e dois caracteres de ponto (..).

## Conectar [!DNL Azure Data Lake Storage Gen2] ao Experience Platform

>[!NOTE]
>
>A entidade de serviço usada na criação de uma conta [!DNL Azure Data Lake Storage Gen2] deve ter pelo menos a função **Storage Blob Data Reader** atribuída pelo controle de acesso (IAM)

A documentação abaixo fornece informações sobre como conectar o [!DNL Azure Data Lake Storage Gen2] ao Experience Platform usando APIs ou a interface do usuário:

### Uso de APIs

- [Criar uma conexão base  [!DNL Azure Data Lake Storage Gen2]  usando a API de Serviço de Fluxo](../../tutorials/api/create/cloud-storage/adls-gen2.md)
- [Explore a estrutura de dados e o conteúdo de uma fonte de armazenamento na nuvem usando a API do serviço de fluxo](../../tutorials/api/explore/cloud-storage.md)
- [Criar um fluxo de dados para uma fonte de armazenamento na nuvem usando a API do Serviço de fluxo](../../tutorials/api/collect/cloud-storage.md)

### Uso da interface

- [Criar uma conexão de origem  [!DNL Azure Data Lake Storage Gen2]  na interface](../../tutorials/ui/create/cloud-storage/adls-gen2.md)
- [Criar um fluxo de dados para uma conexão de armazenamento na nuvem na interface](../../tutorials/ui/dataflow/batch/cloud-storage.md)
