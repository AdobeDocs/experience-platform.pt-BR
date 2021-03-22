---
keywords: Experience Platform, home, tópicos populares, Azure Data Lake Storage Gen2, ADLS-Gen2, adls gen2, ADLS Gen2
solution: Experience Platform
title: Visão Geral do Conector de Origem Gen2 do Armazenamento Azure Data Lake
topic: visão geral
description: Saiba como conectar o Azure Data Lake Storage Gen2 à Adobe Experience Platform usando APIs ou a interface do usuário.
translation-type: tm+mt
source-git-commit: 7fc99214272d2ce743b3666826c66f5d65e4d2ca
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 0%

---


# Conector Gen2 do Armazenamento Azure Data Lake

O Adobe Experience Platform fornece conectividade nativa para provedores de nuvem como AWS, [!DNL Google Cloud Platform] e [!DNL Azure], permitindo que você traga seus dados desses sistemas.

As fontes de armazenamento em nuvem podem trazer seus próprios dados para [!DNL Platform] sem a necessidade de baixar, formatar ou fazer upload. Os dados assimilados podem ser formatados como XDM JSON, XDM Parquet ou delimitados. Cada etapa do processo é integrada ao fluxo de trabalho Fontes . [!DNL Platform] O permite trazer dados do  [!DNL Azure Data Lake Storage Gen2] (ADLS-Gen2) por meio de lotes.

## LISTA DE PERMISSÕES de endereço IP

Uma lista de endereços IP deve ser adicionada a uma lista de permissões antes de trabalhar com conectores de origem. A não adição de endereços IP específicos da região à lista de permissões pode causar erros ou não desempenho ao usar fontes. Consulte a página [lista de permissões de endereço IP](../../ip-address-allow-list.md) para obter mais informações.

>[!IMPORTANT]
>
>No momento, o conector de origem [!DNL Azure Data Lake Storage Gen2] não oferece suporte à conectividade de mesma região com a Plataforma. Isso significa que se a instância do Azure estiver usando a mesma região de rede que a Plataforma, uma conexão com as fontes da Plataforma não poderá ser estabelecida. Atualmente, somente a conectividade entre regiões é compatível. Entre em contato com o gerente de conta do Adobe para obter mais informações.

## Restrições de nomenclatura para arquivos e diretórios

Esta é uma lista de restrições que devem ser consideradas ao nomear seu arquivo ou diretório de armazenamento em nuvem.

- Os nomes de componentes de diretório e arquivo não podem exceder 255 caracteres.
- Os nomes de diretório e arquivo não podem terminar com uma barra (`/`). Se fornecido, ele será removido automaticamente.
- Os seguintes caracteres de URL reservados devem ser evitados corretamente: `! ' ( ) ; @ & = + $ , % # [ ]`
- Os seguintes caracteres não são permitidos: `" \ / : | < > * ?`.
- Caracteres de caminho de URL inválidos não permitidos. Pontos de código como `\uE000`, enquanto válidos em nomes de arquivo NTFS, não são caracteres Unicode válidos. Além disso, alguns caracteres ASCII ou Unicode, como caracteres de controle (0x00 a 0x1F, \u0081, etc.), também não são permitidos. Para regras que regem cadeias de caracteres Unicode no HTTP/1.1, consulte [RFC 2616, Seção 2.2: Regras básicas](https://www.ietf.org/rfc/rfc2616.txt) e [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Os seguintes nomes de arquivo não são permitidos: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, caractere de ponto (...) e dois caracteres de ponto (.).

## Conecte [!DNL Azure Data Lake Storage Gen2] a [!DNL Platform]

A documentação abaixo fornece informações sobre como se conectar [!DNL Azure Data Lake Storage Gen2] a [!DNL Platform] usando APIs ou a interface do usuário:

### Uso de APIs

- [Criar uma conexão de origem ADLS-Gen2 usando a API do Serviço de Fluxo](../../tutorials/api/create/cloud-storage/adls-gen2.md)
- [Explore um sistema de armazenamento em nuvem usando a API do Serviço de Fluxo](../../tutorials/api/explore/cloud-storage.md)
- [Colete dados de armazenamento em nuvem usando a API do Serviço de Fluxo](../../tutorials/api/collect/cloud-storage.md)

### Uso da interface do usuário

- [Criar uma conexão de origem ADLS-Gen2 na interface do usuário](../../tutorials/ui/create/cloud-storage/adls-gen2.md)
- [Configurar um fluxo de dados para uma conexão de armazenamento em nuvem na interface do usuário](../../tutorials/ui/dataflow/batch/cloud-storage.md)