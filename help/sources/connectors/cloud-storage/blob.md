---
keywords: Experience Platform, home, tópicos populares, blob, blob, blob do Azure, blob do azure
solution: Experience Platform
title: Visão Geral do Conector de Origem Azure Blob
description: Saiba como conectar o Azure Blob ao Adobe Experience Platform usando APIs ou a interface do usuário.
exl-id: 62adc74f-3570-42c7-9ae6-3ddbc09eccc7
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 0%

---

# Conector de blob do Azure

O Adobe Experience Platform fornece conectividade nativa para provedores de nuvem como o AWS, [!DNL Google Cloud Platform]e [!DNL Azure]. Você pode trazer seus dados desses sistemas para [!DNL Platform].

As fontes de armazenamento na nuvem podem trazer seus próprios dados para o [!DNL Platform] sem a necessidade de baixar, formatar ou fazer upload. Os dados assimilados podem ser formatados como XDM JSON, XDM Parquet ou delimitados. Cada etapa do processo é integrada ao fluxo de trabalho Fontes . [!DNL Platform] permite trazer dados do [!DNL Azure Blob] por lotes.

## LISTA DE PERMISSÕES de endereço IP

Uma lista de endereços IP deve ser adicionada a uma lista de permissões antes de trabalhar com conectores de origem. A não adição de endereços IP específicos da região à lista de permissões pode causar erros ou não desempenho ao usar fontes. Consulte a [LISTA DE PERMISSÕES de endereço IP](../../ip-address-allow-list.md) para obter mais informações.

>[!IMPORTANT]
>
>O [!DNL Azure Blob] A origem não suporta conectividade de mesma região com o Experience Platform. Se a instância do Azure estiver usando a mesma região de rede que o Experience Platform, não será possível estabelecer uma conexão com fontes Experience Platform. Não use as regiões do Azure East US 2, Azure West Europe e Azure Austrália East ao configurar seu [!DNL Azure Blob] fonte. Atualmente, somente a conectividade entre regiões é compatível.

## Restrições de nomenclatura para arquivos e diretórios

Esta é uma lista de restrições que devem ser consideradas ao nomear seu arquivo ou diretório de armazenamento em nuvem.

- Os nomes de componentes de diretório e arquivo não podem exceder 255 caracteres.
- Os nomes de diretório e arquivo não podem terminar com uma barra (`/`). Se fornecido, ele será removido automaticamente.
- Os seguintes caracteres de URL reservados devem ser evitados corretamente: `! ' ( ) ; @ & = + $ , % # [ ]`
- Os seguintes caracteres não são permitidos: `" \ / : | < > * ?`.
- Caracteres de caminho de URL inválidos não permitidos. Pontos de código como `\uE000`, embora válidas em nomes de arquivo NTFS, não são caracteres Unicode válidos. Além disso, alguns caracteres ASCII ou Unicode, como caracteres de controle (0x00 a 0x1F, \u0081, etc.), também não são permitidos. Para obter as regras que regem as cadeias de caracteres Unicode no HTTP/1.1, consulte [RFC 2616, Seção 2.2: Regras básicas](https://www.ietf.org/rfc/rfc2616.txt) e [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Os seguintes nomes de arquivo não são permitidos: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, caractere de ponto (...) e dois caracteres de ponto (.).

## Connect [!DNL Azure Blob] para [!DNL Platform]

A documentação abaixo fornece informações sobre como conectar o Azure Blob ao Adobe Experience Platform usando APIs ou a interface do usuário:

### Uso de APIs

- [Criar uma conexão base do Azure Blob usando a API do Serviço de Fluxo](../../tutorials/api/create/cloud-storage/blob.md)
- [Explore a estrutura de dados e o conteúdo de uma fonte de armazenamento em nuvem usando a API do Serviço de Fluxo](../../tutorials/api/explore/cloud-storage.md)
- [Criar um fluxo de dados para uma fonte de armazenamento em nuvem usando a API do Serviço de Fluxo](../../tutorials/api/collect/cloud-storage.md)

### Uso da interface do usuário

- [Criar uma conexão de origem do Azure Blob na interface do usuário](../../tutorials/ui/create/cloud-storage/blob.md)
- [Criar um fluxo de dados para uma conexão de armazenamento em nuvem na interface do usuário do](../../tutorials/ui/dataflow/batch/cloud-storage.md)
