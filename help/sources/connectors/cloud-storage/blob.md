---
keywords: Experience Platform;página inicial;tópicos populares;Blob;blob;Blob do Azure;blob do Azure
solution: Experience Platform
title: Visão geral do Conector de origem do Azure Blob
description: Saiba como conectar o Azure Blob ao Adobe Experience Platform usando APIs ou a interface do usuário.
exl-id: 62adc74f-3570-42c7-9ae6-3ddbc09eccc7
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 0%

---

# Conector de blob do Azure

O Adobe Experience Platform fornece conectividade nativa para provedores de nuvem, como o AWS, [!DNL Google Cloud Platform], e [!DNL Azure]. Você pode trazer seus dados desses sistemas para [!DNL Platform].

As fontes de armazenamento na nuvem podem trazer seus próprios dados para [!DNL Platform] sem a necessidade de baixar, formatar ou fazer upload. Os dados assimilados podem ser formatados como XDM JSON, XDM Parquet ou delimitados. Cada etapa do processo é integrada ao fluxo de trabalho Origens. [!DNL Platform] permite trazer dados do [!DNL Azure Blob] em lotes.

## LISTA DE PERMISSÕES de endereço IP

Uma lista de endereços IP deve ser adicionada a uma lista de permissões antes de trabalhar com conectores de origem. Falha ao adicionar endereços IP específicos da região à lista de permissões pode levar a erros ou ao não desempenho ao usar origens. Consulte a [LISTA DE PERMISSÕES de endereço IP](../../ip-address-allow-list.md) para obter mais informações.

>[!IMPORTANT]
>
>A variável [!DNL Azure Blob] a origem não oferece suporte à conectividade da mesma região com o Experience Platform. Se sua instância do Azure estiver usando a mesma região de rede que o Experience Platform, não será possível estabelecer uma conexão com as origens de Experience Platform. Não use as regiões Leste dos EUA 2 do Azure, Europa Ocidental do Azure e Leste da Austrália do Azure ao configurar seu [!DNL Azure Blob] origem. Atualmente, somente a conectividade entre regiões é compatível.

## Restrições de nomenclatura para arquivos e diretórios

Veja a seguir uma lista de restrições que você deve considerar ao nomear seu arquivo ou diretório de armazenamento em nuvem.

- Os nomes dos componentes de diretório e arquivo não podem exceder 255 caracteres.
- Nomes de diretório e arquivo não podem terminar com uma barra (`/`). Se fornecido, ele será removido automaticamente.
- Os seguintes caracteres de URL reservados devem ter escape adequado: `! ' ( ) ; @ & = + $ , % # [ ]`
- Os seguintes caracteres não são permitidos: `" \ / : | < > * ?`.
- Caracteres de caminho de URL inválidos não permitidos. Pontos de código como `\uE000`, embora sejam válidos em nomes de arquivo NTFS, não são caracteres Unicode válidos. Além disso, alguns caracteres ASCII ou Unicode, como caracteres de controle (0x00 a 0x1F, \u0081 etc.), também não são permitidos. Para obter as regras que regem strings Unicode em HTTP/1.1, consulte [RFC 2616, Seção 2.2: regras básicas](https://www.ietf.org/rfc/rfc2616.txt) e [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Os seguintes nomes de arquivo não são permitidos: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, caractere de ponto (.) e dois caracteres de ponto (..).

## Conectar [!DNL Azure Blob] para [!DNL Platform]

A documentação abaixo fornece informações sobre como conectar o Azure Blob ao Adobe Experience Platform usando APIs ou a interface do usuário:

### Uso de APIs

- [Criar uma conexão básica do Azure Blob usando a API do Serviço de fluxo](../../tutorials/api/create/cloud-storage/blob.md)
- [Explore a estrutura de dados e o conteúdo de uma fonte de armazenamento na nuvem usando a API do serviço de fluxo](../../tutorials/api/explore/cloud-storage.md)
- [Criar um fluxo de dados para uma fonte de armazenamento na nuvem usando a API do Serviço de fluxo](../../tutorials/api/collect/cloud-storage.md)

### Uso da interface

- [Criar uma conexão de origem do Azure Blob na interface do usuário](../../tutorials/ui/create/cloud-storage/blob.md)
- [Criar um fluxo de dados para uma conexão de armazenamento na nuvem na interface](../../tutorials/ui/dataflow/batch/cloud-storage.md)
