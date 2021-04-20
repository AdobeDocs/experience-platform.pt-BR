---
keywords: Experience Platform;home;popular topics;Oracle Object Armazenamento;oracle object armazenamento
solution: Experience Platform
title: Visão geral do conector de origem do Armazenamento do objeto Oracle
topic: overview
description: Saiba como conectar o Armazenamento Oracle Object à Adobe Experience Platform usando APIs ou a interface do usuário.
translation-type: tm+mt
source-git-commit: 04c605aedd4c52b54d0f075c169ce919650cdee9
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 0%

---


# Conector Oracle Object Armazenamento

A Adobe Experience Platform fornece conectividade nativa para provedores de nuvem como AWS, [!DNL Google Cloud Platform], permitindo que você coloque dados desses sistemas na Plataforma para uso em serviços e destinos de downstream.

As fontes de armazenamentos na nuvem podem trazer seus dados para a plataforma sem a necessidade de baixar, formatar ou fazer upload. Os dados ingeridos podem ser formatados como XDM JSON, XDM Parquet ou delimitados. Cada etapa do processo é integrada ao fluxo de trabalho de fontes. A plataforma permite trazer dados de [!DNL Oracle Object Storage] por lotes.

## LISTA DE PERMISSÕES de endereço IP

Uma lista de endereços IP deve ser adicionada a uma lista de permissões antes de trabalhar com conectores de origem. A não adição de endereços IP específicos da região à sua lista de permissões pode resultar em erros ou em não desempenho ao usar fontes. Consulte o documento [lista de permissões de endereço IP](../../ip-address-allow-list.md) para obter mais informações.

## Restrições de nomenclatura para arquivos e diretórios

Esta é uma lista de restrições que você deve considerar ao nomear seu arquivo ou diretório de armazenamento na nuvem:

- Nomes de diretório e de componente de arquivo não podem exceder 255 caracteres.
- Os nomes de diretório e arquivo não podem terminar com uma barra (`/`). Se fornecido, ele será removido automaticamente.
- Os seguintes caracteres de URL reservados devem ser escapados corretamente: `! ' ( ) ; @ & = + $ , % # [ ]`
- Os seguintes caracteres não são permitidos: `" \ / : | < > * ?`.
- Caracteres de caminho de URL ilegais não permitidos. Pontos de código como `\uE000`, embora válidos em nomes de arquivo NTFS, não são caracteres Unicode válidos. Além disso, alguns caracteres ASCII ou Unicode também não são permitidos, como caracteres de controle (0x00 a 0x1F, \u0081, etc.). Para obter as regras que regem strings Unicode em HTTP/1.1, consulte [RFC 2616, Seção 2.2: Regras básicas](https://www.ietf.org/rfc/rfc2616.txt) e [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Os seguintes nomes de arquivo não são permitidos: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, caractere de ponto (..) e dois caracteres de ponto (.).

## Conectar [!DNL Oracle Object Storage] à plataforma

A documentação abaixo fornece informações sobre como conectar o Armazenamento Oracle Object à Adobe Experience Platform usando APIs ou a interface do usuário:

### Uso de APIs

- [Criar uma conexão de origem de Armazenamento de objeto de Oracle usando a API de Serviço de Fluxo](../../tutorials/api/create/cloud-storage/oracle-object-storage.md)
- [Explore um sistema de armazenamento em nuvem usando a API de Serviço de Fluxo](../../tutorials/api/explore/cloud-storage.md)
- [Coletar dados de armazenamento na nuvem usando a API de Serviço de Fluxo](../../tutorials/api/collect/cloud-storage.md)

### Uso da interface

- [Criar uma conexão de origem de Armazenamento de objeto de Oracle na interface do usuário](../../tutorials/ui/create/cloud-storage/oracle-object-storage.md)
- [Configurar um fluxo de dados para uma conexão de armazenamento em nuvem na interface do usuário](../../tutorials/ui/dataflow/batch/cloud-storage.md)