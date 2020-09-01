---
keywords: Experience Platform;home;popular topics;PSQL;psql;Query service;query service;metadata;commands;metadata commands;
solution: Experience Platform
title: Comandos de metadados
topic: metadata
description: Uma lista de comandos PSQL que são suportados atualmente para consulta de metadados.
translation-type: tm+mt
source-git-commit: c5d3be4706ca6d6a30e203067db6ddc894b9bfb4
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---


# Comandos de metadados

Para metadados em seu conjunto de dados, os seguintes comandos PSQL são suportados atualmente para consulta:

>[!NOTE]
>
>Os comandos listados abaixo fazem distinção entre maiúsculas e minúsculas.

| Comando | Descrição |
|------- | ------------|
| `\conninfo` | Gera informações sobre a conexão de banco de dados atual. |
| `\d` | Exibe uma lista de todas as tabelas visíveis, visualizações, visualizações materializadas, sequências e tabelas estrangeiras. |
| `\dE` | Exibe uma lista de tabelas estrangeiras. |
| `\df or \df+` | Exibe uma lista de funções. |
| `\di` | Exibe uma lista de índices. |
| `\dm` | Exibe uma lista de visualizações materializadas. |
| `\dn` | Exibe uma lista de schemas (namespace). |
| `\ds` | Exibe uma lista de sequências. |
| `\dS` | Exibe uma lista de tabelas definidas pelo PostgreSQL. |
| `\dt` | Exibe uma lista de tabelas. |
| `\dT` | Exibe uma lista de tipos de dados. |
| `\dv` | Exibe uma lista de visualizações. |
| `\encoding` | Lista a codificação do conjunto de caracteres do cliente atual. |
| `\errverbose` | Repete a mensagem de erro mais recente do servidor com a verbosidade máxima. |
| `\l or \list` | Exibe uma lista de bancos de dados no servidor. |
| `\set` | Exibe os nomes e valores de todas as variáveis psql atuais. |
| `\showtables` | Mostra as seguintes informações: <br>name: O nome pelo qual a tabela será referenciada.<br>datasetId: A ID do conjunto de dados que está armazenado.<br>conjunto de dados: O nome do conjunto de dados armazenado.<br>descrição: Uma descrição do conjunto de dados.<br>resolvido: Um valor booliano que indica se o conjunto de dados foi ou não resolvido na sessão atual. |
| `\timing` | Alterna entre ligar e desligar a tela. A exibição é em milissegundos. Intervalos maiores que um segundo são mostrados no formato minutos:segundos, com campos de horas e dias adicionados quando necessário. |

Todos os comandos com os quais o start se  `\d` podem ser combinados. Por exemplo, você pode emitir `\dtsn` para exibir uma lista de todas as tabelas, sequências e schemas. `\d` por si só mostra todas as tabelas visíveis, visualizações, visualizações materializadas e sequências.

Para obter informações adicionais sobre os comandos listados acima, consulte a documentação em [postgresql.org](https://www.postgresql.org/docs/10/app-psql.html). No entanto, lembre-se de que nem todas as opções mostradas na documentação do PostgreSQL são suportadas por [!DNL Experience Platform].

