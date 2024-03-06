---
title: Importação de dados de prospecção da Acxiom
description: Saiba como conectar os dados de prospecção da Acxiom ao Adobe Experience Platform e à Adobe Real-time Customer Data Platform usando a interface do usuário do.
badge: Beta
source-git-commit: 64975ccb6a44730489427cef745f3dbce5bcedf1
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 1%

---

# [!DNL Acxiom Prospecting Data Import]

>[!NOTE]
>
>A variável [!DNL Acxiom Prospecting Data Import] a fonte está na versão beta. Leia as [visão geral das origens](../../home.md#terms-and-conditions) para obter mais informações sobre o uso de fontes rotuladas como beta.

A Adobe Experience Platform oferece suporte para assimilação de dados de um aplicativo de parceiro de dados. O suporte para parceiros de dados e identidade inclui [!DNL Acxiom Prospecting Data Import].

[!DNL Acxiom]A Importação de dados de prospecção da para o Adobe Real-time Customer Data Platform é um processo para fornecer os públicos-alvo de prospecção mais produtivos possíveis. [!DNL Acxiom] O pega dados primários do Real-Time CDP por meio de uma exportação segura e executa esses dados por meio de um sistema premiado de higiene e resolução de identidades. Um arquivo de dados que pode ser usado como uma lista de supressão é produzido. Esse arquivo de dados é comparado com o [!DNL Acxiom Global] banco de dados, que permite que as listas de clientes potenciais sejam personalizadas para importação.

Você pode usar o [!DNL Acxiom] origem a ser recuperada e mapear respostas do [!DNL Acxiom] serviço de cliente potencial usando [!DNL Amazon S3] como um ponto de soltar.

## Pré-requisitos

Para acessar seu bucket no Experience Platform, é necessário fornecer valores válidos para as seguintes credenciais:

| Credencial | Descrição |
| --- | --- |
| [!DNL Acxiom] chave de autenticação | A chave de autenticação. Você pode recuperar esse valor da variável [!DNL Acxiom] equipe. |
| [!DNL Amazon S3] chave de acesso | A ID da chave de acesso do seu bucket. Você pode recuperar esse valor da variável [!DNL Acxiom] equipe. |
| [!DNL Amazon S3] chave secreta | A ID da chave secreta para o seu bucket. Você pode recuperar esse valor da variável [!DNL Acxiom] equipe. |
| Nome do bucket | Esse é o seu bucket onde os arquivos serão compartilhados. Você pode recuperar esse valor da variável [!DNL Acxiom] equipe. |

### Permissões

Você deve ter ambos **[!UICONTROL Exibir fontes]** e **[!UICONTROL Gerenciar fontes]** permissões habilitadas para sua conta para conectar seu [!DNL Acxiom Prospecting Data Import] conta para Experience Platform. Entre em contato com o administrador do produto para obter as permissões necessárias. Para obter mais informações, leia a [guia da interface do usuário de controle de acesso](../../../access-control/abac/ui/permissions.md).

## LISTA DE PERMISSÕES de endereço IP

Uma lista de endereços IP deve ser adicionada a uma lista de permissões antes de trabalhar com conectores de origem. Falha ao adicionar endereços IP específicos da região à lista de permissões pode levar a erros ou ao não desempenho ao usar origens. Consulte a [LISTA DE PERMISSÕES de endereço IP](../../ip-address-allow-list.md) para obter mais informações.

## Restrições de nomenclatura para arquivos e diretórios

As restrições listadas abaixo devem ser consideradas ao nomear o arquivo ou diretório de armazenamento em nuvem:

- Os nomes dos componentes de diretório e arquivo não podem exceder 255 caracteres.
- Nomes de diretório e arquivo não podem terminar com uma barra (`/`). Se fornecido, ele será removido automaticamente.
- Os seguintes caracteres de URL reservados devem ter escape adequado: `! ' ( ) ; @ & = + $ , % # [ ]`
- Os seguintes caracteres não são permitidos: `" \ / : | < > * ?`.
- Caracteres de caminho de URL inválidos não são permitidos. Pontos de código como `\uE000`, embora sejam válidos em nomes de arquivo NTFS, não são caracteres Unicode válidos. Além disso, alguns caracteres ASCII ou Unicode, como caracteres de controle (0x00 a 0x1F, \u0081 etc.), também não são permitidos. Para obter as regras que regem strings Unicode em HTTP/1.1, consulte [RFC 2616, Seção 2.2: regras básicas](https://www.ietf.org/rfc/rfc2616.txt) e [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Os seguintes nomes de arquivo não são permitidos: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, caractere de ponto (.) e dois caracteres de ponto (..).

## Próximas etapas

Ao ler este documento, você concluiu a configuração de pré-requisito necessária para trazer dados do seu [!DNL Acxiom] conta para Experience Platform. Agora você pode prosseguir para o guia em [conectando [!DNL Acxiom Prospecting Data Import] para Experience Platform usando a interface do usuário](../../tutorials/ui/create/data-partners/acxiom-prospecting-data-import.md).