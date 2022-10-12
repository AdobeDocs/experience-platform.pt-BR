---
keywords: Experience Platform; query; serviço de consulta; solução de problemas; medidas de proteção; diretrizes; limite;
title: Medidas de proteção para o serviço de consulta
description: Este documento fornece informações sobre limites de uso para dados do Serviço de query para ajudá-lo a otimizar o uso do query.
exl-id: 1ad5dcf4-d048-49ff-97e3-07040392b65b
source-git-commit: e40a9fb0149e194de693a98e5d185860a255b5c4
workflow-type: tm+mt
source-wordcount: '1029'
ht-degree: 4%

---

# Medidas de proteção para o serviço de consulta

As garantias são limites que orientam os dados e o uso do sistema, a otimização do desempenho e a prevenção de erros ou resultados inesperados no Adobe Experience Platform.

Este documento fornece limites de uso padrão para dados do Serviço de query para ajudar você a otimizar o desempenho do sistema ao consultar dados em relação aos direitos de licenciamento.

## Pré-requisitos

Antes de continuar com este documento, você deve ter uma boa compreensão das principais definições e recursos do Serviço de query. Elas estão descritas abaixo:

* **Consultas ad hoc**: Para execução `SELECT` consultas para explorar, experimentar e validar dados, onde os resultados das consultas **não são armazenadas** no lago de dados.

* **Consultas em lote**: Para execução `INSERT TABLE AS SELECT` e `CREATE TABLE AS SELECT` consultas para limpar, moldar, manipular e enriquecer dados. Os resultados desses queries **são armazenadas** no lago de dados. A métrica para medir o consumo dessa funcionalidade são horas computacionais.

* **Usuários do Serviço de query**: Os usuários do Serviço de query fornecidos em sua licença atual para Customer Journey Analytics, Adobe Real-time Customer Data Platform e/ou Adobe Journey Optimizer também podem ser usados com o Data Distiller. Os usuários do Serviço de query são compartilhados entre os recursos.

* **Usuários ad hoc**: Usuários ad hoc são aqueles que executam consultas ad hoc.

* **Usuários em lote**: Os usuários em lote são aqueles que executam consultas em lote.

* **API de relatórios**: Uma API para fazer chamadas de busca de dados (interna ou externamente). Modelos de dados de relatório estendido são derivados de modelos de dados de relatório nativos no Adobe Experience Platform, como o modelo de dados de painéis do Real-Time CDP.

A ilustração abaixo resume como os recursos do Serviço de query estão atualmente empacotados e licenciados:

![Um diagrama para explicar a distribuição e o empacotamento dos recursos do Serviço de query em relação ao licenciamento.](./images/guardrails/query-capabilities.png)

## Tipos de limite

Existem dois tipos de limites padrão neste documento:

* **Limite suave**: Você pode ir além de um limite suave, no entanto, os limites suaves fornecem uma diretriz recomendada para o desempenho do sistema.

* **Limite rígido**: Um limite rígido fornece um máximo absoluto.

>[!NOTE]
>
>Os limites padrão descritos neste documento estão sendo constantemente melhorados. Verifique regularmente se há atualizações.

## Medidas de proteção de desempenho da entidade primária

As tabelas abaixo fornecem os limites de garantia e as descrições recomendadas para a execução da consulta ao usar um padrão de consulta específico.

**Consultas ad hoc**

| Grade de Proteção | Limite | Tipo de limite | Descrição |
|---|---|---|---|
| Tempo máximo de execução | 10 minutos | Grave | Isso define o tempo máximo de saída para uma consulta SQL ad-hoc. Exceder o limite de tempo para retornar um resultado aciona o código de erro 53400. |
| Usuários simultâneos do Serviço de query | <ul><li>Conforme especificado na descrição do produto do aplicativo.</li><li>+5 (com cada pacote adicional de usuários de consulta ad hoc comprado)</li></ul> | Grave | Isso define quantos usuários podem criar sessões simultaneamente para uma determinada organização. Se o limite de simultaneidade for excedido, o usuário receberá uma `Session Limit Reached` erro. |
| Simultaneidade de query | <ul><li>Conforme especificado na descrição do produto do aplicativo.</li><li>+1 (com cada pacote de SKU adicional de usuário Ad hoc comprado)</li></ul> | Grave | Isso define quantas consultas podem ser executadas simultaneamente para uma determinada organização. Se o limite de simultaneidade for excedido, as consultas serão enfileiradas. |
| Limite de saída do conector e do resultado do cliente | Conector do cliente<ul><li>Interface do usuário do Query (100 linhas)</li><li>Cliente de terceiros (50.000)</li><li>[!DNL PostgresSQL] cliente (50.000)</li></ul> | Grave | O resultado de um query pode ser recebido por meio dos seguintes meios:<ul><li>Interface do usuário do serviço de query</li><li>Cliente de terceiros</li><li>[!DNL PostgresSQL] cliente</li></ul>Observação: Adicionar uma limitação à contagem de saída pode retornar resultados mais rapidamente. Por exemplo, `LIMIT 5`, `LIMIT 10`, e assim por diante. |
| Resultados retornados por | Interface do usuário do cliente | N/D | Isso define como os resultados são disponibilizados para os usuários. |

