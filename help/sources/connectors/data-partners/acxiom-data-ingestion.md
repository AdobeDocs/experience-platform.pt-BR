---
title: Assimilação de dados da Acxiom
description: Saiba como assimilar dados do  [!DNL Acxiom]  no Real-Time Customer Data Platform, enriquecer perfis primários e melhorar o público-alvo e ativar em canais de marketing.
exl-id: 3bbbe4e1-5e34-4104-bf39-2c452865b807
source-git-commit: e402a58f51de49b26f9d279cebf551ec11e4698f
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 1%

---

# [!DNL Acxiom Data Ingestion]

Use a fonte [!DNL Acxiom Data Ingestion] para assimilar dados [!DNL Acxiom] na Real-Time Customer Data Platform e enriquecer perfis próprios. Em seguida, você pode usar seus perfis primários enriquecidos com [!DNL Acxiom] para melhorar os públicos e ativar em canais de marketing.

![acxiom-data-ingestion-workflow](../../images/tutorials/create/acxiom-data-enhancement-import/acxiom-data-ingestion.png)

Leia o documento abaixo para obter informações sobre como configurar sua conta de origem do [!DNL Acxiom Data Ingestion].

## Pré-requisitos {#prerequisites}

Para conectar sua conta do [!DNL Acxiom Data Ingestion] à Experience Platform, você deve fornecer valores para as seguintes credenciais de autenticação:

| Credencial | Descrição |
| --- | --- |
| Chave de autenticação [!DNL Acxiom] | A chave de autenticação. Você pode recuperar esse valor da equipe [!DNL Acxiom]. |
| [!DNL Amazon S3] chave de acesso | A ID da chave de acesso do seu bucket. Você pode recuperar esse valor da equipe [!DNL Acxiom]. |
| [!DNL Amazon S3] chave secreta | A ID da chave secreta para o seu bucket. Você pode recuperar esse valor da equipe [!DNL Acxiom]. |
| Nome do bucket | Esse é o seu bucket onde os arquivos serão compartilhados. Você pode recuperar esse valor da equipe [!DNL Acxiom]. |

## INCLUIR NA LISTA DE PERMISSÕES endereço IP

Antes de usar conectores de origem, você deve adicionar os endereços IP necessários para sua região ao incluo na lista de permissões de pesquisa. Se você não adicionar esses endereços IP, os conectores de origem poderão não funcionar corretamente ou poderão gerar erros. Para obter instruções detalhadas e a lista de endereços IP permitidos, leia a página [inclui na lista de permissões de endereço IP](../../ip-address-allow-list.md).

### Configurar permissões no Experience Platform

Você deve ter as permissões **[!UICONTROL Exibir Fontes]** e **[!UICONTROL Gerenciar Fontes]** habilitadas para sua conta a fim de conectar sua conta do [!DNL Acxiom Data Ingestion] à Experience Platform. Entre em contato com o administrador do produto para obter as permissões necessárias. Para obter mais informações, leia o [guia da interface do usuário de controle de acesso](../../../access-control/ui/overview.md).

### Restrições de nomenclatura para arquivos e diretórios

As restrições listadas abaixo devem ser consideradas ao nomear o arquivo ou diretório de armazenamento em nuvem:

- Os nomes dos componentes de diretório e arquivo não podem exceder 255 caracteres.
- Nomes de diretório e arquivo não podem terminar com uma barra (`/`). Se fornecido, ele será removido automaticamente.
- Os seguintes caracteres de URL reservados devem ter um escape adequado: `! ' ( ) ; @ & = + $ , % # [ ]`
- Os seguintes caracteres não são permitidos: `" \ / : | < > * ?`.
- Caracteres de caminho de URL inválidos não são permitidos. Pontos de código como `\uE000`, embora válidos em nomes de arquivo NTFS, não são caracteres Unicode válidos. Além disso, alguns caracteres ASCII ou Unicode, como caracteres de controle (0x00 a 0x1F, \u0081 etc.), também não são permitidos. Para regras que regem cadeias de caracteres Unicode em HTTP/1.1, consulte [RFC 2616, Seção 2.2: Regras Básicas](https://www.ietf.org/rfc/rfc2616.txt) e [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Os seguintes nomes de arquivo não são permitidos: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, caractere de ponto (.) e dois caracteres de ponto (..).

## Próximas etapas

Ao ler este documento, você concluiu a configuração de pré-requisito necessária para trazer dados da sua conta do [!DNL Acxiom] para a Experience Platform. Agora você pode prosseguir para o guia em [conectando [!DNL Acxiom Data Ingestion] ao Experience Platform usando a interface do usuário](../../tutorials/ui/create/data-partners/acxiom-data-ingestion.md).
