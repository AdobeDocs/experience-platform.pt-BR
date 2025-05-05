---
keywords: Experience Platform;consulta;serviço de consulta;solução de problemas;medidas de proteção;diretrizes;limite;
title: Medidas de proteção do serviço de consulta
description: Este documento fornece informações sobre limites de uso para dados do Serviço de consulta para ajudar você a otimizar o uso da consulta.
exl-id: 1ad5dcf4-d048-49ff-97e3-07040392b65b
source-git-commit: 23c7a4590b365a49edb066567b6ebe2ac08c67e8
workflow-type: tm+mt
source-wordcount: '1168'
ht-degree: 2%

---

# Medidas de proteção do serviço de consulta

As garantias são limites que orientam o uso do sistema e dos dados, a otimização do desempenho e a prevenção de erros ou resultados inesperados no Adobe Experience Platform.
Este documento fornece limites de uso padrão para dados do Serviço de consulta para ajudar você a otimizar o desempenho do sistema ao consultar dados em relação aos seus direitos de licença.

>[!IMPORTANT]
>
>Verifique os direitos de licença em seu Pedido de Venda e a [Descrição do Produto](https://helpx.adobe.com/br/legal/product-descriptions.html?lang=pt-BR) correspondente sobre os limites de uso reais, além desta página de medidas de proteção.

## Pré-requisitos

Antes de continuar com este documento, você deve ter uma boa compreensão das principais definições e recursos do Serviço de consulta. Elas são descritas abaixo:

* **Consultas ad hoc**: Para executar `SELECT` consultas para explorar, testar e validar dados em que os resultados das consultas **não estão armazenados** no data lake.

* **Consultas em lote**: para executar consultas `INSERT TABLE AS SELECT` e `CREATE TABLE AS SELECT` para limpar, formatar, manipular e enriquecer dados. Os resultados destas consultas **são armazenados** no data lake. A métrica para medir o consumo dessa funcionalidade é a de horas computacionais.

* **Usuários do Serviço de Consulta**: os usuários do Serviço de Consulta fornecidos em sua licença atual para Customer Journey Analytics, Adobe Real-Time Customer Data Platform e/ou Adobe Journey Optimizer também podem ser usados com o Data Distiller. Os usuários do Serviço de consulta são compartilhados entre os recursos.

* **Usuários ad hoc**: os usuários ad hoc são aqueles que executam consultas ad hoc.

* **Usuários em lote**: são os usuários em lote que executam consultas em lote.

* **API de relatórios**: uma API para fazer chamadas de busca de dados (interna ou externamente). Os modelos de dados de relatórios estendidos são derivados dos modelos de dados de relatórios nativos no Adobe Experience Platform, como o modelo de dados dos painéis do Real-Time CDP.

## Tipos de grade de proteção

Há dois tipos de limites padrão neste documento:

| Tipo de grade de proteção | Descrição |
|----------|---------|
| **Proteção de desempenho (limite flexível)** | As medidas de proteção de desempenho são limites de uso relacionados ao escopo dos seus casos de uso. Ao exceder as medidas de proteção de desempenho, você pode enfrentar degradação e latência do desempenho. A Adobe não é responsável por essa degradação de desempenho. Os clientes que excederem consistentemente uma garantia de desempenho podem optar por licenciar capacidade adicional para evitar a degradação do desempenho. |
| **Medidas de proteção aplicadas pelo sistema (Limite rígido)** | As medidas de proteção aplicadas pelo sistema são aplicadas pela interface do usuário ou API do Real-Time CDP. Esses são limites que você não pode exceder, pois a interface do usuário e a API o bloquearão de fazer isso ou retornarão um erro. |

{style="table-layout:auto"}

>[!NOTE]
>
>Os limites padrão descritos neste documento estão sendo constantemente aprimorados. Verifique regularmente se há atualizações.

## Medidas de proteção de desempenho da entidade principal

As tabelas abaixo fornecem os limites de proteção e descrições recomendados para execução de consulta ao usar um padrão de consulta específico.

**Consultas ad hoc**

| Grade de Proteção | Limite | Tipo de limite | Descrição |
|---|---|---|---|
| Tempo máximo de execução | 10 minutos | Proteção imposta pelo sistema | Isso define o tempo máximo de saída para uma consulta SQL ad-hoc. Exceder o limite de tempo para retornar um resultado aciona o código de erro 53400. |
| Usuários do Serviço de consulta simultâneo | <ul><li>Conforme especificado na descrição do produto do aplicativo.</li><li>+5 (com cada pacote complementar de usuários de query ad hoc adicional adquirido)</li></ul> | Proteção imposta pelo sistema | Isso define quantos usuários podem criar sessões simultaneamente para uma organização específica. Se o limite de simultaneidade for excedido, o usuário receberá um erro `Session Limit Reached`. |
| Consultar simultaneidade | <ul><li>Conforme especificado na descrição do produto do aplicativo.</li><li>+1 (com cada pacote SKU suplementar de usuário de consulta ad hoc adicional adquirido)</li></ul> | Proteção imposta pelo sistema | Isso define quantas consultas podem ser executadas simultaneamente para uma organização específica. Se o limite de simultaneidade for excedido, as consultas serão enfileiradas. |
| Conector do cliente e limite de saída de resultados | Conector do cliente<ul><li>Interface do usuário de consulta (100 linhas)</li><li>Cliente de terceiros (50.000)</li><li>Cliente [!DNL PostgresSQL] (50.000)</li></ul> | Proteção imposta pelo sistema | O resultado de um query pode ser recebido pelos seguintes meios:<ul><li>Interface do usuário do serviço de consulta</li><li>Cliente de terceiros</li><li>cliente [!DNL PostgresSQL]</li></ul>Observação: adicionar uma limitação à contagem de saída pode retornar resultados mais rapidamente. Por exemplo, `LIMIT 5`, `LIMIT 10`, e assim por diante. |
| Resultados retornados via | Interface do cliente | N/D | Isso define como os resultados são disponibilizados aos usuários. |

{style="table-layout:auto"}

**Consultas em lote**

| **Grade de Proteção** | **Limite** | **Tipo de limite** | **Descrição** |
|---|---|---|---|
| Tempo máximo de execução | 24 horas | Proteção imposta pelo sistema | Isso define o tempo máximo de execução para uma consulta SQL em lote.<br>O tempo de processamento de uma consulta depende do volume de dados a serem processados e da complexidade da consulta. |
| Usuários do Serviço de Consulta Concorrente para Lote Não Programado | <ul><li>Conforme especificado na descrição do produto do aplicativo.</li><li>+5 (com cada pacote complementar de usuários de query ad hoc adicional adquirido)</li></ul> | Proteção imposta pelo sistema | Para consultas em lote não agendadas (por exemplo, consultas CTAS/ITAS no modo interativo), isso define quantos usuários podem criar sessões simultaneamente para uma organização específica. Se o limite de simultaneidade for excedido, o usuário receberá um erro `Session Limit Reached`. |
| Usuários do Serviço de Consulta Simultâneos para um Lote agendado | Sem limitação de usuário | N/D | As consultas em lote agendadas são trabalhos assíncronos, portanto, não há limitação de usuário. |
| Horas computacionais para processamento de dados em lote | Conforme especificado na Ordem de venda de SKU personalizada de Consulta de Adobe Experience Platform Intelligence do Cliente | Proteção de desempenho | Isso define a quantidade de tempo computacional por ano que um cliente tem permissão para executar consultas em lote para digitalizar, processar e gravar dados de volta no data lake. |
| Consultar simultaneidade | Suportado | N/D | As consultas em lote agendadas são trabalhos assíncronos, portanto, as consultas simultâneas são compatíveis. |
| Conector do cliente e limite de saída do resultado | Conector do cliente<ul><li>Interface do usuário de consulta (sem limite superior para linhas)</li><li>Cliente de terceiros (sem limite superior para linhas)</li><li>Cliente [!DNL PostgresSQL] (sem limite superior para linhas)</li><li>REST APIs (sem limite superior para linhas)</li></ul> | Proteção imposta pelo sistema | O resultado de um query pode ser disponibilizado usando os seguintes métodos:<ul><li>Pode ser armazenado como conjuntos de dados derivados</li><li>Pode ser inserido nos conjuntos de dados derivados existentes</li></ul>Observação: não há limite superior para o número de contagem de registros no resultado da consulta. |
| Resultados retornados via | Conjunto de dados | N/D | Isso define como os resultados são disponibilizados aos usuários. |

{style="table-layout:auto"}

## Consultar armazenamento acelerado {#query-accelerated-store}

A tabela abaixo fornece os limites de garantia recomendados e a descrição do armazenamento acelerado da consulta.

| Grade de Proteção | Limite | Tipo de limite | Descrição |
|---|---|---|---|
| Consultar simultaneidade | 4 | Proteção imposta pelo sistema | Para garantir que as consultas em dados agregados por meio da API de relatórios (incluindo consultas que aprimoram modelos de dados, como os modelos de dados do Real-Time CDP) tenham os recursos para serem executados com eficiência, a API de relatórios rastreia a utilização de recursos atribuindo slots de simultaneidade a cada consulta. O sistema coloca as consultas em uma fila e aguarda até que os slots de simultaneidade fiquem disponíveis ou possam ser atendidos do cache. Um máximo de quatro slots de consulta simultâneos estão disponíveis a qualquer momento.<br>Se você acessar a API de relatórios por meio de uma ferramenta de BI e precisar de mais simultaneidade, será necessário um servidor de BI. |

{style="table-layout:auto"}

## Próximas etapas

Depois de ler este documento, você terá uma melhor compreensão dos limites padrão para execução de consulta com os padrões de consulta disponíveis.

Consulte a documentação a seguir para obter mais informações sobre o Serviço de consulta:

* [API do serviço de consulta](./api/getting-started.md)
* [Interface do usuário do serviço de consulta](./ui/overview.md)

Consulte a documentação a seguir para obter mais informações sobre outras medidas de proteção dos serviços da Experience Platform, informações de latência de ponta a ponta e informações de licenciamento dos documentos Descrição do produto da Real-Time CDP:

* [Medidas de proteção do Real-Time CDP](/help/rtcdp/guardrails/overview.md)
* [Diagramas de latência de ponta a ponta](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/deployment/guardrails.html?lang=pt-BR#end-to-end-latency-diagrams) para vários serviços da Experience Platform.
* [Real-Time Customer Data Platform (B2C Edition - Pacotes do Prime e Ultimate)](https://helpx.adobe.com/br/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html)
* [Real-Time Customer Data Platform (B2P - Pacotes do Prime e Ultimate)](https://helpx.adobe.com/br/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html)
* [Real-Time Customer Data Platform (B2B - Pacotes do Prime e Ultimate)](https://helpx.adobe.com/br/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html)