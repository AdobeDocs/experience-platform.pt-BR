---
keywords: Experience Platform;página inicial;tópicos populares;Armazenamento de arquivos do Azure;armazenamento de arquivos do Azure
solution: Experience Platform
title: Visão geral do Conector do Source de Armazenamento de Arquivos do Azure
description: Saiba como conectar o Armazenamento de arquivos do Azure ao Adobe Experience Platform usando APIs ou a interface do usuário.
exl-id: 0a5e9df6-9760-4eeb-86d5-d92d77df3d2b
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 0%

---

# Conector de armazenamento de arquivos do Azure

O Adobe Experience Platform fornece conectividade nativa para provedores de nuvem, como o AWS, o [!DNL Google Cloud Platform] e o [!DNL Azure], permitindo que você traga seus dados desses sistemas.

As fontes de armazenamento na nuvem podem trazer seus próprios dados para o [!DNL Experience Platform] sem precisar baixar, formatar ou carregar. Os dados assimilados podem ser formatados como XDM JSON, XDM Parquet ou delimitados. Cada etapa do processo é integrada ao fluxo de trabalho Origens. O [!DNL Experience Platform] permite trazer dados de [!DNL Azure File Storage] por meio de lotes.

## LISTA DE PERMISSÕES de endereço IP

Uma lista de endereços IP deve ser adicionada a uma lista de permissões antes de trabalhar com conectores de origem. Falha ao adicionar endereços IP específicos da região à lista de permissões pode levar a erros ou ao não desempenho ao usar origens. Consulte a página [lista de permissões de endereço IP](../../ip-address-allow-list.md) para obter mais informações.

## Restrições de nomenclatura para arquivos e diretórios

Veja a seguir uma lista de restrições que você deve considerar ao nomear seu arquivo ou diretório de armazenamento em nuvem.

- Os nomes dos componentes de diretório e arquivo não podem exceder 255 caracteres.
- Nomes de diretório e arquivo não podem terminar com uma barra (`/`). Se fornecido, ele será removido automaticamente.
- Os seguintes caracteres de URL reservados devem ter um escape adequado: `! ' ( ) ; @ & = + $ , % # [ ]`
- Os seguintes caracteres não são permitidos: `" \ / : | < > * ?`.
- Caracteres de caminho de URL inválidos não permitidos. Pontos de código como `\uE000`, embora válidos em nomes de arquivo NTFS, não são caracteres Unicode válidos. Além disso, alguns caracteres ASCII ou Unicode, como caracteres de controle (0x00 a 0x1F, \u0081 etc.), também não são permitidos. Para regras que regem cadeias de caracteres Unicode em HTTP/1.1, consulte [RFC 2616, Seção 2.2: Regras Básicas](https://www.ietf.org/rfc/rfc2616.txt) e [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Os seguintes nomes de arquivo não são permitidos: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, caractere de ponto (.) e dois caracteres de ponto (..).

## Conectar [!DNL Azure File Storage] a [!DNL Experience Platform]

A documentação abaixo fornece informações sobre como conectar o [!DNL Azure File Storage] ao [!DNL Experience Platform] usando APIs ou a interface do usuário:

### Uso de APIs

- [Criar uma conexão básica do Armazenamento de arquivos do Azure usando a API do Serviço de fluxo](../../tutorials/api/create/cloud-storage/azure-file-storage.md)
- [Explore a estrutura de dados e o conteúdo de uma fonte de armazenamento na nuvem usando a API do serviço de fluxo](../../tutorials/api/explore/cloud-storage.md)
- [Criar um fluxo de dados para uma fonte de armazenamento na nuvem usando a API do Serviço de fluxo](../../tutorials/api/collect/cloud-storage.md)

### Uso da interface

- [Criar uma conexão de origem do Armazenamento de arquivos do Azure na interface](../../tutorials/ui/create/cloud-storage/azure-file-storage.md)
- [Criar um fluxo de dados para uma conexão de armazenamento na nuvem na interface](../../tutorials/ui/dataflow/batch/cloud-storage.md)
