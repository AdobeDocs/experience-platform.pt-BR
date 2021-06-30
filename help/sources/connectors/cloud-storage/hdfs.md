---
keywords: Experience Platform, home, tópicos populares, HDFS, hdfs, Apache HDFS, apache hdfs
solution: Experience Platform
title: Visão geral do conector de origem do Apache HDFS
topic-legacy: overview
description: Saiba como conectar o Apache HDFS ao Adobe Experience Platform usando APIs ou a interface do usuário.
exl-id: 1f156f7b-a19d-4dcf-a51d-ab6cb396d8f7
source-git-commit: 1f9948d6e419ee5d6a021a589378f7aa990b7291
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 0%

---

# (Beta) [!DNL Apache] Conector HDFS

>[!NOTE]
>
>O conector HDFS do Apache está em beta. Consulte a [Visão geral das Fontes](../../home.md#terms-and-conditions) para obter mais informações sobre o uso de conectores com marca beta.

O Adobe Experience Platform fornece conectividade nativa para provedores de nuvem como AWS, [!DNL Google Cloud Platform] e [!DNL Azure], permitindo que você traga seus dados desses sistemas. Os dados assimilados podem ser formatados como JSON, Parquet ou delimitados. O suporte para provedores de armazenamento em nuvem inclui [!DNL Apache] HDFS.

## LISTA DE PERMISSÕES de endereço IP

Uma lista de endereços IP deve ser adicionada a uma lista de permissões antes de trabalhar com conectores de origem. A não adição de endereços IP específicos da região à lista de permissões pode causar erros ou não desempenho ao usar fontes. Consulte a página [lista de permissões de endereço IP](../../ip-address-allow-list.md) para obter mais informações.

## Restrições de nomenclatura para arquivos e diretórios

Esta é uma lista de restrições que devem ser consideradas ao nomear seu arquivo ou diretório de armazenamento em nuvem.

- Os nomes de componentes de diretório e arquivo não podem exceder 255 caracteres.
- Os nomes de diretório e arquivo não podem terminar com uma barra (`/`). Se fornecido, ele será removido automaticamente.
- Os seguintes caracteres de URL reservados devem ser evitados corretamente: `! ' ( ) ; @ & = + $ , % # [ ]`
- Os seguintes caracteres não são permitidos: `" \ / : | < > * ?`.
- Caracteres de caminho de URL inválidos não permitidos. Pontos de código como `\uE000`, enquanto válidos em nomes de arquivo NTFS, não são caracteres Unicode válidos. Além disso, alguns caracteres ASCII ou Unicode, como caracteres de controle (0x00 a 0x1F, \u0081, etc.), também não são permitidos. Para regras que regem cadeias de caracteres Unicode no HTTP/1.1, consulte [RFC 2616, Seção 2.2: Regras básicas](https://www.ietf.org/rfc/rfc2616.txt) e [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Os seguintes nomes de arquivo não são permitidos: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, caractere de ponto (...) e dois caracteres de ponto (.).

## Conecte [!DNL Apache] HDFS a [!DNL Platform]

A documentação abaixo fornece informações sobre como conectar [!DNL Apache] HDFS a [!DNL Platform] usando APIs ou a interface do usuário:

### Uso de APIs

- [Criar uma conexão base HDFS usando a API do Serviço de Fluxo](../../tutorials/api/create/cloud-storage/hdfs.md)
- [Explore a estrutura de dados e o conteúdo de uma fonte de armazenamento em nuvem usando a API do Serviço de Fluxo](../../tutorials/api/explore/cloud-storage.md)
- [Criar um fluxo de dados para uma fonte de armazenamento em nuvem usando a API do Serviço de Fluxo](../../tutorials/api/collect/cloud-storage.md)

### Uso da interface do usuário

- [Criar uma conexão de origem do Apache HDFS na interface do usuário](../../tutorials/ui/create/cloud-storage/hdfs.md)
- [Criar um fluxo de dados para uma conexão de armazenamento em nuvem na interface do usuário do](../../tutorials/ui/dataflow/batch/cloud-storage.md)
