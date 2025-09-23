---
title: Importação de dados de prospecção da Acxiom
description: Saiba como conectar dados de prospecção da Acxiom à Adobe Experience Platform e à Adobe Real-Time CDP por meio da interface.
exl-id: 6df674d9-c14b-42ea-a287-5377484e567d
source-git-commit: e402a58f51de49b26f9d279cebf551ec11e4698f
workflow-type: tm+mt
source-wordcount: '544'
ht-degree: 5%

---

# [!DNL Acxiom Prospecting Data Import]

A Adobe Experience Platform oferece suporte para assimilação de dados de um aplicativo de parceiro de dados. O suporte para parceiros de dados e identidade inclui [!DNL Acxiom Prospecting Data Import].

A importação de dados de prospecção do [!DNL Acxiom] para o Adobe Real-Time Customer Data Platform é um processo para fornecer os públicos-alvo de prospecção mais produtivos possíveis. O [!DNL Acxiom] coleta dados primários da Real-Time CDP por meio de uma exportação segura e executa esses dados por meio de um sistema premiado de higiene e resolução de identidades. Um arquivo de dados que pode ser usado como uma lista de supressão é produzido. Este arquivo de dados é comparado ao banco de dados [!DNL Acxiom Global], o que permite que as listas de clientes potenciais sejam personalizadas para importação.

Você pode usar a origem [!DNL Acxiom] para recuperar e mapear respostas do serviço de prospecto [!DNL Acxiom] usando [!DNL Amazon S3] como ponto de depósito.

![acxiom-prospecting-workflow](../../images/tutorials/create/acxiom-prospect-suppression-data-sourcing/acxiom-prospecting.png)

Leia o documento abaixo para obter informações sobre como configurar sua conta de origem do [!DNL Acxiom Prospecting Data Import].

## Pré-requisitos

Para acessar seu bucket no Experience Platform, você precisa fornecer valores válidos para as seguintes credenciais:

| Credencial | Descrição |
| --- | --- |
| Chave de autenticação [!DNL Acxiom] | A chave de autenticação. Você pode recuperar esse valor da equipe [!DNL Acxiom]. |
| [!DNL Amazon S3] chave de acesso | A ID da chave de acesso do seu bucket. Você pode recuperar esse valor da equipe [!DNL Acxiom]. |
| [!DNL Amazon S3] chave secreta | A ID da chave secreta para o seu bucket. Você pode recuperar esse valor da equipe [!DNL Acxiom]. |
| Nome do bucket | Esse é o seu bucket onde os arquivos serão compartilhados. Você pode recuperar esse valor da equipe [!DNL Acxiom]. |

## INCLUIR NA LISTA DE PERMISSÕES endereço IP

Antes de usar conectores de origem, você deve adicionar os endereços IP necessários para sua região ao incluo na lista de permissões de pesquisa. Se você não adicionar esses endereços IP, os conectores de origem poderão não funcionar corretamente ou poderão gerar erros. Para obter instruções detalhadas e a lista de endereços IP permitidos, leia a página [inclui na lista de permissões de endereço IP](../../ip-address-allow-list.md).

### Configurar permissões no Experience Platform

Você deve ter as permissões **[!UICONTROL Exibir Fontes]** e **[!UICONTROL Gerenciar Fontes]** habilitadas para sua conta a fim de conectar sua conta do [!DNL Acxiom Prospecting Data Import] à Experience Platform. Entre em contato com o administrador do produto para obter as permissões necessárias. Para obter mais informações, leia o [guia da interface do usuário de controle de acesso](../../../access-control/abac/ui/permissions.md).

## Restrições de nomenclatura para arquivos e diretórios

As restrições listadas abaixo devem ser consideradas ao nomear o arquivo ou diretório de armazenamento em nuvem:

- Os nomes dos componentes de diretório e arquivo não podem exceder 255 caracteres.
- Nomes de diretório e arquivo não podem terminar com uma barra (`/`). Se fornecido, ele será removido automaticamente.
- Os seguintes caracteres de URL reservados devem ter um escape adequado: `! ' ( ) ; @ & = + $ , % # [ ]`
- Os seguintes caracteres não são permitidos: `" \ / : | < > * ?`.
- Caracteres de caminho de URL inválidos não são permitidos. Pontos de código como `\uE000`, embora válidos em nomes de arquivo NTFS, não são caracteres Unicode válidos. Além disso, alguns caracteres ASCII ou Unicode, como caracteres de controle (0x00 a 0x1F, \u0081 etc.), também não são permitidos. Para regras que regem cadeias de caracteres Unicode em HTTP/1.1, consulte [RFC 2616, Seção 2.2: Regras Básicas](https://www.ietf.org/rfc/rfc2616.txt) e [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Os seguintes nomes de arquivo não são permitidos: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, caractere de ponto (.) e dois caracteres de ponto (..).

## Próximas etapas

Ao ler este documento, você concluiu a configuração de pré-requisito necessária para trazer dados da sua conta do [!DNL Acxiom] para a Experience Platform. Agora você pode prosseguir para o guia em [conectando [!DNL Acxiom Prospecting Data Import] ao Experience Platform usando a interface do usuário](../../tutorials/ui/create/data-partners/acxiom-prospecting-data-import.md).
