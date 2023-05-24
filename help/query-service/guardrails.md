---
keywords: Experience Platform;consulta;serviço de consulta;solução de problemas;medidas de proteção;diretrizes;limite;
title: Medidas de proteção do serviço de consulta
description: Este documento fornece informações sobre limites de uso para dados do Serviço de consulta para ajudar você a otimizar o uso da consulta.
exl-id: 1ad5dcf4-d048-49ff-97e3-07040392b65b
source-git-commit: 5ceb261dbf1cac58d0cfe620875b8fa7c761abf2
workflow-type: tm+mt
source-wordcount: '1004'
ht-degree: 3%

---

# Medidas de proteção do serviço de consulta

As garantias são limites que orientam o uso do sistema e dos dados, a otimização do desempenho e a prevenção de erros ou resultados inesperados no Adobe Experience Platform.

Este documento fornece limites de uso padrão para dados do Serviço de consulta para ajudar você a otimizar o desempenho do sistema ao consultar dados em relação aos seus direitos de licença.

## Pré-requisitos

Antes de continuar com este documento, você deve ter uma boa compreensão das principais definições e recursos do Serviço de consulta. Elas são descritas abaixo:

* **Consultas ad hoc**: Para execução `SELECT` consultas para explorar, testar e validar dados em que os resultados das consultas **não estão armazenados** no data lake.

* **Consultas em lote**: Para execução `INSERT TABLE AS SELECT` e `CREATE TABLE AS SELECT` consultas para limpar, moldar, manipular e enriquecer dados. Os resultados dessas consultas **são armazenados** no data lake. A métrica para medir o consumo dessa funcionalidade é a de horas computacionais.

* **Usuários do Serviço de consulta**: os usuários do Serviço de consulta fornecidos em sua licença atual para Customer Journey Analytics, Adobe Real-time Customer Data Platform e/ou Adobe Journey Optimizer também podem ser usados com o Data Distiller. Os usuários do Serviço de consulta são compartilhados entre os recursos.

* **Usuários ad hoc**: Os usuários ad hoc são aqueles que executam consultas ad hoc.

* **Usuários em lote**: usuários em lote são aqueles que executam consultas em lote.

* **API de relatórios**: uma API para fazer chamadas de busca de dados (interna ou externamente). Os modelos de dados de relatórios estendidos são derivados dos modelos de dados de relatórios nativos no Adobe Experience Platform, como o modelo de dados dos painéis do Real-Time CDP.

A ilustração abaixo resume como os recursos do Serviço de consulta são atualmente empacotados e licenciados:

## Tipos de limite

Há dois tipos de limites padrão neste documento:

* **Limite flexível**: Você pode ir além de um limite flexível, no entanto, os limites flexíveis fornecem uma diretriz recomendada para o desempenho do sistema.

* **Limite rígido**: um limite rígido fornece um máximo absoluto.

>[!NOTE]
>
>Os limites padrão descritos neste documento estão sendo constantemente aprimorados. Verifique regularmente se há atualizações.

## Medidas de proteção de desempenho da entidade principal

As tabelas abaixo fornecem os limites de proteção e descrições recomendados para execução de consulta ao usar um padrão de consulta específico.

**Consultas ad hoc**

| Grade de Proteção | Limite | Tipo de limite | Descrição |
|---|---|---|---|
| Tempo máximo de execução | 10 minutos | Grave | Isso define o tempo máximo de saída para uma consulta SQL ad-hoc. Exceder o limite de tempo para retornar um resultado aciona o código de erro 53400. |
| Usuários do Serviço de consulta simultâneo | <ul><li>Conforme especificado na descrição do produto do aplicativo.</li><li>+5 (com cada pacote complementar de usuários de query ad hoc adicional adquirido)</li></ul> | Grave | Isso define quantos usuários podem criar sessões simultaneamente para uma organização específica. Se o limite de simultaneidade for excedido, o usuário receberá uma `Session Limit Reached` erro. |
| Consultar simultaneidade | <ul><li>Conforme especificado na descrição do produto do aplicativo.</li><li>+1 (com cada pacote SKU suplementar de usuário de consulta ad hoc adicional adquirido)</li></ul> | Grave | Isso define quantas consultas podem ser executadas simultaneamente para uma organização específica. Se o limite de simultaneidade for excedido, as consultas serão enfileiradas. |
| Conector do cliente e limite de saída de resultados | Conector do cliente<ul><li>Interface do usuário de consulta (100 linhas)</li><li>Cliente de terceiros (50.000)</li><li>[!DNL PostgresSQL] cliente (50.000)</li></ul> | Grave | O resultado de um query pode ser recebido pelos seguintes meios:<ul><li>Interface do usuário do serviço de consulta</li><li>Cliente de terceiros</li><li>[!DNL PostgresSQL] cliente</li></ul>Observação: adicionar uma limitação à contagem de saída pode retornar resultados mais rapidamente. Por exemplo, `LIMIT 5`, `LIMIT 10`, e assim por diante. |
| Resultados retornados via | Interface do cliente | N/D | Isso define como os resultados são disponibilizados aos usuários. |