{style=&quot;table-layout:auto&quot;}

**Consultas em lote**

| **Grade de Proteção** | **Limite** | **Tipo de limite** | **Descrição** |
|---|---|---|---|
| Tempo máximo de execução | 24 horas | Grave | Isso define o tempo máximo de execução de uma consulta SQL em lote.<br>O tempo de processamento de um query depende do volume de dados a serem processados e da complexidade da consulta. |
| Usuários do Serviço de Consulta Simultâneo para Lote Não Agendado | <ul><li>Conforme especificado na descrição do produto do aplicativo.</li><li>+5 (com cada pacote adicional de usuários de consulta ad hoc comprado)</li></ul> | Grave | Para consultas em lote não agendadas (por exemplo, consultas CTAS/ITAS no modo interativo), isso define quantos usuários podem criar sessões simultaneamente para uma determinada organização. Se o limite de simultaneidade for excedido, o usuário receberá uma `Session Limit Reached` erro. |
| Usuários do Serviço de Consulta Simultâneo para Lote Agendado | Sem limitação de usuário | N/D | As consultas agendadas em lote são trabalhos assíncronos, portanto, não há limitação de usuário. |
| Horas computacionais para processamento de dados em lote | Conforme especificado na ordem de vendas do SKU personalizado da Consulta de Inteligência Adobe Experience Platform do Cliente | Suave | Isso define o escopo do tempo computacional por ano em que um cliente tem permissão para executar consultas em lote para digitalizar, processar e gravar dados de volta no lago de dados. |
| Simultaneidade de query | Suportado | N/D | As consultas agendadas em lote são trabalhos assíncronos, portanto, as consultas simultâneas são suportadas. |
| Limite de saída do conector do cliente e do resultado | Conector do cliente<ul><li>Interface do usuário do Query (sem limite superior para linhas)</li><li>Cliente de terceiros (sem limite superior para linhas)</li><li>[!DNL PostgresSQL] cliente (sem limite superior para linhas)</li><li>REST APIs (sem limite superior para linhas)</li></ul> | Grave | O resultado de um query pode ser disponibilizado usando os seguintes métodos:<ul><li>Pode ser armazenado como conjuntos de dados derivados</li><li>Pode ser inserido nos conjuntos de dados derivados existentes</li></ul>Observação: Não há limite superior para o número de contagem de registros do resultado da consulta. |
| Resultados retornados por | Conjunto de dados | N/D | Isso define como os resultados são disponibilizados para os usuários. |

{style=&quot;table-layout:auto&quot;}

## Armazenamento acelerado de consulta {#query-accelerated-store}

A tabela abaixo fornece os limites de garantia e a descrição recomendados para o armazenamento acelerado de query.

| Grade de Proteção | Limite | Tipo de limite | Descrição |
|---|---|---|---|
| Simultaneidade de query | 4 | Grave | Para garantir que as consultas sobre dados agregados por meio da API de relatórios (incluindo consultas que aprimoram modelos de dados, como os modelos de dados da CDP em tempo real) tenham os recursos para serem executadas com eficiência, a API de relatórios rastreia a utilização de recursos atribuindo slots de simultaneidade a cada query. O sistema coloca consultas em uma fila e aguarda até que os slots de simultaneidade fiquem disponíveis ou possam ser enviados do cache. No máximo quatro slots de query simultâneos estão disponíveis em um determinado momento.<br>Se você acessar a API de relatórios por meio de uma ferramenta de BI e precisar de mais simultaneidade, será necessário um servidor de BI. |

{style=&quot;table-layout:auto&quot;}

## Próximas etapas

Após a leitura deste documento, você deve ter uma melhor compreensão dos limites padrão para execução de query com os padrões de query disponíveis.

Consulte a documentação a seguir para obter mais informações sobre o Serviço de query:

* [API do serviço de consulta](./api/getting-started.md)
* [Interface do usuário do serviço de query](./ui/overview.md)
