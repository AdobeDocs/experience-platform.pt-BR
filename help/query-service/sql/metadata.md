---
keywords: Experience Platform, home, tópicos populares, PSQL, psql, serviço de consulta, serviço de consulta, metadados, comandos, comandos de metadados;
solution: Experience Platform
title: Comandos PostgreSQL de Metadados no Serviço de Consulta
topic-legacy: metadata
description: Uma lista de comandos PostgreSQL atualmente compatíveis com a consulta de metadados no Serviço de Consulta do Adobe Experience Platform.
exl-id: bfcbad55-3086-44c9-9938-6ba0504e747b
source-git-commit: 9c450f340706040593dfea5292702c4b00dd9852
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 0%

---

# Metadados [!DNL PostgreSQL] comandos no Serviço de Consulta

Para metadados em seu conjunto de dados, faça o seguinte [!DNL PostgreSQL] comandos são suportados atualmente para consulta:

>[!NOTE]
>
>Os comandos listados abaixo fazem distinção entre maiúsculas e minúsculas.

| Comando | Descrição |
|------- | ------------|
| `\conninfo` | Gera informações sobre a conexão de banco de dados atual. |
| `\d` | Exibe uma lista de todas as tabelas, views, views materializadas, sequências e tabelas estrangeiras visíveis. |
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
| `\encoding` | Lista a codificação atual do conjunto de caracteres do cliente. |
| `\errverbose` | Repete a mensagem de erro do servidor mais recente com a verbosidade máxima. |
| `\l or \list` | Exibe uma lista de bancos de dados no servidor. |
| `\set` | Exibe os nomes e valores de todas as variáveis psql atuais. |
| `\showtables` | Mostra as seguintes informações: <br>name: O nome pelo qual a tabela será referenciada.<br>datasetId: A ID do conjunto de dados que está armazenado.<br>conjunto de dados: O nome do conjunto de dados que está armazenado.<br>descrição: Uma descrição do conjunto de dados.<br>resolvido: Um valor booleano que indica se o conjunto de dados foi ou não resolvido na sessão atual. |
| `\timing` | Alterna a exibição entre ligado e desligado. A exibição é em milissegundos. Intervalos maiores que um segundo são mostrados no formato minutos:segundos, com campos de horas e dias adicionados quando necessário. |

Todos os comandos que começam com `\d` pode ser combinado. Por exemplo, você pode emitir `\dtsn` para exibir uma lista de todas as tabelas, sequências e schemas. `\d` por si só mostra todas as tabelas, views, views materializadas e sequências visíveis.

Para obter informações adicionais sobre os comandos listados acima, consulte a documentação em [postgresql.org](https://www.postgresql.org/docs/10/app-psql.html). No entanto, esteja ciente de que nem todas as opções mostradas no [!DNL PostgreSQL] a documentação é suportada por [!DNL Experience Platform].