{style="table-layout:auto"}

**Consultas em lote**

| **Grade de Proteção** | **Limite** | **Tipo de limite** | **Descrição** |
|---|---|---|---|
| Tempo máximo de execução | 24 horas | Grave | Isso define o tempo máximo de execução para uma consulta SQL em lote.<br>O tempo de processamento de um query depende do volume de dados a serem processados e da complexidade do query. |
| Usuários do Serviço de Consulta Concorrente para Lote Não Programado | <ul><li>Conforme especificado na descrição do produto do aplicativo.</li><li>+5 (com cada pacote complementar de usuários de query ad hoc adicional adquirido)</li></ul> | Grave | Para consultas em lote não agendadas (por exemplo, consultas CTAS/ITAS no modo interativo), isso define quantos usuários podem criar sessões simultaneamente para uma organização específica. Se o limite de simultaneidade for excedido, o usuário receberá uma `Session Limit Reached` erro. |
| Usuários do Serviço de Consulta Simultâneos para um Lote agendado | Sem limitação de usuário | N/D | As consultas em lote agendadas são trabalhos assíncronos, portanto, não há limitação de usuário. |
| Horas computacionais para processamento de dados em lote | Conforme especificado na Ordem de venda de SKU personalizada de Consulta de Adobe Experience Platform Intelligence do Cliente | Suave | Isso define a quantidade de tempo computacional por ano que um cliente tem permissão para executar consultas em lote para digitalizar, processar e gravar dados de volta no data lake. |
| Consultar simultaneidade | Suportado | N/D | As consultas em lote agendadas são trabalhos assíncronos, portanto, as consultas simultâneas são compatíveis. |
| Conector do cliente e limite de saída do resultado | Conector do cliente<ul><li>Interface do usuário de consulta (sem limite superior para linhas)</li><li>Cliente de terceiros (sem limite superior para linhas)</li><li>[!DNL PostgresSQL] cliente (sem limite superior para linhas)</li><li>REST APIs (sem limite superior para linhas)</li></ul> | Grave | O resultado de um query pode ser disponibilizado usando os seguintes métodos:<ul><li>Pode ser armazenado como conjuntos de dados derivados</li><li>Pode ser inserido nos conjuntos de dados derivados existentes</li></ul>Observação: não há limite superior para o número de contagem de registros no resultado da consulta. |
| Resultados retornados via | Conjunto de dados | N/D | Isso define como os resultados são disponibilizados aos usuários. |

{style="table-layout:auto"}

## Consultar armazenamento acelerado {#query-accelerated-store}

A tabela abaixo fornece os limites de garantia recomendados e a descrição do armazenamento acelerado da consulta.

| Grade de Proteção | Limite | Tipo de limite | Descrição |
|---|---|---|---|
| Consultar simultaneidade | 4 | Grave | Para garantir que as consultas em dados agregados por meio da API de relatórios (incluindo consultas que aprimoram modelos de dados, como os modelos de dados do Real-Time CDP) tenham os recursos para serem executados com eficiência, a API de relatórios rastreia a utilização de recursos atribuindo slots de simultaneidade a cada consulta. O sistema coloca as consultas em uma fila e aguarda até que os slots de simultaneidade fiquem disponíveis ou possam ser atendidos do cache. Um máximo de quatro slots de consulta simultâneos estão disponíveis a qualquer momento.<br>Se você acessar a API de relatórios por meio de uma ferramenta de BI e precisar de mais simultaneidade, será necessário um servidor de BI. |

{style="table-layout:auto"}

## Próximas etapas

Depois de ler este documento, você terá uma melhor compreensão dos limites padrão para execução de consulta com os padrões de consulta disponíveis.

Consulte a documentação a seguir para obter mais informações sobre o Serviço de consulta:

* [API do serviço de consulta](./api/getting-started.md)
* [Interface do usuário do serviço de consulta](./ui/overview.md)
