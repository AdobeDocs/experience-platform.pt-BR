---
keywords: Experience Platform;lar;tópicos populares;Armazenamento Gen2 do Azure Data Lake;ADLS-Gen2;adls gen2;ADLS Gen2
solution: Experience Platform
title: Conector Gen2 do Armazenamento Azure Data Lake
topic: overview
description: A documentação abaixo fornece informações sobre como conectar o Armazenamento Gen2 do Azure Data Lake à Plataforma usando APIs ou a interface do usuário.
translation-type: tm+mt
source-git-commit: 2940f030aa21d70cceeedc7806a148695f68739e
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 0%

---


# Conector Gen2 do Armazenamento Azure Data Lake

A Adobe Experience Platform fornece conectividade nativa para provedores de nuvem como AWS, [!DNL Google Cloud Platform] e [!DNL Azure], permitindo que você extraia seus dados desses sistemas.

As fontes de armazenamentos na nuvem podem trazer seus próprios dados para [!DNL Platform] sem a necessidade de baixar, formatar ou fazer upload. Os dados ingeridos podem ser formatados como XDM JSON, XDM Parquet ou delimitados. Cada etapa do processo é integrada ao fluxo de trabalho de Fontes. [!DNL Platform] permite trazer dados do  [!DNL Azure Data Lake Storage Gen2] (ADLS-Gen2) por lotes.

## LISTA DE PERMISSÕES de endereço IP

Uma lista de endereços IP deve ser adicionada a uma lista de permissões antes de trabalhar com conectores de origem. A não adição de endereços IP específicos da região à sua lista de permissões pode resultar em erros ou em não desempenho ao usar fontes. Consulte a página [lista de permissões de endereço IP](../../ip-address-allow-list.md) para obter mais informações.

## Restrições de nomenclatura para arquivos e diretórios

A seguir, há uma lista de restrições que você deve levar em conta ao nomear seu arquivo ou diretório de armazenamento na nuvem.

- Nomes de diretório e de componente de arquivo não podem exceder 255 caracteres.
- Os nomes de diretório e arquivo não podem terminar com uma barra (`/`). Se fornecido, ele será removido automaticamente.
- Os seguintes caracteres de URL reservados devem ser escapados corretamente: `! * ' ( ) ; : @ & = + $ , / ? % # [ ]`
- Os seguintes caracteres não são permitidos: `" \ / : | < > * ?`.
- Caracteres de caminho de URL ilegais não permitidos. Pontos de código como `\uE000`, embora válidos em nomes de arquivo NTFS, não são caracteres Unicode válidos. Além disso, alguns caracteres ASCII ou Unicode, como caracteres de controle (0x00 a 0x1F, \u0081 etc.), também não são permitidos. Para obter as regras que regem strings Unicode em HTTP/1.1, consulte [RFC 2616, Seção 2.2: Regras básicas](https://www.ietf.org/rfc/rfc2616.txt) e [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Os seguintes nomes de arquivo não são permitidos: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, caractere de ponto (..) e dois caracteres de ponto (.).

## Conectar [!DNL Azure Data Lake Storage Gen2] a [!DNL Platform]

A documentação abaixo fornece informações sobre como conectar [!DNL Azure Data Lake Storage Gen2] a [!DNL Platform] usando APIs ou a interface do usuário:

### Uso de APIs

- [Criar um conector ADLS-Gen2 usando a API de Serviço de Fluxo](../../tutorials/api/create/cloud-storage/adls-gen2.md)
- [Explore um sistema de armazenamento em nuvem usando a API de Serviço de Fluxo](../../tutorials/api/explore/cloud-storage.md)
- [Coletar dados de armazenamento na nuvem usando a API de Serviço de Fluxo](../../tutorials/api/collect/cloud-storage.md)

## Uso da interface

- [Criar um conector de origem ADLS-Gen2 na interface do usuário](../../tutorials/ui/create/cloud-storage/adls-gen2.md)
- [Configurar um fluxo de dados para um conector de armazenamento em nuvem na interface do usuário](../../tutorials/ui/dataflow/batch/cloud-storage.md)