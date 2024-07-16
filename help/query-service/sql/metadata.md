---
keywords: Experience Platform;página inicial;tópicos populares;PSQL;psql;Serviço de consulta;serviço de consulta;metadados;comandos;comandos de metadados;
solution: Experience Platform
title: Comandos PostgreSQL de metadados no serviço de consulta
description: Uma lista de comandos PostgreSQL atualmente compatíveis com a consulta de metadados no Serviço de consulta do Adobe Experience Platform.
exl-id: bfcbad55-3086-44c9-9938-6ba0504e747b
source-git-commit: 58eadaaf461ecd9598f3f508fab0c192cf058916
workflow-type: tm+mt
source-wordcount: '332'
ht-degree: 0%

---

# Comandos de metadados [!DNL PostgreSQL] no Serviço de consulta

Para metadados em seu conjunto de dados, os seguintes comandos [!DNL PostgreSQL] têm suporte para consulta no momento:

>[!NOTE]
>
>Os comandos listados abaixo fazem distinção entre maiúsculas e minúsculas.

| Comando | Descrição |
|------- | ------------|
| `\conninfo` | Gera informações sobre a conexão de banco de dados atual. |
| `\d` | Exibe uma lista de todas as tabelas visíveis, views, views materializadas, sequências e tabelas estrangeiras. |
| `\dE` | Exibe uma lista de tabelas estrangeiras. |
| `\df or \df+` | Exibe uma lista de funções. |
| `\di` | Exibe uma lista de índices. |
| `\dm` | Exibe uma lista de views materializadas. |
| `\dn` | Exibe uma lista de esquemas (namespaces). |
| `\ds` | Exibe uma lista de sequências. |
| `\dS` | Exibe uma lista de tabelas definidas pelo PostgreSQL. |
| `\dt` | Exibe uma lista de tabelas. |
| `\dT` | Exibe uma lista de tipos de dados. |
| `\dv` | Exibe uma lista de exibições. |
| `\encoding` | Lista a codificação do conjunto de caracteres do cliente atual. |
| `\errverbose` | Repete a mensagem de erro de servidor mais recente com o máximo de verbosidade. |
| `\l or \list` | Exibe uma lista de bancos de dados no servidor. |
| `\set` | Exibe os nomes e os valores de todas as variáveis psql atuais. |
| `\showtables` | Mostra as seguintes informações: <br>name: O nome pelo qual a tabela será referenciada.<br>datasetId: a ID do conjunto de dados que está armazenado.<br>conjunto de dados: o nome do conjunto de dados que está armazenado.<br>descrição: uma descrição do conjunto de dados.<br>resolved: um valor booleano que declara se o conjunto de dados é ou não resolvido na sessão atual. |
| `\timing` | Alterna a exibição entre ligada e desligada. A exibição é em milissegundos. Intervalos maiores que um segundo são mostrados no formato minutos:segundos, com campos de horas e dias adicionados quando necessário. |

Todos os comandos que começam com `\d` podem ser combinados. Por exemplo, você pode emitir `\dtsn` para exibir uma lista de todas as tabelas, sequências e esquemas. `\d` por si só mostra todas as tabelas, visualizações, visualizações materializadas e sequências visíveis.

Para obter informações adicionais sobre os comandos listados acima, consulte a documentação em [postgresql.org](https://www.postgresql.org/docs/10/app-psql.html). No entanto, esteja ciente de que nem todas as opções mostradas na documentação do [!DNL PostgreSQL] são suportadas pelo [!DNL Experience Platform].
