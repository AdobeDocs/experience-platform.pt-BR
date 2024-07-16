---
title: Visão geral da Source para resolução de identidade corporativa do Merkury
description: Saiba como conectar o Merkury Enterprise Identity Resolution à Adobe Experience Platform usando a interface do usuário.
last-substantial-update: 2023-12-12T00:00:00Z
badge: Beta
exl-id: c5eaa561-d620-4c82-bce1-972d0a422c3f
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 0%

---

# [!DNL Merkury Enterprise Identity Resolution]

>[!NOTE]
>
>A origem [!DNL Merkury Enterprise Identity Resolution] está na versão beta. Leia a [visão geral das fontes](../../home.md#terms-and-conditions) para obter mais informações sobre o uso de fontes com rótulo beta.

A Adobe Experience Platform oferece suporte para assimilação de dados de um aplicativo de parceiro de dados. O suporte para parceiros de dados inclui [!DNL Merkury Enterprise Identity Resolution].

Você pode usar o [!DNL Merkury] da [!DNL Merkle] para reconhecer mais visitantes digitais, mesmo sem o uso de cookies, e fornecer experiências relevantes e personalizadas das quais seu cliente precisa.

Você pode utilizar a **ID de pessoa** como parte da origem [!DNL Merkury] para combinar tudo o que sua organização sabe sobre um indivíduo em um único perfil abrangente. Esses detalhes podem incluir:

- comportamentos digitais
- preferências de compra
- informações de identificação, como nome, endereço de email, endereço físico ou ID do dispositivo.

É possível formatar dados assimilados como JSON, XDM Parquet ou delimitados do Experience Data Model (XDM). Cada etapa do processo é integrada ao trabalho das origens

![Uma ilustração do fluxo de trabalho de processamento de dados para a fonte do Merkury.](../../images/tutorials/create/merkury-enterprise-identity-resolution-assets/architecture.png)

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

## Pré-requisitos

Você deve atender aos seguintes pré-requisitos para começar a usar a origem [!DNL Merkury]:

- Você deve concluir a configuração do [!DNL Merkury] com a equipe do [!DNL Merkury].
- Você deve recuperar suas credenciais (chave de acesso, chave secreta e nome do bucket) da equipe do [!DNL Merkury]. 

>[!NOTE]
>
>Um caminho de arquivo como `myBucket/folder/subfolder/subsubfolder/abc.csv` pode levá-lo a acessar apenas `subsubfolder/abc.csv`. Se quiser acessar a subpasta, especifique o parâmetro de bucket como myBucket e folderPath como folder/subfolder para garantir que a exploração de arquivos comece na subpasta, em vez de `subsubfolder/abc.csv`.

## Próximas etapas

Ao ler este documento, você concluiu os pré-requisitos de configuração necessários para trazer dados da sua conta [!DNL Merkury] para o Experience Platform. Agora você pode prosseguir para o guia em [conectando [!DNL Merkury] ao Experience Platform usando a interface de usuário](../../tutorials/ui/create/data-partners/merkury.md).
