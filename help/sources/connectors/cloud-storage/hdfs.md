---
keywords: Experience Platform;página inicial;tópicos populares;HDFS;hdfs;Apache HDFS;apache hdfs
solution: Experience Platform
title: Visão geral do Conector de origem do Apache HDFS
description: Saiba como conectar o Apache HDFS ao Adobe Experience Platform usando APIs ou a interface do usuário.
exl-id: 1f156f7b-a19d-4dcf-a51d-ab6cb396d8f7
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 0%

---

# (Beta) [!DNL Apache] Conector HDFS

>[!NOTE]
>
>O conector Apache HDFS está na versão beta. Consulte a [Visão geral das fontes](../../home.md#terms-and-conditions) para obter mais informações sobre o uso de conectores rotulados com beta.

O Adobe Experience Platform fornece conectividade nativa para provedores de nuvem, como o AWS, [!DNL Google Cloud Platform], e [!DNL Azure], permitindo que você traga seus dados desses sistemas. Os dados assimilados podem ser formatados como JSON, Parquet ou delimitados. O suporte para provedores de armazenamento em nuvem inclui [!DNL Apache] HDFS.

## LISTA DE PERMISSÕES de endereço IP

Uma lista de endereços IP deve ser adicionada a uma lista de permissões antes de trabalhar com conectores de origem. Falha ao adicionar endereços IP específicos da região à lista de permissões pode levar a erros ou ao não desempenho ao usar origens. Consulte a [LISTA DE PERMISSÕES de endereço IP](../../ip-address-allow-list.md) para obter mais informações.

## Restrições de nomenclatura para arquivos e diretórios

Veja a seguir uma lista de restrições que você deve considerar ao nomear seu arquivo ou diretório de armazenamento em nuvem.

- Os nomes dos componentes de diretório e arquivo não podem exceder 255 caracteres.
- Nomes de diretório e arquivo não podem terminar com uma barra (`/`). Se fornecido, ele será removido automaticamente.
- Os seguintes caracteres de URL reservados devem ter escape adequado: `! ' ( ) ; @ & = + $ , % # [ ]`
- Os seguintes caracteres não são permitidos: `" \ / : | < > * ?`.
- Caracteres de caminho de URL inválidos não permitidos. Pontos de código como `\uE000`, embora sejam válidos em nomes de arquivo NTFS, não são caracteres Unicode válidos. Além disso, alguns caracteres ASCII ou Unicode, como caracteres de controle (0x00 a 0x1F, \u0081 etc.), também não são permitidos. Para obter as regras que regem strings Unicode em HTTP/1.1, consulte [RFC 2616, Seção 2.2: regras básicas](https://www.ietf.org/rfc/rfc2616.txt) e [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Os seguintes nomes de arquivo não são permitidos: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, caractere de ponto (.) e dois caracteres de ponto (..).

## Conectar [!DNL Apache] HDFS para [!DNL Platform]

A documentação abaixo fornece informações sobre como se conectar [!DNL Apache] HDFS para [!DNL Platform] uso de APIs ou da interface do usuário:

### Uso de APIs

- [Criar uma conexão de base HDFS usando a API do Serviço de Fluxo](../../tutorials/api/create/cloud-storage/hdfs.md)
- [Explore a estrutura de dados e o conteúdo de uma fonte de armazenamento na nuvem usando a API do serviço de fluxo](../../tutorials/api/explore/cloud-storage.md)
- [Criar um fluxo de dados para uma fonte de armazenamento na nuvem usando a API do Serviço de fluxo](../../tutorials/api/collect/cloud-storage.md)

### Uso da interface

- [Criar uma conexão de origem Apache HDFS na interface](../../tutorials/ui/create/cloud-storage/hdfs.md)
- [Criar um fluxo de dados para uma conexão de armazenamento na nuvem na interface](../../tutorials/ui/dataflow/batch/cloud-storage.md)
