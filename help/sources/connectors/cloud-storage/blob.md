---
keywords: Experience Platform;home;popular topics;Blob;blob;Azure Blob;azure blob
solution: Experience Platform
title: Conector Blob do Azure
topic: overview
description: A documentação abaixo fornece informações sobre como conectar o Blob do Azure à plataforma usando APIs ou a interface do usuário.
translation-type: tm+mt
source-git-commit: d42351c194bb5a11f3175535de83fbd3b6ac58d2
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 0%

---


# Conector Blob do Azure

A Adobe Experience Platform fornece conectividade nativa para provedores de nuvem como AWS, [!DNL Google Cloud Platform]e [!DNL Azure]. Você pode trazer seus dados desses sistemas para [!DNL Platform].

As fontes de armazenamentos na nuvem podem inserir seus próprios dados [!DNL Platform] sem a necessidade de baixar, formatar ou fazer upload. Os dados ingeridos podem ser formatados como XDM JSON, XDM parquet ou delimitados. Cada etapa do processo é integrada ao fluxo de trabalho de Fontes. [!DNL Platform] permite trazer dados de [!DNL Azure Blob] lotes.

## LISTA DE PERMISSÕES de endereço IP

Os seguintes endereços IP devem ser adicionados a uma lista de permissões antes de trabalhar com conectores de origem. A não adição de endereços IP específicos da região à sua lista de permissões pode resultar em erros ou em não desempenho ao usar fontes.

### Região Leste dos EUA

- `20.41.2.0/23`
- `20.41.4.0/26`
- `20.44.17.80/28`
- `20.49.102.16/29`
- `40.70.148.160/28`
- `52.167.107.224/28`

### Região da Europa Ocidental

- `13.69.67.192/28`
- `13.69.107.112/28`
- `13.69.112.128/28`
- `40.74.24.192/26`
- `40.74.26.0/23`
- `40.113.176.232/29`
- `52.236.187.112/28`

### Austrália Oriental

- `13.70.74.144/28`
- `20.37.193.0/25`
- `20.37.193.128/26`
- `20.37.198.224/29`
- `40.79.163.80/28`
- `40.79.171.160/28`

## Restrições de nomenclatura para arquivos e diretórios

A seguir, há uma lista de restrições que você deve levar em conta ao nomear seu arquivo ou diretório de armazenamento na nuvem.

- Nomes de diretório e de componente de arquivo não podem exceder 255 caracteres.
- Os nomes de diretório e arquivo não podem terminar com uma barra (`/`). Se fornecido, ele será removido automaticamente.
- Os seguintes caracteres de URL reservados devem ser escapados corretamente: `! * ' ( ) ; : @ & = + $ , / ? % # [ ]`
- Os seguintes caracteres não são permitidos: `" \ / : | < > * ?`.
- Caracteres de caminho de URL ilegais não permitidos. Pontos de código como `\uE000`, embora válidos em nomes de arquivo NTFS, não são caracteres Unicode válidos. Além disso, alguns caracteres ASCII ou Unicode, como caracteres de controle (0x00 a 0x1F, \u0081 etc.), também não são permitidos. Para obter as regras que regem strings Unicode em HTTP/1.1, consulte [RFC 2616, Seção 2.2: Regras](https://www.ietf.org/rfc/rfc2616.txt) básicas e [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Os seguintes nomes de arquivo não são permitidos: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, caractere de ponto (..) e dois caracteres de ponto (.).

## Conectar-se [!DNL Azure Blob] a [!DNL Platform]

A documentação abaixo fornece informações sobre como conectar o Blob do Azure à plataforma usando APIs ou a interface do usuário:

### Uso de APIs

- [Criar um conector Blob do Azure usando a API de Serviço de Fluxo](../../tutorials/api/create/cloud-storage/blob.md)
- [Explore um sistema de armazenamento em nuvem usando a API de Serviço de Fluxo](../../tutorials/api/explore/cloud-storage.md)
- [Coletar dados de armazenamento na nuvem usando a API de Serviço de Fluxo](../../tutorials/api/collect/cloud-storage.md)

### Uso da interface

- [Criar um conector de origem do Blob do Azure na interface do usuário](../../tutorials/ui/create/cloud-storage/blob.md)
- [Configurar um fluxo de dados para um conector de armazenamento em nuvem na interface do usuário](../../tutorials/ui/dataflow/batch/cloud-storage.md)