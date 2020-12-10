---
keywords: Experience Platform;home;popular topics;SFTP;sftp
solution: Experience Platform
title: Conector SFTP
topic: overview
description: A documentação abaixo fornece informações sobre como conectar um servidor SFTP à plataforma usando APIs ou a interface do usuário.
translation-type: tm+mt
source-git-commit: 5e5ac80e0c79b3cc0354b469edc036523e29b45d
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 0%

---


# Conector SFTP (Beta)

>[!NOTE]
>
>O conector SFTP está em beta. Consulte a visão geral [das](../../home.md#terms-and-conditions) Fontes para obter mais informações sobre o uso de conectores com rótulo beta.

A Adobe Experience Platform fornece conectividade nativa para provedores de nuvem como AWS, [!DNL Google Cloud Platform]e [!DNL Azure], permitindo que você traga seus dados desses sistemas.

As fontes de armazenamentos na nuvem podem inserir seus próprios dados [!DNL Platform] sem a necessidade de baixar, formatar ou fazer upload. Os dados ingeridos podem ser formatados como XDM JSON, XDM parquet ou delimitados. Cada etapa do processo é integrada ao fluxo de trabalho de Fontes. [!DNL Platform] permite trazer dados de um servidor FTP ou SFTP por lotes.

## LISTA DE PERMISSÕES de endereço IP

Uma lista de endereços IP deve ser adicionada a uma lista de permissões antes de trabalhar com conectores de origem. A não adição de endereços IP específicos da região à sua lista de permissões pode resultar em erros ou em não desempenho ao usar fontes. Consulte a página lista de permissões [do endereço](../../ip-address-allow-list.md) IP para obter mais informações.

## Restrições de nomenclatura para arquivos e diretórios

A seguir, há uma lista de restrições que você deve levar em conta ao nomear seu arquivo ou diretório de armazenamento na nuvem.

- Nomes de diretório e de componente de arquivo não podem exceder 255 caracteres.
- Os nomes de diretório e arquivo não podem terminar com uma barra (`/`). Se fornecido, ele será removido automaticamente.
- Os seguintes caracteres de URL reservados devem ser escapados corretamente: `! * ' ( ) ; : @ & = + $ , / ? % # [ ]`
- Os seguintes caracteres não são permitidos: `" \ / : | < > * ?`.
- Caracteres de caminho de URL ilegais não permitidos. Pontos de código como `\uE000`, embora válidos em nomes de arquivo NTFS, não são caracteres Unicode válidos. Além disso, alguns caracteres ASCII ou Unicode, como caracteres de controle (0x00 a 0x1F, \u0081 etc.), também não são permitidos. Para obter as regras que regem strings Unicode em HTTP/1.1, consulte [RFC 2616, Seção 2.2: Regras](https://www.ietf.org/rfc/rfc2616.txt) básicas e [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Os seguintes nomes de arquivo não são permitidos: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, caractere de ponto (..) e dois caracteres de ponto (.).

## Conectar SFTP a [!DNL Platform]

>[!IMPORTANT]
>
>Os usuários devem desativar a Autenticação interativa do teclado na configuração do servidor SFTP antes da conexão. Desativar a configuração permitirá que as senhas sejam inseridas manualmente, em vez de serem inseridas por meio de um serviço ou programa. Consulte o documento [](https://doc.componentpro.com/ComponentPro-Sftp/authenticating-with-a-keyboard-interactive-authentication) Component Pro para obter mais informações sobre Autenticação interativa do teclado.

A documentação abaixo fornece informações sobre como conectar um servidor SFTP a [!DNL Platform] APIs ou à interface do usuário:

### Uso das APIs

- [Criar um conector SFTP usando a API de Serviço de Fluxo](../../tutorials/api/create/cloud-storage/sftp.md)
- [Explore um sistema de armazenamento em nuvem usando a API de Serviço de Fluxo](../../tutorials/api/explore/cloud-storage.md)
- [Coletar dados de armazenamento na nuvem usando a API de Serviço de Fluxo](../../tutorials/api/collect/cloud-storage.md)

### Uso da interface

- [Criar um conector de origem SFTP na interface do usuário](../../tutorials/ui/create/cloud-storage/sftp.md)
- [Configurar um fluxo de dados para um conector de armazenamento em nuvem na interface do usuário](../../tutorials/ui/dataflow/batch/cloud-storage.md)