---
keywords: Experience Platform;home;tópicos populares;Oracle Object Storage;oracle object storage
solution: Experience Platform
title: Visão geral do Oracle Object Storage Source Connector
description: Saiba como conectar o Oracle Object Storage ao Adobe Experience Platform usando APIs ou a interface do usuário.
exl-id: 5e8b85c8-9f01-49a6-9556-7b9c7518fb4b
source-git-commit: 06b2108715ce368ff4ecf5c6c7dd3a327d9f61b1
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 0%

---

# Conector de armazenamento de objetos do Oracle

O Adobe Experience Platform fornece conectividade nativa para provedores de nuvem, como o AWS, [!DNL Google Cloud Platform], permitindo que você traga dados desses sistemas para o Experience Platform para uso em serviços e destinos downstream.

As fontes de armazenamento na nuvem podem trazer seus dados para a Experience Platform sem precisar baixar, formatar ou carregar. Os dados assimilados podem ser formatados como XDM JSON, XDM Parquet ou delimitados. Cada etapa do processo é integrada ao fluxo de trabalho de origens. O Experience Platform permite trazer dados de [!DNL Oracle Object Storage] por meio de lotes.

## INCLUO NA LISTA DE PERMISSÕES de endereços IP

Você deve adicionar endereços IP específicos da região ao incluo na lista de permissões antes de conectar suas fontes à Experience Platform. Para obter mais informações, leia o guia sobre [como ler os endereços IP de incluir na lista de permissões para se conectar ao Experience Platform](../../ip-address-allow-list.md) para obter mais informações.

## Restrições de nomenclatura para arquivos e diretórios

Veja a seguir uma lista de restrições que você deve considerar ao nomear o arquivo ou diretório de armazenamento em nuvem:

- Os nomes dos componentes de diretório e arquivo não podem exceder 255 caracteres.
- Nomes de diretório e arquivo não podem terminar com uma barra (`/`). Se fornecido, ele será removido automaticamente.
- Os seguintes caracteres de URL reservados devem ter um escape adequado: `! ' ( ) ; @ & = + $ , % # [ ]`
- Os seguintes caracteres não são permitidos: `" \ / : | < > * ?`.
- Caracteres de caminho de URL inválidos não permitidos. Pontos de código como `\uE000`, embora válidos em nomes de arquivo NTFS, não são caracteres Unicode válidos. Além disso, alguns caracteres ASCII ou Unicode também não são permitidos, como caracteres de controle (0x00 a 0x1F, \u0081 etc.). Para regras que regem cadeias de caracteres Unicode em HTTP/1.1, consulte [RFC 2616, Seção 2.2: Regras Básicas](https://www.ietf.org/rfc/rfc2616.txt) e [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Os seguintes nomes de arquivo não são permitidos: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, caractere de ponto (.) e dois caracteres de ponto (..).

## Conectar [!DNL Oracle Object Storage] ao Experience Platform

A documentação abaixo fornece informações sobre como conectar o Oracle Object Storage à Adobe Experience Platform usando APIs ou a interface do usuário:

### Uso de APIs

- [Criar uma conexão básica de Armazenamento de objetos do Oracle usando a API do Serviço de fluxo](../../tutorials/api/create/cloud-storage/oracle-object-storage.md)
- [Explore a estrutura de dados e o conteúdo de uma fonte de armazenamento na nuvem usando a API do serviço de fluxo](../../tutorials/api/explore/cloud-storage.md)
- [Criar um fluxo de dados para uma fonte de armazenamento na nuvem usando a API do Serviço de fluxo](../../tutorials/api/collect/cloud-storage.md)

### Uso da interface

- [Criar uma conexão de origem do Oracle Object Storage na interface do usuário](../../tutorials/ui/create/cloud-storage/oracle-object-storage.md)
- [Criar um fluxo de dados para uma conexão de armazenamento na nuvem na interface](../../tutorials/ui/dataflow/batch/cloud-storage.md)
