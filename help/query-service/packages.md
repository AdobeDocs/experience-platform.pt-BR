---
title: Pacotes do Serviço de Consulta
description: O documento a seguir descreve os pacotes de recursos e produtos disponíveis para o Serviço de query e destaca as diferenças entre consultas ad hoc e em lote.
source-git-commit: 3d2802ff5cdb359b28da23a05d1d6831cc273a52
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 3%

---

# Pacotes do Serviço de query

Este documento descreve os diferentes tipos de empacotamento e recursos de execução de consulta disponíveis no Serviço de query.

O Adobe Experience Platform Query Service pode ser dividido em dois recursos com base nos padrões de consulta que podem ser executados:

- **Consultas ad hoc** são consultas SQL usadas para explorar conjuntos de dados assimilados para verificação, validação, experimentação e assim por diante. Essas consultas não gravam dados de volta no lago de dados da plataforma.
- **Consultas em lote** são queries SQL usados para executar o processamento pós-assimilação de conjuntos de dados assimilados. Essas consultas limpam, modelam, manipulam e enriquecem dados, cujos resultados são gravados de volta no lago de dados da plataforma. Essas consultas podem ser agendadas, gerenciadas e monitoradas como trabalhos em lote.

Os recursos do Serviço de query são empacotados com os seguintes produtos e complementos:

- **Aplicativos baseados em plataforma** (Real-time Customer Data Platform, Customer Journey Analytics e Adobe Journey Optimizer): O acesso do Serviço de query para executar consultas ad hoc é fornecido desde o início com cada variação e nível de aplicativos baseados em plataforma.
- **[!DNL Data Distiller]** (pacote complementar que pode ser comprado com Adobe Real-Time CDP, Customer Journey Analytics e Adobe Journey Optimizer): O acesso do Serviço de query para executar consultas em lote é fornecido com [!DNL Data Distiller].

A tabela a seguir descreve os principais direitos do Serviço de Consulta com base em como são empacotados:

| Direito do Serviço de Consulta | Empacotado com aplicativos baseados em plataforma | Embalado com [!DNL Data Distiller] |
|---|---|---|
| Padrão de consulta suportado | Somente consulta ad hoc | Consulta em lote |
| Caso de uso suportado | <ul><li>&#x200B; de exploração</li><li>&#x200B; de descoberta de dados</li><li>Validação de dados</li><li>Experimentação</li></ul> | <ul><li>Limpeza</li><li>Forma</li><li>Manipulação</li><li>Enriquecimento</li></ul> |
| Semântica suportada | <ul><li>SELECIONAR consultas</li></ul> | <ul><li>Consultas CTAS e ITAS</li></ul> |
| Tempo Máximo de Execução | 10 minutos | 24 horas |
| Métrica de licença | **Consultar simultaneidade do usuário**: <ul><li>1 usuário simultâneo (CDP em tempo real, Adobe Journey Optimizer) &#x200B;</li><li>5 usuários simultâneos (Customer Journey Analytics) &#x200B;</li></ul> **Simultaneidade de Consulta**: <ul><li>1 query de execução simultânea (todos os aplicativos) &#x200B;</li></ul> **Complemento do pacote de usuários ad hoc adicionais** O pode ser comprado para aumentar os direitos de consulta ad hoc autorizados dos clientes. <ul><li>+5 utilizadores simultâneos adicionais por embalagem</li><li>+1 consulta de execução simultânea adicional por pacote</li></ul> | **Computar Horas**: <ul><li>Variável (com base nos direitos de aplicativo do cliente)</li></ul> **Computar Horas** é uma medida do tempo gasto pelo mecanismo do Serviço de Consulta para ler, processar e gravar dados de volta no lago de dados quando uma consulta em lote é executada. |
| Interface de execução de query | <ul><li>Interface do usuário do serviço de query</li><li>Interface do usuário do cliente de terceiros</li><li>[!DNL PostgresSQL] interface do usuário do cliente</li></ul> | <ul><li>interface do usuário do Query </li><li>Interface do usuário do cliente de terceiros</li><li>[!DNL PostgresSQL] interface do usuário do cliente</li><li>REST APIs</li></ul> |
| Resultados da consulta retornados por | Interface do usuário do cliente | Conjunto de dados derivado armazenado no lago de dados |
| Limite do resultado | <ul><li>Interface do usuário do Query - 100 linhas</li><li>Cliente de terceiros - 50.000</li><li>[!DNL PostgresSQL] cliente - 50.000</li></ul> | <ul><li>Interface do usuário do Query (sem limite superior para linhas)</li><li>Clientes de terceiros (sem limite superior para linhas)</li><li>[!DNL PostgresSQL] cliente (sem limite superior para linhas)</li><li>REST APIs (sem limite superior para linhas)</li></ul> |
| Ler capacidade do conjunto de dados | Sim | Sim |
| Capacidade do conjunto de dados de gravação | Não | Sim |
| Capacidade de agendamento | Não | Sim |
| Capacidade de monitoramento | Sim | Sim |
| Capacidade de configuração do alerta de consulta | Não | Sim |

{style=&quot;table-layout:auto&quot;}

## Controle de acesso

O controle de acesso do Experience Platform é administrado por meio do [Adobe Admin Console](https://adminconsole.adobe.com/) em que perfis de produtos vinculam usuários com permissões e sandboxes. Consulte a [visão geral do controle de acesso](../access-control/home.md) para obter mais informações.

Para usar o Serviço de query, a variável [!DNL Manage Queries] deve ser ativada no admin console. Essa permissão permite que os usuários executem consultas ad hoc e em lote. Instruções detalhadas para solicitar acesso ao perfil do produto [!DNL Manage Queries] a permissão foi descrita na seção [gerenciar permissões para um perfil de produto](../access-control/ui/permissions.md) e [gerenciar usuários para um perfil de produto](../access-control/ui/users.md) documentos.

Depois de comprar a [!DNL Data Distiller] complemento, o [!DNL Write Dataset] permissão deve ser concedida. Essa permissão permite [!DNL Data Distiller] para executar consultas em lote.

O quadro seguinte descreve os efeitos da [!DNL Manage Queries] permissão:

| Permissão | Função |
|---|---|
| [!DNL Manage Queries] (sem permissão de gravação de dados) | Fornece acesso para executar consultas ad hoc |
| [!DNL Manage Queries] (com permissão de gravação de dados) | Fornece acesso para executar consultas em lote |

{style=&quot;table-layout:auto&quot;}

## Suporte a sandbox

As sandboxes são partições virtuais em uma única instância do Experience Platform. Cada instância da Platform é compatível com várias sandboxes de produção e não produção, cada uma mantendo sua própria biblioteca de recursos da Platform. As sandboxes de não produção permitem testar recursos, executar experimentos e fazer configurações personalizadas sem afetar as sandboxes de produção. Para obter mais informações sobre sandboxes, consulte o [visão geral das sandboxes](../sandboxes/home.md). Todos os direitos do Serviço de Consulta são compartilhados em todas as sandboxes

## Próximas etapas

Ao ler este documento, você deve ter uma melhor compreensão dos diferentes tipos de empacotamento e recursos de execução de query disponíveis no Serviço de query. Para saber mais sobre o Serviço de query, como casos de uso conhecidos do setor, leia o [documentação do caso de uso](./use-cases/abandoned-browse.md). Para obter informações mais gerais, visite o [Visão geral do Serviço de query](./home.md).
