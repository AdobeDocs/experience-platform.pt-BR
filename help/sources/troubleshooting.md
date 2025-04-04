---
keywords: Experience Platform;página inicial;tópicos populares;fontes;assimilação;solução de problemas;solução de problemas de fontes;perguntas frequentes de fontes;conectores de origem;conectores de origem perguntas frequentes;solução de problemas de conectores de origem;
solution: Experience Platform
title: Solução de problemas de origens
description: Este documento fornece respostas a perguntas frequentes sobre fontes no Adobe Experience Platform.
exl-id: 94875121-7d4d-4eb2-8760-aa795933dd7e
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '749'
ht-degree: 0%

---

# Guia de solução de problemas de origens

Este documento fornece respostas a perguntas frequentes sobre fontes no Adobe Experience Platform. Para perguntas e soluções de problemas relacionadas a outros serviços do [!DNL Experience Platform], incluindo aquelas encontradas em todas as APIs do [!DNL Experience Platform], consulte o [guia de solução de problemas do Experience Platform](../landing/troubleshooting.md).

## Perguntas frequentes

Veja a seguir uma lista de respostas para perguntas frequentes sobre fontes.

### Preciso fazer alterações em nossas configurações de segurança de rede para habilitar as fontes?

Talvez seja necessário incluir na lista de permissões determinados endereços IP para ativar as fontes. Para obter mais informações, leia a documentação no seu conector de origem específico.

### Que tipos de autenticação são aceitos pelas fontes?

As fontes podem ser autenticadas usando sequências de conexão, nomes de usuário e senhas ou tokens e chaves de acesso. Detalhes específicos sobre os tipos de autenticação compatíveis podem ser encontrados na documentação do conector de origem especificado.

### Por que todas as minhas execuções de fluxo recentes estão falhando?

Se você estiver observando que todas as execuções de fluxo recentes estão falhando, suas credenciais podem ter sido alteradas ou expiradas. Para corrigir esse problema, tente atualizar sua conexão com as credenciais mais recentes.

### Que tipos de arquivos são aceitos?

Atualmente, os tipos de arquivos compatíveis são arquivos delimitados, JSON e Parquet.

### Quais são as restrições em nomes e tamanhos de arquivo?

Veja a seguir uma lista de restrições que você deve considerar para os arquivos nas origens.

- Os nomes dos componentes de diretório e arquivo não podem exceder 255 caracteres.
- Nomes de diretório e arquivo não podem terminar com uma barra (`/`). Se fornecido, ele será removido automaticamente.
- Os seguintes caracteres de URL reservados devem ter um escape adequado: `! ' ( ) ; @ & = + $ , % # [ ]`
- Os seguintes caracteres não são permitidos: `" \ / : | < > * ?`.
- Caracteres de caminho de URL inválidos não permitidos. Pontos de código como `\uE000`, embora válidos em nomes de arquivo NTFS, não são caracteres Unicode válidos. Além disso, alguns caracteres ASCII ou Unicode, como caracteres de controle (0x00 a 0x1F, \u0081 etc.), também não são permitidos. Para regras que regem cadeias de caracteres Unicode em HTTP/1.1, consulte [RFC 2616, Seção 2.2: Regras Básicas](https://www.ietf.org/rfc/rfc2616.txt) e [RFC 3987](https://www.ietf.org/rfc/rfc3987.txt).
- Os seguintes nomes de arquivo não são permitidos: LPT1, LPT2, LPT3, LPT4, LPT5, LPT6, LPT7, LPT8, LPT9, COM1, COM2, COM3, COM4, COM5, COM6, COM7, COM8, COM9, PRN, AUX, NUL, CON, CLOCK$, caractere de ponto (.) e dois caracteres de ponto (..).
- O número máximo de arquivos por lote é 1500, com um tamanho máximo de lote de 100 GB.
- O número máximo de propriedades ou campos por linha é 10.000.
- O número máximo de lotes que podem ser enviados por usuário por minuto é 2000.

### Que tipos de dados são aceitos?

Os tipos de dados compatíveis incluem inteiros, strings, booleanos, objetos datetime, matrizes e objetos.

### Quais formatos de data e hora são compatíveis?

As fontes oferecem suporte a uma grande variedade de formatos de data e hora ao assimilar dados. Mais informações sobre formatos de data e hora com suporte podem ser encontradas na seção de datas do [guia de manipulação de formato de dados](../data-prep/data-handling.md#dates) na documentação de Preparo de Dados.

### Como formatar matrizes em arquivos CSV, JSON e Parquet?

Os arquivos JSON e Parquet suportam arrays nativamente. Para estruturas simples, como CSVs, matrizes não são compatíveis. No entanto, cadeias de caracteres com vários valores podem ser divididas em uma matriz, usando funções de preparação de dados, como explodir e unir. Mais informações sobre estas funções de preparação de dados podem ser encontradas no [guia de funções de preparação de dados](../data-prep/functions.md#string)

### Quais fontes oferecem suporte à assimilação parcial?

Todas as fontes de assimilação em lote oferecem suporte à assimilação parcial. No entanto, as fontes de assimilação por transmissão não oferecem suporte à assimilação parcial.

### Quando devo usar a assimilação parcial?

A assimilação parcial deve ser usada se você **não** tiver restrições, como ter o arquivo inteiro sendo assimilado na Experience Platform. Como alternativa, a assimilação parcial deve ser usada se você não se importar em assimilar dados que possam conter erros dentro dela.

### Qual é o limite típico de erro de assimilação parcial?

Não há &quot;limite de erro típico&quot; para assimilação parcial. Em vez disso, esse valor pode variar de caso de uso para caso de uso. Por padrão, o limite de erro é definido como 5%.

### Quanto tempo leva para um status de execução de fluxo ser atualizado após a criação de um novo fluxo de dados?

As execuções de fluxo não são geradas instantaneamente e podem levar de dois a três minutos para serem atualizadas após sua `startTime` designada. A verificação do status de uma execução de fluxo, imediatamente após a criação de um novo fluxo de dados, não retorna informações sobre a execução de fluxo `lastRunDetails`, pois isso ainda não aconteceu. É recomendável permitir que o fluxo de dados tenha alguns minutos para ser gerado antes de verificar o status da execução do fluxo.