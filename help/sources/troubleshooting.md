---
keywords: Experience Platform; home; tópicos populares; fontes; ingestão; solução de problemas; solução de problemas de fontes; perguntas frequentes sobre fontes; perguntas frequentes; conectores de origem; conector de origem; perguntas frequentes sobre conectores de origem; solução de problemas dos conectores de origem;
solution: Experience Platform
title: Solução de problemas de fontes
topic: troubleshooting
description: Este documento fornece respostas a perguntas frequentes sobre fontes no Adobe Experience Platform.
exl-id: 94875121-7d4d-4eb2-8760-aa795933dd7e
translation-type: tm+mt
source-git-commit: 827a593c046530edba701edf26d9a47918cfd8f8
workflow-type: tm+mt
source-wordcount: '663'
ht-degree: 0%

---

# (Beta) Guia de solução de problemas de fontes

Este documento fornece respostas a perguntas frequentes sobre fontes no Adobe Experience Platform. Para perguntas e solução de problemas relacionados a outros [!DNL Platform] serviços, incluindo aqueles encontrados em todas as [!DNL Platform] APIs, consulte o [Guia de solução de problemas do Experience Platform](../landing/troubleshooting.md).

## Perguntas frequentes

Veja a seguir uma lista de respostas para perguntas frequentes sobre fontes.

### Preciso fazer alterações nas nossas configurações de segurança de rede para habilitar as fontes?

Talvez seja necessário lista de permissões determinados endereços IP para ativar as fontes. Para obter mais informações, leia a documentação sobre seu conector de origem específico.

### Quais tipos de autenticação são aceitos pelas fontes?

As fontes podem ser autenticadas usando strings de conexão, nomes de usuário e senhas ou tokens e chaves de acesso. Detalhes específicos sobre os tipos de autenticação suportados podem ser encontrados na documentação do conector de origem especificado.

### Por que todas as minhas execuções recentes estão falhando?

Se você perceber que todas as execuções recentes estão falhando, suas credenciais podem ter sido alteradas ou expirado. Para corrigir esse problema, tente atualizar sua conexão com as credenciais mais recentes.

### Quais tipos de arquivo são compatíveis?

Atualmente, os tipos de arquivos suportados são arquivos delimitados, JSON e Parquet.

### Quais são as restrições nos nomes e tamanhos dos arquivos?

Esta é uma lista de restrições que você deve contabilizar para arquivos nas fontes.

- Os nomes de componentes de diretório e arquivo não podem exceder 255 caracteres.
- Os nomes de diretório e arquivo não podem terminar com uma barra (`/`). Se fornecido, ele será removido automaticamente.
- Os seguintes caracteres de URL reservados devem ser evitados corretamente: `! ' ( ) ; @ & = + $ , % # [ ]`
- Os seguintes caracteres não são permitidos: `" \ / : | < > * ?`.
- Caracteres de caminho de URL inválidos não permitidos. Pontos de código como `\uE000`, enquanto válidos em nomes de arquivo NTFS, não são caracteres Unicode válidos. Além disso, alguns caracteres ASCII ou Unicode, como caracteres de controle (0x00 a 0x1F, \u0081, etc.), também não são permitidos. Para regras que regem cadeias de caracteres Unicode no HTTP/1.1, consulte [RFC 2616, Seção 2.2: Regras básicas](https://www.ietf.org/rfc/rfc2616.txt) e [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Os seguintes nomes de arquivo não são permitidos: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, caractere de ponto (...) e dois caracteres de ponto (.).
- O número máximo de arquivos por lote é 1500, com um tamanho de lote máximo de 100 GB.
- O número máximo de propriedades ou campos por linha é 10.000.
- O número máximo de lotes que podem ser enviados por usuário, por minuto, é de 138.

### Quais tipos de dados são compatíveis?

Os tipos de dados suportados incluem números inteiros, strings, booleanos, objetos datetime, arrays e objetos.

### Quais formatos de data e hora são compatíveis?

As fontes são compatíveis com uma grande variedade de formatos de data e hora ao assimilar dados. Mais informações sobre formatos datetime compatíveis podem ser encontradas na seção de datas do [guia de manipulação do formato de dados](../data-prep/data-handling.md#dates) na documentação Preparação de dados.

### Como formatar arrays em arquivos CSV, JSON e Parquet?

Arquivos JSON e Parquet são originalmente compatíveis com arrays. Para estruturas planas, como CSVs, as matrizes não são compatíveis. No entanto, cadeias de caracteres com vários valores podem ser divididas em uma matriz, usando funções de preparação de dados, como explodir e unir. Mais informações sobre essas funções de preparação de dados podem ser encontradas no [guia de funções de preparação de dados](../data-prep/functions.md#string)

### Quais fontes suportam a ingestão parcial?

Todas as fontes de ingestão em lote oferecem suporte para ingestão parcial. No entanto, as fontes de assimilação de streaming não suportam assimilação parcial.

### Quando devo usar a ingestão parcial?

A assimilação parcial deve ser usada se você **not** tiver restrições, como ter o arquivo inteiro sendo assimilado na Platform. Como alternativa, a assimilação parcial deve ser usada se você não se importar em assimilar dados que possam conter erros.

### Qual é o limite de erro de ingestão parcial típico?

Não há um &quot;limite de erro típico&quot; para a ingestão parcial. Em vez disso, esse valor pode variar de caso de uso para caso de uso. Por padrão, o limite de erro é definido como 5%.
